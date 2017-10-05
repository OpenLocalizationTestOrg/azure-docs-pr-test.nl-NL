---
title: Azure Service Bus-resources met behulp van Azure Resource Manager-sjablonen maken | Microsoft Docs
description: Azure Resource Manager-sjablonen gebruiken om het maken van Service Bus-resources te automatiseren
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="f02a3-103">Service Bus-resources met behulp van Azure Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="f02a3-104">In dit artikel wordt beschreven hoe maken en implementeren van Service Bus-resources met behulp van Azure Resource Manager-sjablonen, PowerShell en de Service Bus-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="f02a3-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="f02a3-105">Azure Resource Manager-sjablonen helpen u bij het definiëren van de resources te implementeren voor een oplossing en de parameters en variabelen die u voor het invoeren van waarden voor verschillende omgevingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="f02a3-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="f02a3-106">De sjabloon bestaat uit JSON en uitdrukkingen die u gebruiken kunt om waarden voor uw implementatie samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="f02a3-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="f02a3-107">Zie voor gedetailleerde informatie over het schrijven van Azure Resource Manager-sjablonen en een overzicht van de indeling template [structuur en de syntaxis van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f02a3-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f02a3-108">De voorbeelden in dit artikel tonen het gebruik van Azure Resource Manager voor het maken van een Service Bus-naamruimte en Berichtentiteit (wachtrij).</span><span class="sxs-lookup"><span data-stu-id="f02a3-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="f02a3-109">Andere voorbeelden sjabloon vindt u de [galerie van Azure-Snelstartsjablonen] [ Azure Quickstart Templates gallery] en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="f02a3-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="f02a3-110">Service Bus-Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="f02a3-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="f02a3-111">Deze Service Bus Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="f02a3-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="f02a3-112">Klik op de volgende koppelingen voor meer informatie over elk ervan, met koppelingen naar de sjablonen op GitHub:</span><span class="sxs-lookup"><span data-stu-id="f02a3-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="f02a3-113">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="f02a3-114">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="f02a3-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="f02a3-115">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="f02a3-116">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="f02a3-117">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="f02a3-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="f02a3-118">Implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="f02a3-118">Deploy with PowerShell</span></span>

<span data-ttu-id="f02a3-119">De volgende procedure beschrijft hoe u PowerShell gebruikt voor het implementeren van een Azure Resource Manager-sjabloon die u maakt een **standaard** servicetier Service Bus-naamruimte en een wachtrij binnen deze naamruimte.</span><span class="sxs-lookup"><span data-stu-id="f02a3-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="f02a3-120">In dit voorbeeld is gebaseerd op de [een Service Bus-naamruimte maken met de wachtrij](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f02a3-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="f02a3-121">De geschatte werkstroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f02a3-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="f02a3-122">Installeer PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f02a3-122">Install PowerShell.</span></span>
2. <span data-ttu-id="f02a3-123">De sjabloon en (optioneel) een parameterbestand maken.</span><span class="sxs-lookup"><span data-stu-id="f02a3-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="f02a3-124">In PowerShell, moet u zich aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f02a3-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="f02a3-125">Een nieuwe resourcegroep maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f02a3-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="f02a3-126">De implementatie testen.</span><span class="sxs-lookup"><span data-stu-id="f02a3-126">Test the deployment.</span></span>
6. <span data-ttu-id="f02a3-127">Indien gewenst kunt u de implementatiemodus.</span><span class="sxs-lookup"><span data-stu-id="f02a3-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="f02a3-128">De sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="f02a3-128">Deploy the template.</span></span>

<span data-ttu-id="f02a3-129">Zie voor meer informatie over het implementeren van Azure Resource Manager-sjablonen [implementeren van resources met Azure Resource Manager-sjablonen][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="f02a3-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="f02a3-130">PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="f02a3-130">Install PowerShell</span></span>

<span data-ttu-id="f02a3-131">Azure PowerShell installeren door de instructies in [aan de slag met Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f02a3-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="f02a3-132">Een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-132">Create a template</span></span>

<span data-ttu-id="f02a3-133">Kloon of kopieer de [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) sjabloon vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="f02a3-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="f02a3-134">Maak een parameterbestand (optioneel)</span><span class="sxs-lookup"><span data-stu-id="f02a3-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="f02a3-135">Een optionele parameters als bestand wilt gebruiken, kopieert u de [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) bestand.</span><span class="sxs-lookup"><span data-stu-id="f02a3-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="f02a3-136">Vervang de waarde van `serviceBusNamespaceName` met de naam van de Service Bus-naamruimte die u wilt maken in deze implementatie en vervang de waarde van `serviceBusQueueName` met de naam van de wachtrij die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f02a3-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="f02a3-137">Zie voor meer informatie de [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f02a3-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="f02a3-138">Aanmelden bij Azure en het Azure-abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="f02a3-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="f02a3-139">Voer de volgende opdracht vanaf een PowerShell-prompt:</span><span class="sxs-lookup"><span data-stu-id="f02a3-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f02a3-140">U wordt gevraagd om aan te melden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f02a3-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="f02a3-141">Voer de volgende opdracht om de beschikbare abonnementen weer te geven na aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f02a3-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="f02a3-142">Deze opdracht retourneert een lijst met beschikbare Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f02a3-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="f02a3-143">Kies een abonnement voor de huidige sessie met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="f02a3-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="f02a3-144">Vervang `<YourSubscriptionId>` met de GUID voor de Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f02a3-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="f02a3-145">Instellen van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f02a3-145">Set the resource group</span></span>

<span data-ttu-id="f02a3-146">Als u nog geen een bestaande resource groep, maakt u een nieuwe resourcegroep met de ** New-AzureRmResourceGroup ** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f02a3-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="f02a3-147">Geef de naam van de resourcegroep en de locatie die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f02a3-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="f02a3-148">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f02a3-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="f02a3-149">Als dit lukt, wordt een samenvatting van de nieuwe resourcegroep wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f02a3-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="f02a3-150">De implementatie testen</span><span class="sxs-lookup"><span data-stu-id="f02a3-150">Test the deployment</span></span>

<span data-ttu-id="f02a3-151">Valideren van uw implementatie door de `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f02a3-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="f02a3-152">Bij het testen van de implementatie, Geef parameters op exact dezelfde manier als bij het uitvoeren van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f02a3-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="f02a3-153">De implementatie maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-153">Create the deployment</span></span>

<span data-ttu-id="f02a3-154">Als u wilt maken van nieuwe implementatie uitvoeren de `New-AzureRmResourceGroupDeployment` cmdlet, en geef de benodigde parameters op wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f02a3-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="f02a3-155">De parameters bevatten een naam voor uw implementatie, de naam van de resourcegroep en het pad of de URL naar het sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="f02a3-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="f02a3-156">Als de **modus** parameter niet is opgegeven, de standaardwaarde van **incrementele** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f02a3-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="f02a3-157">Zie voor meer informatie [incrementele en volledige implementaties](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="f02a3-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="f02a3-158">De volgende opdracht wordt u gevraagd om de drie parameters in de PowerShell-venster:</span><span class="sxs-lookup"><span data-stu-id="f02a3-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="f02a3-159">Geef in plaats daarvan een parameterbestand door de volgende opdracht te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f02a3-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="f02a3-160">U kunt ook parameters inline gebruiken wanneer u de deployment-cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f02a3-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="f02a3-161">De opdracht is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f02a3-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="f02a3-162">Om uit te voeren een [voltooid](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) implementatie, stel de **modus** -parameter voor **Complete**:</span><span class="sxs-lookup"><span data-stu-id="f02a3-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="f02a3-163">De implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="f02a3-163">Verify the deployment</span></span>
<span data-ttu-id="f02a3-164">Als de bronnen worden geïmplementeerd, wordt een samenvatting van de implementatie weergegeven in het venster PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f02a3-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="f02a3-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f02a3-165">Next steps</span></span>
<span data-ttu-id="f02a3-166">U hebt nu de basiswerkstroom en opdrachten voor het implementeren van een Azure Resource Manager-sjabloon gezien.</span><span class="sxs-lookup"><span data-stu-id="f02a3-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="f02a3-167">Ga naar de volgende koppelingen voor meer gedetailleerde informatie:</span><span class="sxs-lookup"><span data-stu-id="f02a3-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="f02a3-168">[Overzicht van Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="f02a3-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="f02a3-169">[Resources met Resource Manager-sjablonen en Azure PowerShell implementeren][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="f02a3-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="f02a3-170">Azure Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="f02a3-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
