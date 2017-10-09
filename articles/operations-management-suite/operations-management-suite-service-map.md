---
title: aaaUse hello Serviceoverzicht oplossing in de Operations Management Suite | Microsoft Docs
description: Serviceoverzicht is een Operations Management Suite-oplossing die automatisch de onderdelen van toepassing op Windows detecteert en Linux-systemen en maps Hallo communicatie tussen services. Dit artikel bevat informatie voor het Serviceoverzicht implementeren in uw omgeving en gebruiken in verschillende scenario's.
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Hallo Serviceoverzicht oplossing gebruiken in Operations Management Suite
Serviceoverzicht detecteert automatisch de onderdelen van toepassing op Windows-en Linux- en maps Hallo communicatie tussen services. Met het Serviceoverzicht, kunt u uw servers weergeven Hallo manier waarop u denkt ze dat: als onderling verbonden systemen die essentiële services leveren. Hallo installatie van een agent Serviceoverzicht ziet u de verbindingen tussen servers, processen en poorten voor elke architectuur TCP-verbinding zonder configuratie dan vereist.

Dit artikel wordt beschreven Hallo details van het gebruik van Serviceoverzicht. Zie voor meer informatie over het configureren van Serviceoverzicht en voorbereiding agents [oplossing Serviceoverzicht configureren in de Operations Management Suite](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Gebruiksvoorbeelden: maken van uw IT-processen op de hoogte van afhankelijkheid

### <a name="discovery"></a>Detectie
Een algemene referentie-kaart van afhankelijkheden maakt Serviceoverzicht automatisch in uw servers, processen en services van derden. Het detecteert en alle TCP-afhankelijkheden, identificeren verrassing verbindingen, externe van derden systemen die u afhankelijk en afhankelijkheden tootraditional donkere gebieden van uw netwerk, zoals Active Directory wordt toegewezen. Serviceoverzicht detecteert mislukte netwerkverbindingen dat uw beheerde systemen toomake, probeert u identificeren mogelijke onjuiste configuratie van server, onderbreking van deze service en netwerkproblemen te helpen.

### <a name="incident-management"></a>Incidentbeheer
Serviceoverzicht helpt Hallo vermijden probleem isolatielaag elimineren door die laat zien hoe systemen zijn verbonden en elkaar beïnvloeden. Bovendien verbindingen in tooidentifying is mislukt, het identificeren van onjuist geconfigureerde load balancers, verrassend of overmatige belasting van essentiële services en clients, zoals ontwikkelaars machines praten tooproduction systemen rogue helpt. Via geïntegreerde werkstromen met Operations Management Suite wijzigen bijhouden ook ziet u of de wijzigingsgebeurtenis voor een op een back-end-machine of service wordt uitgelegd Hallo hoofdoorzaak van een incident.

### <a name="migration-assurance"></a>Migratie zekerheid
Met behulp van Serviceoverzicht, kunt u effectief plannen, versnellen en Azure migraties valideren die zorgt ervoor dat er niets is achtergelaten en geen onverwachte storingen optreden. U kunt alle onderling afhankelijk systemen samen die toomigrate moet detecteren, beoordelen systeemconfiguratie en de capaciteit en bepalen of een actieve gebruikers nog steeds bedient of geschikt is voor het buiten gebruik stellen in plaats van de migratie. Nadat Hallo verplaatsen voltooid is, kunt u controleren op de client laden en identiteit tooverify die testen systemen en klanten verbinding maakt. Als uw subnetdefinities plannen en firewall problemen hebt, wijst mislukte verbindingen Serviceoverzicht Maps toohello systemen die moeten zijn verbonden.

### <a name="business-continuity"></a>Bedrijfscontinuïteit
Als u van Azure Site Recovery gebruikmaakt en moet help definiëren Hallo herstel reeks voor uw toepassingsomgeving, serviceoverzicht automatisch ziet u hoe systemen zijn afhankelijk van elkaar tooensure herstelplan is betrouwbaar. Door een kritieke server of een groep te kiezen en de clients te bekijken, kunt u welke toorecover front-end systemen identificeren nadat Hallo server teruggezet en beschikbaar is. Als u daarentegen door kritieke servers back-end afhankelijkheden bekijkt, kunt u bepalen welke systemen toorecover voordat uw systemen focus zijn hersteld.

### <a name="patch-management"></a>Patch management
Uw gebruik van Hallo Operations Management Suite System Update Assessment verbetert Serviceoverzicht door te tonen die andere teams en -servers hangen af van uw service, zodat u deze vooraf waarschuwen kunt voordat u uw systeem voor patch-doeleinden. Patchbeheer van de in Operations Management Suite verbetert Serviceoverzicht ook door u of uw services beschikbaar en goed verbonden nadat zijn ze worden hersteld en opnieuw opgestart.


## <a name="mapping-overview"></a>Overzicht van de toewijzing
Serviceoverzicht agents verzamelen informatie over alle TCP verbonden processen op Hallo server waarop ze worden geïnstalleerd en meer informatie over binnenkomende en uitgaande verbindingen voor elk proces Hallo. In de lijst Hallo in het linkerdeelvenster hello, kunt u computers of groepen die hun afhankelijkheden Serviceoverzicht agents toovisualize via een opgegeven periode hebben. Afhankelijkheid van de machine wordt toegewezen focus op een specifieke computer en ze alle Hallo-machines die directe TCP-clients of servers van de desbetreffende computer weergeven.  Groepstoewijzingen machine weergeven sets van servers en de bijbehorende afhankelijkheden.

![Overzicht van het Serviceoverzicht](media/oms-service-map/service-map-overview.png)

Machines kunnen worden uitgebreid in Hallo kaart tooshow Hallo actieve processen met actieve netwerkverbindingen tijdens tijdsbereik Hallo geselecteerd. Wanneer een externe computer met een Serviceoverzicht-agent uitgevouwen tooshow procesgegevens is, worden alleen die processen die met de Hallo focus machine communiceren weergegeven. Hallo-telling van zonder agents front-machines die verbinding met de Hallo focus machine wordt aan de linkerkant Hallo Hallo processen die ze verbinding met maken aangegeven. Als Hallo focus machine maakt een verbinding tooa back-end-machine waarop geen agent is, Hallo back-endserver is opgenomen in een servergroep poort, samen met andere verbindingen toohello hetzelfde poortnummer.

Standaard wijst Serviceoverzicht weergeven Hallo afgelopen 30 minuten van afhankelijkheidsinformatie. Via Hallo tijd besturingselementen in de linkerbovenhoek Hallo kunt u een query-toewijzingen voor historische tijdsbereik up tooone uur tooshow hoe afhankelijkheden in Hallo opgezocht verleden (bijvoorbeeld, tijdens een incident, of voordat er een wijziging is opgetreden). Serviceoverzicht gegevens worden opgeslagen voor 30 dagen in betaalde werkruimten en 7 dagen in gratis werkruimten.

## <a name="status-badges-and-border-coloring"></a>Status badges en de kleur van rand
Onder aan elke server in Hallo kaart kan een lijst met status badges overbrengen statusinformatie over Hallo-server worden op Hallo. Hallo badges erop duiden dat er een relevante informatie voor Hallo-server uit een Hallo Operations Management Suite-oplossing integraties. Een badge te klikken gaat u rechtstreeks toohello details van status Hallo in het rechterdeelvenster Hallo. Hallo bevatten momenteel beschikbare status badges waarschuwingen, servicedesk, beveiliging, wijzigingen en Updates.

Afhankelijk van de ernst van Hallo status badges Hallo machine knooppunt randen worden gekleurde rood (Kritiek), geel (waarschuwing) of blauw (informatief). Hallo kleur vertegenwoordigt Hallo ernstigste status van Hallo status badges. Een grijze rand geeft aan dat een knooppunt dat geen statusindicatoren is.

![Status badges](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Computergroepen
Met behulp van de machine groepen kunt u toosee maps gecentreerd rond een reeks servers, niet alleen een zodat u alle Hallo leden van een cluster met meerdere lagen toepassings- of in een kaart kunt zien.

Gebruikers selecteren welke servers deel uitmaken van een groep samen en kies een naam voor het Hallo-groep.  U kunt vervolgens kies tooview Hallo groep met alle processen en verbindingen of andere leden van de groep Hallo weergeven met alleen Hallo processen en verbindingen die rechtstreeks verband toohello houden.

![Computergroep](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Maken van een groep machines
toocreate een groep, selecteer Hallo machine of machines gewenste op Hallo Machines lijst en klikt u op **toogroup toevoegen**.

![Groep maken](media/oms-service-map/machine-groups-create.png)

Daar kunt u **nieuw** en geef een naam Hallo-groep.

![De naam van groep](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Computergroepen zijn momenteel beperkt too10 servers, maar we zullen tooincrease deze limiet snel.

### <a name="viewing-a-group"></a>Een groep weergeven
Als u een aantal groepen hebt gemaakt, kunt u ze kunt weergeven door Hallo groepen tabblad te kiezen.

![Tabblad groepen](media/oms-service-map/machine-groups-tab.png)

Selecteer vervolgens Hallo Group name tooview Hallo-toewijzing voor de groep computer.
![Machinegroep](media/oms-service-map/machine-group.png) Hallo-machines die deel uitmaken van de groep toohello worden beschreven in wit in Hallo-kaart.

Hallo-machines die gezamenlijk Hallo Machinegroep uitbreidbare Hallo groep wordt een lijst.

![Machine groep machines](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filteren op processen
U kunt schakelen Hallo overzichtsweergave tussen alle processen en verbindingen in groep Hallo weergegeven en alleen Hallo die rechtstreeks verband toohello Machinegroep houden.  Hallo standaardweergave is tooshow alle processen.  U kunt Hallo weergave wijzigen door te klikken op het filterpictogram Hallo boven Hallo-kaart.

![Filter-groep](media/oms-service-map/machine-groups-filter.png)

Wanneer **alle processen** is geselecteerd, Hallo kaart neemt alle processen en verbindingen op elk van de machines Hallo in Hallo groep.

![Alle Machinegroep verwerkt](media/oms-service-map/machine-groups-all.png)

Als u alleen Hallo weergave tooshow wijzigt **processen groep verbonden**, Hallo kaart wordt verkleind omlaag tooonly die processen en verbindingen die rechtstreeks zijn verbonden tooother machines in de groep hello, een vereenvoudigde weergave maken.

![Machinegroep gefilterd processen](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Toe te voegen machines tooa groep
tooadd machines tooan bestaande groep, controleert u Hallo vakken volgende toohello machines u wilt en klik vervolgens op **toogroup toevoegen**.  Kies vervolgens de gewenste tooadd Hallo machines Hallo-groep.
 
### <a name="removing-machines-from-a-group"></a>Machines verwijderen uit een groep
Vouw in de lijst groepen Hallo, Hallo groep naam toolist Hallo machines in Hallo Machinegroep.  Klik vervolgens op Hallo weglatingsteken menu volgende toohello machine gewenste tooremove en kies **verwijderen**.

![Machine uit groep verwijderen](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Verwijderen of hernoemen van een groep
Klik op Hallo weglatingsteken menu volgende toohello groepsnaam in Hallo lijst voor de groep.

![Menu voor groep machines](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Rolpictogrammen
Bepaalde processen dienen bepaalde functies op computers: web-servers, toepassingsservers en -database. Serviceoverzicht annotates proces en machine vakken met rol pictogrammen toohelp vastgesteld in een oogopslag Hallo functie een proces of de server wordt afgespeeld.

| Functiepictogram | Beschrijving |
|:--|:--|
| ![Webserver](media/oms-service-map/role-web-server.png) | Webserver |
| ![Appserver](media/oms-service-map/role-application-server.png) | Toepassingsserver |
| ![Database-server](media/oms-service-map/role-database.png) | Database-server |
| ![LDAP-server](media/oms-service-map/role-ldap.png) | LDAP-server |
| ![SMB-server](media/oms-service-map/role-smb.png) | SMB-server |

![Rolpictogrammen](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Mislukte verbindingen
Mislukte verbindingen worden weergegeven in Serviceoverzicht toegewezen processen en computers, met een rode stippellijn die aangeeft dat een clientsysteem is niet mogelijk tooreach een proces of poort. Mislukte verbindingen worden gerapporteerd door een systeem met een geïmplementeerde Serviceoverzicht agent als dat systeem Hallo één tijdens het Hallo kan geen verbinding is. Serviceoverzicht meet dit proces door een verbinding voor TCP-sockets die niet voldoen aan tooestablish observeren. Deze fout kan het gevolg zijn van een firewall, een onjuiste configuratie van het Hallo-client of server, of een externe service is tijdelijk niet beschikbaar zijn.

![Mislukte verbindingen](media/oms-service-map/failed-connections.png)

Informatie over mislukte verbindingen kunnen helpen bij het oplossen van problemen validatie van de migratie, beveiligingsanalyse en algemene architectuur understanding. Mislukte verbindingen zijn soms onschadelijk, maar ze vaak wijst rechtstreeks tooa probleem, zoals een failover-omgeving plotseling is onbereikbaar of twee toepassingslagen niet kan tootalk wordt na de cloudmigratie van een.

## <a name="client-groups"></a>Clientgroepen
Clientgroepen zijn vakken op Hallo kaart die clientcomputers waarvoor geen afhankelijkheid Agents vertegenwoordigen. Een enkele clientgroep vertegenwoordigt Hallo-clients voor een afzonderlijk proces of de machine.

![Clientgroepen](media/oms-service-map/client-groups.png)

toosee hello IP-adressen van servers in een groep van de Client, selecteer Hallo groep Hallo. Hallo-inhoud van Hallo groep wordt weergegeven in Hallo **Client groepseigenschappen** deelvenster.

![Eigenschappen van client](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Serverpoort groepen
Serverpoort groepen zijn vakken waarin de server-poorten op servers waarop geen afhankelijkheid Agents. Hallo vak bevat Hallo server-poort en een telling van Hallo aantal servers met verbindingen toothat poort. Vouw Hallo vak toosee Hallo afzonderlijke servers en verbindingen. Als er slechts één server in het vak hello, wordt Hallo-naam of IP-adres vermeld.

![Serverpoort groepen](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Contextmenu
Te klikken op Hallo weglatingsteken (...) boven Hallo rechts van elke server Hallo contextmenu voor die server worden weergegeven.

![Mislukte verbindingen](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Load server-kaart
Te klikken op **Load Server kaart** gaat u een nieuw overzicht met de geselecteerde server Hallo als Hallo nieuwe focus machine tooa.

### <a name="show-self-links"></a>Weergeven Self link-elementen
Te klikken op **Self-Links weergeven** opnieuw getekend Hallo-serverknooppunt, inclusief alle Self link-elementen, die zijn TCP-verbindingen die beginnen en eindigen op processen binnen Hallo-server. Als self link-elementen zijn gewijzigd in de menuopdrachten te zien, Hallo**Self-Links verbergen**, zodat u kunt deze uitschakelen.

## <a name="computer-summary"></a>Samenvatting van computer
Hallo **Machine samenvatting** deelvenster bevat een overzicht van een server-besturingssysteem, afhankelijkheid tellingen en gegevens van andere Operations Management Suite-oplossingen. Dergelijke gegevens omvatten maatstaven voor prestaties, helpdesk servicetickets, bijhouden, beveiliging en updates.

![Samenvattingsvenster machine](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Eigenschappen van de computer en het proces
Wanneer u een kaart Serviceoverzicht navigeert, kunt u computers en processen toogain aanvullende context over de eigenschappen. Machines bieden informatie over DNS-naam, IPv4-adressen, CPU en geheugen capaciteit, VM-type, besturingssysteem en versie, laatste opnieuw opstarten tijd en het Hallo-id's van de Operations Management Suite en Serviceoverzicht agents.

![Deelvenster machine-eigenschappen](media/oms-service-map/machine-properties.png)

U kunt procesgegevens verzamelen van metagegevens over het uitvoeren van processen, waaronder procesnaam, Procesbeschrijving, gebruikersnaam en domein (op Windows), bedrijfsnaam, productnaam, versie van het product, werkmap, opdrachtregel en proces besturingssysteem de begintijd.

![Deelvenster Eigenschappen verwerken](media/oms-service-map/process-properties.png)

Hallo **overzicht** deelvenster biedt aanvullende informatie over het Hallo-proces connectiviteit, met inbegrip van de afhankelijke poorten, binnenkomende en uitgaande verbindingen en verbindingen is mislukt.

![Deelvenster Overzicht van het proces](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Integratie van operations Management Suite-waarschuwingen
Serviceoverzicht integreert met Operations Management Suite waarschuwingen tooshow gestart waarschuwingen voor de geselecteerde server Hallo in tijdsbereik Hallo geselecteerd. Hallo-server wordt een pictogram weergegeven als er huidige waarschuwingen en Hallo **Machine waarschuwingen** deelvenster toont Hallo waarschuwingen.

![Deelvenster waarschuwingen van de computer](media/oms-service-map/machine-alerts.png)

tooenable Serviceoverzicht toodisplay relevante waarschuwingen, maakt een waarschuwingsregel die wordt geactiveerd voor een specifieke computer. de juiste waarschuwingen toocreate:
- Een component toogroup opnemen door computer (bijvoorbeeld **met Computer interval 1 minuut**).
- Kies tooalert op basis van metrische meting.

![Configuratie van de waarschuwing](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Integratie van operations Management Suite logboek gebeurtenissen
Serviceoverzicht worden geïntegreerd met logboek zoeken tooshow een telling van alle beschikbare logboekgebeurtenissen voor de geselecteerde server Hallo tijdens tijdsbereik Hallo geselecteerd. U kunt op elke rij in de lijst Hallo van gebeurtenis aantallen toojump tooLog zoeken en Hallo afzonderlijke gebeurtenissen te bekijken.

![Machine logboekgebeurtenissen deelvenster](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Integratie van operations Management Suite-servicedesk
Serviceoverzicht integratie met Hallo IT Service Management-Connector is automatische wanneer beide oplossingen zijn ingeschakeld en geconfigureerd in de Operations Management Suite-werkruimte. Hallo-integratie in Service-kaart wordt aangeduid als "Servicedesk." Zie voor meer informatie [centraal beheren van werkitems ITSM IT Service Management-Connector met](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Hallo **Machine servicedesk** deelvenster toont alle gebeurtenissen voor IT-servicebeheer voor de geselecteerde server Hallo in tijdsbereik Hallo geselecteerd. Hallo-server, wordt er een pictogram weergegeven als er huidige items en Hallo Machine servicedesk deelvenster geeft een lijst van deze.

![Machine servicedesk deelvenster](media/oms-service-map/service-desk.png)

tooopen hello item in de verbonden ITSM-oplossing, klikt u op **weergave werkitem**.

tooview hello details van Hallo-item in logboek zoekopdracht, klikt u op **weergeven in het logboek zoeken**.


## <a name="operations-management-suite-change-tracking-integration"></a>Integratie van operations Management Suite-bijhouden
Serviceoverzicht integratie met wijzigingen bijhouden is automatische wanneer beide oplossingen zijn ingeschakeld en geconfigureerd in de Operations Management Suite-werkruimte.

Hallo **Machine bijhouden** deelvenster geeft een lijst van alle wijzigingen, met de meest recente Hallo eerst, samen met een koppeling toodrill omlaag tooLog zoeken naar aanvullende informatie.

![Machine bijhouden deelvenster](media/oms-service-map/change-tracking.png)

Hallo volgende afbeelding bevat een gedetailleerde weergave van een configuratiewijziging gebeurtenis die u ziet nadat u hebt geselecteerd **weergeven in logboekanalyse**.

![Configuratiewijziging gebeurtenis](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Integratie van operations Management Suite-prestaties
Hallo **Machine prestaties** deelvenster standaard prestatiemetrieken voor de geselecteerde server Hallo worden weergegeven. Hallo metrische gegevens behoren CPU-gebruik, geheugengebruik verzonden en ontvangen netwerkbytes en een lijst van veelgebruikte processen Hallo door verzonden en ontvangen netwerkbytes. prestatiegegevens van tooget Hallo netwerk, u moet ook ingeschakeld Hallo kabel gegevens 2.0-oplossing in de Operations Management Suite.

![Machine prestaties deelvenster](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Integratie van operations Management Suite-beveiliging
Serviceoverzicht integratie met beveiligings- en Audit is automatische wanneer beide oplossingen zijn ingeschakeld en geconfigureerd in de Operations Management Suite-werkruimte.

Hallo **Machine beveiliging** deelvenster geeft gegevens uit de beveiliging van Operations Management Suite en Audit oplossing voor de geselecteerde server Hallo Hallo. Hallo deelvenster geeft een overzicht van openstaande beveiligingsproblemen voor Hallo server tijdens het tijdsbereik Hallo geselecteerd. Het selecteren van Hallo beveiliging problemen zoomt u in een zoekopdracht logboek voor meer informatie over deze.

![Machine beveiliging deelvenster](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Integratie van operations Management Suite-Updates
Serviceoverzicht integratie met beheer van updates is automatisch wanneer beide oplossingen zijn ingeschakeld en geconfigureerd in de Operations Management Suite-werkruimte.

Hallo **Machine Updates** deelvenster worden gegevens uit Hallo updatebeheer van Operations Management Suite-oplossing voor de geselecteerde server Hallo weergegeven. Hallo deelvenster geeft een samenvatting weer van eventuele ontbrekende updates voor Hallo server tijdens het tijdsbereik Hallo geselecteerd.

![Machine bijhouden deelvenster](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Log Analytics-records
Serviceoverzicht computer- en inventarisgegevens is beschikbaar voor [search](../log-analytics/log-analytics-log-searches.md) in logboekanalyse. U kunt deze gegevens tooscenarios met migratieplanning, capaciteitsanalyse detectie en het oplossen van de prestaties op aanvraag toepassen.

Een record per uur voor elke unieke computernaam en het proces wordt gegenereerd, Daarnaast toohello records die worden gegenereerd wanneer een proces of de computer wordt gestart of geïntegreerde tooService is toegewezen. Deze records hebben Hallo eigenschappen in Hallo tabellen te volgen. Hallo-velden en waarden in Hallo ServiceMapComputer_CL gebeurtenissen toewijzen toofields Hallo machinebron in Hallo ServiceMap Azure Resource Manager-API. Hallo velden en waarden in Hallo ServiceMapProcess_CL gebeurtenissen toohello velden toewijzen Hallo proces resource in Hallo ServiceMap Azure Resource Manager-API. Hallo ResourceName_s veld komt overeen met de Hallo naamveld in Hallo overeenkomende Resource Manager-resource. 

>[!NOTE]
>Naarmate Serviceoverzicht functies groeien, zijn deze velden onderwerp toochange.

Er zijn intern gegenereerde eigenschappen kunt u tooidentify unieke processen en computers:

- Computer: Gebruik ResourceId of ResourceName_s toouniquely identificeren een computer binnen een Operations Management Suite-werkruimte.
- Proces: Gebruik ResourceId toouniquely identificeren een proces binnen een Operations Management Suite-werkruimte. ResourceName_s is uniek binnen de context Hallo van Hallo-machine op welke Hallo proces (MachineResourceName_s) wordt uitgevoerd 

Omdat er meerdere records kunnen zijn voor een bepaald proces en de computer in een opgegeven tijdperiode, query's meer dan een record voor Hallo kunnen terugkeren dezelfde computer of proces. tooinclude Hallo alleen meest recente record toevoegen "| Ontdubbeling ResourceId' toohello query.

### <a name="servicemapcomputercl-records"></a>ServiceMapComputer_CL records
Records van het type *ServiceMapComputer_CL* inventarisgegevens voor servers met Serviceoverzicht agents hebben. Deze records hebben Hallo eigenschappen in de volgende tabel Hallo:

| Eigenschap | Beschrijving |
|:--|:--|
| Type | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | de unieke id voor een computer in de werkruimte Hallo Hallo |
| ResourceName_s | de unieke id voor een computer in de werkruimte Hallo Hallo |
| ComputerName_s | Hallo computer FQDN-naam |
| Ipv4Addresses_s | Een lijst met IPv4-adressen Hallo-server |
| Ipv6Addresses_s | Een lijst met IPv6-adressen Hallo-server |
| DnsNames_s | Een matrix van DNS-namen |
| OperatingSystemFamily_s | Windows- of Linux |
| OperatingSystemFullName_s | volledige naam van het besturingssysteem Hallo Hallo  |
| Bitness_s | Hallo bitness van Hallo-machine (32-bits of 64-bits)  |
| PhysicalMemory_d | Hallo fysiek geheugen in MB |
| Cpus_d | Hallo aantal CPU 's |
| CpuSpeed_d | Hallo CPU-snelheid in MHz|
| VirtualizationState_s | *Onbekende*, *fysieke*, *virtuele*, *hypervisor* |
| VirtualMachineType_s | *Hyper-v*, *vmware*, enzovoort |
| VirtualMachineNativeMachineId_g | Hallo VM-ID die is toegewezen door de hypervisor |
| VirtualMachineName_s | Hallo-naam van Hallo VM |
| BootTime_t | Hallo opstarten |



### <a name="servicemapprocesscl-type-records"></a>Type ServiceMapProcess_CL records
Records van het type *ServiceMapProcess_CL* beschikken over inventarisgegevens voor TCP-gerelateerde processen op servers met Serviceoverzicht agents. Deze records hebben Hallo eigenschappen in de volgende tabel Hallo:

| Eigenschap | Beschrijving |
|:--|:--|
| Type | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | de unieke id voor een proces in de werkruimte Hallo Hallo |
| ResourceName_s | Hallo unieke id voor een proces binnen Hallo-machine waarop deze wordt uitgevoerd|
| MachineResourceName_s | de resourcenaam Hallo van Hallo machine |
| ExecutableName_s | Hallo-naam van het uitvoerbare bestand voor het Hallo |
| StartTime_t | Begintijd van Hallo proces van toepassingen |
| FirstPid_d | eerste PID in de procesgroep Hallo Hallo |
| Description_s | Hallo Procesbeschrijving |
| CompanyName_s | Hallo-naam van Hallo bedrijf |
| InternalName_s | de interne naam Hallo |
| ProductName_s | Hallo-naam van Hallo product |
| ProductVersion_s | Hallo productversie |
| FileVersion_s | Hallo bestandsversie |
| CommandLine_s | Hallo-opdrachtregel |
| ExecutablePath _K | Hallo pad toohello uitvoerbaar bestand |
| WorkingDirectory_s | Hallo-werkmap |
| Gebruikersnaam | Hallo account onder welke Hallo proces wordt uitgevoerd |
| UserDomain | Hallo domein onder welke Hallo proces wordt uitgevoerd |


## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken

### <a name="list-all-known-machines"></a>Lijst van alle bekende machines
Type = ServiceMapComputer_CL | Ontdubbeling ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Lijst Hallo de capaciteit van het fysieke geheugen van alle beheerde computers.
Type = ServiceMapComputer_CL | Selecteer PhysicalMemory_d, ComputerName_s | Ontdubbeling ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Computernaam van de lijst, DNS, IP- en OS.
Type = ServiceMapComputer_CL | Selecteer ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s | Ontdubbeling ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Alle processen met 'sql' niet vinden in Hallo vanaf de opdrachtregel
Type = ServiceMapProcess_CL CommandLine_s = \*sql\* | Ontdubbeling ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Een machine (meest recente record) vinden met de resourcenaam
Type = "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" ServiceMapComputer_CL | Ontdubbeling ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Een machine (meest recente record) vinden door IP-adres
Type = "10.229.243.232" ServiceMapComputer_CL | Ontdubbeling ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Lijst van alle bekende processen op een opgegeven computer
Type ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b =" | Ontdubbeling ResourceId

### <a name="list-all-computers-running-sql"></a>Lijst van alle computers met SQL
Type ServiceMapComputer_CL ResourceName_s IN = {Type = ServiceMapProcess_CL \*sql\* | Afzonderlijke MachineResourceName_s} | Ontdubbeling ResourceId | Afzonderlijke ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Lijst van alle unieke productversies van curl in mijn datacenter
Type = ServiceMapProcess_CL ExecutableName_s = curl | Afzonderlijke ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Maak een computergroep van alle computers met CentOS
Type = ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Afzonderlijke ComputerName_s


## <a name="rest-api"></a>REST API
Alle Hallo-server, verwerken en afhankelijkheid gegevens in het Serviceoverzicht is beschikbaar via Hallo [REST-API van kaart](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Diagnostische gegevens en gebruiksgegevens
Microsoft verzamelt automatisch gebruiks- en via uw gebruik van Hallo Serviceoverzicht service. Microsoft gebruikt deze gegevens tooprovide en Hallo kwaliteit, beveiliging en integriteit van Hallo Serviceoverzicht service te verbeteren. tooprovide nauwkeurige en efficiënte mogelijkheden voor probleemoplossing, Hallo gegevens omvatten informatie over Hallo configuratie van uw software, zoals het besturingssysteem en versie, IP-adres, DNS-naam en de Werkstationnaam van het. Microsoft verzamelt geen namen, adressen of andere contactgegevens.

Zie voor meer informatie over het verzamelen van gegevens en gebruiksgegevens Hallo [privacyverklaring van Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Volgende stappen
Meer informatie over [Meld zoekopdrachten](../log-analytics/log-analytics-log-searches.md) in logboekanalyse tooretrieve gegevens die worden verzameld door Serviceoverzicht.


## <a name="troubleshooting"></a>Problemen oplossen
Zie Hallo [probleemoplossing sectie Hallo Serviceoverzicht configureren document](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Feedback
Hebt u feedback voor ons over Serviceoverzicht of deze documentatie?  Ga naar onze [User Voice pagina](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), kunt u functies aanbevelen of om bestaande suggesties stemmen.
