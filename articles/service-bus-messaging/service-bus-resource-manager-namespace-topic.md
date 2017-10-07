---
title: aaaCreate Azure Service Bus-naamruimte onderwerpabonnement met Azure Resource Manager-sjabloon | Microsoft Docs
description: Een Service Bus-naamruimte maken met het onderwerp en een abonnement met Azure Resource Manager-sjabloon
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="52874-103">Een Service Bus-naamruimte maken met het onderwerp en een abonnement met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="52874-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="52874-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een Service Bus-naamruimte en een onderwerp en een abonnement binnen deze naamruimte.</span><span class="sxs-lookup"><span data-stu-id="52874-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="52874-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="52874-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="52874-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten</span><span class="sxs-lookup"><span data-stu-id="52874-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="52874-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="52874-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="52874-108">Zie voor de volledige sjabloon hello, Hallo [Service Bus-naamruimte met onderwerp en een abonnement] [ Service Bus namespace with topic and subscription] sjabloon.</span><span class="sxs-lookup"><span data-stu-id="52874-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="52874-109">Hallo na Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="52874-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="52874-110">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="52874-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="52874-111">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="52874-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="52874-112">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="52874-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="52874-113">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="52874-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="52874-114">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="52874-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="52874-115">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="52874-115">What will you deploy?</span></span>

<span data-ttu-id="52874-116">Met deze sjabloon implementeert u een Service Bus-naamruimte met onderwerp en een abonnement.</span><span class="sxs-lookup"><span data-stu-id="52874-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="52874-117">[Service Bus-onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) biedt een een-op-veel-vorm van communicatie, in een *publiceren/abonneren* patroon.</span><span class="sxs-lookup"><span data-stu-id="52874-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="52874-118">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="52874-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="52874-119">[![TooAzure implementeren](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="52874-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="52874-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="52874-120">Parameters</span></span>

<span data-ttu-id="52874-121">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="52874-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="52874-122">Hallo-sjabloon bevat een sectie met de naam `Parameters` die Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="52874-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="52874-123">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="52874-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="52874-124">Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="52874-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="52874-125">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="52874-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="52874-126">Hallo sjabloon definieert Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="52874-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="52874-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="52874-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="52874-128">Hallo-naam van Hallo Service Bus-naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="52874-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="52874-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="52874-129">serviceBusTopicName</span></span>
<span data-ttu-id="52874-130">Hallo-naam van Hallo onderwerp in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52874-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="52874-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="52874-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="52874-132">Hallo-naam van het Hallo-abonnement in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52874-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="52874-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="52874-133">serviceBusApiVersion</span></span>
<span data-ttu-id="52874-134">Hallo Service Bus-API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="52874-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="52874-135">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="52874-135">Resources toodeploy</span></span>
<span data-ttu-id="52874-136">Maakt een standaard Service Bus-naamruimte van het type **Messaging**, met het onderwerp en een abonnement.</span><span class="sxs-lookup"><span data-stu-id="52874-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="52874-137">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="52874-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="52874-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52874-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="52874-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="52874-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="52874-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52874-140">Next steps</span></span>
<span data-ttu-id="52874-141">Nu u hebt gemaakt en geïmplementeerd resources met behulp van Azure Resource Manager, kunt u nagaan hoe toomanage deze resources aan de hand van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="52874-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="52874-142">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="52874-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="52874-143">Service Bus-resources beheren met Hallo Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="52874-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
