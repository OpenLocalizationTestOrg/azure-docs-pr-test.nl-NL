---
title: Azure virtuele Data Center aaaMicrosoft | Microsoft Docs
description: Meer informatie over hoe toobuild uw virtuele datacentrum in Azure
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Microsoft Azure virtuele Data Center
**Microsoft Azure**: sneller, geld besparen, integreren lokale apps en gegevens

## <a name="overview"></a>Overzicht
Migreren van lokale toepassingen tooAzure kunnen zelfs zonder aanzienlijke wijzigingen (een methode die bekend staat als 'lift- en verschuiven'), organisaties Hallo voordelen van een beveiligde en voordelige infrastructuur. Echter toomake meest Hallo van Hallo flexibiliteit mogelijk met cloud computing, ondernemingen hun architecturen tootake profiteren van de mogelijkheden van Azure te ontwikkelen. Microsoft Azure biedt hyperschaal services en infrastructuur, bedrijfsniveau mogelijkheden en betrouwbaarheid en veel keuzes voor hybride verbindingen. Klanten kunnen kiezen tooaccess deze cloud services-via Internet Hallo of met Azure ExpressRoute, waarmee de verbinding met het particuliere netwerk. Hallo Microsoft Azure-platform kan klanten tooseamlessly Hallo cloud kunnen hun infrastructuur uitbreiden en meerdere lagen architecturen bouwen. Bovendien Microsoft-partners uitgebreide mogelijkheden bieden door het aanbieden van beveiligingsservices en virtuele apparaten die zijn geoptimaliseerd toorun in Azure.

In dit artikel biedt een overzicht van patronen en modellen die gebruikt toosolve worden kunnen Hallo architectuur schaal, prestaties en beveiliging problemen die veel klanten te maken wanneer u nadenkt over het verplaatsen en masse toohello cloud. Een overzicht van hoe toofit verschillende organisatie-IT-functies in Hallo management en beheer van Hallo system wordt ook beschreven, met nadruk toosecurity vereisten en kostenoptimalisatie van de.

## <a name="what-is-a-virtual-data-center"></a>Wat is er een virtuele-Datacenter?
In Hallo vroege dagen cloud oplossingen zijn ontworpen toohost enkele, relatief geïsoleerde toepassingen in de openbare spectrum Hallo. Deze aanpak goed functioneren voor een aantal jaren. Echter als Hallo voordelen van cloudcomputing oplossingen is gebleken en meerdere grootschalige workloads zijn gehost op cloud hello, beveiliging, betrouwbaarheid, prestaties, adressering en de kosten van de problemen van implementaties in een of meer regio's is essentieel in de gehele Hallo geworden levenscyclus van Hallo-cloudservice.

Hallo volgende cloud implementatie diagram ziet u enkele voorbeelden van beveiliging hiaten (rood kader) en ruimte voor de optimalisatie van virtuele netwerkapparaten via werkbelastingen (geel vak).

[![0]][0]

Hallo virtuele Data Center (VDC's) van deze noodzaak voor het schalen van de werklast toosupport is geboren en Hallo moet toodeal Hallo problemen die ontstaan doordat ondersteunende grootschalige toepassingen in Hallo openbare cloud.

Een vDC is niet alleen Hallo toepassingsworkloads in Hallo cloud, maar ook Hallo netwerk, beveiliging, beheer en infrastructuur (bijvoorbeeld DNS- en Directory Services). Gewoonlijk biedt ook een particuliere verbinding back tooan lokale netwerk of data center. Meer werkbelastingen verplaatsen tooAzure, is het belangrijk toothink over Hallo ondersteunende infrastructuur en -objecten die in deze werkbelastingen worden geplaatst. Nadenken over de structuur van resources zorgvuldig kunt Hallo verspreiding van honderden 'werkbelasting eilanden' moeten afzonderlijk worden beheerd met onafhankelijke gegevensstroom, beveiligingsmodellen en naleving uitdagingen voorkomen.

Een virtuele Data Center is in feite een verzameling afzonderlijke maar gerelateerde entiteiten met het gemeenschappelijke ondersteunende functies, onderdelen en infrastructuur. Door uw werkbelastingen als een geïntegreerde vDC bekijkt, zult u ontdekken lagere kosten vanwege tooeconomies van schaal aan, geoptimaliseerde beveiliging via het onderdeel en gegevens centralisering, samen met eenvoudiger bewerkingen, management en compliance-audits stromen.

> [!NOTE]
> Het is belangrijk toounderstand die Hallo vDC **niet** een discrete Azure product, maar Hallo combinatie van verschillende functies en mogelijkheden te voldoen aan uw exacte vereisten. vDC is een manier nadenkt over uw workloads en het gebruik van Azure toomaximize uw resources en de mogelijkheden in Hallo cloud. Hallo virtuele domeincontroller is daarom een modulaire benadering voor het toobuild van IT-services in Azure, organisatie-rollen en verantwoordelijkheden te respecteren Hallo.

Hallo vDC kunt ondernemingen ophalen van werkbelastingen en toepassingen in Azure voor Hallo volgen scenario's:

-   Meerdere gerelateerde workloads die als host fungeert
-   Migreren van de werkbelastingen van een lokale omgeving tooAzure
-   Uitvoering van de gedeelde of gecentraliseerde beveiliging en vereisten voor toegang via werkbelastingen
-   De combinatie van DevOps en gecentraliseerd IT op de juiste wijze voor een grote onderneming

Hallo sleutel toounlock Hallo voordelen van vDC, is een gecentraliseerde topologie (hub en spaken) met een combinatie van Azure-functies: [Azure VNet][VNet], [nsg's] [ NSG], [VNet-Peering][VNetPeering], [gebruiker gedefinieerde Routes (UDR)][UDR], en Azure identiteit met [ Role Base Access Control (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>Die behoefte hebben aan een virtuele Datacenter?
Elke Azure klant die toomove meer dan een paar workloads in Azure behoeften kan profiteren van het denken over het gebruik van algemene bronnen. Afhankelijk van de magnitude hello, zelfs enkele toepassingen kunnen profiteren van Hallo patronen en onderdelen toobuild een vDC gebruikt.

Als uw organisatie een gecentraliseerde IT, het netwerk, beveiliging heeft en/of/nalevingsafdeling team, een vDC kunt u beleid punten scheiding van rechten, afdwingen en uniformiteit van algemene onderdelen tijdens het doorgeven van App-teams zo veel onderliggende hello vrijheid en het besturingselement is die geschikt zijn voor uw vereisten.

Organisaties die op zoek bent tooDevOps kunnen gebruikmaken van Hallo vDC concepten tooprovide geautoriseerd zakken van Azure-resources en zorg ervoor dat ze hebben volledige controle binnen die groep (abonnement of resourcegroep groep in een algemene abonnement), maar het Hallo-netwerk en beveiligingsgrenzen blijven compatibel zoals gedefinieerd door een gecentraliseerde beleid in een hub VNet en een resourcegroep.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Overwegingen bij het implementeren van een virtuele Data Center
Bij het ontwerpen van een vDC, zijn er enkele belangrijke problemen tooconsider:

-   Identiteit en directoryservices
-   Infrastructuur voor de beveiliging
-   Connectiviteit toohello cloud
-   Verbindingen binnen Hallo cloud

##### <a name="identity-and-directory-service"></a>*Identiteits- en Active Directory*
Identiteit en Directory services zijn een belangrijk aspect van alle gegevens draait, zowel on-premises en in de cloud Hallo. Identiteit is gerelateerde tooall aspecten van toegang en autorisatie tooservices binnen Hallo vDC. toohelp Zorg ervoor dat alleen geautoriseerde gebruikers en processen toegang tot uw Azure-Account en resources, Azure verschillende soorten referenties gebruikt voor verificatie. Het gaat hierbij om wachtwoorden (tooaccess hello Azure-account), cryptografische sleutels, digitale handtekeningen en certificaten. [*Azure multi-factor Authentication* (MFA)] [ MFA] is een extra beveiligingslaag voor toegang tot Azure-services. Azure MFA biedt geavanceerde verificatie met een bereik van eenvoudige verificatie-opties, telefoongesprek, tekstbericht of mobiele-appmelding, waardoor klanten toochoose Hallo wijze.

Een grote onderneming moet een proces voor het beheer van identiteit dat wordt beschreven Hallo beheer van afzonderlijke identiteiten, hun verificatie, autorisatie, rollen en bevoegdheden binnen of tussen verschillende Hallo vDC toodefine. Hallo doelstellingen van dit proces moet tooincrease beveiliging en productiviteit en het verlagen van kosten, uitvaltijd en herhaalde manuele taken.

Werknemers hebben vaak verschillende rollen wanneer betrokken met verschillende projecten en ondernemingen/vereist een veeleisende combinatie van services voor verschillende regel van bedrijven (LOB's). Een vDC vereist goede samenwerking tussen verschillende teams, elk met specifieke roldefinities, tooget-systemen met met goed bestuur. Hallo-matrix van verantwoordelijkheden, de toegang en de rechten kunt zeer complex zijn. Identiteitsbeheer in vDC wordt geïmplementeerd via [ *Azure Active Directory* (AAD)] [ AAD] en op rollen gebaseerde toegangsbeheer (RBAC).

Een adreslijstservice biedt een infrastructuur gedeelde informatie voor het zoeken, beheren, beheren en ordenen van dagelijkse items en netwerkbronnen. Deze resources kunnen volumes, mappen, bestanden, printers, gebruikers, groepen, apparaten en andere objecten bevatten. Elke resource op Hallo netwerk wordt beschouwd als een object door Hallo Active directory-server. Informatie over een bron wordt opgeslagen als een verzameling van kenmerken die zijn gekoppeld aan deze resource of object.

Alle Microsoft online Bedrijfsservices vertrouwen op Azure Active Directory (AAD) voor aanmelding en andere identiteit moet. Azure Active Directory is een uitgebreide en zeer beschikbare cloudoplossing voor identiteits- en toegangsbeheer die kernadreslijstservices, geavanceerd identiteitsbeheer en toegangsbeheer voor toepassingen combineert. AAD kan worden geïntegreerd met de lokale Active Directory tooenable eenmalige aanmelding voor alle cloud-gebaseerde en lokaal (on-premises) toepassingen die worden gehost. Hallo gebruikerskenmerken van lokale Active Directory kunnen automatisch gesynchroniseerde tooAAD zijn.

Één globale beheerder is niet vereist tooassign alle machtigingen in een vDC. In plaats daarvan kan elke bepaalde afdeling (of de groep van gebruikers of services in Active Directory Hallo) hebben Hallo machtigingen vereist toomanage hun eigen resources binnen een vDC. Structureren machtigingen vereist netwerktaakverdeling. Te veel machtigingen kunnen belemmeren prestaties efficiëntie, en te weinig of losse machtigingen beveiligingsrisico's kunnen verhogen. Azure op rollen gebaseerde toegangsbeheer (RBAC) helpt tooaddress dit probleem door het aanbieden van Geavanceerd toegangsbeheer voor vDC-bronnen.

##### <a name="security-infrastructure"></a>*Infrastructuur voor de beveiliging*
Beveiligingsinfrastructuur voor in de context van een vDC Hallo is hoofdzakelijk gerelateerde toohello scheiding van verkeer in Hallo vDC van specifieke virtuele-netwerksegment en hoe de Hallo vDC toocontrol inkomende en uitgaande doorloopt. Azure is gebaseerd op een architectuur met meerdere tenants waarmee wordt voorkomen onbevoegde en onbedoelde verkeer tussen implementaties dat, met behulp van virtueel netwerk (VNet) isolatie toegangsbeheerlijsten (ACL's), load balancers en IP-filters, samen met verkeer stroom beleidsregels. Netwerkadresomzetting (NAT) scheidt interne netwerkverkeer van externe verkeer.

Hello Azure-infrastructuur infrastructuur bronnen toegewezen tootenant werkbelastingen en communicatie tooand beheert van virtuele machines (VM's). Hello Azure hypervisor afgedwongen geheugen en proces scheiding tussen VM's en veilig routes netwerkverkeer tooguest OS tenants.

##### <a name="connectivity-toohello-cloud"></a>*Connectiviteit toohello cloud*
Hallo vDC moet verbinding met externe netwerken toooffer services toocustomers, partners en/of interne gebruikers. Dit betekent meestal connectiviteit niet alleen toohello Internet, maar ook tooon-premises netwerken en gegevenscentra.

Klanten kunnen hun beleid beveiliging toocontrol wat bouwen en hoe specifieke vDC gehoste services toegankelijk naar/van worden Internet via virtuele netwerkapparaten (met filteren en verkeer inspection), en aangepaste beleidsregels voor doorsturen en filteren (netwerk Hallo De gebruiker gedefinieerde Routering en Netwerkbeveiligingsgroepen).

Bedrijven moeten vaak tooconnect Copy-VDC's tooon-premises datacenters of andere bronnen. Hallo-connectiviteit tussen Azure en on-premises netwerken is daarom een aspect van cruciaal belang bij het ontwerpen van een effectieve architectuur. Bedrijven hebben twee verschillende manieren toocreate een koppeling tussen vDC en on-premises in Azure: onderweg via Internet Hallo en/of persoonlijke rechtstreekse verbindingen.

Een [ **Azure Site-naar-Site VPN** ] [ VPN] is een onderling verbonden service via Internet Hallo tussen on-premises netwerken en Hallo vDC, tot stand gebracht via beveiligde versleuteld verbindingen (IPsec/IKE-tunnels). Azure Site-naar-Site-verbinding is flexibel, snelle toocreate en vereist geen eventuele verdere inkoop, zoals alle verbindingen verbinding maken via internet Hallo.

[**ExpressRoute** ] [ ExR] is een verbinding met Azure-service waarmee u particuliere verbindingen maken tussen vDC en Hallo on-premises netwerken. ExpressRoute-verbindingen gaan niet meer dan Hallo openbare Internet en bieden betere beveiliging, betrouwbaarheid en hogere snelheden (omhoog too10 Gbps) samen met consistente latentie. ExpressRoute is zeer nuttig is voor Copy-VDC's, als ExpressRoute klanten Hallo voordelen van compliantieregels die zijn gekoppeld aan particuliere verbindingen kunnen krijgen.

ExpressRoute-verbindingen implementeren omvat bezighouden met een ExpressRoute-serviceprovider. Voor klanten die toostart snel nodig, het is vaak tooinitially gebruikt Site-naar-Site VPN-tooestablish connectiviteit tussen Hallo vDC en on-premises resources en vervolgens migreren tooExpressRoute verbinding.

##### <a name="connectivity-within-hello-cloud"></a>*Verbindingen binnen Hallo cloud*
[VNets] [ VNet] en [VNet-Peering] [ VNetPeering] zijn Hallo basic netwerkservices connectiviteit binnen een vDC. De grens van een natuurlijke van isolatie voor vDC-resources wordt gegarandeerd dat een VNet en VNet-peering kunt onderling tussen verschillende VNets binnen Hallo dezelfde Azure-regio. Beheer van netwerkverkeer binnen een VNet en tussen VNets moet toomatch een reeks beveiliging regels opgegeven met de Access Control Lists ([Netwerkbeveiligingsgroep][NSG]), [virtuele netwerkapparaten ] [ NVA], en aangepaste routeringstabellen ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Virtuele Data Center-overzicht

### <a name="topology"></a>Topologie
Hub en spaken model uitgebreide Hallo virtuele Data Center binnen één Azure-regio

[![1]][1]

Hallo-hub is Hallo centrale zone die u beheert en inspecteert inkomend en/of uitgaande verkeer tussen verschillende zones: Internet, on-premises en Hallo spaken. Hallo-hub en spoke-topologie biedt Hallo IT-afdeling een effectieve manier tooenforce beveiligingsbeleid op een centrale locatie Hallo mogelijkheden voor onjuiste configuratie en de blootstelling te verlagen.

Hallo hub bevat Hallo algemene serviceonderdelen door Hallo spaken verbruikt. Hier volgen enkele typische voorbeelden van algemene centrale services:

-   Hallo Windows Active Directory-infrastructuur (Hallo gerelateerde ADFS-service) vereist voor de verificatie van derden dat openen vanuit niet-vertrouwde netwerken voordat ophalen toegang toohello werkbelastingen in Hallo spoke
-   Een DNS-service tooresolve naamgeving voor Hallo werkbelasting in Hallo spaken, tooaccess lokale en op Hallo Internet
-   Een PKI-infrastructuur tooimplement eenmalige aanmelding op werkbelastingen
-   Datatransportbesturing (TCP/UDP) tussen hello spaken en Internet
-   Datatransportbesturing tussen Hallo spoke en on-premises
-   Indien gewenst, datatransportbesturing tussen één spoke

totale kosten beperkt Hallo vDC met behulp van Hallo gedeelde hub infrastructuur tussen meerdere spaken.

Hallo-rol van elke spoke mag toohost verschillende typen werkbelastingen. Hallo spaken biedt ook een modulaire benadering voor herhaalbare implementaties (bijvoorbeeld, ontwikkeling en tests, gebruikersacceptatietests, preproductie en productie) Hallo dezelfde werkbelastingen. Hallo spaken kunnen ook worden gebruikt toosegregate en het inschakelen van verschillende groepen binnen uw organisatie (bijvoorbeeld DevOps groepen). Het is mogelijk toodeploy een basic werkbelasting of complexe werkbelastingen van meerdere lagen met verkeer tussen lagen Hallo beheren binnen een spoke.

##### <a name="subscription-limits-and-multiple-hubs"></a>Abonnementen en meerdere hubs
Elk onderdeel, van welke aard hello, wordt in Azure worden geïmplementeerd in een Azure-abonnement. Hallo isolatie van Azure-componenten in verschillende Azure-abonnementen voldoen aan de vereisten voor Hallo van verschillende LOB's, zoals het gedifferentieerde niveaus van toegang en autorisatie in te stellen.

Een enkele vDC kunt opschalen toolarge aantal spaken, hoewel net als bij elke IT-systeem, zijn er beperkingen voor platforms gelden. Hallo hub implementatie is gebonden tooa specifieke Azure-abonnement, met beperkingen en limieten (bijvoorbeeld een maximum aantal VNet-peerings - Zie [Azure-abonnement en Servicelimieten, quota's en beperkingen] [ Limits] voor meer informatie). In gevallen waar limieten mogelijk een probleem Hallo architectuur kan opschalen verder omhoog door Hallo model van een cluster met één hub-spaken tooa van hub en spaken uit te breiden. Meerdere hubs in een of meer Azure-regio's kunnen ook worden verbonden met Express Route of site-naar-site VPN.

[![2]][2]

Hallo introductie van meerdere hubs verhoogt Hallo kosten en management inspanning van Hallo systeem en alleen gerechtvaardigd zijn door schaalbaarheid (voorbeelden: systeemlimieten of redundantie) en regionale replicatie (voorbeelden: eindgebruikers prestaties of herstel na noodgevallen). In scenario's met meerdere hubs vereisen, moeten alle Hallo hubs toooffer Hallo dezelfde van services voor operationele eenvoudig set streven.

##### <a name="interconnection-between-spokes"></a>Koppeling tussen spaken
Het is mogelijk tooimplement complexe met meerdere lagen werkbelastingen binnen een enkele spoke. Configuraties met meerdere lagen kunnen worden geïmplementeerd met behulp van subnetten (één voor elke laag) in hetzelfde VNet en filteren Hallo loopt met nsg's Hallo.

Op Hallo daarentegen, een architect wil toodeploy een werkbelasting met meerdere lagen tussen meerdere VNets. Met behulp van VNet-peering, spaken verbinding kunnen maken tooother spaken in Hallo dezelfde hub of andere hubs. Een typisch voorbeeld van dit scenario is Hallo-geval waar verwerking toepassingsservers zich bevindt in een spoke (VNet) tijdens het Hallo-database in een andere spoke (VNet) is geïmplementeerd. In dit geval is eenvoudig toointerconnect Hallo spaken met VNet-peering en daardoor wilt voorkomen dat bij doorvoer over Hallo hub. Een zorgvuldige beoordeling van de architectuur en beveiliging moet worden uitgevoerd tooensure die belangrijke beveiligings- of controle-punten dat mag alleen bestaan in de hub Hallo Hallo hub omzeilen niet overslaan.

[![3]][3]

Spaken kunnen ook worden onderling verbonden tooa spoke die als een hub fungeert. Deze methode maakt u een hiërarchie met twee niveaus: Hallo spoke in Hallo hoger niveau (niveau 0) worden Hallo hub van lagere spaken (niveau 1) van Hallo-hiërarchie. Hallo spaken van vDC moeten tooforward Hallo verkeer toohello centrale hub tooreach toohello on-premises netwerk of internet. Een architectuur met twee niveaus van hub introduceert complexe routering dat Hallo voordelen van een eenvoudige hub spoke relatie verwijdert.

Hoewel Azure complexe topologieën toestaat, is een kernprincipes Hallo Hallo vDC concept herhaalbaarheid en eenvoud. toominimize management inspanning, Hallo eenvoudige hub spoke ontwerp is Hallo vDC referentiearchitectuur aanbevolen.

### <a name="components"></a>Onderdelen
Een virtuele Data Center bestaat uit vier elementaire onderdeeltypen: **infrastructuur**, **perimeternetwerken**, **werkbelastingen**, en **bewaking**.

Elk onderdeeltype bestaat uit verschillende Azure-functies en bronnen. Uw vDC is afhankelijk van exemplaren van typen met meerdere onderdelen en meerdere variaties van Hallo dezelfde onderdeeltype. Mogelijk hebt u bijvoorbeeld veel exemplaren van de werkbelasting afwijken, logisch gescheiden, waarbij verschillende toepassingen. Gebruik van deze typen verschillende onderdelen en exemplaren tooultimately Hallo vDC bouwen.

[![4]][4]

Hallo bevat voorgaande architectuur op hoog niveau van een vDC verschillende onderdelen die worden gebruikt in verschillende zones van Hallo hub spaken topologie. Hallo diagram ziet u onderdelen van de infrastructuur in verschillende onderdelen van Hallo-architectuur.

Als een goede gewoonte (voor een lokale DC of vDC) toegang moet rechten en bevoegdheden op basis van een groep. Omgaan met groepen, kunnen in plaats van afzonderlijke gebruikers toegangsbeleid consistent van binnen teams en hulpmiddelen in voor het minimaliseren van fouten in de configuratie. Toe te wijzen en gebruikers tooand verwijderen uit groepen helpt Hallo bevoegdheden van een specifieke gebruiker up-to-date te houden.

Elke rolgroep moet een uniek voorvoegsel hebben voor hun namen zodat u eenvoudig tooidentify welke groep gekoppeld aan welke werkbelasting is. Bijvoorbeeld, een werkbelasting die als host fungeert voor een verificatieservice wellicht groepen met de naam *AuthServiceNetOps, AuthServiceSecOps AuthServiceDevOps en AuthServiceInfraOps.* Op dezelfde manier geldt voor gecentraliseerde rollen of functies niet gerelateerde tooa bepaalde service, kan worden voorafgegaan door "Corp" *CorpNetOps* bijvoorbeeld.

Veel organisaties gebruiken een variant van Hallo groepen tooprovide een belangrijke verdeling van rollen te volgen:

-   Hallo *centrale IT-groep (Corp)* heeft Hallo eigendom rechten toocontrol infrastructuur hebben (zoals netwerk- en beveiliging) onderdelen, en daarom moet toohave Hallo rol van Inzender op Hallo abonnement (en beheer hebben over Hallo hub) en Inzender-rechten op Hallo spaken netwerk. Deze verantwoordelijkheid management tussen meerdere teams zoals; grote organisatie vaak opsplitsen een groep netwerkbewerkingen (CorpNetOps) (met exclusieve toegang is geactiveerd) en een groep beveiligingsbewerkingen (CorpSecOps) (die verantwoordelijk is voor de firewall-en beveiligingsbeleid). In dit specifieke geval moeten twee verschillende groepen toobe gemaakt voor de toewijzing van deze aangepaste rollen.
-   Hallo *dev & testgroep (AppDevOps)* heeft Hallo verantwoordelijkheid toodeploy werkbelastingen (Apps of Services). Deze groep heeft Hallo van Virtual Machine Contributor voor IaaS-implementaties en/of een of meer PaaS-Inzender-rollen (Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer][Roles]). Eventueel Hallo dev & testteam wellicht toohave zichtbaarheid van beveiligingsbeleid (nsg's) en routeringsbeleid (UDR) in de hub hello of een specifieke spoke. Daarom in toevoeging toohello rollen van inzender voor werkbelastingen moet deze groep tevens Hallo-rol van netwerk-lezer.
-   Hallo *bewerking en onderhoud groep (CorpInfraOps of AppInfraOps)* Hallo verantwoordelijkheid voor het beheer van de werkbelastingen in productie hebben. Deze groep moet toobe abonnement bijdrager van werkbelastingen in een productie-abonnementen. Sommige organisaties mogelijk ook evalueren of ze nodig hebben een aanvullende escalatie team ondersteuningsgroep met Hallo-rol van Inzender abonnement in productie en in Hallo centrale hub abonnement, in volgorde toofix potentiële problemen in productie Hallo -omgeving.

Er is een vDC gestructureerd zodat groepen die zijn gemaakt voor Hallo centrale IT-groepen beheren Hallo hub bijbehorende groepen op Hallo werkbelasting niveau hebben. Bovendien zou toomanaging hub alleen Hallo centrale IT resourcegroepen kunnen toocontrol externe toegang en op het hoogste niveau machtigingen op Hallo-abonnement. Werkbelastinggroepen zich echter kunnen toocontrol resources en de machtigingen van hun VNet onafhankelijk op centrale IT-afdeling.

Hallo vDC behoeften toobe gepartitioneerd toosecurely host meerdere projecten in verschillende regel van bedrijven (LOB's). Alle projecten vereist verschillende geïsoleerde omgevingen (Dev, UAT, productie). Afzonderlijke Azure-abonnementen voor elk van deze omgevingen bieden natuurlijke isolatie.

[![5]][5]

Hallo toont voorgaande diagram Hallo relatie tussen een organisatie projecten, gebruikers, groepen en Hallo omgevingen waarin hello Azure onderdelen worden ingezet.

Normaal gesproken in IT, een omgeving (of laag) is een systeem waarin meerdere toepassingen worden geïmplementeerd en uitgevoerd. Grote ondernemingen gebruiken een ontwikkelomgeving (waar wijzigingen oorspronkelijk en getest) en een productie-omgeving (wat eindgebruikers gebruiken). Deze omgevingen worden gescheiden, vaak met verschillende faseringsomgevingen tussen deze tooallow gefaseerde implementatie (implementatie), testen en terugdraaien in geval van problemen. Implementatie-architecturen aanzienlijk verschillen, maar meestal Hallo basisproces van op ontwikkeling (DEV) begint en eindigt bij productie (PROD) nog steeds wordt gevolgd.

Een algemene architectuur voor deze typen omgevingen met meerdere lagen bestaat uit DevOps (ontwikkelen en testen), UAT (fasering) en productieomgevingen. Organisaties kunnen gebruikmaken van één of meerdere Azure AD-tenants toodefine toegang en machtigingen toothese omgevingen. Hallo vorige diagram ziet u een aanvraag wanneer twee andere Azure AD-tenants worden gebruikt: één voor DevOps en UAT en Hallo andere is uitsluitend bedoeld is voor productie.

Hallo aanwezigheid van andere Azure AD-tenants dwingt Hallo scheiding tussen omgevingen. Hallo van dezelfde groep gebruikers (als u bijvoorbeeld centrale IT-afdeling) moet wijzigen met behulp van een andere URI tooaccess een andere AD-tenant tooauthenticate Hallo rollen of machtigingen van zowel Hallo DevOps of productieomgevingen van een project. Hallo aanwezigheid van andere gebruiker verificatie tooaccess verschillende omgevingen vermindert mogelijke storingen en andere problemen veroorzaakt door menselijke fouten.

#### <a name="component-type-infrastructure"></a>Onderdeeltype: infrastructuur
Dit onderdeel is waar de meeste Hallo ondersteunende infrastructuur zich bevindt. Het is ook waar uw centrale IT, beveiliging en/of naleving teams besteden aan de meeste van de tijd.

[![6]][6]

Onderdelen van de infrastructuur bieden een koppeling tussen de verschillende onderdelen van een vDC Hallo en aanwezig zijn in zowel Hallo hub en Hallo spaken. Hallo verantwoordelijkheid voor het beheren en onderhouden van Hallo infrastructuuronderdelen is doorgaans toegewezen toohello centrale IT en/of beveiligingsteam.

Een van de primaire taken Hallo Hallo IT-team voor infrastructuur is tooguarantee Hallo consistentie van IP-adres schema's in de onderneming Hallo. Hallo persoonlijke IP-adres toegewezen ruimte toohello vDC moet toobe consistent en niet overlappen met particuliere IP-adressen toegewezen op uw on-premises netwerken.

Terwijl de NAT voor Hallo on-premises routers van de rand of in Azure omgevingen IP-adresconflicten kunnen voorkomen, wordt er problemen tooyour infrastructuuronderdelen toegevoegd. Eenvoud van management is een van de belangrijkste doelstellingen Hallo van vDC, zodat u met behulp van NAT toohandle IP-problemen is geen aanbevolen oplossing.

Onderdelen van de infrastructuur bevatten Hallo functionaliteit te volgen:

-   [**Identiteits-en**][AAD]. Toegang tooevery brontype in Azure wordt beheerd door een identiteit die is opgeslagen in Active Directory. Hallo directory service winkels niet alleen lijst met gebruikers Hallo maar ook Hallo toegang rechten tooresources in een specifieke Azure-abonnement. Deze services alleen in de cloud kunnen bestaan of ze kunnen worden gesynchroniseerd met de on-premises identiteits opgeslagen in Active Directory.
-   [**Virtueel netwerk**][VPN]. Virtuele netwerken zijn een van de belangrijkste onderdelen van een vDC en toocreate een grens van de isolatie van verkeer op Hallo Azure-platform inschakelen. Een virtueel netwerk bestaat uit één of meerdere virtuele netwerksegmenten, elk met een bepaald IP-netwerk voorvoegsel (subnet). Hallo virtueel netwerk definieert een interne perimeter-gebied waar IaaS virtuele machines en PaaS-services besloten communicatie kunnen maken. Virtuele machines (en PaaS-services) in een virtueel netwerk kan niet communiceren rechtstreeks tooVMs (en PaaS-services) in een ander virtueel netwerk, zelfs als beide virtuele netwerken worden gemaakt met dezelfde klant onder Hallo Hallo hetzelfde abonnement. Isolatie is een kritieke eigenschap die ervoor zorgt dat de klant VM's en communicatie blijft persoonlijke binnen een virtueel netwerk.
-   [**UDR**][UDR]. Verkeer in een virtueel netwerk wordt doorgestuurd standaard op basis van de routeringstabel Hallo-systeem. Een Route voor het definiëren van de gebruiker is een aangepaste routeringstabel dat netwerkbeheerders kunnen tooone of meer subnetten toooverwrite Hallo gedrag van Hallo system-routeringstabel koppelen en een communicatiepad binnen een virtueel netwerk opgeven. Hallo aanwezigheid van udr's zorgt ervoor dat uitgaande verkeer van Hallo spoke doorvoer door specifieke aangepaste VM's en/of virtuele netwerkapparaten en netwerktaakverdelers aanwezig in Hallo hub en Hallo spaken.
-   [**NSG**][NSG]. Een Netwerkbeveiligingsgroep is een lijst met beveiligingsregels voor verbindingen die fungeren als verkeer filteren op IP-bronnen, doel-IP-protocollen, bron-IP-poorten en doel-IP-poorten. Hallo NSG mag toegepaste tooa het subnet van een virtuele NIC-kaart die is gekoppeld aan een Azure VM of beide. Hallo nsg's zijn essentieel tooimplement een juiste datatransportbesturing in Hallo hub en Hallo spaken. Hallo-niveau van beveiliging die worden geboden door Hallo NSG is een functie van welke poorten u opent, en wat is het doel. Klanten moeten aanvullende VM filters met een host gebaseerde firewall zoals IPtables toepassen of Hallo Windows Firewall.
-   **DNS**. Hallo-naamomzetting van resources in Hallo VNets van een vDC is beschikbaar via DNS. Hallo-bereik van naamomzetting van Hallo standaard DNS-is beperkt toohello VNet. Normaal gesproken een aangepaste DNS-service moet toobe geïmplementeerd in Hallo hub als onderdeel van algemene services, maar de belangrijkste gebruikers Hallo van DNS-services zich bevinden in Hallo spoke. Indien nodig, kunnen klanten een hiërarchische structuur voor DNS-kunnen maken met de overdracht van DNS-zones toohello spaken.
-   [** Abonnement] [ SubMgmt] en [resourcegroep Management][RGMgmt]**. Een abonnement definieert een natuurlijke grens toocreate meerdere groepen van resources in Azure. Resources in een abonnement worden samen in logische containers met de naam resourcegroepen worden samengesteld. Hallo resourcegroep vertegenwoordigt een logische groep tooorganize Hallo resources van een vDC.
-   [**RBAC**][RBAC]. Via RBAC is het mogelijk toomap organisatierol samen met rechten tooaccess specifieke Azure-resources, zodat u toorestrict gebruikers tooonly een bepaalde subset van acties. Met RBAC, kunt u toegang verlenen door toe te wijzen Hallo geschikte rol toousers, groepen en toepassingen binnen relevante Hallo-bereik. Hallo-bereik van een roltoewijzing kan dit een Azure-abonnement, een resourcegroep of één resource. RBAC kunt overname van machtigingen. Een rol die is toegewezen aan een bovenliggend bereik verleent toegang ook toohello onderliggende items erin opgenomen. Met RBAC kunt u taken scheiden en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk. Bijvoorbeeld, gebruik RBAC toolet één werknemer virtuele machines in een abonnement beheren terwijl een andere SQL-databases kan beheren binnen Hallo hetzelfde abonnement.
-   [**VNet-Peering**][VNetPeering]. Hallo fundamenteel onderdeel gebruikt toocreate Hallo infrastructuur van een vDC is VNet-Peering, een mechanisme dat verbinding twee virtuele netwerken (vnet's) in Hallo maakt dezelfde regio via Hallo-netwerk van hello Azure-Datacenter.

#### <a name="component-type-perimeter-networks"></a>Onderdeeltype: Perimeternetwerken
[Perimeternetwerk] [ DMZ] componenten (ook wel een DMZ-netwerk), kunt u tooprovide netwerkverbinding tussen uw on-premises of fysieke datacenternetwerken, samen met eventuele tooand connectiviteit van Hallo Internet. Het is ook waar uw netwerk- en teams waarschijnlijk te besteden aan de meeste van de tijd.

Inkomende pakketten moeten stromen Hallo beveiligingsapparaten in Hallo hub, zoals firewall Hallo-id's en IP-Adressen, voordat het Hallo-back-end-servers in Hallo spaken heeft bereikt. Internet-gebonden pakketten van Hallo werkbelastingen moeten ook door Hallo beveiligingsapparaten in het perimeternetwerk Hallo voor het afdwingen van beleid, controle en controledoeleinden voordat deze uit het Hallo-netwerk stromen.

Perimeter-netwerkonderdelen bieden Hallo volgende kenmerken:

-   [Virtuele netwerken][VNet], [UDR][UDR], [NSG][NSG]
-   [Virtueel netwerkapparaat][NVA]
-   [De Load Balancer][ALB]
-   [Toepassingsgateway][AppGW] / [WAF][WAF]
-   [Openbare IP-adressen][PIP]

Normaal gesproken Hallo centrale IT en beveiliging teams verantwoordelijkheid voor de Vereistedefinitie en bewerkingen van Hallo perimeternetwerken hebben.

[![7]][7]

Hallo voorgaande diagram geeft Hallo afdwinging van twee verbindingen met toohello toegang tot internet en een on-premises netwerk, beide residente in Hallo-hub. In een enkel hub kunt Hallo perimeter netwerk toointernet toosupport grote aantallen LOB's, met behulp van meerdere farms van Web Application Firewalls (WAFs) en/of firewalls opschalen.

[**Virtuele netwerken** ] [ VNet] Hallo hub wordt gewoonlijk samengesteld op een VNet met meerdere subnetten toohost Hallo ander type van services voor het filteren en bekijken tooor verkeer van internet via NVAs, WAFs, Hallo en Gateways van Azure-toepassing.

[**UDR** ] [ UDR] UDR met behulp van klanten kunnen implementeren firewalls, -id's / IP-Adressen en andere virtuele apparaten en doorsturen van netwerkverkeer via deze beveiligingsapparaten voor beveiliging grens wordt afgedwongen, controle en controle. Udr's kunnen worden gemaakt in beide Hallo hub en Hallo spaken tooguarantee die verkeer passages via Hallo specifieke aangepaste virtuele machines, virtuele netwerkapparaten en netwerktaakverdelers door Hallo vDC gebruikt. tooguarantee die verkeer gegenereerd op basis van virtuele machines in Hallo spoke onderweg toohello juiste virtuele apparaten woont, een UDR moet toobe ingesteld in Hallo subnetten van Hallo spoke door in te stellen Hallo front-end-IP-adres van Hallo interne load balancer Hallo volgende hop. Hallo interne load balancer distribueert Hallo interne verkeer toohello virtuele apparaten (groep load balancer back-end).

[![8]][8]

[**Virtuele apparaten** ] [ NVA] In Hallo-hub Hallo perimeternetwerk met toegang toohello internet normaal gesproken wordt beheerd via een farm met firewalls en/of Web Application Firewalls (WAFs).

Andere LOB's gebruiken doorgaans veel webtoepassingen en deze toepassingen vaak toosuffer van verschillende beveiligingsproblemen en potentiële aanvallen. Web Applications Firewalls zijn dat een speciale vorm van het product toodetect aanvallen tegen de webtoepassingen (HTTP/HTTPS) gebruikt in de diepte van meer dan een algemene firewall. Vergeleken met traditie firewall-technologie, hebben WAFs een set van specifieke functies tooprotect interne webservers tegen bedreigingen.

Een firewall-farm is groep firewalls werkt in combinatie onder Hallo dezelfde algemene beheer met een reeks beveiliging regels tooprotect Hallo werkbelastingen in Hallo spaken en beheer toegang tooon-premises netwerken gehost. Een firewall-farm heeft minder gespecialiseerde software vergeleken met een WAF, maar heeft een algemene toepassing toofilter bereik en inspecteren van elk type verkeer en uitgangsclaims. Firewall-farms worden normaal gesproken geïmplementeerd in Azure via virtuele netwerkapparaten (NVAs) die beschikbaar in hello Azure marketplace zijn.

Het verdient aanbeveling toouse één verzameling NVAs voor verkeer op Hallo Internet, en één voor verkeer van oorsprong on-premises. Met behulp van slechts één set met NVAs voor beide vormt een beveiligingsrisico, aangezien deze geen beveiliging perimeter tussen twee sets Hallo van netwerkverkeer biedt. Met afzonderlijke NVAs vermindert Hallo complexiteit van het controleren van de beveiligingsregels voor verbindingen en is dit duidelijk welke regels toowhich binnenkomende netwerkaanvraag overeenkomen.

Meest grote ondernemingen beheren meerdere domeinen. Azure DNS kan worden gebruikt toohost Hallo DNS-records voor een bepaald domein. Als voorbeeld kan Hallo virtueel IP-adres (VIP) van hello Azure externe load balancer (of Hallo WAFs) worden geregistreerd in Hallo A-record van een Azure DNS-record.

[**Azure Load Balancer** ] [ ALB] Azure load balancer biedt een hoge beschikbaarheid laag 4 (TCP, UDP)-service, die binnenkomend verkeer over service-exemplaren die zijn gedefinieerd in een set met gelijke taakverdeling kunt distribueren. Verkeer wordt verzonden toohello load balancer van front-eindpunten (openbare IP-eindpunten of persoonlijke IP-eindpunten) kan worden gedistribueerd met of zonder address translation tooa reeks backend-IP-adresgroep (voorbeelden wordt; Virtuele netwerkapparaten of VM's).

Azure Load Balancer kunt probe Hallo health Hallo verschillende exemplaren van server ook en wanneer een test toorespond Hallo load balancer reageert verkeer toohello slecht exemplaar verzenden is mislukt. In een vDC hebben we Hallo aanwezigheid van een externe load balancer in Hallo hub (bijvoorbeeld saldo Hallo verkeer tooNVAs) en in Hallo spaken (tooperform taken zoals het verkeer tussen verschillende virtuele machines van een toepassing met meerdere lagen balancing).

[**Toepassingsgateway** ] [ AppGW] Microsoft Azure Application Gateway is een toegewezen virtueel apparaat toepassing levering controller (ADC) bieden als een service biedt u verschillende laag 7 taakverdeling mogelijkheden voor uw toepassing. Hiermee kunt u toooptimize web farm productiviteit door het offloaden van CPU intensief SSL-beëindiging toohello toepassingsgateway. Het biedt ook andere laag 7 routering mogelijkheden met inbegrip van round robin-distributie van inkomend verkeer, sessie cookies gebaseerde affiniteit URL-pad gebaseerde routering en Hallo mogelijkheid toohost meerdere websites achter een enkele Gateway van de toepassing. Web application firewall (WAF) is ook beschikbaar als onderdeel van de toepassingsgateway Hallo WAF SKU. De SKU biedt bescherming tooweb toepassingen van algemene web beveiligingsproblemen en aanvallen. Application Gateway kan worden geconfigureerd als op internet gerichte gateway, interne enige gateway of een combinatie van beide. 

[**Openbare IP-adressen** ] [ PIP] sommige Azure-functies inschakelen u tooassociate service-eindpunten tooa openbaar IP-adres waarmee tooyour resource toobe via internet Hallo. Dit eindpunt maakt gebruik van NAT (Network Address Translation) tooroute verkeer toohello interne adres en poort op Hallo virtuele Azure-netwerk. Dit pad is Hallo primaire manier voor het externe verkeer toopass in Hallo virtueel netwerk. Hallo openbare IP-adressen kunnen geconfigureerde toodetermine welk verkeer wordt doorgegeven in, en hoe en waar deze wordt omgezet in het virtuele netwerk toohello.

#### <a name="component-type-monitoring"></a>Onderdeeltype: bewaking
Bewaking componenten bieden zichtbaarheid en waarschuwingen van alle andere typen onderdelen Hallo. Alle teams moeten hebben toegang toomonitoring voor Hallo-onderdelen en services die toegang hebben tot. Als u een gecentraliseerde help helpdesk of de operations-teams hebt, moet ze toohave geïntegreerd toegang toohello gegevens van deze onderdelen.

Azure biedt verschillende soorten logboekregistratie en controle van services tootrack Hallo gedrag van Azure gehoste bronnen. Beheer en controle van workloads in Azure is gebaseerde logboekgegevens niet alleen op het verzamelen, maar ook Hallo mogelijkheid tootrigger acties op basis van specifieke gemelde gebeurtenissen.

Er zijn twee belangrijke gebeurtenistypen Logboeken in Azure:

-   [**Activiteitenlogboeken** ] [ ActLog] (ook als 'Operationele logboek' genoemd) bieden inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in hello Azure-abonnement. Deze logboeken rapport Hallo besturingselement vlak gebeurtenissen voor uw abonnementen. Elke Azure-resource produceert controlelogboeken.

-   [**Azure diagnostische logboeken** ] [ DiagLog] logboeken die worden gegenereerd door een resource die uitgebreide, regelmatig gegevens over Hallo-bewerking van de bron zijn. Hallo-inhoud van deze logboeken varieert per resourcetype.

[![9]][9]

In een vDC is zeer belangrijk tootrack hello nsg's Logboeken, met name deze informatie:

-   [**Gebeurtenislogboeken**][NSGLog]: bevat informatie over welke NSG-regels zijn toegepaste tooVMs en de exemplaar-functies op basis van MAC-adres.
-   [**Logboeken teller**][NSGLog]: houdt het aantal keren dat elke NSG regel is uitgevoerd toodeny of verkeer toestaan.

Alle logboeken kunnen worden opgeslagen in Azure Storage-Accounts voor controle, statische analyses of back-updoeleinden. Wanneer het Hallo-logboeken worden opgeslagen in Azure storage-account, klanten verschillende typen kunnen gebruiken van frameworks tooretrieve, voorbereiding, analyseren en visualiseren van deze gegevens tooreport Hallo status en gezondheid van cloudresources.

Grote ondernemingen moeten al hebt aangeschaft een standaard framework voor bewaking van on-premises systemen en kan worden uitgebreid framework toointegrate logboeken die worden gegenereerd door de cloudimplementaties. Voor organisaties die willen tookeep alle Hallo logboekregistratie in de cloud Hallo, [Microsoft Operations Management Suite (OMS)] [ OMS] is een uitstekende keuze. Aangezien OMS wordt geïmplementeerd als een cloudservice, kunt u er al snel mee aan de slag, en dat met minimale investeringen in infrastructuurservices. OMS kan ook worden geïntegreerd met System Center-onderdelen, zoals System Center Operations Manager tooextend uw bestaande investeringen in de management in Hallo cloud.

OMS Log analytics is een onderdeel van Hallo OMS framework toohelp verzamelen, correleer, zoeken en handelen in logboek-en prestatiegegevens die worden gegenereerd door de besturingssystemen, toepassingen, infrastructuur cloud onderdelen. Dit biedt klanten realtime operationeel inzicht geïntegreerd zoeken en aangepaste dashboards tooanalyze alle Hallo records met voor alle werkbelastingen in een vDC.

#### <a name="component-type-workloads"></a>Onderdeeltype: werkbelastingen
Onderdelen van de werkbelasting zijn waarin de werkelijke toepassingen en services zich bevinden. Het is ook waar ontwikkelteams toepassing te besteden aan de meeste van de tijd.

Hallo werkbelasting mogelijkheden zijn echt eindeloze. Hallo volgen slechts enkele Hallo mogelijke werkbelasting typen:

**Interne LOB-toepassingen**

Line-of-business-toepassingen zijn computer toepassingen kritieke toohello lopende bewerking van een onderneming. LOB-toepassingen hebben een aantal gemeenschappelijke kenmerken:

-   **Interactieve**. LOB-toepassingen, zijn interactief aard: gegevens worden ingevoerd en resultaat/rapporten worden geretourneerd.
-   **Gegevensgestuurde**. LOB-toepassingen zijn intensieve met regelmatig toegang toohello databases of andere opslag van gegevens.
-   **Geïntegreerde**. LOB-toepassingen aanbieding integratie met andere systemen binnen of buiten de organisatie Hallo.

**Klantgerichte websites (Internet of een intern facing)** de meeste toepassingen die interactie met Internet Hallo hebben websites zijn. Azure biedt Hallo mogelijkheid toorun een website op een IaaS-VM of vanuit een [Azure Web Apps] [ WebApps] site (PaaS). Azure Web Apps ondersteuning voor integratie met VNets die de implementatie van de Hallo Hallo Web-Apps in Hallo spoke van een vDC toestaan. Hallo VNET integratie, u hoeft niet tooexpose een Internet-eindpunt voor uw toepassingen maar kunt gebruiken om Hallo resources persoonlijke internet-routeerbare adresruimte van uw persoonlijke VNet in plaats daarvan.

**BIG gegevensanalyse** wanneer gegevens tooscale up tooa zeer grote volumes moeten, databases kunnen niet omhoog schalen goed. Hadoop-technologie biedt een systeem toorun gedistribueerde query's parallel op een groot aantal knooppunten. Klanten hebben Hallo optie toorun gegevens werkbelastingen in IaaS VM's of PaaS ([HDInsight][HDI]). HDInsight kunnen ondersteunt implementeren in een VNet op basis van locatie, geïmplementeerde tooa cluster in een spoke van Hallo vDC.

**Gebeurtenissen en berichten**
[Azure Event Hubs] [ EventHubs] is een verwerkingsservice voor grote hoeveelheden telemetrie opname-service die worden verzameld, transformeert en miljoenen gebeurtenissen worden opgeslagen. Als een gedistribueerde streaming platform, lage latentie en configureerbare tijd bewaren, zodat u tooingest enorme hoeveelheden telemetrie in Azure heeft en die gegevens lezen uit meerdere toepassingen. Met Event Hubs, kan één stream realtime en op basis van batch pijplijnen ondersteunen.

Een uiterst betrouwbare cloud messaging-service tussen toepassingen en services, kunnen worden geïmplementeerd via [Azure Service Bus] [ ServiceBus] dat aanbiedingen asynchrone brokered messaging tussen client en server, samen met gestructureerd first in first out (FIFO) messaging en publiceren/abonneren mogelijkheden.

[![10]][10]

### <a name="multiple-vdc"></a>Meerdere vDC
In dit artikel is tot nu toe gericht op een enkele vDC, waarin de basisonderdelen van Hallo en architectuur tooa robuuste vDC bijdragen. Azure-functies zoals Azure load balancer, NVAs, beschikbaarheidssets-schaalsets, samen met andere mechanismen bijdragen tooa systeem waarmee u toobuild effen SLA niveaus in uw productie-services.

Echter een enkel vDC wordt gehost binnen één regio en is kwetsbaar toomajor storing die invloed kan zijn op de hele regio. Klanten die tooachieve wilt hoge Sla's moeten tooprotect Hallo services via implementaties van Hallo hetzelfde in twee (of meer) Copy-VDC's project, geplaatst in verschillende regio's.

In aanvulling tooSLA weergegeven zijn er enkele algemene scenario's waarin het implementeren van meerdere Copy-VDC's zinvol:

-   Regionale/Global aanwezigheid
-   Noodherstel
-   Mechanisme toodivert verkeer tussen DC

#### <a name="regionalglobal-presence"></a>Regionale/Global aanwezigheid
Azure-datacenters zijn aanwezig in verschillende regio's over de hele wereld. Als u meerdere Azure-datacenters, klanten nodig hebben tooconsider twee factoren: geografische afstanden en latentie. Klanten moeten tooevaluate Hallo geografische afstand tussen Hallo Copy-VDC's en Hallo afstand tussen Hallo vDC en eindgebruikers hello, toooffer Hallo beste gebruikerservaring.

Hello Azure-regio waar Copy-VDC's worden gehost moet ook tooconform met wettelijke vereisten die zijn ingesteld door een rechtsgebied, waaronder uw organisatie werkt.

#### <a name="disaster-recovery"></a>Noodherstel
Hallo-implementatie van een noodherstelplan is sterk verwante toohello type werkbelasting betrokken en Hallo mogelijkheid toosynchronize Hallo werkbelasting status tussen verschillende Copy-VDC's. De meeste klanten wilt in het ideale geval toosynchronize toepassingsgegevens tussen implementaties die worden uitgevoerd in twee verschillende Copy-VDC's tooimplement een snelle failover-mechanisme. De meeste toepassingen gevoelige toolatency zijn en die kan ertoe leiden dat mogelijke time-outs en vertraging in de gegevenssynchronisatie.

Synchronisatie of heartbeat-bewaking van toepassingen in andere Copy-VDC's moet communicatie ertussen. Twee Copy-VDC's in verschillende regio's kunnen worden verbonden via:

-   ExpressRoute privépeering wanneer Hallo vDC-hubs verbonden toohello zijn hetzelfde ExpressRoute-circuit
-   meerdere ExpressRoute-circuits die zijn verbonden via uw bedrijfsnetwerken en uw mesh vDC verbonden toohello ExpressRoute-circuits
-   Site-naar-Site VPN-verbindingen tussen uw vDC-hubs in elke Azure-regio

Hallo ExpressRoute-verbinding is meestal Hallo voorkeurs-mechanisme vanwege de hogere bandbreedte en consistente latentie wanneer bij doorvoer over Hallo backbone van Microsoft.

Er is geen toovalidate magische recept van een toepassing die zijn gedistribueerd tussen twee (of meer) andere Copy-VDC's zich in verschillende regio's. Klanten kwalificatie tests tooverify Hallo netwerklatentie en bandbreedte van het Hallo-verbindingen en het doel moeten uitvoeren of synchrone of asynchrone replicatie geschikt is en welke Hallo optimale beoogde hersteltijd (RTO) kan gelden voor uw werkbelastingen.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Mechanisme toodivert verkeer tussen DC
Een effectieve techniek toodivert Hallo verkeer binnenkomende in één DC tooanother is gebaseerd op DNS. [Azure Traffic Manager] [ TM] gebruikt Hallo Domain Name System (DNS) mechanisme toodirect Hallo eindgebruiker verkeer toohello meest geschikte openbaar eindpunt in een specifieke vDC. Via tests Traffic Manager controleert regelmatig de servicestatus Hallo van openbare eindpunten in verschillende Copy-VDC's en in geval van storing van de eindpunten wordt gerouteerd automatisch toohello secundaire vDC.

Traffic Manager werkt op Azure openbare eindpunten en kan worden gebruikt, bijvoorbeeld toocontrol/omleiden verkeer tooAzure VM's en Web-Apps in Hallo vDC nodig. Traffic Manager is tegen zelfs in Hallo vlak van het mislukken van een volledige Azure-regio en Hallo distributie van gebruikersverkeer voor service-eindpunten in verschillende Copy-VDC's op basis van verschillende criteria beheren (bijvoorbeeld een storing van een service in een specifieke vDC of selecteren Hallo vDC met Hallo laagste netwerklatentie voor Hallo client).

### <a name="conclusion"></a>Conclusie
Hallo virtuele Data Center is een benadering toodata center migratie naar Hallo cloud die gebruikmaakt van een combinatie van functies en mogelijkheden toocreate een schaalbare architectuur in Azure die gebruik van cloud-bronnen, maximaliseert de kosten te verlagen en vereenvoudigen van systeem toezicht. Hallo vDC concept is gebaseerd op een hub spaken-topologie biedt algemene gedeelde services in Hallo hub en specifieke toepassingen/werkbelastingen in Hallo spaken toestaan. Een vDC komt overeen met de Hallo-structuur van het bedrijf rollen, waarbij verschillende afdelingen (centrale IT-afdeling, DevOps, bewerking en onderhoud) samen, elk met een specifieke lijst met functies en rechten werken. Een vDC voldoet aan de vereisten voor de migratie van een 'Lift-en Shift' hello, maar ook toonative cloudimplementaties biedt veel voordelen.

## <a name="references"></a>Verwijzingen
Hallo volgende kenmerken zijn in dit document besproken. Klik op Hallo koppelingen toolearn meer.

| | | |
|-|-|-|
|Network-functies|Taakverdeling|Connectiviteit|
|[Virtuele netwerken in Azure][VNet]</br>[Netwerkbeveiligingsgroepen][NSG]</br>[NSG-Logboeken][NSGLog]</br>[De gebruiker gedefinieerde routering][UDR]</br>[Virtuele netwerkapparaten][NVA]</br>[Openbare IP-adressen][PIP]|[Azure Load Balancer (N3)][ALB]</br>[Toepassingsgateway (N7)][AppGW]</br>[Web Application Firewall][WAF]</br>[Met Azure Traffic Manager][TM] |[VNet-Peering][VNetPeering]</br>[Virtueel particulier netwerk][VPN]</br>[ExpressRoute][ExR]
|Identiteit</br>|Bewaking</br>|Beste praktijken</br>|
|[Azure Active Directory][AAD]</br>[Multi-factor Authentication][MFA]</br>[Role Base Access besturingselementen][RBAC]</br>[Standaardrollen AAD][Roles] |[Activiteitenlogboeken][ActLog]</br>[Diagnostische logboeken][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Aanbevolen procedures voor perimeter-netwerken][DMZ]</br>[Beheer van abonnementen][SubMgmt]</br>[Beheer van resourcegroep][RGMgmt]</br>[Limieten voor Azure-abonnement][Limits] |
|Andere Azure-Services|
|[Azure-Web-Apps][WebApps]</br>[HDInsights (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>Volgende stappen
 - Verken [VNet-Peering][VNetPeering], Hallo basis-technologie voor vDC-hub en spaak ontwerpen
 - Implementeer [AAD] [ AAD] tooget gestart met [RBAC] [ RBAC] exploratie
 - Een abonnement en de Resource management-model te ontwikkelen en RBAC model toomeet Hallo structuur, vereisten en het beleid van uw organisatie. Hallo belangrijkste activiteit is de planning. Plan zo veel mogelijk reorganisaties, fusies, nieuwe regels van het product, enzovoort.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Voorbeelden van onderdeel overlappen" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Op hoog niveau voorbeeld van een hub en spoke vDC"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Cluster met hubs en spaken"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Spoke-spoke-"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Blok niveau diagram van Hallo vDC"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Gebruikers, groepen, abonnementen en projecten"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Op hoog niveau infrastructuurdiagram"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Op hoog niveau infrastructuurdiagram"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "VNet-Peering en perimeter netwerken"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Op hoog niveau diagram voor bewaking"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Op hoog niveau diagram voor werkbelasting"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
