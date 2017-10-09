---
title: aaaCreate Azure Service Bus-naamruimte en in een wachtrij met Azure Resource Manager-sjabloon | Microsoft Docs
description: Een Service Bus-naamruimte en een wachtrij met Azure Resource Manager-sjabloon maken
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="3c8c4-103">Een Service Bus-naamruimte en een wachtrij met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="3c8c4-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="3c8c4-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een Service Bus-naamruimte en een wachtrij binnen deze naamruimte.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="3c8c4-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="3c8c4-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="3c8c4-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="3c8c4-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3c8c4-108">Zie voor de volledige sjabloon hello, Hallo [Service Bus-naamruimte en de wachtrij sjabloon] [ Service Bus namespace and queue template] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="3c8c4-109">Hallo na Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="3c8c4-110">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="3c8c4-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3c8c4-111">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="3c8c4-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="3c8c4-112">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="3c8c4-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="3c8c4-113">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="3c8c4-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="3c8c4-114">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3c8c4-115">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="3c8c4-115">What will you deploy?</span></span>

<span data-ttu-id="3c8c4-116">Met deze sjabloon implementeert u een Service Bus-naamruimte met een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="3c8c4-117">[Service Bus-wachtrijen](service-bus-queues-topics-subscriptions.md#queues) bieden First In, eerste Out (FIFO) message delivery tooone of meer concurrerende consumenten.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="3c8c4-118">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c8c4-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="3c8c4-119">[![TooAzure implementeren](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3c8c4-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3c8c4-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="3c8c4-120">Parameters</span></span>

<span data-ttu-id="3c8c4-121">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="3c8c4-122">Hallo-sjabloon bevat een sectie met de naam `Parameters` die Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="3c8c4-123">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="3c8c4-124">Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="3c8c4-125">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="3c8c4-126">Hallo sjabloon definieert Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3c8c4-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3c8c4-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="3c8c4-128">Hallo-naam van Hallo Service Bus-naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="3c8c4-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="3c8c4-129">serviceBusQueueName</span></span>
<span data-ttu-id="3c8c4-130">de naam van de Hallo van Hallo wachtrij in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="3c8c4-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3c8c4-131">serviceBusApiVersion</span></span>
<span data-ttu-id="3c8c4-132">Hallo Service Bus-API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="3c8c4-133">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="3c8c4-133">Resources toodeploy</span></span>
<span data-ttu-id="3c8c4-134">Maakt een standaard Service Bus-naamruimte van het type **Messaging**, met een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c8c4-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
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
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="3c8c4-135">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="3c8c4-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="3c8c4-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c8c4-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="3c8c4-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c8c4-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="3c8c4-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c8c4-138">Next steps</span></span>
<span data-ttu-id="3c8c4-139">Nu u hebt gemaakt en geïmplementeerd resources met behulp van Azure Resource Manager, kunt u nagaan hoe toomanage deze resources aan de hand van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="3c8c4-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="3c8c4-140">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="3c8c4-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3c8c4-141">Service Bus-resources beheren met Hallo Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="3c8c4-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
