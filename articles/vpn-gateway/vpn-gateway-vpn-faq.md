---
title: Veelgestelde vragen over het VPN-Gateway aaaAzure | Microsoft Docs
description: Hallo Veelgestelde vragen over het VPN-Gateway. Veelgestelde vragen over cross-premises verbindingen, verbindingen voor hybride configuraties en VPN-gateways voor Microsoft Azure Virtual Network.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>Veelgestelde vragen VPN-gateways

## <a name="connecting"></a>Toovirtual netwerken met elkaar verbinden

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Kan ik virtuele netwerken in verschillende Azure-regio's verbinden?

Ja. Er is zelfs helemaal geen regiobeperking. Een virtueel netwerk verbinding kan maken van virtueel netwerk in Hallo tooanother dezelfde regio of in een andere Azure-regio. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Kan ik virtuele netwerken uit verschillende abonnementen verbinden?

Ja.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>Kan ik toomultiple sites uit één virtueel netwerk verbinden?

U kunt toomultiple sites verbinding maken met behulp van Windows PowerShell en hello Azure REST API's. Zie Hallo [multi-site- en VNet-naar-VNet-connectiviteit](#V2VMulti) sectie Veelgestelde vragen.

### <a name="what-are-my-cross-premises-connection-options"></a>Wat zijn de opties voor cross-premises-verbinding?

Hallo volgende cross-premises verbindingen worden ondersteund:

* Site-naar-site: VPN-verbinding via IPsec (IKE v1 en IKE v2). Voor dit type verbinding is een VPN-apparaat of RRAS vereist. Zie [Site-naar-site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) voor meer informatie.
* Punt-naar-site: VPN-verbinding via SSTP (Secure Socket Tunneling Protocol). Voor deze verbinding is geen VPN-apparaat vereist. Zie [Punt-naar-site](vpn-gateway-howto-point-to-site-resource-manager-portal.md) voor meer informatie.
* VNet-naar-VNet – dit type verbinding is hetzelfde als een Site-naar-Site-configuratie Hallo. VNet tooVNet is een VPN-verbinding via IPsec (IKE v1 en IKE v2). Hiervoor is geen VPN-apparaat vereist. Zie [VNet-naar-VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) voor meer informatie.
* Meerdere Site-dit is een variant van een Site-naar-Site-configuratie waarmee u tooconnect meerdere on-premises sites tooa virtuele netwerk. Zie [Multi-site](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) voor meer informatie.
* ExpressRoute: ExpressRoute is een rechtstreekse verbinding tooAzure van uw WAN, niet een VPN-verbinding via Hallo openbare Internet. Zie voor meer informatie, Hallo [technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) en Hallo [Veelgestelde vragen over ExpressRoute](../expressroute/expressroute-faqs.md).

Zie [Informatie over VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gatewayverbindingen.

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Wat is Hallo verschil tussen een verbinding met Site-naar-Site en punt-naar-Site?

Er is sprake van **site-naar-site**-configuraties (IPsec-/IKE VPN-tunnel) tussen uw on-premises locatie en Azure. Dit betekent dat u verbinding van een van de computers die zich op uw lokale tooany virtuele machine of rolinstantie in uw virtuele netwerk maken kunt, afhankelijk van hoe u routering tooconfigure en machtigingen. Het is een geweldige optie voor een cross-premises-verbinding die altijd beschikbaar is. Dit type verbinding is gebaseerd op een apparaat met IPsec VPN (hardwareapparaat of software), die moet worden geïmplementeerd op Hallo rand van uw netwerk. toocreate dit type verbinding, hebt u een extern gericht IPv4-adres dat zich niet achter een NAT bevinden.

**Punt-naar-Site** (VPN via SSTP) configuraties kunnen u vanaf één computer vanaf elke locatie verbinding maken tooanything zich in het virtuele netwerk. Hallo Windows meegeleverde VPN-client wordt gebruikt. Als onderdeel van Hallo punt-naar-Site-configuratie installeert u een certificaat en een VPN-client, dit pakket bevat Hallo-instellingen waarmee uw computer tooconnect tooany virtuele machine of rolinstantie in Hallo virtueel netwerk. Het is ideaal wanneer u tooconnect tooa virtueel netwerk wilt, maar worden niet zich op locatie. Het is ook een goede optie wanneer er geen toegang tot tooVPN hardware of een extern gericht IPv4-adres, die beide vereist voor een Site-naar-Site-verbinding zijn.

Kunt u uw virtuele netwerk toouse beide Site-naar-Site en punt-naar-Site gelijktijdig, zolang u de Site-naar-Site verbinding maken met een op route gebaseerde VPN-type voor uw gateway. Op route gebaseerde VPN-typen worden dynamische gateways genoemd in het klassieke implementatiemodel Hallo.

## <a name="gateways"></a>Virtuele netwerkgateways

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Is een VPN-gateway een virtuele netwerkgateway?

Een VPN-gateway is een type virtuele netwerkgateway. Een VPN-gateway verzendt via een openbare verbinding versleuteld verkeer tussen uw virtuele netwerk en uw on-premises locatie. U kunt ook een VPN-gateway toosend verkeer tussen virtuele netwerken gebruiken. Wanneer u een VPN-gateway maakt, kunt u Hallo - GatewayType waarde 'VPN-' gebruiken. Zie [Informatie over VPN-gatewayconfiguratie-instellingen](vpn-gateway-about-vpn-gateway-settings.md) voor meer informatie.

### <a name="what-is-a-policy-based-static-routing-gateway"></a>Wat is een op beleid gebaseerde gateway (statische routering)?

Op beleid gebaseerde gateways implementeren op beleid gebaseerde VPN's. Op beleid gebaseerde VPN-verbindingen versleutelen pakketten en sturen via IPsec-tunnels op basis van Hallo combinaties van adresvoorvoegsels tussen uw on-premises netwerk en hello Azure VNet. Hallo-beleid (of de Verkeersselector) wordt gewoonlijk gedefinieerd als een toegangslijst in Hallo VPN-configuratie.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Wat is een op route gebaseerde gateway (dynamische routering)?

Op route gebaseerde gateways implementeren Hallo route gebaseerde VPN's. Op route gebaseerde VPN's gebruiken 'routes' hello IP-doorstuurtabel of doorsturen van tabel toodirect pakketten in de bijbehorende tunnelinterfaces. vervolgens Hallo tunnelinterfaces versleutelen of ontsleutelen hello-pakketten naar en vanuit Hallo tunnels. Hallo beleid of de verkeersselector voor op route gebaseerde VPN's zijn geconfigureerd als alles-naar-alles (of jokertekens).

### <a name="do-i-need-a-gatewaysubnet"></a>Heb ik een gatewaysubnet nodig?

Ja. gatewaysubnet Hallo bevat Hallo IP-adressen die gebruikmaken van services voor virtueel netwerk gateway Hallo. U moet een gatewaysubnet toocreate voor uw VNet in volgorde tooconfigure een virtuele netwerkgateway. Alle gatewaysubnetten moeten de naam 'GatewaySubnet' toowork goed. Geef het gatewaysubnet geen andere naam. En virtuele machines of alles anders toohello gatewaysubnet niet implementeren.

Wanneer u Hallo gatewaysubnet maakt, geeft u het aantal IP-adressen die subnet Hallo Hallo bevat. Hallo IP-adressen in het gatewaysubnet Hallo eerder toegewezen toohello gateway-service. Sommige configuraties moeten meer IP-adressen toobe toegewezen toohello gatewayservices dan andere. Wilt u ervoor dat het gatewaysubnet bevat onvoldoende IP-adressen tooaccommodate toekomstige groei en mogelijk aanvullende nieuwe verbinding configuraties toomake. U kunt dus wel een gatewaysubnet maken met een grootte van slechts /29, maar het wordt aangeraden om een gatewaysubnet van /27 of groter te maken (/27, /26, /25 enz.). Hallo-vereisten voor de configuratie van Hallo kijken u toocreate wilt gebruiken en controleer of dat Hallo gatewaysubnet dat u voldoet aan deze vereisten.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>Kan ik virtuele Machines of rollen exemplaren toomy gatewaysubnet implementeren?

Nee.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Kan ik het IP-adres van de VPN-gateway verkrijgen voordat ik de gateway maak?

Nee. U hebt uw eerste tooget Hallo IP-gatewayadres toocreate. Hallo IP-adres verandert als u verwijdert en opnieuw maken van uw VPN-gateway.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>Kan ik een statisch openbaar IP-adres voor mijn VPN-gateway aanvragen?

Nee. Alleen dynamische IP-adrestoewijzing wordt ondersteund. Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen. de enige keer Hallo IP-adreswijzigingen voor Hallo VPN-gateway is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Hallo openbare IP-adres van VPN-gateway verandert niet via vergroten of verkleinen, opnieuw wordt ingesteld, of een andere interne onderhoud of upgrades worden uitgevoerd van uw VPN-gateway. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>Hoe wordt mijn VPN-tunnel geverifieerd?

Azure VPN maakt gebruik van PSK-verificatie (verificatie op basis van een vooraf gedeelde sleutel). We een vooraf gedeelde sleutel (PSK) genereren wanneer we Hallo VPN-tunnel maakt. U kunt Hallo automatisch gegenereerde PSK tooyour eigen met Hallo ingesteld Pre-Shared Key PowerShell-cmdlet of REST-API wijzigen.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>Kan ik gebruiken Hallo API Set Pre-Shared Key tooconfigure mijn op beleid gebaseerde VPN-gateway (statische routering)?

Ja, Hallo API Set Pre-Shared Key en PowerShell-cmdlet gebruikt tooconfigure kan worden zowel Azure op beleid gebaseerde (statische) VPN-verbindingen en route-gebaseerd (dynamische) routering VPN-verbindingen.

### <a name="can-i-use-other-authentication-options"></a>Kan ik andere verificatieopties gebruiken?

We zijn beperkt toousing vooraf gedeelde sleutels (PSK) voor verificatie.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Hoe geef ik op welk verkeer via Hallo VPN-gateway loopt?

#### <a name="resource-manager-deployment-model"></a>Resource Manager-implementatiemodel

* PowerShell: 'AddressPrefix' toospecify verkeer voor de lokale netwerkgateway hello gebruiken.
* Azure-portal: de lokale netwerkgateway toohello navigeren > Configuration >-adresruimte.

#### <a name="classic-deployment-model"></a>Klassiek implementatiemodel

* Azure-portal: Ga toohello klassiek virtueel netwerk > VPN-verbindingen > Site-naar-site VPN-verbindingen > lokale sitenaam > lokale site > adresruimte van de Client. 
* Klassieke portal: elk bereik dat u voor het virtuele netwerk op de pagina van de Hallo netwerken onder lokale netwerken verzonden via de gateway Hallo wilt toevoegen. 

### <a name="can-i-configure-forced-tunneling"></a>Kan ik geforceerde tunneling configureren?

Ja. Zie [Configure forced tunneling](vpn-gateway-about-forced-tunneling.md) (Geforceerde tunneling configureren).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>Kan ik mijn eigen VPN-server in Azure instellen en gebruiken tooconnect toomy on-premises netwerk?

Ja, kunt u uw eigen VPN-gateways of -servers in Azure vanuit Azure Marketplace Hallo of maken van uw eigen VPN-routers implementeren. U moet de gebruiker gedefinieerde routes tooconfigure in uw virtuele netwerk tooensure verkeer juist wordt gerouteerd tussen uw on-premises netwerken en de subnetten van het virtuele netwerk.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Waarom zijn bepaalde poorten geopend op mijn VPN-gateway?

Deze zijn nodig voor communicatie met de Azure-infrastructuur. Ze zijn beveiligd (vergrendeld) met Azure-certificaten. Zonder de juiste certificaten kunnen externe entiteiten, waaronder Hallo klanten van deze gateways, worden niet kunnen toocause een op de eindpunten effect.

Een VPN-gateway is in feite een multihomed apparaat met één NIC te tikken in Hallo klant particulier netwerk en één NIC gerichte Hallo openbaar netwerk. Infrastructuurentiteiten van Azure toegang geen tot particuliere netwerken van klanten om wettelijke redenen, zodat ze voor infrastructuurcommunicatie tooutilize openbare eindpunten nodig hebben. Hallo openbare eindpunten worden periodiek gescand door de beveiligingscontrole van Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Meer informatie over gatewaytypen, vereisten en doorvoer

Zie [Informatie over VPN-gatewayconfiguratie-instellingen](vpn-gateway-about-vpn-gateway-settings.md) voor meer informatie.

## <a name="s2s"></a>Site-naar-site-verbindingen en VPN-apparaten

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Waaraan moet ik denken bij het selecteren van een VPN-apparaat?

We hebben samen met apparaatleveranciers een reeks standaard site-naar-site-VPN-apparaten gevalideerd. Een lijst met bekende compatibele VPN-apparaten, hun bijbehorende configuratie-instructies of voorbeelden en apparaatspecificaties vindt u in Hallo [over VPN-apparaten](vpn-gateway-about-vpn-devices.md) artikel. Alle apparaten in Hallo apparaatfamilies die worden vermeld als compatibel moeten samenwerken met het virtuele netwerk. toohelp configureren van uw VPN-apparaat, toohello apparaat configuratievoorbeeld of koppeling die overeenkomt met de apparaatfamilie tooappropriate verwijzen.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Waar vind ik configuratie-instellingen voor VPN-apparaten?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Hoe bewerk ik voorbeelden van VPN-apparaatconfiguraties?

Zie [Bewerkingsvoorbeelden](vpn-gateway-about-vpn-devices.md#editing) voor voorbeelden van het bewerken van de apparaatconfiguratie.

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Waar vind ik IPsec- en IKE-parameters?

Zie [Parameters](vpn-gateway-about-vpn-devices.md#ipsec) voor de IPsec-/IKE-parameters.

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Waarom wordt mijn op beleid gebaseerde VPN-tunnel inactief als er geen verkeer is?

Dit is normaal voor op beleid gebaseerde VPN-gateways (ook wel bekend als statische routering genoemd). Wanneer het Hallo-verkeer via de tunnel Hallo niet actief is gedurende meer dan 5 minuten, wordt Hallo tunnel verwijderd. Wanneer weer verkeer is in beide richtingen, wordt de tunnel Hallo onmiddellijk hersteld.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>Kan ik software VPN-verbindingen tooconnect tooAzure gebruiken?

Windows Server 2012 RRAS-servers (Routering en RAS) worden ondersteund voor site-naar-site-cross-premises-configuratie.

Andere VPN-softwareoplossingen moeten samen met onze gateway zolang ze tooindustry IPsec-implementaties voldoen. Neem contact op met de Hallo leverancier van Hallo-software voor configuratie- en ondersteuningsinstructies.

## <a name="P2S"></a>Punt-naar-site-verbindingen

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>VNet-naar-VNET- en multi-site-verbindingen

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>Kan ik Azure VPN-gateway tootransit verkeer tussen mijn lokale sites of tooanother virtueel netwerk gebruiken?

**Resource Manager-implementatiemodel**<br>
Ja. Zie Hallo [BGP](#bgp) sectie voor meer informatie.

**Klassiek implementatiemodel**<br>
Transitverkeer via Azure VPN-gateway is mogelijk met het klassieke implementatiemodel hello, maar is afhankelijk van statisch gedefinieerde adresruimten in het configuratiebestand Hallo-netwerk. BGP is nog niet ondersteund met Azure Virtual Networks en VPN-gateways met Hallo klassieke implementatiemodel. Zonder BGP is het handmatig definiëren van adresruimten voor doorvoer zeer foutgevoelig en het wordt daarom niet aanbevolen.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Genereert Azure Hallo dezelfde IPsec/IKE vooraf gedeelde sleutel voor Mijn VPN-verbindingen voor Hallo hetzelfde virtuele netwerk?

Nee, Azure genereert standaard verschillende vooraf gedeelde sleutels voor verschillende VPN-verbindingen. U kunt echter Hallo ingesteld VPN-Gateway REST-API of PowerShell-cmdlet tooset Hallo gewenste sleutelwaarde. Hallo-sleutel moet alfanumerieke tekenreeks van tussen de 1 too128 tekens lang zijn.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Krijg ik meer bandbreedte met meerdere site-naar-site-VPN-verbindingen dan met één virtueel netwerk?

Nee, alle VPN-tunnels, inclusief punt-naar-Site VPN-verbindingen, delen dezelfde Azure VPN-gateway en Hallo beschikbare bandbreedte Hallo.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Kan ik meerdere tunnels tussen mijn virtuele netwerk en mijn on-premises site configureren met multi-site-VPN?

Ja, maar moet u BGP configureren op beide toohello tunnels dezelfde locatie.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Kan ik punt-naar-site-VPN-verbindingen met het virtuele netwerk gebruiken met meerdere VPN-tunnels?

Ja, punt-naar-Site (P2S) VPN-verbindingen kunnen worden gebruikt met Hallo VPN-gateways verbinden toomultiple on-premises sites en andere virtuele netwerken.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>Kan ik een virtueel netwerk verbinden met IPsec VPN-verbindingen toomy ExpressRoute-circuit?

Ja, dit wordt ondersteund. Voor meer informatie raadpleegt u [Expressroute en site-naar-site-VPN-verbindingen die naast elkaar kunnen worden gebruikt configureren](../expressroute/expressroute-howto-coexist-classic.md)

## <a name="ipsecike"></a>IPsec/IKE-beleid

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Cross-premises-connectiviteit en virtuele machines

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Als de virtuele machine zich in een virtueel netwerk en ik een cross-premises-verbinding heb, hoe moet ik verbinding toohello VM?

U hebt een aantal opties. Als u RDP ingeschakeld voor uw virtuele machine hebt, kunt u tooyour virtuele machine met behulp van Hallo privé IP-adres. In dat geval geeft u Hallo privé IP-adres en het Hallo-poort die u tooconnect te wilt (meestal 3389). U moet tooconfigure Hallo poort op de virtuele machine voor Hallo-verkeer.

U kunt ook tooyour virtuele machine verbinden met privé IP-adres van een andere virtuele machine die is bevindt op Hallo hetzelfde virtuele netwerk. U kunt geen RDP tooyour virtuele machine met behulp van Hallo privé IP-adres als u verbinding vanaf een locatie buiten het virtuele netwerk maakt. Als er een punt-naar-Site van een virtueel netwerk is geconfigureerd en u geen verbinding maakt vanaf uw computer, kan geen u toohello virtuele machine verbinding op persoonlijke IP-adres.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Als mijn virtuele machine zich in een virtueel netwerk met cross-premises connectiviteit, alle Hallo verkeer vanuit Mijn VM via die verbinding?

Nee. Alleen Hallo-verkeer met een doel-IP dat is opgenomen in Hallo virtueel netwerk lokale netwerk-IP-adresbereiken die u hebt opgegeven, loopt via Hallo virtuele netwerkgateway. Verkeer heeft een doel-IP binnen het virtuele netwerk Hallo binnen het virtuele netwerk Hallo blijft. Het andere verkeer wordt verzonden via openbare netwerken voor Hallo load balancer toohello of als geforceerde tunneling wordt gebruikt, verzonden via hello Azure VPN-gateway.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Hoe kan ik een RDP-verbinding tooa VM oplossen

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Veelgestelde vragen over Virtual Network

U extra virtuele netwerkgegevens weergeven in Hallo [Veelgestelde vragen over het virtuele netwerk](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Volgende stappen

* Zie [Over VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN Gateway.
* Zie [Informatie over VPN-gatewayconfiguratie-instellingen](vpn-gateway-about-vpn-gateway-settings.md) voor meer informatie over VPN-gatewayconfiguratie-instellingen.
