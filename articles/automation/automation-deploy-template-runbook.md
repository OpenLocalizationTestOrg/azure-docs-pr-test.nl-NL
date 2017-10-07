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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="08b53-104">Een Azure Resource Manager-sjabloon in een Azure Automation PowerShell-runbook implementeren</span><span class="sxs-lookup"><span data-stu-id="08b53-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="08b53-105">U kunt schrijven een [PowerShell voor Azure Automation-runbook](automation-first-runbook-textual-powershell.md) die een Azure-resource implementeert met behulp van een [Azure Resource Management-sjabloon](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="08b53-106">Op deze manier kunt u de implementatie van Azure-resources te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="08b53-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="08b53-107">U kunt uw Resource Manager-sjablonen in een beveiligde centrale locatie zoals Azure Storage onderhouden.</span><span class="sxs-lookup"><span data-stu-id="08b53-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="08b53-108">In dit onderwerp, maken we een PowerShell-runbook die gebruikmaakt van een Resource Manager-sjabloon die is opgeslagen in [Azure Storage](../storage/common/storage-introduction.md) toodeploy een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="08b53-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08b53-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="08b53-109">Prerequisites</span></span>

<span data-ttu-id="08b53-110">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="08b53-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="08b53-111">Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="08b53-111">Azure subscription.</span></span> <span data-ttu-id="08b53-112">Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="08b53-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="08b53-113">[Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="08b53-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="08b53-114">Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08b53-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="08b53-115">[Azure Storage-account](../storage/common/storage-create-storage-account.md) in welke toostore Hallo Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="08b53-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="08b53-116">Azure Powershell installeren op een lokale machine.</span><span class="sxs-lookup"><span data-stu-id="08b53-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="08b53-117">Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08b53-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="08b53-118">Hallo Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="08b53-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="08b53-119">In dit voorbeeld gebruiken we een Resource Manager-sjabloon die u een nieuwe Azure Storage-account implementeert.</span><span class="sxs-lookup"><span data-stu-id="08b53-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="08b53-120">Kopieer in een teksteditor Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="08b53-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="08b53-121">Hallo bestand opslaan lokaal als `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="08b53-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="08b53-122">Hallo Resource Manager-sjabloon opslaan in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="08b53-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="08b53-123">Nu gebruik van PowerShell toocreate een Azure Storage-bestandsshare en Hallo uploaden `TemplateTest.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="08b53-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="08b53-124">Zie voor instructies over hoe een bestand toocreate delen en uploaden van een bestand in hello Azure-portal, [aan de slag met Azure File storage in Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="08b53-125">Start PowerShell op uw lokale machine en Voer Hallo opdrachten toocreate een bestandsshare te volgen en upload Hallo Resource Manager-sjabloon toothat-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="08b53-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

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

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="08b53-126">Hallo PowerShell-script voor runbook maken</span><span class="sxs-lookup"><span data-stu-id="08b53-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="08b53-127">Nu we maken een PowerShell-script dat Hallo opgehaald `TemplateTest.json` bestand van Azure Storage en implementeert Hallo sjabloon toocreate een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="08b53-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="08b53-128">In een teksteditor plakken Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="08b53-128">In a text editor, paste hello following text:</span></span>

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

<span data-ttu-id="08b53-129">Hallo bestand opslaan lokaal als `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="08b53-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="08b53-130">Importeren en Hallo runbook publiceren in Azure Automation-account</span><span class="sxs-lookup"><span data-stu-id="08b53-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="08b53-131">Nu we PowerShell tooimport hello runbook gebruiken in uw Azure Automation-account en vervolgens publiceren Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="08b53-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="08b53-132">Voor informatie over het tooimport en een runbook publiceren in hello Azure-portal, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="08b53-133">tooimport `DeployTemplate.ps1` uitvoeren in uw Automation-account als een PowerShell-runbook Hallo volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="08b53-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

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

## <a name="start-hello-runbook"></a><span data-ttu-id="08b53-134">Hallo runbook starten</span><span class="sxs-lookup"><span data-stu-id="08b53-134">Start hello runbook</span></span>

<span data-ttu-id="08b53-135">Nu we Hallo runbook door de aanroepende Hallo starten [Start AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08b53-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="08b53-136">Voor informatie over hoe toostart een runbook in Azure-portal Hallo zien [een runbook starten in Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="08b53-137">Voer Hallo opdrachten in Hallo PowerShell-console te volgen:</span><span class="sxs-lookup"><span data-stu-id="08b53-137">Run hello following commands in hello PowerShell console:</span></span>

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

<span data-ttu-id="08b53-138">Hallo runbook wordt uitgevoerd en u kunt de status ervan controleren door te voeren `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="08b53-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="08b53-139">Hallo-runbook opgehaald Hallo Resource Manager-sjabloon en gebruikt deze toodeploy een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="08b53-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="08b53-140">U kunt zien of Hallo nieuw opslagaccount is gemaakt door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="08b53-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="08b53-141">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="08b53-141">Summary</span></span>

<span data-ttu-id="08b53-142">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="08b53-142">That's it!</span></span> <span data-ttu-id="08b53-143">Nu kunt u Azure Automation en Azure Storage en Resource Manager-sjablonen toodeploy alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="08b53-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08b53-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08b53-144">Next steps</span></span>

* <span data-ttu-id="08b53-145">toolearn meer informatie over het Resource Manager-sjablonen, Zie [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="08b53-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="08b53-146">Zie tooget slag met Azure Storage [inleiding tooAzure opslag](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="08b53-147">toofind andere nuttige Azure Automation-runbooks, Zie [galerieën Runbook en de module voor Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="08b53-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="08b53-148">toofind andere nuttige Resource Manager-sjablonen, Zie [Azure Quick Start-sjablonen](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="08b53-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

