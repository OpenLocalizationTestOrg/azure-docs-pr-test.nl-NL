---
title: aaaAzure bedrijfsbeveiliging | Microsoft Docs
description: Meer informatie over de Microsoft Operations Management Suite (OMS), de services en hoe het werkt.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure-operationele beveiliging
## <a name="introduction"></a>Inleiding

### <a name="overview"></a>Overzicht
We weten dat beveiliging taak in de cloud Hallo en het is belangrijk dat u tijdig en informatie over Azure-beveiliging. Een van de Hallo beste redenen-toouse Azure voor uw toepassingen en services is tootake profiteren van Hallo breed scala aan beveiligingsprogramma's en mogelijkheden die beschikbaar. Deze hulpprogramma's en mogelijkheden helpen mogelijke toocreate veilige oplossingen maken op Hallo beveiligde Azure-platform. Windows Azure moet vertrouwelijkheid, integriteit en beschikbaarheid van klantgegevens, maar ook transparante accountability opgeven.

toohelp klanten Hallo-matrix van beveiligingsmechanismen geïmplementeerd in Microsoft Azure van beide Hallo-klant beter te begrijpen en Microsoft operationele perspectieven dit witboek 'Azure operationele beveiliging', is geschreven en waarmee een uitgebreide bekijkt hello operationele beveiliging met Windows Azure.

### <a name="azure-platform"></a>Azure-Platform
Azure is een openbare cloud service-platform die ondersteuning biedt voor een brede selectie van besturingssystemen, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten. Linux-containers kan worden uitgevoerd met Docker-integratie; bouwen van apps met JavaScript, Python, .NET, PHP, Java en Node.js; Build back-ends voor iOS, Android en Windows apparaten. Azure cloudservice ondersteunt Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen.

Wanneer u bouwen op of IT-activa te migreren, een openbare cloud serviceprovider u zijn afhankelijk te zijn van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met Hallo services en Hallo besturingselementen ze bieden toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven kunnen voldoen aan de beveiligingsvereisten. Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw organisatie implementaties kunt aanpassen. Dit document wordt helpt u begrijpen hoe Azure-beveiliging mogelijkheden kunt u aan deze vereisten voldoen.

### <a name="abstract"></a>Abstracte
Azure bedrijfsbeveiliging verwijst toohello services, besturingselementen en functies beschikbaar toousers voor het beveiligen van hun gegevens, toepassingen en andere elementen in Microsoft Azure. Azure operationele beveiliging is gebaseerd op een framework dat Hallo kennis die is opgedaan met verschillende mogelijkheden die de unieke tooMicrosoft, met inbegrip van Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center Hallo Hallo zijn opgenomen programma en grondige kennis van Hallo cybersecurity threat Liggend.

Dit technisch document bevat een overzicht van Microsoft benadering tooAzure operationele beveiliging binnen Hallo Microsoft Azure cloud-platform en dekt volgende services:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure-netwerk-watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure Storage analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) is Hallo IT beheeroplossing voor Hallo hybride cloud. Alleen wordt gebruikt of uw bestaande System Center-implementatie, OMS biedt u tooextend Hallo maximale flexibiliteit en beheer voor cloud-gebaseerde beheer van uw infrastructuur.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Met OMS, kunt u een instantie in een cloud, met inbegrip van lokale, Azure, AWS, Windows Server, Linux, VMware en OpenStack, tegen lagere kosten dan concurrerende oplossingen beheren. Gebouwd voor Hallo cloud eerste wereld, biedt OMS een nieuwe benadering toomanaging uw onderneming die Hallo snelste, meest rendabele manier toomeet nieuwe zakelijke uitdagingen en geschikt voor de nieuwe werkbelastingen, toepassingen en cloudomgevingen.

### <a name="oms-services"></a>OMS-services

Hallo kernfunctionaliteit van OMS wordt verstrekt door een set services die worden uitgevoerd in Azure. Elke service biedt een specifieke beheerfunctie en u kunt verschillende scenario's voor services tooachieve combineren.

| Service  | Beschrijving|
| :------------- | :-------------|
| Log Analytics | Bewaak en analyseer Hallo beschikbaarheid en prestaties van andere bronnen, met inbegrip van fysieke en virtuele machines. |
|Automatisering | Automatiseer handmatige processen en dwing configuraties af voor fysieke en virtuele machines. |
| Back-up | Back-up en herstel van essentiële gegevens. |
| Site Recovery | Bied hoge beschikbaarheid voor kritieke toepassingen. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) biedt bewakingsservices voor OMS door in een centrale opslagplaats gegevens te verzamelen van beheerde resources. Deze gegevens kan bevatten gebeurtenissen, prestatiegegevens of aangepaste worden geleverd via Hallo API. Zodra verzameld, zijn Hallo gegevens beschikbaar voor waarschuwingen, analyse en exporteren.


Deze methode kunt u tooconsolidate gegevens uit diverse bronnen, zodat u kunt combineren gegevens van uw Azure-services met uw bestaande lokale omgeving. Ook duidelijk scheidt u Hallo verzamelen van gegevens van de Hallo van Hallo actie op die van die gegevens, zodat alle acties beschikbaar tooall soorten gegevens zijn.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Hallo Log Analytics-service beheert uw cloud-gebaseerde gegevens veilig door Hallo volgende methoden:
-   gegevensscheiding
-   bewaren van gegevens
-   Fysieke beveiliging
-   Incidentbeheer
-   Naleving
-   standaarden veiligheidscertificaten

### <a name="azure-backup"></a>Azure Backup

[Azure Backup](http://azure.microsoft.com/documentation/services/backup) biedt gegevens back-up en herstellen van services en maakt deel uit van Hallo OMS-suite van producten en services.
Het beschermt uw toepassingsgegevens en bewaart deze jarenlang, zonder dat u grote investeringen hoeft te doen en met een minimum aan operationele kosten. Deze kunt back-ups van fysieke en virtuele Windows-servers bovendien tooapplication werkbelastingen zoals SQL Server en SharePoint. Kan ook worden gebruikt door [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate beveiligde gegevens tooAzure voor redundantie en langdurige opslag.


Beveiligde gegevens in Azure Backup worden opgeslagen in een back-upkluis in een bepaalde geografische regio. Hallo-gegevens worden gerepliceerd binnen dezelfde regio Hallo en, afhankelijk van Hallo type kluis, kan ook worden gerepliceerde tooanother regio voor verdere tolerantie.

### <a name="management-solutions"></a>Beheeroplossingen
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.


[Oplossingen voor](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) voorverpakte sets met logics die een bepaalde beheerscenario met een of meer OMS-services te implementeren. Er zijn verschillende oplossingen beschikbaar van Microsoft en partners kunt u eenvoudig toevoegen tooyour Azure-abonnement tooincrease Hallo waarde van uw investering in OMS. Als partner kunt u uw eigen oplossingen toosupport uw toepassingen en services maken en bieden ze toousers via hello Azure Marketplace of Quick Start-sjablonen.


![Beheeroplossingen](./media/azure-operational-security/azure-operational-security-fig4.png)

Een goed voorbeeld van een oplossing die gebruikmaakt van meerdere services tooprovide aanvullende functionaliteit is Hallo [Update beheeroplossing](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Deze oplossing gebruikt Hallo [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agent voor Windows en Linux toocollect informatie over vereiste updates op elke agent. Deze gegevens toohello logboekanalyse opslagplaats, waar u het met een opgenomen dashboard analyseren kunt geschreven.

Wanneer u een implementatie van runbooks in maakt [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) gebruikte tooinstall vereiste updates beschikbaar zijn. U hoeft tooworry Hallo onderliggende details over of deze het volledige proces in Hallo portal beheren.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center beschermt u uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen. Binnen het Hallo-service, u zich kunt toodefine beleidsregels niet alleen op basis van uw Azure-abonnementen, maar ook tegen [resourcegroepen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), zodat u gedetailleerder worden uitgevoerd kunt.

### <a name="security-policies-and-recommendations"></a>Beveiligingsbeleid en aanbevelingen

Een beveiligingsbeleid bepaalt Hallo set besturingselementen wordt aanbevolen voor resources binnen de opgegeven abonnement of resourcegroep groep Hallo.

In Security Center definieert u beleid op basis van tooyour en van het bedrijf beveiligingsvereisten Hallo type toepassingen of vertrouwelijkheid van gegevens Hallo.

![Beveiligingsbeleid en aanbevelingen](./media/azure-operational-security/azure-operational-security-fig5.png)


Beleidsregels die zijn ingeschakeld op het abonnementsniveau Hallo automatisch doorgegeven tooall resourcegroepen binnen Hallo abonnement zoals weergegeven in het diagram aan de rechterkant Hallo Hallo:


### <a name="data-collection"></a>Gegevensverzameling

Security Center verzamelt gegevens van uw virtuele machines (VM's) tooassess hun beveiligingsstatus, aanbevelingen voor beveiliging bieden en waarschuwt u toothreats. Wanneer uw eerste toegang Security Center, verzamelen van gegevens is ingeschakeld op alle VM's in uw abonnement. Verzamelen van gegevens wordt aanbevolen, maar u kunt opt-out door het uitschakelen van gegevensverzameling in Hallo Security Center-beleid.

### <a name="data-sources"></a>Gegevensbronnen

- Azure Security Center analyseert gegevens van Hallo bronnen tooprovide zichtbaarheid in uw beveiligingsstatus te volgen, kwetsbaarheden identificeren en oplossingen het beste actieve bedreigingen te detecteren:

-   Azure-Services: Informatie over Hallo configuratie van Azure-services die u hebt geïmplementeerd door de communicatie met die service resourceprovider gebruikt.

- Netwerkverkeer: gebruikt steekproefgewijs netwerkverkeermetagegevens uit de infrastructuur van Microsoft, zoals bron-/doel-IP/poort, pakketgrootte en netwerkprotocol.

-   Oplossingen van partners: gebruikt beveiligingswaarschuwingen van geïntegreerde partneroplossingen, zoals firewalls en antimalwareoplossingen.

-   Uw virtuele machines: gebruikt configuratie-informatie en informatie over beveiligingsgebeurtenissen, zoals Windows-gebeurtenis- en auditlogboeken, IIS-logboeken, syslog-berichten en crashdumpbestanden van uw virtuele machines.

### <a name="data-protection"></a>Gegevensbeveiliging

toohelp klanten detecteren, voorkomen van en reageren toothreats, Azure Security Center verzamelt en beveiliging gerelateerde gegevens, inclusief informatie over de configuratie, metagegevens, gebeurtenislogboeken, crashdumpbestanden en meer verwerkt. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen.

-   **Gegevensscheiding**: gegevens worden voor elk onderdeel in de gehele Hallo service logisch gescheiden gehouden. Alle gegevens worden gemarkeerd per organisatie. Deze labels zich blijft voordoen gedurende de levenscyclus van Hallo gegevens en het wordt afgedwongen op elke laag van Hallo-service.

-   **Toegang tot gegevens**: tooprovide beveiligingsaanbevelingen en onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft kunnen toegang krijgen tot gegevens die worden verzameld of geanalyseerd door Azure-services, waaronder crashdumpbestanden, het maken van gebeurtenissen, schijf van de virtuele machine verwerken momentopnamen en artefacten, waaronder mogelijk per ongeluk gegevens van de klant of persoonlijke gegevens van uw virtuele machines. We ons houden toohello [privacyverklaring voor Microsoft Online Services-voorwaarden en](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), welke status die Microsoft is niet maakt gebruik van gegevens van de klant of een afleiding van gegevens uit het voor reclame of vergelijkbare commerciële doeleinden.

-   **Gebruik**: Microsoft patronen gebruikt en dreigingen gezien over meerdere tenants tooenhance onze mogelijkheden voor preventie en detectie; zo doen dat in overeenstemming met Hallo privacy verbintenissen beschreven in onze [Privacy Instructie](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Gegevenslocatie

Azure Security Center verzamelt tijdelijke kopieën van uw crashdumpbestanden en analyseert deze op bewijs van pogingen tot misbruik en geslaagde aanvallen. Azure Security Center voert deze analyse binnen dezelfde Geo Hallo zoals Hallo werkruimte en verwijderingen Hallo kortstondige kopieën wanneer de analyse is voltooid. Machine artefacten worden opgeslagen in een centraal in dezelfde regio Hallo zoals Hallo VM.

-   **Uw Opslagaccounts**: een opslagaccount is opgegeven voor elke regio waarin virtuele machines worden uitgevoerd. Dit kunt u toostore gegevens in dezelfde regio bevinden als Hallo virtuele machine uit welke Hallo gegevens worden verzameld Hallo.

-   **Azure Security Center opslag**: informatie over beveiligingswaarschuwingen, met inbegrip van de partner waarschuwingen, aanbevelingen en status van de beveiliging in Hallo Verenigde Staten centraal, momenteel wordt opgeslagen. Deze informatie kan bestaan uit verwante configuratie-informatie en beveiligingsgebeurtenissen verzameld van uw virtuele machines als de benodigde tooprovide u met Hallo-beveiliging waarschuwing, de aanbeveling of gezondheidsstatus.


## <a name="azure-monitor"></a>Azure Monitor

Hallo [OMS beveiliging](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) en Audit oplossing kunnen IT-tooactively bewaken alle resources die kunnen helpen minimaliseren Hallo impact van beveiligingsincidenten. OMS beveiligings- en Audit hebben security-domeinen die kunnen worden gebruikt voor het bewaken van de resources. Hallo beveiligingsdomein toooptions voor snelle toegang biedt, voor veiligheidscontrole Hallo volgende domeinen worden behandeld in meer informatie:

-   evaluatie van schadelijke software
-   Update-evaluatie
-   Identiteit en toegang.

Azure biedt een aanwijzers tooinformation op specifieke typen resources. Biedt visualisatie, query routering, waarschuwingen, automatisch schalen en automatisering op gegevens van hello Azure-infrastructuur (activiteitenlogboek) en elke afzonderlijke Azure-resource (diagnostische logboeken).

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Cloud-toepassingen zijn complexe met veel bewegende onderdelen. Monitoring biedt gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt. Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn.

Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.

### <a name="azure-activity-log"></a>Azure Activity Log


Het is een logboek biedt inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement. Hallo activiteitenlogboek heette vroeger 'Controlelogboeken' of 'Operationele Logs', omdat het besturingselement vlak gebeurtenissen voor uw abonnementen rapporten.

![Azure Activity Log](./media/azure-operational-security/azure-operational-security-fig7.png)

Hallo activiteitenlogboek gebruikt, u kunt bepalen Hallo ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die zijn gemaakt op Hallo van resources in uw abonnement. U kunt ook Hallo status Hallo-werking en andere relevante eigenschappen begrijpen. Hallo activiteitenlogboek bevat geen lezen (GET)-bewerkingen en bewerkingen voor resources die gebruikmaken van Hallo klassieke model.

### <a name="azure-diagnostic-logs"></a>Azure diagnostische logboeken

Deze logboeken worden gegenereerd door een resource en leveren rijke, regelmatig gegevens over Hallo-bewerking van de bron. Hallo-inhoud van deze logboeken varieert per resourcetype.

Bijvoorbeeld Windows-gebeurtenislogboeken system zijn één categorie van diagnostische logboeken voor virtuele machines en blob, table en queue logboeken zijn categorieën van diagnostische logboeken voor opslagaccounts.

Diagnostische logboeken verschillen van Hallo [activiteitenlogboek (voorheen bekend als het auditlogboek of operationeel logboek)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Hallo activiteitenlogboek verschaft inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement. Diagnostische logboeken bieden inzicht in bewerkingen dat de bron zelf uitgevoerd.

### <a name="metrics"></a>Metrische gegevens

Monitor voor Azure kunt u tooconsume telemetrie toogain inzicht in prestaties Hallo en status van uw workloads in Azure. Hallo belangrijkste type Azure telemetriegegevens is Hallo metrische gegevens (ook wel prestatiemeteritems) die door de meeste Azure-resources. Monitor voor Azure biedt verschillende manieren tooconfigure en verbruikt [metrische gegevens](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) voor bewaking en probleemoplossing. Metrische gegevens zijn een waardevolle bron van Telemetrie en kunt u toodo Hallo taken te volgen:

-   **Hallo prestaties bijhouden** van de bron (zoals een VM, website of logic app) door de metrische gegevens over een portal grafiek uitzetten en die grafiek tooa dashboard vastmaken.

-   **Blijf op de hoogte van een probleem** dat invloed op prestaties van uw resource Hallo wanneer een metriek een bepaalde drempelwaarde overschrijden.

-   **Configureer automatische acties**, zoals automatisch schalen van een resource of een runbook wordt gestart wanneer een metriek een bepaalde drempelwaarde overschrijden.

-   **Geavanceerde analyses uitvoeren** of rapportage over trends prestatie- of informatie over het gebruik van de bron.

-   **Archief** Hallo geschiedenis van prestaties of de status van de bron voor controledoeleinden of compatibiliteit.

### <a name="azure-diagnostics"></a>Azure Diagnostics

Het is Hallo-functionaliteit in Azure waarmee Hallo verzamelen van diagnostische gegevens op een geïmplementeerde toepassing. U kunt Hallo-extensie voor diagnostische gegevens uit diverse verschillende bronnen. Op dit moment ondersteund zijn [Azure Cloud Service-Web- en werkrollen](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/overview) met Microsoft Windows, en [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Andere Azure-services hebben hun eigen afzonderlijke diagnostische gegevens.

## <a name="azure-network-watcher"></a>Azure-netwerk-Watcher

Controle van de netwerkbeveiliging van uw is het essentieel zijn voor netwerk beveiligingsproblemen detecteren en de naleving van uw IT-beveiliging en regelgeving governance model. U kunt met de weergave van de beveiligingsgroep, Hallo geconfigureerd Netwerkbeveiligingsgroep en beveiliging regels ophalen en Hallo effectieve beveiligingsregels voor verbindingen. Hallo-lijst met regels die zijn toegepast, kunt u Hallo-poorten die zijn geopend en beoordelen van network vulnerability bepalen.

[Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) is een regionale service waarmee u toomonitor en onderzoeken van de voorwaarden op het netwerkniveau van een in, naar en van Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure. Deze service omvat pakketopname, volgende hop, IP-stroom controleren, groep beveiligingsweergave, NSG stroom Logboeken. Scenario niveau bewaking biedt een end-tooend-weergave van netwerkbronnen in contrast tooindividual resource netwerkbewaking.

![Azure-netwerk-Watcher](./media/azure-operational-security/azure-operational-security-fig8.png)

Netwerk-Watcher heeft momenteel Hallo volgende mogelijkheden:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Controlelogboeken</a>**-bewerkingen die worden uitgevoerd als onderdeel van de configuratie van netwerken Hallo worden geregistreerd. Deze logboeken kunnen worden weergegeven in hello Azure-portal of opgehaald met behulp van Microsoft-hulpprogramma's zoals Power BI of hulpprogramma's van derden. Controlelogboeken zijn beschikbaar via het Hallo-portal, PowerShell, CLI en Rest-API. Zie voor meer informatie over controlelogboeken Audit-bewerkingen met Resource Manager. Controlelogboeken zijn beschikbaar voor bewerkingen die op alle netwerkbronnen.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">IP-stroom controleert of </a>**  -controleert of een pakket wordt toegestaan of geweigerd op basis van stroom informatie 5-tuple pakket parameters (doel-IP, bron-IP, doelpoort, bronpoort en Protocol). Als hello-pakket is geweigerd door een Netwerkbeveiligingsgroep, wordt Hallo regel en de Netwerkbeveiligingsgroep die geweigerd hello-pakket geretourneerd.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Volgende hop</a>**  -Hallo volgende hop voor pakketten worden gerouteerd in hello Azure Network-Fabric, zodat u toodiagnose een verkeerd geconfigureerde gebruiker gedefinieerde routes bepaalt.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Groep beveiligingsweergave</a>**  -Hallo effectieve en toegepaste beveiligingsregels voor verbindingen die worden toegepast op een virtuele machine opgehaald.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Logboekregistratie NSG Flow</a>**  -logboeken van de stroom voor Netwerkbeveiligingsgroepen kunt u toocapture gerelateerde tootraffic logboeken die worden toegestaan of geweigerd door Hallo beveiligingsregels voor verbindingen in groep Hallo. Hallo-stroom wordt gedefinieerd door de gegevens van een 5-tuple: bron-IP, doel-IP, bronpoort, doelpoort en -Protocol.

## <a name="azure-storage-analytics"></a>Azure Storage Analytics

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) metrische gegevens die samengevoegde statistieken en capaciteit transactiegegevens over aanvragen tooa storage-service zijn kan opslaan. Transacties worden gerapporteerd op beide Hallo API-niveau van de bewerking en op Hallo serviceniveau voor storage en capaciteit op Hallo opslag serviceniveau wordt gerapporteerd. Metrische gegevens kunt gebruikte tooanalyze service opslaggebruik, vaststellen van problemen met aanvragen tegen Hallo storage-service en tooimprove Hallo prestaties van toepassingen die gebruikmaken van een service.

[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) voert logboekregistratie en voorziet in metrische gegevens voor een opslagaccount. U kunt deze gegevensaanvragen tootrace gebruiken, trends in gebruik analyseren en vaststellen van problemen met uw opslagaccount. Logboekregistratie van Storage Analytics is beschikbaar voor Hallo [services Blob, wachtrijen en tabellen](https://docs.microsoft.com/azure/storage/storage-introduction). Storage Analytics registreert gedetailleerde informatie over geslaagde en mislukte aanvragen tooa storage-service.

Deze informatie kan worden gebruikt toomonitor afzonderlijke aanvragen en toodiagnose problemen met de storage-service. Aanvragen worden geregistreerd op basis van best-effort. Logboekvermeldingen worden alleen gemaakt als er ten opzichte van de service-eindpunt Hallo aanvragen zijn. Voor bijvoorbeeld als een opslagaccount heeft een activiteit in de Blob-eindpunt maar niet in de tabel of een wachtrij-eindpunten alleen die deel uitmaakt van registreert wordt toohello Blob-service gemaakt.

toouse Storage Analytics, moet u deze inschakelen voor elke service wilt u afzonderlijk toomonitor. U kunt ze inschakelen in Hallo [Azure-portal](https://portal.azure.com/); voor meer informatie Zie [een opslagaccount in hello Azure-portal bewaken](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). U kunt ook Opslaganalyse programmatisch via Hallo REST-API of clientbibliotheek Hallo inschakelen. Hallo-Service-eigenschappen instellen bewerking tooenable Storage Analytics afzonderlijk gebruiken voor elke service.

Hallo wordt geaggregeerde gegevens opgeslagen in een bekende blob (voor logboekregistratie) en in een bekende tabellen (voor metrische gegevens) waartoe toegang kunnen worden verkregen met behulp van Hallo Blob-service en service API's van de tabel.

Storage Analytics heeft een limiet van 20 TB op Hallo en de hoeveelheid opgeslagen gegevens die onafhankelijk is van de totale Hallo-limiet voor uw opslagaccount. Alle logboeken worden opgeslagen in [blok-blobs](https://docs.microsoft.com/azure/storage/storage-analytics) in een container met de naam $logs, die automatisch worden gemaakt wanneer Opslaganalyse is ingeschakeld voor een opslagaccount.

Hallo van de volgende activiteiten uitgevoerd door Storage Analytics zijn factureerbare:

-   Aanvragen toocreate blobs voor logboekregistratie
-   Aanvragen toocreate tabelentiteiten voor de metrische gegevens.

> [!Note]
> Zie voor meer informatie over facturering en bewaarbeleid voor gegevens [Storage Analytics en facturering](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
> Voor optimale prestaties wordt u toolimit Hallo aantal maximaal gebruikte schijven gekoppeld toohello virtuele machine tooavoid mogelijk beperking. Als alle schijven niet sterk wordt gebruikt op Hallo hetzelfde moment Hallo storage-account een groter aantal schijf kan ondersteunen.

> [!Note]
> Zie voor meer informatie over opslagaccountlimieten [Azure Storage Scalability and Performance Targets](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


Hallo volgende typen geverifieerde en anonieme aanvragen worden geregistreerd.

| Geverifieerd  | Anonieme|
| :------------- | :-------------|
| Geslaagde aanvragen | Geslaagde aanvragen |
|Mislukte aanvragen, met inbegrip van de time-outperiode, beperking, netwerk, autorisatie en andere fouten | -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen |
| -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen |Time-out fouten voor zowel client als server |
|   Aanvragen tooanalytics gegevens |    GET-aanvragen is mislukt met foutcode 304 (niet gewijzigd) |
| Aanvragen door Storage Analytics zelf, zoals logboekbestanden worden gemaakt of verwijderd, worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) en [Storage Analytics logboekindeling](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) onderwerpen. | Alle andere mislukte anonieme aanvragen worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) en [Storage Analytics logboekindeling](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD bevat ook een volledige reeks mogelijkheden voor identiteitsbeheer waaronder multi-factor authentication-server, apparaatregistratie, selfservice voor wachtwoordherstel management, self-service groepsbeheer, bevoegd accountmanagement, op rollen gebaseerde toegangsbeheer, gebruik bewaking, uitgebreide controle en beveiligingsbewaking en waarschuwingen.

-   Verbeterde Toepassingsbeveiliging met Azure AD multifactor-verificatie en voorwaardelijke toegang.

-   Controleren van het gebruik en uw bedrijf beschermen tegen geavanceerde bedreigingen met beveiliging rapportage en bewaking.

Azure Active Directory (Azure AD) bevat beveiligings-, activiteits- en controlerapporten voor uw directory. [Hello Azure Active Directory-controlerapport](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) helpt klanten tooidentify bevoegde acties die is opgetreden in Azure Active Directory. Bevoegdheden omvatten wijzigingen van de uitbreiding van bevoegdheden (bijvoorbeeld het maken of opnieuw instellen van wachtwoorden), het wijzigen van beleidsconfiguraties (bijvoorbeeld wachtwoordbeleid) of wijzigingen toodirectory configuratie (bijvoorbeeld wijzigingen toodomain federation instellingen).

Hallo-rapporten geven Hallo controlerecord voor gebeurtenisnaam hello, Hallo actor die Hallo actie, Hallo doelbron beïnvloed door wijziging van de Hallo en Hallo datum en tijd (in UTC) heeft uitgevoerd. Klanten kunnen tooretrieve Hallo lijst van de controlegebeurtenissen voor Azure Active Directory via Hallo zijn [Azure-portal](https://portal.azure.com/), zoals beschreven in [uw logboeken Audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Hier volgt een lijst met opgenomen Hallo-rapporten:

| Beveiligingsrapporten  | Activiteitsrapporten| Controlerapporten |
| :------------- | :-------------| :-------------|
|Aanmeldingen van onbekende bronnen | Toepassingsgebruik: samenvatting | Directorycontrolerapport |
|Aanmeldingen na meerdere mislukte pogingen | Toepassingsgebruik: gedetailleerd |   |
|Aanmeldingen vanuit meerdere locaties | Toepassingsdashboard |  |
|Aanmeldingen van IP-adressen met verdachte activiteit |Fouten bij het inrichten van een account |  |
|Onregelmatige aanmeldingsactiviteiten |Afzonderlijke gebruikersapparaten |  |
|Aanmeldingen vanaf mogelijk geïnfecteerde apparaten |Afzonderlijke gebruikersactiviteiten |   |
|Gebruikers met afwijkende aanmeldingsactiviteiten |Rapport met groepsactiviteiten |   |
| |Rapport voor de registratie van opnieuw ingestelde wachtwoorden |   |
| |Activiteit voor wachtwoord opnieuw instellen |   | |



Hallo-gegevens van deze rapporten kunnen nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden. Hello Azure AD-rapportage [API's](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's. U kunt deze API aanroepen vanuit verschillende programmeertalen en hulpprogramma's.

Gebeurtenissen in hello Azure AD-controlerapport worden bewaard gedurende 180 dagen.

> [!Note]
> Zie voor meer informatie over de bewaarperiode op rapporten [bewaarbeleid voor Azure Active Directory rapport](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Voor klanten die de bij het opslaan van hun [controlegebeurtenissen](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) voor langere bewaartermijn hello rapportage-API kan worden gebruikt tooregularly pull-controlegebeurtenissen in een afzonderlijke gegevensarchief.

## <a name="summary"></a>Samenvatting

Dit artikel samenvattingen van de bescherming van uw privacy en beveiliging van uw gegevens tijdens de levering van software en services die u helpen beheren Hallo IT-infrastructuur van uw organisatie. Microsoft herkent dat wanneer ze hun gegevens tooothers belasten, vertrouwensrelatie strengere beveiliging vereist. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen. Beveiliging en bescherming van gegevens is een topprioriteit bij Microsoft.

Dit artikel wordt uitgelegd

-   Hoe gegevens wordt verzameld, verwerkt en beveiligd in Hallo Operations Management Suite (OMS).

-   Analyseer snel gebeurtenissen in meerdere gegevensbronnen. Beveiligingsrisico's identificeren en begrijpen Hallo bereik en de invloed van bedreigingen en aanvallen toomitigate Hallo beschadiging van een inbreuk op de beveiliging.

-   Identificeer aanvalspatronen door uitgaand, schadelijk IP-verkeer en schadelijke bedreigingstypen te visualiseren. Begrijpen Hallo beveiligingsstatus van uw hele omgeving ongeacht het platform.

-   Alle Hallo logboek en gebeurtenis gegevens die nodig zijn voor een controle beveiligings- of naleving vastleggen. Slash Hallo tijd en bronnen nodig toosupply beveiliging controleren met een volledig, doorzoekbaar en exporteerbaar logboek en gebeurtenis gegevensset.

<ul>
<li>Verzamelt gebeurtenissen die betrekking hebben op beveiliging, controle en inbreuk op de analysis tookeep een sluit uw assets ogen:</li>
<ul>
<li>Beveiligingspostuur</li>
<li>Opmerkelijke probleem</li>
<li>Samenvattingen bedreigingen</li>
</ul>
</ul>

## <a name="next-steps"></a>Volgende stappen

- [Ontwerp- en operationele beveiliging](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft ontwerpen van de services en software met beveiliging in gedachten toohelp Zorg ervoor dat de cloudinfrastructuur robuuste en beveiligd zijn tegen aanvallen.

- [Operations Management Suite | Beveiliging en naleving](https://www.microsoft.com/cloud-platform/security-and-compliance)

Microsoft security gegevens en analyse tooperform meer intelligente en doeltreffend gebruik bedreigingendetectie.

- [Azure Security Center plannen en bewerkingen](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) een reeks stappen en taken die u kunt uw gebruik van het Beveiligingscentrum op basis van de beveiligingsvereisten van uw organisatie en het cloudbeheermodel toooptimize volgen.

