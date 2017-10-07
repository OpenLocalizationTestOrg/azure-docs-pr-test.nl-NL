---
title: aanbevolen beveiligingsprocedures aaaAzure netwerk | Microsoft Docs
description: Meer informatie over dat sommige van de belangrijkste functies die beschikbaar zijn in Azure toohelp Hallo beveiligde netwerkomgevingen maken
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Microsoft cloud services en netwerk-beveiliging
Microsoft cloud-services leveren hyperschaal services en -infrastructuur, bedrijfsniveau mogelijkheden en veel keuzes voor hybride verbindingen. Klanten kunnen tooaccess deze services via Internet Hallo of met Azure ExpressRoute, waarmee u verbinding met het particuliere netwerk kiezen. Hallo Microsoft Azure-platform kan klanten tooseamlessly Hallo cloud kunnen hun infrastructuur uitbreiden en meerdere lagen architecturen bouwen. Bovendien kunt derden uitgebreide mogelijkheden inschakelen door het aanbieden van beveiligingsservices en virtuele apparaten. In dit artikel biedt een overzicht van beveiliging en architectuur problemen die klanten rekening houden moeten bij het gebruik van Microsoft-cloudservices is toegankelijk via ExpressRoute. Het omvat tevens veiliger services in Azure virtuele netwerken maken.

## <a name="fast-start"></a>Snel starten
Hallo volgende logica grafiek kunt u tooa specifiek voorbeeld Hallo directe veel beveiligingstechnieken beschikbaar met hello Azure-platform. Vinden voor snelle naslag Hallo voorbeeld die het beste past bij uw aanvraag. Uitgebreide uitleg blijven lezen via Hallo papier.
[![0]][0]

[Voorbeeld 1: Een perimeternetwerk (ook wel DMZ, gedemilitariseerde zone of gescreend subnet) bouwen toohelp beveiligen toepassingen met netwerkbeveiligingsgroepen (nsg's).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Voorbeeld 2: Een perimeternetwerk bouwen netwerk toohelp toepassingen met een firewall en nsg's beveiligen.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Voorbeeld 3: Een perimeternetwerk bouwen netwerk toohelp netwerken met een firewall, de gebruiker gedefinieerde route (UDR) en het NSG beschermen.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Voorbeeld 4: Voeg een hybride verbinding met een site-naar-site, een virtueel apparaat virtueel particulier netwerk (VPN).](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Voorbeeld 5: Een hybride verbinding met een site-naar-site Azure VPN-gateway wordt toegevoegd.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Voorbeeld 6: Een hybride verbinding met ExpressRoute toevoegen.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Voorbeelden voor het toevoegen van de verbindingen tussen virtuele netwerken, hoge beschikbaarheid en service-koppeling wordt toegevoegd toothis document via Hallo komende maanden.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Microsoft-naleving en infrastructuur beveiliging
toohelp organisaties nationaal, regionaal, voldoen en branchespecifieke vereisten van bestuur Hallo verzamelen en gebruiken van personen gegevens, biedt Microsoft meer dan 40 certificeringen en verklaringen. Hallo meest uitgebreide instellen van een cloud serviceprovider.

Zie voor meer informatie, informatie over de compatibiliteit van Hallo op Hallo [Microsoft Trust Center][TrustCenter].

Microsoft heeft een uitgebreide benadering tooprotect infrastructuur die nodig is toorun hyperschaal globale cloudservices. Microsoft-cloudinfrastructuur omvat hardware, software, netwerken, en administratieve en medewerkers, Daarnaast toohello fysieke datacenters.

![2]

Deze aanpak geeft u een veiliger basis voor klanten toodeploy hun Hallo Microsoft cloud-services. de volgende stap Hallo is bedoeld voor klanten toodesign en maak een architectuur beveiliging tooprotect deze services.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Traditionele beveiliging architecturen en perimeternetwerken
Hoewel Microsoft sterk investeert in het beveiligen van de cloudinfrastructuur hello, moeten klanten ook beveiligen hun cloud-services en -resourcegroepen. Een meerlaagse benadering toosecurity biedt de beste verdediging Hallo. De beveiligingszone van een perimeter-netwerk beveiligt interne netwerkbronnen vanaf een niet-vertrouwd netwerk. Een perimeternetwerk verwijst toohello randen of het delen van Hallo netwerk tussen Hallo Internet en Hallo beveiligd enterprise IT-infrastructuur.

In typische bedrijfsnetwerken wordt Hallo-basisinfrastructuur sterk verbeterd op Hallo-verbindingen met meerdere lagen beveiligingsapparaten. Hallo grens van elke laag bestaat uit de apparaten en beleid afdwingingspunten. Elke laag kan een combinatie van Hallo beveiliging netwerkapparaten volgende bevatten: firewalls, voorkomen van Denial of Service (DoS), inbraakdetectie of beveiliging systemen (id's / IP-Adressen) en VPN-apparaten. Afdwingen van beleid kan Hallo vorm van firewall-beleid, toegangsbeheerlijsten (ACL's) of specifieke routering krijgen. de eerste regel Hallo verdediging in Hallo netwerk rechtstreeks accepteren van binnenkomende verkeer van Hallo Internet, is een combinatie van deze mechanismen tooblock aanvallen en schadelijk verkeer terwijl verdere legitieme aanvragen in Hallo netwerk. Dit verkeer routeert rechtstreeks tooresources in het perimeternetwerk Hallo. Deze resource kan vervolgens "praten" tooresources dieper in Hallo netwerk, doorvoer Hallo volgende grens voor validatie van de eerste. Hallo buitenste laag wordt Hallo perimeternetwerk genoemd, omdat dit deel van het netwerk Hallo blootgestelde toohello Internet, meestal met een vorm van beveiliging aan beide zijden. Hallo toont volgende afbeelding een voorbeeld van een perimeternetwerk één subnet in een bedrijfsnetwerk met twee beveiligingsgrenzen.

![3]

Er zijn veel architecturen gebruikt tooimplement een perimeternetwerk. Deze architecturen kunnen variëren van een eenvoudige load balancer tooa meerdere subnetten perimeternetwerk met uiteenlopende mechanismen op elke grens tooblock verkeer en Hallo diepere lagen van het bedrijfsnetwerk Hallo beveiligen. Hoe Hallo perimeternetwerk wordt gemaakt, is afhankelijk van de specifieke behoeften Hallo van Hallo-organisatie en de algehele risicotolerantie.

Zoals klanten hun werkbelastingen toopublic clouds verplaatsen, is het essentieel toosupport vergelijkbare mogelijkheden voor perimeter netwerkarchitectuur in Azure toomeet naleving en de beveiligingsvereisten. Dit document bevat richtlijnen over hoe klanten een beveiligde netwerkomgeving in Azure kunnen samenstellen. Het is gericht op een perimeternetwerk hello, maar bevat ook een uitgebreide bespreking van veel aspecten van netwerkbeveiliging. Hallo vragen te volgen in deze discussie kennis:

* Hoe kunt u een perimeternetwerk in Azure gemaakt?
* Wat zijn enkele hello Azure-functies beschikbaar toobuild Hallo perimeternetwerk bevinden?
* Hoe kunnen back-end-werkbelastingen beveiligd?
* Hoe weet Internet communicatie beheerd toohello werkbelastingen in Azure?
* Hoe Hallo on-premises netwerken worden beschermd tegen implementaties in Azure?
* Wanneer moeten systeemeigen Azure beveiligingsfuncties worden gebruikt in plaats van de apparaten van derden of services?

Hallo volgende diagram toont de verschillende beveiligingslagen aan te brengen die Azure toocustomers biedt. Deze lagen zijn zowel systeemeigen in hello Azure-platform zelf en de klant gedefinieerde functies:

![4]

Binnenkomend van Hallo Internet, Azure DDoS tegen grootschalige aanvallen op Azure beschermt. de volgende laag Hallo is door de klant gedefinieerde openbare IP-adressen (eindpunten) die zijn gebruikt toodetermine welk verkeer Hallo cloud service toohello virtueel netwerk kunt doorgeven. Systeemeigen Azure virtuele netwerkisolatie garandeert volledige isolatie van alle andere netwerken en dat alleen via paden van de gebruiker die is geconfigureerd en methoden verkeersstromen. Deze paden en methoden zijn de volgende laag hello, waar nsg's, UDR en virtuele netwerkapparaten gebruikte toocreate beveiliging grenzen tooprotect Hallo implementaties van toepassingen in Hallo beveiligd netwerk kunnen worden.

de volgende sectie Hallo biedt een overzicht van virtuele netwerken in Azure. Deze virtuele netwerken worden gemaakt door klanten en wat hun geïmplementeerde werkbelastingen zijn verbonden met zijn. Virtuele netwerken zijn Hallo op basis van alle functies van het netwerk beveiliging Hallo tooestablish vereist een perimeternetwerk netwerk tooprotect implementaties van de klant in Azure.

## <a name="overview-of-azure-virtual-networks"></a>Overzicht van virtuele netwerken in Azure
Voordat het internetverkeer krijgt toohello virtuele Azure-netwerken, zijn er twee lagen beveiliging inherent toohello Azure-platform:

1.    **DDoS-bescherming**: DDoS-bescherming is een laag met hello Azure fysiek netwerk waarnaar hello Azure-platform zelf tegen grootschalige aanvallen via Internet beschermt. Deze aanvallen meerdere 'bot' knooppunten in een poging toooverwhelm een internetservice gebruiken. Azure heeft een robuuste DDoS-bescherming net voor alle binnenkomende, uitgaande en meerdere Azure-regio connectiviteit. Deze laag DDoS-beveiliging heeft geen gebruiker configureerbare kenmerken en is niet toegankelijk toohello klant. Hallo DDoS beschermingslaag Azure beschermt als een platform van grootschalige aanvallen, ook wordt bewaakt uitgaande gebonden verkeer en meerdere Azure-regio. Met virtuele netwerkapparaten op Hallo VNet, worden extra verificatielagen herstelmogelijkheden geconfigureerd door de klant voor een kleinere schaal aanval die geen beveiliging op netwerkniveau Hallo platform krachtvoertuigen Hallo. Een voorbeeld van een DDoS in actie; Als een internetgericht IP-adres van een grootschalige DDoS-aanval is aangevallen, zou Azure Hallo bronnen Hallo aanvallen te detecteren en wissen Hallo verkeer foutieve voordat deze de bestemming bereikt. In bijna alle gevallen hello aangevallen eindpunt is niet van invloed op een aanval Hallo. Er is geen verkeer is in Hallo zeldzame gevallen heeft invloed op een eindpunt betrokken tooother eindpunten, aangevallen Hallo-eindpunt. Andere klanten en -services ziet geen gevolgen van deze aanval. Het is essentieel toonote die Azure DDoS alleen grootschalige aanvallen zoekt. Het is mogelijk dat uw specifieke service overbelast kan voordat Hallo platform beveiliging op netwerkniveau drempels zijn overschreden. Bijvoorbeeld: een website op een enkele A0 IIS-server kan offline worden gehaald van een DDoS-aanval voordat Azure-platform niveau DDoS-bescherming een bedreiging geregistreerd.

2.  **Openbare IP-adressen**: openbare IP-adres (ingeschakeld via de service-eindpunten, openbare IP-adressen, Application Gateway en andere Azure-functies die een openbare IP-adres toohello internet doorgestuurd tooyour resource) adressen cloudservices toestaan of resourcegroepen toohave openbare Internet IP-adressen en poorten die worden weergegeven. Hallo-eindpunt maakt gebruik van NAT (Network Address Translation) tooroute verkeer toohello interne adres en poort op Hallo virtuele Azure-netwerk. Dit pad is Hallo primaire manier voor het externe verkeer toopass in Hallo virtueel netwerk. Hallo openbare IP-adressen zijn configureerbare toodetermine welk verkeer wordt doorgegeven in, en hoe en waar deze wordt omgezet in het virtuele netwerk toohello.

Zodra verkeer Hallo virtueel netwerk bereikt, zijn er veel functies die een rol spelen. Virtuele netwerken in Azure zijn fundering voor klanten tooattach Hallo hun werkbelasting en wanneer de basisprincipes van beveiliging op netwerkniveau wordt toegepast. Er is een particulier netwerk (een virtueel netwerk overlay) in Azure voor klanten met Hallo functies en kenmerken te volgen:

* **Isolatie van verkeer**: een virtueel netwerk is Hallo verkeer isolatiegrens op Hallo Azure-platform. Virtuele machines (VM's) in één virtueel netwerk kan niet communiceren rechtstreeks tooVMs in een ander virtueel netwerk, zelfs als beide virtuele netwerken worden gemaakt door Hallo dezelfde klant. Isolatie is een kritieke eigenschap die ervoor zorgt dat de klant VM's en communicatie blijft persoonlijke binnen een virtueel netwerk.

>[!NOTE]
>Isolatie van verkeer verwijst alleen tootraffic *inkomende* toohello virtueel netwerk. Standaard uitgaand verkeer van Hallo VNet toohello internet is toegestaan, maar kan worden voorkomen door het nsg's desgewenst.
>
>

* **Topologie met meerdere niveaus**: virtuele netwerken kunnen klanten topologie met meerdere niveaus toodefine door het toewijzen van subnetten en het toewijzen van afzonderlijke adresruimten voor verschillende elementen of 'laag' van hun werkbelasting. Deze logische groeperingen en topologieën klanten toodefine ander-beleid op basis van het type van de workload Hallo inschakelen en ook bepalen verkeersstromen tussen Hallo lagen.
* **Cross-premises connectiviteit**: klanten kunnen cross-premises-connectiviteit tussen een virtueel netwerk en meerdere on-premises sites of andere virtuele netwerken maken in Azure. een verbinding tooconstruct, klanten kunnen gebruiken VNet-Peering, Azure VPN-Gateways, virtuele apparaten van derden of ExpressRoute. Azure biedt ondersteuning voor site-naar-site (S2S) VPN-verbindingen met IPsec/IKE standaardprotocollen en ExpressRoute particuliere connectiviteit.
* **NSG** klanten toocreate regels (ACL's) kunnen op Hallo gewenst niveau van granulatie: network interfaces, afzonderlijke virtuele machines of virtuele subnetten. Klanten kunnen toegang door toestaan of weigeren van communicatie tussen Hallo werkbelastingen binnen een virtueel netwerk, van systemen op klantnetwerken via cross-premises-connectiviteit te controleren of directe communicatie met Internet.
* **UDR** en **doorsturen via IP** kunnen klanten toodefine Hallo communicatiepaden tussen verschillende lagen binnen een virtueel netwerk. Klanten kunnen een firewall, -id's / IP-Adressen en andere virtuele apparaten implementeren en netwerkverkeer te routeren via deze beveiligingsapparaten voor beveiliging grens wordt afgedwongen, controle en controle.
* **Virtuele apparaten** in hello Azure Marketplace: beveiligingsapparaten, zoals firewalls, netwerktaakverdelers en id's / IP-Adressen beschikbaar zijn in hello Azure Marketplace en Hallo galerie voor VM-installatiekopie. Klanten kunnen deze apparaten naar hun virtuele netwerken en in het bijzonder op hun beveiligde netwerkomgeving van beveiliging grenzen (inclusief Hallo perimeter subnetten) toocomplete een meerdere lagen implementeren.

Met deze functies en mogelijkheden is een voorbeeld van hoe een perimeter-netwerkarchitectuur kan worden samengesteld in Azure Hallo-diagram te volgen:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Perimeter netwerkkenmerken en vereisten
perimeternetwerk Hallo is Hallo-front-end van Hallo netwerk, rechtstreeks in aanraking komt communicatie van Hallo Internet. inkomende hello-pakketten moeten stromen Hallo beveiligingsapparaten, zoals firewall Hallo-id's en IP-Adressen, alvorens Hallo back-endservers. Door Hallo beveiligingsapparaten in het perimeternetwerk Hallo voor het afdwingen van beleid, controle en controledoeleinden voordat deze uit het Hallo-netwerk kunnen ook Internet bestemd pakketten van Hallo werkbelastingen stromen. Hallo perimeternetwerk kan bovendien cross-premises VPN-gateways tussen virtuele netwerken van klanten en on-premises netwerken te hosten.

### <a name="perimeter-network-characteristics"></a>Perimeter-netwerkeigenschappen
Verwijst naar de vorige afbeelding hello, zijn Hallo kenmerken van een goede perimeternetwerk als volgt:

* Internetgerichte:
  * Hallo perimeter netwerksubnet zelf is internetgerichte, rechtstreeks communiceren met de Hallo Internet.
  * Openbare IP-adressen, VIP's en/of service-eindpunten doorgeven Internet verkeer toohello front-netwerk en apparaten.
  * Binnenkomend verkeer van Internet beveiligingsapparaten voordat andere bronnen op de front-endnetwerk Hallo passeert Hallo.
  * Als u uitgaande beveiliging is ingeschakeld, passeert verkeer beveiligingsapparaten, als laatste stap hello, voordat deze toohello Internet.
* Beveiligd netwerk:
  * Er is geen directe pad van de basisinfrastructuur voor Hallo Internet toohello.
  * Kanalen toohello basisinfrastructuur moet passeren via beveiligingsapparaten, zoals het nsg's, firewalls of VPN-apparaten.
  * Andere apparaten moeten niet via Internet en Hallo basisinfrastructuur overbruggen.
  * Beveiligingsapparaten op beide internetgerichte Hallo en Hallo beveiligd netwerk geconfronteerd met grenzen van het perimeternetwerk hello (bijvoorbeeld Hallo twee firewall pictogrammen in de vorige afbeelding Hallo) kan in werkelijkheid bestaan uit een enkel virtueel apparaat met gedifferentieerde regels of interfaces voor elke grens. Bijvoorbeeld één fysieke apparaat, logisch van elkaar gescheiden, Hallo belasting voor beide grenzen van het perimeternetwerk Hallo verwerken.
* Andere algemene procedures en beperkingen:
  * Werkbelastingen moeten essentiële bedrijfsgegevens niet opslaan.
  * Toegang en updates tooperimeter netwerkconfiguraties en implementaties zijn beperkt tooonly geautoriseerd-beheerders.

### <a name="perimeter-network-requirements"></a>Perimeter netwerkvereisten
tooenable deze kenmerken, volgt u deze richtlijnen op virtueel netwerk vereisten tooimplement een geslaagde perimeternetwerk:

* **Subnet-architectuur:** Geef Hallo virtueel netwerk dat is een hele subnet als het perimeternetwerk hello toegewezen, gescheiden van andere subnetten in Hallo dezelfde virtueel netwerk. Deze scheiding zorgt ervoor dat Hallo-verkeer tussen het perimeternetwerk Hallo en andere interne of particuliere subnet lagen stromen via een firewall of een virtueel apparaat-id's / IP-Adressen.  Gebruiker gedefinieerde routes op Hallo grens subnetten zijn vereist tooforward dit verkeer toohello virtueel apparaat.
* **NSG:** Hallo perimeter netwerksubnet zelf moet open tooallow communicatie met Internet hello, maar dat betekent niet dat klanten moeten de omzeilen nsg's. Volg algemene beveiliging procedures toominimize Hallo netwerk verwerkingsinformatie blootgesteld toohello Internet. Vergrendelen van externe adresbereiken Hallo toegestaan tooaccess Hallo implementaties of Hallo specifieke toepassingsprotocollen en poorten die geopend zijn. Mogelijk zijn er echter omstandigheden waarin een volledige Lockdown niet mogelijk is. Bijvoorbeeld, als klanten een externe website in Azure, perimeternetwerk Hallo Hallo binnenkomende webaanvragen van openbare IP-adressen moet toestaan, maar moet alleen Hallo web application poorten openen: TCP op poort 80 en/of TCP op poort 443.
* **Routeringstabel:** Hallo perimeter netwerksubnet zelf moet kunnen toocommunicate toohello Internet rechtstreeks, maar mag niet worden tooand rechtstreekse communicatie van de back-end- of on-premises netwerken Hallo zonder tussenkomst van een firewall of beveiligingsapparaat.
* **Beveiligingsconfiguratie toestel:** tooroute en inspecteren van pakketten tussen het perimeternetwerk Hallo en rest Hallo Hallo beveiligde netwerken, Hallo beveiligingsapparaten, zoals firewall, id's en IP-Adressen apparaten mogelijk multihomed. Ze hebben wellicht afzonderlijke NIC's voor het perimeternetwerk Hallo en Hallo back-end-subnetten. Hallo NIC's in het perimeternetwerk Hallo communiceren rechtstreeks tooand van Hallo Internet, hello bijbehorende nsg's en Hallo perimeter-routeringstabel. Hallo NIC's die verbinding maken met back-end-subnetten toohello beperkte meer nsg's en routeringstabellen van Hallo overeenkomstige back-end-subnetten.
* **Functie voor beveiliging toestel:** Hallo beveiligingsapparaten meestal geïmplementeerd in het perimeternetwerk Hallo Hallo functionaliteit volgende uitvoeren:
  * Firewall: Afdwingen firewallregels of beleid voor toegangsbeheer voor inkomende hello-aanvragen.
  * Detectie en preventie van dreiging: opsporen en schadelijke aanvallen van Hallo Internet te beperken.
  * Controle en logboekregistratie: gedetailleerde logboeken voor controle en analyse onderhouden.
  * Omgekeerde proxy: toohello overeenkomende back-endservers omleiden Hallo binnenkomende aanvragen. Deze omleiding omvat het toewijzing en het vertalen van de Hallo doeladressen op Hallo front-apparaten, doorgaans firewalls toohello back-end-serveradressen.
  * Proxy doorsturen: bieden NAT en het uitvoeren van controle-instellingen voor communicatie binnen Hallo virtueel netwerk toohello Internet vanaf gestart.
  * Router: Doorsturen van binnenkomende en meerdere subnetten verkeer in het virtuele netwerk Hallo.
  * VPN-apparaat: fungeert als Hallo cross-premises VPN-gateways voor cross-premises VPN-connectiviteit tussen klant on-premises netwerken en virtuele netwerken in Azure.
  * VPN-server: VPN-clients verbinding maken met virtuele netwerken tooAzure accepteren.

> [!TIP]
> Hallo na twee groepen aparte behouden: Hallo personen gemachtigd tooaccess Hallo perimeter netwerk beveiliging tandwielpictogram en Hallo personen geautoriseerd als beheerders voor ontwikkeling, -implementatie of -bewerkingen. Deze groepen en gescheiden te houden voor een scheiding van taken kunt voorkomen dat één persoon zowel beveiliging van toepassingen en besturingselementen voor de beveiliging.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Vragen toobe gevraagd tijdens het bouwen van de grenzen van netwerken
In deze sectie tenzij specifiek vermeld, Hallo term "netwerken" verwijst tooprivate Azure virtuele netwerken die zijn gemaakt door de abonnementsbeheerder van een. Hallo term verwijst niet toohello onderliggende fysieke netwerken in Azure.

Virtuele netwerken in Azure zijn ook vaak gebruikte tooextend traditionele on-premises netwerken. Het is mogelijk tooincorporate site-naar-site of ExpressRoute hybride oplossingen met perimeter netwerkarchitectuur netwerken. Deze hybride-koppeling is een belangrijk aandachtspunt bij het bouwen van beveiligingsgrenzen netwerk.

Hallo zijn volgende drie vragen kritieke tooanswer wanneer u bij het bouwen van een netwerk met een perimeternetwerk en meerdere beveiligingsgrenzen.

#### <a name="1-how-many-boundaries-are-needed"></a>1) hoeveel grenzen nodig zijn?
de eerste beslissingspunt Hallo is toodecide hoeveel beveiligingsgrenzen nodig zijn in een bepaald scenario:

* De grens van een enkele: één op Hallo front-perimeternetwerk, tussen Hallo virtuele netwerk en Internet Hallo.
* Twee grenzen: een op Internet-zijde van het perimeternetwerk Hallo Hallo en een tussen Hallo perimeter netwerksubnet en Hallo back-end subnetten in Hallo virtuele netwerken in Azure.
* Drie grenzen: één Hallo Internet-zijde van het perimeternetwerk hello, één tussen het perimeternetwerk Hallo en back-end-subnetten en één tussen Hallo back-end-subnetten en Hallo on-premises netwerk.
* N grenzen: het nummer van een variabele. Afhankelijk van de beveiligingsvereisten geldt er geen limiet toohello aantal beveiligingsgrenzen die in een bepaalde netwerk kunnen worden toegepast.

Hallo aantal en type grenzen nodig variëren op basis van een bedrijf risico tolerantie en Hallo specifieke scenario wordt geïmplementeerd. Deze beslissing wordt vaak samen met meerdere groepen binnen een organisatie, inclusief vaak een team risico en naleving, een netwerk en platform-team en het ontwikkelteam van een toepassing uitgevoerd. Mensen met kennis van beveiliging, Hallo gegevens die zijn betrokken en Hallo-technologieën worden gebruikt, moet een zeg hebben in deze beslissing tooensure Hallo geschikte beveiligingscontroles houding ten voor elke implementatie.

> [!TIP]
> Hallo kleinste aantal grenzen die voldoen aan de beveiligingsvereisten Hallo voor een bepaalde situatie gebruiken. Met meer grenzen kunnen bewerkingen en het oplossen van problemen moeilijker, evenals Hallo beheer-overhead voor het beheren van Hallo meerdere grens beleidsregels gedurende een bepaalde periode. Onvoldoende grenzen worden echter risico verhogen. Zoeken naar Hallo saldo is essentieel.
>
>

![6]

Hallo toont voorgaande afbeelding een globaal overzicht van een netwerk met drie beveiliging grens. Hallo grenzen zijn tussen Hallo perimeternetwerk en Hallo Internet, hello Azure front-end en back-end particuliere subnetten, en hello Azure back-end-subnet en Hallo on-premises zakelijke netwerk.

#### <a name="2-where-are-hello-boundaries-located"></a>2) waar zich Hallo grenzen bevinden?
Als Hallo aantal grenzen zijn besloten, waar ze is tooimplement volgende beslissingspunt Hallo. Er zijn doorgaans drie opties:

* Met behulp van een Internet-gebaseerd tussenliggende-service (bijvoorbeeld een cloud-gebaseerde Web application firewall, dit niet in dit document beschreven wordt)
* Gebruik systeemeigen functies en/of virtuele netwerkapparaten in Azure
* Met behulp van fysieke apparaten op Hallo on-premises netwerk

Hallo-opties zijn systeemeigen Azure-functies (bijvoorbeeld Azure Load Balancers) op puur Azure-netwerken, of virtuele netwerkapparaten van Hallo uitgebreide partner ecosysteem van Azure (bijvoorbeeld firewalls Check Point).

Als een grens is vereist tussen Azure en een on-premises netwerk, kunnen Hallo beveiligingsapparaten zich aan beide zijden van Hallo verbinding (of beide zijden). Een beslissing moet dus worden aangebracht op Hallo locatie tooplace beveiliging tandwielpictogram.

In de vorige afbeelding hello, de Internet-perimeternetwerk Hallo Hallo front-to-back-end grenzen volledig zijn opgenomen in Azure en moeten systeemeigen Azure-functies of virtuele netwerkapparaten. Van beveiligingsapparaten op Hallo grens tussen Azure (back-end subnet) en Hallo bedrijfsnetwerk kan worden op Hallo Azure aan clientzijde of Hallo lokale aan clientzijde of zelfs een combinatie van apparaten aan beide zijden. Kan er grote voordelen en nadelen tooeither optie die ernstig moet worden beschouwd.

Bijvoorbeeld, gebruik bestaande fysieke beveiliging versnelling op Hallo on-premises netwerk heeft Hallo voordeel dat er geen nieuwe tandwielpictogram is vereist. Deze moet herconfiguratie. Hallo-nadeel is echter dat alle verkeer van Azure toohello lokale netwerk toobe gezien door Hallo beveiliging tandwielpictogram terugkeren moet. Dus Azure naar Azure-verkeer kan worden belangrijke latentie en invloed hebben op prestaties en gebruikerservaring van toepassing, als back-toohello is afgedwongen op het lokale netwerk voor beveiliging wordt afgedwongen.

#### <a name="3-how-are-hello-boundaries-implemented"></a>3) de wijze waarop zijn Hallo grenzen geïmplementeerd?
Elke beveiligingsgrens wordt waarschijnlijk hebben verschillende vereisten (bijvoorbeeld-id's en firewallregels op Hallo Internet kant van het perimeternetwerk hello, maar alleen ACL's tussen Hallo perimeternetwerk en het subnet van de back-end). Bepalen op welke apparaat (of het aantal apparaten) toouse is afhankelijk van Hallo scenario en beveiligingsvereisten. In de Hallo volgende sectie, besproken voorbeelden 1, 2 en 3 enkele mogelijkheden die kunnen worden gebruikt. Hello Azure systeemeigen netwerkfuncties en beschikbaar zijn in Azure uit ecosysteem voor partners Hallo Hallo-apparaten te controleren, toont Hallo allerlei opties beschikbaar toosolve vrijwel elk scenario.

Een ander beslissingspunt voor de implementatie van de sleutel is hoe tooconnect Hallo lokale netwerk met Azure. Moet u hello Azure virtuele gateway of een virtueel netwerkapparaat gebruiken? Deze opties worden in de volgende sectie (voorbeelden 4, 5 en 6) Hallo uitgebreider besproken.

Bovendien het verkeer tussen virtuele netwerken in Azure nodig. Deze scenario's worden toegevoegd in toekomstige Hallo.

Zodra u Hallo-antwoorden toohello vorige vragen weet, Hallo [snel starten](#fast-start) sectie kunt achterhalen welke voorbeelden zijn het meest geschikt is voor een bepaald scenario.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Voorbeelden: Beveiligingsgrenzen met virtuele netwerken in Azure bouwen
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Voorbeeld 1 Build een perimeternetwerk netwerk toohelp toepassingen met nsg's beveiligen
[Back-tooFast start](#fast-start) | [gedetailleerde instructies voor dit voorbeeld bouwen][Example1]

[![7]][7]

#### <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld zijn er is een abonnement met Hallo resources te volgen:

- Één resourcegroep
- Een virtueel netwerk met twee subnetten: 'FrontEnd' en back-end'
- Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten
- Een Windows-server waarmee een toepassing webserver ('IIS01')
- Twee Windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')
- Een Windows-server met een DNS-server ('DNS01')
- Een openbaar IP-adres die zijn gekoppeld aan de webserver Hallo-toepassing

Zie voor scripts en een Azure Resource Manager-sjabloon Hallo [gedetailleerde instructies voor de build][Example1].

#### <a name="nsg-description"></a>NSG-beschrijving
In dit voorbeeld is een groep NSG gebouwd en vervolgens met zes regels worden geladen.

> [!TIP]
> In het algemeen moet u maken uw specifieke regels voor 'Toestaan' eerst, gevolgd door Hallo algemene regels voor ' toestaan'. Hallo prioriteit bepaalt welke regels eerst worden geëvalueerd. Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd. NSG-regels kunnen toepassen in een Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).
>
>

Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:

1. Interne DNS-verkeer (poort 53) is toegestaan.
2. RDP-verkeer (poort 3389) van Hallo Internet tooany virtuele Machine is toegestaan.
3. HTTP-verkeer (poort 80) van Hallo tooweb internetserver (IIS01) is toegestaan.
4. Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan.
5. Verkeer (alle poorten) met Hallo Internet toohello volledige virtuele netwerk (beide subnetten) is geweigerd.
6. Verkeer (alle poorten) van Hallo front-end-subnet toohello back-end-subnet is geweigerd.

Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn. Maar omdat regel 3 een hogere prioriteit heeft, alleen zou worden toegepast en regel 5 niet in de play zou komen. Hallo HTTP-aanvraag zou dus toohello webserver toegestaan. Als dat dezelfde verkeer tooreach hello DNS01 server probeert is, regel 5 (weigeren) Hallo eerste tooapply en Hallo verkeer zou niet toegestaan toopass toohello server zou zijn. Regel 6 (weigeren) blokken Hallo front-end-subnet uit praten toohello back-end-subnet (met uitzondering van toegestane verkeer in regels 1 en 4). Deze regelset beschermt Hallo back-endnetwerk als een aanvaller wordt aangetast Hallo webtoepassing op Hallo-front-end. Hallo aanvaller zou hebben beperkte toegang tot toohello back-end 'beveiligde' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).

Er is een uitgaande standaardregel waarmee verkeer van toohello Internet. Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen. toolock omlaag verkeer in beide richtingen gebruiker gedefinieerde routering is vereist (Zie voorbeeld 3).

#### <a name="conclusion"></a>Conclusie
In dit voorbeeld is een relatief eenvoudig en snel manier Hallo back-end subnet uit binnenkomend verkeer isoleren. Zie voor meer informatie, Hallo [gedetailleerde instructies voor de build][Example1]. Deze instructies zijn onder andere:

* Hoe toobuild deze perimeter netwerk met klassieke PowerShell-scripts.
* Hoe toobuild deze perimeter netwerk met een Azure Resource Manager-sjabloon.
* Gedetailleerde beschrijvingen van elke NSG-opdracht.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe het verkeer wordt toegestaan of geweigerd in elke laag.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Voorbeeld 2 Build een perimeternetwerk netwerk toohelp toepassingen met een firewall en nsg's beveiligen
[Back-tooFast start](#fast-start) | [gedetailleerde instructies voor dit voorbeeld bouwen][Example2]

[![8]][8]

#### <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld zijn er is een abonnement met Hallo resources te volgen:

* Één resourcegroep
* Een virtueel netwerk met twee subnetten: 'FrontEnd' en back-end'
* Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten
* Een virtueel netwerkapparaat, in dit geval een firewall, verbonden toohello front-end-subnet
* Een Windows-server waarmee een toepassing webserver ('IIS01')
* Twee Windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')

Zie voor scripts en een Azure Resource Manager-sjabloon Hallo [gedetailleerde instructies voor de build][Example2].

#### <a name="nsg-description"></a>NSG-beschrijving
In dit voorbeeld is een groep NSG gebouwd en vervolgens met zes regels worden geladen.

> [!TIP]
> In het algemeen moet u maken uw specifieke regels voor 'Toestaan' eerst, gevolgd door Hallo algemene regels voor ' toestaan'. Hallo prioriteit bepaalt welke regels eerst worden geëvalueerd. Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd. NSG-regels kunnen toepassen in een Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).
>
>

Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:

1. Interne DNS-verkeer (poort 53) is toegestaan.
2. RDP-verkeer (poort 3389) van Hallo Internet tooany virtuele Machine is toegestaan.
3. Een Internet-verkeer (alle poorten) toohello virtueel netwerkapparaat (firewall) is toegestaan.
4. Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan.
5. Verkeer (alle poorten) met Hallo Internet toohello volledige virtuele netwerk (beide subnetten) is geweigerd.
6. Verkeer (alle poorten) van Hallo front-end-subnet toohello back-end-subnet is geweigerd.

Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo toohello firewall voor Internet-beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn. Maar omdat regel 3 een hogere prioriteit heeft, alleen zou worden toegepast en regel 5 niet in de play zou komen. Hallo HTTP-aanvraag zou dus toohello firewall toegestaan. Als dat dezelfde verkeer tooreach hello IIS01 server, probeerde zelfs als het op de front-end-subnet hello, regel 5 (weigeren) toepassing zou zijn, en Hallo verkeer zou mag niet worden toopass toohello server. Regel 6 (weigeren) blokken Hallo front-end-subnet uit praten toohello back-end-subnet (met uitzondering van toegestane verkeer in regels 1 en 4). Deze regelset beschermt Hallo back-endnetwerk als een aanvaller wordt aangetast Hallo webtoepassing op Hallo-front-end. Hallo aanvaller zou hebben beperkte toegang tot toohello back-end 'beveiligde' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).

Er is een uitgaande standaardregel waarmee verkeer van toohello Internet. Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen. toolock omlaag verkeer in beide richtingen gebruiker gedefinieerde routering is vereist (Zie voorbeeld 3).

#### <a name="firewall-rule-description"></a>De beschrijving van de firewall-regel
Hallo-firewall voor moet het doorsturen van regels worden gemaakt. Omdat dit voorbeeld alleen routes Internet verkeer in de gebonden toohello firewall en vervolgens toohello webserver, slechts één doorsturen netwerkadresomzetting (NAT) wordt regel vereist.

Hallo doorsturen regel accepteert inkomende bronadres dat treffers Hallo firewall probeert tooreach HTTP (poort 80 of 443 voor HTTPS). Deze heeft verzonden buiten de lokale interface van Hallo firewall en toohello webserver met IP-adres van 10.0.1.5 Hallo omgeleid.

#### <a name="conclusion"></a>Conclusie
In dit voorbeeld is een relatief eenvoudige manier van het beveiligen van uw toepassing met een firewall en Hallo back-end subnet uit binnenkomend verkeer isoleren. Zie voor meer informatie, Hallo [gedetailleerde instructies voor de build][Example2]. Deze instructies zijn onder andere:

* Hoe toobuild deze perimeter netwerk met klassieke PowerShell-scripts.
* Hoe toobuild in dit voorbeeld met een Azure Resource Manager-sjabloon.
* Gedetailleerde beschrijvingen van elke NSG-opdracht en firewall-regel.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe het verkeer wordt toegestaan of geweigerd in elke laag.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Voorbeeld 3 Build een perimeternetwerk netwerk toohelp netwerken met een firewall en UDR en NSG beschermen
[Back-tooFast start](#fast-start) | [gedetailleerde instructies voor dit voorbeeld bouwen][Example3]

[![9]][9]

#### <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld zijn er is een abonnement met Hallo resources te volgen:

* Één resourcegroep
* Een virtueel netwerk met drie subnetten: 'SecNet', 'FrontEnd' en back-end'
* Een virtueel netwerkapparaat, in dit geval een firewall, verbonden toohello SecNet subnet
* Een Windows-server waarmee een toepassing webserver ('IIS01')
* Twee Windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')

Zie voor scripts en een Azure Resource Manager-sjabloon Hallo [gedetailleerde instructies voor de build][Example3].

#### <a name="udr-description"></a>UDR beschrijving
Standaard worden Hallo na systeemroutes gedefinieerd als:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hallo VNETLocal is altijd een of meer gedefinieerde adresvoorvoegsels die gezamenlijk Hallo virtueel netwerk voor het specifieke netwerk (dat wil zeggen, verandert van virtueel netwerk toovirtual netwerk, afhankelijk van hoe elk specifiek virtueel netwerk is gedefinieerd). Hallo resterende systeemroutes zijn statisch en standaard aangegeven in de tabel Hallo.

In dit voorbeeld zijn twee routeringstabellen gemaakt, één voor Hallo front-end en back-end-subnetten. Elke tabel is geladen met statische routes die geschikt is voor Hallo opgegeven subnet. In dit voorbeeld wordt elke tabel heeft drie routes die alle verkeer (0.0.0.0/0) via de firewall hello (volgende hop = virtueel apparaat IP-adres):

1. Lokaal subnetverkeer met geen volgende Hop gedefinieerd tooallow lokale subnet verkeer toobypass Hallo firewall.
2. Virtueel netwerkverkeer met een volgende Hop gedefinieerd als een firewall. Deze volgende hops overschrijvingen Hallo standaardregel waarmee lokale virtuele netwerkverkeer tooroute rechtstreeks.
3. Alle resterende verkeer (0/0) met de volgende Hop gedefinieerd als een firewall Hallo.

> [!TIP]
> Hallo lokale subnetvermelding hoeft niet in Hallo UDR einden lokale subnet communicatie.
>
> * In ons voorbeeld is de 10.0.1.0/24 wijzen tooVNETLocal kritieke! Zonder dit mislukken pakket verlaten Hallo Web Server (10.0.1.4) dat is bestemd tooanother lokale server (bijvoorbeeld) 10.0.1.25 als ze worden verzonden toohello NVA. Hallo NVA stuurt het toohello subnet en Hallo subnet wordt deze verzenden toohello NVA in een oneindige lus.
> * Hallo kans op een routeringslus zijn meestal hoger op apparaten met meerdere NIC's die zijn verbonden tooseparate subnetten, dit is vaak van traditionele, lokale apparaten.
>
>

Zodra de routeringstabellen Hallo zijn gemaakt, moeten afhankelijke tootheir subnetten. Hallo front-end-subnet routeringstabel, eenmaal is gemaakt en gekoppeld toohello subnet, eruit als deze uitvoer:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR kan nu worden toegepaste toohello gatewaysubnet op welke Hallo ExpressRoute circuit is verbonden.
>
> Voorbeelden van hoe tooenable uw perimeternetwerk netwerk via ExpressRoute of site-naar-site-netwerk worden weergegeven in de voorbeelden 3 en 4.
>
>

#### <a name="ip-forwarding-description"></a>Beschrijving doorsturen via IP
Doorsturen via IP is een functie companion tooUDR. Doorsturen via IP is een instelling op een virtueel apparaat die toestaat dat deze tooreceive verkeer niet specifiek gericht toohello toestel en vervolgens doorsturen die verkeer tooits uiteindelijke bestemming.

Als AppVM01 een aanvraag toohello DNS01-server doet, zou UDR deze toohello-firewall verkeer routeren. Bij het doorsturen via IP is ingeschakeld, is het Hallo-verkeer voor Hallo DNS01 doel (10.0.2.4) geaccepteerd door Hallo toestel (10.0.0.4) en vervolgens doorgestuurd tooits uiteindelijke bestemming (10.0.2.4). Zonder doorsturen via IP op Hallo-firewall is ingeschakeld, zou verkeer niet geaccepteerd door Hallo toestel Hoewel routetabel Hallo Hallo firewall als de volgende hop Hallo is. een virtueel apparaat toouse, kritieke tooremember tooenable IP Forwarding samen met UDR is.

#### <a name="nsg-description"></a>NSG-beschrijving
In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met een enkele regel. Deze groep wordt vervolgens gebonden alleen toohello front-end en back-end subnetten (geen hello SecNet). Declaratief wordt Hallo-regel samengesteld:

* Verkeer (alle poorten) met Hallo Internet toohello volledige virtuele netwerk (alle subnetten) is geweigerd.

Hoewel het nsg's in dit voorbeeld worden gebruikt, worden de belangrijkste doel is als een laag secundaire beveiliging tegen handmatige onjuiste configuratie. Hallo doel is tooblock al het inkomende verkeer van Hallo Internet tooeither Hallo front-end of back-end-subnetten. Verkeersstroom moet alleen via Hallo SecNet subnet toohello firewall (en vervolgens, indien van toepassing op de front- of back-end subnetten toohello). Bovendien met Hallo UDR regels aanwezig is, zou verkeer om het in Hallo front-end of back-end subnetten omgeleid uit toohello firewall (Bedankt tooUDR). Hallo firewall zou dit verkeer zien als een asymmetrische stroom en uitgaand verkeer hello wilt verwijderen. Er zijn dus drie beveiligingslagen Hallo subnetten beveiligen:

* Er is geen openbare IP-adressen op elke front-end of back-end-NIC's.
* Nsg's voor het weigeren van verkeer van de Hallo Internet.
* Hallo firewall weggehaald asymmetrische verkeer.

Een interessant punt met betrekking tot Hallo NSG in dit voorbeeld is dat deze toodeny Internet verkeer toohello volledige virtuele netwerk, inclusief Hallo beveiliging subnet slechts één regel bevat. Aangezien Hallo die NSG alleen is gebonden toohello front-end en back-end-subnetten, Hallo-regel is niet verwerkt op het verkeer inkomend echter toohello beveiliging subnet. Als gevolg hiervan verkeersstromen toohello beveiliging subnet.

#### <a name="firewall-rules"></a>Firewall-regels
Hallo-firewall voor moet het doorsturen van regels worden gemaakt. Omdat Hallo-firewall geblokkeerd of doorsturen alle binnenkomende, uitgaande en binnen virtueel netwerkverkeer is, worden veel firewallregels vereist. Ook alle binnenkomend verkeer komt binnen via Hallo beveiligingsservice openbaar IP-adres (op verschillende poorten) toobe verwerkt door Hallo firewall. Is een best practice toodiagram Hallo logische stromen voordat u Hallo subnetten instelt en firewallregels, tooavoid later bijwerken. Hallo is volgende afbeelding een logische weergave van de firewallregels Hallo voor dit voorbeeld:

![10]

> [!NOTE]
> Op basis van Hallo die virtueel netwerkapparaat gebruikt, variëren Hallo beheerpoorten. In dit voorbeeld wordt een Barracuda NextGen Firewall naar wordt verwezen, waarbij poorten 22, 801 en 807 wordt gebruikt. Raadpleeg Hallo toestel leverancier documentatie toofind Hallo exacte poorten die worden gebruikt voor het beheer van Hallo-apparaat wordt gebruikt.
>
>

#### <a name="firewall-rules-description"></a>Beschrijving van de firewall-regels
In Hallo voorgaande logisch diagram, Hallo beveiliging subnet niet weergegeven omdat Hallo firewall Hallo enige resource in dat subnet. Hallo diagram worden weergegeven Hallo firewallregels en hoe ze logisch toestaan of verkeersstromen, niet Hallo werkelijke gerouteerde pad weigeren. Ook Hallo externe poorten geselecteerd voor Hallo RDP-verkeer hoger varieerde poorten (8014 – 8026) zijn en zijn geselecteerde tooloosely zijn afgestemd op Hallo van laatste twee octetten van het lokale IP-adres voor een eenvoudiger leesbaarheid Hallo (bijvoorbeeld 10.0.1.4-adres van de lokale server is gekoppeld met de externe poort 8014). Eventuele niet-conflicterende hoger poorten, kunnen echter worden gebruikt.

Bijvoorbeeld moeten we zeven typen regels:

* Externe regels (voor inkomend verkeer):
  1. Firewallregel management: deze App omleiden regel staat toe dat verkeer toopass toohello beheerpoorten van virtueel netwerkapparaat Hallo.
  2. RDP-regels (voor elke WindowsServer): beheer van Hallo afzonderlijke servers via RDP deze vier regels (één voor elke server) toestaan. Hallo vier RDP-regels kunnen ook worden samengevoegd tot één regel, afhankelijk van het Hallo-mogelijkheden van Hallo virtueel netwerkapparaat wordt gebruikt.
  3. Regels voor het netwerkverkeer van toepassing: Er zijn twee van deze regels, Hallo eerst voor de front-webverkeer Hallo en Hallo tweede voor verkeer van de back-end hello (bijvoorbeeld web server toodata laag). Hallo-configuratie van deze regels, is afhankelijk van Hallo netwerkarchitectuur (waar uw servers worden geplaatst) en verkeersstromen (welke richting Hallo-verkeersstromen en welke poorten worden gebruikt).
     * Hallo eerste regel staat toe Hallo werkelijke verkeer tooreach Hallo toepassing toepassingsserver. Hallo andere regels toestaan voor beveiliging en beheer, zijn toepassing verkeersregels wat kunnen externe gebruikers of services tooaccess Hallo-toepassingen. In dit voorbeeld moet u er één webserver is op poort 80. Een firewallregel voor één toepassing omgeleid dus binnenkomend verkeer toohello extern IP-adres, toohello web servers interne IP-adres. Hallo omgeleid verkeer sessie zou worden omgezet via NAT toohello interne serverfout.
     * de tweede regel Hallo is Hallo back-end-regel tooallow Hallo server tootalk toohello AppVM01 webserver (maar niet AppVM02) via een willekeurige poort.
* Interne regels (voor binnen virtueel netwerkverkeer)
  1. Regel voor uitgaande tooInternet: met deze regel kunnen het verkeer van een netwerk toopass toohello geselecteerd netwerken. Deze regel is meestal een standaardregel al op Hallo firewall, maar in een uitgeschakelde status. Deze regel moet worden ingeschakeld voor dit voorbeeld.
  2. Een DNS-regel: met deze regel kunnen alleen DNS (poort 53)-verkeer toopass toohello DNS-server. Voor deze omgeving zijn de meeste verkeer van Hallo toohello back-end-front-end is geblokkeerd. Deze regel kunnen specifiek DNS van een lokale subnet.
  3. Subnet toosubnet regel: met deze regel is tooallow een server op Hallo back-end subnet tooconnect tooany server op Hallo front-end-subnet (maar niet Hallo omgekeerde).
* Foutveilige regel (voor verkeer dat niet voldoet aan een van de vorige Hallo):
  1. Alle verkeersregel voor weigeren: deze regel voor weigeren moet altijd de laatste regel hello (in termen van prioriteit) en als zodanig als netwerkverkeer mislukt toomatch van Hallo voorafgaand aan de regels wordt deze verwijderd door deze regel. Deze regel is een standaardregel en meestal in-place en actief. Er zijn geen wijzigingen zijn meestal nodig toothis regel.

> [!TIP]
> Op Hallo is tweede toepassing verkeer regel toosimplify dit voorbeeld wordt een willekeurige poort toegestaan. In een echte scenario moet de meest specifiek poort en bereiken Hallo gebruikte tooreduce Hallo kwetsbaarheid voor aanvallen van deze regel.
>
>

Zodra de vorige regels Hallo zijn gemaakt, is het belangrijk tooreview Hallo prioriteit van elke regel tooensure-verkeer wordt toegestaan of geweigerd desgewenst. In dit voorbeeld zijn Hallo regels in volgorde van prioriteit.

#### <a name="conclusion"></a>Conclusie
In dit voorbeeld is een complexere maar manier van het beveiligen en isoleren Hallo netwerk dan eerdere voorbeelden Hallo voltooien. (Voorbeeld 2 beveiligt alleen de toepassing hello en net isoleert subnetten voorbeeld 1). Dit ontwerp kunt u verkeer in beide richtingen, bewaking en niet alleen Hallo die inkomende toepassingsserver beveiligt, maar wordt afgedwongen beveiligingsbeleid voor alle servers in dit netwerk netwerk. Ook afhankelijk van het Hallo-apparaat gebruikt, kunnen verkeer met volledige controle en het bewustzijn worden bereikt. Zie voor meer informatie, Hallo [gedetailleerde instructies voor de build][Example3]. Deze instructies zijn onder andere:

* Hoe toobuild in dit voorbeeld perimeter netwerk met klassieke PowerShell-scripts.
* Hoe toobuild in dit voorbeeld met een Azure Resource Manager-sjabloon.
* Gedetailleerde beschrijvingen van elke UDR, NSG opdracht en de firewallregel.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe het verkeer wordt toegestaan of geweigerd in elke laag.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Voorbeeld 4 een hybride verbinding met een site-naar-site, een virtueel apparaat VPN toevoegen
[Back-tooFast start](#fast-start) | Gedetailleerde build instructies beschikbaar binnenkort

[![11]][11]

#### <a name="environment-description"></a>Beschrijving van de omgeving
Hybride netwerken met behulp van een virtueel netwerkapparaat (NVA) kan worden toegevoegd als tooany van Hallo typen perimeternetwerk dat wordt beschreven in de voorbeelden 1, 2 of 3.

Zoals u in de vorige afbeelding hello, is een VPN-verbinding via Internet (site-naar-site) Hallo gebruikte tooconnect een lokaal netwerk tooan virtuele Azure-netwerk via een NVA.

> [!NOTE]
> Als u ExpressRoute met hello Azure openbare Peering optie is ingeschakeld gebruikt, kan een statische route moet worden gemaakt. Deze statische route moet routeren toohello NVA VPN-IP-adres van uw zakelijke Internet en niet via Hallo ExpressRoute-verbinding. Hallo NAT vereist op Hallo optie ExpressRoute Azure openbare Peering kunt Hallo VPN-sessie te verbreken.
>
>

Hallo VPN-netwerk aanwezig is, is NVA Hallo maakt Hallo centrale hub voor alle netwerken en subnetten. Hallo doorsturen firewallregels bepalen welk verkeer stroomt zijn toegestaan, worden omgezet via NAT worden omgeleid of worden verwijderd (zelfs voor verkeersstromen tussen Hallo on-premises netwerk en Azure).

Verkeersstromen moeten zorgvuldig worden beschouwd als ze kunnen worden geoptimaliseerd of gedegradeerd door dit ontwerp gaat, afhankelijk van specifieke Hallo gebruiksvoorbeeld.

Gebruik Hallo-omgeving is ingebouwd in voorbeeld 3 en vervolgens toe te voegen een netwerkverbinding voor site-naar-site VPN-hybride produceert Hallo ontwerp te volgen:

[![12]][12]

Hallo lokale router of andere netwerkapparaten die compatibel is met uw NVA voor VPN, zou Hallo VPN-client zijn. Deze fysieke apparaat zou zijn verantwoordelijk voor het initiëren en Hallo VPN-verbinding met uw NVA onderhouden.

Logisch toohello NVA, Hallo netwerk eruit vier afzonderlijke "beveiligingszones" hello regels op Hallo NVA wordt Hallo primaire directeur van verkeer tussen deze zones:

![13]

#### <a name="conclusion"></a>Conclusie
Hallo toevoeging van een site-naar-site VPN-hybride netwerk verbinding tooan virtuele Azure-netwerk kunt op een veilige manier Hallo on-premises netwerk uitbreiden naar Azure. Bij het gebruik van een VPN-verbinding verkeer worden versleuteld en routeert via Hallo Internet. Hallo NVA in dit voorbeeld biedt een centrale locatie tooenforce en Hallo beveiligingsbeleid beheren. Zie voor meer informatie, Hallo gedetailleerde instructies (binnenkort uitgebracht) bouwen. Deze instructies zijn onder andere:

* Hoe toobuild in dit voorbeeld perimeter netwerk met PowerShell-scripts.
* Hoe toobuild in dit voorbeeld met een Azure Resource Manager-sjabloon.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe verkeer via dit ontwerp loopt.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Voorbeeld 5 een hybride verbinding met een Azure VPN-gateway voor site-naar-site toevoegen
[Back-tooFast start](#fast-start) | Gedetailleerde build instructies beschikbaar binnenkort

[![14]][14]

#### <a name="environment-description"></a>Beschrijving van de omgeving
Hybride netwerken met behulp van een Azure VPN-gateway kan worden toegevoegd als tooeither type perimeternetwerk dat wordt beschreven in de voorbeelden 1 of 2.

Zoals u in de voorgaande afbeelding hello, is een VPN-verbinding via Internet (site-naar-site) Hallo gebruikte tooconnect een lokaal netwerk tooan virtuele Azure-netwerk via een Azure VPN-gateway.

> [!NOTE]
> Als u ExpressRoute met hello Azure openbare Peering optie is ingeschakeld gebruikt, kan een statische route moet worden gemaakt. Deze statische route moet toohello NVA VPN-IP-adres van uw zakelijke Internet en niet via ExpressRoute WAN Hallo routeren. Hallo NAT vereist op Hallo optie ExpressRoute Azure openbare Peering kunt Hallo VPN-sessie te verbreken.
>
>

Hallo volgende afbeelding toont Hallo twee netwerk randen in dit voorbeeld. Op de eerste rand hello, Hallo NVA en nsg's beheren van verkeersstromen voor binnen Azure-netwerken en tussen Azure en Internet Hallo. de tweede rand Hallo is hello Azure VPN-gateway, een afzonderlijke en geïsoleerd netwerk-rand tussen on-premises en Azure is.

Verkeersstromen moeten zorgvuldig worden beschouwd als ze kunnen worden geoptimaliseerd of gedegradeerd door dit ontwerp gaat, afhankelijk van specifieke Hallo gebruiksvoorbeeld.

Gebruik Hallo-omgeving is ingebouwd in voorbeeld 1 en vervolgens toe te voegen een netwerkverbinding voor site-naar-site VPN-hybride produceert Hallo ontwerp te volgen:

[![15]][15]

#### <a name="conclusion"></a>Conclusie
Hallo toevoeging van een site-naar-site VPN-hybride netwerk verbinding tooan virtuele Azure-netwerk kunt op een veilige manier Hallo on-premises netwerk uitbreiden naar Azure. Met Hallo systeemeigen Azure VPN-gateway, het verkeer is IPSec-versleuteld en via Internet Hallo van routes. Met behulp van hello Azure VPN-gateway kunt ook een lagere kosten-optie (Er is geen aanvullende licenties kosten net als bij de derde partij NVAs) opgeven. Deze optie is meest voordelige in voorbeeld 1, waarbij geen NVA wordt gebruikt. Zie voor meer informatie, Hallo gedetailleerde instructies (binnenkort uitgebracht) bouwen. Deze instructies zijn onder andere:

* Hoe toobuild in dit voorbeeld perimeter netwerk met PowerShell-scripts.
* Hoe toobuild in dit voorbeeld met een Azure Resource Manager-sjabloon.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe verkeer via dit ontwerp loopt.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Voorbeeld 6 een hybride verbinding toevoegen met ExpressRoute
[Back-tooFast start](#fast-start) | Gedetailleerde build instructies beschikbaar binnenkort

[![16]][16]

#### <a name="environment-description"></a>Beschrijving van de omgeving
Hybride netwerken met behulp van een ExpressRoute persoonlijke peering verbinding kan worden toegevoegd tooeither type perimeternetwerk dat wordt beschreven in de voorbeelden 1 of 2.

Zoals u in de voorgaande afbeelding hello, biedt privépeering ExpressRoute een rechtstreekse verbinding tussen uw on-premises netwerk en het Hallo virtuele Azure-netwerk. Verkeer passages alleen Hallo serviceprovider-netwerk en Hallo Microsoft Azure-netwerk, nooit door Hallo Internet aan te raken.

> [!TIP]
> Met behulp van ExpressRoute, houdt u zakelijke netwerkverkeer uitschakelen Hallo Internet. Daarnaast kunt u serviceovereenkomsten van uw ExpressRoute-provider. Hello Azure Gateway kunt doorgeven up too10 Gbps met ExpressRoute, terwijl met site-naar-site-VPN's hello Azure Gateway maximale doorvoer 200 Mbps.
>
>

Zoals u in het volgende diagram hello, met deze optie Hallo heeft omgeving nu twee randen van het netwerk. Hallo NVA en NSG besturingselement verkeersstromen voor binnen Azure-netwerken en tussen Azure en Hallo Internet, terwijl het Hallo-gateway is een afzonderlijke en geïsoleerd netwerk-rand tussen on-premises en Azure.

Verkeersstromen moeten zorgvuldig worden beschouwd als ze kunnen worden geoptimaliseerd of gedegradeerd door dit ontwerp gaat, afhankelijk van specifieke Hallo gebruiksvoorbeeld.

Gebruik Hallo-omgeving is ingebouwd in voorbeeld 1 en vervolgens toe te voegen een netwerkverbinding ExpressRoute hybride produceert Hallo ontwerp te volgen:

[![17]][17]

#### <a name="conclusion"></a>Conclusie
toevoeging van een netwerkverbinding ExpressRoute persoonlijke Peering Hallo kunt Hallo on-premises netwerk uitbreiden naar Azure in een beveiligde, lagere latentie, manier hoger uitvoeren. Hallo met biedt systeemeigen Azure-Gateway, zoals in dit voorbeeld ook een lagere kosten-optie (Er is geen nadere net als bij de derde partij NVAs-licentieverlening). Zie voor meer informatie, Hallo gedetailleerde instructies (binnenkort uitgebracht) bouwen. Deze instructies zijn onder andere:

* Hoe toobuild in dit voorbeeld perimeter netwerk met PowerShell-scripts.
* Hoe toobuild in dit voorbeeld met een Azure Resource Manager-sjabloon.
* Gedetailleerde verkeer stroom scenario's, die laat zien hoe verkeer via dit ontwerp loopt.

## <a name="references"></a>Verwijzingen
### <a name="helpful-websites-and-documentation"></a>Documentatie en nuttige websites
* Toegang van Azure met Azure Resource Manager:
* Toegang tot Azure met PowerShell: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Informatie over virtuele netwerken: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Network security groep documentatie: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Gebruiker gedefinieerde routering documentatie: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Azure virtuele gateways: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* Site-naar-Site VPN-verbindingen: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* ExpressRoute-documentatie (ervoor toocheck Hallo 'Aan de slag' en 'How To'-secties worden): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Stroomdiagram beveiligingsopties"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "azure beveiligingsfuncties"
[3]: ./media/best-practices-network-security/dmzcorporate.png "DMZ A in een bedrijfsnetwerk"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "architectuur van de azure-beveiliging"
[5]: ./media/best-practices-network-security/dmzazure.png "een DMZ in een Azure-netwerk"
[6]: ./media/best-practices-network-security/dmzhybrid.png "hybride netwerk met drie beveiligingsgrenzen"
[7]: ./media/best-practices-network-security/example1design.png "Inkomende DMZ met NSG"
[8]: ./media/best-practices-network-security/example2design.png "Inkomende DMZ met NVA en NSG"
[9]: ./media/best-practices-network-security/example3design.png "Bidirectionele DMZ met NVA, NSG en UDR"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "logische weergave van Hallo Firewall-regels"
[11]: ./media/best-practices-network-security/example3designoptions.png "Perimeternetwerk met NVA hybride netwerk verbonden"
[12]: ./media/best-practices-network-security/example4designs2s.png "Perimeternetwerk met NVA verbonden via een Site-naar-Site-VPN"
[13]: ./media/best-practices-network-security/example4networklogical.png "logisch netwerk vanuit NVA perspectief"
[14]: ./media/best-practices-network-security/example5designoptions.png "Perimeternetwerk met Azure-Gateway verbonden Site-naar-Site hybride netwerk"
[15]: ./media/best-practices-network-security/example5designs2s.png "Perimeternetwerk met Azure via Site-naar-Site VPN-Gateway"
[16]: ./media/best-practices-network-security/example6designoptions.png "Perimeternetwerk met Azure-Gateway verbonden ExpressRoute hybride netwerk"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Perimeternetwerk met Azure-Gateway met behulp van een ExpressRoute-verbinding"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
