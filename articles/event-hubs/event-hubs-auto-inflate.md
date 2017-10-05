---
title: Automatisch opschalen doorvoereenheden Azure Event Hubs | Microsoft Docs
description: Een naamruimte worden automatisch uitgebreid doorvoereenheden inschakelen automatisch vergroten
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
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="ec933-103">Automatisch opschalen doorvoereenheden Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ec933-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="ec933-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ec933-104">Overview</span></span>

<span data-ttu-id="ec933-105">Azure Event Hubs is een uiterst schaalbare gegevens streaming-platform.</span><span class="sxs-lookup"><span data-stu-id="ec933-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="ec933-106">Event Hubs klanten verhogen als zodanig vaak hun gebruik na het voorbereiden van de service.</span><span class="sxs-lookup"><span data-stu-id="ec933-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="ec933-107">Dergelijke toeneemt, moet u de vooraf ingestelde doorvoereenheden (tabel) Event Hubs schalen en te verwerken groter overdrachtssnelheid meer.</span><span class="sxs-lookup"><span data-stu-id="ec933-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="ec933-108">De *automatisch vergroten* functie van Event Hubs schaalt automatisch het aantal meer om te voldoen aan moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec933-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="ec933-109">Verhogen van de tabel voorkomt dat scenario's waarin beperking:</span><span class="sxs-lookup"><span data-stu-id="ec933-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="ec933-110">Meer instellen gegevens inkomend tarieven overschrijden</span><span class="sxs-lookup"><span data-stu-id="ec933-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="ec933-111">Uitgaande gegevensaanvraag tarieven overschrijden meer instellen.</span><span class="sxs-lookup"><span data-stu-id="ec933-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="ec933-112">Hoe automatisch vergroten werkt</span><span class="sxs-lookup"><span data-stu-id="ec933-112">How Auto-inflate works</span></span>

<span data-ttu-id="ec933-113">Event Hubs-verkeer wordt geregeld door doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="ec933-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="ec933-114">Een enkele TU kunt 1 MB per seconde van inkomende en twee keer de omvang van uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="ec933-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="ec933-115">Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="ec933-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="ec933-116">Automatisch vergroten, kunt u met de minimale vereiste doorvoereenheden klein beginnen.</span><span class="sxs-lookup"><span data-stu-id="ec933-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="ec933-117">De functie wordt vervolgens automatisch geschaald naar het maximum aantal doorvoereenheden die u nodig hebt, afhankelijk van de toename van het verkeer.</span><span class="sxs-lookup"><span data-stu-id="ec933-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="ec933-118">Automatisch vergroten biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ec933-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="ec933-119">Een efficiënte vergroten/verkleinen mechanisme voor het begin klein en schaal omhoog wanneer u groeit.</span><span class="sxs-lookup"><span data-stu-id="ec933-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="ec933-120">Automatisch schalen in de opgegeven bovengrens zonder problemen beperking.</span><span class="sxs-lookup"><span data-stu-id="ec933-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="ec933-121">Meer controle over het schalen, als u wanneer bepaalt en hoeveel op schaal.</span><span class="sxs-lookup"><span data-stu-id="ec933-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="ec933-122">Een naamruimte inschakelen automatisch vergroten</span><span class="sxs-lookup"><span data-stu-id="ec933-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="ec933-123">U kunt in- of uitschakelen van automatische vergroten voor een naamruimte met een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="ec933-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="ec933-124">De [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec933-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec933-125">Een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ec933-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="ec933-126">Automatisch vergroten inschakelen via de portal</span><span class="sxs-lookup"><span data-stu-id="ec933-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="ec933-127">U kunt de functie automatisch vergroten op een naamruimte inschakelen bij het maken van een Event Hubs-naamruimte:</span><span class="sxs-lookup"><span data-stu-id="ec933-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="ec933-128">Met deze optie is ingeschakeld, kunt u begin klein op uw doorvoereenheden en schaal omhoog wanneer gebruik van uw toename behoeften.</span><span class="sxs-lookup"><span data-stu-id="ec933-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="ec933-129">De bovengrens voor inflatie heeft geen invloed op prijzen die afhankelijk is het aantal meer per uur gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ec933-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="ec933-130">U kunt ook inschakelen automatisch vergroten met behulp van de **Scale** optie op de instellingenblade in de portal:</span><span class="sxs-lookup"><span data-stu-id="ec933-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="ec933-131">Schakel automatisch vergroten met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="ec933-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="ec933-132">U kunt automatisch vergroten inschakelen tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec933-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="ec933-133">Bijvoorbeeld, stelt de `isAutoInflateEnabled` eigenschap **true** en stel `maximumThroughputUnits` tot en met 10.</span><span class="sxs-lookup"><span data-stu-id="ec933-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

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

<span data-ttu-id="ec933-134">Zie voor de volledige sjabloon, het [maken Event Hubs-naamruimte en schakel vergroten](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) sjabloon op GitHub.</span><span class="sxs-lookup"><span data-stu-id="ec933-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec933-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec933-135">Next steps</span></span>

<span data-ttu-id="ec933-136">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="ec933-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ec933-137">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="ec933-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ec933-138">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="ec933-138">Create an Event Hub</span></span>](event-hubs-create.md)
