---
title: aaaPartitioning tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met Tabelpartities in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="8e911-103">Tabellen in SQL Data Warehouse partitioneren</span><span class="sxs-lookup"><span data-stu-id="8e911-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8e911-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="8e911-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="8e911-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="8e911-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="8e911-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8e911-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="8e911-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="8e911-107">[Index][Index]</span></span>
> * <span data-ttu-id="8e911-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="8e911-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="8e911-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8e911-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="8e911-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8e911-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="8e911-111">Partitioneren wordt ondersteund op alle SQL Data Warehouse tabeltypen; inclusief geclusterde columnstore geclusterde index en heap.</span><span class="sxs-lookup"><span data-stu-id="8e911-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="8e911-112">Partitioneren wordt ook ondersteund voor alle typen distributiepunten, inclusief zowel hash of round-robin gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="8e911-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="8e911-113">Partitioneren, kunt u uw gegevens in kleinere groepen van gegevens en in de meeste gevallen partitioneren is uitgevoerd op een datumkolom toodivide.</span><span class="sxs-lookup"><span data-stu-id="8e911-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="8e911-114">Voordelen van het partitioneren</span><span class="sxs-lookup"><span data-stu-id="8e911-114">Benefits of partitioning</span></span>
<span data-ttu-id="8e911-115">Partitioneren, profiteert gegevens onderhoud en query-prestaties.</span><span class="sxs-lookup"><span data-stu-id="8e911-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="8e911-116">Hiermee wordt aangegeven of deze voordelen biedt voor beide of slechts één is afhankelijk van hoe gegevens worden geladen en of hello dezelfde kolom kan worden gebruikt voor beide doeleinden, omdat het partitioneren kan alleen worden uitgevoerd op één kolom.</span><span class="sxs-lookup"><span data-stu-id="8e911-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="8e911-117">Voordelen tooloads</span><span class="sxs-lookup"><span data-stu-id="8e911-117">Benefits tooloads</span></span>
<span data-ttu-id="8e911-118">Hallo belangrijkste voordeel van het partitioneren in SQL datawarehouse is verbeteren Hallo efficiëntie en prestaties van het laden van gegevens via het gebruik van de partitie verwijderen, overschakelen en samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="8e911-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="8e911-119">Kolom die nauw gekoppeld in de meeste gevallen gegevens op een datum is gepartitioneerd toohello volgorde welke Hallo-gegevens geladen toohello database zijn.</span><span class="sxs-lookup"><span data-stu-id="8e911-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="8e911-120">Een van de grootste voordelen van het gebruik van partities toomaintain gegevens het vermijden van transactielogboeken Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e911-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="8e911-121">Gewoon invoegen, bijwerken of verwijderen van gegevens kan de eenvoudigste manier Hallo met een beetje gedachte en moeite, zijn met behulp van partities tijdens het laadproces aanzienlijk prestaties kan verbeteren.</span><span class="sxs-lookup"><span data-stu-id="8e911-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="8e911-122">Overschakelen van de partitie kan gebruikte tooquickly verwijderen of een gedeelte van een tabel te vervangen.</span><span class="sxs-lookup"><span data-stu-id="8e911-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="8e911-123">Bijvoorbeeld, een verkoop feitentabel bevat mogelijk alleen gegevens voor Hallo afgelopen 36 maanden.</span><span class="sxs-lookup"><span data-stu-id="8e911-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="8e911-124">Aan het einde van de Hallo van elke maand, wordt hello oudste maand verkoopgegevens verwijderd uit Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="8e911-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="8e911-125">Deze gegevens kan worden verwijderd met behulp van een delete-instructie toodelete Hallo-gegevens voor Hallo oudste maand.</span><span class="sxs-lookup"><span data-stu-id="8e911-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="8e911-126">Echter kan verwijderen van een grote hoeveelheid gegevens per rij met een delete-instructie erg lang duren, evenals Hallo risico van grote transacties die een toorollback lang duren kan als er iets mis gaat maken.</span><span class="sxs-lookup"><span data-stu-id="8e911-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="8e911-127">Een meer optimale aanpak is toosimply neerzetten Hallo oudste partitie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8e911-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="8e911-128">Waar verwijderen van afzonderlijke rijen Hallo kan uren duren, kan verwijderen van een volledige partitie seconden duren.</span><span class="sxs-lookup"><span data-stu-id="8e911-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="8e911-129">Voordelen tooqueries</span><span class="sxs-lookup"><span data-stu-id="8e911-129">Benefits tooqueries</span></span>
<span data-ttu-id="8e911-130">Gebruikte tooimprove queryprestaties kan ook worden veroorzaakt partitioneren.</span><span class="sxs-lookup"><span data-stu-id="8e911-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="8e911-131">Als een query wordt een filter op een gepartitioneerde kolom toegepast, kan dit Hallo scan tooonly Hallo in aanmerking komende partities die mogelijk een veel kleinere subset uit Hallo gegevens, waardoor het voorkomen van een volledige tabelscan beperken.</span><span class="sxs-lookup"><span data-stu-id="8e911-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="8e911-132">Met Hallo introductie van geclusterde kolomopslagindexen, Hallo predikaat eliminatie prestatievoordelen minder nuttige, maar in sommige gevallen kan er een voordeel tooqueries.</span><span class="sxs-lookup"><span data-stu-id="8e911-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="8e911-133">Bijvoorbeeld, als Hallo verkoop feitentabel in 36 maanden met behulp van de verkoop datumveld Hallo is gepartitioneerd, kunnen vervolgens query's die op Hallo Verkoopdatum filteren overslaan zoeken in partities die niet overeenkomen met de Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="8e911-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="8e911-134">Richtlijn voor partitie</span><span class="sxs-lookup"><span data-stu-id="8e911-134">Partition sizing guidance</span></span>
<span data-ttu-id="8e911-135">Bij het partitioneren van prestaties van de gebruikte tooimprove sommige scenario's voor het maken van een tabel met kan worden **te veel** partities prestaties in bepaalde omstandigheden kunnen schaden.</span><span class="sxs-lookup"><span data-stu-id="8e911-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="8e911-136">Deze problemen zijn vooral voor geclusterde columnstore-tabellen.</span><span class="sxs-lookup"><span data-stu-id="8e911-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="8e911-137">Voor het partitioneren toobe handig zijn, is het belangrijk toounderstand wanneer toouse partitionerings- en Hallo aantal partities toocreate.</span><span class="sxs-lookup"><span data-stu-id="8e911-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="8e911-138">Er is geen vaste snelle regel als toohow veel partities zijn te veel, dit is afhankelijk van uw gegevens en het aantal partities u toosimultaneously laadt.</span><span class="sxs-lookup"><span data-stu-id="8e911-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="8e911-139">Maar als een algemene vuistregel Denk toe te voegen per 10 too100s met partities, niet 1000s.</span><span class="sxs-lookup"><span data-stu-id="8e911-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="8e911-140">Bij het maken van partities op **geclusterde columnstore** tabellen, het is belangrijk tooconsider komt dan uit hoeveel rijen in elke partitie.</span><span class="sxs-lookup"><span data-stu-id="8e911-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="8e911-141">Voor optimale compressie en prestaties van de geclusterde columnstore-tabellen, is een minimum van 1 miljoen rijen per partitie distributie en het nodig.</span><span class="sxs-lookup"><span data-stu-id="8e911-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="8e911-142">Voordat partities worden gemaakt, wordt elke tabel al verdeeld met SQL Data Warehouse in 60 gedistribueerde databases.</span><span class="sxs-lookup"><span data-stu-id="8e911-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="8e911-143">Elke partitionering toegevoegde tooa-tabel is bovendien toohello distributies achter de schermen Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8e911-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="8e911-144">In dit voorbeeld gebruiken als Hallo verkoop feitentabel 36 maandelijkse partities bevat, en het gezien het feit dat SQL Data Warehouse 60 distributies is vervolgens Hallo verkoop feit tabel 60 miljoen rijen per maand of 2.1 miljard rijen moet bevatten wanneer alle maanden worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="8e911-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="8e911-145">Als een tabel aanzienlijk minder rijen dan Hallo minimum aantal rijen per partitie aanbevolen bevat, kunt u overwegen minder partities in volgorde toomake toename Hallo aantal rijen per partitie.</span><span class="sxs-lookup"><span data-stu-id="8e911-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="8e911-146">Zie ook Hallo [indexering] [ Index] artikel waaronder query's die kunnen worden uitgevoerd op de SQL Data Warehouse tooassess Hallo kwaliteit van de cluster columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="8e911-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="8e911-147">Syntaxis verschil van SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e911-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="8e911-148">SQL Data Warehouse introduceert een vereenvoudigde definitie van de partities die enigszins van SQL Server verschilt.</span><span class="sxs-lookup"><span data-stu-id="8e911-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="8e911-149">Partitionering functies en schema's worden niet gebruikt in SQL Data Warehouse omdat ze zich in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8e911-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="8e911-150">In plaats daarvan toodo hoeft u gepartitioneerde punten voor kolom- en Hallo grens te identificeren.</span><span class="sxs-lookup"><span data-stu-id="8e911-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="8e911-151">Tijdens het Hallo-syntaxis van het partitioneren van mogelijk enigszins afwijken van de SQL Server, worden de basisconcepten Hallo Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="8e911-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="8e911-152">SQL Server en SQL Data Warehouse ondersteuning voor één partitiekolom per tabel, wat kan varieerde partitie.</span><span class="sxs-lookup"><span data-stu-id="8e911-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="8e911-153">toolearn meer informatie over partitioneren, Zie [gepartitioneerde tabellen en indexen][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="8e911-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="8e911-154">Hallo onderstaand voorbeeld van een SQL Data Warehouse gepartitioneerd [CREATE TABLE] [ CREATE TABLE] -instructie partities Hallo heeft tabel op de Hallo OrderDateKey kolom:</span><span class="sxs-lookup"><span data-stu-id="8e911-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="8e911-155">Partitioneren van SQL-Server migreren</span><span class="sxs-lookup"><span data-stu-id="8e911-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="8e911-156">SQL Server toomigrate partitie definities tooSQL Data Warehouse gewoon:</span><span class="sxs-lookup"><span data-stu-id="8e911-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="8e911-157">Hallo SQL Server elimineren [partitieschema][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="8e911-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="8e911-158">Hallo toevoegen [partitiefunctie] [ partition function] definitie tooyour tabel maken.</span><span class="sxs-lookup"><span data-stu-id="8e911-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="8e911-159">Als u een gepartitioneerde tabel van een SQL Server-exemplaar Hallo hieronder SQL migreert kunt u toointerrogate Hallo aantal rijen dat in elke partitie.</span><span class="sxs-lookup"><span data-stu-id="8e911-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="8e911-160">Houd er rekening mee dat als hello dezelfde partitionering granulariteit wordt gebruikt in SQL Data Warehouse, het aantal rijen per partitie Hallo met een factor van 60 neemt.</span><span class="sxs-lookup"><span data-stu-id="8e911-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="8e911-161">Werklastbeheer</span><span class="sxs-lookup"><span data-stu-id="8e911-161">Workload management</span></span>
<span data-ttu-id="8e911-162">Is een sluitstuk overweging toofactor in toohello tabel partitie besluit [werkbelasting management][workload management].</span><span class="sxs-lookup"><span data-stu-id="8e911-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="8e911-163">Beheer van de werkbelasting in SQL Data Warehouse is voornamelijk Hallo beheer van geheugen en een gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="8e911-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="8e911-164">Maximaal geheugen toegewezen tooeach distributie tijdens de uitvoering van de query is in SQL Data Warehouse Hallo geregeld resource klassen.</span><span class="sxs-lookup"><span data-stu-id="8e911-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="8e911-165">De partities wordt in het ideale geval worden aangepast met het oog andere factoren zoals Hallo geheugenvereisten van het bouwen van de geclusterde columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="8e911-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="8e911-166">Geclusterde columnstore-indexen voordeel aanzienlijk wanneer ze meer geheugen worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8e911-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="8e911-167">Daarom wilt u tooensure die een index met partitie opnieuw maken is niet tekort komt geheugen.</span><span class="sxs-lookup"><span data-stu-id="8e911-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="8e911-168">Uitbreiding Hallo en de hoeveelheid geheugen beschikbaar tooyour query kan worden bereikt door het overschakelen van standaardrol hello, smallrc, tooone van andere functies, zoals largerc Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e911-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="8e911-169">Informatie over het Hallo-toewijzing van geheugen per distributie is beschikbaar door het uitvoeren van query's Hallo resource gouverneur dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="8e911-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="8e911-170">In werkelijkheid wordt uw geheugentoekenning niet kleiner zijn dan Hallo onderstaande afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="8e911-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="8e911-171">Dit biedt echter een niveau van de richtlijnen die u gebruiken kunt wanneer het formaat van partities voor gegevens beheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8e911-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="8e911-172">Probeer het formaat van uw partities groter dan Hallo geheugentoekenning geleverd door de extra grote resourceklasse hello tooavoid.</span><span class="sxs-lookup"><span data-stu-id="8e911-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="8e911-173">Als uw partities afgezien van deze afbeelding groeien loopt u Hallo risico van geheugendruk wat op zijn beurt tooless optimale compressie leidt.</span><span class="sxs-lookup"><span data-stu-id="8e911-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="8e911-174">Partitie overschakelen</span><span class="sxs-lookup"><span data-stu-id="8e911-174">Partition switching</span></span>
<span data-ttu-id="8e911-175">SQL Data Warehouse ondersteunt partitie splitsen en overschakelen samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="8e911-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="8e911-176">Elk van deze functies is excuted met Hallo [ALTER TABLE] [ ALTER TABLE] instructie.</span><span class="sxs-lookup"><span data-stu-id="8e911-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="8e911-177">tooswitch partities tussen twee tabellen, die u ervoor zorgen moet dat Hallo partities zijn uitgelijnd op hun respectieve grenzen en Hallo tabeldefinities overeen met.</span><span class="sxs-lookup"><span data-stu-id="8e911-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="8e911-178">Als de check-beperkingen zijn niet beschikbaar tooenforce Hallo bereik van waarden in de brontabel van een tabel Hallo Hallo moet bevatten dezelfde partitie grenzen als Hallo doeltabel.</span><span class="sxs-lookup"><span data-stu-id="8e911-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="8e911-179">Als dit niet Hallo geval mislukken Hallo partitie switch als Hallo partitiemetagegevens niet gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="8e911-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="8e911-180">Hoe toosplit een partitie die gegevens bevat</span><span class="sxs-lookup"><span data-stu-id="8e911-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="8e911-181">Hallo efficiëntste methode toosplit een partitie die al gegevens bevat is toouse een `CTAS` instructie.</span><span class="sxs-lookup"><span data-stu-id="8e911-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="8e911-182">Als Hallo gepartitioneerde tabel een geclusterde columnstore moet vervolgens Hallo tabel partitie niet leeg zijn voordat deze kan worden gesplitst.</span><span class="sxs-lookup"><span data-stu-id="8e911-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="8e911-183">Hieronder volgt een voorbeeld-gepartitioneerde columnstore-tabel met één rij in elke partitie:</span><span class="sxs-lookup"><span data-stu-id="8e911-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="8e911-184">Door Creating Hallo statistiek object, zorgen wij ervoor dat tabelmetagegevens nauwkeuriger zijn.</span><span class="sxs-lookup"><span data-stu-id="8e911-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="8e911-185">Als we het maken van statistieken weglaat, wordt SQL Data Warehouse standaardwaarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e911-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="8e911-186">Voor meer informatie over statistieken Controleer [statistieken][statistics].</span><span class="sxs-lookup"><span data-stu-id="8e911-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="8e911-187">We kunnen vervolgens zoeken naar aantal Hallo-rijen met Hallo `sys.partitions` catalogusweergave:</span><span class="sxs-lookup"><span data-stu-id="8e911-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="8e911-188">Als we toosplit deze tabel probeert, verschijnt er een fout:</span><span class="sxs-lookup"><span data-stu-id="8e911-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8e911-189">Bericht 35346, 15 niveau 1 staat, regel 44 GESPLITST component van de instructie ALTER PARTITION is mislukt omdat het Hallo-partitie is niet leeg.</span><span class="sxs-lookup"><span data-stu-id="8e911-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="8e911-190">Alleen lege partities kunnen worden gesplitst wanneer een columnstore-index op Hallo tabel bestaat.</span><span class="sxs-lookup"><span data-stu-id="8e911-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="8e911-191">Houd rekening met het uitschakelen van de columnstore-index Hallo voordat u de instructie ALTER PARTITION Hallo geeft en bouw vervolgens de columnstore-index Hallo nadat ALTER PARTITION voltooid is.</span><span class="sxs-lookup"><span data-stu-id="8e911-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="8e911-192">We kunnen echter gebruiken `CTAS` toocreate een nieuwe tabel toohold onze gegevens.</span><span class="sxs-lookup"><span data-stu-id="8e911-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="8e911-193">Een switch is toegestaan als Hallo partitiegrenzen worden uitgelijnd.</span><span class="sxs-lookup"><span data-stu-id="8e911-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="8e911-194">Dit betekent dat de brontabel Hallo met een lege partitie die we later kunt verdelen.</span><span class="sxs-lookup"><span data-stu-id="8e911-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8e911-195">Het enige dat blijft toodo tooalign nieuwe partitie grenzen met onze gegevens toohello is `CTAS` en onze gegevens terug in de hoofdtabel toohello-switch</span><span class="sxs-lookup"><span data-stu-id="8e911-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="8e911-196">Als u klaar bent Hallo verkeer van Hallo gegevens is een goed idee toorefresh Hallo statistieken op Hallo doel tabel tooensure ze nauwkeurig Hallo nieuwe verdeling van gegevens in hun respectieve partities Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="8e911-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="8e911-197">Tabel broncodebeheer partitioneren</span><span class="sxs-lookup"><span data-stu-id="8e911-197">Table partitioning source control</span></span>
<span data-ttu-id="8e911-198">tooavoid de tabeldefinitie van de van **roesten** in uw bronbeheersysteem kunt u tooconsider Hallo benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e911-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="8e911-199">Hallo-tabel maken als een gepartitioneerde tabel, maar geen waarden partitie</span><span class="sxs-lookup"><span data-stu-id="8e911-199">Create hello table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="8e911-200">`SPLIT`Hallo tabel als onderdeel van het implementatieproces Hallo:</span><span class="sxs-lookup"><span data-stu-id="8e911-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="8e911-201">Met deze benadering Hallo code in broncodebeheer statische blijft en Hallo partitionering waarden zijn toegestaan toobe dynamische; ontwikkeling met Hallo warehouse gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="8e911-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e911-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e911-202">Next steps</span></span>
<span data-ttu-id="8e911-203">toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [tabelstatistieken onderhouden] [ Statistics] en [ Tijdelijke tabellen][Temporary].</span><span class="sxs-lookup"><span data-stu-id="8e911-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="8e911-204">Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="8e911-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
