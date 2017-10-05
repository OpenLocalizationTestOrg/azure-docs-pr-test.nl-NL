---
title: Azure PowerShell-Script steekproef - sjabloon implementeren | Microsoft Docs
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
ms.openlocfilehash: b7a7dda1da653d084e02e6724d2f0cb5aa76807a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="d22b9-103">Azure Resource Manager sjabloonimplementatie - PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="d22b9-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="d22b9-104">Dit script implementeert u een Resource Manager-sjabloon naar een resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d22b9-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d22b9-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d22b9-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #The subscription id where the template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #The resource group where the template will be deployed. Can be the name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #The deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path to the template file. Defaults to template.json.
    [string]$TemplateFilePath = "template.json",  

    #Path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login to Azure and select subscription
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

# Start the deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="d22b9-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="d22b9-106">Clean up deployment</span></span> 

<span data-ttu-id="d22b9-107">Voer de volgende opdracht om te verwijderen van de resourcegroep en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="d22b9-107">Run the following command to remove the resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d22b9-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d22b9-108">Script explanation</span></span>

<span data-ttu-id="d22b9-109">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="d22b9-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="d22b9-110">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="d22b9-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d22b9-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="d22b9-111">Command</span></span> | <span data-ttu-id="d22b9-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d22b9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d22b9-113">Register AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="d22b9-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="d22b9-114">Registreert een resourceprovider zodat de brontypen die kunnen worden geïmplementeerd voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d22b9-114">Registers a resource provider so its resource types can be deployed to your subscription.</span></span>  |
| [<span data-ttu-id="d22b9-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d22b9-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="d22b9-116">Hiermee haalt u resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="d22b9-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="d22b9-117">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d22b9-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d22b9-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d22b9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d22b9-119">Nieuwe AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="d22b9-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="d22b9-120">Hiermee voegt u een Azure-implementatie toe aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d22b9-120">Adds an Azure deployment to a resource group.</span></span>  |
| [<span data-ttu-id="d22b9-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d22b9-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d22b9-122">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="d22b9-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="d22b9-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d22b9-123">Next steps</span></span>
* <span data-ttu-id="d22b9-124">Zie voor een inleiding tot het implementeren van sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d22b9-124">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="d22b9-125">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="d22b9-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="d22b9-126">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="d22b9-126">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="d22b9-127">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d22b9-127">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

