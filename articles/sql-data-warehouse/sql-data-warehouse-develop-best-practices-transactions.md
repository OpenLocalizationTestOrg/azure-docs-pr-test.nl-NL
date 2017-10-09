---
title: aaaOptimizing transacties voor SQL Data Warehouse | Microsoft Docs
description: "Aanbevolen procedurerichtlijn over het schrijven van efficiënte transactie-updates in Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="4699e-103">Optimaliseren van transacties voor SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4699e-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="4699e-104">Dit artikel wordt uitgelegd hoe toooptimize Hallo prestaties van uw code transactionele terwijl het risico voor lange Rollback minimaliseert.</span><span class="sxs-lookup"><span data-stu-id="4699e-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="4699e-105">Transacties en logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="4699e-105">Transactions and logging</span></span>
<span data-ttu-id="4699e-106">Transacties zijn een belangrijk onderdeel van een relationele database-engine.</span><span class="sxs-lookup"><span data-stu-id="4699e-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="4699e-107">SQL Data Warehouse maakt gebruik van transacties tijdens het aanpassen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4699e-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="4699e-108">Deze transacties kunnen expliciete of impliciete zijn.</span><span class="sxs-lookup"><span data-stu-id="4699e-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="4699e-109">Één `INSERT`, `UPDATE` en `DELETE` -instructies zijn alle voorbeelden van impliciete transacties.</span><span class="sxs-lookup"><span data-stu-id="4699e-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="4699e-110">Expliciete transacties expliciet worden geschreven door een ontwikkelaar met behulp van `BEGIN TRAN`, `COMMIT TRAN` of `ROLLBACK TRAN` en worden doorgaans gebruikt wanneer meerdere wijziging instructies nodig toobe aan elkaar gekoppeld in een atomic-eenheid.</span><span class="sxs-lookup"><span data-stu-id="4699e-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="4699e-111">Azure SQL Data Warehouse voert wijzigingen toohello database met behulp van transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="4699e-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="4699e-112">Elk distributiepunt heeft een eigen transactielogboek.</span><span class="sxs-lookup"><span data-stu-id="4699e-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="4699e-113">Transactie logboekschrijfbewerkingen worden automatisch.</span><span class="sxs-lookup"><span data-stu-id="4699e-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="4699e-114">Er is geen configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="4699e-114">There is no configuration required.</span></span> <span data-ttu-id="4699e-115">Tijdens dit proces wordt gegarandeerd dat Hallo schrijven deze een overhead introduceren in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="4699e-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="4699e-116">U kunt deze gevolgen minimaliseren door transactioneel efficiënte code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="4699e-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="4699e-117">Transactioneel efficiënte code grote schaal worden onderverdeeld in twee categorieën.</span><span class="sxs-lookup"><span data-stu-id="4699e-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="4699e-118">Waar mogelijk gebruikmaken van minimale logboekregistratie constructies</span><span class="sxs-lookup"><span data-stu-id="4699e-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="4699e-119">Procesgegevens met behulp van ingedeeld batches tooavoid enkelvoudige langlopende transacties</span><span class="sxs-lookup"><span data-stu-id="4699e-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="4699e-120">Een patroon voor grote wijzigingen tooa opgegeven partitie overschakelen partitie vaststellen</span><span class="sxs-lookup"><span data-stu-id="4699e-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="4699e-121">Minimale versus volledige logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="4699e-121">Minimal vs. full logging</span></span>
<span data-ttu-id="4699e-122">In tegenstelling tot volledig geregistreerde bewerkingen, die gebruikmaken van Hallo transactie logboek tookeep bijhouden van elke rijwijziging, minimaal geregistreerde bewerkingen van bijhouden mate toewijzingen, en alleen de wijzigingen voor de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="4699e-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="4699e-123">Daarom minimale logboekregistratie omvat logboekregistratie alleen Hallo-informatie die is vereist toorollback Hallo transactie in Hallo gebeurtenis van een storing of een expliciete aanvraag (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="4699e-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="4699e-124">Omdat veel minder gegevens worden bijgehouden in het transactielogboek hello, presteert een minimaal geregistreerde bewerking beter dan een vergelijkbaar formaat volledig geregistreerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="4699e-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="4699e-125">Bovendien, omdat minder schrijfbewerkingen transactielogboek hello gaat, een veel kleinere hoeveelheid gegevens aan het logboek is gegenereerd en dus meer i/o efficiënt.</span><span class="sxs-lookup"><span data-stu-id="4699e-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="4699e-126">Hallo transactie veiligheid limieten gelden alleen bewerkingen toofully geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="4699e-127">Minimaal geregistreerde bewerkingen kunnen deelnemen aan expliciete transacties.</span><span class="sxs-lookup"><span data-stu-id="4699e-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="4699e-128">Zoals alle wijzigingen in de toewijzing van structuren worden bijgehouden, is het mogelijk tooroll back minimaal bewerkingen in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="4699e-129">Het is belangrijk toounderstand die Hallo wijziging 'minimaal' is het logboek geregistreerd niet is niet geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="4699e-130">Minimaal geregistreerde bewerkingen</span><span class="sxs-lookup"><span data-stu-id="4699e-130">Minimally logged operations</span></span>
<span data-ttu-id="4699e-131">Hallo zijn volgende bewerkingen geschikt voor minimaal aan te melden:</span><span class="sxs-lookup"><span data-stu-id="4699e-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="4699e-132">MAAK TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="4699e-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="4699e-133">INSERT... SELECTEER</span><span class="sxs-lookup"><span data-stu-id="4699e-133">INSERT..SELECT</span></span>
* <span data-ttu-id="4699e-134">INDEX MAKEN</span><span class="sxs-lookup"><span data-stu-id="4699e-134">CREATE INDEX</span></span>
* <span data-ttu-id="4699e-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="4699e-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="4699e-136">INDEX VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="4699e-136">DROP INDEX</span></span>
* <span data-ttu-id="4699e-137">TABEL AFKAPPEN</span><span class="sxs-lookup"><span data-stu-id="4699e-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="4699e-138">TABEL VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="4699e-138">DROP TABLE</span></span>
* <span data-ttu-id="4699e-139">ALTER TABLE SWITCH PARTITIE</span><span class="sxs-lookup"><span data-stu-id="4699e-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="4699e-140">Interne data movement-bewerkingen (zoals `BROADCAST` en `SHUFFLE`) worden niet beïnvloed door Hallo transactie veiligheid limiet.</span><span class="sxs-lookup"><span data-stu-id="4699e-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="4699e-141">Minimale logboekregistratie met bulksgewijs laden</span><span class="sxs-lookup"><span data-stu-id="4699e-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="4699e-142">`CTAS`en `INSERT...SELECT` zijn beide bulksgewijs laden bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4699e-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="4699e-143">Echter beide zijn beïnvloed door de tabeldefinitie Hallo-doel en zijn afhankelijk van Hallo load scenario.</span><span class="sxs-lookup"><span data-stu-id="4699e-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="4699e-144">Hieronder vindt u een tabel met uitleg over als uw bulkbewerking volledig of minimaal geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="4699e-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="4699e-145">Primaire Index</span><span class="sxs-lookup"><span data-stu-id="4699e-145">Primary Index</span></span> | <span data-ttu-id="4699e-146">Load Scenario</span><span class="sxs-lookup"><span data-stu-id="4699e-146">Load Scenario</span></span> | <span data-ttu-id="4699e-147">Modus voor logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="4699e-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4699e-148">Object-heap</span><span class="sxs-lookup"><span data-stu-id="4699e-148">Heap</span></span> |<span data-ttu-id="4699e-149">Alle</span><span class="sxs-lookup"><span data-stu-id="4699e-149">Any</span></span> |<span data-ttu-id="4699e-150">**Minimale**</span><span class="sxs-lookup"><span data-stu-id="4699e-150">**Minimal**</span></span> |
| <span data-ttu-id="4699e-151">Geclusterde Index</span><span class="sxs-lookup"><span data-stu-id="4699e-151">Clustered Index</span></span> |<span data-ttu-id="4699e-152">Lege doeltabel</span><span class="sxs-lookup"><span data-stu-id="4699e-152">Empty target table</span></span> |<span data-ttu-id="4699e-153">**Minimale**</span><span class="sxs-lookup"><span data-stu-id="4699e-153">**Minimal**</span></span> |
| <span data-ttu-id="4699e-154">Geclusterde Index</span><span class="sxs-lookup"><span data-stu-id="4699e-154">Clustered Index</span></span> |<span data-ttu-id="4699e-155">Geladen rijen niet overlappen met bestaande pagina's in het doel</span><span class="sxs-lookup"><span data-stu-id="4699e-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="4699e-156">**Minimale**</span><span class="sxs-lookup"><span data-stu-id="4699e-156">**Minimal**</span></span> |
| <span data-ttu-id="4699e-157">Geclusterde Index</span><span class="sxs-lookup"><span data-stu-id="4699e-157">Clustered Index</span></span> |<span data-ttu-id="4699e-158">Geladen rijen overlappen met bestaande pagina's in het doel</span><span class="sxs-lookup"><span data-stu-id="4699e-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="4699e-159">Volledig</span><span class="sxs-lookup"><span data-stu-id="4699e-159">Full</span></span> |
| <span data-ttu-id="4699e-160">Geclusterde Columnstore-Index</span><span class="sxs-lookup"><span data-stu-id="4699e-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="4699e-161">Batchgrootte > = 102,400 per partitie uitgelijnd distributie</span><span class="sxs-lookup"><span data-stu-id="4699e-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="4699e-162">**Minimale**</span><span class="sxs-lookup"><span data-stu-id="4699e-162">**Minimal**</span></span> |
| <span data-ttu-id="4699e-163">Geclusterde Columnstore-Index</span><span class="sxs-lookup"><span data-stu-id="4699e-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="4699e-164">Batch-grootte < 102,400 per partitie uitgelijnd distributie</span><span class="sxs-lookup"><span data-stu-id="4699e-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="4699e-165">Volledig</span><span class="sxs-lookup"><span data-stu-id="4699e-165">Full</span></span> |

<span data-ttu-id="4699e-166">Hierbij moet worden opgemerkt dat er geen schrijfbewerkingen tooupdate secundaire of door de niet-geclusterde indexen altijd volledig worden operations geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4699e-167">SQL Data Warehouse is 60 distributies.</span><span class="sxs-lookup"><span data-stu-id="4699e-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="4699e-168">Daarom, ervan uitgaande dat alle rijen gelijkmatig worden verdeeld en aanvoer in één partitie, uw batch moet toocontain 6,144,000 rijen bevatten of groter toobe minimaal geregistreerd bij het schrijven van tooa geclusterde Columnstore-Index.</span><span class="sxs-lookup"><span data-stu-id="4699e-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="4699e-169">Als Hallo-tabel is gepartitioneerd en Hallo rijen worden ingevoegd span grenzen van partities, moet u 6,144,000 rijen per partitie grens ervan uitgaande dat zelfs gegevensdistributie.</span><span class="sxs-lookup"><span data-stu-id="4699e-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="4699e-170">Elke partitie in elk distributiepunt moet onafhankelijk Hallo 102.400 rij drempelwaarde overschrijden voor Hallo insert toobe aangemeld minimaal Hallo distributie.</span><span class="sxs-lookup"><span data-stu-id="4699e-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="4699e-171">Laden van gegevens naar een niet-lege tabel met een geclusterde index kunt bevatten vaak een combinatie van volledig vastgelegd en minimaal geregistreerde rijen.</span><span class="sxs-lookup"><span data-stu-id="4699e-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="4699e-172">Een geclusterde index is een evenwichtige structuur (b-tree) van pagina's.</span><span class="sxs-lookup"><span data-stu-id="4699e-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="4699e-173">Als Hallo pagina geschreven tooalready bevat rijen uit een andere transactie, wordt klikt u vervolgens deze schrijfbewerkingen volledig vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="4699e-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="4699e-174">Echter als Hallo pagina leeg vervolgens Hallo schrijven toothat pagina minimaal geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="4699e-175">Hiermee verwijdert u optimaliseren</span><span class="sxs-lookup"><span data-stu-id="4699e-175">Optimizing deletes</span></span>
<span data-ttu-id="4699e-176">`DELETE`is een volledig geregistreerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="4699e-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="4699e-177">Als u een grote hoeveelheid gegevens in een tabel of een partitie toodelete nodig, het vaak zinvol meer te`SELECT` Hallo gegevens u wenst dat tookeep die kan worden uitgevoerd als een minimaal geregistreerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="4699e-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="4699e-178">tooaccomplish, maak een nieuwe tabel met [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="4699e-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="4699e-179">Zodra u hebt gemaakt, gebruikt u [naam] [ RENAME] tooswap uit uw oude tabel met nieuwe Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="4699e-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="4699e-180">Updates optimaliseren</span><span class="sxs-lookup"><span data-stu-id="4699e-180">Optimizing updates</span></span>
<span data-ttu-id="4699e-181">`UPDATE`is een volledig geregistreerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="4699e-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="4699e-182">Als u tooupdate een groot aantal rijen in een tabel moet zijn of een partitie vaak veel efficiënter toouse een minimaal geregistreerde bewerking zoals [CTAS] [ CTAS] toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="4699e-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="4699e-183">Hallo voorbeeld hieronder een update van de volledige tabel is geconverteerd tooa `CTAS` zodat minimale logboekregistratie mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="4699e-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="4699e-184">In dit geval toevoegen we achteraf een korting bedrag toohello verkoop in Hallo tabel:</span><span class="sxs-lookup"><span data-stu-id="4699e-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="4699e-185">Opnieuw maken van grote tabellen kan profiteren van beheerfuncties voor SQL Data Warehouse werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="4699e-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="4699e-186">Voor meer informatie raadpleegt u toohello werkbelasting-sectie in management in Hallo [gelijktijdigheid] [ concurrency] artikel.</span><span class="sxs-lookup"><span data-stu-id="4699e-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="4699e-187">Aan het overschakelen van de partitie optimaliseren</span><span class="sxs-lookup"><span data-stu-id="4699e-187">Optimizing with partition switching</span></span>
<span data-ttu-id="4699e-188">Als u bijvoorbeeld grote schaal wijzigingen in een [tabel partitie][table partition], en vervolgens een partitie overschakelen patroon een groot aantal zin maakt.</span><span class="sxs-lookup"><span data-stu-id="4699e-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="4699e-189">Hallo wijziging van gegevens is van belang als meerdere partities, gewoon sequentieel via Hallo partities realiseert reeksen Hallo hetzelfde resultaat.</span><span class="sxs-lookup"><span data-stu-id="4699e-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="4699e-190">Hallo stappen tooperform een switch partitie zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="4699e-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="4699e-191">Maak een lege van de partitie</span><span class="sxs-lookup"><span data-stu-id="4699e-191">Create an empty out partition</span></span>
2. <span data-ttu-id="4699e-192">Hallo 'update' uitvoeren als een CTAS</span><span class="sxs-lookup"><span data-stu-id="4699e-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="4699e-193">Overschakelen van bestaande gegevens toohello Hallo uit de tabel</span><span class="sxs-lookup"><span data-stu-id="4699e-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="4699e-194">In de nieuwe gegevens Hallo-switch</span><span class="sxs-lookup"><span data-stu-id="4699e-194">Switch in hello new data</span></span>
5. <span data-ttu-id="4699e-195">Hallo gegevens opschonen</span><span class="sxs-lookup"><span data-stu-id="4699e-195">Clean up hello data</span></span>

<span data-ttu-id="4699e-196">Toohelp identificeren echter Hallo partities tooswitch we moet eerst een procedure helper zoals Hallo een toobuild hieronder.</span><span class="sxs-lookup"><span data-stu-id="4699e-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="4699e-197">Deze procedure maximaliseert de code opnieuw te gebruiken en houdt Hallo partitie voorbeeld compacter overschakelen.</span><span class="sxs-lookup"><span data-stu-id="4699e-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="4699e-198">Hallo-code hieronder laat zien Hallo vijf stappen hierboven tooachieve vermeld met een volledige partitie routine overschakelen.</span><span class="sxs-lookup"><span data-stu-id="4699e-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="4699e-199">Logboekregistratie met kleine batches minimaliseren</span><span class="sxs-lookup"><span data-stu-id="4699e-199">Minimize logging with small batches</span></span>
<span data-ttu-id="4699e-200">Voor bewerkingen voor het wijzigen van grote hoeveelheden gegevens kan het zin toodivide Hallo bewerking in segmenten of batches tooscope Hallo-eenheid van het werk te doen.</span><span class="sxs-lookup"><span data-stu-id="4699e-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="4699e-201">Hieronder vindt u een voorbeeld van een werkende.</span><span class="sxs-lookup"><span data-stu-id="4699e-201">A working example is provided below.</span></span> <span data-ttu-id="4699e-202">Hallo batchgrootte is tooa trivial nummer toohighlight Hallo techniek ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4699e-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="4699e-203">In werkelijkheid zou Hallo batchgrootte aanzienlijk groter worden.</span><span class="sxs-lookup"><span data-stu-id="4699e-203">In reality hello batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="4699e-204">Onderbreken en richtlijnen schalen</span><span class="sxs-lookup"><span data-stu-id="4699e-204">Pause and scaling guidance</span></span>
<span data-ttu-id="4699e-205">Azure SQL Data Warehouse kunt u onderbreken, hervatten en schalen van uw datawarehouse op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4699e-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="4699e-206">Wanneer u onderbreken of schalen van uw SQL Data Warehouse is het belangrijk toounderstand dat onderweg transacties onmiddellijk; zijn beëindigd veroorzaakt door een toobe open transacties teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="4699e-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="4699e-207">Als uw werkbelasting heeft afgegeven een langlopende en onvolledige gegevenswijziging voorafgaande moet toohello onderbreken of schaalaanpassing, wordt dit werk toobe ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4699e-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="4699e-208">Dit mogelijk invloed op Hallo duurt toopause of schalen van uw Azure SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="4699e-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4699e-209">Beide `UPDATE` en `DELETE` zijn volledig geregistreerde bewerkingen en zodat deze ongedaan maken/opnieuw bewerkingen kunnen aanzienlijk langer duren dan equivalent minimaal operations geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4699e-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="4699e-210">Hallo beste scenario is toolet in vlucht gegevens wijziging transacties voltooid voorafgaande toopausing of vergroten/verkleinen SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4699e-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="4699e-211">Maar kan dit niet altijd praktisch zijn.</span><span class="sxs-lookup"><span data-stu-id="4699e-211">However, this may not always be practical.</span></span> <span data-ttu-id="4699e-212">toomitigate hello risico een lange terugdraaiactie heeft plaatsgevonden, overweeg dan een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="4699e-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="4699e-213">Herschrijven langlopende bewerkingen met behulp van [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="4699e-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="4699e-214">Hallo bewerking onderverdelen in stukken verdeeld; uitgevoerd op een subset van Hallo rijen</span><span class="sxs-lookup"><span data-stu-id="4699e-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="4699e-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4699e-215">Next steps</span></span>
<span data-ttu-id="4699e-216">Zie [transacties in SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn meer over isolatieniveaus en transactionele limieten.</span><span class="sxs-lookup"><span data-stu-id="4699e-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="4699e-217">Zie voor een overzicht van de andere aanbevelingen [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="4699e-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

