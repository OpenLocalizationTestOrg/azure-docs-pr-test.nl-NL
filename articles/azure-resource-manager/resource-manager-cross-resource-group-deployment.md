---
title: aaaDeploy Azure-resources toomultiple resourcegroepen | Microsoft Docs
description: "Toont hoe tootarget meer dan één Azure-resource groep tijdens de implementatie."
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
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="4719f-103">Azure-resources toomore dan één resourcegroep implementeren</span><span class="sxs-lookup"><span data-stu-id="4719f-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="4719f-104">Normaal gesproken implementeren u alle Hallo resources in uw sjabloon tooa één resource-groep.</span><span class="sxs-lookup"><span data-stu-id="4719f-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="4719f-105">Er zijn echter scenario's waarbij u toodeploy een set resources samen, maar in verschillende resourcegroepen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="4719f-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="4719f-106">U kunt bijvoorbeeld toodeploy Hallo back-virtuele machine voor Azure Site Recovery tooa afzonderlijke resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="4719f-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="4719f-107">Resource Manager kunt u toouse geneste sjablonen tootarget verschillende resourcegroepen bevinden dan Hallo resourcegroep gebruikt voor Hallo bovenliggende sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4719f-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="4719f-108">Hallo-resourcegroep is Hallo lifecycle container voor de toepassing hello en de verzameling van resources.</span><span class="sxs-lookup"><span data-stu-id="4719f-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="4719f-109">U de resourcegroep Hallo buiten Hallo-sjabloon maken en Hallo resource groep tootarget opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="4719f-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="4719f-110">Zie voor een inleiding tooresource groepen, [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="4719f-111">Van de voorbeeldsjabloon</span><span class="sxs-lookup"><span data-stu-id="4719f-111">Example template</span></span>

<span data-ttu-id="4719f-112">een andere resource tootarget, moet u een sjabloon geneste of gekoppelde gebruiken tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="4719f-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="4719f-113">Hallo `Microsoft.Resources/deployments` brontype beschikt over een `resourceGroup` parameter waarmee u een andere resourcegroep voor Hallo toospecify geneste implementatie.</span><span class="sxs-lookup"><span data-stu-id="4719f-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="4719f-114">Alle brongroepen voor Hallo moeten bestaan voordat Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4719f-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="4719f-115">Hallo volgende voorbeeld implementeert twee storage-accounts: een in de resourcegroep Hallo opgegeven tijdens de implementatie, en één in een resourcegroep met de naam `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="4719f-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="4719f-116">Als u instelt `resourceGroup` toohello-naam van een resourcegroep die niet bestaat, Hallo implementatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="4719f-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="4719f-117">Als u een waarde op voor geen specifieke `resourceGroup`, Hallo bovenliggende resourcegroep maakt gebruik van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4719f-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="4719f-118">Hallo-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="4719f-118">Deploy hello template</span></span>

<span data-ttu-id="4719f-119">toodeploy hello voorbeeldsjabloon, kunt u Hallo-portal, Azure PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4719f-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="4719f-120">Voor Azure PowerShell of Azure CLI, moet u een release in mei 2017 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4719f-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="4719f-121">Hallo voorbeelden wordt ervan uitgegaan dat u hebt Hallo sjabloon lokaal opgeslagen als een bestand met de naam **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="4719f-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="4719f-122">Voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4719f-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="4719f-123">Voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="4719f-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="4719f-124">Nadat de implementatie is voltooid, ziet u twee resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="4719f-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="4719f-125">Elke resourcegroep bevat een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4719f-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="4719f-126">Gebruik de functie resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="4719f-126">Use resourceGroup() function</span></span>

<span data-ttu-id="4719f-127">Voor cross-resourcegroepimplementaties, hello [resouceGroup() functie](resource-group-template-functions-resource.md#resourcegroup) wordt omgezet is anders op basis van hoe u Hallo geneste sjabloon opgeven.</span><span class="sxs-lookup"><span data-stu-id="4719f-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="4719f-128">Als u een sjabloon in een andere sjabloon insluit, opgelost resouceGroup() in geneste sjabloon Hallo toohello bovenliggende resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4719f-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="4719f-129">Een ingesloten sjabloon maakt gebruik van Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="4719f-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="4719f-130">Als u afzonderlijke sjabloon tooa koppelt, oplossing resouceGroup() in de gekoppelde sjabloon Hallo toohello geneste resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4719f-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="4719f-131">Een gekoppelde sjabloon maakt gebruik van Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="4719f-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="4719f-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4719f-132">Next steps</span></span>

* <span data-ttu-id="4719f-133">hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4719f-134">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="4719f-135">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
