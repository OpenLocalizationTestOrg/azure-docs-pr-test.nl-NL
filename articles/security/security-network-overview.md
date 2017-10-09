---
title: aaaNetwork veiligheidsconcepten & vereisten in Azure | Microsoft Docs
description: " In dit artikel kunt u gemakkelijk voor u toounderstand wat Microsoft Azure heeft toooffer in Hallo gebied van netwerkbeveiliging. We leveren basic uitleg voor core network security concepten en vereisten en informatie over welke Azure heeft toooffer in elk van deze gebieden. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Overzicht van Azure-netwerk-beveiliging
Microsoft Azure omvat een robuuste netwerken infrastructuur toosupport uw toepassing en de vereisten voor service-connectiviteit. Netwerkverbinding is tussen de bronnen in Azure, tussen on-premises en Azure gehoste bronnen, en tooand van Hallo Internet en Azure.

Hallo-doel van dit artikel toomake is het eenvoudiger voor u toounderstand wat Microsoft Azure heeft toooffer in Hallo gebied van netwerkbeveiliging. We bieden hier basic uitleg voor core network security concepten en vereisten. We bieden ook informatie over welke Azure heeft toooffer in elk van deze gebieden evenals koppelingen toohelp krijgt u een beter begrip van interessante gebieden.

In dit artikel beveiligingsoverzicht van Azure-netwerk is gericht op Hallo gebieden te volgen:

* Azure-netwerken
* Netwerktoegangsbeheer
* Veilige externe toegang en cross-premises-connectiviteit
* Beschikbaarheid
* Naamomzetting
* DMZ-architectuur
* Controle en detectie van bedreigingen


## <a name="azure-networking"></a>Azure-netwerken
Verbinding met het netwerk, moeten virtuele machines. toosupport is vereist dat dit vereiste, Azure virtuele machines toobe verbonden tooan Azure Virtual Network. Een Azure-netwerk is een logische constructie die is gebouwd op Hallo fysieke netwerk van Azure-infrastructuur. Elke logische Azure Virtual Network is geïsoleerd van alle andere virtuele netwerken van Azure. Dit helpt ervoor zorgen dat netwerkverkeer in uw implementaties niet toegankelijk tooother Microsoft Azure-klanten is.

Meer informatie:

* [Overzicht van Virtual Network](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Network Access Control
Netwerktoegangsbeheer wordt Hallo connectiviteit tooand van specifieke apparaten of subnetten binnen een Azure-netwerk te beperken. Hallo-doel van netwerktoegangsbeheer is toolimit toegang tooyour virtuele machines en services tooapproved gebruikers en apparaten. Toegangsbeheer zijn gebaseerd op toestaan of weigeren beslissingen voor verbindingen tooand van uw virtuele machine of service.

Azure ondersteunt meerdere typen van network access control zoals:

* Regeling van de laag
* Besturingselement routeren en geforceerde tunneling
* Virtueel netwerk beveiligingsapparaten

### <a name="network-layer-control"></a>Network Layer Control
Alle beveiligde implementatie vereist sommige meting van network access control. Hallo-doel van netwerktoegangsbeheer is toorestrict virtuele machine communicatie toohello nodig systemen en dat andere communicatiepogingen worden geblokkeerd.

Als u Basisnetwerk toegangsbeheer op gebruikersniveau (op basis van IP-adres en Hallo TCP of UDP-protocollen) nodig hebt, kunt u Netwerkbeveiligingsgroepen gebruiken. Een Netwerkbeveiligingsgroep (NSG) is een eenvoudige filterregels voor pakketten firewall en zorgt ervoor dat u toocontrol toegang op basis van een [5-tuple](https://www.techopedia.com/definition/28190/5-tuple). Nsg's bieden geen application layer inspectie of geverifieerde toegangsbeheer.

Meer informatie:

* [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Route besturingselement en geforceerde Tunneling
Hallo mogelijkheid toocontrol routeringsgedrag op uw virtuele Azure-netwerken is een kritieke beveiliging en toegang besturingselement mogelijkheid via het netwerk. Als routering verkeerd is geconfigureerd, kunnen toepassingen en services die worden gehost op de virtuele machine toounauthorized apparaten, zoals systemen die eigendom zijn van en beheerd door potentiële aanvallers verbinding.

Azure-netwerken ondersteunt Hallo mogelijkheid toocustomize Hallo routeringsgedrag voor netwerkverkeer op uw virtuele netwerken van Azure. Hiermee kunt u tooalter Hallo standaardvermeldingen in de routeringstabel in uw Azure Virtual Network. Besturingselement van het routeringsgedrag kunt u ervoor zorgen dat al het verkeer van een bepaald apparaat of een groep apparaten binnengaat of het virtuele netwerk via een specifieke locatie verlaat.

U wellicht bijvoorbeeld beveiliging van een virtueel netwerkapparaat op uw Azure Virtual Network. Wilt u ervoor dat alle verkeer tooand van uw Azure Virtual Network dat toestel virtuele beveiliging doorloopt toomake. U kunt dit doen door het configureren van [gebruiker gedefinieerde Routes](../virtual-network/virtual-networks-udr-overview.md) in Azure.

[Geforceerde tunneling](https://www.petri.com/azure-forced-tunneling) is een mechanisme kunt u tooensure die uw services niet zijn toegestaan tooinitiate een toodevices verbinding op Hallo Internet. Houd er rekening mee dat dit verschilt van binnenkomende verbindingen accepteert en vervolgens reageert toothem. Front-end-webservers moeten toorespond toorequests via Internet-hosts en dus Internet afkomstig verkeer is toegestaan inkomende toothese-webservers en webservers Hallo toorespond zijn toegestaan.

Wat u niet wilt tooallow is een front-end web server tooinitiate een uitgaande aanvraag. Dergelijke aanvragen mogelijk een beveiligingsrisico vertegenwoordigen, omdat deze verbindingen gebruikt toodownload malware worden kunnen. Zelfs als u wenst deze front-servers tooinitiate uitgaande aanvragen toohello Internet, kunt u tooforce ze toogo via uw on-premises web proxy's, zodat u kunt profiteren van de URL voor het filteren en logboekregistratie.

In plaats daarvan kunt u toouse geforceerde tunneling tooprevent dit. Wanneer u geforceerde tunneling inschakelt, worden alle verbindingen toohello Internet afgedwongen via uw on-premises gateway. U kunt configureren om geforceerde tunneling door gebruik te maken van de gebruiker gedefinieerde Routes.

Meer informatie:

* [Wat zijn de gebruiker gedefinieerde Routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Virtueel netwerk beveiligingsapparaten
Terwijl Netwerkbeveiligingsgroepen, de gebruiker gedefinieerde Routes en geforceerde tunneling u een niveau van beveiliging op de netwerk- en lagen Hallo Hallo bieden [OSI-model](https://en.wikipedia.org/wiki/OSI_model), het kan gebeuren als u wilt dat de beveiliging tooenable hogere niveaus dan Hallo-netwerk.

Bijvoorbeeld: de beveiligingsvereisten van uw kunnen opnemen:

* Verificatie en autorisatie voordat toegang tooyour toepassing toestaan
* Inbraakdetectie en inbraakdetectie antwoord
* Application layer inspectie van protocollen op hoog niveau
* URL-filtering
* Netwerk niveau antivirus- en antimalwaresoftware
* Bescherming tegen bot
* Toegangsbeheer voor toepassing
* Aanvullende DDoS-bescherming (hierboven Hallo DDoS-bescherming als gegeven hello Azure-infrastructuur zelf)

U kunt deze beveiligingsfuncties verbeterde netwerk openen met behulp van een Azure-partner-oplossing. U vindt Hallo meest recente Azure network security partneroplossingen Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/) en zoeken naar 'beveiliging' en "netwerkbeveiliging."

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Veilige externe toegang en Cross-Premises-connectiviteit
Installatie, configuratie en beheer van uw Azure-resources moet toobe op afstand worden uitgevoerd. Bovendien kunt u toodeploy [hybride IT](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) oplossingen die onderdelen on-premises en in hello Azure openbare cloud. Deze scenario's moet veilige externe toegang.

Azure-netwerken ondersteunt Hallo veilige externe toegang-scenario's te volgen:

* Verbinding maken met afzonderlijke werkstations tooan Azure Virtual Network
* Uw lokale netwerk tooan Azure Virtual Network bij een VPN-verbinding
* Verbinding maken met uw lokale netwerk tooan Azure Virtual Network met een specifieke WAN-verbinding
* Verbinding maken met Azure Virtual Networks tooeach andere

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Verbinding maken met afzonderlijke werkstations tooan Azure Virtual Network
Het kan gebeuren als u wilt dat tooenable afzonderlijke ontwikkelaars of operations personeel toomanage virtuele machines en services in Azure. Bijvoorbeeld, u moet toegang tot tooa virtuele machine op een Azure-netwerk en beveiligingsbeleid van uw daardoor niet RDP of SSH RAS tooindividual virtuele machines. In dit geval kunt u een punt-naar-site VPN-verbinding.

punt-naar-site VPN-verbinding gebruikmaakt Hallo Hallo [SSTP VPN](https://technet.microsoft.com/library/cc731352.aspx) protocol tooenable tooset om een persoonlijke en beveiligde verbinding tussen Hallo gebruiker en hello Azure Virtual Network. Als Hallo VPN-verbinding tot stand is gebracht, Hallo gebruiker worden kunnen tooRDP of SSH via VPN Hallo koppelen aan een virtuele machine op Hallo Azure Virtual Network (ervan uitgaande dat hello gebruiker kan worden geverifieerd en gemachtigd is).

Meer informatie:

* [Configureren van een punt-naar-Site-verbinding tooa virtueel netwerk met behulp van PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>Uw On-Premises netwerk tooan Azure Virtual Network bij een VPN-verbinding
U kunt tooconnect uw hele bedrijfsnetwerk of gedeelten van deze tooan Azure Virtual Network. Dit is gebruikelijk in hybride IT scenario's waarin bedrijven [datacenter op locatie uitbreiden in Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). In veel gevallen host bedrijven delen van een service in Azure en delen op locatie, zoals wanneer een oplossing voor de front-endwebservers in Azure en back-end databases on-premises bevat. Deze typen 'cross-premises' verbindingen maken ook beheer van Azure bevinden resources beter beveiligen en scenario's mogelijk, zoals Active Directory-domeincontrollers uit te breiden naar Azure.

Eenzijdige tooaccomplish dit toouse is een [site-naar-site VPN](https://www.techopedia.com/definition/30747/site-to-site-vpn). Hallo verschil tussen een site-naar-site-VPN en een punt-naar-site VPN is dat een punt-naar-site VPN verbinding een enkel apparaat tooan virtueel netwerk in Azure maakt tijdens een site-naar-site VPN een gehele netwerk (zoals uw on-premises netwerk) tooan Azure Virtual Network verbindt . Site-naar-site VPN-verbindingen tooan Azure Virtual Network Hallo maximaal beveiligde IPSec-tunnel modus VPN-protocol gebruiken.

Meer informatie:

* [Een Resource Manager VNet maken met een site-naar-site VPN-verbinding met hello Azure Portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Planning en ontwerp voor VPN Gateway](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Verbinding maken met uw On-premises netwerk tooan Azure Virtual Network met een specifiek WAN-koppeling
Punt-naar-site en site-naar-site VPN-verbindingen zijn nuttig voor het inschakelen van cross-premises connectiviteit. Sommige organisaties overwegen ze toohave Hallo volgende nadelen:

* VPN-verbindingen gegevens verplaatst via Internet Hallo – dit beschrijft deze verbindingen toopotential beveiligen met het verplaatsen van gegevens via een openbaar netwerk. Bovendien worden niet betrouwbaarheid en beschikbaarheid voor Internet-verbindingen gegarandeerd.
* VPN-verbindingen tooAzure virtuele netwerken kan worden overwogen bandbreedte beperkt voor sommige toepassingen en -doeleinden, als ze max uit met ongeveer 200 Mbps.

Organisaties die het hoogste niveau van beveiliging en beschikbaarheid voor hun cross-premises verbindingen moeten doorgaans Hallo Gebruik specifieke WAN-verbindingen tooconnect tooremote sites. Azure biedt dat u de mogelijkheid toouse een speciale WAN-koppeling die u tooconnect uw lokale netwerk tooan Azure Virtual Network gebruiken kunt Hallo. Dit wordt ingeschakeld via Azure ExpressRoute.

Meer informatie:

* [Technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Verbinding maken met Azure Virtual Networks tooEach andere
Het is mogelijk dat u toouse veel virtuele Azure-netwerken voor uw implementaties. Er zijn diverse redenen waarom u dit kunt doen. Een van de Hallo redenen mogelijk toosimplify management; het is mogelijk dat een andere uit veiligheidsoverwegingen. Ongeacht de Hallo motivering of logica voor het plaatsen van bronnen op verschillende virtuele netwerken van Azure kan gebeuren als u wilt dat de bronnen op elke Hallo netwerken tooconnect met elkaar.

Een optie voor services op één Azure Virtual Network tooconnect tooservices op een andere Azure Virtual Network door 'terug lussen' niet via Internet Hallo. Hallo verbinding wilt starten op een Azure Virtual Network, doorlopen Hallo Internet en vervolgens terugkeren toohello bestemming Azure Virtual Network. Deze optie wordt Hallo verbinding toohello beveiliging problemen inherente tooany Internet-communicatie.

Een betere optie is mogelijk een Azure virtuele netwerk naar Azure Virtual Network site-naar-site VPN toocreate. Dit virtuele Azure-netwerk naar Azure virtuele netwerk maakt gebruik van site-naar-site VPN Hallo dezelfde [IPsec-tunnelmodus](https://technet.microsoft.com/library/cc786385.aspx) protocol zoals Hallo cross-premises site-naar-site VPN-verbinding hierboven vermeld.

Hallo voordeel van het gebruik van een Azure virtuele netwerk naar Azure Virtual Network site-naar-site VPN is dat Hallo VPN-verbinding tot stand is gebracht via Hallo fabric Azure-netwerk in plaats van via Hallo Internet verbinding maken. Dit biedt dat u een extra beveiligingslaag toosite-naar-site-VPN's die verbinding via Internet Hallo maken vergeleken.

Meer informatie:

* [Een VNet-naar-VNet-verbinding configureren met behulp van Azure Resource Manager en PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Beschikbaarheid
Beschikbaarheid is een belangrijk onderdeel van elk beveiligingsprogramma. Als uw gebruikers en systemen geen toegang tot wat ze moeten tooaccess via Hallo-netwerk wordt hello service kan worden overwogen aangetast. Azure heeft netwerktechnologieën die ondersteuning Hallo mechanismen voor hoge beschikbaarheid te volgen:

* HTTP-gebaseerde taakverdeling
* Niveau voor netwerktaakverdeling
* Globale taakverdeling

De Load Balancer is een mechanisme ontworpen tooequally distribueren verbindingen tussen meerdere apparaten. Hallo doelstellingen van taakverdeling zijn:

* Beschikbaarheid – vergroten wanneer u saldo verbindingen op meerdere apparaten laden, een of meer Hallo apparaten niet beschikbaar zijn en Hallo services worden uitgevoerd op Hallo online apparaten resterende tooserve Hallo inhoud van Hallo-service kunnen worden voortgezet
* Betere prestaties – wanneer u saldo verbindingen op meerdere apparaten laadt, één apparaat tootake Hallo processor niet hebben bereikt. In plaats daarvan wordt Hallo capaciteit en geheugenbronnen verzoeken voor inhoud Hallo verdeeld over meerdere apparaten.

### <a name="http-based-load-balancing"></a>HTTP-gebaseerde taakverdeling
Organisaties die vaak webservices uitvoeren desire toohave een HTTP-gebaseerde load balancer voor deze web-services toohelp zorgen dat voldoende niveaus qua prestaties en hoge beschikbaarheid. Daarentegen tootraditional netwerk gebaseerde taakverdelers, hello load balancing beslissingen van HTTP-gebaseerde netwerktaakverdelers worden op basis van kenmerken Hallo HTTP-protocol niet op Hallo netwerk- en protocollen die gebruikmaken van.

tooprovide u HTTP-gebaseerde taakverdeling voor uw web gebaseerde services, Azure biedt u hello Azure Application Gateway. Hello Azure Application Gateway ondersteunt:

* HTTP-gebaseerde taakverdeling – load balancing beslissingen zijn gemaakt op basis van kenmerkende speciale toohello HTTP-protocol
* Sessie cookies gebaseerde affiniteit – deze mogelijkheid ervoor zorgt dat verbindingen tooone Hallo-servers achter die load balancer blijft intact tussen Hallo-client en server gemaakt. Hierdoor weet u zeker stabiliteit van transacties.
* SSL-offload – wanneer een clientverbinding tot stand is gebracht met Hallo load balancer, sessie tussen Hallo-client en Hallo load balancer is versleuteld met behulp van Hallo HTTPS (SSL /) protocol. Echter, in volgorde tooincrease prestaties hebt u Hallo optie toohave Hallo verbinding tussen Hallo load balancer en de webserver Hallo achter Hallo load balancer gebruik hello (niet-versleuteld) HTTP-protocol. Namelijk waarnaar wordt verwezen tooas 'SSL-offload' Hallo webservers achter Hallo load balancer niet ervaren processoroverhead Hallo betrokken met versleuteling en moeten daarom kunnen tooservice aanvragen sneller zijn.
* URL gebaseerde inhoud routering – deze functie maakt het mogelijk voor Hallo load balancer toomake besluiten over waar tooforward verbindingen op basis van Hallo doel-URL. Dit biedt veel meer flexibiliteit dan oplossingen die u de werklast verdelen beslissingen op basis van IP-adressen.

Meer informatie:

* [Overzicht van Application Gateway](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Niveau voor netwerktaakverdeling
Daarentegen maakt tooHTTP-gebaseerde taakverdeling, niveau Netwerktaakverdeling taakverdeling beslissingen op basis van IP-adres en poort (TCP of UDP) nummers worden geladen.
U kunt toegang Hallo voordelen van het niveau voor netwerktaakverdeling in Azure met behulp van hello Azure Load Balancer. Er zijn een aantal belangrijke kenmerken van hello Azure Load Balancer:

* Netwerktaakverdeling voor niveau op basis van IP-adres en poort-nummers
* Ondersteuning voor elk application layer protocol
* Load tegoeden tooAzure virtuele machines en cloud services-rolinstanties
* Kan worden gebruikt voor zowel de internetgerichte (externe load balancing) en de Internet-gerichte (interne load balancing)-toepassingen en virtuele machines
* Eindpunt bewaking, namelijk gebruikte toodetermine als een van de services Hallo achter Hallo load balancer zijn niet beschikbaar

Meer informatie:

* [Internetgerichte load balancers tussen meerdere virtuele machines of services](../load-balancer/load-balancer-internet-overview.md)
* [Interne Load Balancer-overzicht](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Globale taakverdeling
Sommige organisaties willen Hallo hoogste niveau van beschikbaarheid mogelijk. Eenzijdige tooreach die dit doel toohost toepassingen in globaal is gedistribueerd datacenters. Wanneer een toepassing wordt gehost in de gehele Hallo wereld datacenters, is het mogelijk voor een hele geopolitieke regio toobecome niet beschikbaar en nog steeds toepassing hello up en wordt uitgevoerd.

Bovendien toohello beschikbaarheid voordelen die u verkrijgen door toepassingen in globaal gedistribueerde datacenters hosten, ook kunt u krijgen prestatievoordelen. Deze prestatievoordelen kunnen worden verkregen met behulp van een mechanisme waarmee aanvragen voor Hallo service toohello datacenter waarin zich het dichtst bij toohello-apparaat dat het Hallo-aanvraag.

Globale taakverdeling kunt bieden u beide van deze voordelen. In Azure krijgt u Hallo voordelen van globale taakverdeling met behulp van Azure Traffic Manager.

Meer informatie:

* [Wat is Traffic Manager?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Naamomzetting
Naamomzetting is een essentiële functie voor alle services die u in Azure host. Vanuit het beveiligingsoogpunt van kan inbreuk op Hallo name resolution functie tooan aanvaller omleiding aanvragen van de website van uw sites tooan aanvaller leiden. Beveiligde naamomzetting is een vereiste voor alle in de cloud gehoste services.

Er zijn twee soorten naamomzetting moet u tooaddress:

* Interne naamomzetting – interne naamomzetting wordt gebruikt door de services op uw virtuele Azure-netwerken, uw on-premises netwerken of beide. Gebruikt voor interne naamomzetting namen zijn niet toegankelijk via Hallo Internet. Voor een optimale beveiliging is het belangrijk uw interne naam resolutie-schema is niet toegankelijk tooexternal gebruikers.
* Externe naamomzetting – externe naamomzetting wordt gebruikt door mensen en apparaten buiten uw on-premises en virtuele netwerken van Azure. Dit zijn Hallo-namen die zijn zichtbaar toohello Internet en gebruikte toodirect verbinding tooyour cloudgebaseerde services.

Voor interne naamomzetting hebt u twee opties:

* Een Azure Virtual Network DNS-server – wanneer u een nieuw virtueel netwerk in Azure maakt een DNS-server is voor u gemaakt. Deze DNS-server kan omzetten Hallo namen van Hallo machines op dit virtuele netwerk van Azure. Deze DNS-server kan niet worden geconfigureerd en wordt beheerd door hello Azure-infrastructuur, zodat een veilige naam resolutie-oplossing.
* Breng uw eigen DNS-server: u hebt de optie Hallo bij het plaatsen van een DNS-server van uw eigen kiezen op uw Azure Virtual Network. Deze DNS-server wordt mogelijk dat een Active Directory geïntegreerde DNS-server of een specifieke DNS-server-oplossing geleverd door een Azure-partner die u van hello Azure Marketplace verkrijgen kunt.

Meer informatie:

* [Overzicht van Virtual Network](../virtual-network/virtual-networks-overview.md)
* [DNS-Servers die worden gebruikt door een virtueel netwerk (VNet) beheren](../virtual-network/virtual-network-manage-network.md#dns-servers)

Voor externe DNS-omzetting hebt u twee opties:

* Host uw eigen externe DNS-server on-premises
* Uw eigen externe DNS-server host met een serviceprovider

Veel grote organisaties hun eigen DNS-servers on-premises fungeert als host. Ze kunnen dit doen omdat ze Hallo expertise en wereldwijde aanwezigheid toodo dus toegang hebben.

In de meeste gevallen is het beter toohost uw DNS-naamomzetting services met een serviceprovider. Deze serviceproviders hebben Hallo netwerk expertise en wereldwijde aanwezigheid tooensure zeer hoge beschikbaarheid voor uw naamomzettingsservices. Beschikbaarheid is essentieel voor voor omdat als uw naamomzetting services mislukken, geen wordt DNS-services kunnen tooreach worden de services van uw internetverbinding.

Azure biedt u een maximaal beschikbare en zodat externe DNS-oplossing in de vorm Hallo van Azure DNS. Deze oplossing externe naam oplossing maakt gebruik van Hallo wereldwijd Azure DNS-infrastructuur. Hiermee kunt u toohost uw domein aan Azure met dezelfde referenties, API's, hulpprogramma's en facturering Hallo als uw andere Azure-services. Als onderdeel van Azure neemt deze ook sterk beveiligingsmechanismen Hallo ingebouwd in Hallo-platform.

Meer informatie:

* [Azure DNS-overzicht](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>DMZ-architectuur
Veel enterprise organisaties gebruiken DMZ's toosegment hun netwerken toocreate een buffer-zone tussen Hallo Internet en hun services. Hallo DMZ gedeelte van Hallo netwerk wordt beschouwd als een laag beveiligingszone en geen activa hoge waarde in die netwerksegment worden geplaatst. Doorgaans ziet u beveiliging netwerkapparaten die een netwerkinterface op Hallo DMZ segment en een ander netwerk interface tooa verbonden netwerk met virtuele machines en services die accepteren van binnenkomende verbindingen van Hallo Internet hebben.

Er zijn een aantal variaties van DMZ ontwerp Hallo besluit toodeploy een DMZ en vervolgens wat voor soort DMZ toouse als u toouse besluit, is gebaseerd op de beveiligingsvereisten van uw netwerk.

Meer informatie:

* [Microsoft-Cloudservices en netwerkbeveiliging](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Controle en detectie van bedreigingen

Azure biedt mogelijkheden toohelp u op dit gebied sleutel met vroege detectie, bewaking en Hallo mogelijkheid toocollect en bekijk netwerkverkeer.

### <a name="azure-network-watcher"></a>Azure-netwerk-Watcher
Azure-netwerk-Watcher bevat een groot aantal mogelijkheden die helpen bij het oplossen van problemen, evenals een geheel nieuwe set hulpprogramma's voor tooassist voorzien van Hallo beveiligingsproblemen te identificeren.

[Weergave van de beveiligingsgroep ](/network-watcher/network-watcher-security-group-view-overview.md) helpt bij de naleving van controle en beveiliging van virtuele Machines en gebruikte tooperform programmatische audits vergelijken Hallo basislijnen beleid gedefinieerd door uw organisatie tooeffective regels voor elk van uw virtuele machines kan worden. Hiermee kunt u afwijking van de configuratie te identificeren.

[Pakketopname](/network-watcher/network-watcher-packet-capture-overview.md) kunt u toocapture netwerkverkeer tooand van Hallo virtuele machine. Problemen met pakketopname kan worden waardevol zijn bij onderzoek van netwerk indringers Hallo naast helpen doordat u toocollect netwerkstatistieken en Hallo van toepassing op te lossen. Bovendien kunt u deze functionaliteit samen met Azure Functions toostart netwerkcontroles in antwoord toospecific Azure waarschuwingen.

Voor meer informatie over Azure-netwerk-Watcher en hoe sommige Hallo-functionaliteit testen in uw labs toostart Bekijk Hallo [bewakingsoverzicht Azure-netwerk-watcher](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Azure-netwerk-watcher wordt nog steeds openbare preview dus mogelijk niet hebben Hallo hetzelfde niveau van beschikbaarheid en betrouwbaarheid als de services die in het algemeen beschikbaarheid release. Bepaalde functies mogelijk niet wordt ondersteund, kunnen hebben beperkte mogelijkheden en mogelijk niet beschikbaar in alle Azure-locaties. Meest recente meldingen Hallo niet op de beschikbaarheid en de status van deze service, Controleer Hallo [pagina Azure-updates](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure Security Center
Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats en vindt dat u meer inzicht in, en controle over, Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen die anders onopgemerkt, en werkt met een groot aantal beveiligingsoplossingen te detecteren.

Azure Security Center helpt u te optimaliseren en netwerkbeveiliging door te controleren:

* Aanbevelingen voor netwerk-beveiliging bieden
* Hallo-status van uw netwerkconfiguratie beveiliging controleren
* Waarschuwt u toonetwork op basis van bedreigingen, zowel op Hallo eindpunt en het netwerk niveaus

Meer informatie:

* [Inleiding tooAzure Security Center](../security-center/security-center-intro.md)


### <a name="logging"></a>Logboekregistratie
Logboekregistratie op het netwerkniveau van een is een belangrijke functie voor een netwerk voor beveiliging. U kunt zich aanmelden voor Netwerkbeveiligingsgroepen tooget niveau van de logboekregistratie informatie verkregen gegevens in Azure. Met NSG logboekregistratie beschikt u over gegevens van:

* [Activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) – deze logboeken vormen een gebruikte tooview alle bewerkingen verzonden tooyour Azure abonnementen. Deze logboeken zijn standaard ingeschakeld en kunnen worden gebruikt binnen hello Azure-portal. Ze werden voorheen bekend als 'Controlelogboeken' of 'Operationele Logs'.
* Gebeurtenislogboeken: deze logboeken bevatten informatie over welke NSG-regels zijn toegepast.
* Teller logboeken – deze logboeken laten u weten hoe vaak elke NSG-regel is toegepast toodeny of verkeer toestaan.

U kunt ook [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), een krachtige gegevensvisualisatie hulpprogramma tooview en analyseren van deze logboeken.

Meer informatie:

* [Log Analytics voor Netwerkbeveiligingsgroepen (nsg's)](../virtual-network/virtual-network-nsg-manage-log.md)
