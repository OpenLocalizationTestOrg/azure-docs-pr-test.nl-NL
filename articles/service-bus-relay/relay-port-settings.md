---
title: Relay-poortinstellingen aaaAzure | Microsoft Docs
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
ms.openlocfilehash: e66785f786ee241c974d250f9ec29dfcc1fdc3fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-port-settings"></a>Azure Relay-poortinstellingen

Hallo beschrijft volgende tabel Hallo vereiste configuratie voor poortwaarden voor Azure Relay.

## <a name="hybrid-connections"></a>Hybride verbindingen
Hybride verbindingen gebruikt WebSockets als transportmechanisme dat gebruikmaakt van de onderliggende hello **HTTPS** alleen. 

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
toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:
* [Wat is Azure Relay?](relay-what-is-it.md)
* [Veelgestelde vragen over Relay](relay-faq.md)