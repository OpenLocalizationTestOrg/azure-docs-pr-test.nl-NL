---
title: een Azure Resource Manager-sjabloon in een Azure Automation-runbook aaaDeploy | Microsoft Docs
description: Hoe toodeploy een Azure Resource Manager-sjabloon opgeslagen in Azure Storage vanuit een runbook
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Een Azure Resource Manager-sjabloon in een Azure Automation PowerShell-runbook implementeren

U kunt schrijven een [PowerShell voor Azure Automation-runbook](automation-first-runbook-textual-powershell.md) die een Azure-resource implementeert met behulp van een [Azure Resource Management-sjabloon](../azure-resource-manager/resource-manager-create-first-template.md).

Op deze manier kunt u de implementatie van Azure-resources te automatiseren. U kunt uw Resource Manager-sjablonen in een beveiligde centrale locatie zoals Azure Storage onderhouden.

In dit onderwerp, maken we een PowerShell-runbook die gebruikmaakt van een Resource Manager-sjabloon die is opgeslagen in [Azure Storage](../storage/common/storage-introduction.md) toodeploy een nieuw Azure-opslagaccount.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, moet u hello te volgen:

* Azure-abonnement. Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).
* [Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.  Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.
* [Azure Storage-account](../storage/common/storage-create-storage-account.md) in welke toostore Hallo Resource Manager-sjabloon
* Azure Powershell installeren op een lokale machine. Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het tooget Azure PowerShell.

## <a name="create-hello-resource-manager-template"></a>Hallo Resource Manager-sjabloon maken

In dit voorbeeld gebruiken we een Resource Manager-sjabloon die u een nieuwe Azure Storage-account implementeert.

Kopieer in een teksteditor Hallo volgende tekst:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

Hallo bestand opslaan lokaal als `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Hallo Resource Manager-sjabloon opslaan in Azure Storage

Nu gebruik van PowerShell toocreate een Azure Storage-bestandsshare en Hallo uploaden `TemplateTest.json` bestand.
Zie voor instructies over hoe een bestand toocreate delen en uploaden van een bestand in hello Azure-portal, [aan de slag met Azure File storage in Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Start PowerShell op uw lokale machine en Voer Hallo opdrachten toocreate een bestandsshare te volgen en upload Hallo Resource Manager-sjabloon toothat-bestandsshare.

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>Hallo PowerShell-script voor runbook maken

Nu we maken een PowerShell-script dat Hallo opgehaald `TemplateTest.json` bestand van Azure Storage en implementeert Hallo sjabloon toocreate een nieuw Azure-opslagaccount.

In een teksteditor plakken Hallo volgende tekst:

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Hallo bestand opslaan lokaal als `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importeren en Hallo runbook publiceren in Azure Automation-account

Nu we PowerShell tooimport hello runbook gebruiken in uw Azure Automation-account en vervolgens publiceren Hallo runbook.
Voor informatie over het tooimport en een runbook publiceren in hello Azure-portal, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` uitvoeren in uw Automation-account als een PowerShell-runbook Hallo volgende PowerShell-opdrachten:

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>Hallo runbook starten

Nu we Hallo runbook door de aanroepende Hallo starten [Start AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.

Voor informatie over hoe toostart een runbook in Azure-portal Hallo zien [een runbook starten in Azure Automation](automation-starting-a-runbook.md).

Voer Hallo opdrachten in Hallo PowerShell-console te volgen:

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

Hallo runbook wordt uitgevoerd en u kunt de status ervan controleren door te voeren `$job.Status`.

Hallo-runbook opgehaald Hallo Resource Manager-sjabloon en gebruikt deze toodeploy een nieuw Azure-opslagaccount.
U kunt zien of Hallo nieuw opslagaccount is gemaakt door het uitvoeren van de volgende opdracht Hallo:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Samenvatting

Dat is alles. Nu kunt u Azure Automation en Azure Storage en Resource Manager-sjablonen toodeploy alle Azure-resources.

## <a name="next-steps"></a>Volgende stappen

* toolearn meer informatie over het Resource Manager-sjablonen, Zie [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* Zie tooget slag met Azure Storage [inleiding tooAzure opslag](../storage/common/storage-introduction.md).
* toofind andere nuttige Azure Automation-runbooks, Zie [galerieën Runbook en de module voor Azure Automation](automation-runbook-gallery.md).
* toofind andere nuttige Resource Manager-sjablonen, Zie [Azure Quick Start-sjablonen](https://azure.microsoft.com/resources/templates/)

