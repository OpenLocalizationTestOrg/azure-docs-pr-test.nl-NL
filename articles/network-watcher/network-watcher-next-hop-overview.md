---
title: aaaIntroduction toonext hop in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van netwerk-Watcher Hallo volgende hop-functionaliteit
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Inleiding toonext hop in Azure-netwerk-Watcher

Verkeer van een virtuele machine wordt verzonden tooa bestemming op basis van Hallo effectieve routes die zijn gekoppeld aan een NIC. Volgende hop opgehaald Hallo volgend hoptype en IP-adres van een pakket vanuit een specifieke virtuele machine en de NIC. Dit helpt toodetermine als hello pakket gerichte toohello bestemming wordt of het Hallo-verkeer wordt zwarte gaan is. Een onjuiste configuratie van routes door de gebruiker hello, waarbij een verkeer gerichte tooan on-premises locatie of een virtueel apparaat is, kan leiden tooconnectivity problemen. Ook wordt de volgende hop Hallo routetabel die zijn gekoppeld aan de volgende hop Hallo. Tijdens het opvragen van een volgende hop als Hallo route is gedefinieerd als een gebruiker gedefinieerde route worden die route geretourneerd. Anders retourneert de volgende hop 'Systeemroute'.

![overzicht van volgende hop][1]

Hallo Hieronder volgt een lijst met het volgende hoptypen hello, die kunnen worden geretourneerd bij het opvragen van de volgende hop.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Geen

### <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe de volgende hop toofind toouse problemen met de netwerkverbinding in via [selectievakje Hallo volgende hop op een virtuele machine](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













