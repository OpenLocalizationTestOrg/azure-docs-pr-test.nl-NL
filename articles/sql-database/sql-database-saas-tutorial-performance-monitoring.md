---
title: aaaMonitor prestaties van veel Azure SQL-databases in een multitenant SaaS-app | Microsoft Docs
description: Bewaken en beheren van de prestaties van databases en pools in hello Azure SQL Database Wingtip SaaS-app
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Bewaking van prestaties van Hallo Wingtip SaaS-toepassing

In deze zelfstudie worden de verschillende prestatie scenario's voor beheer in de SaaS-toepassingen gebruikt verkend. Met behulp van een activiteit load generator toosimulate voor alle databases van de tenant, worden Hallo ingebouwde bewaking en waarschuwingen functies van SQL-Database en elastische pools uitgelegd.

Hallo Wingtip SaaS app gebruikmaakt van een één-tenant-gegevensmodel waar elke locatie vast (tenant) hun eigen database heeft. Net als veel SaaS-toepassingen verwachten Hallo tenant werkbelasting patroon is onvoorspelbare en sporadisch. Met andere woorden, kaartverkoop kan op ieder moment plaatsvinden. tootake profiteren van deze databases meestal gebruikspatroon, tenant databases zijn geïmplementeerd in pools voor elastische databases. Elastische pools optimaliseren Hallo kosten van een oplossing die resources delen tussen meerdere databases. Met dit type patroon, is het belangrijk toomonitor database en groep resource gebruik tooensure dat wordt geladen redelijkerwijs verdeeld zijn over groepen. U moet ook tooensure of afzonderlijke databases voldoende resources hebt en dat groepen zijn niet kunt u door hun [eDTU](sql-database-what-is-a-dtu.md) limieten. Deze zelfstudie behandelt manieren toomonitor en beheren van databases en pools, en hoe tootake corrigerende maatregelen in antwoord toovariations in werkbelasting.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]

> * Gebruik op Hallo tenant databases door het uitvoeren van een opgegeven load generator simuleren
> * Monitor Hallo tenant zoals ze toohello toename van de load reageren-databases
> * Hallo opschalen met elastische pool in antwoord toohello toegenomen database laden
> * Een tweede elastische pool tooload saldo database activiteit inrichten


toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.

## <a name="introduction-toosaas-performance-management-patterns"></a>Inleiding tooSaaS prestaties management patronen

Het beheren van de prestaties van de database bestaat uit het compileren en prestatiegegevens analyseren en vervolgens reageren toothis gegevens door aan te passen parameters toomaintain een acceptabele reactietijd voor uw toepassing. Bij het hosten van meerdere tenants pools voor elastische databases zijn een rendabele manier tooprovide resources en beheren voor een groep van databases met onvoorspelbare werkbelastingen. Met bepaalde workloadpatronen kan het al bij twee S3-databases voordelig zijn om ze door een pool te laten beheren.

![media](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Pools en Hallo-databases in pools moet bewaakte tooensure ze binnen acceptabele prestaties blijven. Hallo groep configuratie toomeet Hallo behoeften van de cumulatieve werkbelasting Hallo van alle databases, ervoor te zorgen dat Hallo groepen met edtu's geschikt is voor Hallo stemmen Algehele werkbelasting. Hallo per database minimum- en per database max eDTU waarden tooappropriate waarden aanpassen voor uw specifieke vereisten.

### <a name="performance-management-strategies"></a>Strategieën voor prestatiebeheer

* tooavoid toomanually monitor prestaties, met het meest effectieve is te**waarschuwingen die wordt geactiveerd wanneer databases of groepen buiten het normale adresbereiken afwijken instellen**.
* toorespond tooshort term schommelingen in Hallo cumulatieve prestatieniveau van een groep Hallo **pool-eDTU niveau kan worden geschaald omhoog of omlaag**. Als deze fluctuatie op een basis reguliere of voorspelbare optreedt **schalen Hallo van toepassingen kan worden geplande toooccur automatisch**. U kunt bijvoorbeeld omlaag schalen wanneer de workload licht is, zoals 's nachts of tijdens het weekend.
* toorespond toolonger term schommelingen of wijzigingen in het aantal databases, Hallo **afzonderlijke databases kunnen worden verplaatst in andere groepen**.
* toename van de toorespond tooshort term *afzonderlijke* belasting van de database **afzonderlijke databases kunnen worden genomen buiten een pool en een afzonderlijke prestatieniveau toegewezen**. Zodra het Hallo laden wordt verminderd, kan Hallo-database vervolgens worden geretourneerd toohello van toepassingen. Wanneer dit van tevoren bekend, kunnen databases worden verplaatst pre-emptively tooensure Hallo-database heeft altijd Hallo resources moet en tooavoid impact op andere databases in de groep Hallo. Deze vereiste is voorspelbaar, zoals een u wilt een snel uitgevoerd van de verkoop ticket voor een populaire gebeurtenis voordoet, kan dit gedrag management worden geïntegreerd in de toepassing hello.

Hallo [Azure-portal](https://portal.azure.com) biedt ingebouwde bewaking en waarschuwingen op de meeste bronnen. Voor SQL Database zijn bewaking en waarschuwingen beschikbaar voor databases en pools. Deze ingebouwde bewaking en waarschuwingen is resource-specifieke, zodat het handige toouse voor een klein aantal bronnen is, maar niet erg handig is als u werkt met veel resources.

Voor grootschalige scenario's waarin u met veel reources werkt [logboekanalyse (OMS)](sql-database-saas-tutorial-log-analytics.md) kan worden gebruikt. Dit is een afzonderlijke Azure-service die in analyse via verzonden diagnostische logboeken en telemetrie verzameld in een log analytics-werkruimte voorziet. Log Analytics kunt verzamelen van telemetriegegevens van veel services en gebruikte tooquery en waarschuwingen instellen.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Hallo Wingtip toepassing broncode en scripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Extra tenants inrichten

Groepen kunnen zijn met slechts twee S3 databases rendabele, Hallo meer databases die zich in Hallo groep Hallo rendabeler Hallo gemiddelde van kracht wordt. U hebt voor deze zelfstudie ten minste 20 geïmplementeerde databases nodig om een goed inzicht te krijgen in de werking van het bewaken en beheren van prestaties op schaal.

Als u al een batch van tenants in een eerdere zelfstudie voorzien, gaat u verder toohello [simuleren-gebruik op alle databases van de tenant](#simulate-usage-on-all-tenant-databases) sectie.

1. Open... \\Learning-Modules\\prestatiebewaking en beheer\\*Demo PerformanceMonitoringAndManagement.ps1* in Hallo *PowerShell ISE*. Houd dit script open; u gaat verschillende scenario's uitvoeren tijdens deze zelfstudie.
1. Stel het volgende in: **$DemoScenario** = **1**, **Batch met tenants inrichten**
1. Druk op **F5** toorun Hallo script.

Hallo script implementeert 17 tenants in minder dan vijf minuten.

Hallo *nieuw TenantBatch* script maakt gebruik van een geneste of gekoppelde set [Resource Manager](../azure-resource-manager/index.md) sjablonen die maken van een batch-tenants, die standaard Hallo database kopieert **basetenantdb** op Hallo catalogus server toocreate Hallo nieuwe tenant-databases en vervolgens geregistreerd in de catalogus Hallo en ten slotte als wordt geïnitialiseerd met Hallo tenant naam en u wilt. Dit komt overeen met de Hallo manier Hallo app voorziet in een nieuwe tenant. Eventuele wijzigingen te*basetenantdb* toegepaste tooany nieuwe tenants daarna ingericht zijn. Zie Hallo [Schemabeheer zelfstudie](sql-database-saas-tutorial-schema-management.md) toosee hoe toomake schema te verandert*bestaande* tenant-databases (inclusief Hallo *basetenantdb* database).

## <a name="simulate-usage-on-all-tenant-databases"></a>Gebruik simuleren op alle tenantdatabases

Hallo *Demo PerformanceMonitoringAndManagement.ps1* script is opgegeven dat een werkbelasting die wordt uitgevoerd op alle databases van de tenant simuleert. Hallo load wordt gegenereerd met behulp van een Hallo beschikbare load-scenario's:

| Demo | Scenario |
|:--|:--|
| 2 | Belasting met normale intensiteit genereren (ongeveer 40 DTU's) |
| 3 | Load genereren met langere en frequentere bursts per database|
| 4 | Load genereren met meer DTU-bursts per database (ongeveer 80 DTU's)|
| 5 | Een normale load en hoge load genereren op één tenant (ongeveer 95 DTU's)|
| 6 | Niet-gebalanceerde load genereren voor meerdere pools|

Hallo load generator van toepassing is een *synthetische* alleen CPU-belasting tooevery tenant-database. Hallo generator start een taak voor elke tenant-database, die een opgeslagen procedure periodiek die Hallo load genereert aanroept. Hallo belastingsniveaus (in edtu's), duur en intervallen voor alle databases, onvoorspelbare tenant activiteit simuleren verspreid.

1. Open... \\Learning-Modules\\prestatiebewaking en beheer\\*Demo PerformanceMonitoringAndManagement.ps1* in Hallo *PowerShell ISE*. Houd dit script open; u gaat verschillende scenario's uitvoeren tijdens deze zelfstudie.
1. Stel **$DemoScenario** = **2**, *genereren normale intensiteit load*.
1. Druk op **F5** tooapply een load-tooall uw tenant-databases.

Wingtip is een SaaS-app en Hallo echte belasting van een SaaS-app is doorgaans sporadisch en onvoorspelbaar. toosimulate dit Hallo load generator produceert een willekeurige belasting verdeeld over alle tenants. Enkele minuten nodig zijn voor Hallo load patroon tooemerge, dus uitvoeren Hallo load generator gedurende 3-5 minuten voordat u probeert de werklast van toomonitor Hallo Hallo uit te voeren.

> [!IMPORTANT]
> Hallo load generator wordt uitgevoerd als een reeks taken in uw lokale PowerShell-sessie. Hallo houden *Demo PerformanceMonitoringAndManagement.ps1* tabblad is geopend. Als u Hallo tab sluiten of onderbreken van de computer, stopt Hallo load generator. Hallo load generator blijft in een *aanroepen van de taak* status waar belasting van een nieuwe tenants die zijn ingericht genereert nadat Hallo generator is gestart. Gebruik *Ctrl-C* toostop nieuwe taken en afsluiten Hallo script wordt aangeroepen. Hallo load generator blijven toorun, maar alleen op bestaande tenants.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Resourcegebruik hello Azure-portal met bewaken

toomonitor hello Resourcegebruik die resultaten van Hallo laden wordt toegepast, open Hallo portal toohello groep met Hallo tenant databases:

1. Open Hallo [Azure-portal](https://portal.azure.com) en blader toohello *tenants1 -&lt;gebruiker&gt;*  server.
1. Scrol naar beneden, zoek de elastische pools en klik op **Pool1**. Deze groep bevat alle Hallo tenant databases gemaakt tot nu toe.

Hallo observeren **elastische pool bewaking** en **elastische database bewaken** grafieken.

Hallo is Resourcegebruik van de groep van toepassingen Hallo statistische database gebruik voor alle databases in Hallo-groep. Hallo database diagram toont Hallo vijf gegevensbeheer databases:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Omdat er extra databases zijn in de groep Hallo buiten Hallo van bovenste vijf, Hallo groep gebruik toont activiteit die niet wordt weergegeven in het bovenste vijf databases grafiek Hallo. Klik voor meer informatie **Database Resourcegebruik**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Prestatiewaarschuwingen op Hallo van toepassingen instellen

Een waarschuwing instellen op Hallo van toepassingen die u activeert op \>75% gebruik als volgt:

1. Open *Pool1* (op Hallo *tenants1 -\<gebruiker\>*  server) in Hallo [Azure-portal](https://portal.azure.com).
1. Klik op **Waarschuwingsregels** en klik vervolgens op **+ Waarschuwing toevoegen**:

   ![waarschuwing toevoegen](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Geef een naam op, bijvoorbeeld **hoog DTU**.
1. Stel Hallo volgende waarden:
   * **Metriek = eDTU-percentage**
   * **Voorwaarde = groter dan**.
   * **Drempel = 75**.
   * **Periode = via Hallo afgelopen 30 minuten**.
1. Toevoegen van een e-mailadres toohello *aanvullende beheerder email(s)* vak en klikt u op **OK**.

   ![waarschuwing instellen](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Een zwaar belaste pool omhoog schalen

Als Hallo cumulatieve load niveau op een groep toohello verhoogt dat het Hallo-pool maximaliseert en 100% eDTU-gebruik is bereikt, wordt klikt u vervolgens afzonderlijke databaseprestaties beïnvloed, mogelijk vertraging query responstijden voor alle databases in Hallo-groep.

**Korte termijn**, overweeg schaalt Hallo groep tooprovide aanvullende bronnen, of databases te verwijderen uit groep hello (verplaatsen van opslaggroepen tooother, of buiten het zelfstandige groepservicelaag tooa Hallo).

**Lange termijn**, u kunt query's of gebruik tooimprove databaseprestaties index. Afhankelijk van Hallo van de toepassing gevoeligheid tooperformance, verstrekt de best practice tooscale een pool van voordat het eDTU-gebruik van 100% is bereikt. Gebruik een waarschuwing toowarn u van tevoren.

Door toenemende Hallo belasting die wordt geproduceerd door Hallo generator, kunt u een groep bezet simuleren. Waardoor Hallo databases tooburst vaker en voor statistische load langer, toenemende Hallo op Hallo van toepassingen zonder Hallo vereisten van de afzonderlijke databases Hallo. Hallo groep schaalt gebeurt eenvoudig in Hallo-portal of PowerShell. In deze oefening gebruikt Hallo-portal.

1. Stel *$DemoScenario* = **3**, _load genereren met langer en vaker bursts per database_ tooincrease Hallo intensiteit van Hallo cumulatieve belasting op Hallo-pool zonder Hallo piekbelasting vereist voor elke database.
1. Druk op **F5** tooapply een load-tooall uw tenant-databases.

1. Ga te**Pool1** in hello Azure-portal.

Monitor Hallo eDTU-gebruik van toepassingen op de bovenste grafiek Hallo verhoogd. Het duurt enkele minuten voordat Hallo nieuwe hogere belasting tookick, maar ziet u snel Hallo van toepassingen starten toohit max gebruik, en als Hallo load steadies in het nieuwe patroon Hallo, het Hallo-groep snel overloads.

1. tooscale up Hallo-groep, klikt u op **pool configureren** bovenaan Hallo Hallo **Pool1** pagina.
1. Hallo aanpassen **groeps-eDTU** instellen te**100**. Hallo groeps-eDTU verandert niet Hallo per database-instellingen (dit is nog steeds 50 eDTU max per database). U ziet Hallo per database-instellingen aan de rechterkant Hallo Hallo **pool configureren** pagina.
1. Klik op **opslaan** toosubmit Hallo aanvraag tooscale Hallo van toepassingen.

Ga terug te**Pool1** > **overzicht** tooview Hallo bewaking grafieken. Hallo effect van het bieden van Hallo van toepassingen met meer bronnen (Hoewel u met enkele databases en een willekeurige belasting is het niet altijd eenvoudig toosee afdoende totdat u enige tijd uitvoert) controleren. Terwijl u bekijkt hello grafieken voorzien zijn rekening dan 100% op Hallo bovenste wordt nu grafiek vertegenwoordigt 100 edtu's, hoewel op Hallo lager is 100% van de grafiek is nog steeds 50 edtu's als Hallo per database max nog steeds 50 edtu's.

Databases blijft online en volledig beschikbaar tijdens Hallo-proces. Momenteel Hallo zijn laatste ogenblik omdat elke database klaar toobe ingeschakeld met nieuwe groeps-eDTU hello, alle actieve verbindingen verbroken. Toepassingscode altijd worden geschreven verbindingen tooretry verwijderd, en dus verbinding toohello database in Hallo omhoog geschaalde-pool wordt hersteld.

## <a name="load-balance-between-pools"></a>Taakverdeling tussen mediagroepen

Als een alternatieve tooscaling up Hallo-groep, een tweede pool maken en verplaatsen van databases in de App toobalance Hallo laden tussen Hallo twee groepen. Deze nieuwe pool Hallo moet worden gemaakt op toodo Hallo dezelfde server als Hallo eerst.

1. In Hallo [Azure-portal](https://portal.azure.com)Open Hallo **tenants1 -&lt;gebruiker&gt;**  server.
1. Klik op **+ nieuwe pool** toocreate een pool op Hallo huidige server.
1. Op Hallo **pool voor elastische database** sjabloon:

    1. Stel **naam** te*Pool2*.
    1. Hallo prijscategorie als laat **Standaardpool**.
    1. Klik op **Groep configureren**.
    1. Stel **groeps-eDTU** te*50 eDTU*.
    1. Klik op **databases toevoegen** toosee een lijst met databases op Hallo-server die te kunnen worden toegevoegd*Pool2*.
    1. Selecteer elke 10 databases toomove deze nieuwe toohello van toepassingen en klik vervolgens op **Selecteer**. Als Hallo load generator aan u is uitgevoerd, weet Hallo-service al dat uw profiel prestaties vereist een grotere groep dan de standaardgrootte 50 eDTU Hallo raadt aan om te beginnen met een 100 eDTU-instelling.

    ![Aanbeveling](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Voor deze zelfstudie laat Hallo standaard op 50 edtu's en op **Selecteer** opnieuw.
    1. Selecteer **OK** toocreate Hallo nieuwe pool en toomove Hallo databases geselecteerd in de App.

Hallo-toepassingen maken en verplaatsen van databases Hallo duurt een paar minuten. Zoals databases, ze online en toegankelijk blijven totdat Hallo laatste tijdstip verplaatst worden, waarna worden alle geopende verbindingen gesloten. Zolang u een aantal Pogingslogica hebt, maken clients toohello database in de nieuwe groep Hallo vervolgens verbinding.

Te bladeren**Pool2** (op Hallo *tenants1* server) tooopen Hallo van toepassingen en zijn prestaties controleren. Als u deze niet ziet, wacht u totdat het inrichten van de nieuwe groep toocomplete Hallo.

U ziet nu dat Resourcegebruik op *Pool1* is verwijderd en dat *Pool2* nu op dezelfde manier is geladen.

## <a name="manage-performance-of-a-single-database"></a>Prestaties van één database beheren

Als een individuele database in een pool een continue hoge belasting, afhankelijk van de configuratie van de groep Hallo krijgt, kan het vaak toodominate Hallo resources in de groep Hallo en invloed zijn op andere databases. Als Hallo activiteit waarschijnlijk toocontinue gedurende een bepaalde periode, kan de Hallo database tijdelijk worden verplaatst buiten het Hallo-groep. Hierdoor kunnen extra bronnen nodig heeft en andere databases geïsoleerd van Hallo Hallo database toohave Hallo.

In deze oefening simuleert Hallo effect van Contoso overleg Hall overbelast wanneer tickets verkoop voor een populaire samen.

1. Open Hallo... \\ *Demo PerformanceMonitoringAndManagement.ps1* script.
1. Stel het volgende in: **$DemoScenario = 5, Een normale load en hoge load genereren op één tenant (ongeveer 95 DTU's).**
1. Stel **$SingleTenantDatabaseName = contosoconcerthall** in
1. Uitvoeren van script met behulp van Hallo **F5**.


1. In Hallo [Azure-portal](https://portal.azure.com) openen **Pool1**.
1. Hallo inspecteren **elastische pool bewaking** grafiek en zoekt u Hallo verhoogd pool-eDTU-gebruik. Na een minuut of twee Hallo hogere belasting tookick in moet beginnen en ziet u snel dat Hallo groep treffers 100% gebruik.
1. Hallo inspecteren **elastische database bewaken** weergave waarin Hallo gegevensbeheer databases in Hallo afgelopen uur. Hallo *contosoconcerthall* database moet binnenkort worden weergegeven als een van de populairste databases Hallo vijf.
1. **Klik op het Hallo elastische database bewaken** **grafiek** en deze wordt geopend Hallo **Database Resourcegebruik** pagina waar u een van de databases Hallo kunt bewaken. Hiermee kunt u weergeven voor Hallo Hallo isoleren *contosoconcerthall* database.
1. Hallo-lijst met databases, klik op **contosoconcerthall**.
1. Klik op **prijscategorie (schaal dtu's)** tooopen hello **prestaties configureren** pagina waarin u een zelfstandige prestatieniveau voor Hallo database kunt instellen.
1. Klik op Hallo **standaard** tooopen Hallo schalingsopties in Hallo standaardcategorie tabblad.
1. Schuif Hallo **DTU schuifregelaar** tooright tooselect **100** dtu's. Dit komt overeen met de servicedoelstelling toohello Opmerking **S3**.
1. Klik op **toepassen** toomove Hallo database buiten het Hallo-toepassingen, waardoor het een *Standard-S3* database.
1. Zodra de schaal is voltooid, monitor Hallo effect op Hallo contosoconcerthall database en Pool1 op Hallo elastische toepassingen en de databasegegevens blades.

Zodra het Hallo hoge belasting van Hallo contosoconcerthall database subsidies retourneer het toohello groep tooreduce de kosten. Als het is onduidelijk wanneer dat gebeurt u kan een waarschuwing op Hallo database instellen die wordt geactiveerd wanneer de DTU-gebruik onder Hallo per database zakt max op Hallo van toepassingen. Het verplaatsen van een database naar een pool wordt beschreven in oefening 5.

## <a name="other-performance-management-patterns"></a>Andere patronen voor prestatiebeheer

**Preventieve schalen** In Hallo oefening waar u verkend hoe tooscale een geïsoleerde-database, u kent welke toolook database voor. Als het Hallo-beheer van Contoso overleg Hall had op de hoogte Wingtips van Hallo aanstaande ticket verkoop, kan Hallo-database zijn verplaatst buiten het Hallo-pool pre-emptively. Anders wordt moest deze waarschijnlijk worden een waarschuwing op Hallo van toepassingen of Hallo database toospot wat is er gebeurt. Je wilt niet dat toolearn hierover van Hallo andere tenants in Hallo groep klagen van verminderde prestaties. En als Hallo tenant kan voorspellen hoe lang ze aanvullende bronnen moet u een Azure Automation runbook toomove Hallo database buiten Hallo van toepassingen instellen en vervolgens weer op een ingesteld schema.

**Tenant selfservice schalen** omdat het schalen van een taak eenvoudig via Hallo management API aangeroepen, kunt u eenvoudig hello mogelijkheid tooscale tenant databases bouwen in uw toepassing tenant gerichte en aanbieden als onderdeel van uw SaaS-service. Laat bijvoorbeeld tenants self-administer omhoog en omlaag schalen mogelijk rechtstreeks gekoppelde tootheir facturering!

**Een pool schalen omhoog en omlaag van de gebruikspatronen van een planning toomatch**

Wanneer het gebruik van de cumulatieve tenant volgt voorspelbare gebruikspatronen, kunt u Azure Automation tooscale een pool omhoog en omlaag volgens een schema. Schaal een pool bijvoorbeeld omlaag na 18:00 uur en weer omhoog vóór 06:00 op dagen waarvan u weet dat er een afname in de benodigde resources is.



## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Gebruik op Hallo tenant databases door het uitvoeren van een opgegeven load generator simuleren
> * Monitor Hallo tenant zoals ze toohello toename van de load reageren-databases
> * Hallo opschalen met elastische pool in antwoord toohello toegenomen database laden
> * Een tweede elastische pool tooload saldo Hallo databaseactiviteiten inrichten

[Zelfstudie Een individuele tenant terugzetten](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Aanvullende bronnen

* Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassingsimplementatie bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastische SQL-pools](sql-database-elastic-pool.md)
* [Azure Automation](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md): zelfstudie Log Analytics instellen en gebruiken
