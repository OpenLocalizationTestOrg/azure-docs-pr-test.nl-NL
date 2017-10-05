---
title: Azure Service Bus-naamruimte onderwerpabonnement met Azure Resource Manager-sjabloon maken | Microsoft Docs
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
ms.openlocfilehash: 8dd48787e7b788d249085b3110484de1a2c1d265
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="a811d-103">Een Service Bus-naamruimte maken met het onderwerp en een abonnement met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a811d-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="a811d-104">Dit artikel laat zien hoe u een Azure Resource Manager-sjabloon die wordt gemaakt van een Service Bus-naamruimte en een onderwerp en een abonnement binnen deze naamruimte.</span><span class="sxs-lookup"><span data-stu-id="a811d-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="a811d-105">U leert hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a811d-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="a811d-106">U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen</span><span class="sxs-lookup"><span data-stu-id="a811d-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="a811d-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a811d-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a811d-108">Zie voor de volledige sjabloon, het [Service Bus-naamruimte met onderwerp en een abonnement] [ Service Bus namespace with topic and subscription] sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a811d-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="a811d-109">De volgende Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="a811d-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="a811d-110">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="a811d-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="a811d-111">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="a811d-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="a811d-112">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="a811d-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="a811d-113">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="a811d-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="a811d-114">Om te controleren of de meest recente sjablonen, gaat u naar de [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="a811d-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a811d-115">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="a811d-115">What will you deploy?</span></span>

<span data-ttu-id="a811d-116">Met deze sjabloon implementeert u een Service Bus-naamruimte met onderwerp en een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a811d-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="a811d-117">[Service Bus-onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) biedt een een-op-veel-vorm van communicatie, in een *publiceren/abonneren* patroon.</span><span class="sxs-lookup"><span data-stu-id="a811d-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="a811d-118">Klik op de volgende knop om de implementatie automatisch uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a811d-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="a811d-119">[![Implementeren in Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a811d-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a811d-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="a811d-120">Parameters</span></span>

<span data-ttu-id="a811d-121">Met Azure Resource Manager kunt u parameters definiëren voor waarden die u wilt opgeven wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a811d-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a811d-122">De sjabloon bevat een sectie met de naam `Parameters` die de parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="a811d-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="a811d-123">U moet een parameter voor de waarden die variëren op basis van het project dat u wilt implementeren of op basis van de omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="a811d-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="a811d-124">Geen parameters op voor waarden die u altijd hetzelfde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a811d-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="a811d-125">De waarde van elke parameter wordt gebruikt in de sjabloon voor het definiëren van de resources die worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a811d-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="a811d-126">De sjabloon definieert de volgende parameters.</span><span class="sxs-lookup"><span data-stu-id="a811d-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="a811d-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a811d-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="a811d-128">De naam van de Service Bus-naamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="a811d-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="a811d-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="a811d-129">serviceBusTopicName</span></span>
<span data-ttu-id="a811d-130">De naam van het onderwerp in de Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a811d-130">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="a811d-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="a811d-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="a811d-132">De naam van het abonnement in de Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a811d-132">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="a811d-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="a811d-133">serviceBusApiVersion</span></span>
<span data-ttu-id="a811d-134">De Service Bus-API-versie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a811d-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="a811d-135">Resources om te implementeren</span><span class="sxs-lookup"><span data-stu-id="a811d-135">Resources to deploy</span></span>
<span data-ttu-id="a811d-136">Maakt een standaard Service Bus-naamruimte van het type **Messaging**, met het onderwerp en een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a811d-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a811d-137">Opdrachten om implementatie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="a811d-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="a811d-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a811d-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="a811d-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a811d-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="a811d-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a811d-140">Next steps</span></span>
<span data-ttu-id="a811d-141">Nu dat u hebt gemaakt en geïmplementeerd met Azure Resource Manager bronnen, meer informatie over deze resources beheren door deze artikelen te bekijken:</span><span class="sxs-lookup"><span data-stu-id="a811d-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="a811d-142">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="a811d-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="a811d-143">Service Bus-resources beheren met de Service Bus-Explorer</span><span class="sxs-lookup"><span data-stu-id="a811d-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
