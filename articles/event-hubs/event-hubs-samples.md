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
# <a name="event-hubs-samples"></a>Voorbeelden van Event Hubs 

Hallo reeks voorbeelden van Azure Event Hubs wordt gedemonstreerd belangrijke functies in [Azure Event Hubs](/azure/event-hubs/). In dit artikel wordt ingedeeld en Hallo voorbeelden beschikbaar is, met koppelingen tooeach beschrijft.

Op Hallo moment van schrijven van dit zijn voorbeelden van Event Hubs bevinden zich op verschillende plaatsen:

- [MSDN developer-codevoorbeelden](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Zie voor meer informatie over de verschillende versies van .NET Framework Hallo [Frameworks en doelen](/dotnet/articles/standard/frameworks).

Meer voorbeelden worden toegevoegd na verloop van tijd, dus Kijk regelmatig op updates.

## <a name="net-standard"></a>.NET-standaard

Hallo volgende voorbeelden laten zien hoe toosend en ontvangen van gebeurtenissen met Hallo [Event Hubs-client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) voor Hallo [standaard .NET-bibliotheek](/dotnet/articles/standard/library).

### <a name="send-events"></a>Gebeurtenissen verzenden 

Hallo [verzenden aan de slag](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) voorbeeld laat zien hoe een .NET Core toowrite consoletoepassing die gebeurtenissen tooan event hub verzendt.

### <a name="receive-events"></a>Gebeurtenissen ontvangen 

Hallo [aan de slag met Hallo Event Processor Host ontvangen](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) voorbeeld is een .NET Core-consoletoepassing die berichten ontvangt van een event hub met Hallo Event Processor Host.

## <a name="net-framework"></a>.NET framework   

Deze voorbeelden demonstreren verschillende andere functies van Azure Event Hubs, die gericht is op Hallo [.NET Framework-bibliotheek](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Waarschuw gebruikers van gebeurtenissen ontvangen

Hallo [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) voorbeeld waarschuwt gebruikers gegevens ontvangen van sensoren of andere systemen.

### <a name="get-started-with-event-hubs"></a>Aan de slag met Event Hubs 

Hallo [Event Hubs aan de slag](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) voorbeeld demonstreert Hallo essentiële mogelijkheden van Event Hubs, zoals hoe toocreate een event hub, gebeurtenissen tooan event hub te verzenden en gebruiken van gebeurtenissen met Hallo [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Verwerking van de gebeurtenis uitschalen 

Hallo [Scale-out gebeurtenisverwerking](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) voorbeeld laat zien hoe toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute Hallo werkbelasting Event Hubs stroom verbruikt. Er wordt weergegeven hoe tooimplement hello **EventProcessor** en **EventProcessorFactory** objecten toomanage Hallo gebeurtenisstroom. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Ophalen van gegevens uit SQL in een event hub

Hallo [binnenhalen van SQL-gegevens](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) voorbeeld laat zien hoe toopull gegevens uit een SQL tabel en druk de tooan event hub, toouse als invoer in downstream analytische toepassingen.

### <a name="pull-web-data-into-an-event-hub"></a>Pull-web-gegevens in een event hub 

Hallo [gegevens importeren uit Hallo web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) voorbeeld laat zien hoe toopull gegevens uit de openbare-kanalen (bijvoorbeeld afdeling van vervoer van verkeersinformatie feed Hallo) en druk de tooan event hub.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over de versies van .NET Framework via Hallo koppelingen te volgen:

- [Frameworks en doelen](/dotnet/articles/standard/frameworks)
- [.NET framework 4.6 en 4.5](/dotnet/framework/index)

U meer informatie over Event Hubs in Hallo artikelen te volgen:

- [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
- [Een Event Hub maken](event-hubs-create.md)
- [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)