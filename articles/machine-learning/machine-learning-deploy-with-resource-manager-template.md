---
title: aaaDeploy een Machine Learning-werkruimte met Azure Resource Manager | Microsoft Docs
description: Hoe toodeploy een werkruimte voor Azure Machine Learning met Azure Resource Manager-sjabloon
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="9e848-103">Machine Learning-werkruimte implementeren met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e848-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="9e848-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="9e848-104">Introduction</span></span>
<span data-ttu-id="9e848-105">Met een Azure Resource Manager-implementatiesjabloon u bespaart tijd doordat u een toodeploy schaalbare manier met elkaar verbonden onderdelen van een mechanisme voor validatie en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9e848-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="9e848-106">tooset van Azure Machine Learning werkruimten, bijvoorbeeld, moet u toofirst Azure storage-account configureert en vervolgens implementeert uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9e848-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="9e848-107">Stel dit handmatig te doen voor honderden werkruimten.</span><span class="sxs-lookup"><span data-stu-id="9e848-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="9e848-108">Een eenvoudiger alternatief is toouse een Azure Resource Manager-sjabloon toodeploy een Azure Machine Learning-werkruimte en de afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="9e848-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="9e848-109">In dit artikel leert u dit proces stapsgewijs.</span><span class="sxs-lookup"><span data-stu-id="9e848-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="9e848-110">Zie voor een goed overzicht van Azure Resource Manager [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e848-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="9e848-111">Stap voor stap: een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="9e848-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="9e848-112">We wordt een Azure-resourcegroep maken en implementeren van een nieuwe Azure-opslagaccount en een nieuwe Azure Machine Learning-werkruimte met een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9e848-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="9e848-113">Zodra het Hallo-implementatie is voltooid, wordt er belangrijke informatie over het Hallo-werkruimten die zijn gemaakt (de primaire sleutel hello, Hallo workspaceID en Hallo URL toohello werkruimte) afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="9e848-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="9e848-114">Een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="9e848-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="9e848-115">Een Machine Learning-werkruimte vereist een Azure storage-account toostore Hallo gegevensset gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="9e848-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="9e848-116">Hallo volgende sjabloon gebruikt Hallo-naam van Hallo toogenerate Hallo storage account Resourcegroepnaam en de naam van de werkruimte Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e848-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="9e848-117">Verder wordt Hallo opslagaccountnaam als een eigenschap tijdens het Hallo-werkruimte maken.</span><span class="sxs-lookup"><span data-stu-id="9e848-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="9e848-118">Deze sjabloon opslaan als mlworkspace.json bestand onder c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="9e848-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="9e848-119">Hallo-resourcegroep, op basis van Hallo sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="9e848-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="9e848-120">Open PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e848-120">Open PowerShell</span></span>
* <span data-ttu-id="9e848-121">Modules voor Azure Resource Manager en Azure Service Management installeren</span><span class="sxs-lookup"><span data-stu-id="9e848-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="9e848-122">Deze stappen download en installeer Hallo modules nodig toocomplete Hallo resterende stappen.</span><span class="sxs-lookup"><span data-stu-id="9e848-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="9e848-123">Dit hoeft slechts één keer uitgevoerd in Hallo omgeving waar het uitvoeren van PowerShell-opdrachten Hallo toobe.</span><span class="sxs-lookup"><span data-stu-id="9e848-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="9e848-124">TooAzure verifiëren</span><span class="sxs-lookup"><span data-stu-id="9e848-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="9e848-125">Deze stap moet toobe herhaald voor elke sessie.</span><span class="sxs-lookup"><span data-stu-id="9e848-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="9e848-126">Eenmaal is geverifieerd, moet uw abonnementsgegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9e848-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure-Account][1]

<span data-ttu-id="9e848-128">Nu we tooAzure toegang hebben, kunnen we Hallo resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="9e848-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="9e848-129">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="9e848-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="9e848-130">Controleer of dat die resourcegroep Hallo juist is ingericht.</span><span class="sxs-lookup"><span data-stu-id="9e848-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="9e848-131">**ProvisioningState** moet worden "is voltooid."</span><span class="sxs-lookup"><span data-stu-id="9e848-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="9e848-132">Hallo de naam van resourcegroep wordt gebruikt door Hallo sjabloon toogenerate Hallo naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9e848-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="9e848-133">Hallo opslagaccountnaam moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9e848-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Resourcegroep][2]

* <span data-ttu-id="9e848-135">Met resource Hallo implementatie kunt implementeren die een nieuwe Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9e848-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="9e848-136">Zodra het Hallo-implementatie is voltooid, is het eenvoudig tooaccess eigenschappen van Hallo werkruimte die u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9e848-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="9e848-137">U kunt bijvoorbeeld toegang tot Hallo primaire Key Token.</span><span class="sxs-lookup"><span data-stu-id="9e848-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="9e848-138">Een andere manier tooretrieve tokens van bestaande werkruimte is toouse Hallo Invoke-AzureRmResourceAction-opdracht.</span><span class="sxs-lookup"><span data-stu-id="9e848-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="9e848-139">Bijvoorbeeld, kunt u de primaire en secundaire tokens Hallo van alle werkruimten aanbieden.</span><span class="sxs-lookup"><span data-stu-id="9e848-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="9e848-140">Nadat het Hallo-werkruimte is ingericht, kunt u ook veel Azure Machine Learning Studio taken met behulp van Hallo automatiseren [PowerShell-Module voor Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="9e848-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e848-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e848-141">Next Steps</span></span>
* <span data-ttu-id="9e848-142">Meer informatie over [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e848-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="9e848-143">Bekijk Hallo [Azure Quickstart-opslagplaats voor sjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="9e848-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="9e848-144">Bekijk deze video over [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="9e848-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
