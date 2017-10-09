---
title: een Azure Event Hubs-naamruimte en de consument een groep met een sjabloon aaaCreate | Microsoft Docs
description: Een Event Hubs-naamruimte maken met een event hub en een consumergroep met behulp van Azure Resource Manager-sjablonen
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="9f4f6-103">Een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="9f4f6-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="9f4f6-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een naamruimte van het type Event Hubs met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="9f4f6-105">Hallo toont hoe artikel toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="9f4f6-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten</span><span class="sxs-lookup"><span data-stu-id="9f4f6-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="9f4f6-107">Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="9f4f6-108">Zie voor de volledige sjabloon hello, Hallo [Event hub- en groep sjabloon] [ Event Hub and consumer group template] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="9f4f6-109">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="9f4f6-110">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="9f4f6-110">What will you deploy?</span></span>
<span data-ttu-id="9f4f6-111">Met deze sjabloon implementeert u een Event Hubs-naamruimte met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="9f4f6-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is een service die wordt gebruikt tooprovide gebeurtenissen en telemetriegegevens inkomend tooAzure op grote schaal met weinig latentie en hoge betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="9f4f6-113">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9f4f6-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="9f4f6-114">[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9f4f6-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="9f4f6-115">Parameters</span><span class="sxs-lookup"><span data-stu-id="9f4f6-115">Parameters</span></span>
<span data-ttu-id="9f4f6-116">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="9f4f6-117">Hallo-sjabloon bevat een sectie met de naam `Parameters` die alle Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="9f4f6-118">Een parameter voor de waarden die variëren, op basis van Hallo-project die u implementeert of op basis van Hallo omgeving toowhich die u implementeert, moet u definiëren.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="9f4f6-119">Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="9f4f6-120">Elke parameterwaarde in Hallo sjabloon definieert Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="9f4f6-121">Hallo sjabloon definieert Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="9f4f6-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="9f4f6-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="9f4f6-122">eventHubNamespaceName</span></span>
<span data-ttu-id="9f4f6-123">Hallo-naam van Hallo Event Hubs naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="9f4f6-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="9f4f6-124">eventHubName</span></span>
<span data-ttu-id="9f4f6-125">Hallo-naam van Hallo event hub in Hallo Event Hubs-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="9f4f6-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="9f4f6-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="9f4f6-127">Hallo-naam van consumentengroep Hallo voor Hallo event hub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="9f4f6-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9f4f6-128">apiVersion</span></span>
<span data-ttu-id="9f4f6-129">Hallo API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="9f4f6-130">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="9f4f6-130">Resources toodeploy</span></span>
<span data-ttu-id="9f4f6-131">Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="9f4f6-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="9f4f6-132">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="9f4f6-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="9f4f6-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f4f6-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="9f4f6-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9f4f6-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="9f4f6-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f4f6-135">Next steps</span></span>
<span data-ttu-id="9f4f6-136">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9f4f6-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9f4f6-137">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="9f4f6-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9f4f6-138">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="9f4f6-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="9f4f6-139">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9f4f6-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
