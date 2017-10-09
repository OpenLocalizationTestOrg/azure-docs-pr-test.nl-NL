---
title: 'Connectiviteitsmodellen ExpressRoute: verbinding maken met tooMicrosoft Azure via het netwerkserviceproviders kunnen worden uitgewisseld en Ethernet-providers | Microsoft Docs'
description: Dit artikel wordt beschreven Hallo verschillende modi van de verbinding tussen het netwerk en de services van Microsoft Azure, Office 365 en Dynamics 365 Hallo van de klant. Klanten kunnen gebruikmaken van MPLS-providers, cloudexchanges en Ethernet-providers.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>ExpressRoute-connectiviteitsmodellen
U kunt een verbinding tussen uw on-premises netwerk en Microsoft cloud Hallo maken op drie verschillende manieren [CloudExchange CO-locatie](#CloudExchange), [Point-to-point Ethernet-verbinding](#Ethernet), en [Any-to-any (IPVPN) verbinding](#IPVPN). Connectiviteitsproviders kunnen een of meer connectiviteitsmodellen bieden. U kunt werken met uw netwerkverbinding provider toopick Hallo model die geschikt is voor u.
<br><br>

![Diagram van ExpressRoute-connectiviteitsmodellen](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Co-locatie op een cloudexchange
Als u in een faciliteit met een exchange-cloud bevindt zich, kunt u virtuele overlappende verbindingen toohello Microsoft cloud via het Ethernet-exchange Hallo CO-locatie van de provider bestellen. CO-locatieproviders kunnen Layer 2-overlappende verbindingen of beheerde laag-3 overlappende verbindingen tussen uw infrastructuur in Hallo CO-locatiefaciliteit en Hallo Microsoft cloud aanbieden.

## <a name="Ethernet"></a>Point-to-Point Ethernet-verbindingen
U kunt uw lokale datacenters/kantoren toohello Microsoft cloud verbinden via point-to-point Ethernet-koppelingen. Point-to-Point Ethernet-providers kunnen laag-2-verbindingen bieden of beheerde laag-3-verbindingen tussen uw site en Hallo Microsoft cloud.

## <a name="IPVPN"></a>Any-to-any (IPVPN) netwerken
U kunt uw WAN integreren met Microsoft cloud Hallo. IPVPN-providers (doorgaans MPLS VPN) bieden any-to-any connectiviteit tussen uw filialen en datacenters. Hallo Microsoft cloud kan worden onderling verbonden tooyour WAN toomake ziet er net zoals een filiaal. WAN-providers bieden doorgaans beheerde Laag-3-connectiviteit. ExpressRoute-functies en zijn identiek voor alle Hallo bovenstaande connectiviteitsmodellen. 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over ExpressRoute-verbindingen en -routeringsdomeinen. Zie [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).
* Meer informatie over ExpressRoute-functies. Zie Hallo [technisch overzicht van ExpressRoute](expressroute-introduction.md)
* Zoek een serviceprovider Zie [ExpressRoute partners and peering locations](expressroute-locations.md) (ExpressRoute-partners en -peeringlocaties).
* Controleer of aan alle vereisten is voldaan. Zie [ExpressRoute prerequisites](expressroute-prerequisites.md) (Vereisten voor ExpressRoute).
* Raadpleeg de vereisten voor toohello [routering](expressroute-routing.md), [NAT](expressroute-nat.md), en [QoS](expressroute-qos.md).
* Configureer uw ExpressRoute-verbinding.
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-portal-resource-manager.md)
  * [Routering configureren](expressroute-howto-routing-portal-resource-manager.md)
  * [Koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md)
