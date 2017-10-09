---
title: aaaOverview van BGP met Azure VPN-Gateways | Microsoft Docs
description: Dit artikel bevat een overzicht van BGP met Azure VPN-gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Overzicht van BGP met Azure VPN-gateways
Dit artikel bevat een overzicht van BGP-ondersteuning (Border Gateway Protocol) in Azure VPN-gateways.

BGP is Hallo standaardprotocol voor routering gebruikte in Hallo Internet tooexchange Routering en bereikbaarheid tussen twee of meer netwerken. Wanneer gebruikt in de context Hallo van Azure Virtual Networks, maakt BGP hello Azure VPN-Gateways en uw on-premises VPN-apparaten, aangeroepen BGP-peers of neighbors, tooexchange 'routes' die wordt beide gateways informeren over Hallo beschikbaarheid en bereikbaarheid voor gebruikers voorvoegsels toogo via Hallo gateways of routers die betrokken zijn. BGP ook transitroutering tussen meerdere netwerken door routes die een BGP-gateway van één BGP-peer-tooall leert andere BGP-peers. 

## <a name="why-use-bgp"></a>Waarom BGP gebruiken?
BGP is een optionele functie die u kunt gebruiken met op Azure-routes gebaseerde VPN-gateways. Moet u zorgen dat uw on-premises VPN-apparaten BGP ondersteunen voordat u Hallo-functie inschakelen. U kunt toouse Azure VPN-gateways en uw on-premises VPN-apparaten zonder BGP blijven. Hallo equivalent van het gebruik van statische routes (zonder BGP) is *versus* gebruik van dynamische routering met BGP tussen uw netwerken en Azure.

Het gebruik van BGP heeft een aantal voordelen en nieuwe mogelijkheden:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Ondersteuning van automatische en flexibele voorvoegselupdates
Met BGP hoeft u alleen toodeclare een minimaal voorvoegsel tooa specifieke BGP-peer via Hallo IPsec S2S VPN-tunnel. Het kan ook zo klein is als een hostvoorvoegsel (/ 32) Hallo BGP-peer-IP-adres van uw on-premises VPN-apparaat. U kunt bepalen welke on-premises netwerkvoorvoegsels u uw Azure Virtual Network-tooaccess tooadvertise tooAzure tooallow wilt.

U kunt ook grotere voorvoegsels met enkele van uw VNet-adresvoorvoegsels, zoals een grote privé IP-adresruimte (bijvoorbeeld 10.0.0.0/8) adverteren. Houd er rekening mee dat Hallo voorvoegsels mogen niet identiek zijn met een van uw VNet-voorvoegsels. Routes die identiek tooyour VNet-voorvoegsels wordt geweigerd.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Ondersteuning van meerdere tunnels tussen een VNet en een on-premises site met automatische failover op basis van BGP
U kunt meerdere verbindingen maken tussen uw Azure VNet en uw on-premises VPN-apparaten in Hallo dezelfde locatie. Deze mogelijkheid biedt meerdere tunnels (paden) tussen de twee netwerken Hallo in een actief / actief-configuratie. Als een van de Hallo tunnels wordt verbroken, Hallo bijbehorende routes ingetrokken via BGP en Hallo verkeer automatisch verplaatst toohello resterende tunnels.

Hallo volgende diagram ziet u een eenvoudig voorbeeld van deze maximaal beschikbare installatie:

![Meerdere actieve paden](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Ondersteuning van transitroutering tussen uw on-premises netwerken en meerdere Azure VNets
BGP kunnen meerdere gateways toolearn en voorvoegsels van verschillende netwerken propageren, ongeacht of ze direct of indirect verbonden bent. Op die manier is transitroutering met Azure VPN-gateways mogelijk tussen uw on-premises sites of tussen meerdere Azure Virtual Networks.

Hallo toont volgende diagram een voorbeeld van een Multihop-topologie met meerdere paden die verkeer tussen Hallo twee on-premises netwerken via Azure VPN-gateways binnen Hallo Microsoft Networks kan worden doorgevoerd:

![Multihop-transit](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>VEELGESTELDE VRAGEN OVER BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zie [aan de slag met BGP op Azure VPN-gateways](vpn-gateway-bgp-resource-manager-ps.md) voor stappen tooconfigure BGP voor uw cross-premises en VNet-naar-VNet-verbindingen.

