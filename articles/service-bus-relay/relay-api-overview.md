---
title: overzicht van de Relay-API aaaAzure | Microsoft Docs
description: Overzicht van de beschikbare Azure Relay-API 's
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>Beschikbare Relay-API 's

## <a name="runtime-apis"></a>Runtime-API 's

Hallo bevat volgende tabel alle beschikbare Relay runtime-clients.

Hallo [aanvullende informatie](#additional-information) sectie vindt u meer informatie over Hallo status van elke runtime-bibliotheek.

| Taal/Platform | Beschikbare functie | Clientpakket | Opslagplaats |
| --- | --- | --- | --- |
| .NET-standaard | Hybride verbindingen | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET framework | WCF-relay | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N.v.t. |
| Knooppunt | Hybride verbindingen | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Aanvullende informatie

#### <a name="net"></a>.NET
Hallo .NET ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs. Hallo .NET standaardbibliotheek kan worden uitgevoerd met .NET Core of .NET Framework, Hallo Hallo .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework. Zie voor meer informatie over .NET Frameworks [framework-versies](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:
* [Wat is Azure Relay?](relay-what-is-it.md)
* [Veelgestelde vragen over Relay](relay-faq.md)