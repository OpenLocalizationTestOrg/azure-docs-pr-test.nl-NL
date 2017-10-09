---
title: overzicht van Event Hubs-API aaaAzure | Microsoft Docs
description: Overzicht van de beschikbare Azure Event Hubs-API 's
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>Beschikbare Event Hubs-API 's

## <a name="runtime-apis"></a>Runtime-API 's

Hallo Hieronder volgt een beschrijving van alle beschikbare Azure Event Hubs runtime-clients. Sommige van deze bibliotheken ook beperkte beheerfunctionaliteit bevatten, maar er zijn ook [specifieke bibliotheken](#management-apis) toomanagement operations toegewezen. Hallo core focus van deze bibliotheken is toosend en berichten ontvangen van een event hub.

Zie [aanvullende informatie](#additional-information) voor meer informatie over de huidige status Hallo van elke runtime-bibliotheek.

| Taal/Platform | Clientpakket | EventProcessorHost-pakket | Opslagplaats |
| --- | --- | --- | --- |
| .NET-standaard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N.v.t. |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Knooppunt | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N.v.t. | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N.v.t. | N.v.t. | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Aanvullende informatie

#### <a name="net"></a>.NET
Hallo .NET ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs. Hallo .NET standaardbibliotheek kan worden uitgevoerd met .NET Core of .NET Framework, Hallo Hallo .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework. Zie voor meer informatie over .NET Frameworks [framework-versies](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Knooppunt

Hallo Node.js-bibliotheek is momenteel in preview en als een kant-project wordt beheerd door Microsoft-werknemers en externe medewerkers. Alle bijdragen, met inbegrip van broncode Welkom zijn en zal worden beoordeeld.

## <a name="management-apis"></a>Management-API 's

Hallo Hieronder volgt een lijst van alle beschikbare management specifieke bibliotheken. Geen van deze bibliotheken runtime bewerkingen bevatten, en zijn voor Hallo enig doel van het beheer van Event Hubs-entiteiten.

| Taal/Platform | Management Pack | Opslagplaats |
| --- | --- | --- | --- |
| .NET-standaard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)