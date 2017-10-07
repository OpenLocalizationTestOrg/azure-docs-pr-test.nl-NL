---
title: aaaCreate Azure Service Bus-onderwerpabonnement en regel met behulp van Azure Resource Manager-sjabloon | Microsoft Docs
description: Een Service Bus-naamruimte maken met onderwerp, abonnement en regel met behulp van Azure Resource Manager-sjabloon
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="b38cd-103">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b38cd-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="b38cd-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een Service Bus-naamruimte met een onderwerp, abonnement en regel (filter).</span><span class="sxs-lookup"><span data-stu-id="b38cd-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="b38cd-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b38cd-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="b38cd-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten</span><span class="sxs-lookup"><span data-stu-id="b38cd-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="b38cd-107">Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b38cd-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="b38cd-108">Zie voor meer informatie over de praktijken en patronen op Azure-resources naamconventies [aanbevolen naamgevingsregels voor Azure-resources][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="b38cd-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="b38cd-109">Zie voor de volledige sjabloon hello, Hallo [Service Bus-naamruimte met onderwerp, abonnement en regel] [ Service Bus namespace with topic, subscription, and rule] sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b38cd-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="b38cd-110">Hallo na Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="b38cd-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="b38cd-111">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="b38cd-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="b38cd-112">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="b38cd-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="b38cd-113">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="b38cd-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="b38cd-114">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="b38cd-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="b38cd-115">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b38cd-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="b38cd-116">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="b38cd-116">What will you deploy?</span></span>

<span data-ttu-id="b38cd-117">Met deze sjabloon kunt u een Service Bus-naamruimte met onderwerp, abonnement en regel (filter) implementeren.</span><span class="sxs-lookup"><span data-stu-id="b38cd-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="b38cd-118">[Service Bus-onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) biedt een een-op-veel-vorm van communicatie, in een *publiceren/abonneren* patroon.</span><span class="sxs-lookup"><span data-stu-id="b38cd-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="b38cd-119">Bij gebruik van onderwerpen en abonnementen, communiceren onderdelen van een gedistribueerde toepassing niet direct met elkaar, in plaats daarvan wisselen ze berichten uit via een onderwerp dat als intermediair fungeert. Een abonnement tooa onderwerp lijkt op een virtuele wachtrij die kopieën van berichten die zijn verzonden toohello onderwerp ontvangt.</span><span class="sxs-lookup"><span data-stu-id="b38cd-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="b38cd-120">Een filter op abonnement kunt u toospecify welke berichten verzonden tooa onderwerp moet worden weergegeven binnen een bepaald onderwerpabonnement.</span><span class="sxs-lookup"><span data-stu-id="b38cd-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="b38cd-121">Wat zijn de regels (filters)?</span><span class="sxs-lookup"><span data-stu-id="b38cd-121">What are rules (filters)?</span></span>

<span data-ttu-id="b38cd-122">In veel scenario's, moeten de berichten met specifieke kenmerken op verschillende manieren worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b38cd-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="b38cd-123">tooenable, kunt u abonnementen toofind berichten die specifieke eigenschappen hebben en voert u de wijzigingen toothose eigenschappen configureren.</span><span class="sxs-lookup"><span data-stu-id="b38cd-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="b38cd-124">Hoewel Service Bus-abonnementen alle berichten die verstuurd toohello onderwerp zien, kunt u alleen een subset van deze wachtrij berichten toohello virtuele abonnement kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b38cd-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="b38cd-125">Dit wordt bereikt met behulp van abonnementsfilters.</span><span class="sxs-lookup"><span data-stu-id="b38cd-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="b38cd-126">toolearn meer informatie over regels (filters), Zie [regels en acties](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="b38cd-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="b38cd-127">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="b38cd-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="b38cd-128">[![TooAzure implementeren](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b38cd-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b38cd-129">Parameters</span><span class="sxs-lookup"><span data-stu-id="b38cd-129">Parameters</span></span>

<span data-ttu-id="b38cd-130">Met Azure Resource Manager, moet u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b38cd-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="b38cd-131">Hallo-sjabloon bevat een sectie met de naam `Parameters` die alle Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="b38cd-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="b38cd-132">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="b38cd-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="b38cd-133">Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="b38cd-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="b38cd-134">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b38cd-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="b38cd-135">Hallo sjabloon definieert Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="b38cd-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="b38cd-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="b38cd-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="b38cd-137">Hallo-naam van Hallo Service Bus-naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="b38cd-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="b38cd-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="b38cd-138">serviceBusTopicName</span></span>
<span data-ttu-id="b38cd-139">Hallo-naam van Hallo onderwerp in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b38cd-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="b38cd-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="b38cd-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="b38cd-141">Hallo-naam van het Hallo-abonnement in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b38cd-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="b38cd-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="b38cd-142">serviceBusRuleName</span></span>
<span data-ttu-id="b38cd-143">Hallo-naam van Hallo rule(filter) in Hallo Service Bus-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b38cd-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="b38cd-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="b38cd-144">serviceBusApiVersion</span></span>
<span data-ttu-id="b38cd-145">Hallo Service Bus-API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b38cd-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="b38cd-146">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="b38cd-146">Resources toodeploy</span></span>
<span data-ttu-id="b38cd-147">Maakt een standaard Service Bus-naamruimte van het type **Messaging**, onderwerp, abonnement en regels.</span><span class="sxs-lookup"><span data-stu-id="b38cd-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="b38cd-148">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="b38cd-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="b38cd-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b38cd-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="b38cd-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b38cd-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="b38cd-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b38cd-151">Next steps</span></span>
<span data-ttu-id="b38cd-152">Nu u hebt gemaakt en geïmplementeerd resources met behulp van Azure Resource Manager, kunt u nagaan hoe toomanage deze resources aan de hand van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="b38cd-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="b38cd-153">Azure Servicebus beheren</span><span class="sxs-lookup"><span data-stu-id="b38cd-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="b38cd-154">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="b38cd-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="b38cd-155">Service Bus-resources beheren met Hallo Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="b38cd-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

