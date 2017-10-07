---
title: aaaOverview van maximaal beschikbare configuraties met Azure VPN-Gateways | Microsoft Docs
description: Dit artikel bevat een overzicht van maximaal beschikbare configuratieopties met Azure VPN-gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit
Dit artikel bevat een overzicht van maximaal beschikbare configuratieopties voor uw cross-premises en VNet-naar-VNet-connectiviteit met Azure VPN-gateways.

## <a name = "activestandby"></a>Over Azure VPN-gateway redundantie
Elke Azure VPN-gateway bestaat uit twee instanties in een actieve stand-byconfiguratie. Voor gepland onderhoud of niet-geplande onderbreking die toohello actief exemplaar plaatsvindt, zou Hallo stand-by-exemplaar (failover) automatisch overnemen en hervat Hallo S2S VPN of VNet-naar-VNet-verbindingen. Hallo-switch via, ontstaat er een korte onderbreking. Voor gepland onderhoud moet Hallo connectiviteit binnen 10 too15 seconden worden hersteld. Voor niet-geplande problemen Hallo verbinding herstel wordt niet langer, over 1 minuut too1 en een halve in het ergste geval Hallo minuten. Voor P2S-VPN-client-verbindingen toohello gateway Hallo P2S-verbindingen moeten worden beëindigd en Hallo gebruikers moet tooreconnect van Hallo-clientcomputers.

![Actieve stand-by](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Maximaal beschikbare cross-premises connectiviteit
tooprovide betere beschikbaarheid voor uw cross-premises verbindingen, er zijn een aantal opties beschikbaar:

* Meerdere on-premises VPN-apparaten
* Actief/actief Azure VPN-gateway
* Combinatie van beide

### <a name = "activeactiveonprem"></a>Meerdere on-premises VPN-apparaten
Zoals wordt weergegeven in het volgende diagram hello, kunt u meerdere VPN-apparaten van uw on-premises netwerk tooconnect tooyour Azure VPN-gateway:

![Meerdere on-premises VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Deze configuratie biedt meerdere actieve tunnels van Hallo dezelfde Azure VPN-gateway tooyour on-premises apparaten in Hallo dezelfde locatie. Er zijn enkele vereisten en beperkingen:

1. U moet toocreate meerdere S2S VPN-verbindingen van uw VPN-apparaten tooAzure. Wanneer u verbinding maakt meerdere VPN-apparaten van Hallo dezelfde lokale netwerk tooAzure, moet u toocreate een lokale netwerkgateway voor elke VPN-apparaat en een verbinding van uw Azure VPN-gateway toohello lokale netwerkgateway.
2. lokale netwerkgateways Hallo overeenkomt tooyour VPN-apparaten moeten unieke openbare IP-adressen in Hallo 'GatewayIpAddress'-eigenschap hebben.
3. BGP is vereist voor deze configuratie. Elke lokale netwerkgateway die vertegenwoordigt een VPN-apparaat moet een uniek IP-adres voor BGP-peer opgegeven in de eigenschap 'BgpPeerIpAddress' hello hebben.
4. Hallo AddressPrefix eigenschapsveld in elke lokale netwerkgateway mogen niet overlappen. U moet Hallo 'BgpPeerIpAddress' opgeven in /32 CIDR-indeling in Hallo AddressPrefix veld, bijvoorbeeld 10.200.200.254/32.
5. Moet u BGP tooadvertise dezelfde voorvoegsels Hallo Hallo dezelfde lokale netwerkgateway voorvoegsels tooyour Azure VPN- en Hallo verkeer wordt doorgestuurd via deze tunnels van tegelijkertijd.
6. Elke verbinding wordt geteld tegen Hallo kunt u het maximum aantal tunnels voor uw Azure VPN-gateway, 10 voor Basic en Standard-SKU's en 30 voor HighPerformance SKU. 

In deze configuratie hello Azure VPN-gateway, wordt nog steeds actief stand-by-modus, dus Hallo dezelfde overname bij storing en korte onderbreking gebeurt nog steeds zoals beschreven [hierboven](#activestandby). Deze installatie beschermt echter tegen storingen of onderbrekingen op uw on-premises netwerk en VPN-apparaten.

### <a name="active-active-azure-vpn-gateway"></a>Actief/actief Azure VPN-gateway
U kunt nu een Azure VPN-gateway maken in een actief / actief-configuratie, waarbij beide exemplaren van Hallo gateway die VM 's tot stand brengen dat s2s VPN tunnels tooyour on-premises VPN-apparaat als weergegeven Hallo volgende diagram:

![Actief-actief](./media/vpn-gateway-highlyavailable/active-active.png)

In deze configuratie is elk Azure-gateway-exemplaar heeft een unieke openbare IP-adres en elk een IPsec/IKE S2S-VPN-tunnel tooyour on-premises VPN-apparaat opgegeven in uw lokale netwerkgateway en verbinding tot stand brengen. Houd er rekening mee dat zowel VPN-tunnels daadwerkelijk deel van Hallo uitmaken dezelfde verbinding. Of u kunt wordt nog steeds tooconfigure uw lokale VPN-apparaat tooaccept tot stand brengen van twee S2S VPN-tunnels toothose twee Azure VPN-gateway openbare IP-adressen.

Omdat hello Azure-gateway-exemplaren in actief / actief-configuratie, Hallo verkeer van uw virtuele Azure-netwerk tooyour lokale netwerk worden doorgestuurd via beide tunnels tegelijk, zelfs als uw on-premises VPN-apparaat kan één tunnel voorkeur via Hallo andere. Houd er rekening mee Hoewel Hallo dezelfde TCP of UDP-stroom wordt altijd passeren Hallo dezelfde tunnel of pad, tenzij er een gebeurtenis onderhoud wordt uitgevoerd op één van Hallo-exemplaren.

Als een gepland onderhoud of niet-geplande gebeurtenis tooone gatewayexemplaar gebeurt, Hallo IPSec-tunnel van dat exemplaar tooyour lokale VPN-apparaat moet worden beëindigd. Hallo bijbehorende routes op uw VPN-apparaten moeten worden verwijderd of automatisch worden ingetrokken, zodat het Hallo-verkeer wordt overgeschakeld toohello andere actieve IPsec-tunnel. Op Hallo Azure aan clientzijde, Hallo switch via gebeurt automatisch van Hallo van invloed op een exemplaar toohello actieve exemplaar.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Dubbele redundantie: actief/actief VPN-gateways voor Azure en on-premises netwerken
Hallo meest betrouwbare optie is toocombine Hallo actieve gateways in uw netwerk- en Azure, zoals wordt weergegeven in het onderstaande diagram kunt Hallo.

![Dubbele redundantie](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Hier maken en setup hello Azure VPN-gateway in een actief / actief-configuratie en twee lokale netwerkgateways maken en twee verbindingen voor de twee on-premises VPN-apparaten zoals hierboven is beschreven. Hallo-resultaat is een volledige mesh-connectiviteit van 4 IPsec-tunnels tussen uw virtuele Azure-netwerk en uw on-premises netwerk.

Alle gateways en tunnels hello Azure aan clientzijde actief zijn, zodat Hallo verkeer wordt verdeeld tussen alle 4 tunnels tegelijk, hoewel elke TCP of UDP-stromen worden opnieuw Volg dezelfde tunnel Hallo of pad van hello Azure aan clientzijde. Hoewel door te spreiden Hallo verkeer, kan er iets betere doorvoer via Hallo IPSec-tunnels, is Hallo voornaamste doel van deze configuratie voor hoge beschikbaarheid. En vanwege toohello statistische aard van het Hallo spreiden, is moeilijk tooprovide Hallo meting op hoe verschillende toepassing verkeer voorwaarden zijn van invloed op Hallo geaggregeerde doorvoer.

Deze topologie waarvoor twee lokale netwerkgateways en twee verbindingen toosupport Hallo paar on-premises VPN-apparaten en BGP is vereist tooallow Hallo twee verbindingen toohello dezelfde on-premises netwerk. Deze vereisten gelden dezelfde als Hallo Hallo [hierboven](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Maximaal beschikbare VNet-naar-VNet-connectiviteit via VPN Azure-gateways
Hallo dezelfde actief / actief-configuratie kan ook worden toegepast tooAzure VNet-naar-VNet-verbindingen. U kunt actieve VPN-gateways voor beide virtuele netwerken maken en verbind ze samen tooform Hallo dezelfde volledige connectiviteit van 4 tunnels tussen Hallo twee VNets NET, zoals wordt weergegeven in Hallo diagram hieronder:

![VNet-naar-VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Dit zorgt ervoor dat er zijn altijd een paar tunnels tussen twee virtuele netwerken Hallo voor alle gebeurtenissen voor gepland onderhoud nog beter beschikbaarheid biedt. Hoewel hello dezelfde topologie voor cross-premises connectiviteit twee verbindingen vereist, moet Hallo VNet-naar-VNet-topologie hierboven weergegeven voor elke gateway slechts één verbinding. BGP is bovendien optioneel tenzij transitroutering via Hallo VNet-naar-VNet-verbinding vereist is.

## <a name="next-steps"></a>Volgende stappen
Zie [actieve VPN-Gateways voor Cross-Premises en VNet-naar-VNet-verbindingen configureren](vpn-gateway-activeactive-rm-powershell.md) voor stappen tooconfigure actieve cross-premises en VNet-naar-VNet-verbindingen.

