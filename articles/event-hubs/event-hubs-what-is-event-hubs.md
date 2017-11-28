---
title: Wat is Azure Event Hubs en waarom is het nuttig | Microsoft Docs
description: Overzicht van en inleiding tot Azure Event Hubs - Telemetrie van websites, apps en apparaten op cloudniveau opnemen
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: 1a6bf0a0352e6d9e3a22586ac825558d12e1307a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="70941-103">Wat is Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="70941-103">What is Event Hubs?</span></span>

<span data-ttu-id="70941-104">Azure Event Hubs is een uiterst schaalbaar platform voor het streamen van gegevens en een gebeurtenisopneemservice die miljoenen gebeurtenissen per seconde kan opnemen en verwerken.</span><span class="sxs-lookup"><span data-stu-id="70941-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="70941-105">Event Hubs kan gebeurtenissen, gegevens of telemetrie die wordt geproduceerd door gedistribueerde software en apparaten verwerken en opslaan.</span><span class="sxs-lookup"><span data-stu-id="70941-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="70941-106">Gegevens die naar een Event Hub worden verzonden, kunnen worden omgezet en opgeslagen via een provider voor realtime analytische gegevens of batchverwerking/opslagadapters.</span><span class="sxs-lookup"><span data-stu-id="70941-106">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="70941-107">Event Hubs biedt mogelijkheden voor klein- en grootschalige scenario’s voor [publiceren/abonneren](https://msdn.microsoft.com/library/aa560414.aspx). Hierbij fungeert de service als toegangspunt voor big data.</span><span class="sxs-lookup"><span data-stu-id="70941-107">With the ability to provide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="70941-108">Het nut van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="70941-108">Why use Event Hubs?</span></span>

<span data-ttu-id="70941-109">De verwerkingsmogelijkheden voor gebeurtenissen en telemetrie van Event Hubs zijn ideaal voor:</span><span class="sxs-lookup"><span data-stu-id="70941-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="70941-110">Toepassingsinstrumentatie</span><span class="sxs-lookup"><span data-stu-id="70941-110">Application instrumentation</span></span>
* <span data-ttu-id="70941-111">Verwerking van gebruikerservaringen of werkstromen</span><span class="sxs-lookup"><span data-stu-id="70941-111">User experience or workflow processing</span></span>
* <span data-ttu-id="70941-112">Internet of Things (IoT)-scenario’s</span><span class="sxs-lookup"><span data-stu-id="70941-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="70941-113">Event Hubs maakt bijvoorbeeld het bijhouden van het gebruik van mobiele apps mogelijk, evenals het verzamelen van informatie over gegevensverkeer van web-farms, het vastleggen van spelgebeurtenissen in consolegames en het verzamelen van telemetriegegevens van industriële machines, verbonden voertuigen of andere apparaten.</span><span class="sxs-lookup"><span data-stu-id="70941-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="70941-114">Overzicht van Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="70941-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="70941-115">De algemene rol die Event Hubs in oplossingsarchitecturen speelt, is die van 'voordeur' van een gebeurtenispijplijn. We spreken ook wel van een *event ingestor*.</span><span class="sxs-lookup"><span data-stu-id="70941-115">The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="70941-116">Een event ingestor is een onderdeel dat of een service die zich tussen gebeurtenisuitgever en gebeurtenisconsumer bevindt en de productie van de gebeurtenisstroom loskoppelt van het gebruik van de betreffende gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="70941-116">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="70941-117">U ziet deze architectuur in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="70941-117">The following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="70941-119">Event Hubs biedt de mogelijkheid voor het verwerken van een berichtenstroom, maar sommige van de kenmerken wijken af van wat u gewend bent bij traditionele zakelijke tools voor berichtenverzending.</span><span class="sxs-lookup"><span data-stu-id="70941-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="70941-120">De mogelijkheden van Event Hubs zijn gebaseerd op maximale doorvoer en scenario's voor de verwerking van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="70941-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="70941-121">Event Hubs wijkt af van [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)-messaging en implementeert niet alle berichtenmogelijkheden die beschikbaar zijn voor [Service Bus messaging](/azure/service-bus-messaging/)-entiteiten, zoals onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="70941-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of the capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="70941-122">Functies van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="70941-122">Event Hubs features</span></span>

<span data-ttu-id="70941-123">Event Hubs bevat de volgende belangrijke elementen:</span><span class="sxs-lookup"><span data-stu-id="70941-123">Event Hubs contains the following key elements:</span></span>

- <span data-ttu-id="70941-124">[**Gebeurtenisproducent/-uitgever**](event-hubs-features.md#event-publishers): dit is een entiteit die gegevens naar een gebeurtenishub verzendt.</span><span class="sxs-lookup"><span data-stu-id="70941-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data to an event hub.</span></span> <span data-ttu-id="70941-125">Een gebeurtenis wordt gepubliceerd via AMQP 1.0 of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="70941-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="70941-126">[**Vastleggen**](event-hubs-features.md#capture): hiermee kunt u streaminggegevens van gebeurtenishubs vastleggen en opslaan in een Azure Blob-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="70941-126">[**Capture**](event-hubs-features.md#capture): Enables you to capture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="70941-127">[**Partities**](event-hubs-features.md#partitions): hiermee kan elke consument alleen een specifieke subset, of partitie, van de gebeurtenisstroom lezen.</span><span class="sxs-lookup"><span data-stu-id="70941-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer to only read a specific subset, or partition, of the event stream.</span></span>
- <span data-ttu-id="70941-128">[**SAS-tokens**](event-hubs-features.md#sas-tokens): voor het identificeren en verifiëren van de gebeurtenisuitgever.</span><span class="sxs-lookup"><span data-stu-id="70941-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates the event publisher.</span></span>
- <span data-ttu-id="70941-129">[**Gebeurtenisconsumenten**](event-hubs-features.md#event-consumers): een entiteit die gebeurtenisgegevens van een gebeurtenishub leest.</span><span class="sxs-lookup"><span data-stu-id="70941-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="70941-130">Gebeurtenisconsumenten maken verbinding via AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="70941-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="70941-131">[**Consumentengroepen**](event-hubs-features.md#consumer-groups): biedt elke veelvoudige verbruikstoepassing een afzonderlijke weergave van de gebeurtenisstroom, waardoor deze consumenten onafhankelijk kunnen reageren.</span><span class="sxs-lookup"><span data-stu-id="70941-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of the event stream, enabling those consumers to act independently.</span></span>
- <span data-ttu-id="70941-132">[**Doorvoereenheden**](event-hubs-features.md#capacity): vooraf aangeschafte capaciteitseenheden.</span><span class="sxs-lookup"><span data-stu-id="70941-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="70941-133">Per partitie is maximaal één doorvoereenheid mogelijk.</span><span class="sxs-lookup"><span data-stu-id="70941-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="70941-134">Zie voor technische informatie over deze en andere functies van Event Hubs het [Overzicht van functies voor Event Hubs](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="70941-134">For technical details about these and other Event Hubs features, see the [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="70941-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70941-135">Next steps</span></span>

<span data-ttu-id="70941-136">Zie [Prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) voor gedetailleerde informatie over prijzen van Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="70941-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="70941-137">Voor meer informatie over Event Hubs gaat u naar de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="70941-137">For more information about Event Hubs, visit the following links:</span></span>

* <span data-ttu-id="70941-138">Aan de slag met een [Event Hubs-zelfstudie](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="70941-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="70941-139">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="70941-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="70941-140">Voorbeeldtoepassingen die gebruikmaken van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="70941-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

