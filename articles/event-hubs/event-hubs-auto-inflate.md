---
title: aaaAutomatically opschaling van Azure Event Hubs doorvoereenheden | Microsoft Docs
description: Automatisch vergroten inschakelen op een schaal van de naamruimte tooautomatically doorvoer-eenheden
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="24189-103">Automatisch opschalen doorvoereenheden Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="24189-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="24189-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="24189-104">Overview</span></span>

<span data-ttu-id="24189-105">Azure Event Hubs is een uiterst schaalbare gegevens streaming-platform.</span><span class="sxs-lookup"><span data-stu-id="24189-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="24189-106">Event Hubs klanten verhogen als zodanig vaak hun gebruik na onboarding toohello service.</span><span class="sxs-lookup"><span data-stu-id="24189-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="24189-107">Dergelijke toeneemt vereisen toenemende Hallo zoekgedrag doorvoer eenheden (tabel) tooscale Event Hubs en grotere overdrachtssnelheid afhandelen.</span><span class="sxs-lookup"><span data-stu-id="24189-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="24189-108">Hallo *automatisch vergroten* functie van Event Hubs schaalt automatisch een Hallo aantal meer toomeet gebruik behoeften.</span><span class="sxs-lookup"><span data-stu-id="24189-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="24189-109">Verhogen van de tabel voorkomt dat scenario's waarin beperking:</span><span class="sxs-lookup"><span data-stu-id="24189-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="24189-110">Meer instellen gegevens inkomend tarieven overschrijden</span><span class="sxs-lookup"><span data-stu-id="24189-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="24189-111">Uitgaande gegevensaanvraag tarieven overschrijden meer instellen.</span><span class="sxs-lookup"><span data-stu-id="24189-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="24189-112">Hoe automatisch vergroten werkt</span><span class="sxs-lookup"><span data-stu-id="24189-112">How Auto-inflate works</span></span>

<span data-ttu-id="24189-113">Event Hubs-verkeer wordt geregeld door doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="24189-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="24189-114">Een enkele TU kunt 1 MB per seconde van inkomende en twee keer de omvang van uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="24189-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="24189-115">Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="24189-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="24189-116">Automatisch vergroten, kunt u toostart kleine met Hallo minimale vereiste doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="24189-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="24189-117">Hallo functie vervolgens schaalt automatisch toohello maximumlimiet van doorvoereenheden die u nodig hebt, afhankelijk van Hallo toename van het verkeer.</span><span class="sxs-lookup"><span data-stu-id="24189-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="24189-118">Automatisch vergroten biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="24189-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="24189-119">Een efficiënte vergroten/verkleinen mechanisme toostart klein en schaal omhoog als u groeien.</span><span class="sxs-lookup"><span data-stu-id="24189-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="24189-120">Automatisch schalen toohello opgegeven bovengrens zonder bandbreedteregeling problemen.</span><span class="sxs-lookup"><span data-stu-id="24189-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="24189-121">Meer controle over schalen, als u wanneer bepaalt en hoeveel tooscale.</span><span class="sxs-lookup"><span data-stu-id="24189-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="24189-122">Een naamruimte inschakelen automatisch vergroten</span><span class="sxs-lookup"><span data-stu-id="24189-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="24189-123">U kunt in- of uitschakelen van automatische vergroten voor een naamruimte met een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="24189-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="24189-124">Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24189-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="24189-125">Een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="24189-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="24189-126">Automatisch vergroten inschakelen via de portal Hallo</span><span class="sxs-lookup"><span data-stu-id="24189-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="24189-127">Bij het maken van een naamruimte Event Hubs, kunt u automatisch vergroten Hallo-functie op een naamruimte inschakelen:</span><span class="sxs-lookup"><span data-stu-id="24189-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="24189-128">Met deze optie is ingeschakeld, kunt u begin klein op uw doorvoereenheden en schaal omhoog wanneer gebruik van uw toename behoeften.</span><span class="sxs-lookup"><span data-stu-id="24189-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="24189-129">Hallo bovengrens voor inflatie heeft geen invloed op prijzen die afhankelijk is Hallo aantal meer per uur gebruikt.</span><span class="sxs-lookup"><span data-stu-id="24189-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="24189-130">U kunt ook inschakelen automatisch vergroten met Hallo **Scale** optie op de blade van Hallo-instellingen in Hallo-portal:</span><span class="sxs-lookup"><span data-stu-id="24189-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="24189-131">Schakel automatisch vergroten met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="24189-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="24189-132">U kunt automatisch vergroten inschakelen tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24189-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="24189-133">Bijvoorbeeld: set Hallo `isAutoInflateEnabled` eigenschap te**true** en stel `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="24189-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="24189-134">Zie voor de volledige sjabloon hello, Hallo [maken Event Hubs-naamruimte en schakel vergroten](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) sjabloon op GitHub.</span><span class="sxs-lookup"><span data-stu-id="24189-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24189-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24189-135">Next steps</span></span>

<span data-ttu-id="24189-136">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="24189-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="24189-137">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="24189-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="24189-138">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="24189-138">Create an Event Hub</span></span>](event-hubs-create.md)
