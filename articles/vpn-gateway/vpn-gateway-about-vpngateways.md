---
title: 'Overzicht van de VPN-Gateway: Cross-premises VPN-verbindingen maken tooAzure virtuele netwerken | Microsoft Docs'
description: Dit overzicht van de VPN-Gateway wordt Hallo manieren tooconnect tooAzure virtuele netwerken die gebruikmaken van een VPN-verbinding via Internet Hallo uitgelegd. U vindt hier ook schema's van basisverbindingsconfiguraties.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>Informatie over VPN-gateway

Een VPN-gateway is een type van de virtuele netwerkgateway die versleuteld verkeer via een openbare verbinding tooan lokale locatie verzendt. Ook kunt u VPN-gateways toosend versleuteld verkeer tussen virtuele netwerken via Hallo Microsoft-netwerk in Azure. toosend versleuteld netwerkverkeer tussen uw virtuele Azure-netwerk en uw on-premises site, moet u een VPN-gateway maken voor het virtuele netwerk.

Elk virtueel netwerk kan slechts één VPN-gateway hebben, maar kunt u meerdere verbindingen toohello dezelfde VPN-gateway. Een voorbeeld hiervan is een configuratie met meerdere siteverbindingen. Wanneer u meerdere verbindingen toohello maakt dezelfde VPN-gateway, alle VPN-tunnels, inclusief punt-naar-Site VPN-verbindingen, delen Hallo bandbreedte die beschikbaar is voor het Hallo-gateway.

### <a name="whatis"></a>Wat is een virtuele netwerkgateway?

Een virtuele netwerkgateway bestaat uit twee of meer virtuele machines die zijn geïmplementeerd tooa specifiek subnet Hallo GatewaySubnet aangeroepen. Hallo virtuele machines die zich in Hallo GatewaySubnet worden gemaakt bevinden wanneer u de virtuele netwerkgateway Hallo maakt. Virtuele netwerkgateway VMs zijn geconfigureerd toocontain routeringstabellen en gateway services specifieke toohello gateway. U kunt geen virtuele machines die deel van de virtuele netwerkgateway Hallo uitmaken Hallo rechtstreeks configureren en moet u aanvullende bronnen toohello GatewaySubnet nooit implementeren.

Wanneer u een virtuele netwerkgateway met type 'Vpn', Hallo gateway maakt, een specifiek type virtuele netwerkgateway die verkeer versleutelt; wordt gemaakt een VPN-gateway. Een VPN-gateway kan toocreate van too45 minuten duren. Dit is omdat Hallo virtuele machines voor Hallo VPN-gateway worden geïmplementeerde toohello GatewaySubnet en geconfigureerd met Hallo-instellingen die u hebt opgegeven. Hallo Gateway-SKU die u selecteert, bepaalt hoe krachtige Hallo VM's zijn.

## <a name="gwsku"></a>Gateway-SKU's

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Een VPN-gateway configureren

Een VPN-gatewayverbinding is afhankelijk van meerdere resources die zijn geconfigureerd met specifieke instellingen. Meeste Hallo bronnen kunnen afzonderlijk, hoewel ze moeten worden geconfigureerd in een bepaalde volgorde in sommige gevallen worden geconfigureerd.

### <a name="settings"></a>Instellingen

Hallo-instellingen die u hebt gekozen voor elke resource zijn kritieke toocreating verbinding is geslaagd. Zie voor meer informatie over afzonderlijke resources en de instellingen voor VPN Gateway [Over VPN Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md). Hallo artikel bevat informatie toohelp u gatewaytypen, VPN-typen, verbindingstypen, gateway-subnetten, lokale netwerkgateways en verschillende andere broninstellingen dat u tooconsider kunt begrijpen.

### <a name="tools"></a>Implementatiehulpmiddelen

U kunt starten uit maken en configureren van resources met behulp van een configuratiehulpprogramma, zoals hello Azure-portal. U kunt later besluit tooswitch tooanother hulpprogramma, zoals PowerShell, tooconfigure aanvullende bronnen of wijzigen van bestaande bronnen, indien van toepassing. Op dit moment kunt configureren u niet elke resource en de resource-instelling in hello Azure-portal. Hallo-instructies in Hallo artikelen voor elke verbinding-topologie opgeven wanneer een specifieke configuratie-hulpprogramma nodig is. 

### <a name="models"></a>Implementatiemodel

Wanneer u een VPN-gateway configureert, afhankelijk Hallo u stappen ondernemen Hallo implementatiemodel dat u toocreate het virtuele netwerk gebruikt. Bijvoorbeeld, als u uw VNet gemaakt met het klassieke implementatiemodel hello, u gebruik Hallo richtlijnen en instructies voor het Hallo-classic deployment model toocreate en de instellingen van uw VPN-gateway configureren. Zie [Het Resource Manager-implementatiemodel en het klassieke implementatiemodel begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de implementatiemodellen.

## <a name="diagrams"></a>Diagrammen over de verbindingstopologie

Het is belangrijk tooknow dat er verschillende configuraties beschikbaar voor VPN-gateway-verbindingen zijn. U moet toodetermine welke configuratie komt het beste past bij uw behoeften. In onderstaande Hallo secties, vindt u informatie en topologie diagrammen over Hallo VPN-gatewayverbindingen te volgen: Hallo volgende secties bevatten tabellen die:

* Beschikbaar implementatiemodel
* Beschikbare configuratiehulpprogramma's
* Koppelingen rechtstreeks tooan artikel, indien beschikbaar

Gebruik Hallo diagrammen en beschrijvingen toohelp Selecteer Hallo verbinding topologie toomatch uw vereisten. Hallo diagrammen geven Hallo belangrijkste basistopologieën, maar het is mogelijk toobuild complexere configuraties Hallo diagrammen als richtlijn gebruiken.

## <a name="s2smulti"></a>Site-naar-site en multi-site (IPsec-/IKE VPN-tunnel)

### <a name="S2S"></a>Site-naar-site

Een site-naar-site-VPN-gatewayverbinding (S2S) is een verbinding via een VPN-tunnel met IPsec/IKE (IKEv1 of IKEv2). Een S2S-verbinding is vereist voor een VPN-zich on-premises apparaten met een openbare IP-adres toegewezen tooit en bevindt zich niet achter een NAT bevinden. S2S-verbindingen kunnen worden gebruikt voor cross-premises en hybride configuraties.   

![Voorbeeld van een site-naar-site-verbinding met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Multi-site

Dit type verbinding is een variatie Hallo Site-naar-Site-verbinding. U meer dan één VPN-verbinding maken van uw virtuele netwerkgateway, doorgaans verbinden toomultiple lokale sites. Als u met meerdere verbindingen werkt, moet u een op een route gebaseerd VPN-type (ook bekend als een dynamische gateway voor klassieke VNets) gebruiken. Omdat elke virtueel netwerk slechts één VPN-gateway hebben kan, delen alle verbindingen via de gateway Hallo Hallo beschikbare bandbreedte. Dit wordt vaak een multi-site-verbinding genoemd.

![Voorbeeld van een verbinding tussen meerdere locaties met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Implementatiemodellen en -methoden voor site-naar-site en multi-site

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Punt-naar-site (VPN via SSTP)

Een punt-naar-Site (P2S) VPN-gateway kunt u een beveiligde verbinding tooyour virtueel netwerk maken van een afzonderlijke clientcomputer. Punt-naar-Site VPN-verbindingen zijn handig als u wilt dat tooconnect tooyour VNet vanaf een externe locatie, zoals wanneer u vanaf thuis of een conferentie zijn teleforenzen. Een P2S-VPN is ook een uitstekende oplossing toouse in plaats van een Site-naar-Site VPN-wanneer u slechts enkele clients hebt die tooconnect tooa VNet nodig hebt. 

Bij P2S-verbindingen is er, in tegenstelling tot bij S2S-verbindingen, geen on-premises openbaar IP-adres en geen VPN-apparaat nodig. P2S-verbindingen kunnen worden gebruikt met S2S-verbindingen via Hallo dezelfde VPN-gateway, zolang alle Hallo configuratievereisten voor beide verbindingen compatibel zijn.

Maakt gebruik van P2S Hallo SSTP Secure Socket Tunneling Protocol (), die een VPN op basis van een SSL-protocol. Een P2S-VPN-verbinding tot stand is gebracht vanaf Hallo-clientcomputer.

![Voorbeeld van een punt-naar-site-verbinding met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Implementatiemodellen en -methoden voor punt-naar-site

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>VNet-naar-VNet-verbindingen (IPsec-/IKE VPN-tunnel)

Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE. U kunt zelfs VNet-naar-VNet-communicatie met multi-site-verbindingsconfiguraties combineren. Zo kunt u netwerktopologieën maken waarin cross-premises connectiviteit is gecombineerd met connectiviteit tussen virtuele netwerken.

Hallo VNets die u verbindt kan zijn:

* in Hallo dezelfde of verschillende regio's
* in Hallo dezelfde of verschillende abonnementen 
* in Hallo dezelfde of verschillende implementatiemodellen

![Voorbeeld van Azure VPN-Gateway VNet tooVNet verbinding](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Verbindingen tussen implementatiemodellen

Azure heeft momenteel twee implementatiemodellen: klassiek en Resource Manager. Als u al langer met Azure hebt gewerkt, hebt u waarschijnlijk Azure-VM's en -rolinstanties in een klassiek VNet. De nieuwere VM's en rolinstanties werken mogelijk in een VNet dat is gemaakt in Resource Manager. U kunt een verbinding tussen Hallo VNets tooallow Hallo resources maken in een VNet toocommunicate rechtstreeks met resources in een andere.

### <a name="vnet-peering"></a>VNet-peering

Hebt u mogelijk kunnen toouse VNet-peering toocreate uw verbinding, zolang het virtuele netwerk aan bepaalde vereisten voldoet. Bij VNet-peering wordt geen virtuele netwerkgateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Implementatiemodellen en -methoden voor VNet-naar-VNet

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (exclusieve privéverbinding)

Microsoft Azure ExpressRoute kunt u uw on-premises netwerken in Hallo Microsoft cloud uitbreiden via een speciale persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider. Met ExpressRoute kunt kunt u verbindingen tooMicrosoft cloudservices, zoals Microsoft Azure, Office 365 en CRM Online maken. Via een connectiviteitsprovider in een co-locatiefaciliteit is connectiviteit mogelijk vanuit een any-to-any (IP VPN) netwerk, een point-to-point Ethernet-netwerk of een virtuele overlappende verbinding.

ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. ExpressRoute-verbindingen toooffer kan dit meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo.

Een ExpressRoute-verbinding gebruikt geen VPN-gateway. Er wordt echter wel een virtuele netwerkgateway gebruikt als onderdeel van de vereiste configuratie. Hallo virtuele netwerkgateway is in een ExpressRoute-verbinding geconfigureerd met Gatewaytype Hallo 'ExpressRoute', in plaats van 'VPN-'. Zie voor meer informatie over ExpressRoute hello [technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Site-naar-site- en ExpressRoute-verbindingen naast elkaar

ExpressRoute is een directe, exclusieve verbinding van uw WAN (niet via openbaar Internet Hallo) tooMicrosoft Services, waaronder Azure. Site-naar-Site VPN-verkeer reis gecodeerd via Hallo openbare Internet. Kan tooconfigure wordt Site-naar-Site VPN en ExpressRoute-verbindingen voor hello hetzelfde virtuele netwerk verschillende voordelen heeft.

U kunt een Site-naar-Site-VPN configureren als een beveiligd failoverpad voor ExpressRoute of Site-naar-Site VPN-verbindingen tooconnect toosites die geen deel uitmaken van uw netwerk, maar die zijn verbonden via ExpressRoute. U ziet dat deze configuratie is vereist voor twee virtuele netwerkgateways Hallo hetzelfde virtuele netwerk, een met Gatewaytype VPN '-' Hallo en andere met behulp van het Gatewaytype Hallo 'ExpressRoute' Hallo.

![Voorbeeld van ExpressRoute en VPN Gateway in eenzelfde implementatie](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Implementatiemodellen en -methoden voor S2S en ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Prijzen

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie over gateway-SKU's voor VPN Gateway.

## <a name="faq"></a>Veelgestelde vragen

Zie voor veelgestelde vragen over VPN-gateway Hallo [Veelgestelde vragen over het VPN-Gateway](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Volgende stappen

- De VPN-gatewayconfiguratie plannen. Zie [Planning en ontwerp voor VPN Gateway](vpn-gateway-plan-design.md).
- Weergave Hallo [Veelgestelde vragen over het VPN-Gateway](vpn-gateway-vpn-faq.md) voor meer informatie.
- Weergave Hallo [abonnement en Servicelimieten](../azure-subscription-service-limits.md#networking-limits).
- Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.
