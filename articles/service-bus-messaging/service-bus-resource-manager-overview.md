---
title: aaaCreate Azure Service Bus-resources met behulp van Azure Resource Manager-sjablonen | Microsoft Docs
description: Gebruik Azure Resource Manager sjablonen tooautomate Hallo maken van Service Bus-resources
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="34e11-103">Service Bus-resources met behulp van Azure Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="34e11-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="34e11-104">Dit artikel wordt beschreven hoe toocreate en implementeren van Service Bus-resources met behulp van Azure Resource Manager-sjablonen, PowerShell en Hallo Service Bus-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="34e11-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="34e11-105">Azure Resource Manager-sjablonen kunt u definiëren Hallo resources toodeploy voor een oplossing en toospecify parameters en variabelen vaststellen waarmee u tooinput waarden voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="34e11-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="34e11-106">Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34e11-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="34e11-107">Zie voor gedetailleerde informatie over het schrijven van Azure Resource Manager-sjablonen en een beschrijving van de indeling van de template Hallo [structuur en de syntaxis van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34e11-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="34e11-108">voorbeelden in dit artikel tonen hoe Hallo toouse Azure Resource Manager toocreate een Service Bus-naamruimte en de messaging-eenheid (wachtrij).</span><span class="sxs-lookup"><span data-stu-id="34e11-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="34e11-109">Andere voorbeelden sjabloon vindt u op Hallo [galerie van Azure-Snelstartsjablonen] [ Azure Quickstart Templates gallery] en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="34e11-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="34e11-110">Service Bus-Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34e11-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="34e11-111">Deze Service Bus Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="34e11-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="34e11-112">Klik op Hallo volgende koppelingen voor meer informatie over elk ervan, met koppelingen toohello sjablonen op GitHub:</span><span class="sxs-lookup"><span data-stu-id="34e11-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="34e11-113">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="34e11-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="34e11-114">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="34e11-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="34e11-115">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="34e11-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="34e11-116">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="34e11-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="34e11-117">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="34e11-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="34e11-118">Implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e11-118">Deploy with PowerShell</span></span>

<span data-ttu-id="34e11-119">Hallo volgende procedure wordt beschreven hoe toouse PowerShell toodeploy een Azure Resource Manager-sjabloon die wordt gemaakt een **standaard** servicetier Service Bus-naamruimte en een wachtrij binnen deze naamruimte.</span><span class="sxs-lookup"><span data-stu-id="34e11-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="34e11-120">In dit voorbeeld is gebaseerd op Hallo [een Service Bus-naamruimte maken met de wachtrij](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="34e11-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="34e11-121">Hallo geschatte werkstroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="34e11-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="34e11-122">Installeer PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34e11-122">Install PowerShell.</span></span>
2. <span data-ttu-id="34e11-123">Hallo-sjabloon en (optioneel) een parameterbestand maken.</span><span class="sxs-lookup"><span data-stu-id="34e11-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="34e11-124">Aanmelden in PowerShell tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="34e11-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="34e11-125">Een nieuwe resourcegroep maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="34e11-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="34e11-126">Hallo-implementatie testen.</span><span class="sxs-lookup"><span data-stu-id="34e11-126">Test hello deployment.</span></span>
6. <span data-ttu-id="34e11-127">Indien gewenst kunt u Hallo implementatiemodus.</span><span class="sxs-lookup"><span data-stu-id="34e11-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="34e11-128">Hallo-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="34e11-128">Deploy hello template.</span></span>

<span data-ttu-id="34e11-129">Zie voor meer informatie over het implementeren van Azure Resource Manager-sjablonen [implementeren van resources met Azure Resource Manager-sjablonen][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="34e11-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="34e11-130">PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="34e11-130">Install PowerShell</span></span>

<span data-ttu-id="34e11-131">Azure PowerShell installeren door de instructies te volgen Hallo in [aan de slag met Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="34e11-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="34e11-132">Een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="34e11-132">Create a template</span></span>

<span data-ttu-id="34e11-133">Kloon of kopieer Hallo [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) sjabloon vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="34e11-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="34e11-134">Maak een parameterbestand (optioneel)</span><span class="sxs-lookup"><span data-stu-id="34e11-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="34e11-135">toouse een optionele parameters-bestand kopiëren Hallo [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) bestand.</span><span class="sxs-lookup"><span data-stu-id="34e11-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="34e11-136">Vervang de waarde Hallo van `serviceBusNamespaceName` met de naam van de Service Bus-naamruimte Hallo Hallo u toocreate in deze implementatie wilt en vervang de waarde Hallo van `serviceBusQueueName` met de naam van de wachtrij Hallo Hallo gewenste toocreate.</span><span class="sxs-lookup"><span data-stu-id="34e11-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="34e11-137">Zie voor meer informatie, Hallo [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="34e11-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="34e11-138">Meld u bij tooAzure en hello Azure-abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="34e11-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="34e11-139">Voer vanuit een PowerShell-prompt Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="34e11-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="34e11-140">U bent na vragen aan gebruiker toolog op tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="34e11-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="34e11-141">Na aanmelding uitgevoerd na de opdracht tooview Hallo uw beschikbare abonnementen.</span><span class="sxs-lookup"><span data-stu-id="34e11-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="34e11-142">Deze opdracht retourneert een lijst met beschikbare Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="34e11-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="34e11-143">Kies een abonnement voor Hallo huidige sessie door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="34e11-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="34e11-144">Vervang `<YourSubscriptionId>` Hello GUID voor hello Azure-abonnement u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="34e11-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="34e11-145">Set Hallo resourcegroep</span><span class="sxs-lookup"><span data-stu-id="34e11-145">Set hello resource group</span></span>

<span data-ttu-id="34e11-146">Als u een bestaande resource groep, maakt u een nieuwe resourcegroep met Hallo niet hebt ** New-AzureRmResourceGroup ** opdracht.</span><span class="sxs-lookup"><span data-stu-id="34e11-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="34e11-147">Hallo-naam van het Hallo-resourcegroep en locatie die u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="34e11-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="34e11-148">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="34e11-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="34e11-149">Als dit lukt, wordt een overzicht van de nieuwe resourcegroep Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="34e11-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="34e11-150">Hallo-implementatie testen</span><span class="sxs-lookup"><span data-stu-id="34e11-150">Test hello deployment</span></span>

<span data-ttu-id="34e11-151">Valideren van uw implementatie door Hallo `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34e11-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="34e11-152">Bij het testen van Hallo implementatie Geef parameters op exact dezelfde manier als bij het uitvoeren van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="34e11-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="34e11-153">Hallo implementatie maken</span><span class="sxs-lookup"><span data-stu-id="34e11-153">Create hello deployment</span></span>

<span data-ttu-id="34e11-154">toocreate hello nieuwe implementatie, Voer Hallo `New-AzureRmResourceGroupDeployment` cmdlet, en geef de benodigde parameters op Hallo wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="34e11-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="34e11-155">Hallo parameters bevatten een naam voor uw implementatie, het Hallo-naam van uw resourcegroep, en het Hallo-pad of de URL toohello sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="34e11-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="34e11-156">Als hello **modus** parameter niet is opgegeven, de standaardwaarde van Hallo **incrementele** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34e11-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="34e11-157">Zie voor meer informatie [incrementele en volledige implementaties](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="34e11-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="34e11-158">Hallo volgende opdrachtprompts u voor Hallo drie parameters in Hallo PowerShell-venster:</span><span class="sxs-lookup"><span data-stu-id="34e11-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="34e11-159">een parameterbestand toospecify gebruiken in plaats daarvan Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="34e11-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="34e11-160">U kunt ook parameters inline gebruiken als u Hallo deployment cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="34e11-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="34e11-161">Hallo-opdracht is als volgt:</span><span class="sxs-lookup"><span data-stu-id="34e11-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="34e11-162">toorun een [voltooid](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) voor implementatie, set Hallo **modus** parameter te**Complete**:</span><span class="sxs-lookup"><span data-stu-id="34e11-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="34e11-163">Hallo-implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="34e11-163">Verify hello deployment</span></span>
<span data-ttu-id="34e11-164">Als het Hallo-resources zijn geïmplementeerd, wordt een overzicht van Hallo-implementatie in Hallo PowerShell-venster weergegeven:</span><span class="sxs-lookup"><span data-stu-id="34e11-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="34e11-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34e11-165">Next steps</span></span>
<span data-ttu-id="34e11-166">U hebt nu gezien Hallo basiswerkstroom en opdrachten voor het implementeren van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="34e11-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="34e11-167">Ga naar Hallo koppelingen volgen voor meer gedetailleerde informatie:</span><span class="sxs-lookup"><span data-stu-id="34e11-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="34e11-168">[Overzicht van Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="34e11-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="34e11-169">[Resources met Resource Manager-sjablonen en Azure PowerShell implementeren][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="34e11-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="34e11-170">Azure Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="34e11-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
