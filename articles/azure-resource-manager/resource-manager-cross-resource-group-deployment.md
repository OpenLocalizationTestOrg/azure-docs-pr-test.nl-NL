---
title: Azure-resources implementeren op meerdere resourcegroepen | Microsoft Docs
description: "Laat zien hoe u meer dan één Azure-resourcegroep als doel tijdens de implementatie."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="b9bf0-103">Azure-resources implementeren op meer dan één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b9bf0-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="b9bf0-104">Normaal gesproken implementeren u alle resources in de sjabloon één resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="b9bf0-105">Er zijn echter scenario's waarin u wilt implementeren van een set resources samen, maar in verschillende resourcegroepen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="b9bf0-106">U wilt bijvoorbeeld de back-virtuele machine voor Azure Site Recovery implementeert naar een afzonderlijke resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="b9bf0-107">Resource Manager kunt u geneste sjablonen met verschillende resourcegroepen bevinden dan de resourcegroep voor de bovenliggende sjabloon gebruikt als doel.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="b9bf0-108">De resourcegroep is de container levenscyclus voor de toepassing en de verzameling van resources.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="b9bf0-109">U maakt de resourcegroep buiten de sjabloon en geef de resourcegroep toe te passen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="b9bf0-110">Zie voor een inleiding tot resourcegroepen, [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf0-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="b9bf0-111">Van de voorbeeldsjabloon</span><span class="sxs-lookup"><span data-stu-id="b9bf0-111">Example template</span></span>

<span data-ttu-id="b9bf0-112">Als u wilt richten op een andere resource, moet u een sjabloon geneste of gekoppelde tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="b9bf0-113">De `Microsoft.Resources/deployments` brontype beschikt over een `resourceGroup` parameter waarmee u een andere resourcegroep voor de geneste implementatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="b9bf0-114">Alle brongroepen moeten bestaan voordat de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="b9bf0-115">Het volgende voorbeeld worden twee storage-accounts: in de resourcegroep die is opgegeven tijdens de implementatie, geïmplementeerd en één in een resourcegroep met de naam `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="b9bf0-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="b9bf0-116">Als u instelt `resourceGroup` op de naam van een resourcegroep die niet bestaat, mislukt de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="b9bf0-117">Als u een waarde op voor geen specifieke `resourceGroup`, Resource Manager maakt gebruik van de bovenliggende resource-groep.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="b9bf0-118">De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="b9bf0-118">Deploy the template</span></span>

<span data-ttu-id="b9bf0-119">U kunt de portal, Azure PowerShell of Azure CLI gebruiken voor het implementeren van de voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="b9bf0-120">Voor Azure PowerShell of Azure CLI, moet u een release in mei 2017 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="b9bf0-121">De voorbeelden wordt ervan uitgegaan dat u de sjabloon lokaal hebt opgeslagen als een bestand met de naam **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="b9bf0-122">Voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9bf0-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="b9bf0-123">Voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="b9bf0-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="b9bf0-124">Nadat de implementatie is voltooid, ziet u twee resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="b9bf0-125">Elke resourcegroep bevat een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="b9bf0-126">Gebruik de functie resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="b9bf0-126">Use resourceGroup() function</span></span>

<span data-ttu-id="b9bf0-127">Voor cross-resourcegroepimplementaties, de [resouceGroup() functie](resource-group-template-functions-resource.md#resourcegroup) wordt omgezet is anders op basis van hoe u de geneste sjabloon opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="b9bf0-128">Als u een sjabloon in een andere sjabloon insluit, is resouceGroup() in de geneste sjabloon wordt omgezet naar de bovenliggende resource-groep.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="b9bf0-129">Een ingesloten sjabloon maakt gebruik van de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="b9bf0-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="b9bf0-130">Als u een koppeling naar een afzonderlijke sjabloon, wordt resouceGroup() in de gekoppelde sjabloon omgezet in de geneste resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b9bf0-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="b9bf0-131">Een gekoppelde sjabloon maakt gebruik van de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="b9bf0-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b9bf0-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9bf0-132">Next steps</span></span>

* <span data-ttu-id="b9bf0-133">Om te begrijpen hoe parameters in de sjabloon definieert, Zie [inzicht in de structuur en de syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf0-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b9bf0-134">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf0-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b9bf0-135">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf0-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
