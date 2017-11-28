---
title: aaaDistributing tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met het distribueren van tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="2c5f9-103">Distributie van tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2c5f9-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2c5f9-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="2c5f9-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="2c5f9-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="2c5f9-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-107">[Index][Index]</span></span>
> * <span data-ttu-id="2c5f9-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="2c5f9-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="2c5f9-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="2c5f9-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="2c5f9-111">SQL Data Warehouse is een gedistribueerd MPP-databasesysteem (Massively Parallel Processing).</span><span class="sxs-lookup"><span data-stu-id="2c5f9-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="2c5f9-112">Door gegevens- en processorcapaciteit over meerdere knooppunten te verdelen, kan SQL Data Warehouse grote schaalbaarheid bieden, veel groter dan enkel ander systeem.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="2c5f9-113">Bepalen hoe toodistribute uw gegevens in uw SQL Data Warehouse is een van de belangrijkste Hallo factoren tooachieving optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="2c5f9-114">Hallo sleutel toooptimal prestaties is voor het minimaliseren van verplaatsing van gegevens en op zijn beurt Hallo sleutel toominimizing gegevensverplaatsing Hallo rechts distributiestrategie selecteert.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="2c5f9-115">Understanding gegevensverplaatsing</span><span class="sxs-lookup"><span data-stu-id="2c5f9-115">Understanding data movement</span></span>
<span data-ttu-id="2c5f9-116">Hallo-gegevens van elke tabel is in een systeem MPP verdeeld over verschillende onderliggende databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="2c5f9-117">Hallo meest geoptimaliseerde query's op een MPP-systeem kunnen eenvoudig worden doorgegeven via tooexecute Hallo afzonderlijke gedistribueerde databases zonder interactie tussen Hallo andere databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="2c5f9-118">Stel dat u hebt een database met verkoopgegevens die twee tabellen, verkoop en klanten bevat.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="2c5f9-119">Als u een query die toojoin uw verkoop tooyour klantentabel nodig hebt en u uw verkoop- en de klantentabellen up door klantnummer deelt, plaatsen van elke klant in een aparte database, kunnen alle query's die lid van de verkoop- en worden opgelost binnen elke database met zonder enige kennis van Hallo andere databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="2c5f9-120">Daarentegen als u uw verkoopgegevens gedeeld door het nummer en de gegevens van de klant op klantnummer van de, vervolgens een bepaalde database geen bijbehorende Hallo-gegevens voor elke klant en dus als u uw klantgegevens van verkoopgegevens tooyour toojoin wilt, moet u tooget hello gegevens voor elke klant van Hallo andere databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="2c5f9-121">In dit voorbeeld tweede moet gegevensverplaatsing toooccur toomove Hallo gegevens toohello verkoop klantgegevens, zodat Hallo twee tabellen kunnen worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="2c5f9-122">Verplaatsing van gegevens niet altijd slecht, soms is het nodig toosolve een query.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="2c5f9-123">Maar nadat deze extra stap kan worden vermeden, natuurlijk uw query wordt sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="2c5f9-124">Verplaatsing van gegevens ontstaat meestal als tabellen zijn gekoppeld of aggregaties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="2c5f9-125">U moet vaak toodo beide, dus terwijl u mogelijk toooptimize voor een scenario, zoals een join, u nog moet data movement toohelp u oplossen voor Hallo ander scenario, zoals een aggregatie.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="2c5f9-126">Hallo truc uitzoeken wat minder werk is.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="2c5f9-127">In de meeste gevallen is distribueren grote feitentabellen op een algemeen lid kolom Hallo meest effectieve methode voor het beperken van Hallo meeste gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="2c5f9-128">Distributie van gegevens op de join-kolommen is een meer algemene methode tooreduce verplaatsing van gegevens dan het distribueren van gegevens voor kolommen die zijn betrokken bij een aggregatie.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="2c5f9-129">De methode distributiepunten selecteren</span><span class="sxs-lookup"><span data-stu-id="2c5f9-129">Select distribution method</span></span>
<span data-ttu-id="2c5f9-130">Uw gegevens worden in SQL Data Warehouse achter de schermen Hallo worden opgedeeld in 60 databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="2c5f9-131">Elke individuele database waarnaar wordt verwezen tooas is een **distributie**.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="2c5f9-132">Wanneer gegevens in elke tabel is geladen, is SQL Data Warehouse tooknow hoe toodivide van uw gegevens over deze 60 verdelingen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="2c5f9-133">Hallo distributiemethode is gedefinieerd op Hallo tabelniveau en er zijn momenteel twee mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="2c5f9-134">**Round robin** die gegevens distribueren gelijkmatig maar willekeurig.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="2c5f9-135">**Hash-gedistribueerde** die gegevens op basis van het hash-waarden uit één kolom distribueert</span><span class="sxs-lookup"><span data-stu-id="2c5f9-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="2c5f9-136">Standaard, wanneer u een distributiemethode gegevens niet definieert uw tabel worden gedistribueerd met behulp van Hallo **round-robin** distributiemethode.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="2c5f9-137">Echter, naarmate u meer geavanceerde in uw implementatie, zult u met behulp van tooconsider **hash gedistribueerd** toominimize gegevensverplaatsing die op zijn beurt queryprestaties optimaliseert tabellen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="2c5f9-138">Round Robin tabellen</span><span class="sxs-lookup"><span data-stu-id="2c5f9-138">Round Robin Tables</span></span>
<span data-ttu-id="2c5f9-139">Gebruik van Hallo Round Robin-methode voor het distribueren van gegevens is zeer veel hoe het klinkt.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="2c5f9-140">Als uw gegevens zijn geladen, wordt elke rij gewoon toohello volgende distributiepunt verzonden.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="2c5f9-141">Deze methode van het distribueren van Hallo gegevens wordt altijd willekeurig Hallo gegevens zeer gelijkmatig verdelen over alle Hallo-distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="2c5f9-142">Er is geen sorteren gereed tijdens Hallo round robin-proces waarop uw gegevens geplaatst.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="2c5f9-143">Een round robin-distributie is wel een willekeurige hash om deze reden.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="2c5f9-144">Met een gedistribueerde tabel round robin-zijn er geen noodzaak toounderstand Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="2c5f9-145">Round-Robin met tabellen kunnen daarom vaak goed laden doelen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="2c5f9-146">Standaard als er geen distributiemethode is gekozen, wordt hello distributiemethode round-robin gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="2c5f9-147">Terwijl round-robin tabellen eenvoudig toouse zijn omdat gegevens willekeurig is verdeeld over Hallo system dit betekent dat Hallo systeem biedt geen garantie van welke distributiepunten moet elke rij is echter op.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="2c5f9-148">Als gevolg hiervan zijn soms Hallo system tooinvoke nodig heeft om een data movement bewerking toobetter uw gegevens delen voordat het oplossen van een query.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="2c5f9-149">Deze extra stap kan uw query's vertragen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="2c5f9-150">Overweeg het gebruik van Round Robin distributie voor uw tabel in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="2c5f9-151">Wanneer aan de slag als een eenvoudige beginpunt</span><span class="sxs-lookup"><span data-stu-id="2c5f9-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="2c5f9-152">Als er geen duidelijke die sleutel is</span><span class="sxs-lookup"><span data-stu-id="2c5f9-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="2c5f9-153">Als er geen kolom met een goede kandidaat voor hash-tabel Hallo distribueren</span><span class="sxs-lookup"><span data-stu-id="2c5f9-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="2c5f9-154">Als hello delen tabel niet een gemeenschappelijke join-sleutel met andere tabellen</span><span class="sxs-lookup"><span data-stu-id="2c5f9-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="2c5f9-155">Als Hallo join is een minder belangrijke dan andere joins in Hallo-query</span><span class="sxs-lookup"><span data-stu-id="2c5f9-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="2c5f9-156">Wanneer Hallo-tabel is een tijdelijke tabel fasering</span><span class="sxs-lookup"><span data-stu-id="2c5f9-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="2c5f9-157">Beide voorbeelden maakt een tabel Round Robin:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="2c5f9-158">Tijdens een round-robin wordt Hallo tabel standaardtype expliciete in uw DDL wordt beschouwd als best practice zodat Hallo bedoelingen van de indeling van de tabel wissen tooothers zijn.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="2c5f9-159">Hash-tabellen gedistribueerde</span><span class="sxs-lookup"><span data-stu-id="2c5f9-159">Hash Distributed Tables</span></span>
<span data-ttu-id="2c5f9-160">Met behulp van een **Hash gedistribueerd** algoritme toodistribute uw tabellen kunnen de prestaties verbeteren voor veel scenario's door verplaatsing van gegevens op het moment dat de query.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="2c5f9-161">Hash gedistribueerde tabellen zijn tabellen die zijn verdeeld over de Hallo gedistribueerde databases met een hash-algoritme in één kolom die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="2c5f9-162">Hallo distributie kolom is wat bepaalt hoe gegevens Hallo is verdeeld over uw gedistribueerde databases.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="2c5f9-163">Hallo hash-functie maakt gebruik van Hallo distributie kolom tooassign rijen toodistributions.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="2c5f9-164">Hallo hash-algoritme en de resulterende distributie is deterministisch.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="2c5f9-165">Dat wil Hallo dezelfde waarde altijd hetzelfde gegevenstype wordt Hello toohello heeft hetzelfde distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="2c5f9-166">In dit voorbeeld maakt een tabel die wordt gedistribueerd bij-id:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="2c5f9-167">De kolom distributiepunten selecteren</span><span class="sxs-lookup"><span data-stu-id="2c5f9-167">Select distribution column</span></span>
<span data-ttu-id="2c5f9-168">Als u ervoor kiest te**hash distribueren** een tabel, moet u een kolom voor één distributiepunt tooselect.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="2c5f9-169">Wanneer u een distributie-kolom selecteert, zijn er drie belangrijke factoren tooconsider.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="2c5f9-170">Selecteer één kolom die wordt:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-170">Select a single column which will:</span></span>

1. <span data-ttu-id="2c5f9-171">Niet worden bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="2c5f9-171">Not be updated</span></span>
2. <span data-ttu-id="2c5f9-172">Verdelen gegevens, gegevens scheeftrekken voorkomen</span><span class="sxs-lookup"><span data-stu-id="2c5f9-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="2c5f9-173">Verplaatsing van gegevens beperken</span><span class="sxs-lookup"><span data-stu-id="2c5f9-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="2c5f9-174">Distributiepunten selecteren kolom die wordt niet bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="2c5f9-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="2c5f9-175">Distributiekolommen kunnen niet worden bijgewerkt, dus, selecteert u een kolom met statische waarden.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="2c5f9-176">Als een kolom toobe bijgewerkt moet, wordt dit doorgaans niet goed distributiepunt geschikt is.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="2c5f9-177">Als er een aanvraag waarin u een distributie-kolom moet bijwerken, kunt u dit doen door eerst Hallo rij te verwijderen en voegt vervolgens een nieuwe rij.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="2c5f9-178">Distributiepunten selecteren kolom die gegevens wordt gelijkmatig verdelen</span><span class="sxs-lookup"><span data-stu-id="2c5f9-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="2c5f9-179">Omdat alleen als de traagste distributie snel een gedistribueerd systeem wordt uitgevoerd, is het belangrijk toodivide Hallo werk gelijkmatig over Hallo distributies in volgorde tooachieve met gelijke taakverdeling worden uitgevoerd in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="2c5f9-180">Hallo manier Hallo werk is onderverdeeld in een gedistribueerde systeem is gebaseerd op waar gegevens voor elke distributie Hallo woont.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="2c5f9-181">Dit maakt het heel belangrijk tooselect Hallo rechts distributie kolom voor het distribueren van Hallo gegevens, zodat elke verdeling gelijk werk heeft en zal nemen Hallo dezelfde tijd toocomplete het gedeelte van het Hallo werk.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="2c5f9-182">Wanneer het werk goed is onderverdeeld in Hallo-systeem, wordt Hallo gegevens gelijkmatig over Hallo-distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="2c5f9-183">Wanneer gegevens niet gelijkmatig wordt verdeeld, noemen we dit **gegevens tijdverschil**.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="2c5f9-184">toodivide gegevens gelijkmatig en te voorkomen dat gegevens scheeftrekken, Hallo volgende denken bij het selecteren van de kolom distributie:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="2c5f9-185">Selecteer een kolom die een groot aantal afzonderlijke waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="2c5f9-186">Vermijd het distribueren van gegevens voor kolommen met een aantal afzonderlijke waarden.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="2c5f9-187">Vermijd het distribueren van gegevens voor kolommen met een hoge frequentie van null-waarden.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="2c5f9-188">Vermijd het distribueren van gegevens op datumkolommen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="2c5f9-189">Omdat elke waarde hash too1 van 60 distributies, zelfs distributie tooachieve zult u tooselect een kolom die maximaal uniek is en meer dan 60 unieke waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="2c5f9-190">tooillustrate, een situatie waarin een kolom alleen 40 unieke waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="2c5f9-191">Als deze kolom is geselecteerd als de distributiesleutel hello, zou Hallo-gegevens voor die tabel neerzetten op 40 distributies maximaal 20-distributies die met geen gegevens en geen toodo verwerking.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="2c5f9-192">Als u daarentegen er hello andere 40 distributies meer werk toodo dat als hello gegevens is gelijkmatig verspreid over 60 distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="2c5f9-193">Dit scenario is een voorbeeld van gegevens scheeftrekken.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="2c5f9-194">In de MPP-systeem, elke stap van de query wordt gewacht op alle distributies toocomplete hun aandeel van Hallo werk.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="2c5f9-195">Als een distributiepunt meer werk dan Hallo anderen, wordt de bron van het Hallo Hallo worden andere distributies in wezen NET wachten op Hallo bezet distributie verspild.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="2c5f9-196">Wanneer het werk niet gelijkmatig verdeeld over alle distributies, noemen we dit **verwerking scheeftrekken**.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="2c5f9-197">Verwerking tijdverschil zorgt ervoor dat de query's toorun langzamer dan als Hallo werkbelasting gelijkmatig kan worden verspreid via Hallo-distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="2c5f9-198">Gegevens tijdverschil leidt tooprocessing scheeftrekken.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="2c5f9-199">Vermijd distribueren op maximaal kolom zoals Hallo null-waarden worden alle land op Hallo dezelfde distributie.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="2c5f9-200">Distribueren op een datumkolom kan ook worden veroorzaakt verwerking scheeftrekken omdat alle gegevens voor een gegeven datum komt dan uit op Hallo dezelfde distributie.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="2c5f9-201">Als het uitvoeren van meerdere gebruikers worden query's alle filteren op Hallo dezelfde datum is, en vervolgens alleen 1 van 60 distributies Hallo al Hallo werk doen gaan aangezien een gegeven datum wordt slechts op één distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="2c5f9-202">Hallo-query's in dit scenario wordt waarschijnlijk 60 keer langzamer dan als Hallo gegevens gelijkmatig zijn verdeeld over alle Hallo distributies uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="2c5f9-203">Als er geen goede kandidaat kolommen bestaan, klikt u vervolgens kunt u overwegen round-robin als Hallo distributiemethode.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="2c5f9-204">Distributiepunten selecteren kolom verplaatsing van gegevens te minimaliseren</span><span class="sxs-lookup"><span data-stu-id="2c5f9-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="2c5f9-205">Verplaatsing van gegevens voor het minimaliseren Hallo rechts distributie kolom te selecteren, is een van de Hallo belangrijkste strategieën voor het optimaliseren van de prestaties van uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="2c5f9-206">Verplaatsing van gegevens ontstaat meestal als tabellen zijn gekoppeld of aggregaties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="2c5f9-207">Kolommen die worden gebruikt `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` en `HAVING` componenten alle maken voor **goed** hash-kandidaten voor distributie.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="2c5f9-208">Op Hallo daarentegen kolommen in Hallo `WHERE` component komen **niet** maken voor goede hash-kolom kandidaten omdat zij welke distributies deelnemen Hallo query beperken, waardoor verwerking scheeftrekken.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="2c5f9-209">Een goed voorbeeld van een kolom die mogelijk verleidelijk toodistribute op, maar vaak kan leiden tot deze scheeftrekken verwerking is een datumkolom.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="2c5f9-210">In het algemeen hebt u twee grote feitentabellen vaak die betrokken zijn in een join, krijgt u Hallo meeste prestaties door het distribueren van beide tabellen op een van de Hallo join-kolommen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="2c5f9-211">Als u een tabel die nooit gekoppelde tooanother grote feitentabel hebt, en zoek vervolgens toocolumns die vaak in Hallo `GROUP BY` component.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="2c5f9-212">Er zijn enkele belangrijke criteria wordt voldaan tooavoid gegevensverplaatsing tijdens een join:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="2c5f9-213">Hallo tabellen die zijn betrokken Hallo join moet hash gedistribueerd bij **één** Hallo kolommen die deel uitmaken van Hallo join.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="2c5f9-214">Hallo gegevenstypen van Hallo join-kolommen moeten tussen beide tabellen overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="2c5f9-215">Hallo-kolommen moeten worden toegevoegd met een operator equals.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="2c5f9-216">Hallo jointype niet mogelijk een `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="2c5f9-217">Analytische gegevens scheeftrekken</span><span class="sxs-lookup"><span data-stu-id="2c5f9-217">Troubleshooting data skew</span></span>
<span data-ttu-id="2c5f9-218">Wanneer tabelgegevens worden gedistribueerd met behulp van Hallo distributiemethode voor hash-er is vervormd een kans dat een aantal distributies wordt toohave niet goed meer gegevens dan andere.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="2c5f9-219">Veel gegevens scheeftrekken kan gevolgen voor queryprestaties omdat Hallo uiteindelijke resultaat van een gedistribueerde query Hallo langste actieve distributie toofinish moet wachten.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="2c5f9-220">Afhankelijk van de Hallo mate van Hallo gegevens scheeftrekken dat tooaddress moet u mogelijk het.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="2c5f9-221">Tijdverschil identificeren</span><span class="sxs-lookup"><span data-stu-id="2c5f9-221">Identifying skew</span></span>
<span data-ttu-id="2c5f9-222">Een eenvoudige manier tooidentify een tabel als vervormd is toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="2c5f9-223">Dit is een zeer snelle en eenvoudige manier toosee Hallo aantal rijen die zijn opgeslagen in elk Hallo 60 distributies van uw database.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="2c5f9-224">Houd er rekening mee dat voor de prestaties van de meest met gelijke taakverdeling Hallo Hallo rijen in een gedistribueerde moeten worden gelijkmatig verdeeld over alle Hallo-distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="2c5f9-225">Als u een query hello Azure SQL Data Warehouse dynamische beheerweergaven (DMV) kunt u een meer gedetailleerde analyse uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="2c5f9-226">toostart, Hallo weergave maken [dbo.vTableSizes] [ dbo.vTableSizes] bekijken met behulp van SQL van Hallo [tabel overzicht] [ Overview] artikel.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="2c5f9-227">Zodra Hallo weergave is gemaakt, worden deze query tooidentify welke tabellen meer dan 10% gegevens tijdverschil hebben uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="2c5f9-228">Het omzetten van gegevens scheeftrekken</span><span class="sxs-lookup"><span data-stu-id="2c5f9-228">Resolving data skew</span></span>
<span data-ttu-id="2c5f9-229">Niet alle scheeftrekken is voldoende toowarrant een oplossing.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="2c5f9-230">In sommige gevallen Hallo prestaties van een tabel in sommige query's kan bieden, opwegen tegen Hallo beschadiging van gegevens scheeftrekken.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="2c5f9-231">toodecide als u gegevens moet oplossen scheeftrekken in een tabel, moet u weten zo veel mogelijk over gegevensvolumes Hallo en query's in uw workload.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="2c5f9-232">Eenzijdige toolook op Hallo gevolgen van het tijdverschil is toouse Hallo stappen in Hallo [Query bewaking] [ Query Monitoring] artikel toomonitor Hallo gevolgen van het scheeftrekken op de prestaties van query's en specifiek Hallo impact toohow lange query's toocomplete ondernemen Hallo afzonderlijke distributies.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="2c5f9-233">Distributie van gegevens is een kwestie van het zoeken naar de juiste balans Hallo tussen gegevens tijdverschil minimaliseren en de verplaatsing van gegevens voor het minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="2c5f9-234">Deze doelstellingen kunnen tegengestelde en soms is het verstandig tookeep gegevens scheeftrekken in volgorde tooreduce gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="2c5f9-235">Bijvoorbeeld, wanneer de Hallo distributie kolom is vaak Hallo gedeelde kolom in samenvoegingen en aggregaties, zal u worden minimaliseren verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="2c5f9-236">Hallo voordeel dat de minimale gegevensverplaatsing Hallo kan bieden, opwegen tegen Hallo impact van leiden tot onjuiste gegevens.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="2c5f9-237">de gebruikelijke manier Hallo tooresolve gegevens tijdverschil toore is-Hallo-tabel maken met een ander distributiepunt-kolom.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="2c5f9-238">Omdat er geen enkele manier toochange Hallo distributie kolom op een bestaande tabel, Hallo manier toochange Hallo distributie van een tabel deze toorecreate deze met een [CTAS] [].</span><span class="sxs-lookup"><span data-stu-id="2c5f9-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="2c5f9-239">Hier vindt u twee voorbeelden van hoe u gegevens scheeftrekken oplossen:</span><span class="sxs-lookup"><span data-stu-id="2c5f9-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="2c5f9-240">Voorbeeld 1: Opnieuw Hallo tabel met een nieuwe kolom voor distributie maken</span><span class="sxs-lookup"><span data-stu-id="2c5f9-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="2c5f9-241">In dit voorbeeld wordt [CTAS] [] toore-Maak een tabel met een andere hash-distributie-kolom.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="2c5f9-242">Voorbeeld 2: Maak Hallo-tabel met behulp van round robin distributie</span><span class="sxs-lookup"><span data-stu-id="2c5f9-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="2c5f9-243">In dit voorbeeld wordt [CTAS] [] toore-Maak een tabel met round-robin in plaats van een hash-distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="2c5f9-244">Deze wijziging wordt zelfs gegevensdistributie Hallo kosten van de verplaatsing van grotere hoeveelheden gegevens produceren.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="2c5f9-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c5f9-245">Next steps</span></span>
<span data-ttu-id="2c5f9-246">toolearn meer informatie over het ontwerp van de tabel Zie Hallo [distribueren][Distribute], [Index][Index], [partitie] [ Partition], [Gegevenstypen][Data Types], [statistieken] [ Statistics] en [tijdelijke tabellen] [ Temporary] artikelen.</span><span class="sxs-lookup"><span data-stu-id="2c5f9-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="2c5f9-247">Zie voor een overzicht van best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2c5f9-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
