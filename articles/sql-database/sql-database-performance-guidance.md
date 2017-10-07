---
title: aaaAzure SQL Database-prestaties afstemmen richtlijnen | Microsoft Docs
description: In dit artikel kunt u bepalen welke service tier toochoose voor uw toepassing. Het ook aanbevolen manieren tootune uw toepassing tooget Hallo optimaal van Azure SQL Database.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Afstemming van de prestaties in Azure SQL Database

Azure SQL Database biedt [aanbevelingen](sql-database-advisor.md) dat kunt u tooimprove prestaties van uw database, of kunt u gebruiken om Azure SQL Database [automatisch aanpassen tooyour toepassing](sql-database-automatic-tuning.md) en wijzigingen toepassen die worden de prestaties van uw workload.

In dat u geen toepasselijke aanbevelingen, en u nog steeds prestatieproblemen, kunt u Hallo methoden tooimprove prestaties te volgen:
1. Verhogen [Servicelagen](sql-database-service-tiers.md) en bieden meer resources tooyour-database.
2. Uw toepassing afstemmen en enkele aanbevolen procedures die u kunnen de prestaties verbeteren van toepassing. 
3. Hallo database afstemmen door indexen en query's toomore efficiënt werken met gegevens te wijzigen.

Dit zijn handmatige methodes omdat u nodig toodecide wat hebt [Servicelagen](sql-database-service-tiers.md) kiest u of u zou moeten toorewrite toepassing of databasecode en deply Hallo wijzigingen.

## <a name="increasing-performance-tier-of-your-database"></a>Laag van de toenemende prestaties van uw database

Azure SQL Database biedt vier [Servicelagen](sql-database-service-tiers.md) die u kunt kiezen uit: Basic, Standard, Premium en Premium RS (prestaties wordt gemeten in database-eenheden voor doorvoer, of [dtu's](sql-database-what-is-a-dtu.md). Elke servicelaag isoleert strikt Hallo resources uw SQL-database kunt gebruiken, en wordt gegarandeerd dat voorspelbare prestaties voor dit serviceniveau. In dit artikel bieden we hulp kunt u ervoor kiezen de servicelaag Hallo voor uw toepassing. Dat kunt u uw toepassing tooget Hallo optimaal van Azure SQL Database afstemmen manieren ook besproken.

> [!NOTE]
> Dit artikel is gericht op prestaties richtlijnen voor individuele databases in Azure SQL Database. Zie voor instructies voor prestaties gerelateerde tooelastic pools [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool-guidance.md). Merk echter op dat u kunt toepassen veel Hallo aanbevelingen in dit artikel toodatabases in een elastische pool afstemmen en vergelijkbare prestatievoordelen ophalen.
> 

* **Basic**: Hallo Basic service tier aanbiedingen voorspelbaarheid goede prestaties voor elke database, uur ruim uur. In een Basic-database ondersteuning voldoende bronnen zijn voor goede prestaties in een kleine database die niet meerdere, gelijktijdige aanvragen. Er zijn typische gebruiksvoorbeelden wanneer u Basic servicelaag wilt gebruiken:
  * **U alleen aan de slag met Azure SQL Database**. Toepassingen die zich in ontwikkeling vaak hoeft geen hoge prestaties. Basic-databases zijn een ideale omgeving voor databaseontwikkeling of tests, tegen een lage prijs.
  * **U hebt een database met één gebruiker**. Toepassingen die meestal een enkele gebruiker aan een database koppelt hebt geen hoge gelijktijdigheid van taken en prestaties van de vereisten. Deze toepassingen zijn kandidaten voor Hallo Basic servicetier.
* **Standaard**: Hallo standaard servicelaag biedt verbeterde prestaties, voorspelbaarheid en biedt goede prestaties voor databases die meerdere gelijktijdige aanvragen, zoals werkgroep en webtoepassingen. Wanneer u een database van de laag Standard service kiest, u kunt het formaat van uw databasetoepassing op basis van voorspelbare prestaties, minuut gedurende een minuut.
  * **Uw database heeft meerdere gelijktijdige aanvragen**. Toepassingen die meer dan één gebruiker op een tijdstip meestal moeten hogere prestaties. Werkgroep- of webtoepassingen toepassingen met lage toomedium i/o-verkeer vereisten ondersteunen meerdere gelijktijdige query's zijn bijvoorbeeld geschikt voor Hallo standaard servicelaag.
* **Premium**: Hallo Premium servicecategorie voorziet in voorspelbare prestaties tweede via ten tweede voor elke database Premium. Wanneer u de Premium servicecategorie Hallo kiest, kunt u het formaat van uw databasetoepassing op basis van de piekbelasting Hallo voor die database. Hallo-abonnement verwijdert gevallen waarin prestaties van de variantie kleine query's tootake langer dan verwacht in latentie gevoelig bewerkingen kan veroorzaken. Dit model kan Hallo ontwikkelings- en validatie cycli voor toepassingen die toomake sterk instructies over de resourcebehoeften piek, prestaties van de variantie of latentie van query moeten sterk vereenvoudigen. De meeste Premium-laag service gebruiksvoorbeelden hebben een of meer van deze kenmerken:
  * **Hoge piekbelasting**. Een toepassing die is vereist aanzienlijk CPU, geheugen of input/output (I/O) toocomplete bewerkingen is vereist voor een specifieke, hoge prestaties. Een bekend tooconsume databasebewerking meerdere CPU-kernen voor een langere periode is bijvoorbeeld geschikt is voor de Premium servicecategorie Hallo.
  * **Veel gelijktijdige aanvragen**. Sommige databasetoepassingen-service is veel gelijktijdige aanvragen, bijvoorbeeld wanneer voor een website die een intensief verkeer. Basis en standaard Servicelagen Hallo aantal gelijktijdige aanvragen per database beperken. Toepassingen waarvoor meer verbindingen moet toochoose een juiste reservering grootte toohandle Hallo maximum aantal benodigde aanvragen.
  * **Lage latentie**. Sommige toepassingen moeten tooguarantee een reactie van Hallo-database in de minimale tijd. Als een specifieke opgeslagen procedure als onderdeel van een bredere klant-bewerking wordt aangeroepen, wellicht u een vereiste toohave een return-aanroep die in 99 procent van Hallo tijd niet meer dan 20 milliseconden. Dit type toepassing voordelen van de Premium servicecategorie hello, zorg ervoor dat deze Hallo vereiste rekenkracht toomake is beschikbaar.
* **Premium-RS**: Hallo Premium RS servicetier is ontworpen voor i/o-intensieve werkbelastingen die niet hoeven Hallo hoogste beschikbaarheidsgaranties. Voorbeelden omvatten het testen van werklasten met hoge prestaties of een analytische werkbelasting Hallo-database is waar geen Hallo-systeem van record.

Hallo serviceniveau dat u nodig hebt voor de SQL-database, is afhankelijk van Hallo piek load vereisten voor de resourcedimensie van elke. Sommige toepassingen een trivial bedrag van één resource gebruiken, maar belangrijke vereisten voor andere bronnen.

### <a name="service-tier-capabilities-and-limits"></a>Service tier mogelijkheden en beperkingen

Op elke servicelaag ingesteld prestatieniveau hello, zodat u Hallo flexibiliteit toopay alleen voor Hallo capaciteit die u nodig hebt. U kunt [aanpassen capaciteit](sql-database-service-tiers.md), omhoog of omlaag, omdat wijzigingen van de werkbelasting. Bijvoorbeeld als de werkbelasting van uw database tijdens Hallo terug naar school winkelwagen seizoen hoog is, kunt u verhogen Hallo prestatieniveau voor Hallo database gedurende een bepaalde periode, juli tot en met September. U kunt deze beperken wanneer uw seizoen piek wordt beëindigd. U betaalt door het optimaliseren van uw cloud omgeving toohello seizoensgebonden van uw bedrijf, kunt u minimaliseren. Dit model ook geschikt is voor software product release cycli. Een testteam mogelijk capaciteit toewijzen terwijl deze wordt uitgevoerd test en vervolgens die capaciteit vrijgeven wanneer ze klaar bent met testen. In een model van de aanvraag capaciteit betaalt u voor capaciteit terwijl u nodig hebt en besparen op toegewijde bronnen die u mogelijk zelden gebruikt.

### <a name="why-service-tiers"></a>Waarom Servicelagen?
Hoewel elke werkbelasting database verschillen kan, wordt in het Hallo-doel van Servicelagen tooprovide prestaties voorspelbaarheid op verschillende prestatieniveaus is. Klanten met grootschalige database resourcevereisten kunnen in een meer specifieke computeromgeving werken.

## <a name="tune-your-application"></a>Uw toepassing optimaliseren
Bij traditionele on-premises SQL Server is Hallo proces van de eerste capaciteitsplanning vaak gescheiden van Hallo proces van het uitvoeren van een toepassing in productie. Hardware- en licenties eerst zijn aangeschaft en prestatieafstemming later wordt uitgevoerd. Wanneer u Azure SQL Database gebruikt, is het een goed idee toointerweave Hallo proces van het uitvoeren van een toepassing en het afstemmen. Met de Hallo model van de capaciteit op aanvraag betaalt, kunt u uw toepassing toouse Hallo minimaal benodigde resources nu in plaats van overmatige inrichting op hardware gebaseerd op wat van toekomstige groeiplannen voor een toepassing die vaak onjuist afstemmen. Sommige klanten mogelijk niet tootune een toepassing te selecteren en in plaats daarvan kiezen toooverprovision hardwarebronnen. Deze aanpak mogelijk een goed idee als u niet dat toochange een sleutel toepassing gedurende een periode van bezet wilt. Maar afstemming van een toepassing kunt minimaliseren resourcevereisten en maandelijkse rekeningen te verlagen wanneer u de servicecategorieën Hallo in Azure SQL Database gebruikt.

### <a name="application-characteristics"></a>Kenmerken van toepassingen
Hoewel Azure SQL Database Servicelagen ontworpen tooimprove prestaties stabiliteit en voorspelbaarheid voor een toepassing zijn, kunt enkele aanbevolen procedures u uw toepassing toobetter profiteren van Hallo bronnen op een prestatieniveau van de te optimaliseren. Hoewel veel toepassingen hebben aanzienlijke prestatieverbeteringen gewoon door gegevenslaag tooa overschakelen hoger prestatieniveau of service vormt, bepaalde toepassingen nodig aanvullende afstemmen toobenefit van een hoger niveau van de service. Voor betere prestaties kunt u eventueel extra toepassing afstemmen voor toepassingen die de volgende kenmerken:

* **Toepassingen met trage prestaties vanwege 'chatty' gedrag**. Chatty toepassingen maken overmatige gegevenstoegangbewerkingen die gevoelige toonetwork latentie. Mogelijk moet u toomodify deze soorten toepassingen tooreduce Hallo aantal data access operations toohello SQL-database. Bijvoorbeeld, u mogelijk de toepassingsprestaties verbeteren door met behulp van technieken zoals ad-hocquery's batchverwerking of Hallo query toostored procedures te verplaatsen. Zie voor meer informatie [Batch-query's](#batch-queries).
* **Databases met een intensieve werkbelasting dat kan niet worden ondersteund door een volledige één machine**. Databases die groter is dan Hallo bronnen van het prestatieniveau van Hallo hoogste Premium nuttig Hallo werkbelasting uitbreiden. Zie voor meer informatie [tussen meerdere databases sharding](#cross-database-sharding) en [functionele partitioneren](#functional-partitioning).
* **Toepassingen die suboptimale query's hebben**. Toepassingen, met name voor die in Hallo gegevenstoegangslaag, die query's zijn niet goed zijn afgestemd niet nuttig een hoger prestatieniveau. Het gaat hierbij om query's die niet over een WHERE-component, indexen ontbrekende of verouderde statistieken. Deze toepassingen profiteren van de prestaties afstemmen standaard query-technieken. Zie voor meer informatie [ontbrekende indexen](#identifying-and-adding-missing-indexes) en [Query afstemmen en coderingstips](#query-tuning-and-hinting).
* **Toepassingen die suboptimale gegevens hebben toegang tot ontwerp**. Toepassingen die intrinsieke gegevens gelijktijdigheid toegangsproblemen, bijvoorbeeld deadlocking, hebben mogelijk niet profiteren van een hoger prestatieniveau. Overwegen retouren tegen hello Azure SQL Database met caching gegevens aan de clientzijde Hallo Hello Azure cache service of een andere caching-technologie. Zie [toepassing laag caching](#application-tier-caching).

## <a name="tune-your-database"></a>Uw database afstemmen
In dit gedeelte kijken we enkele technieken tootune Azure SQL Database toogain Hallo optimale prestaties gebruiken voor uw toepassing en voer deze uit op Hallo laagst mogelijke prestatieniveau. Enkele van de volgende manieren traditionele SQL Server best practices afstemmen overeenkomen, maar sommige specifieke tooAzure SQL-Database zijn. In sommige gevallen kunt u onderzoeken Hallo verbruikt resources voor een database toofind gebieden toofurther afstemmen en uitbreiden van traditionele SQL Server-technieken toowork in Azure SQL Database.

### <a name="identify-performance-issues-using-azure-portal"></a>Identificeren van prestatieproblemen met Azure portal
Hallo volgende hulpprogramma's in hello Azure-portal kunt u analyseren en oplossen van prestatieproblemen met uw SQL-database:

* [Inzicht in queryprestaties](sql-database-query-performance.md)
* [SQL Database Advisor](sql-database-advisor.md)

Hello Azure portal vindt u meer informatie over beide van deze hulpprogramma's en hoe toouse ze. tooefficiently opsporen en corrigeren van problemen, het is raadzaam dat u de eerste keer Hallo-hulpprogramma's in hello Azure-portal. Het is raadzaam dat u Hallo handmatige methoden die we vervolgens bespreken ontbrekende indexen en query afstemmen, in bijzondere gevallen afstemmen.

Meer informatie over het identificeren van problemen in Azure SQL Database op [prestatiebewaking](sql-database-single-database-monitor.md) artikel.

### <a name="identifying-and-adding-missing-indexes"></a>Te identificeren en ontbrekende indexen toe te voegen
Een veelvoorkomend probleem in de prestaties van de OLTP-database is gekoppeld toohello fysieke databaseontwerp. Vaak worden databaseschema ontworpen en getest op schaal (ofwel in load of gegevensvolume) verzonden. Helaas Hallo prestaties van een queryplan kan acceptabele op kleine schaal, maar aanzienlijk verslechteren onder productieniveau gegevensvolumes. Hallo meest voorkomende oorzaak van dit probleem is Hallo gebrek aan de juiste indexen toosatisfy filters of andere beperkingen in een query. Vaak ontbrekende indexen manifesten als een tabel als kan worden volstaan met een index seek scannen.

In dit voorbeeld gebruikt de geselecteerde queryplan Hallo een scan wanneer seek zou voldoende:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Het queryplan met ontbrekende indexen](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL Database kunt u zoeken naar en fix algemene ontbreken index voorwaarden. DMV's die zijn ingebouwd in Azure SQL Database bekijken querycompilaties waarin een index aanzienlijk sneller een Hallo geschatte kosten toorun een query. Tijdens het uitvoeren van query SQL-Database houdt hoe vaak elke queryplan wordt uitgevoerd en houdt Hallo geschatte hiaat tussen Hallo queryplan en Hallo uitvoeren maar één waar die index bestaat. U kunt deze DMV's tooquickly schatting welke wijzigingen tooyour fysieke databaseontwerp werkbelasting van de totale kosten voor een database en de werkelijke werkbelasting kan worden verbeterd.

U kunt deze query tooevaluate potentieel ontbrekende indexen gebruiken:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

In dit voorbeeld geeft Hallo query deze suggestie:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Nadat deze gemaakt, haalt die dezelfde SELECT-instructie een ander abonnement dat seek gebruikt in plaats van een scan, en vervolgens efficiënter uitgevoerd Hallo plannen:

![Een queryplan met de gecorrigeerde indexen](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

Hallo sleutel inzicht is die Hallo i/o-capaciteit van een gedeelde, grondstoffen system beperkter dan die van een speciale server-machine. Er is een premium op voor het minimaliseren van onnodige i/o-tootake maximaal voordeel van Hallo systeem in Hallo DTU van elke prestatieniveau van hello Azure SQL Database servicecategorieën. Juiste fysieke database ontwerpbeslissingen die kunnen aanzienlijk verbeteren Hallo latentie voor afzonderlijke query's, Hallo doorvoer van gelijktijdige aanvragen verwerkt per schaaleenheid verbeteren en Hallo kosten vereist toosatisfy Hallo query minimaliseren. Zie voor meer informatie over Hallo ontbreekt index DMV's [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Query afstemmen en coderingstips
Hallo queryoptimalisatie in Azure SQL Database is vergelijkbaar traditionele SQL Server toohello-queryoptimalisatie. De meeste Hallo aanbevolen procedures voor het afstemmen van query's en kennis Hallo redeneren model beperkingen voor queryoptimalisatie Hallo ook van toepassing tooAzure SQL-Database. Als u query's in Azure SQL Database afstemmen, krijgt u mogelijk Hallo extra voordeel cumulatieve resourcebehoeften verminderen. Uw toepassing mogelijk kunnen toorun, tegen lagere kosten dan een ruiseffect gelijkwaardige omdat kan worden uitgevoerd op een lager prestatieniveau.

Een voorbeeld die vaak worden uitgevoerd in SQL Server en dat geldt ook tooAzure SQL-Database is hoe Hallo queryparameters optimaliseren "bithandtekeningen'. Tijdens de compilatie evalueert queryoptimalisatie Hallo Hallo huidige waarde van een parameter toodetermine of meer optimale queryplan kan worden gegenereerd. Hoewel deze strategie vaak tooa queryplan dat zijn aanzienlijk sneller dan een plan dat is gecompileerd zonder bekende parameterwaarden leiden kan, momenteel het werkt dat zowel in SQL Server en in Azure SQL Database. Hallo-parameter is soms niet sniff, en soms Hallo-parameter is sniff maar Hallo gegenereerde plan is suboptimale voor de volledige set Hallo van parameterwaarden in een werkbelasting. Microsoft levert queryhints (richtlijnen) zodat u kunt meer doelbewust doel opgeven en Hallo standaardgedrag van de parameter het bewaken van netwerken negeren. Als u hints gebruikt, kunt u vaak gevallen waarin Hallo SQL Server of Azure SQL Database standaardgedrag imperfecte voor een specifieke klant werkbelasting oplossen.

Hallo volgende voorbeeld laat zien hoe Hallo queryprocessor een plan dat is suboptimale voor prestaties en resourcevereisten kan genereren. Dit voorbeeld ziet ook als u een hint query gebruikt, u query uitvoeren tijd- en vereisten voor de SQL-database verkleinen kunt:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

Hallo Setupcode maakt een tabel die Gegevensdistributie is vervormd. Hallo optimale query verschilt van de planning gebaseerd op welke parameter is geselecteerd. Helaas compileren niet Hallo plan cachegedrag altijd Hallo-query op basis van de meest voorkomende parameterwaarde Hallo. Het is dus mogelijk voor een toobe suboptimale plan in de cache opgeslagen en gebruikt voor meerdere waarden, zelfs wanneer een ander schema is mogelijk een betere keuze voor plan gemiddeld. Het queryplan Hallo maakt vervolgens twee opgeslagen procedures die identiek zijn, behalve dat een een hint speciale query heeft.

**Bijvoorbeeld: deel 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Bijvoorbeeld: deel 2**

(We raden u ten minste 10 minuten voordat u begint met deel 2 van Hallo bijvoorbeeld zodat Hallo resultaten zijn uniek is in de resulterende telemetriegegevens Hallo.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Elk deel van dit voorbeeld probeert een geparameteriseerde insert-instructie toorun 1000 keer (toogenerate een voldoende load toouse als een testgegevensset). Bij het uitvoeren van opgeslagen procedures, onderzoekt queryprocessor Hallo Hallo parameterwaarde die toohello procedure wordt doorgegeven tijdens de eerste compilatie (parameter ' bekijken'). Hallo-processor resulterende plan Hallo-cache en wordt gebruikt voor latere aanroepen, zelfs als de parameterwaarde Hallo verschilt. Hallo optimale planning kan niet worden gebruikt in alle gevallen. Soms moet u tooguide Hallo optimaliseren toopick een plan dat is beter geschikt voor gemiddelde geval Hallo in plaats van specifieke geval Hallo uit wanneer Hallo query voor het eerst is gecompileerd. In dit voorbeeld genereert Hallo initiële plan een plan 'scan', die alle rijen toofind elke waarde die overeenkomt met de parameter Hallo leest:

![Query afstemmen met behulp van een scan plannen](./media/sql-database-performance-guidance/query_tuning_1.png)

Aangezien we Hallo procedure uitgevoerd met behulp van Hallo waarde 1, Hallo resulterende plan is optimaal is voor Hallo waarde 1 maar suboptimale voor alle andere waarden in de tabel Hallo. Hallo resultaat waarschijnlijk niet wat u zou willen zijn als u toopick elk willekeurig plannen omdat Hallo plan traag meer en meer bronnen worden gebruikt.

Als u een test met Hallo uitvoert `SET STATISTICS IO` instellen te`ON`, Hallo logische scan werk in dit voorbeeld achter de schermen hello wordt uitgevoerd. U kunt zien dat er 1,148 leesbewerkingen gedaan door Hallo plan (dit is inefficiënt als Hallo gemiddelde geval tooreturn slechts één rij) zijn:

![Query afstemmen met behulp van een logische scan](./media/sql-database-performance-guidance/query_tuning_2.png)

Hallo secondegedeelte van Hallo voorbeeld maakt gebruik van een query hint tootell Hallo optimaliseren toouse een specifieke waarde tijdens de compilatie van Hallo. In dit geval u gedwongen wordt Hallo query processor tooignore Hallo waarde die wordt doorgegeven als parameter hello, en in plaats daarvan tooassume `UNKNOWN`. Dit verwijst tooa waarde Hallo gemiddelde frequentie in Hallo-tabel (tijdverschil worden genegeerd). Hallo resulterende plan is een seek op basis van een plan dat is sneller en gebruikt minder bronnen, gemiddeld dan Hallo plan in dit voorbeeld, deel 1:

![Query afstemmen met behulp van een query-hint](./media/sql-database-performance-guidance/query_tuning_3.png)

Ziet u Hallo effect in Hallo **sys.resource_stats** tabel (Er is een vertraging van Hallo tijd dat u Hallo test- en wanneer gegevens Hallo Hallo tabel gevuld uitvoeren). Voor dit voorbeeld, deel 1 uitgevoerd tijdens Hallo 22:25:00 tijdvenster en deel 2 om 22:35:00 uur uitgevoerd. Hallo eerdere tijdvenster gebruikt meer bronnen in dat tijdvenster dan hello later een (vanwege plan efficiëntieverbeteringen).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Prestatieafstemming voorbeeld queryresultaten](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Hoewel Hallo volume in dit voorbeeld opzettelijk klein is, kan Hallo effect van suboptimale parameters aanzienlijke vooral op database groter worden. Hallo verschil in uitzonderlijke gevallen mag tussen seconden voor snelle gevallen en uur trage gevallen.
> 
> 

U kunt controleren **sys.resource_stats** toodetermine of Hallo resource voor een test maakt gebruik van meer of minder resources dan een andere test. Als u gegevens vergelijken, scheidt u Hallo timing van tests zodat ze zich niet in Hallo dezelfde 5 minuten venster in Hallo **sys.resource_stats** weergeven. Hallo is doel van Hallo oefening toominimize Hallo totale hoeveelheid resources die worden gebruikt en niet toominimize Hallo piek bronnen. In het algemeen minder een stuk code voor latentie optimaliseren ook brongebruik. Zorg ervoor dat Hallo wijzigingen tooan toepassing nodig zijn en dat wijzigingen Hallo Hallo klantervaring voor iemand die queryhints in toepassing hello gebruikmaken mogelijk niet negatief beïnvloeden.

Als een werklast heeft een set met herhaalde query's, vaak er wordt zin toocapture en optimalisatie van uw keuzes plan Hallo valideren omdat deze de Hallo minimale grootte eenheid vereist toohost Hallo resourcedatabase. Het valideren van tijd tot tijd Hallo plannen dat toohelp u ervoor zorgen dat ze hebben niet is gedegradeerd te klikken. U kunt meer lezen over [hints (Transact-SQL) query](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Meerdere databases sharding
Omdat Azure SQL Database wordt uitgevoerd op basishardware, zijn Hallo capaciteitslimieten voor één database lager dan bij traditionele on-premises installatie van SQL Server. Sommige klanten gebruik sharding technieken toospread databasebewerkingen over meerdere databases wanneer Hallo bewerkingen niet binnen Hallo grenzen van een individuele database in Azure SQL Database passen. De meeste klanten die sharding technieken in Azure SQL Database gebruiken wordt hun gegevens op één dimensie verdelen over meerdere databases. Voor deze benadering moet u toounderstand OLTP-toepassingen voeren vaak transacties die betrekking hebben tooonly één rij of tooa kleine groep rijen in het Hallo-schema.

> [!NOTE]
> SQL-Database biedt nu een bibliotheek tooassist met sharding. Zie voor meer informatie [overzicht van clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md).
> 
> 

Bijvoorbeeld, als een database heeft de naam van de klant, volgorde en volgorde details (zoals Hallo traditionele voorbeeld Northwind database die wordt geleverd met SQL Server), u kan deze gegevens splitsen in meerdere databases door een klant Hello groepering verwante volgorde en volgorde details informatie. U kunt garanderen dat Hallo klantgegevens in een individuele database blijft staan. Hallo toepassing zou verschillende klanten verdelen over databases en effectief Hallo load verspreid over meerdere databases. Met sharding, klanten niet alleen kunnen voorkomen dat maximale limiet databasegrootte hello, maar Azure SQL Database ook werkbelastingen die aanzienlijk groter dan Hallo grenzen van de verschillende prestatieniveaus hello, zijn zolang elke afzonderlijke database in past kan verwerken ervan DTU.

Database sharding niet Hallo cumulatieve resourcecapaciteit voor een oplossing te verminderen, is het zeer effectief te ondersteunen van zeer grote oplossingen die worden verdeeld over meerdere databases. Elke database kunt uitvoeren op een andere prestaties niveau toosupport erg groot is, 'effectieve' databases met hoge benodigde middelen.

### <a name="functional-partitioning"></a>Functionele partities
SQL Server-gebruikers combineren vaak veel functies in één database. Bijvoorbeeld, als een toepassing logica toomanage inventaris voor een winkel heeft, wellicht dat de database logica die is gekoppeld aan Voorraadbeheer, inkoop, opgeslagen procedures en geïndexeerde of gerealiseerde weergaven die het einde van de maand rapportage beheren. Op deze manier kunt eenvoudiger tooadminister Hallo-database voor bewerkingen zoals back-up, maar het vereist dat u toosize Hallo hardware toohandle Hallo piekbelasting over alle functies van een toepassing.

Als u een uitbreidbare architectuur in Azure SQL Database gebruikt, is het een goed idee toosplit verschillende functies van een toepassing in andere databases. Met deze techniek kunnen schaalt elke toepassing onafhankelijk van elkaar. Als een toepassing veelgebruikte wordt (en belasting op Hallo database toeneemt Hallo) kunt Hallo beheerder onafhankelijke prestatieniveaus voor elke functie in Hallo-toepassing. Hallo-bereikt met deze architectuur kan een toepassing niet groter zijn dan een machine één product verwerken kan, omdat Hallo load is verdeeld over meerdere machines.

### <a name="batch-queries"></a>Batch-query 's
Voor toepassingen die toegang gegevens tot met behulp van hoog volume, regelmatig, ad hoc query wordt uitgevoerd, een aanzienlijke hoeveelheid reactietijd is besteed aan netwerkcommunicatie tussen Hallo toepassingslaag of hello Azure SQL Database. Zelfs wanneer beide Hallo zijn toepassings- en Azure SQL Database in hetzelfde Datacenter, Hallo netwerklatentie tussen twee Hallo kan worden vergroot door een groot aantal gegevenstoegangbewerkingen Hallo. tooreduce hello netwerk ronde reizen voor Hallo gegevens toegangsbewerkingen, overweeg Hallo optie tooeither batch Hallo ad-hocquery's of toocompile als opgeslagen procedures. Als u de ad-hocquery's Hallo batch, kunt u meerdere query's verzenden als één grote batch in een enkele reis tooAzure SQL-Database. Als u ad-hocquery's in een opgeslagen procedure compileert, kunt u hetzelfde resultaat als wanneer u deze batch Hallo kan bereiken. Met behulp van een opgeslagen procedure ook kunt u voordeel van het verhogen van de kans op Hallo van Hallo queryplannen in Azure SQL Database in het cachegeheugen zodat u Hallo kunt Hallo opgeslagen procedure opnieuw.

Sommige toepassingen zijn schrijven-intensief. U kunt soms Hallo totale i/o-belasting voor een database verminderen door rekening te houden hoe toobatch samen schrijft. Dit is vaak net zo eenvoudig als expliciete transacties via in plaats van automatisch doorvoeren transacties in de opgeslagen procedures en ad-hoc batches. Zie voor een evaluatie van verschillende technieken die u kunt gebruiken, [batchverwerking technieken voor toepassingen in Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Experimenteer met uw eigen werkbelasting toofind Hallo rechts model voor batchverwerking. Ervoor toounderstand die een model mogelijk enigszins worden verschillende transactionele consistentie gegarandeerd. Hallo rechts werkbelasting die gebruik van bronnen minimaliseert zoeken vereist Hallo combinatie van de consistentie en prestaties-en nadelen te zoeken.

### <a name="application-tier-caching"></a>Toepassingslaag caching
Sommige databasetoepassingen hebben lezen zware workloads. Opslaan in cache lagen Hallo belasting op Hallo database mogelijk te verminderen en mogelijk verkleint Hallo prestaties niveau vereist toosupport een database met behulp van Azure SQL Database. Met [Azure Redis-Cache](https://azure.microsoft.com/services/cache/), hebt u een werkbelasting lezen zware, vindt u Hallo gegevens eenmaal (of bijvoorbeeld eenmaal per toepassingslaag machine, afhankelijk van hoe deze is geconfigureerd), en die gegevens buiten uw SQL-database op te slaan. Dit is een manier tooreduce belasting van de database (CPU en i/o-lezen), maar er is een effect op transactionele consistentie omdat Hallo-gegevens lezen uit cache Hallo mogelijk niet gesynchroniseerd met de Hallo-gegevens in Hallo-database. Hoewel in veel toepassingen een zekere mate van inconsistentie acceptabel is, die geldt niet voor alle werkbelastingen. U moet eventuele toepassingsvereisten volledig begrijpen voordat u een toepassing lagen in het cachegeheugen strategie implementeert.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over Servicelagen [SQL Database-opties en prestaties](sql-database-service-tiers.md)
* Zie voor meer informatie over elastische pools [wat is er een Azure elastische groep?](sql-database-elastic-pool.md)
* Zie voor meer informatie over prestaties en elastische pools [wanneer tooconsider een elastische pool](sql-database-elastic-pool-guidance.md)

