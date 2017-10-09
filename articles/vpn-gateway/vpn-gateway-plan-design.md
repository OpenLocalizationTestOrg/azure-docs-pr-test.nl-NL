---
title: 'Planning en ontwerp voor cross-premises verbindingen: Azure VPN-Gateway | Microsoft Docs'
description: Meer informatie over VPN-Gateway planning en ontwerp voor cross-premises en hybride VNet-naar-VNet-verbindingen
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Planning en ontwerp voor VPN Gateway

Plannen en ontwerpen van uw cross-premises en VNet-naar-VNet-configuraties kunnen zijn eenvoudige of complexe, afhankelijk van de behoeften van uw netwerk. Dit artikel begeleidt u bij basic plannings- en ontwerpoverwegingen.

## <a name="planning"></a>Plannen

### <a name="compare"></a>Opties voor cross-premises-connectiviteit

Als u wilt dat tooconnect uw on-premises sites veilig tooa virtueel netwerk, hebt u drie verschillende manieren toodo dus: Site-naar-Site, punt-naar-Site en ExpressRoute. Vergelijk Hallo verschillende cross-premises verbindingen die beschikbaar zijn. Hallo-optie die u kiest kan afhankelijk zijn van verschillende overwegingen, zoals:

* Wat voor doorvoer heeft uw oplossing nodig?
* Wilt u toocommunicate via Hallo openbare Internet via een beveiligd VPN, of via een particuliere verbinding?
* Hebt u een openbaar IP-adres beschikbaar toouse?
* Bent u van plan toouse een VPN-apparaat? Zo ja, is het compatibel?
* Verbindt u slechts enkele computers met elkaar, of u wilt een persistente verbinding voor uw site?
* Welk type VPN-gateway is vereist voor de oplossing Hallo gewenste toocreate?
* Welke gateway SKU moet u gebruiken?

### <a name="planningtable"></a>Tabel plannen

Hallo volgende tabel kunt u bepalen Hallo beste connectiviteitsoptie voor uw oplossing.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>Gateway-SKU's

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Werkstroom

Hallo Hallo volgende overzichten van de lijst algemene werkstroom voor cloud-verbinding:

1. Ontwerp- en plan dat uw connectiviteit topologie en lijst Hallo adresruimten voor alle netwerken u wilt dat tooconnect.
2. Maak een Azure-netwerk. 
3. Een VPN-gateway voor Hallo virtueel netwerk maken.
4. Maak en configureer verbindingen tooon-premises netwerken of andere virtuele netwerken (indien nodig).
5. Maak en configureer een punt-naar-Site-verbinding voor uw Azure VPN-gateway (indien nodig).

## <a name="design"></a>Ontwerp
### <a name="topologies"></a>Topologieën voor verbinding

Bekijkt hello diagrammen in Hallo [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel. Hallo artikel bevat basic diagrammen Hallo implementatiemodellen voor elke topologie en Hallo beschikbaar implementatiehulpprogramma's kunt u toodeploy uw configuratie.

### <a name="designbasics"></a>Basisprincipes van ontwerp

Hallo uit te voeren bespreken basisbeginselen van Hallo VPN-gateway. 

#### <a name="servicelimits"></a>Limieten voor netwerken services

Blader door Hallo tabellen tooview [netwerken services limieten](../azure-subscription-service-limits.md#networking-limits). uw ontwerp mogelijk van invloed op Hallo-limieten die zijn vermeld.

#### <a name="subnets"></a>Over subnetten

Als u verbindingen maakt, moet u rekening houden met subnet bereiken. U kunt geen overlappende subnet-adresbereiken. Een overlappend subnet is als één virtueel netwerk of on-premises locatie bevat Hallo dezelfde adresruimte die door andere locatie Hallo bevat. Dit betekent dat u moet uw netwerk engineers voor uw lokale lokale netwerken toocarve uit een bereik voor u toouse voor uw Azure-IP-adressering ruimte/subnetten. U moet een adresruimte die niet wordt gebruikt op Hallo lokale on-premises netwerk.

Vermijden overlappende subnetten is ook belangrijk wanneer u met VNet-naar-VNet-verbindingen werkt. Als uw subnetten overlappen en een IP-adres in zowel Hallo verzenden als de doelserver VNets bestaat, mislukt de VNet-naar-VNet-verbindingen. Azure kan geen route Hallo gegevens toohello andere VNet omdat Hallo doeladres deel uitmaakt van Hallo VNet verzenden.

VPN-Gateways vereist een specifiek subnet met de naam van een gatewaysubnet. Alle gatewaysubnetten moeten de naam GatewaySubnet toowork goed. Zorg ervoor dat geen tooname het gatewaysubnet van een andere naam geven en virtuele machines of alles anders toohello gatewaysubnet niet implementeren. Zie [Gatewaysubnetten](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Over lokale netwerkgateways

Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie. In het klassieke implementatiemodel hello is de lokale netwerkgateway Hallo waarnaar wordt verwezen tooas een lokale netwerksite. Wanneer u een lokale netwerkgateway configureert, u een naam geven, Hallo openbare IP-adres van Hallo on-premises VPN-apparaat en geef Hallo adresvoorvoegsels in Hallo on-premises locatie. Azure bekijkt hello bestemmingsadressen voor netwerkverkeer, raadpleegt Hallo-configuratie die u hebt opgegeven voor de lokale netwerkgateway Hallo en routeert pakketten dienovereenkomstig. U kunt Hallo adresvoorvoegsels zo nodig wijzigen. Zie voor meer informatie [lokale netwerkgateways](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Over gatewaytypen

Het is essentieel Hallo juiste Gatewaytype voor uw topologie te selecteren. Als u het verkeerde type Hallo selecteert, werkt uw gateway niet goed. Hallo-Gatewaytype bepaalt hoe Hallo gateway zelf is verbonden en een vereiste configuratie-instelling voor Hallo Resource Manager-implementatiemodel.

Hallo gatewaytypen zijn:

* VPN
* ExpressRoute

#### <a name="connectiontype"></a>Over verbindingstypen

Elke configuratie vereist een specifiek verbindingstype. Hallo verbindingstypen zijn:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>Over VPN-typen

Elke configuratie vereist een specifiek VPN-type. Als u twee configuraties, zoals het maken van een Site-naar-Site-verbinding en een punt-naar-Site-verbinding toohello combineert hetzelfde VNet, moet u een VPN-type dat voldoet aan de vereisten van beide verbindingen.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hallo volgende tabellen bevatten Hallo VPN-type als de verbindingsconfiguratie tooeach wordt toegewezen. Zorg ervoor dat Hallo VPN-type voor uw gateway komt overeen met Hallo configuratie die u toocreate wilt. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>VPN-apparaten voor Site-naar-Site-verbindingen

tooconfigure een Site-naar-Site-verbinding, ongeacht het implementatiemodel, moet u Hallo volgende items:

* Een VPN-apparaat dat compatibel is met Azure VPN-gateways
* Een openbare IPv4-adres die zich niet achter een NAT bevinden.

U moet toohave ervaring voor configuratie van uw VPN-apparaat, of iemand zijn en kunnen Hallo apparaat configureren voor u.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Houd rekening met het geforceerd tunnel routering

U kunt voor de meeste configuraties configureren geforceerde tunneling. Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle. Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels. 

Zonder geforceerde tunneling wordt internetverkeer van uw virtuele machines in Azure altijd passeren van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer. Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.

Een geforceerde tunneling verbinding kan worden geconfigureerd in beide implementatiemodellen en met behulp van verschillende hulpprogramma's. Zie voor meer informatie [geforceerde tunneling configureren](vpn-gateway-forced-tunneling-rm.md).

**Geforceerde tunneling diagram**

![Azure VPN-Gateway geforceerde tunneling diagram](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Volgende stappen

Zie Hallo [Veelgestelde vragen over het VPN-Gateway](vpn-gateway-vpn-faq.md) en [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikelen voor meer informatie toohelp u bij uw ontwerp.

Zie voor meer informatie over specifieke gatewayinstellingen [over VPN-Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md).