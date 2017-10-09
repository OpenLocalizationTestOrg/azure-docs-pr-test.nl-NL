---
title: Voorbeelden van aaaAzure Event Hubs | Microsoft Docs
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
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="a364a-103">Voorbeelden van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a364a-103">Event Hubs samples</span></span> 

<span data-ttu-id="a364a-104">Hallo reeks voorbeelden van Azure Event Hubs wordt gedemonstreerd belangrijke functies in [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a364a-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="a364a-105">In dit artikel wordt ingedeeld en Hallo voorbeelden beschikbaar is, met koppelingen tooeach beschrijft.</span><span class="sxs-lookup"><span data-stu-id="a364a-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="a364a-106">Op Hallo moment van schrijven van dit zijn voorbeelden van Event Hubs bevinden zich op verschillende plaatsen:</span><span class="sxs-lookup"><span data-stu-id="a364a-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="a364a-107">MSDN developer-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="a364a-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="a364a-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="a364a-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="a364a-109">Zie voor meer informatie over de verschillende versies van .NET Framework Hallo [Frameworks en doelen](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="a364a-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="a364a-110">Meer voorbeelden worden toegevoegd na verloop van tijd, dus Kijk regelmatig op updates.</span><span class="sxs-lookup"><span data-stu-id="a364a-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="a364a-111">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="a364a-111">.NET Standard</span></span>

<span data-ttu-id="a364a-112">Hallo volgende voorbeelden laten zien hoe toosend en ontvangen van gebeurtenissen met Hallo [Event Hubs-client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) voor Hallo [standaard .NET-bibliotheek](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="a364a-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="a364a-113">Gebeurtenissen verzenden</span><span class="sxs-lookup"><span data-stu-id="a364a-113">Send events</span></span> 

<span data-ttu-id="a364a-114">Hallo [verzenden aan de slag](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) voorbeeld laat zien hoe een .NET Core toowrite consoletoepassing die gebeurtenissen tooan event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a364a-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="a364a-115">Gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="a364a-115">Receive events</span></span> 

<span data-ttu-id="a364a-116">Hallo [aan de slag met Hallo Event Processor Host ontvangen](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) voorbeeld is een .NET Core-consoletoepassing die berichten ontvangt van een event hub met Hallo Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="a364a-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="a364a-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="a364a-117">.NET Framework</span></span>   

<span data-ttu-id="a364a-118">Deze voorbeelden demonstreren verschillende andere functies van Azure Event Hubs, die gericht is op Hallo [.NET Framework-bibliotheek](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="a364a-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="a364a-119">Waarschuw gebruikers van gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="a364a-119">Notify users of events received</span></span>

<span data-ttu-id="a364a-120">Hallo [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) voorbeeld waarschuwt gebruikers gegevens ontvangen van sensoren of andere systemen.</span><span class="sxs-lookup"><span data-stu-id="a364a-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="a364a-121">Aan de slag met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a364a-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="a364a-122">Hallo [Event Hubs aan de slag](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) voorbeeld demonstreert Hallo essentiële mogelijkheden van Event Hubs, zoals hoe toocreate een event hub, gebeurtenissen tooan event hub te verzenden en gebruiken van gebeurtenissen met Hallo [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="a364a-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="a364a-123">Verwerking van de gebeurtenis uitschalen</span><span class="sxs-lookup"><span data-stu-id="a364a-123">Scale out event processing</span></span> 

<span data-ttu-id="a364a-124">Hallo [Scale-out gebeurtenisverwerking](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) voorbeeld laat zien hoe toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute Hallo werkbelasting Event Hubs stroom verbruikt.</span><span class="sxs-lookup"><span data-stu-id="a364a-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="a364a-125">Er wordt weergegeven hoe tooimplement hello **EventProcessor** en **EventProcessorFactory** objecten toomanage Hallo gebeurtenisstroom.</span><span class="sxs-lookup"><span data-stu-id="a364a-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="a364a-126">Ophalen van gegevens uit SQL in een event hub</span><span class="sxs-lookup"><span data-stu-id="a364a-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="a364a-127">Hallo [binnenhalen van SQL-gegevens](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) voorbeeld laat zien hoe toopull gegevens uit een SQL tabel en druk de tooan event hub, toouse als invoer in downstream analytische toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a364a-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="a364a-128">Pull-web-gegevens in een event hub</span><span class="sxs-lookup"><span data-stu-id="a364a-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="a364a-129">Hallo [gegevens importeren uit Hallo web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) voorbeeld laat zien hoe toopull gegevens uit de openbare-kanalen (bijvoorbeeld afdeling van vervoer van verkeersinformatie feed Hallo) en druk de tooan event hub.</span><span class="sxs-lookup"><span data-stu-id="a364a-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a364a-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a364a-130">Next steps</span></span>

<span data-ttu-id="a364a-131">Meer informatie over de versies van .NET Framework via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a364a-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="a364a-132">Frameworks en doelen</span><span class="sxs-lookup"><span data-stu-id="a364a-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="a364a-133">.NET framework 4.6 en 4.5</span><span class="sxs-lookup"><span data-stu-id="a364a-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="a364a-134">U meer informatie over Event Hubs in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a364a-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="a364a-135">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="a364a-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="a364a-136">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="a364a-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="a364a-137">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a364a-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)