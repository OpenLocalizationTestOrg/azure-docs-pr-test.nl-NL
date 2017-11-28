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
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="5bdeb-104">Verbeterde prestaties van query's met de compatibiliteit van niveau 130 in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5bdeb-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="5bdeb-105">Azure SQL-Database is actief transparant honderden of duizenden databases op veel verschillende compatibiliteitsniveaus behouden en garanderen Hallo achterwaartse compatibiliteit toohello bijbehorende versie van Microsoft SQL Server voor alle klanten!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="5bdeb-106">In dit artikel we Hallo voordelen van uw Azure SQL-database op compatibiliteitsniveau 130 uitgevoerd en gebruik van de voordelen van de nieuwe queryoptimizer Hallo Hallo verkennen en processorfuncties opvragen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="5bdeb-107">We ook betrekking op Hallo mogelijk neveneffecten op Hallo queryprestaties voor Hallo bestaande SQL-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="5bdeb-108">Als een herinnering geschiedenis Hallo uitlijning van de SQL-versies toodefault compatibiliteitsniveaus zijn als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="5bdeb-109">100: in SQL Server 2008 en Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="5bdeb-110">110: in SQL Server 2012 en Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="5bdeb-111">120: in SQL Server 2014 en Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="5bdeb-112">130: in SQL Server 2016 en Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bdeb-113">Vanaf **medio juni 2016**, in Azure SQL Database worden Hallo standaard compatibiliteitsniveau 130 in plaats van 120 voor **nieuw gemaakte** databases.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="5bdeb-114">Databases die zijn gemaakt vóór medio juni 2016 wordt *niet* worden beïnvloed en onderhouden hun huidige compatibiliteitsniveau (100, 110 of 120).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="5bdeb-115">Databases die worden gemigreerd vanuit Azure SQL Database-versie V11 tooV12 heeft een compatibiliteitsniveau van 100 of 110.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="5bdeb-116">Over het compatibiliteitsniveau 130</span><span class="sxs-lookup"><span data-stu-id="5bdeb-116">About compatibility level 130</span></span>
<span data-ttu-id="5bdeb-117">Als u tooknow Hallo huidige compatibiliteitsniveau van uw database wilt, uitvoeren eerst Hallo volgende Transact-SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="5bdeb-118">Voordat u deze wijziging toolevel 130 gebeurt voor **zojuist** databases gemaakt, gaan we controleren wat deze wijziging alles over via een zeer eenvoudige query voorbeelden en Zie hoe iedereen kan profiteren van deze.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="5bdeb-119">Verwerking van query's in relationele databases kan zeer complex en toolots van gedrag en computer wetenschap en wiskunde toounderstand Hallo inherente ontwerpbeslissingen die kan leiden.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="5bdeb-120">In dit document is Hallo inhoud opzettelijk vereenvoudigde tooensure iedereen met een minimale technische achtergrond kunt Hallo het effect van wijzigingen in compatibiliteit Hallo en bepalen hoe deze toepassingen kan profiteren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="5bdeb-121">We hebben een kort overzicht van het compatibiliteitsniveau van welke Hallo 130 op Hallo tabel brengt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="5bdeb-122">U vindt meer informatie op [ALTER databasecompatibiliteitsniveau (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), maar hier een korte samenvatting volgt:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="5bdeb-123">Hallo Insert-bewerking van een instructie Insert select kan met meerdere threads of kan een parallel plan, terwijl voordat deze bewerking één thread is.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="5bdeb-124">Geheugen geoptimaliseerde tabel- en tabel variabelen query's zijn nu parallelle plannen tijdens voordat deze bewerking is ook één thread.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="5bdeb-125">Statistieken voor de tabel geoptimaliseerd voor geheugen kan nu door actieve en worden automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="5bdeb-126">Zie [What's New in Database-Engine: In het geheugen OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="5bdeb-127">Batch-modus v/s rij-modus wordt gewijzigd met de kolom-indexen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="5bdeb-128">Sorteren op een tabel met een index kolom worden nu in batchmodus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="5bdeb-129">Windowing statistische functies worden nu in batchmodus zoals TSQL LAG/LEAD instructies werken.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="5bdeb-130">Query's op kolom Store tabellen met meerdere afzonderlijke componenten werken in batchmodus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="5bdeb-131">Query's onder DOP = 1 of met een seriële plan ook uit te voeren in de batchmodus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="5bdeb-132">Laatste Kardinaliteitsschatting verbeteringen daadwerkelijk afkomstig zijn met een compatibiliteitsniveau 120, maar voor de uitgevoerd op een lager compatibiliteitsniveau (dat wil zeggen 100 of 110), hello verplaatsen toocompatibility niveau 130 ook ervoor zorgt dat deze verbeteringen en deze kunnen ook Hallo query-prestaties van uw toepassingen profiteren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="5bdeb-133">Compatibiliteitsniveau 130 oefenen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="5bdeb-134">Eerste we ophalen bepaalde tabellen, indexen en willekeurige gegevens die zijn gemaakt toopractice enkele van deze nieuwe functies.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="5bdeb-135">Voorbeelden van Hallo TSQL-scripts kunnen worden uitgevoerd onder de SQL Server 2016, of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="5bdeb-136">Bij het maken van een Azure SQL database, zorg er echter u ten minste twee cores tooallow multithreading op Hallo minimaal een P2 database omdat moet u ervoor kiezen en daarom profiteren van deze functies.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

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


<span data-ttu-id="5bdeb-137">Nu gaan we hebben een toosome uiterlijk van Hallo Query verwerken functies met een compatibiliteitsniveau 130 binnenkort.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="5bdeb-138">Parallelle invoegen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-138">Parallel INSERT</span></span>
<span data-ttu-id="5bdeb-139">Hallo invoegbewerking onder compatibiliteitsniveau 120 en 130 die respectievelijk Hallo INSERT-bewerking wordt uitgevoerd in één thread-model (120) en in een multithreaded model (130) uitvoeren Hallo TSQL-instructies die hieronder worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

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


<span data-ttu-id="5bdeb-140">Door het aanvragen van Hallo werkelijke Hallo queryplan, kijken naar de grafische weergave of de XML-inhoud, kunt u bepalen welke Kardinaliteitsschatting functie op play is.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="5bdeb-141">U bekijkt hello plannen side-by-side in afbeelding 1, duidelijk ziet u dat Hallo kolom Store invoegen uitvoering gaat van seriële in 120 tooparallel in 130.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="5bdeb-142">Let ook die wijziging Hallo van Hallo iterator-pictogram in 130 Hallo-indeling met twee parallelle pijlen, inderdaad parallelle ter illustratie van Hallo feit dat nu Hallo iterator-uitvoering is.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="5bdeb-143">Als u grote INSERT operations toocomplete hebt, functioneren Hallo parallelle uitvoering, het aantal core die u tot uw beschikking staan voor Hallo-database hebt, gekoppelde toohello beter; afhankelijk van uw situatie up tooa 100 maal sneller!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="5bdeb-144">*Afbeelding 1: Bewerking wijzigingen uit seriële tooparallel met compatibiliteitsniveau 130 invoegen.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![Afbeelding 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="5bdeb-146">SERIËLE batchmodus</span><span class="sxs-lookup"><span data-stu-id="5bdeb-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="5bdeb-147">Op deze manier kunt verplaatsen toocompatibility niveau 130 bij het verwerken van de rijen met gegevens batchverwerking modus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="5bdeb-148">Modus batchbewerkingen zijn eerst alleen beschikbaar wanneer u beschikken over een columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="5bdeb-149">Ten tweede een batch doorgaans ~ 900 rijen vertegenwoordigt en gebruikt een code-logica geoptimaliseerd voor multicore CPU, hogere geheugendoorvoer en rechtstreeks maakt gebruik van gecomprimeerde gegevens van de kolom Store waar mogelijk Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="5bdeb-150">In deze omstandigheden SQL Server 2016, kunnen verwerken ~ 900 rijen in één keer in plaats van 1 rij tijdens hello, en als gevolg hiervan hello algemene overheadkosten Hallo-bewerking wordt nu gedeeld door Hallo hele batch, verminderen Hallo algehele kosten per rij.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="5bdeb-151">Deze gedeelde hoeveelheid van bewerkingen in wezen in combinatie met Hallo kolom store compressie vermindert Hallo latentie betrokken is bij een bewerking SELECT batch-modus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="5bdeb-152">U kunt meer informatie vinden over Hallo kolom store en batch-modus met [Columnstore-indexen handleiding](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

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


<span data-ttu-id="5bdeb-153">Als daaronder weergegeven ziet door observeren Hallo query plannen side-by-side in afbeelding 2 u dat Hallo verwerkingsmodus is gewijzigd met een compatibiliteitsniveau Hallo en als gevolg hiervan, wanneer u helemaal Hallo query's uitvoert in beide compatibiliteitsniveau, u dat ziet de meeste Hallo verwerkingstijd is besteed in de rij modus (% 86) vergeleken toohello batchmodus (14%), waarbij 2 batches is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="5bdeb-154">Hallo-gegevensset te verhogen, hello voordeel wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="5bdeb-155">*Afbeelding 2: Selecteer bewerking wijzigingen van de seriële toobatch modus met compatibiliteitsniveau 130.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Afbeelding 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="5bdeb-157">Batchmodus bij sorteren van uitvoering</span><span class="sxs-lookup"><span data-stu-id="5bdeb-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="5bdeb-158">Vergelijkbare toohello hierboven, maar de sorteerbewerking toegepaste tooa, Hallo overgang van de rij-modus (compatibiliteitsniveau 120) toobatch modus (compatibiliteitsniveau 130) verbetert de prestaties van Hallo Hallo sorteerbewerking voor Hallo dezelfde redenen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

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


<span data-ttu-id="5bdeb-159">Zichtbaar side-by-side in afbeelding 3, ziet u dat de sorteerbewerking Hallo in rijmodus 81% Hallo kosten, terwijl de batchmodus Hallo alleen 19% van Hallo kosten (respectievelijk 81% en 56% op Hallo sorteren zelf vertegenwoordigt) vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="5bdeb-160">*Afbeelding 3: De sorteerbewerking verandert van rij toobatch modus met compatibiliteitsniveau 130.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Afbeelding 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="5bdeb-162">Uiteraard verloopt bevatten deze voorbeelden alleen tienduizenden rijen, die is niets wanneer bekijkt hello gegevens beschikbaar zijn in de meeste SQL Servers tegenwoordig.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="5bdeb-163">Deze tegen miljoenen rijen in plaats daarvan NET project en dit zich vertalen in enkele minuten voor uitvoering elke dag in behandeling zijnde Hallo aard van uw werkbelasting wordt bespaard.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="5bdeb-164">Verbeteringen in kardinaliteit schatting (CE)</span><span class="sxs-lookup"><span data-stu-id="5bdeb-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="5bdeb-165">Met SQL Server 2014 geïntroduceerd, een database die wordt uitgevoerd op een compatibiliteitsniveau 120 of hoger maakt gebruik van Hallo nieuwe kardinaliteit schatten functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="5bdeb-166">Kardinaliteitsschatting is in wezen Hallo logica gebruikt toodetermine hoe een query op basis van de geschatte kosten op SQL server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="5bdeb-167">Hallo schatting wordt berekend met behulp van de invoer van statistieken die zijn gekoppeld aan de objecten die zijn betrokken bij deze query.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="5bdeb-168">Vrijwel, op een hoog niveau Kardinaliteitsschatting functies zijn rij aantal samen met informatie over het Hallo-distributie van Hallo waarden, unieke waarde aantallen en dubbele aantallen opgenomen in Hallo tabellen en de objecten waarnaar wordt verwezen in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="5bdeb-169">Ophalen van deze schattingen onjuist is, kan leiden toounnecessary schijf-i/o vanwege tooinsufficient geheugen verleent (dat wil zeggen TempDB morsen) of tooa selectie van een seriële plan kan worden uitgevoerd via een parallelle uitvoering, tooname plannen enkele.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="5bdeb-170">Sluiting, onjuist maakt een schatting kunnen leiden tot tooan verslechtering van de algehele prestaties van Hallo queryuitvoering.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="5bdeb-171">Hallo op de andere zijde, betere schattingen, nauwkeuriger schattingen, potentiële klanten toobetter query uitvoeringen!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="5bdeb-172">Zoals al eerder vermeld, query optimalisaties en maakt een schatting van een complexe materie, maar als u meer informatie over het queryplannen en kardinaliteitsschatter toolearn wilt, kunt u toohello document op verwijzen [uw queryplannen optimaliseren Hello SQL Server 2014 Kardinaliteitsschatter](https://msdn.microsoft.com/library/dn673537.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="5bdeb-173">Welke Kardinaliteitsschatting momenteel gebruikt u?</span><span class="sxs-lookup"><span data-stu-id="5bdeb-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="5bdeb-174">toodetermine onder welke Kardinaliteitsschatting uw query's worden uitgevoerd, gaan we zojuist gebruik Hallo query hieronder voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="5bdeb-175">Houd er rekening mee dat het eerste voorbeeld wordt uitgevoerd onder het compatibiliteitsniveau 110, wat impliceert Hallo gebruik van Hallo oude Kardinaliteitsschatting functies.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="5bdeb-176">Zodra de uitvoering is voltooid, klikt u op Hallo XML-koppeling en bekijkt hello eigenschappen van de eerste iterator Hallo zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="5bdeb-177">Houd er rekening mee Hallo eigenschapsnaam CardinalityEstimationModelVersion die is ingesteld op 70 aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="5bdeb-178">Het betekent niet dat het databasecompatibiliteitsniveau Hallo toohello SQL Server 7.0 versie (deze is ingesteld op 110 als zichtbaar in Hallo TSQL-instructies hierboven) is ingesteld, maar Hallo waarde 70 enkel Hallo verouderde Kardinaliteitsschatting functionaliteit beschikbaar sinds SQL vertegenwoordigt Server 7.0, waarvoor geen belangrijke wijzigingen tot SQL Server 2014 (die wordt geleverd met een compatibiliteitsniveau van 120).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="5bdeb-179">*Afbeelding 4: Hallo CardinalityEstimationModelVersion is ingesteld too70 wanneer u een compatibiliteitsniveau 110 of onder.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Afbeelding 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="5bdeb-181">U kunt ook kunt u wijzigen Hallo compatibiliteit niveau too130, en Hallo gebruik van de functie voor nieuwe Kardinaliteitsschatting Hallo uitschakelen met behulp van Hallo LEGACY_CARDINALITY_ESTIMATION ingesteld tooON met [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="5bdeb-182">Dit zal worden exact Hallo dezelfde zijn als het gebruik van 110 van een schatting van de kardinaliteit-functie tijdens het gebruik van Hallo nieuwste queryverwerking compatibiliteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="5bdeb-183">Als u dit doet, kunt u profiteren van nieuwe Hallo-query verwerken functies afkomstig met de meest recente compatibiliteitsniveau hello (dat wil zeggen batchmodus), maar nog steeds zijn afhankelijk van Hallo oude kardinaliteit schatten functionaliteit indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="5bdeb-184">Verplaatsen toohello compatibiliteitsniveau 120 of 130 kunt Hallo nieuwe kardinaliteit schatten functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="5bdeb-185">In dat geval worden Hallo standaard CardinalityEstimationModelVersion ingesteld dienovereenkomstig too120 of 130 als zichtbaar hieronder.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="5bdeb-186">*Afbeelding 5: Hallo CardinalityEstimationModelVersion is ingesteld too130 wanneer u een compatibiliteitsniveau van 130.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Afbeelding 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="5bdeb-188">Den Hallo Kardinaliteitsschatting verschillen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="5bdeb-189">Nu gaan we uitgevoerd iets meer complexe query met betrekking tot een INNER JOIN met een WHERE-component met sommige predicaten en bekijk Hallo rij aantal schatting van de oude Kardinaliteitsschatting functie Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="5bdeb-190">Deze query uit te voeren effectief retourneert 200.704 rijen, terwijl Hallo rij schatting met Hallo oude kardinaliteit schatten functionaliteit claims 194,284 rijen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="5bdeb-191">Natuurlijk, zoals aangegeven voordat, deze rij aantal resultaten is ook afhankelijk hoe vaak u uitgevoerd Hallo vorige voorbeelden die tabellen Hallo steeds opnieuw op elke uitvoering gevuld.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="5bdeb-192">Uiteraard Hallo predicaten in de query wordt ook van invloed zijn op Hallo werkelijke schatting behalve Hallo tabelvorm inhoudsgegevens en hoe deze gegevens daadwerkelijk met elkaar correleren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="5bdeb-193">*Afbeelding 6: Hallo rij aantal schatting is 194,284 of 6000 rijen uit uit Hallo 200.704 rijen verwacht.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Afbeelding 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="5bdeb-195">In Hallo dezelfde manier Hallo dezelfde query met de nieuwe functionaliteit voor Kardinaliteitsschatting Hallo laten we nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="5bdeb-196">U bekijkt hello hieronder, nu zien we dat schatting van de rij Hallo is 202,877, of veel dichter en hoger dan de oude Kardinaliteitsschatting Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="5bdeb-197">*Afbeelding 7: Hallo rij aantal schatting is nu 202,877 in plaats van 194,284.*</span><span class="sxs-lookup"><span data-stu-id="5bdeb-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Afbeelding 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="5bdeb-199">In werkelijkheid is Hallo resultatenset 200.704 rijen (maar alles is afhankelijk van hoe vaak u Hallo query's uitvoeren Hallo eerdere voorbeelden, maar belangrijker is, omdat Hallo TSQL Hallo ASELECT() instructie gebruikt, Hallo werkelijke waarden geretourneerd kunnen variëren van één uitvoeren toohello naast).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="5bdeb-200">Daarom in dit voorbeeld wordt biedt hello nieuwe Kardinaliteitsschatting een betere taak op het aantal rijen Hallo schatten omdat 202,877 veel dichter too200, 704, dan 194,284!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="5bdeb-201">Achternaam, als u Hallo WHERE-component predicaten tooequality wijzigt (plaats ' > ' bijvoorbeeld), kan hierdoor Hallo maakt een schatting tussen Hallo oude en nieuwe kardinaliteit functie nog andere, afhankelijk van hoeveel overeenkomsten die u kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="5bdeb-202">Uiteraard in dit geval vormt wordt ~ 6000 rijen uit van daadwerkelijk aantal geen grote hoeveelheden gegevens in sommige situaties.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="5bdeb-203">Nu TRANSPONEER deze toomillions van rijen in verschillende tabellen en complexe query's, en soms Hallo schatting zijn uitgeschakeld door miljoenen rijen, en daarom Hallo risico van het verzamelen van Hallo verkeerde uitvoeringsplan of onvoldoende geheugen aanvragen verleent voorloopspaties tooTempDB morsen en dus meer i/o-, zijn veel hoger.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="5bdeb-204">Als u de kans Hallo hebt, deze vergelijking met de meest voorkomende query's en in de gegevenssets in de praktijk en voor uzelf in welke mate enkele van de oude en nieuwe schattingen Hallo worden beïnvloed, terwijl sommige meer uit van Hallo realiteit of enige andere gewoon items alleen kan worden dichter Rijtellingen toohello Werkelijke daadwerkelijk in Hallo resultatensets worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="5bdeb-205">Alles hangen af van de vorm Hallo van uw query's, hello Azure SQL database-kenmerken, Hallo aard en Hallo grootte van uw gegevenssets en Hallo statistieken beschikbaar over deze.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="5bdeb-206">Als u zojuist hebt gemaakt van uw Azure SQL Database-exemplaar, de queryoptimalisatie heeft toobuild Hallo-query wordt de kennis vanaf het begin in plaats van hergebruiken statistieken gemaakt van de vorige query Hallo wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="5bdeb-207">Maakt een schatting Hallo zijn dus zeer contextuele en bijna specifieke tooevery servers en toepassingen situatie.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="5bdeb-208">Het is een belangrijk aspect tookeep in gedachten.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="5bdeb-209">Enkele overwegingen tootake rekening</span><span class="sxs-lookup"><span data-stu-id="5bdeb-209">Some considerations tootake into account</span></span>
<span data-ttu-id="5bdeb-210">Hoewel de meeste werkbelastingen van Hallo compatibiliteitsniveau 130, voordat u de overstap op Hallo compatibiliteitsniveau voor uw productieomgeving profiteren wilt, hebt u in feite 3 opties:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="5bdeb-211">U toocompatibility niveau 130 verplaatsen en u ziet hoe dingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="5bdeb-212">Als u merkt dat sommige regressies, u gewoon items oorspronkelijke niveau instellen Hallo compatibiliteit niveau back tooits of 130 houden en alleen omkeren Hallo Kardinaliteitsschatting back toohello legacy-modus (zoals hierboven is uitgelegd, dit alleen kan adres Hallo probleem).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="5bdeb-213">U uw bestaande toepassingen onder vergelijkbare productie belasting grondig te testen, te stellen en Hallo prestaties voordat gaat tooproduction valideren.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="5bdeb-214">In geval van problemen, dezelfde zijn als hierboven, u kunt altijd teruggaan toohello oorspronkelijke compatibiliteitsniveau of gewoon reverse Hallo Kardinaliteitsschatting back toohello legacy-modus.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="5bdeb-215">Als een laatste optie en Hallo deze vragen, de meest recente manier tooaddress tooleverage Hallo Query Store is.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="5bdeb-216">Dat is de aanbevolen optie vandaag.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-216">That’s today’s recommended option!</span></span> <span data-ttu-id="5bdeb-217">tooassist hello analyse van uw query's onder compatibiliteit niveau 120 of hieronder versus 130, kan niet raden we u voldoende toouse Query Store.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="5bdeb-218">Query Store is beschikbaar met de meest recente versie van Azure SQL Database V12 Hallo en ontworpen toohelp u query prestaties op te lossen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="5bdeb-219">Hallo Query Store beschouwen als een zwarte gegevens doos voor uw database verzamelen en presenteren van gedetailleerde historische informatie over alle query's.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="5bdeb-220">Dit aanzienlijk prestaties forensische vereenvoudigt door te beperken van Hallo tijd toodiagnose en oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="5bdeb-221">U vindt meer informatie op [Query Store: een data zwarte doos voor uw database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="5bdeb-222">Op Hallo op hoog niveau, als u al een set databases die worden uitgevoerd op het niveau van databasecompatibiliteit 120 of onder hebben en plannen van toomove enkele ervan too130, of omdat de werkbelasting van uw nieuwe databases die automatisch worden ingericht snel worden ingesteld met standaard too130, overweeg Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5bdeb-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="5bdeb-223">Voordat u nieuwe compatibiliteitsniveau toohello in productie wijzigt, schakel Query Store.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="5bdeb-224">U kunt te verwijzen[Hallo compatibiliteitsmodus Database en het gebruik Hallo Query Store wijzigen](https://msdn.microsoft.com/library/bb895281.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="5bdeb-225">Test vervolgens alle kritieke werkbelastingen met behulp van representatieve gegevens en query's van een productie-achtige omgeving en vergelijken Hallo prestaties ervaren en zoals gemeld door de Query Store.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="5bdeb-226">Als u een aantal regressies ondervindt, kunt u identificeren Hallo opgelost query's met Hallo Query Store en Hallo-abonnement in Query Store optie forceren gebruiken (aka plan vastmaken).</span><span class="sxs-lookup"><span data-stu-id="5bdeb-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="5bdeb-227">In dat geval moet u definitief blijven met compatibiliteitsniveau Hallo 130, en de voormalige queryplan Hallo zoals voorgesteld door Hallo Query Store.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="5bdeb-228">Als u wilt dat tooleverage nieuwe functies en mogelijkheden van Azure SQL Database (die met SQL Server 2016), maar gevoelige toochanges door Hallo compatibiliteitsniveau 130, als een laatste toevlucht gebracht zijn kunt u ook compatibiliteitsniveau terug Hallo forceren toohello niveau die past bij uw workload met behulp van een instructie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="5bdeb-229">Maar eerst bedenken Hallo Query Store plan vastmaken optie is de beste optie, omdat niet met behulp van 130 in feite op Hallo functionaliteitsniveau van een oudere versie van SQL Server bijwerkt is.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="5bdeb-230">Als u meerdere toepassingen spanning meerdere databases hebt, mogelijk nodig tooupdate Hallo logica van uw databases tooensure een consistente compatibiliteitsniveau inrichten voor alle databases; oude en nieuwe ingerichte die zijn.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="5bdeb-231">De prestaties van uw toepassing werklast kan gevoelige toohello feit dat sommige databases op verschillende compatibiliteitsniveaus worden uitgevoerd en daarom compatibiliteit niveau consistentie binnen elke database mogelijk vereist in volgorde tooprovide Hallo dezelfde alle via het mededelingenbord Hallo-ervaring bieden tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="5bdeb-232">Houd er rekening mee dat het is niet verplicht, dit echt is afhankelijk van hoe uw toepassing wordt beïnvloed door Hallo compatibiliteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="5bdeb-233">Laatste, met betrekking tot Hallo Kardinaliteitsschatting, en net zoals het wijzigen van de compatibiliteitsniveau Hallo voordat u doorgaat in productie, is het aanbevolen tootest als uw toepassing van gebruikmaakt de werkbelasting van uw productie onder de nieuwe voorwaarden toodetermine Hallo Hallo Kardinaliteitsschatting is verbeterd.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5bdeb-234">Conclusie</span><span class="sxs-lookup"><span data-stu-id="5bdeb-234">Conclusion</span></span>
<span data-ttu-id="5bdeb-235">Met behulp van Azure SQL Database kan toobenefit van alle SQL Server 2016 verbeteringen duidelijk verbeteren de uitvoeringen van uw query.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="5bdeb-236">Net zoals-is!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-236">Just as-is!</span></span> <span data-ttu-id="5bdeb-237">Natuurlijk, zoals een nieuwe functie wordt moet een juiste beoordeling worden uitgevoerd toodetermine Hallo precieze voorwaarden waaronder de werkbelasting van uw database Hallo beste werkt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="5bdeb-238">Ervaring blijkt dat de meeste werkbelasting verwachte tooat minste uitvoering transparant compatibiliteitsniveau 130 tijdens het gebruik van nieuwe query functies en nieuwe Kardinaliteitsschatting verwerken.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="5bdeb-239">Die aangegeven in de praktijk zijn altijd enkele uitzonderingen en het uitvoeren van de juiste vervaldatum toewijding inzetten is een belangrijk assessment toodetermine hoeveel u van deze uitbreidingen profiteren kunt.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="5bdeb-240">En opnieuw Hallo Query Store van een nuttige informatie in de hiervoor kunnen zijn!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="5bdeb-241">Als SQL Azure zich verder ontwikkelen, kunt u een compatibiliteitsniveau 140 in Hallo toekomstige verwachten.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="5bdeb-242">Wanneer de tijd van toepassing is, gaat we bespreken wat deze toekomstige compatibiliteitsniveau 140 verschijnt, net zoals kort besproken hier welke compatibiliteitsniveau 130 is vandaag te brengen.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="5bdeb-243">Nu gaan we niet vergeten, vanaf juni 2016, Azure SQL Database wordt gewijzigd Hallo standaard compatibiliteitsniveau van 120 too130 voor nieuwe databases.</span><span class="sxs-lookup"><span data-stu-id="5bdeb-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="5bdeb-244">Let!</span><span class="sxs-lookup"><span data-stu-id="5bdeb-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="5bdeb-245">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-245">References</span></span>
* [<span data-ttu-id="5bdeb-246">Wat is er nieuw in Database-Engine</span><span class="sxs-lookup"><span data-stu-id="5bdeb-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="5bdeb-247">Blog: Query Store: een data zwarte doos voor uw database, door Borko Novakovic, juni 2016 op 8</span><span class="sxs-lookup"><span data-stu-id="5bdeb-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="5bdeb-248">ALTER databasecompatibiliteitsniveau (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="5bdeb-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="5bdeb-249">ALTER DATABASE BINNEN HET BEREIK VAN CONFIGURATIE</span><span class="sxs-lookup"><span data-stu-id="5bdeb-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="5bdeb-250">Compatibiliteitsniveau 130 voor Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="5bdeb-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="5bdeb-251">Plannen van uw Query te optimaliseren Hello Kardinaliteitsschatter van SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="5bdeb-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="5bdeb-252">Handleiding voor Columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="5bdeb-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="5bdeb-253">Blog: Verbeterde prestaties van query's met een compatibiliteitsniveau 130 in Azure SQL Database door aan Alain Lissoir, mei 6 2016</span><span class="sxs-lookup"><span data-stu-id="5bdeb-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
