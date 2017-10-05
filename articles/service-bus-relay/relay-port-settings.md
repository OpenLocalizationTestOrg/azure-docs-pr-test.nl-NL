---
title: Azure Relay-poortinstellingen | Microsoft Docs
description: Meer informatie over Azure Relay-poort waarden.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 5906495c565dad583e74a43b2e5eed57e0c68df1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-port-settings"></a>Azure Relay-poortinstellingen

De volgende tabel beschrijft de vereiste configuratie voor poortwaarden voor Azure Relay.

## <a name="hybrid-connections"></a>Hybride verbindingen
Hybride verbindingen WebSockets gebruikt als onderliggend transportmechanisme, dat gebruikmaakt van **HTTPS** alleen. 

## <a name="wcf-relays"></a>WCF-relays
  
|Binding|Transportbeveiliging|Poort|  
|-------------|------------------------|----------|  
|[Klasse BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)|Ja|HTTPS| 
| |" |Nee|HTTP|  
|[Klasse BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)|Beide|9351/HTTP|  
|[Klasse NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)|Ja|9351/HTTPS|  
||" |Nee|9350/HTTP|  
|[Klasse NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)|Beide|9351/HTTP|  
|[NetTcpRelayBinding klasse](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)|Beide|9352-5671/HTTP (9352/9353 als hybride)|  
|[Klasse NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)|Ja|9351/HTTPS|  
||" |Nee|9350/HTTP|  
|[Klasse NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)|Beide|9351/HTTP|  
|[Klasse WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)|Ja|HTTPS|  
||" |Nee|HTTP|  
|[Klasse WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)|Beide|9351/HTTP|  
|[Klasse WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)|Ja|HTTPS|  
||" |Nee|HTTP|  
|[Klasse WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)|Beide|9351/HTTP|

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen voor meer informatie over Azure Relay:
* [Wat is Azure Relay?](relay-what-is-it.md)
* [Veelgestelde vragen over Relay](relay-faq.md)