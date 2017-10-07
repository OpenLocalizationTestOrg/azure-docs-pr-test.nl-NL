---
title: Aanbevolen beveiligingsprocedures voor netwerk aaaAzure | Microsoft Docs
description: Dit artikel bevat een set met aanbevolen procedures voor het gebruik van netwerk-beveiliging ingebouwd in de mogelijkheden van Azure.
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Aanbevolen beveiligingsprocedures voor Azure-netwerk
Microsoft Azure kunt u tooconnect virtuele machines en toestellen tooother via een netwerk verbonden apparaten door ze te plaatsen op Azure Virtual Networks. Een Azure-netwerk is een virtueel netwerk constructie waarmee u tooconnect virtueel netwerk interface kaarten tooa virtueel netwerk tooallow gebaseerd op TCP/IP-communicatie tussen netwerkapparaten. Azure virtuele Machines verbonden tooan Azure Virtual Network kunnen tooconnect toodevices zich op dezelfde Azure Virtual Network verschillende virtuele netwerken van Azure, op Internet Hallo Hallo of zelfs op uw eigen on-premises netwerken.

In dit artikel bespreken we een verzameling aanbevolen beveiligingsprocedures voor Azure-netwerk. Deze aanbevolen procedures zijn afgeleid van onze ervaring met Azure-netwerken en Hallo ervaringen van klanten, zoals zelf.

Voor elke aanbevolen procedure wordt uitgelegd:

* Welke beste Hallo
* Waarom u wilt dat tooenable die best practices
* Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
* Mogelijke alternatieven toohello best practices
* Hoe meer u tooenable Hallo best practices

In dit artikel Best Practices voor beveiliging op Azure-netwerk is gebaseerd op een advies consensus en mogelijkheden van Azure-platform en functiesets, als deze bestaan in Hallo tijd die in dit artikel is geschreven. Adviezen en technologieën op den duur veranderen en dit artikel worden de wijzigingen op een tooreflect regelmatig wordt bijgewerkt.

Azure netwerk aanbevolen beveiligingsprocedures besproken in dit artikel zijn onder andere:

* Logisch segment subnetten
* Het gedrag van routering bepalen
* Geforceerde Tunneling inschakelen
* Gebruik virtuele netwerkapparaten
* DMZ's voor beveiliging zonering implementeren
* Vermijd blootstelling toohello Internet met specifieke WAN-verbindingen
* Beschikbaarheid en prestaties te optimaliseren
* Globale taakverdeling gebruiken
* RDP-toegang tooAzure virtuele Machines uitschakelen
* Schakel Azure Security Center
* Uw datacenter uitbreiden naar Azure

## <a name="logically-segment-subnets"></a>Logisch segment subnetten
[Virtuele netwerken van Azure](https://azure.microsoft.com/documentation/services/virtual-network/) zijn vergelijkbaar tooa LAN op uw on-premises netwerk. Hallo idee achter een Azure-netwerk is dat u maakt een enkel IP-adres op basis van ruimte privénetwerk waarop u alle plaatsen kunt uw [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/). Hallo privé IP-adresruimten beschikbaar zijn in Hallo klasse A (10.0.0.0/8) klasse B (172.16.0.0/12) en klasse C (192.168.0.0/16) bereiken.

Vergelijkbare toowhat u op lokaal, moet u grotere toosegment Hallo-adresruimte in subnetten. U kunt [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) gebaseerd op een subnet zetten toocreate principes van de subnetten.

Routering tussen subnetten gebeurt automatisch en hoeft u geen toomanually routeringstabellen configureren. De standaardinstelling Hallo is echter dat er zijn geen toegangsbeheer netwerk tussen Hallo-subnetten die u op Hallo Azure Virtual Network maakt. In de volgorde toocreate netwerk toegangscontroles tussen subnetten moet u tooput iets tussen Hallo subnetten.

Hallo bewerkingen kunt u deze taak is tooaccomplish een [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) (NSG). Nsg's zijn eenvoudige stateful pakketinspecties benadering toocreate toestaan/weigeren regels voor het netwerkverkeer van apparaten die gebruikmaken van Hallo 5-tuple (Hallo bron-IP, bronpoort, doel-IP, doelpoort en het protocol van laag 4). U kunt toestaan of weigeren van verkeer tooand van één IP-adres, tooand van meerdere IP-adressen of zelfs tooand uit gehele subnetten.

Nsg's gebruiken voor netwerktoegangsbeheer tussen subnetten kunt u tooput resources die deel uitmaken van toohello gebruikt dezelfde beveiligingszone of functie in hun eigen subnetten. Bijvoorbeeld, een eenvoudige 3-laagse toepassing met een weblaag, een toepassing logicalaag en een databaselaag zien. U plaatsen virtuele machines die deel uitmaken van tooeach van deze lagen in hun eigen subnetten. Vervolgens kunt u nsg's toocontrol verkeer tussen Hallo subnetten gebruiken:

* Web-laag virtuele machines kunnen alleen verbindingen toohello toepassing logica machines initiëren en accepteert alleen verbindingen van Hallo Internet
* Toepassing logica virtuele machines kunnen alleen verbindingen met databaselaag initiëren en accepteert alleen verbindingen van de weblaag Hallo
* Database-laag virtuele machines verbinding met iets buiten hun eigen subnet kan niet starten en accepteert alleen verbindingen van logicalaag Hallo-toepassing

over Netwerkbeveiligingsgroepen en hoe u ze kunt gebruiken toologically segment meer toolearn uw Azure Virtual Networks Lees Hallo-artikel [wat is er een Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Het gedrag van routering bepalen
Als u een virtuele machine op een Azure Virtual Network plaatst, zult u merken dat de virtuele machine Hallo verbinding kunnen maken tooany andere virtuele machine op Hallo hetzelfde virtuele netwerk van Azure, zelfs als hello andere virtuele machines op verschillende subnetten. Hallo reden waarom dit mogelijk is, is er een verzameling van systeemroutes die standaard zijn ingeschakeld waardoor dit type communicatie. Deze standaardroutes zodat virtuele machines op Hallo dezelfde Azure Virtual Network tooinitiate verbindingen met elkaar en met Hallo Internet (voor uitgaande communicatie toohello Internet alleen).

Hallo system standaardroutes zijn handig voor vele implementatiescenario's, maar er zijn vaak wanneer toocustomize Hallo routeringsconfiguratie voor uw implementaties. Deze aanpassingen kunt u tooconfigure Hallo volgende hop adres tooreach bepaalde bestemmingen.

We raden aan dat de gebruiker gedefinieerde Routes configureren wanneer u een virtueel netwerk security-toestel, dat we in latere best practice bespreken implementeert.

> [!NOTE]
> gebruiker gedefinieerde Routes zijn niet vereist en Hallo system standaardroutes werkt in de meeste gevallen.
>
>

U kunt meer informatie over de gebruiker gedefinieerde Routes en hoe tooconfigure ze door te lezen Hallo artikel [wat de gebruiker gedefinieerde Routes en doorsturen via IP zijn](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Geforceerde Tunneling inschakelen
toobetter begrijpen geforceerde tunneling, is het nuttig toounderstand welke 'gesplitste tunneling' is.
de meest voorkomende voorbeeld Hallo van gesplitste tunneling is gezien met VPN-verbindingen. Stel dat u een VPN-verbinding vanuit uw bedrijfsnetwerk voor hotel ruimte tooyour. Deze verbinding kunt u tooconnect tooresources in uw bedrijfsnetwerk en alle communicatie tooresources in uw bedrijfsnetwerk doorlopen Hallo VPN-tunnel.

Wat gebeurt er als u wilt dat tooconnect tooresources op Hallo Internet? Wanneer gesplitste tunneling is ingeschakeld, worden deze verbindingen gaat u rechtstreeks toohello Internet en niet via Hallo VPN-tunnel. Sommige beveiligingsexperts overwegen deze toobe een potentieel risico en daarom raden aan dat gesplitste tunneling uitgeschakeld en alle verbindingen, die bestemd zijn voor Hallo Internet en die bestemd zijn voor uw bedrijfsbronnen doorlopen Hallo VPN-tunnel. Hallo-voordeel van dit te doen is dat verbindingen toohello Internet worden vervolgens afgedwongen via Hallo bedrijfsnetwerk beveiligingsapparaten, die niet zou Hallo geval als Hallo VPN-client is verbonden toohello Internet buiten Hallo VPN-tunnel.

Nu gaan we doen dit back-toovirtual machines op een Azure Virtual Network. Hallo-standaardroutes voor een virtueel netwerk van Azure toestaan virtuele machines tooinitiate verkeer toohello Internet. Dit kan te bestaan uit een beveiligingsrisico als deze uitgaande verbindingen de kwetsbaarheid Hallo van een virtuele machine verhoogt kunnen en door aanvallers worden gebruikt.
Daarom is het raadzaam dat u geforceerde tunneling op uw virtuele machines inschakelt wanneer u cross-premises connectiviteit tussen uw virtuele netwerk van Azure en uw on-premises netwerk hebt. We zullen hebben over cross-premises-connectiviteit verderop in dit Azure netwerken best practices-document.

Als u een cross-premises-verbinding niet hebt, controleert u of u profiteren van Netwerkbeveiligingsgroepen (eerder besproken) of Azure virtual network beveiliging toestellen (besproken naast) tooprevent uitgaande verbindingen toohello Internet van uw Azure-virtuele Machines.

informatie over toolearn geforceerde tunneling en hoe tooenable, lees Hallo-artikel [configureren met behulp van PowerShell en Azure Resource Manager geforceerde Tunneling](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Gebruik virtuele netwerkapparaten
Terwijl Netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routering een zekere mate van netwerkbeveiliging op Hallo netwerk- en lagen Hallo bieden kunnen [OSI-model](https://en.wikipedia.org/wiki/OSI_model), gaat er toobe situaties waar je moet of wilt u tooenable beveiliging op hoog niveau van Hallo-stack. In dergelijke situaties wordt aangeraden dat u een virtueel netwerk beveiligingsapparaten geleverd door Azure partners implementeert.

Azure-netwerk beveiligingsapparaten kunnen aanzienlijk uitgebreide niveaus van beveiliging bieden wat is opgegeven door netwerk niveau besturingselementen. Hallo beveiliging netwerkmogelijkheden geleverd door het virtuele netwerk beveiligingsapparaten onder andere:

* Gebruik
* Inbraakdetectie detectie inbraakdetectie voorkomen
* Beveiligingslek management
* Toepassingsbeheer
* Netwerk gebaseerde afwijkingsdetectie
* Web filteren
* Antivirus
* Botnet beveiliging

Als u een hoger niveau van netwerkbeveiliging dan kunt u met netwerkfuncties toegangsniveau vereist, vervolgens wordt aangeraden dat u onderzoeken en beveiligingsapparaten virtuele Azure-netwerk te implementeren.

toolearn over welke beveiligingsapparaten virtuele Azure-netwerk beschikbaar zijn en over hun mogelijkheden, gaat u naar Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/) en zoek naar 'beveiliging' en 'Netwerkbeveiliging'.

## <a name="deploy-dmzs-for-security-zoning"></a>DMZ's voor beveiliging zonering implementeren
Een DMZ of 'perimeternetwerk' is een fysieke of logische netwerksegment dat is ontworpen tooprovide een extra beveiligingslaag tussen uw bedrijfsmiddelen en Hallo Internet. Hallo bedoeling Hallo DMZ is tooplace gespecialiseerde access control netwerkapparaten op Hallo rand van Hallo DMZ netwerk, zodat alleen de gewenste verkeer is toegestaan voorbij Hallo beveiliging netwerkapparaat en in uw Azure Virtual Network.

DMZ's zijn nuttig omdat u uw netwerk toegangsbeheer, bewaking, logboekregistratie en rapportage op Hallo apparaten aan de rand van uw Azure Virtual Network Hallo zich kunt richten. U zou hier doorgaans inschakelen DDoS preventie, inbraakdetectie detectie/inbraakdetectie preventie systemen (id's / IP-Adressen), firewall-regels en beleid, web filteren, netwerk antimalware en meer. Hallo-netwerkapparaten beveiliging tussen Hallo Internet en het virtuele netwerk van Azure en een interface op beide netwerken hebben.

Dit is Hallo basic ontwerp van een DMZ genoemd, maar er zijn veel verschillende DMZ ontwerpen, zoals back to back, drie homed, multihomed, en andere.

We raden voor alle implementaties van hoge beveiliging een DMZ tooenhance Hallo beveiligingsniveau netwerk voor uw Azure-resources te implementeren.

meer informatie over DMZ's en hoe toodeploy ze in Azure, lees Hallo-artikel toolearn [Microsoft-Cloudservices en netwerkbeveiliging](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Vermijd blootstelling toohello Internet met specifieke WAN-verbindingen
Veel organisaties hebben ervoor gekozen Hallo hybride IT-route. In hybride IT zijn sommige Hallo bedrijfsgegevens in Azure, terwijl andere lokale blijven. In veel gevallen wordt een aantal onderdelen van een service wordt uitgevoerd in Azure terwijl andere onderdelen op lokale blijven.

In Hallo hybride IT-scenario is er meestal een soort cross-premises connectiviteit. Dit cross-premises connectiviteit kunt Hallo bedrijf tooconnect hun lokale netwerken tooAzure virtuele netwerken. Er zijn twee oplossingen voor cross-premises-connectiviteit beschikbaar:

* Site-naar-site VPN
* ExpressRoute

[Site-naar-site VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) vertegenwoordigt een virtuele particuliere verbinding tussen uw on-premises netwerk en een Azure-netwerk. Deze verbinding plaatsvindt Hallo van Internet en kunt u te 'tunnel' gegevens in een versleutelde verbinding tussen uw netwerk en Azure. Site-naar-site VPN is een beveiligde, volwassen technologie die is geïmplementeerd door bedrijven van elke grootte jarenlang. Tunnel-versleuteling wordt uitgevoerd met [IPsec-tunnelmodus](https://technet.microsoft.com/library/cc786385.aspx).

Site-naar-site VPN is een technologie voor het vertrouwde, betrouwbare en tot stand gebracht, verkeer binnen Hallo tunnel Hallo Internet passeren. Bovendien is de bandbreedte relatief beperkte tooa maximaal over 200 Mbps.

Als u een uitzonderlijke niveau van beveiliging of prestaties voor uw cross-premises verbindingen vereist, wordt u aangeraden dat u Azure ExpressRoute voor uw cross-premises-connectiviteit gebruiken. ExpressRoute is een speciale WAN koppeling tussen uw on-premises locatie of een Exchange-hostingprovider. Omdat dit een telco verbinding, worden uw gegevens niet via Hallo Internet worden verzonden en is daarom niet blootgestelde toohello potentiële risico's in de communicatie via Internet.

meer informatie over de werking van Azure ExpressRoute toolearn en hoe toodeploy, lees Hallo-artikel [technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Beschikbaarheid en prestaties te optimaliseren
Vertrouwelijkheid, integriteit en beschikbaarheid (CIA) bestaat uit drie vakken Hallo van meest invloedrijke beveiligingsmodel van vandaag. Vertrouwelijkheid is versleuteling en privacy, integriteit over om ervoor te zorgen dat gegevens worden niet gewijzigd door onbevoegde personen en beschikbaarheid is bedoeld om ervoor te zorgen dat gemachtigde personen kunnen tooaccess Hallo informatie die ze gemachtigd zijn zijn tooaccess. Fout in een van deze gebieden vertegenwoordigt een mogelijke inbreuk in beveiliging.

Beschikbaarheid kan worden beschouwd als over de beschikbaarheid en prestaties. Als een service niet actief is, kan informatie kan niet worden geopend. Als de prestaties zo slecht als toomake Hallo gegevens onbruikbaar, kunt vervolgens we overwegen Hallo gegevens toobe niet toegankelijk. Vanuit beveiligingsoogpunt, moeten we daarom toodo ongeacht kunnen wij toomake of onze services optimale beschikbaarheid en prestaties.
Een populair en effectieve methode gebruikt tooenhance beschikbaarheid en prestaties is toouse voor taakverdeling. Taakverdeling is een methode voor het distribueren van netwerkverkeer op servers die deel van een service uitmaken. Bijvoorbeeld, als u front-endwebservers als onderdeel van uw service hebt, kunt u toodistribute Hallo verkeer voor taakverdeling over uw meerdere front-endwebservers.

Beschikbaarheid van verhoogd deze distributie van verkeer omdat het als een van de webservers Hallo uitvalt, Hallo load balancer wordt stoppen met het verzenden van verkeer toothat server en omleiding verkeer toohello servers die nog steeds online zijn. Taakverdeling helpt ook bij prestaties, omdat het Hallo-processor, netwerk en geheugen overhead voor het voldoen aan aanvragen is verdeeld over alle Hallo taakverdeling servers.

Het is raadzaam dat u gebruikmaken van taakverdeling zoveel mogelijk en geschikt is voor uw services. We je adres geschiktheid in Hallo uit te voeren.
Op Hallo Azure Virtual Network-niveau biedt Azure dat u met drie primaire opties voor load balancing:

* HTTP-gebaseerde taakverdeling
* Externe load balancing
* Interne taakverdeling

## <a name="http-based-load-balancing"></a>HTTP-gebaseerde taakverdeling
HTTP-gebaseerde taakverdeling nemen van beslissingen over welke serververbindingen toosend met behulp van de kenmerken van Hallo HTTP-protocol is gebaseerd. Azure heeft een HTTP-load balancer die u met de naam van toepassingsgateway Hallo.

We raden aan dat u ons Azure Application Gateway wanneer:

* Toepassingen waarvoor aanvragen van Hallo Hallo dezelfde client/gebruiker sessie tooreach dezelfde back-end virtuele machine. Voorbeelden van deze zou worden winkelen winkelwagen apps en web-e-mailservers.
* Toepassingen die u toofree web server-farms van SSL-beëindiging wilt overhead door gebruik te maken van de toepassingsgateway [SSL-offload](https://f5.com/glossary/ssl-offloading) functie.
* Toepassingen, zoals een netwerk voor inhoudslevering, waarvoor meerdere HTTP-aanvragen op Hallo dezelfde langlopende TCP-verbinding toobe doorgestuurd of load balanced toodifferent back-endservers.

Lees artikel Hallo toolearn meer informatie over hoe Azure Application Gateway werkt en hoe u het kunt gebruiken in uw implementaties [Application Gateway Overview](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Externe Load Balancing
Externe load balancing vindt plaats wanneer het binnenkomende verbindingen van Hallo Internet worden verdeeld tussen de servers die zich in een virtuele Azure-netwerk. Hello Azure externe Load balancer kunt u deze mogelijkheid en het is raadzaam dat u deze gebruiken wanneer u geen nodig voor een tijdelijke sessies Hallo hebt of SSL-offload.

TooHTTP-gebaseerde taakverdeling, Hallo externe Load Balancer maakt daarentegen gebruik van informatie op de netwerk- en lagen Hallo van Hallo OSI netwerken model toomake beslissingen op welke server tooload saldo verbinding met.

Het is raadzaam dat u externe Load Balancing wanneer u [staatloze toepassingen](http://whatis.techtarget.com/definition/stateless-app) accepteren van binnenkomende aanvragen via Hallo Internet.

Lees artikel Hallo toolearn meer informatie over de werking van hello Azure externe Load Balancer en hoe u kunt implementeren, [aan de slag maken van een internetgerichte Load Balancer in Resource Manager, met behulp van PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Interne Load Balancing
Interne load balancing is vergelijkbaar tooexternal taakverdeling en maakt gebruik van hetzelfde mechanisme tooload saldo verbindingen toohello servers achter deze Hallo. Hallo enige verschil is dat Hallo load balancer in dit geval verbindingen van virtuele machines die zich niet op Hallo Internet worden geaccepteerd. In de meeste gevallen Hallo-verbindingen die worden geaccepteerd voor taakverdeling geïnitieerd door apparaten op een Azure Virtual Network.

Het is raadzaam dat u voor de interne load balancer voor scenario's die van deze mogelijkheid gebruikmaken, zoals wanneer u tooload saldo verbindingen tooSQL Servers of interne webservers moet gebruiken.

Lees artikel Hallo toolearn meer informatie over hoe Azure interne taakverdeling werkt en hoe u kunt implementeren, [maken van een interne Load Balancer met behulp van PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Globale taakverdeling gebruiken
Openbare cloud computing maakt het mogelijk toodeploy globaal gedistribueerde toepassingen die zich in datacenters over Hallo wereld onderdelen hebben. Dit is mogelijk in Microsoft Azure vanwege de aanwezigheid van tooAzure van globale datacenter. Daarentegen vermeld technologieën voor taakverdeling toohello eerder, globale taakverdeling maakt het mogelijk toomake services beschikbaar zelfs wanneer de volledige datacenters mogelijk niet meer beschikbaar.

U kunt dit type globale taakverdeling in Azure door gebruik te maken van ophalen [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/). Traffic Manager maakt mogelijk tooload saldo verbindingen tooyour services op basis van locatie van de gebruiker Hallo Hallo.

Als gebruiker Hallo een aanvraag tooyour-service van Hallo EU doorvoert is, is Hallo verbinding gerichte tooyour services zich in een datacenter EU. Dit deel van Traffic Manager globale taakverdeling helpt tooimprove prestaties is omdat de verbinding te maken toohello dichtstbijzijnde datacenter sneller dan toodatacenters die ver verbinding te maken.

Zijde van de beschikbaarheid hello zorgt globale taakverdeling ervoor dat uw service beschikbaar is, zelfs als een hele datacenter mag niet meer beschikbaar.

Bijvoorbeeld, als een Azure-datacenter mag niet meer beschikbaar is vanwege tooenvironmental redenen of vervaldatum toooutages (zoals regionale netwerkfouten) verbindingen tooyour service zou worden gerouteerd toohello dichtstbijzijnde online datacenter. Deze globale taakverdeling wordt gerealiseerd door gebruik te maken van DNS-beleidsregels die u in het Traffic Manager kunt maken.

U wordt aangeraden Traffic Manager voor een cloudoplossing die u ontwikkelt die heeft een algemeen gedistribueerde bereik over meerdere regio's en Hallo hoogste niveau van beschikbaarheid mogelijk vereist.

meer over Azure Traffic Manager toolearn en hoe toodeploy, lees Hallo-artikel [wat Traffic Manager is](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>RDP/SSH toegang tooAzure virtuele Machines uitschakelen
Het is mogelijk tooreach Azure Virtual Machines met behulp van Hallo [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) en Hallo [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) (SSH)-protocollen. Deze protocollen maken het mogelijk toomanage virtuele machines vanaf externe locaties en zijn standaard in het datacenter computing.

Hallo potentiële beveiligingsprobleem met gebruik van deze protocollen via Internet Hallo is dat aanvallers verschillende gebruiken kunnen [beveiligingsaanvallen](https://en.wikipedia.org/wiki/Brute-force_attack) technieken toogain toegang tooAzure virtuele Machines. Als Hallo aanvallers toegang krijgen, kunnen ze de virtuele machine gebruiken als een startpunt voor inbreuk op andere computers in uw Azure Virtual Network of zelfs aanvallen netwerkapparaten buiten Azure.

Als gevolg hiervan is het raadzaam dat u direct RDP en SSH toegang tooyour Azure Virtual Machines vanaf Internet Hallo uitschakelen. Nadat u direct RDP en SSH toegang Hallo die Internet is uitgeschakeld, hebt u andere opties kunt u tooaccess deze virtuele machines voor extern beheer:

* Punt-naar-site VPN
* Site-naar-site VPN
* ExpressRoute

[Punt-naar-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) is een andere term voor VPN-client/server-verbinding voor externe toegang. Een punt-naar-site-VPN kunt een enkele gebruiker tooconnect tooan Azure Virtual Network via Hallo Internet. Hallo punt-naar-site-verbinding tot stand is gebracht, Hallo gebruiker worden kunnen toouse RDP of SSH tooconnect tooany virtuele machines op Azure Virtual Network Hallo die gebruiker Hallo verbonden toovia punt-naar-site VPN. Hierbij wordt ervan uitgegaan dat gebruiker Hallo geautoriseerde tooreach die virtuele machines is.

Punt-naar-site VPN is veiliger dan direct RDP of SSH-verbindingen omdat Hallo gebruiker tooauthenticate tweemaal voor verbindende tooa virtuele machine heeft. Ten eerste gebruiker behoeften tooauthenticate Hallo (en worden geautoriseerd) tooestablish Hallo punt-naar-site VPN-verbinding. ten tweede gebruiker behoeften tooauthenticate Hallo (en worden geautoriseerd) tooestablish Hallo RDP of SSH-sessie.

Een [site-naar-site VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) een gehele netwerk tooanother netwerk verbindt via Hallo Internet. U kunt een site-naar-site VPN-tooconnect uw lokale netwerk tooan Azure Virtual Network. Als u een site-naar-site VPN implementeert, wordt gebruikers op uw on-premises netwerk kunnen tooconnect toovirtual machines op het virtuele netwerk van Azure met behulp van Hallo RDP of SSH-protocol meer dan Hallo site-naar-site VPN-verbinding en vereist niet dat u tooallow direct RDP of SSH toegang via Internet Hallo.

U kunt ook een specifieke WAN-verbinding tooprovide functionaliteit vergelijkbaar toohello site-naar-site VPN. de belangrijkste verschillen Hallo zijn 1. Hallo specifieke WAN-verbinding passeren niet Hallo Internet en 2. specifieke WAN-verbindingen zijn meestal meer stabiel en zodat. Azure biedt u een oplossing voor specifieke WAN-verbinding in de vorm van Hallo [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Schakel Azure Security Center
Azure Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats en biedt dat u grotere zichtbaarheid van, en controle over, Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Azure Security Center helpt u te optimaliseren en netwerkbeveiliging door te controleren:

* Aanbevelingen voor netwerk-beveiliging bieden
* Hallo-status van uw netwerkconfiguratie beveiliging controleren
* Waarschuwt u toonetwork op basis van bedreigingen, zowel op Hallo eindpunt en het netwerk niveaus

Het is raadzaam dat u Azure Security Center voor al uw Azure-implementaties inschakelen.

meer informatie over Azure Security Center en hoe tooenable voor uw implementaties Lees Hallo-artikel toolearn [inleiding tooAzure Security Center](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Veilig uitbreiden van uw datacenter in Azure
Veel bedrijven organisaties tooexpand in de cloud Hallo in plaats van hun datacentra lokale groeiende behoefte. Deze uitbreiding vertegenwoordigt een uitbreiding van bestaande IT-infrastructuur in Hallo openbare cloud. Door gebruik te maken van cross-premises connectiviteitsopties is mogelijk tootreat netwerk uw Azure Virtual Networks als een ander subnet op uw on-premises infrastructuur.

Echter is er veel van de planning en ontwerp problemen die toobe moeten aangepakt eerste. Dit is vooral belangrijk in Hallo gebied van netwerkbeveiliging. Een van de aanbevolen manieren toounderstand hello toosee een voorbeeld hoe u een ontwerp voor deze benadering is.

Microsoft heeft gemaakt Hallo [Architectuurdiagram van Datacenter extensie verwijzing](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) en ondersteunende collateral toohelp u begrijpt hoe deze een verlenging van het datacenter eruit zou. Dit zorgt voor een voorbeeldimplementatie verwijzing tooplan gebruiken en ontwerpen van een beveiligde enterprise datacenter extensie toohello cloud. Het is raadzaam dat u dit document tooget een idee van de belangrijke onderdelen van een veilige oplossing Hallo bekijken.

Bekijk Hallo video toolearn meer informatie over hoe toosecurely uw datacenter uitbreiden naar Azure, [uw Datacenter uitbreiden tooMicrosoft Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
