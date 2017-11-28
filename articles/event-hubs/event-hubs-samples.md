---
title: Voorbeelden van Azure Event Hubs | Microsoft Docs
description: Azure Event Hubs-voorbeelden
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="c4e29-103">Voorbeelden van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c4e29-103">Event Hubs samples</span></span> 

<span data-ttu-id="c4e29-104">De set van Azure Event Hubs-voorbeelden worden de belangrijkste functies in [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c4e29-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="c4e29-105">In dit artikel, ingedeeld en beschrijft de voorbeelden die beschikbaar is, met koppelingen naar elk.</span><span class="sxs-lookup"><span data-stu-id="c4e29-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="c4e29-106">Op het moment van schrijven van dit zijn voorbeelden van Event Hubs bevinden zich op verschillende plaatsen:</span><span class="sxs-lookup"><span data-stu-id="c4e29-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="c4e29-107">MSDN developer-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="c4e29-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="c4e29-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="c4e29-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="c4e29-109">Zie voor meer informatie over de verschillende versies van .NET Framework [Frameworks en doelen](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="c4e29-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="c4e29-110">Meer voorbeelden worden toegevoegd na verloop van tijd, dus Kijk regelmatig op updates.</span><span class="sxs-lookup"><span data-stu-id="c4e29-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="c4e29-111">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="c4e29-111">.NET Standard</span></span>

<span data-ttu-id="c4e29-112">De volgende voorbeelden laten zien hoe u verzenden en ontvangen van gebeurtenissen met de [Event Hubs-client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) voor de [standaard .NET-bibliotheek](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="c4e29-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="c4e29-113">Gebeurtenissen verzenden</span><span class="sxs-lookup"><span data-stu-id="c4e29-113">Send events</span></span> 

<span data-ttu-id="c4e29-114">De [verzenden aan de slag](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) voorbeeld laat zien hoe u schrijft een .NET Core-consoletoepassing die gebeurtenissen naar een event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="c4e29-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="c4e29-115">Gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="c4e29-115">Receive events</span></span> 

<span data-ttu-id="c4e29-116">De [aan de slag met het Event Processor Host ontvangen](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) voorbeeld is een .NET Core-consoletoepassing die berichten ontvangt van een event hub met behulp van de Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="c4e29-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="c4e29-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="c4e29-117">.NET Framework</span></span>   

<span data-ttu-id="c4e29-118">Deze voorbeelden demonstreren verschillende andere functies van Azure Event Hubs, die gericht is op de [.NET Framework-bibliotheek](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="c4e29-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="c4e29-119">Waarschuw gebruikers van gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="c4e29-119">Notify users of events received</span></span>

<span data-ttu-id="c4e29-120">De [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) voorbeeld waarschuwt gebruikers gegevens ontvangen van sensoren of andere systemen.</span><span class="sxs-lookup"><span data-stu-id="c4e29-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="c4e29-121">Aan de slag met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c4e29-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="c4e29-122">De [Event Hubs aan de slag](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) voorbeeld demonstreert essentiële mogelijkheden van Event Hubs, zoals het maken van een event hub, gebeurtenissen verzenden naar een event hub en gebruiken van gebeurtenissen met de [Gebeurtenisprocessorhost](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) .</span><span class="sxs-lookup"><span data-stu-id="c4e29-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="c4e29-123">Verwerking van de gebeurtenis uitschalen</span><span class="sxs-lookup"><span data-stu-id="c4e29-123">Scale out event processing</span></span> 

<span data-ttu-id="c4e29-124">De [Scale-out gebeurtenisverwerking](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) voorbeeld laat zien hoe u de [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) voor het distribueren van de werkbelasting van Event Hubs stroom verbruik.</span><span class="sxs-lookup"><span data-stu-id="c4e29-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="c4e29-125">Er wordt weergegeven hoe voor het implementeren van de **EventProcessor** en **EventProcessorFactory** objecten voor het beheren van de gebeurtenisstroom.</span><span class="sxs-lookup"><span data-stu-id="c4e29-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="c4e29-126">Ophalen van gegevens uit SQL in een event hub</span><span class="sxs-lookup"><span data-stu-id="c4e29-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="c4e29-127">De [binnenhalen van SQL-gegevens](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) voorbeeld laat zien hoe u gegevens ophalen uit een SQL-tabel en dit doorgeven aan een event hub, moet worden gebruikt als invoer in downstream analytische toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c4e29-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="c4e29-128">Pull-web-gegevens in een event hub</span><span class="sxs-lookup"><span data-stu-id="c4e29-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="c4e29-129">De [gegevens importeren uit het web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) voorbeeld laat zien hoe u gegevens ophalen uit de openbare feeds (zoals het vervoer afdeling verkeer informatie feed) en dit doorgeven aan een event hub.</span><span class="sxs-lookup"><span data-stu-id="c4e29-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4e29-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4e29-130">Next steps</span></span>

<span data-ttu-id="c4e29-131">Meer informatie over de versies van .NET Framework via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="c4e29-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="c4e29-132">Frameworks en doelen</span><span class="sxs-lookup"><span data-stu-id="c4e29-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="c4e29-133">.NET framework 4.6 en 4.5</span><span class="sxs-lookup"><span data-stu-id="c4e29-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="c4e29-134">U kunt meer informatie over Event Hubs in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="c4e29-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="c4e29-135">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="c4e29-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="c4e29-136">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="c4e29-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="c4e29-137">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c4e29-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)