---
title: het compatibiliteitsniveau aaaDatabase 130 - Azure SQL Database | Microsoft Docs
description: In dit artikel we Hallo voordelen van uw Azure SQL Database op compatibiliteitsniveau 130 uitgevoerd en gebruik van de voordelen van de nieuwe queryoptimizer Hallo Hallo verkennen en processorfuncties opvragen. We ook betrekking op Hallo mogelijk neveneffecten op Hallo queryprestaties voor Hallo bestaande SQL-toepassingen.
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Verbeterde prestaties van query's met de compatibiliteit van niveau 130 in Azure SQL Database
Azure SQL-Database is actief transparant honderden of duizenden databases op veel verschillende compatibiliteitsniveaus behouden en garanderen Hallo achterwaartse compatibiliteit toohello bijbehorende versie van Microsoft SQL Server voor alle klanten!

In dit artikel we Hallo voordelen van uw Azure SQL-database op compatibiliteitsniveau 130 uitgevoerd en gebruik van de voordelen van de nieuwe queryoptimizer Hallo Hallo verkennen en processorfuncties opvragen. We ook betrekking op Hallo mogelijk neveneffecten op Hallo queryprestaties voor Hallo bestaande SQL-toepassingen.

Als een herinnering geschiedenis Hallo uitlijning van de SQL-versies toodefault compatibiliteitsniveaus zijn als volgt uit:

* 100: in SQL Server 2008 en Azure SQL Database V11.
* 110: in SQL Server 2012 en Azure SQL Database V11.
* 120: in SQL Server 2014 en Azure SQL Database V12.
* 130: in SQL Server 2016 en Azure SQL Database V12.

> [!IMPORTANT]
> Vanaf **medio juni 2016**, in Azure SQL Database worden Hallo standaard compatibiliteitsniveau 130 in plaats van 120 voor **nieuw gemaakte** databases.
> 
> Databases die zijn gemaakt vóór medio juni 2016 wordt *niet* worden beïnvloed en onderhouden hun huidige compatibiliteitsniveau (100, 110 of 120). Databases die worden gemigreerd vanuit Azure SQL Database-versie V11 tooV12 heeft een compatibiliteitsniveau van 100 of 110. 
> 

## <a name="about-compatibility-level-130"></a>Over het compatibiliteitsniveau 130
Als u tooknow Hallo huidige compatibiliteitsniveau van uw database wilt, uitvoeren eerst Hallo volgende Transact-SQL-instructie.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Voordat u deze wijziging toolevel 130 gebeurt voor **zojuist** databases gemaakt, gaan we controleren wat deze wijziging alles over via een zeer eenvoudige query voorbeelden en Zie hoe iedereen kan profiteren van deze.

Verwerking van query's in relationele databases kan zeer complex en toolots van gedrag en computer wetenschap en wiskunde toounderstand Hallo inherente ontwerpbeslissingen die kan leiden. In dit document is Hallo inhoud opzettelijk vereenvoudigde tooensure iedereen met een minimale technische achtergrond kunt Hallo het effect van wijzigingen in compatibiliteit Hallo en bepalen hoe deze toepassingen kan profiteren.

We hebben een kort overzicht van het compatibiliteitsniveau van welke Hallo 130 op Hallo tabel brengt.  U vindt meer informatie op [ALTER databasecompatibiliteitsniveau (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), maar hier een korte samenvatting volgt:

* Hallo Insert-bewerking van een instructie Insert select kan met meerdere threads of kan een parallel plan, terwijl voordat deze bewerking één thread is.
* Geheugen geoptimaliseerde tabel- en tabel variabelen query's zijn nu parallelle plannen tijdens voordat deze bewerking is ook één thread.
* Statistieken voor de tabel geoptimaliseerd voor geheugen kan nu door actieve en worden automatisch bijgewerkt. Zie [What's New in Database-Engine: In het geheugen OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) voor meer informatie.
* Batch-modus v/s rij-modus wordt gewijzigd met de kolom-indexen
  * Sorteren op een tabel met een index kolom worden nu in batchmodus.
  * Windowing statistische functies worden nu in batchmodus zoals TSQL LAG/LEAD instructies werken.
  * Query's op kolom Store tabellen met meerdere afzonderlijke componenten werken in batchmodus.
  * Query's onder DOP = 1 of met een seriële plan ook uit te voeren in de batchmodus.
* Laatste Kardinaliteitsschatting verbeteringen daadwerkelijk afkomstig zijn met een compatibiliteitsniveau 120, maar voor de uitgevoerd op een lager compatibiliteitsniveau (dat wil zeggen 100 of 110), hello verplaatsen toocompatibility niveau 130 ook ervoor zorgt dat deze verbeteringen en deze kunnen ook Hallo query-prestaties van uw toepassingen profiteren.

## <a name="practicing-compatibility-level-130"></a>Compatibiliteitsniveau 130 oefenen
Eerste we ophalen bepaalde tabellen, indexen en willekeurige gegevens die zijn gemaakt toopractice enkele van deze nieuwe functies. Voorbeelden van Hallo TSQL-scripts kunnen worden uitgevoerd onder de SQL Server 2016, of Azure SQL Database. Bij het maken van een Azure SQL database, zorg er echter u ten minste twee cores tooallow multithreading op Hallo minimaal een P2 database omdat moet u ervoor kiezen en daarom profiteren van deze functies.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Nu gaan we hebben een toosome uiterlijk van Hallo Query verwerken functies met een compatibiliteitsniveau 130 binnenkort.

## <a name="parallel-insert"></a>Parallelle invoegen
Hallo invoegbewerking onder compatibiliteitsniveau 120 en 130 die respectievelijk Hallo INSERT-bewerking wordt uitgevoerd in één thread-model (120) en in een multithreaded model (130) uitvoeren Hallo TSQL-instructies die hieronder worden uitgevoerd.

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Door het aanvragen van Hallo werkelijke Hallo queryplan, kijken naar de grafische weergave of de XML-inhoud, kunt u bepalen welke Kardinaliteitsschatting functie op play is. U bekijkt hello plannen side-by-side in afbeelding 1, duidelijk ziet u dat Hallo kolom Store invoegen uitvoering gaat van seriële in 120 tooparallel in 130. Let ook die wijziging Hallo van Hallo iterator-pictogram in 130 Hallo-indeling met twee parallelle pijlen, inderdaad parallelle ter illustratie van Hallo feit dat nu Hallo iterator-uitvoering is. Als u grote INSERT operations toocomplete hebt, functioneren Hallo parallelle uitvoering, het aantal core die u tot uw beschikking staan voor Hallo-database hebt, gekoppelde toohello beter; afhankelijk van uw situatie up tooa 100 maal sneller!

*Afbeelding 1: Bewerking wijzigingen uit seriële tooparallel met compatibiliteitsniveau 130 invoegen.*

![Afbeelding 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>SERIËLE batchmodus
Op deze manier kunt verplaatsen toocompatibility niveau 130 bij het verwerken van de rijen met gegevens batchverwerking modus. Modus batchbewerkingen zijn eerst alleen beschikbaar wanneer u beschikken over een columnstore-index. Ten tweede een batch doorgaans ~ 900 rijen vertegenwoordigt en gebruikt een code-logica geoptimaliseerd voor multicore CPU, hogere geheugendoorvoer en rechtstreeks maakt gebruik van gecomprimeerde gegevens van de kolom Store waar mogelijk Hallo Hallo. In deze omstandigheden SQL Server 2016, kunnen verwerken ~ 900 rijen in één keer in plaats van 1 rij tijdens hello, en als gevolg hiervan hello algemene overheadkosten Hallo-bewerking wordt nu gedeeld door Hallo hele batch, verminderen Hallo algehele kosten per rij. Deze gedeelde hoeveelheid van bewerkingen in wezen in combinatie met Hallo kolom store compressie vermindert Hallo latentie betrokken is bij een bewerking SELECT batch-modus. U kunt meer informatie vinden over Hallo kolom store en batch-modus met [Columnstore-indexen handleiding](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Als daaronder weergegeven ziet door observeren Hallo query plannen side-by-side in afbeelding 2 u dat Hallo verwerkingsmodus is gewijzigd met een compatibiliteitsniveau Hallo en als gevolg hiervan, wanneer u helemaal Hallo query's uitvoert in beide compatibiliteitsniveau, u dat ziet de meeste Hallo verwerkingstijd is besteed in de rij modus (% 86) vergeleken toohello batchmodus (14%), waarbij 2 batches is verwerkt. Hallo-gegevensset te verhogen, hello voordeel wordt verhoogd.

*Afbeelding 2: Selecteer bewerking wijzigingen van de seriële toobatch modus met compatibiliteitsniveau 130.*

![Afbeelding 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Batchmodus bij sorteren van uitvoering
Vergelijkbare toohello hierboven, maar de sorteerbewerking toegepaste tooa, Hallo overgang van de rij-modus (compatibiliteitsniveau 120) toobatch modus (compatibiliteitsniveau 130) verbetert de prestaties van Hallo Hallo sorteerbewerking voor Hallo dezelfde redenen.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Zichtbaar side-by-side in afbeelding 3, ziet u dat de sorteerbewerking Hallo in rijmodus 81% Hallo kosten, terwijl de batchmodus Hallo alleen 19% van Hallo kosten (respectievelijk 81% en 56% op Hallo sorteren zelf vertegenwoordigt) vertegenwoordigt.

*Afbeelding 3: De sorteerbewerking verandert van rij toobatch modus met compatibiliteitsniveau 130.*

![Afbeelding 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Uiteraard verloopt bevatten deze voorbeelden alleen tienduizenden rijen, die is niets wanneer bekijkt hello gegevens beschikbaar zijn in de meeste SQL Servers tegenwoordig. Deze tegen miljoenen rijen in plaats daarvan NET project en dit zich vertalen in enkele minuten voor uitvoering elke dag in behandeling zijnde Hallo aard van uw werkbelasting wordt bespaard.

## <a name="cardinality-estimation-ce-improvements"></a>Verbeteringen in kardinaliteit schatting (CE)
Met SQL Server 2014 geïntroduceerd, een database die wordt uitgevoerd op een compatibiliteitsniveau 120 of hoger maakt gebruik van Hallo nieuwe kardinaliteit schatten functionaliteit. Kardinaliteitsschatting is in wezen Hallo logica gebruikt toodetermine hoe een query op basis van de geschatte kosten op SQL server wordt uitgevoerd. Hallo schatting wordt berekend met behulp van de invoer van statistieken die zijn gekoppeld aan de objecten die zijn betrokken bij deze query. Vrijwel, op een hoog niveau Kardinaliteitsschatting functies zijn rij aantal samen met informatie over het Hallo-distributie van Hallo waarden, unieke waarde aantallen en dubbele aantallen opgenomen in Hallo tabellen en de objecten waarnaar wordt verwezen in Hallo-query. Ophalen van deze schattingen onjuist is, kan leiden toounnecessary schijf-i/o vanwege tooinsufficient geheugen verleent (dat wil zeggen TempDB morsen) of tooa selectie van een seriële plan kan worden uitgevoerd via een parallelle uitvoering, tooname plannen enkele. Sluiting, onjuist maakt een schatting kunnen leiden tot tooan verslechtering van de algehele prestaties van Hallo queryuitvoering. Hallo op de andere zijde, betere schattingen, nauwkeuriger schattingen, potentiële klanten toobetter query uitvoeringen!

Zoals al eerder vermeld, query optimalisaties en maakt een schatting van een complexe materie, maar als u meer informatie over het queryplannen en kardinaliteitsschatter toolearn wilt, kunt u toohello document op verwijzen [uw queryplannen optimaliseren Hello SQL Server 2014 Kardinaliteitsschatter](https://msdn.microsoft.com/library/dn673537.aspx) voor meer informatie.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Welke Kardinaliteitsschatting momenteel gebruikt u?
toodetermine onder welke Kardinaliteitsschatting uw query's worden uitgevoerd, gaan we zojuist gebruik Hallo query hieronder voorbeelden. Houd er rekening mee dat het eerste voorbeeld wordt uitgevoerd onder het compatibiliteitsniveau 110, wat impliceert Hallo gebruik van Hallo oude Kardinaliteitsschatting functies.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Zodra de uitvoering is voltooid, klikt u op Hallo XML-koppeling en bekijkt hello eigenschappen van de eerste iterator Hallo zoals hieronder wordt weergegeven. Houd er rekening mee Hallo eigenschapsnaam CardinalityEstimationModelVersion die is ingesteld op 70 aangeroepen. Het betekent niet dat het databasecompatibiliteitsniveau Hallo toohello SQL Server 7.0 versie (deze is ingesteld op 110 als zichtbaar in Hallo TSQL-instructies hierboven) is ingesteld, maar Hallo waarde 70 enkel Hallo verouderde Kardinaliteitsschatting functionaliteit beschikbaar sinds SQL vertegenwoordigt Server 7.0, waarvoor geen belangrijke wijzigingen tot SQL Server 2014 (die wordt geleverd met een compatibiliteitsniveau van 120).

*Afbeelding 4: Hallo CardinalityEstimationModelVersion is ingesteld too70 wanneer u een compatibiliteitsniveau 110 of onder.*

![Afbeelding 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

U kunt ook kunt u wijzigen Hallo compatibiliteit niveau too130, en Hallo gebruik van de functie voor nieuwe Kardinaliteitsschatting Hallo uitschakelen met behulp van Hallo LEGACY_CARDINALITY_ESTIMATION ingesteld tooON met [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). Dit zal worden exact Hallo dezelfde zijn als het gebruik van 110 van een schatting van de kardinaliteit-functie tijdens het gebruik van Hallo nieuwste queryverwerking compatibiliteitsniveau. Als u dit doet, kunt u profiteren van nieuwe Hallo-query verwerken functies afkomstig met de meest recente compatibiliteitsniveau hello (dat wil zeggen batchmodus), maar nog steeds zijn afhankelijk van Hallo oude kardinaliteit schatten functionaliteit indien nodig.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Verplaatsen toohello compatibiliteitsniveau 120 of 130 kunt Hallo nieuwe kardinaliteit schatten functionaliteit. In dat geval worden Hallo standaard CardinalityEstimationModelVersion ingesteld dienovereenkomstig too120 of 130 als zichtbaar hieronder.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Afbeelding 5: Hallo CardinalityEstimationModelVersion is ingesteld too130 wanneer u een compatibiliteitsniveau van 130.*

![Afbeelding 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Den Hallo Kardinaliteitsschatting verschillen
Nu gaan we uitgevoerd iets meer complexe query met betrekking tot een INNER JOIN met een WHERE-component met sommige predicaten en bekijk Hallo rij aantal schatting van de oude Kardinaliteitsschatting functie Hallo eerst.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Deze query uit te voeren effectief retourneert 200.704 rijen, terwijl Hallo rij schatting met Hallo oude kardinaliteit schatten functionaliteit claims 194,284 rijen. Natuurlijk, zoals aangegeven voordat, deze rij aantal resultaten is ook afhankelijk hoe vaak u uitgevoerd Hallo vorige voorbeelden die tabellen Hallo steeds opnieuw op elke uitvoering gevuld. Uiteraard Hallo predicaten in de query wordt ook van invloed zijn op Hallo werkelijke schatting behalve Hallo tabelvorm inhoudsgegevens en hoe deze gegevens daadwerkelijk met elkaar correleren.

*Afbeelding 6: Hallo rij aantal schatting is 194,284 of 6000 rijen uit uit Hallo 200.704 rijen verwacht.*

![Afbeelding 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

In Hallo dezelfde manier Hallo dezelfde query met de nieuwe functionaliteit voor Kardinaliteitsschatting Hallo laten we nu uitvoeren.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


U bekijkt hello hieronder, nu zien we dat schatting van de rij Hallo is 202,877, of veel dichter en hoger dan de oude Kardinaliteitsschatting Hallo.

*Afbeelding 7: Hallo rij aantal schatting is nu 202,877 in plaats van 194,284.*

![Afbeelding 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

In werkelijkheid is Hallo resultatenset 200.704 rijen (maar alles is afhankelijk van hoe vaak u Hallo query's uitvoeren Hallo eerdere voorbeelden, maar belangrijker is, omdat Hallo TSQL Hallo ASELECT() instructie gebruikt, Hallo werkelijke waarden geretourneerd kunnen variëren van één uitvoeren toohello naast). Daarom in dit voorbeeld wordt biedt hello nieuwe Kardinaliteitsschatting een betere taak op het aantal rijen Hallo schatten omdat 202,877 veel dichter too200, 704, dan 194,284! Achternaam, als u Hallo WHERE-component predicaten tooequality wijzigt (plaats ' > ' bijvoorbeeld), kan hierdoor Hallo maakt een schatting tussen Hallo oude en nieuwe kardinaliteit functie nog andere, afhankelijk van hoeveel overeenkomsten die u kunt ophalen.

Uiteraard in dit geval vormt wordt ~ 6000 rijen uit van daadwerkelijk aantal geen grote hoeveelheden gegevens in sommige situaties. Nu TRANSPONEER deze toomillions van rijen in verschillende tabellen en complexe query's, en soms Hallo schatting zijn uitgeschakeld door miljoenen rijen, en daarom Hallo risico van het verzamelen van Hallo verkeerde uitvoeringsplan of onvoldoende geheugen aanvragen verleent voorloopspaties tooTempDB morsen en dus meer i/o-, zijn veel hoger.

Als u de kans Hallo hebt, deze vergelijking met de meest voorkomende query's en in de gegevenssets in de praktijk en voor uzelf in welke mate enkele van de oude en nieuwe schattingen Hallo worden beïnvloed, terwijl sommige meer uit van Hallo realiteit of enige andere gewoon items alleen kan worden dichter Rijtellingen toohello Werkelijke daadwerkelijk in Hallo resultatensets worden geretourneerd. Alles hangen af van de vorm Hallo van uw query's, hello Azure SQL database-kenmerken, Hallo aard en Hallo grootte van uw gegevenssets en Hallo statistieken beschikbaar over deze. Als u zojuist hebt gemaakt van uw Azure SQL Database-exemplaar, de queryoptimalisatie heeft toobuild Hallo-query wordt de kennis vanaf het begin in plaats van hergebruiken statistieken gemaakt van de vorige query Hallo wordt uitgevoerd. Maakt een schatting Hallo zijn dus zeer contextuele en bijna specifieke tooevery servers en toepassingen situatie. Het is een belangrijk aspect tookeep in gedachten.

## <a name="some-considerations-tootake-into-account"></a>Enkele overwegingen tootake rekening
Hoewel de meeste werkbelastingen van Hallo compatibiliteitsniveau 130, voordat u de overstap op Hallo compatibiliteitsniveau voor uw productieomgeving profiteren wilt, hebt u in feite 3 opties:

1. U toocompatibility niveau 130 verplaatsen en u ziet hoe dingen uitvoeren. Als u merkt dat sommige regressies, u gewoon items oorspronkelijke niveau instellen Hallo compatibiliteit niveau back tooits of 130 houden en alleen omkeren Hallo Kardinaliteitsschatting back toohello legacy-modus (zoals hierboven is uitgelegd, dit alleen kan adres Hallo probleem).
2. U uw bestaande toepassingen onder vergelijkbare productie belasting grondig te testen, te stellen en Hallo prestaties voordat gaat tooproduction valideren. In geval van problemen, dezelfde zijn als hierboven, u kunt altijd teruggaan toohello oorspronkelijke compatibiliteitsniveau of gewoon reverse Hallo Kardinaliteitsschatting back toohello legacy-modus.
3. Als een laatste optie en Hallo deze vragen, de meest recente manier tooaddress tooleverage Hallo Query Store is. Dat is de aanbevolen optie vandaag. tooassist hello analyse van uw query's onder compatibiliteit niveau 120 of hieronder versus 130, kan niet raden we u voldoende toouse Query Store. Query Store is beschikbaar met de meest recente versie van Azure SQL Database V12 Hallo en ontworpen toohelp u query prestaties op te lossen. Hallo Query Store beschouwen als een zwarte gegevens doos voor uw database verzamelen en presenteren van gedetailleerde historische informatie over alle query's. Dit aanzienlijk prestaties forensische vereenvoudigt door te beperken van Hallo tijd toodiagnose en oplossen van problemen. U vindt meer informatie op [Query Store: een data zwarte doos voor uw database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Op Hallo op hoog niveau, als u al een set databases die worden uitgevoerd op het niveau van databasecompatibiliteit 120 of onder hebben en plannen van toomove enkele ervan too130, of omdat de werkbelasting van uw nieuwe databases die automatisch worden ingericht snel worden ingesteld met standaard too130, overweeg Hallo volgende:

* Voordat u nieuwe compatibiliteitsniveau toohello in productie wijzigt, schakel Query Store. U kunt te verwijzen[Hallo compatibiliteitsmodus Database en het gebruik Hallo Query Store wijzigen](https://msdn.microsoft.com/library/bb895281.aspx) voor meer informatie.
* Test vervolgens alle kritieke werkbelastingen met behulp van representatieve gegevens en query's van een productie-achtige omgeving en vergelijken Hallo prestaties ervaren en zoals gemeld door de Query Store. Als u een aantal regressies ondervindt, kunt u identificeren Hallo opgelost query's met Hallo Query Store en Hallo-abonnement in Query Store optie forceren gebruiken (aka plan vastmaken). In dat geval moet u definitief blijven met compatibiliteitsniveau Hallo 130, en de voormalige queryplan Hallo zoals voorgesteld door Hallo Query Store.
* Als u wilt dat tooleverage nieuwe functies en mogelijkheden van Azure SQL Database (die met SQL Server 2016), maar gevoelige toochanges door Hallo compatibiliteitsniveau 130, als een laatste toevlucht gebracht zijn kunt u ook compatibiliteitsniveau terug Hallo forceren toohello niveau die past bij uw workload met behulp van een instructie ALTER DATABASE. Maar eerst bedenken Hallo Query Store plan vastmaken optie is de beste optie, omdat niet met behulp van 130 in feite op Hallo functionaliteitsniveau van een oudere versie van SQL Server bijwerkt is.
* Als u meerdere toepassingen spanning meerdere databases hebt, mogelijk nodig tooupdate Hallo logica van uw databases tooensure een consistente compatibiliteitsniveau inrichten voor alle databases; oude en nieuwe ingerichte die zijn. De prestaties van uw toepassing werklast kan gevoelige toohello feit dat sommige databases op verschillende compatibiliteitsniveaus worden uitgevoerd en daarom compatibiliteit niveau consistentie binnen elke database mogelijk vereist in volgorde tooprovide Hallo dezelfde alle via het mededelingenbord Hallo-ervaring bieden tooyour klanten. Houd er rekening mee dat het is niet verplicht, dit echt is afhankelijk van hoe uw toepassing wordt beïnvloed door Hallo compatibiliteitsniveau.
* Laatste, met betrekking tot Hallo Kardinaliteitsschatting, en net zoals het wijzigen van de compatibiliteitsniveau Hallo voordat u doorgaat in productie, is het aanbevolen tootest als uw toepassing van gebruikmaakt de werkbelasting van uw productie onder de nieuwe voorwaarden toodetermine Hallo Hallo Kardinaliteitsschatting is verbeterd.

## <a name="conclusion"></a>Conclusie
Met behulp van Azure SQL Database kan toobenefit van alle SQL Server 2016 verbeteringen duidelijk verbeteren de uitvoeringen van uw query. Net zoals-is! Natuurlijk, zoals een nieuwe functie wordt moet een juiste beoordeling worden uitgevoerd toodetermine Hallo precieze voorwaarden waaronder de werkbelasting van uw database Hallo beste werkt. Ervaring blijkt dat de meeste werkbelasting verwachte tooat minste uitvoering transparant compatibiliteitsniveau 130 tijdens het gebruik van nieuwe query functies en nieuwe Kardinaliteitsschatting verwerken. Die aangegeven in de praktijk zijn altijd enkele uitzonderingen en het uitvoeren van de juiste vervaldatum toewijding inzetten is een belangrijk assessment toodetermine hoeveel u van deze uitbreidingen profiteren kunt. En opnieuw Hallo Query Store van een nuttige informatie in de hiervoor kunnen zijn!

Als SQL Azure zich verder ontwikkelen, kunt u een compatibiliteitsniveau 140 in Hallo toekomstige verwachten. Wanneer de tijd van toepassing is, gaat we bespreken wat deze toekomstige compatibiliteitsniveau 140 verschijnt, net zoals kort besproken hier welke compatibiliteitsniveau 130 is vandaag te brengen.

Nu gaan we niet vergeten, vanaf juni 2016, Azure SQL Database wordt gewijzigd Hallo standaard compatibiliteitsniveau van 120 too130 voor nieuwe databases. Let!

## <a name="references"></a>Verwijzingen
* [Wat is er nieuw in Database-Engine](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Query Store: een data zwarte doos voor uw database, door Borko Novakovic, juni 2016 op 8](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [ALTER databasecompatibiliteitsniveau (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE BINNEN HET BEREIK VAN CONFIGURATIE](https://msdn.microsoft.com/library/mt629158.aspx)
* [Compatibiliteitsniveau 130 voor Azure SQL Database V12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Plannen van uw Query te optimaliseren Hello Kardinaliteitsschatter van SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)
* [Handleiding voor Columnstore-indexen](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog: Verbeterde prestaties van query's met een compatibiliteitsniveau 130 in Azure SQL Database door aan Alain Lissoir, mei 6 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
