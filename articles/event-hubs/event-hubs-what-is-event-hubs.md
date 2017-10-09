---
title: aaaWhat is Azure Event Hubs en waarom gebruiken | Microsoft Docs
description: Overzicht en inleiding tooAzure Event Hubs - Cloud-scale telemetrie opname van websites, apps en apparaten
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
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="0e7b5-103">Wat is Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="0e7b5-103">What is Event Hubs?</span></span>

<span data-ttu-id="0e7b5-104">Azure Event Hubs is een uiterst schaalbaar platform voor het streamen van gegevens en een gebeurtenisopneemservice die miljoenen gebeurtenissen per seconde kan opnemen en verwerken.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="0e7b5-105">Event Hubs kan gebeurtenissen, gegevens of telemetrie die wordt geproduceerd door gedistribueerde software en apparaten verwerken en opslaan.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="0e7b5-106">Gegevens verzonden tooan event hub kan worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="0e7b5-107">Met de Hallo mogelijkheid tooprovide [mogelijkheden voor publiceren / abonneren](https://msdn.microsoft.com/library/aa560414.aspx) met een lage latentie en zeer grote hoeveelheden Event Hubs fungeert als Hallo 'aan' ramp' voor Big Data.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="0e7b5-108">Het nut van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e7b5-108">Why use Event Hubs?</span></span>

<span data-ttu-id="0e7b5-109">De verwerkingsmogelijkheden voor gebeurtenissen en telemetrie van Event Hubs zijn ideaal voor:</span><span class="sxs-lookup"><span data-stu-id="0e7b5-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="0e7b5-110">Toepassingsinstrumentatie</span><span class="sxs-lookup"><span data-stu-id="0e7b5-110">Application instrumentation</span></span>
* <span data-ttu-id="0e7b5-111">Verwerking van gebruikerservaringen of werkstromen</span><span class="sxs-lookup"><span data-stu-id="0e7b5-111">User experience or workflow processing</span></span>
* <span data-ttu-id="0e7b5-112">Internet of Things (IoT)-scenario’s</span><span class="sxs-lookup"><span data-stu-id="0e7b5-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="0e7b5-113">Event Hubs maakt bijvoorbeeld het bijhouden van het gebruik van mobiele apps mogelijk, evenals het verzamelen van informatie over gegevensverkeer van web-farms, het vastleggen van spelgebeurtenissen in consolegames en het verzamelen van telemetriegegevens van industriële machines, verbonden voertuigen of andere apparaten.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="0e7b5-114">Overzicht van Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e7b5-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="0e7b5-115">Hallo algemene rol die Event Hubs in oplossingsarchitecturen speelt is Hallo 'voordeur' van een gebeurtenispijplijn vaak aangeduid als een *event ingestor*.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="0e7b5-116">Een event ingestor is een onderdeel of service die gebeurtenisuitgevers en gebeurtenis consumenten toodecouple Hallo productie van een stroom gebeurtenissen van Hallo gebruik van deze gebeurtenissen tussen.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="0e7b5-117">Hallo ziet volgende figuur deze architectuur:</span><span class="sxs-lookup"><span data-stu-id="0e7b5-117">hello following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="0e7b5-119">Event Hubs biedt de mogelijkheid voor het verwerken van een berichtenstroom, maar sommige van de kenmerken wijken af van wat u gewend bent bij traditionele zakelijke tools voor berichtenverzending.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="0e7b5-120">De mogelijkheden van Event Hubs zijn gebaseerd op maximale doorvoer en scenario's voor de verwerking van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="0e7b5-121">Als zodanig Event Hubs wijkt af van [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging en wordt niet geïmplementeerd voor een aantal Hallo-mogelijkheden die beschikbaar zijn voor [Service Bus-berichtenservice](/azure/service-bus-messaging/) entiteiten, zoals de onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="0e7b5-122">Functies van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e7b5-122">Event Hubs features</span></span>

<span data-ttu-id="0e7b5-123">Event Hubs Hallo volgen de belangrijkste elementen bevat:</span><span class="sxs-lookup"><span data-stu-id="0e7b5-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="0e7b5-124">[**Gebeurtenisuitgevers producenten**](event-hubs-features.md#event-publishers): een entiteit die gegevens tooan event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="0e7b5-125">Een gebeurtenis wordt gepubliceerd via AMQP 1.0 of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="0e7b5-126">[**Vastleggen**](event-hubs-features.md#capture): Hiermee kunt u toocapture Event Hubs gegevensstromen en op te slaan in een Azure Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="0e7b5-127">[**Partities**](event-hubs-features.md#partitions): Hiermee elke consumer tooonly lezen voor een specifieke subset of partitie van Hallo stroom gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="0e7b5-128">[**SAS-tokens**](event-hubs-features.md#sas-tokens): identificeert en Hallo gebeurtenisuitgever verifieert.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="0e7b5-129">[**Gebeurtenisconsumenten**](event-hubs-features.md#event-consumers): een entiteit die gebeurtenisgegevens van een gebeurtenishub leest.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="0e7b5-130">Gebeurtenisconsumenten maken verbinding via AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="0e7b5-131">[**Consumergroepen**](event-hubs-features.md#consumer-groups): biedt elk veelvoud toepassing met een afzonderlijke weergave van de gebeurtenisstroom Hallo verbruikt, die consumenten tooact afzonderlijk inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="0e7b5-132">[**Doorvoereenheden**](event-hubs-features.md#capacity): vooraf aangeschafte capaciteitseenheden.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="0e7b5-133">Per partitie is maximaal één doorvoereenheid mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="0e7b5-134">Zie voor technische informatie over deze en andere functies van Event Hubs Hallo [overzicht van Event Hubs functies](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="0e7b5-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0e7b5-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e7b5-135">Next steps</span></span>

<span data-ttu-id="0e7b5-136">Zie [Prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) voor gedetailleerde informatie over prijzen van Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0e7b5-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="0e7b5-137">Voor meer informatie over Event Hubs, gaat u naar Hallo koppelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0e7b5-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="0e7b5-138">Aan de slag met een [Event Hubs-zelfstudie](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="0e7b5-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="0e7b5-139">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e7b5-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="0e7b5-140">Voorbeeldtoepassingen die gebruikmaken van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0e7b5-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

