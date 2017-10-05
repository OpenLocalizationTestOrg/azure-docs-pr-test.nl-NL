---
title: Een Azure Event Hubs-naamruimte en de consumer-groep met een sjabloon maken | Microsoft Docs
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
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="2e7b7-103">Een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="2e7b7-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="2e7b7-104">Dit artikel laat zien hoe u een Azure Resource Manager-sjabloon die wordt gemaakt van een naamruimte van het type Event Hubs met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="2e7b7-105">Het artikel ziet u hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="2e7b7-106">U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen</span><span class="sxs-lookup"><span data-stu-id="2e7b7-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="2e7b7-107">Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="2e7b7-108">Zie voor de volledige sjabloon, het [Event hub- en groep sjabloon] [ Event Hub and consumer group template] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="2e7b7-109">Om te controleren op de meest recente sjablonen, gaat u naar de galerie [Azure-snelstartsjablonen][Azure Quickstart Templates] en zoekt u naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="2e7b7-110">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="2e7b7-110">What will you deploy?</span></span>
<span data-ttu-id="2e7b7-111">Met deze sjabloon implementeert u een Event Hubs-naamruimte met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="2e7b7-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is een verwerkingsservice van gebeurtenissen, die wordt gebruikt om zeer grote hoeveelheden gebeurtenissen en telemetriegegevens verzamelt in Azure met een lage latentie en hoge betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="2e7b7-113">Klik op de volgende knop om de implementatie automatisch uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2e7b7-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="2e7b7-114">[![Implementeren in Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2e7b7-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="2e7b7-115">Parameters</span><span class="sxs-lookup"><span data-stu-id="2e7b7-115">Parameters</span></span>
<span data-ttu-id="2e7b7-116">Met Azure Resource Manager kunt u parameters definiëren voor waarden die u wilt opgeven wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="2e7b7-117">De sjabloon bevat een sectie met de naam `Parameters` die alle parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="2e7b7-118">Een parameter voor de waarden die variëren, op basis van het project dat u wilt implementeren of op basis van de omgeving waarnaar u implementeert, moet u definiëren.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="2e7b7-119">Definieer geen parameters voor waarden die altijd hetzelfde blijven.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="2e7b7-120">De parameterwaarde van elke in de sjabloon definieert de resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="2e7b7-121">De sjabloon definieert de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="2e7b7-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="2e7b7-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="2e7b7-122">eventHubNamespaceName</span></span>
<span data-ttu-id="2e7b7-123">De naam van de Event Hubs-naamruimte die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="2e7b7-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="2e7b7-124">eventHubName</span></span>
<span data-ttu-id="2e7b7-125">De naam van de gebeurtenishub die in de Event Hubs-naamruimte wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="2e7b7-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="2e7b7-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="2e7b7-127">De naam van de consumergroep gemaakt voor de event hub.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="2e7b7-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2e7b7-128">apiVersion</span></span>
<span data-ttu-id="2e7b7-129">De API-versie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="2e7b7-130">Resources om te implementeren</span><span class="sxs-lookup"><span data-stu-id="2e7b7-130">Resources to deploy</span></span>
<span data-ttu-id="2e7b7-131">Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en een consumergroep.</span><span class="sxs-lookup"><span data-stu-id="2e7b7-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="2e7b7-132">Opdrachten om implementatie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="2e7b7-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="2e7b7-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e7b7-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="2e7b7-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2e7b7-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="2e7b7-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e7b7-135">Next steps</span></span>
<span data-ttu-id="2e7b7-136">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="2e7b7-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="2e7b7-137">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="2e7b7-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2e7b7-138">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="2e7b7-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="2e7b7-139">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2e7b7-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
