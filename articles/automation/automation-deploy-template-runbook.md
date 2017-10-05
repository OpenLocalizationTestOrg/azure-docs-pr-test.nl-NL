---
title: Een Azure Resource Manager-sjabloon in een Azure Automation-runbook implementeren | Microsoft Docs
description: Het implementeren van een Azure Resource Manager-sjabloon die is opgeslagen in Azure Storage vanuit een runbook
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
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="7a73f-104">Een Azure Resource Manager-sjabloon in een Azure Automation PowerShell-runbook implementeren</span><span class="sxs-lookup"><span data-stu-id="7a73f-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="7a73f-105">U kunt schrijven een [PowerShell voor Azure Automation-runbook](automation-first-runbook-textual-powershell.md) die een Azure-resource implementeert met behulp van een [Azure Resource Management-sjabloon](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="7a73f-106">Op deze manier kunt u de implementatie van Azure-resources te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="7a73f-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="7a73f-107">U kunt uw Resource Manager-sjablonen in een beveiligde centrale locatie zoals Azure Storage onderhouden.</span><span class="sxs-lookup"><span data-stu-id="7a73f-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="7a73f-108">In dit onderwerp, maken we een PowerShell-runbook die gebruikmaakt van een Resource Manager-sjabloon die is opgeslagen in [Azure Storage](../storage/common/storage-introduction.md) voor het implementeren van een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7a73f-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a73f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7a73f-109">Prerequisites</span></span>

<span data-ttu-id="7a73f-110">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="7a73f-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="7a73f-111">Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a73f-111">Azure subscription.</span></span> <span data-ttu-id="7a73f-112">Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a73f-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="7a73f-113">[Automation-account](automation-sec-configure-azure-runas-account.md) om het runbook te bevatten en te verifiëren voor Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="7a73f-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="7a73f-114">Dit account moet machtigingen hebben om de virtuele machine te starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="7a73f-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="7a73f-115">[Azure Storage-account](../storage/common/storage-create-storage-account.md) waarin u voor het opslaan van de Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="7a73f-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="7a73f-116">Azure Powershell installeren op een lokale machine.</span><span class="sxs-lookup"><span data-stu-id="7a73f-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="7a73f-117">Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het ophalen van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a73f-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="7a73f-118">Het Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="7a73f-118">Create the Resource Manager template</span></span>

<span data-ttu-id="7a73f-119">In dit voorbeeld gebruiken we een Resource Manager-sjabloon die u een nieuwe Azure Storage-account implementeert.</span><span class="sxs-lookup"><span data-stu-id="7a73f-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="7a73f-120">In een teksteditor, kopieert u de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="7a73f-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="7a73f-121">Sla het bestand lokaal als `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="7a73f-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="7a73f-122">De Resource Manager-sjabloon opslaan in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7a73f-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="7a73f-123">Nu we PowerShell gebruiken voor het maken van een Azure Storage-bestandsshare en upload de `TemplateTest.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="7a73f-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="7a73f-124">Zie voor instructies over het maken van een bestand delen en een bestand in de Azure portal uploaden, [aan de slag met Azure File storage in Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="7a73f-125">Start PowerShell op uw lokale computer en voer de volgende opdrachten een bestandsshare maken en uploaden van de Resource Manager-sjabloon naar of de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7a73f-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="7a73f-126">Het PowerShell-runbookscript maken</span><span class="sxs-lookup"><span data-stu-id="7a73f-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="7a73f-127">Nu we maken een PowerShell-script wordt de `TemplateTest.json` bestand van Azure Storage en implementeert u de sjabloon voor het maken van een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7a73f-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="7a73f-128">In een teksteditor en plak de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="7a73f-128">In a text editor, paste the following text:</span></span>

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



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="7a73f-129">Sla het bestand lokaal als `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="7a73f-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="7a73f-130">Importeren en het runbook publiceren in Azure Automation-account</span><span class="sxs-lookup"><span data-stu-id="7a73f-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="7a73f-131">Nu we PowerShell gebruiken voor het importeren van het runbook in Azure Automation-account en vervolgens het runbook te publiceren.</span><span class="sxs-lookup"><span data-stu-id="7a73f-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="7a73f-132">Zie voor meer informatie over het importeren en publiceren van een runbook in de Azure portal [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="7a73f-133">Voor het importeren van `DeployTemplate.ps1` in uw Automation-account als een PowerShell-runbook, voer de volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7a73f-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="7a73f-134">Het runbook starten</span><span class="sxs-lookup"><span data-stu-id="7a73f-134">Start the runbook</span></span>

<span data-ttu-id="7a73f-135">Nu we het runbook door het aanroepen van starten de [Start AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7a73f-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="7a73f-136">Zie voor meer informatie over het starten van een runbook in de Azure portal [een runbook starten in Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="7a73f-137">Voer de volgende opdrachten in de PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="7a73f-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="7a73f-138">Het runbook wordt uitgevoerd, en u kunt de status ervan controleren door te voeren `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="7a73f-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="7a73f-139">Het runbook opgehaald van de Resource Manager-sjabloon en wordt gebruikt voor het implementeren van een nieuw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7a73f-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="7a73f-140">U kunt zien dat het nieuwe opslagaccount is gemaakt door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7a73f-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="7a73f-141">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="7a73f-141">Summary</span></span>

<span data-ttu-id="7a73f-142">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7a73f-142">That's it!</span></span> <span data-ttu-id="7a73f-143">Nu kunt u Azure Automation en Azure Storage en Resource Manager-sjablonen voor het implementeren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="7a73f-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a73f-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a73f-144">Next steps</span></span>

* <span data-ttu-id="7a73f-145">Zie voor meer informatie over het Resource Manager-sjablonen, [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7a73f-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="7a73f-146">Aan de slag met Azure Storage Zie [Inleiding tot Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="7a73f-147">Andere nuttige Azure Automation-runbooks vindt [galerieën Runbook en de module voor Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="7a73f-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="7a73f-148">Andere nuttige Resource Manager-sjablonen vindt [Azure Quick Start-sjablonen](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="7a73f-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

