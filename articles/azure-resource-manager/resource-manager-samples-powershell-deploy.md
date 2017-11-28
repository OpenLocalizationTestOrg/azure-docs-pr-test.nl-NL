---
title: aaaAzure PowerShell-voorbeeldscript - sjabloon implementeren | Microsoft Docs
description: Voorbeeld van een script voor het implementeren van een Azure Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="73da9-103">Azure Resource Manager sjabloonimplementatie - PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="73da9-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="73da9-104">Dit script wordt geïmplementeerd voor een resourcegroep voor Resource Manager sjabloon tooa in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="73da9-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="73da9-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="73da9-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="73da9-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="73da9-106">Clean up deployment</span></span> 

<span data-ttu-id="73da9-107">Voer Hallo volgende opdracht tooremove Hallo resourcegroep en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="73da9-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="73da9-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="73da9-108">Script explanation</span></span>

<span data-ttu-id="73da9-109">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="73da9-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="73da9-110">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="73da9-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="73da9-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="73da9-111">Command</span></span> | <span data-ttu-id="73da9-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="73da9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="73da9-113">Register AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="73da9-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="73da9-114">Registreert een resourceprovider zodat de brontypen die geïmplementeerd tooyour abonnement worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="73da9-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="73da9-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="73da9-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="73da9-116">Hiermee haalt u resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="73da9-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="73da9-117">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="73da9-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="73da9-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="73da9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="73da9-119">Nieuwe AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="73da9-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="73da9-120">Voegt een Azure-implementatie tooa-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="73da9-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="73da9-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="73da9-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="73da9-122">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="73da9-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="73da9-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73da9-123">Next steps</span></span>
* <span data-ttu-id="73da9-124">Zie voor een inleiding toodeploying sjablonen, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="73da9-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="73da9-125">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="73da9-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="73da9-126">toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="73da9-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="73da9-127">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="73da9-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

