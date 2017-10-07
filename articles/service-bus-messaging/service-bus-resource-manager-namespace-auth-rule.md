---
title: aaaCreate Service Bus-autorisatieregel met Azure Resource Manager-sjabloon | Microsoft Docs
description: Een Service Bus-autorisatieregel voor de naamruimte en de wachtrij met Azure Resource Manager-sjabloon maken
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="33a0b-103">Een Service Bus-autorisatieregel voor de naamruimte en de wachtrij met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="33a0b-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="33a0b-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een [autorisatieregel](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) voor een Service Bus-naamruimte en de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="33a0b-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="33a0b-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="33a0b-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="33a0b-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="33a0b-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="33a0b-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="33a0b-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="33a0b-108">Zie voor de volledige sjabloon hello, Hallo [Service Bus autorisatie regelsjabloon] [ Service Bus auth rule template] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="33a0b-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="33a0b-109">Hallo na Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="33a0b-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="33a0b-110">Een Service Bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="33a0b-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="33a0b-111">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="33a0b-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="33a0b-112">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="33a0b-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="33a0b-113">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="33a0b-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="33a0b-114">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar 'Servicebus'.</span><span class="sxs-lookup"><span data-stu-id="33a0b-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="33a0b-115">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="33a0b-115">What will you deploy?</span></span>
<span data-ttu-id="33a0b-116">Met deze sjabloon implementeert u een Service Bus-autorisatieregel voor een naamruimte en Berichtentiteit (in dit geval een wachtrij).</span><span class="sxs-lookup"><span data-stu-id="33a0b-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="33a0b-117">Maakt gebruik van deze sjabloon [Shared Access Signature (SAS)](service-bus-sas.md) voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="33a0b-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="33a0b-118">SAS kan toepassingen tooauthenticate tooService Bus met behulp van een toegangssleutel die is geconfigureerd op Hallo naamruimte of op Hallo messaging-entiteit (wachtrij of onderwerp) met welke specifieke rechten gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="33a0b-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="33a0b-119">Vervolgens kunt u deze sleutel toogenerate een SAS-token dat clients op zijn beurt tooauthenticate tooService Bus kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33a0b-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="33a0b-120">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="33a0b-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="33a0b-121">[![TooAzure implementeren](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="33a0b-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="33a0b-122">Parameters</span><span class="sxs-lookup"><span data-stu-id="33a0b-122">Parameters</span></span>

<span data-ttu-id="33a0b-123">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="33a0b-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="33a0b-124">Hallo-sjabloon bevat een sectie met de naam `Parameters` die Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="33a0b-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="33a0b-125">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="33a0b-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="33a0b-126">Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="33a0b-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="33a0b-127">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="33a0b-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="33a0b-128">Hallo sjabloon definieert Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="33a0b-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="33a0b-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="33a0b-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="33a0b-130">Hallo-naam van Hallo Service Bus-naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="33a0b-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="33a0b-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="33a0b-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="33a0b-132">Hallo de naam van de autorisatieregel Hallo voor Hallo naamruimte.</span><span class="sxs-lookup"><span data-stu-id="33a0b-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="33a0b-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="33a0b-133">serviceBusQueueName</span></span>
<span data-ttu-id="33a0b-134">Hallo-naam van Hallo wachtrij in Hallo Service Bus-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="33a0b-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="33a0b-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="33a0b-135">serviceBusApiVersion</span></span>
<span data-ttu-id="33a0b-136">Hallo Service Bus-API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="33a0b-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="33a0b-137">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="33a0b-137">Resources toodeploy</span></span>
<span data-ttu-id="33a0b-138">Maakt een standaard Service Bus-naamruimte van het type **Messaging**, en een Service Bus-autorisatieregel voor de naamruimte en de entiteit.</span><span class="sxs-lookup"><span data-stu-id="33a0b-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="33a0b-139">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="33a0b-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="33a0b-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33a0b-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="33a0b-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33a0b-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="33a0b-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33a0b-142">Next steps</span></span>
<span data-ttu-id="33a0b-143">Nu u hebt gemaakt en geïmplementeerd resources met behulp van Azure Resource Manager, kunt u nagaan hoe toomanage deze resources aan de hand van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="33a0b-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="33a0b-144">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="33a0b-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="33a0b-145">Service Bus-resources beheren met Hallo Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="33a0b-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="33a0b-146">Service Bus-verificatie en autorisatie</span><span class="sxs-lookup"><span data-stu-id="33a0b-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
