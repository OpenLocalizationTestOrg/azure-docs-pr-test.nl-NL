---
title: aaaAzure netwerken | Microsoft Docs
description: Meer informatie over Azure netwerkservices en mogelijkheden.
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Azure-netwerken

Azure biedt tal van netwerkmogelijkheden die samen of afzonderlijk kunnen worden gebruikt. Klik op een Hallo kernfuncties toolearn meer informatie hierover te volgen:
- [Connectiviteit tussen Azure-resources](#connectivity): verbinding maken met Azure-resources samen in een beveiligd, persoonlijk virtueel netwerk in Hallo cloud.
- [Verbinding met Internet](#internet-connectivity): tooand van Azure-resources via Hallo Internet communiceren.
- [Lokale connectiviteit](#on-premises-connectivity): verbinding maken met een lokale netwerk tooAzure bronnen via een virtueel particulier netwerk (VPN) via Hallo Internet of via een speciale verbinding tooAzure.
- [Load balancing en verkeer richting](#load-balancing): Load balance verkeer tooservers in Hallo dezelfde locatie en direct verkeer tooservers op verschillende locaties.
- [Beveiliging](#security): filteren van netwerkverkeer tussen subnetten of afzonderlijke virtuele machines (VM).
- [Routering](#routing): gebruik standaardroutering of volledig beheren routering tussen uw Azure- en on-premises resources.
- [Beheerbaarheid](#manageability): bewaken en beheren van uw Azure VPN-resources.
- [Hulpprogramma's voor implementatie en configuratie](#tools): een webportal of de opdrachtregelprogramma's voor meerdere platforms toodeploy gebruiken en netwerkbronnen configureren.

## <a name="Connectivity"></a>Connectiviteit tussen Azure-resources

Azure-resources, zoals virtuele Machines, Cloud Services-Schaalsets virtuele Machines en Azure App Service-omgevingen kunnen privé met elkaar communiceren via een virtueel Azure-netwerk (VNet). Een VNet is een logische isolatie van hello Azure-cloud-specifieke tooyour [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). U kunt meerdere VNets binnen elk Azure-abonnement en Azure implementeren [regio](https://azure.microsoft.com/regions). Elke VNet is geïsoleerd van andere vnet's. U kunt voor elk VNet:

- Geef een aangepaste persoonlijke IP-adresruimte met behulp van openbare en persoonlijke (RFC 1918)-adressen. Azure wijst bronnen verbonden toohello VNet een particulier IP-adres van de adresruimte Hallo die u toewijzen.
- Segmenteer Hallo VNet in een of meer subnetten en een deel van Hallo VNet-ruimte tooeach adressubnet toewijzen.
- Gebruik Azure verschafte naamomzetting of geef dat uw eigen DNS-server voor gebruik door resources verbonden tooa VNet.

meer informatie over hello Azure Virtual Network service, Hallo lezen toolearn [Virtual network-overzicht](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel. U verbinding kunt maken met andere VNets tooeach, resources inschakelen tooeither VNet toocommunicate met elkaar verbonden via VNets. U kunt een of beide van de volgende opties tooconnect VNets tooeach andere hello gebruiken:

- **Peering:** kunnen bronnen verbonden toodifferent Azure VNets binnen Hallo dezelfde Azure-regio toocommunicate met elkaar. Hallo bandbreedte en de latentie tussen VNets is Hallo Hallo dezelfde alsof Hallo resources verbonden toohello hetzelfde VNet. toolearn meer informatie over peering, lezen Hallo [peering Virtual network-overzicht](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **VPN-Gateway:** kunnen resources toodifferent Azure VNets in verschillende Azure-regio's toocommunicate met elkaar verbonden. Verkeer tussen VNets loopt via een Azure VPN-Gateway. Bandbreedte tussen VNets is beperkt toohello bandbreedte van Hallo-gateway. meer over het VNets verbinden met een VPN-Gateway, Hallo lezen toolearn [configureren van een VNet-naar-VNet-verbinding tussen regio's](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

## <a name="internet-connectivity"></a>Verbinding met Internet

Alle Azure-resources verbonden tooa VNet hebben uitgaande verbinding toohello Internet standaard. Hallo privé IP-adres van bron Hallo is Bronnetwerk adres (snat omzetten) tooa openbaar IP-adres vertaald door hello Azure-infrastructuur. meer informatie over uitgaande internetverbinding lezen Hallo toolearn [inzicht in uitgaande verbindingen in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

toocommunicate inkomende tooAzure resources uit Hallo Internet of toocommunicate uitgaande toohello Internet zonder snat omzetten, een resource moet een openbaar IP-adres worden toegewezen. meer informatie over openbare IP-adressen, Hallo lezen toolearn [openbare IP-adressen](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

## <a name="on-premises-connectivity"></a>Lokale connectiviteit

U kunt toegang tot bronnen in uw VNet veilig via een VPN-verbinding of een directe particuliere verbinding. toosend netwerkverkeer tussen uw virtuele Azure-netwerk en uw on-premises netwerk, moet u een virtuele netwerkgateway maken. U configureren instellingen voor Hallo gateway toocreate Hallo type verbinding dat u wilt, VPN- of ExpressRoute.

U kunt verbinding maken uw lokale netwerk tooa VNet met elke combinatie van Hallo volgende opties:

**Punt-naar-site (VPN via SSTP)**

Hallo volgende afbeelding ziet u afzonderlijke punt toosite verbindingen tussen meerdere computers en een VNet:

![Punt-naar-site](./media/networking-overview/point-to-site.png)

Deze verbinding tot stand is gebracht tussen één computer en een VNet. Dit verbindingstype is handig als u alleen aan de slag met Azure of voor ontwikkelaars, omdat hiervoor weinig of geen wijzigingen tooyour bestaande netwerk. Het is ook handig wanneer u verbinding vanaf een externe locatie, zoals een vergaderruimte maakt of thuis. Punt-naar-site-verbindingen zijn vaak samen met een site-naar-site-verbinding via Hallo dezelfde virtuele netwerkgateway. Hallo-verbinding gebruikt Hallo SSTP protocol tooprovide gecodeerde communicatie via Internet Hallo tussen Hallo-computer en Hallo VNet. Hallo latentie voor een punt-naar-site VPN-verbinding is onvoorspelbare, aangezien Hallo verkeer Hallo Internet passeert.

**Site-naar-site (IPsec/IKE-VPN-tunnel)**

![Site-naar-site](./media/networking-overview/site-to-site.png)

Deze verbinding tot stand is gebracht tussen uw on-premises VPN-apparaat en een Azure VPN-Gateway. Dit verbindingstype kunt een on-premises-resource of u wilt hello tooaccess VNet autoriseren. Hallo-verbinding is een VPN IPSec/IKE waarmee gecodeerde communicatie via Internet Hallo tussen uw on-premises apparaat en hello Azure VPN-gateway. U kunt meerdere lokale sites toohello verbinden dezelfde VPN-gateway. Hallo lokale VPN-apparaat op elke site moet een extern gericht openbaar IP-adres die zich niet achter een NAT bevinden. Hallo latentie voor een site-naar-site-verbinding is onvoorspelbaar zijn, aangezien Hallo verkeer Hallo Internet passeert.

**ExpressRoute (speciale persoonlijke verbinding)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Dit type verbinding tot stand is gebracht tussen uw netwerk en Azure, via een ExpressRoute-partner. Deze verbinding is een privéverbinding. Verkeer komt geen Hallo Internet passeren. Hallo latentie voor een ExpressRoute-verbinding is betrouwbaar, aangezien verkeer Hallo Internet niet passeren. ExpressRoute kan worden gecombineerd met een site-naar-site-verbinding.

meer informatie over alle Hallo vorige verbindingsopties lezen Hallo toolearn [gatewayverbindingsdiagrammen topologie](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

## <a name="load-balancing"></a>Load balancing en verkeer richting

Microsoft Azure biedt meerdere services voor het beheren van het netwerkverkeer wordt gedistribueerd en taakverdeling. U kunt een Hallo mogelijkheden na afzonderlijk of samen gebruiken:

**DNS taakverdeling**

Hello Azure Traffic Manager-service biedt globale DNS-taakverdeling. Traffic Manager reageert tooclients met Hallo IP-adres van een gezonde-eindpunt op basis van een Hallo methoden volgen:
- **Geografisch:** Clients worden omgeleid toospecific eindpunten (Azure, externe of geneste) op basis van welke geografische locatie hun DNS-query is afkomstig uit. Deze methode kunt scenario's waar dat bekend is van een client geografische regio en routering toe op basis van het is belangrijk. Voorbeelden zijn die voldoet aan gegevens onafhankelijkheid vereist, lokalisatie van inhoud & gebruiker ervaring, en het meten van verkeer vanuit verschillende regio's.
- **Prestaties:** Hallo IP-adres toohello client wordt Hallo 'dichtstbijzijnde' toohello client geretourneerd. 'dichtstbijzijnde' Hallo-eindpunt is niet noodzakelijkerwijs dichtstbijzijnde door geografische afstand wordt gemeten. Deze methode bepaalt in plaats daarvan de dichtstbijzijnde eindpunt Hallo netwerklatentie meten. Traffic Manager onderhoudt een Internet latentie tabel tootrack Hallo round trip tijd tussen het IP-adresbereiken en elke Azure-datacenter.
- **Prioriteit:** verkeer is gerichte toohello primaire (hoogste prioriteit)-eindpunt. Als de primaire Hallo-eindpunt is niet beschikbaar, Hallo Traffic Manager routes verkeer toohello tweede eindpunt. Als beide Hallo primaire en secundaire eindpunten niet beschikbaar zijn, gaat het Hallo-verkeer toohello derde, enzovoort. Beschikbaarheid van het Hallo-eindpunt is gebaseerd op Hallo geconfigureerd status (ingeschakeld of uitgeschakeld) en Hallo lopende eindpuntcontrole.
- **Gewogen round robin:** voor elke aanvraag kiest Traffic Manager willekeurig een beschikbare eindpunt. Hallo waarschijnlijkheid van het kiezen van een eindpunt is gebaseerd op Hallo gewichten tooall beschikbare eindpunten toegewezen. Hallo met hetzelfde gewicht over alle eindpunten resulteert in een zelfs distributie van verkeer. Met behulp van hogere of lagere gewichten op specifieke eindpunten zorgt ervoor dat deze eindpunten toobe meer of minder vaak in Hallo DNS-antwoorden worden geretourneerd.

Hallo volgende afbeelding ziet u een aanvraag voor een web application omgeleid tooa Web-App-eindpunt. Eindpunten kunnen ook worden andere Azure-services zoals virtuele machines en Cloudservices.

![Traffic Manager](./media/networking-overview/traffic-manager.png)

Hallo-client verbinding rechtstreeks toothat eindpunt. Azure Traffic Manager detecteert wanneer een eindpunt beschadigd is en wordt vervolgens omgeleid clients tooa afwijken, in orde eindpunt. meer over Traffic Manager lezen Hallo toolearn [overzicht van Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

**Taakverdeling voor toepassingen**

Hello Azure Application Gateway-service biedt toepassing levering controller (ADC) als een service. Toepassingsgateway biedt verschillende laag 7 (HTTP/HTTPS) taakverdeling mogelijkheden voor uw toepassingen, met inbegrip van een webtoepassing firewall tooprotect uw webtoepassingen van zwakke plekken en aanvallen. Toepassingsgateway kunt u ook toooptimize web farm productiviteit door het offloaden van CPU-intensief SSL-beëindiging toohello toepassingsgateway. 

Andere mogelijkheden voor het doorsturen van laag 7 bevatten round-robin distributie van inkomend verkeer, sessie cookies gebaseerde affiniteit URL-pad gebaseerde routering en Hallo mogelijkheid toohost meerdere websites achter een gateway één toepassing. Application Gateway kan worden geconfigureerd als een gateway internetgerichte, een gateway interne alleen-lezen of een combinatie van beide. Toepassingsgateway is volledig Azure beheerde, schaalbare en maximaal beschikbaar. Het biedt een uitgebreide verzameling diagnostische gegevens en functies voor logboekregistratie voor betere beheersbaarheid. meer informatie over Application Gateway, Hallo lezen toolearn [Application Gateway overzicht](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

Hallo volgende afbeelding ziet u URL-pad gebaseerde routering met Application Gateway:

![Application Gateway](./media/networking-overview/application-gateway.png)

**Taakverdeling voor netwerken**

Hello Azure Load Balancer biedt hoge prestaties, lage latentie laag 4-taakverdeling voor alle UDP en TCP-protocollen. Het beheert binnenkomende en uitgaande verbindingen. U kunt de openbare en interne eindpunten voor netwerktaakverdeling configureren. U kunt regels toomap definiëren voor binnenkomende verbindingen tooback-end-pool bestemmingen via TCP- en HTTP-status probing opties toomanage beschikbaarheid van de service. meer informatie over de Load Balancer, Hallo lezen toolearn [overzicht van de Load Balancer](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

Hallo volgende afbeelding ziet u een internetgerichte toepassing met meerdere lagen die gebruikmaakt van zowel externe en interne load balancers:

![Load balancer](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Beveiliging

U kunt filteren tooand verkeer vanuit Azure-resources met behulp van Hallo volgende opties:

- **Netwerk:** kunt u implementeren Azure network security groepen (nsg's) toofilter binnenkomend en uitgaand verkeer tooAzure resources. Elke NSG bevat een of meer regels voor binnenkomend en uitgaand. Elke regel geeft Hallo bron-IP-adressen, IP-doeladressen, poort en protocol dat verkeer wordt gefilterd met. Nsg's kunnen worden toegepast tooindividual subnetten en afzonderlijke virtuele machines. meer informatie over nsg's, Hallo lezen toolearn [netwerk beveiligingsgroepen overzicht](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Toepassing:** met behulp van een toepassingsgateway met web application firewall kunt u uw webtoepassingen beschermen tegen beveiligingsproblemen en aanvallen. Algemene voorbeelden zijn SQL-injectieaanvallen, cross-site scripting en een verkeerd ingedeelde kopteksten. Toepassingsgateway dit verkeer gefilterd en voorkomt dat uw webservers is bereikt. U bent kunnen tooconfigure welke regels gewenste ingeschakeld. onderhandelingsbeleid voor Hallo mogelijkheid tooconfigure SSL wordt verstrekt tooallow bepaalde beleidsregels toobe uitgeschakeld. meer informatie over Hallo web application firewall lezen Hallo toolearn [Web application firewall](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

Als u moet de mogelijkheid via het netwerk Azure niet opgeven of toouse netwerktoepassingen die u lokaal wilt, kunt u deze kunt Hallo-producten implementeren in virtuele machines en verbind ze tooyour VNet. Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) bevat verschillende andere virtuele machines die vooraf geconfigureerd met de netwerktoepassingen die u kunt. Deze vooraf geconfigureerde virtuele machines zijn doorgaans waarnaar wordt verwezen tooas virtuele netwerkapparaten (NVA). NVAs zijn beschikbaar met toepassingen zoals firewall en WAN-optimalisatie.

## <a name="routing"></a>Routering

Azure maakt standaard routetabellen waarmee bronnen verbonden tooany subnet in een VNet toocommunicate met elkaar. U kunt ofwel implementeren of beide van de volgende soorten routes toooverride Hallo Hallo standaardroutes die Azure maakt:
- **De gebruiker gedefinieerde:** kunt u aangepaste routetabellen met routes die regelen waarin verkeer wordt gerouteerd toofor elk subnet. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [gebruiker gedefinieerde routes](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Border gateway protocol (BGP):** als u verbinding maakt met uw VNet tooyour on-premises netwerk via een Azure VPN-Gateway of ExpressRoute-verbinding, BGP-routes tooyour vnet's kunnen worden doorgegeven. BGP is Hallo standaardprotocol voor routering gebruikte in Hallo Internet tooexchange Routering en bereikbaarheid tussen twee of meer netwerken. Wanneer gebruikt in de context van Azure Virtual Networks, BGP wordt hello Azure VPN-Gateways en uw on-premises VPN-apparaten Hallo opgeroepen BGP samenwerkt of neighbors tooexchange 'routes' die beide gateways over Hallo beschikbaarheid en bereikbaarheid voor deze voorvoegsels informeren toogo via Hallo gateways of routers die betrokken zijn. BGP ook transitroutering tussen meerdere netwerken door routes die een BGP-gateway van één BGP-peer-tooall leert andere BGP-peers. toolearn meer informatie over BGP, Zie Hallo [BGP met Azure VPN-Gateways overzicht](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

## <a name="manageability"></a>Beheerbaarheid

Azure biedt Hallo volgende hulpprogramma's voor toomonitor en beheren van netwerken:
- **Activiteitenlogboeken:** alle Azure-resources zijn activiteitenlogboeken waarin informatie over de uitgevoerde bewerkingen plaatst, status van bewerkingen en wie Hallo opnieuw gestart. meer informatie over activiteitenlogboeken, Hallo lezen toolearn [activiteit Logboeken overzicht](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Diagnostische logboeken:** periodiek en eigen initiatief gebeurtenissen zijn gemaakt door netwerkbronnen en geregistreerd in Azure storage-accounts, tooan Azure Event Hub wordt verzonden of tooAzure logboekanalyse verzonden. Diagnostische logboeken bieden inzicht toohello status van een resource. Diagnostische logboeken zijn beschikbaar voor de Load Balancer (internetgerichte), netwerk-beveiligingsgroepen, routes en Application Gateway. meer informatie over diagnostische logboeken, Hallo lezen toolearn [diagnostische logboeken overzicht](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Metrische gegevens:** metrische gegevens zijn metingen van de prestaties en prestatiemeteritems die gedurende een periode van bronnen worden verzameld. Metrische gegevens kunnen worden gebruikt tootrigger waarschuwingen op basis van drempelwaarden. Metrische gegevens zijn momenteel beschikbaar op Application Gateway. meer informatie over metrische gegevens en lezen Hallo toolearn [overzicht van metrische gegevens](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Problemen oplossen:** informatie over probleemoplossing is toegankelijk rechtstreeks in hello Azure-portal. Hallo informatie helpt bij het analyseren van algemene problemen met ExpressRoute, VPN-Gateway, Application Gateway, netwerk-beveiligingslogboeken, Routes, DNS, Load Balancer en Traffic Manager.
- **Op rollen gebaseerde toegangsbeheer (RBAC):** bepalen wie kunt maken en beheren van netwerkresources met op rollen gebaseerde toegangsbeheer (RBAC). Meer informatie over RBAC door te lezen Hallo [aan de slag met RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel. 
- **Pakketopname:** hello Azure netwerk-Watcher-service biedt Hallo mogelijkheid toorun vastleggen van een pakket op een virtuele machine via een Hallo VM-extensie. Deze functie is beschikbaar voor Linux en Windows-VM's. meer informatie over pakketopname, Hallo lezen toolearn [pakket vastleggen overzicht](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Controleer of IP-stromen:** netwerk-Watcher Hiermee kunt u tooverify IP-stromen tussen een virtuele machine van Azure en een externe bron toodetermine of pakketten worden toegestaan of geweigerd. Deze mogelijkheid biedt beheerders de mogelijkheid Hallo tooquickly onderzoeken verbindingsproblemen. toolearn meer informatie over hoe tooverify IP loopt, lezen Hallo [IP-stroom controleren overzicht](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **VPN-connectiviteit oplossen:** Hallo VPN-probleemoplosser mogelijkheid van netwerk-Watcher biedt Hallo mogelijkheid tooquery een verbinding of de gateway en status van resources Hallo Hallo controleren. meer informatie over het oplossen van VPN-verbindingen kunnen lezen Hallo toolearn [VPN-verbinding overzicht probleemoplossing](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Netwerktopologie weergeven:** een grafische weergave van Hallo netwerkbronnen in een VNet met de netwerk-Watcher. meer over het weergeven van de netwerktopologie, Hallo lezen toolearn [topologie overzicht](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.

## <a name="tools"></a>Hulpprogramma's voor implementatie en configuratie

U kunt implementeren en Azure VPN-resources configureren met een van de Hallo hulpprogramma's te volgen:

- **Azure-portal:** een grafische gebruikersinterface die wordt uitgevoerd in een browser. Open Hallo [Azure-portal](http://portal.azure.com).
- **Azure PowerShell:** opdrachtregelprogramma's voor het beheren van Azure op Windows-computers. Meer informatie over Azure PowerShell lezen Hallo [overzicht van Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Azure-opdrachtregelinterface (CLI):** opdrachtregelprogramma's voor het beheren van Azure van Linux-, Mac OS- of Windows-computers. Meer informatie over hello Azure CLI door Hallo lezen [overzicht van Azure CLI](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- **Azure Resource Manager-sjablonen:** een bestand (in JSON-indeling) die Hallo-infrastructuur en configuratie van een Azure-oplossing bepaalt. Door het gebruik van een sjabloon kunt u gedurende de levenscyclus de oplossing herhaaldelijk implementeren en erop vertrouwen dat uw resources consistent worden geïmplementeerd. meer over het ontwerpen van sjablonen, Hallo lezen toolearn [aanbevolen procedures voor het maken van sjablonen](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel. Sjablonen kunnen worden geïmplementeerd met hello Azure-portal, CLI of PowerShell. tooget meteen gestart met behulp van sjablonen implementeert een Hallo veel vooraf geconfigureerde sjablonen in Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/?term=network) bibliotheek. 

## <a name="pricing"></a>Prijzen

Sommige Hallo Azure netwerkservices hebben een kosten, terwijl andere gratis. Weergave Hallo [virtueel netwerk](https://azure.microsoft.com/pricing/details/virtual-network), [VPN-Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway), [Application Gateway](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [Load Balancer](https://azure.microsoft.com/pricing/details/load-balancer), [voornetwerk-Watcher](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) en [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) prijzen van pagina's voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- Maken van uw eerste VNet en verbinding maken met een paar virtuele machines tooit, via Hallo stappen in Hallo [maken van uw eerste virtuele netwerk](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- Verbinding maken met uw computer tooa VNet via Hallo stappen in Hallo [een punt-naar-site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
- Taakverdeling maken voor Internet verkeer toopublic-servers via Hallo stappen in Hallo [een internetgerichte load balancer maken](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artikel.
