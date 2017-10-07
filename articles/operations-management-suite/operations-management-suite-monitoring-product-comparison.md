---
title: Productvergelijking bewaking aaaMicrosoft | Microsoft Docs
description: Microsoft Operations Management Suite (OMS) is van Microsoft-cloud-gebaseerde IT-beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.  In dit artikel Hallo verschillende services die worden opgenomen in OMS identificeert en vindt u koppelingen tootheir gedetailleerde inhoud.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Microsoft monitoring-vergelijking
In dit artikel bevat een vergelijking tussen System Center Operations Manager (SCOM) en Log Analytics in Operations Management Suite (OMS) in termen van hun architectuur, het Hallo-logica van hoe ze resources bewaken en hoe ze analyse van gegevens Hallo uitvoeren ze verzamelen.  Dit is toogive u een fundamenteel begrip van hun verschillen en relatieve sterke.  

## <a name="basic-architecture"></a>Basic-architectuur
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Alle SCOM-onderdelen worden geïnstalleerd in uw datacenter.  [Agents zijn geïnstalleerd](http://technet.microsoft.com/library/hh551142.aspx) op Windows- en Linux-machines die worden beheerd door SCOM.  Agents verbinding te maken met[beheerservers](https://technet.microsoft.com/library/hh301922.aspx) die communiceren met de Hallo SCOM database en het datawarehouse.  Agents zijn afhankelijk van domein authentication tooconnect toomanagement-servers.  Die buiten een vertrouwd domein kunnen verificatie uitvoeren of verbinden tooa [gatewayserver](https://technet.microsoft.com/library/hh212823.aspx).

SCOM vereist twee SQL-databases, één voor de operationele gegevens en een andere datawarehouse toosupport rapportages en analyses.  Een [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) tooreport SQL Reporting Services op gegevens uit het datawarehouse hello wordt uitgevoerd. 

SCOM kunt bewaken met behulp van management packs voor producten zoals cloudresources [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708), en [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Deze management packs gebruiken een of meer lokale agents als proxy voor het detecteren van cloud-resources en uitvoeren van werkstromen toomeasure hun prestaties en beschikbaarheid.  Proxy-agents worden ook gebruikt te[netwerkapparaten bewaken](https://technet.microsoft.com/library/hh212935.aspx) en andere externe bronnen.

Hallo is Operations-Console een Windows-toepassing die u verbindt tooone Hallo-beheerservers en kunt Hallo beheerder tooview en verzamelde gegevens te analyseren en Hallo SCOM-omgeving configureren.  Een webconsole kan worden gehost op een IIS-server en analyse van gegevens via een browser biedt.

![SCOM-architectuur](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
De meeste OMS-onderdelen zijn in hello Azure-cloud zodat u kunt implementeren en met minimale kosten en administratieve werk beheren.  Alle gegevens die worden verzameld door Log Analytics wordt opgeslagen in Hallo OMS-opslagplaats.

Log Analytics kunt verzamelen van gegevens uit een van drie bronnen:

* Fysieke en virtuele machines met Windows hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) of Linux- en Hallo [Operations Management Suite-Agent voor Linux](https://technet.microsoft.com/library/mt622052.aspx).  Deze machines kunnen worden on-premises of virtuele machines in Azure of een andere cloud.
* Een Azure Storage-account met [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) gegevens verzameld door de functie Azure worker Webrol of virtuele machine.
* [Verbinding tooa SCOM-beheergroep](https://technet.microsoft.com/library/mt484104.aspx).  In deze configuratie communiceren Hallo agents met SCOM-beheerservers die leveren Hallo gegevens toohello SCOM database waar deze vervolgens toohello OMS-gegevensarchief is geleverd.
  Beheerders verzamelde gegevens te analyseren en Log Analytics configureren met Hallo OMS-portal toegankelijk vanuit elke browser die wordt gehost in Azure.  Mobiele apps tooaccess deze gegevens zijn beschikbaar voor standaard Hallo-platforms.

![Log Analytics-architectuur](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integratie van SCOM en Log Analytics
Wanneer SCOM wordt gebruikt als gegevensbron voor Log Analytics kunt u gebruikmaken van Hallo functies van beide producten in een hybride omgeving bewaken.  U kunt bestaande SCOM-agents via Hallo Operations-Console toobe beheerd door OMS configureren, Daarnaast toocontinuing toorun management packs uit SCOM.  
Gegevens van een verbonden SCOM-beheergroep geleverd tooLog Analytics met een van de vier methoden:

* Gebeurtenissen en prestatiegegevens worden verzameld door Hallo agent en tooSCOM geleverd.  Beheerservers in SCOM levert vervolgens Hallo gegevens tooLog Analytics.
* Sommige gebeurtenissen zoals IIS-logboeken en beveiligingsgebeurtenissen blijven toobe bezorgd rechtstreeks tooLog Analytics Hallo-agent.
* Sommige oplossingen wordt extra software toohello agent leveren of vereisen dat software geïnstalleerde toocollect aanvullende gegevens.  Deze gegevens wordt doorgaans verzonden rechtstreeks tooLog Analytics.
* Sommige oplossingen worden gegevens verzameld rechtstreeks vanuit de SCOM-beheerservers die niet afkomstig is van het Hallo-agent.  Bijvoorbeeld, Hallo [waarschuwing beheeroplossing](https://technet.microsoft.com/library/mt484092.aspx) waarschuwingen verzamelt uit SCOM nadat ze zijn gemaakt.

## <a name="monitoring-logic"></a>Bewakingslogica
SCOM en Log Analytics werkt met vergelijkbare gegevens verzameld van agents maar fundamentele verschillen in hoe ze definiëren en implementeren van de logica voor het verzamelen van gegevens en hoe ze Hallo-gegevens die ze verzamelt analyseren hebben.

### <a name="operations-manager"></a>Operations Manager
Monitoringlogica voor SCOM is geïmplementeerd in [beheerpakketten](https://technet.microsoft.com/library/hh457558.aspx) die logica voor het detecteren van onderdelen toomonitor, Hallo status van deze onderdelen te meten en voor het verzamelen van gegevens tooanalyze bevatten.  Het bewaken van gegevens kan net zo eenvoudig als het verzamelen van een gebeurtenis of prestatiemeteritem, of deze complexe logica geïmplementeerd in een script kan gebruiken.  Management packs met volledige controle zijn beschikbaar voor een verscheidenheid aan [toepassingen van Microsoft en derden](http://go.microsoft.com/fwlink/?LinkId=82105) in toevoeging toohardware en netwerkapparaten.  U kunt [ontwerpen van uw eigen management packs](http://aka.ms/mpauthor) voor aangepaste toepassingen.

Management packs bevatten meerdere werkstromen die elk een afzonderlijke bewaking functie zoals steekproef van een prestatiemeteritem, Hallo status van een service te controleren of een script uitvoeren uitvoert.  Elke werkstroom wordt onafhankelijk uitgevoerd en definieert een eigen resultaten zoals welke database worden geschreven tooand of wordt een waarschuwing gegenereerd. 

U kunt details van de werkstroom zoals Hallo frequentie die ze worden uitgevoerd, Hallo drempelwaarde wanneer ze van mening zijn een fout en Hallo ernst van Hallo-waarschuwing genereren overschrijven.  U kunt ook aanvullende functionaliteit geven door uw eigen werkstromen toe te voegen.

![Onderdrukkingen](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Management packs zijn geïnstalleerd in Operations Manager-database Hallo en automatisch gedistribueerd tooagents door beheerservers.  Elke agent wordt automatisch downloaden van management packs en werkstromen relevante toohello toepassingen die ze hebben geïnstalleerd kunt laden.  Gegevens die worden verzameld door de agent Hallo geleverd back toohello beheerserver voor het invoegen in Hallo SCOM database en het datawarehouse.  Hallo Operations-Console kunt u tooview en deze gegevens via aangepaste weergaven, dashboards en rapporten in management pack voor Hallo analyseren.

Hallo-distributie van management packs wordt weergegeven in Hallo volgende diagram.

![Management pack-stroom](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Gebeurtenis- en Prestatieverzameling
Log Analytics verzamelt de gebeurtenissen en prestatiemeteritems van agent-systemen bronnen zoals Windows-gebeurtenislogboek, IIS-logboeken en Syslog.  U kunt criteria waarvoor gegevens worden verzameld via Hallo Log Analytics-portal en maak vervolgens logboek query's tooanalyze Hallo verzamelde gegevens definiëren.  Een reeks standaard criteria wordt gedefinieerd wanneer de OMS-werkruimte is gemaakt en u kunt extra gegevens voor specifieke toepassingen definiëren. 

![Het definiëren van gebeurtenislogboeken in Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Terwijl SCOM veel gedetailleerde werkstromen die meestal specifieke criteria voor gegevens en Hallo-actie die moet worden uitgevoerd in het antwoord heeft, heeft logboekanalyse meer algemene criteria voor het verzamelen van gegevens.  Logboek query's en oplossingen bieden meer gerichte criteria voor analyseren en stelt op specifieke gegevens in de cloud Hallo nadat deze is verzameld.

#### <a name="solutions"></a>Oplossingen
Oplossingen bieden aanvullende logica voor gegevens verzamelen en analyseren.  U kunt oplossingen tooadd tooyour OMS abonnement selecteren uit Hallo oplossing galerie.

![Galerie met oplossingen](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Oplossingen wordt voornamelijk in Hallo cloud bieden analyse van gebeurtenissen en prestatiemeteritems die worden verzameld in Hallo OMS opslagplaats uitgevoerd.  Ze kunnen ook aanvullende gegevens-toobe verzameld die kan worden geanalyseerd met logboek query's of door aanvullende gebruikersinterface van de oplossing in de OMS-dashboard Hallo Hallo definiëren. 

Bijvoorbeeld, Hallo [oplossing bijhouden](https://technet.microsoft.com/library/mt484099.aspx) detecteert configuratie wijzigingen op de agent-systemen en schrijft gebeurtenissen toohello OMS opslagplaats die kan worden geanalyseerd met verschillende grafische weergaven om samen te vatten wijzigingen gedetecteerd.  U kunt inzoomen op uit de weergave Hallo samengevat logboek query's die weergave Hallo gedetailleerde gegevens verzameld door Hallo-oplossing.

Terwijl u kunt selecteren welke oplossingen u tooyour abonnement toevoegt, moet u niet op dit moment Hallo mogelijkheid toocreate uw eigen oplossingen.  U kunt selecteren Hallo gebeurtenissen en prestatiemeteritems toocollect van prestaties en aangepaste weergaven op basis van uw eigen logboek query's maken.

Hallo monitoringlogica voor logboekanalyse wordt samengevat in de volgende diagram Hallo.

![Log Analytics-oplossing stroom](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Statuscontrole
### <a name="operations-manager"></a>Operations Manager
SCOM kunt Hallo verschillende onderdelen van een toepassing modelleren en geef een realtime status voor elk.  Hiermee kunt u toonot enige weergave gedetecteerd fouten en upprestaties gedurende een periode, maar ook toovalidate Werkelijke status van een toepassing of het systeem en elk van de onderdelen Hallo op elk moment.  Omdat wordt begrepen Hallo perioden die een toepassing beschikbaar is, ondersteunt Hallo health-engine in SCOM ook Service Level Agreements (SLA) die analyseren en rapporteren over Hallo beschikbaarheid van een toepassing gedurende een bepaalde periode.

Hallo weergave hieronder ziet u bijvoorbeeld Hallo realtime status van SQL database-engines bewaakt door SCOM.  status van elk van de databases voor een van de database-engines Hallo HALLO hallo wordt weergegeven op Hallo onder de helft van het Hallo-weergave.

![Statusweergave](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Hallo Health Explorer voor een van de database-engines Hallo hieronder met Hallo monitors met gebruikte toodetermine de algehele status.  Deze monitors zijn gedefinieerd in management pack voor SQL Hallo en uitvoeren op alle SQL database-engines gedetecteerd door SCOM.

![Health explorer](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Onderdelen op meerdere systemen kunnen gecombineerde toomeasure Hallo status van een gedistribueerde toepassing zijn.  Dit kan zijn bijzonder nuttig voor line-of-business-toepassingen die meerdere gedistribueerde onderdelen bevatten.  U kunt een model waarin Hallo status van elk onderdeel gemeten dat rollup maken in de beschikbaarheid van de toepassing hello.

Active Directory is een voorbeeld van een management pack dat voorziet in een model tooanalyze bijbehorende gedistribueerde onderdelen.  Hallo voorbeelddiagram hieronder toont Hallo status van Hallo algehele omgeving en Hallo relatie tussen forests, domeinen en domeincontrollers.  Elk van deze onderdelen bevat onderdelen en meerdere monitoren vergelijkbaar toohello SQL voorbeeld hierboven.

![De diagramweergave SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS niet bevatten een algemene engine toomodel toepassingen of de real-time status meten.  Afzonderlijke oplossingen kunnen beoordelen Hallo algemene status van bepaalde services op basis van de verzamelde gegevens en aangepaste regels kunnen worden geïnstalleerd op Hallo agent tooperform real-time analyse.  Omdat oplossingen worden uitgevoerd in de cloud Hallo met toegang toohello OMS-opslagplaats, kunnen ze vaak grondigere analyse dan gewoonlijk wordt uitgevoerd door management packs te bieden. 

Bijvoorbeeld, Hallo [AD-evaluatie en beoordeling van de SQL-oplossingen](https://technet.microsoft.com/library/mt484102.aspx) verzamelde gegevens te analyseren en geef een classificatie voor verschillende aspecten van Hallo-omgeving.  Het bevat aanbevelingen voor verbeteringen die tooimprove Hallo beschikbaarheid en prestaties van Hallo-omgeving kunnen worden gemaakt.

![Oplossing voor AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Data-analyse
SCOM en Log Analytics kunt u verschillende functies tooanalyze verzamelde gegevens leveren.  SCOM heeft weergaven en Dashboards in Hallo Operations-Console voor het analyseren van recente gegevens in verschillende indelingen en rapporten voor de presentatie van gegevens uit het datawarehouse Hallo in tabelvorm.  Log Analytics biedt een volledig logboek querytaal en interface voor het analyseren van gegevens in Hallo OMS-opslagplaats.  Wanneer SCOM wordt gebruikt als gegevensbron voor logboekanalyse, bevat Hallo opslagplaats gegevens verzameld door SCOM zodat Hallo Log Analytics-hulpprogramma's gebruikt tooanalyze gegevens van beide systemen worden kunnen.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Weergaven
Weergaven in Hallo Operations-Console kunt u de verschillende gegevenstypen tooview door SCOM in verschillende indelingen, doorgaans in tabelvorm voor gebeurtenissen, waarschuwingen, en gegevens van de gebruikersstatus en lijndiagrammen voor prestatiegegevens verzameld.  Weergaven uitvoeren minimale analyse of consolidatie van Hallo gegevens, maar kunnen u toofilter volgens tooparticular criteria. 

![Weergaven](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Management packs bieden doorgaans meerdere weergaven ondersteunende Hallo toepassings- of die deze controleert.  Dit kan zijn onder andere statusweergaven voor verschillende objecten Hallo die Hallo management pack detecteert, waarschuwingen voor gedetecteerde problemen, en prestatieweergaven voor items.

Weergaven zijn met name geschikt voor het analyseren van de huidige status Hallo van Hallo-omgeving met inbegrip van openstaande waarschuwingen en het Hallo-status van bewaakte systemen en objecten.  U kunt inzoomen toodetailed gebeurtenis of gegevens een bepaalde waarschuwing ondersteunende in volgorde toodiagnose de hoofdoorzaak. Op deze manier kunt u weergeven Hallo prestaties en status van de verschillende onderdelen van een toepassing tooassess de huidige status.

#### <a name="dashboards"></a>Dashboards
Dashboards in de Operations-Console voornamelijk werken met Hallo Hallo dezelfde gegevens, zoals maar meer aanpasbare en weergaven uitgebreidere visualisaties bevatten kunnen.  Een reeks standaard dashboards zijn beschikbaar u gemakkelijk kunt aanpassen voor uw eigen doeleinden.  U kunt ook een PowerShell-widget waarin gegevens uit een PowerShell-query zijn geretourneerd.

![Dashboard](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Ontwikkelaars hebben Hallo mogelijkheid tooadd aangepaste onderdelen toodashboards die ze in hun management packs opnemen.  Deze mogelijk bepaalde toepassing zeer gespecialiseerde tooa zoals Hallo dashboard in Hallo SQL management pack hieronder weergegeven.  Dit dashboard kan ook worden gebruikt als een sjabloon voor aangepaste versies.

![SQL-Dashboard](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Rapporten
Rapporten in SCOM analyseren van gegevens uit het datawarehouse Hallo in tabelvorm.  Ze kunnen worden afgedrukt en gepland voor de automatische levering in verschillende bestandsindelingen, met inbegrip van PDF- en CSV- en Word.  Rapporten werken met gegevens uit het datawarehouse Hallo zodat ze met name geschikt voor analyse van trends lange termijn.

Management packs wordt doorgaans aangepaste rapporten geven voor een bepaalde toepassing.  U kunt ook selecteren uit een bibliotheek met algemene rapporten die u aanpassen kunt voor uw eigen toepassingen of voor het uitvoeren van ad-hoc analyses.

Hier volgt een voorbeeldrapport prestaties door Active Directory Management Pack Hallo verzamelde gegevens worden weergegeven.

![Rapport](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Log Analytics is een [querytaal](https://technet.microsoft.com/library/mt484120.aspx) waarmee u tooperform analysis over gegevens van meerdere toepassingen zonder Hallo nodig toocreate een aangepaste weergave of het rapport kunt.  Omdat OMS is geïmplementeerd in de cloud hello, worden de prestaties van query's en analyse van gegevens zijn niet onderwerp tooany hardwarebeperkingen en query's, met inbegrip van miljoenen records snel kunt analyseren. 

Query's in logboekanalyse zijn ook Hallo op basis van andere functies.  U kunt een query opslaan, de tooExcel resultaten exporteren of dit wordt automatisch uitgevoerd met regelmatige tussenpozen en een waarschuwing genereren als de resultaten aan bepaalde criteria voldoen.  

![Logboek query stroom](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Hieronder volgt een voorbeeld van een Log Analytics-query.  In dit voorbeeld alle gebeurtenissen met de 'gestart' hello naam worden geretourneerd en gegroepeerd door gebeurtenis-id.  Hallo gebruiker biedt eenvoudig hello query en Log Analytics genereert dynamisch Hallo gebruikersinterface tooperform Hallo analyse.  Retourneert een item selecteren in lijst Hallo Hallo gedetailleerde gegevens van gebeurtenissen.

![Logboek query](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Bovendien tooproviding ad hoc analyse, query's in logboekanalyse kunnen worden opgeslagen voor toekomstig gebruik, en ook toegevoegde tooyour [OMS dashboard](http://technet.microsoft.com/library/mt484090.aspx) zoals weergegeven in Hallo voorbeeld te volgen.

![OMS-dashboard](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Volgende stappen
* Implementeer [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Aanmelden voor [logboekanalyse](https://azure.microsoft.com/documentation/services/log-analytics).  

