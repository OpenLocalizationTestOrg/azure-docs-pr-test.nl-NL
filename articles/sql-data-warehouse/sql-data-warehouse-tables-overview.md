---
title: aaaOverview van tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met Azure SQL Data Warehouse-tabellen.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="37288-103">Overzicht van tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="37288-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="37288-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="37288-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="37288-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="37288-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="37288-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="37288-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="37288-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="37288-107">[Index][Index]</span></span>
> * <span data-ttu-id="37288-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="37288-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="37288-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="37288-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="37288-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="37288-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="37288-111">Aan de slag met het maken van tabellen in SQL Data Warehouse is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="37288-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="37288-112">Hallo basic [CREATE TABLE] [ CREATE TABLE] syntaxis volgt de algemene syntaxis Hallo hoogstwaarschijnlijk al bekend bent met werken met andere databases.</span><span class="sxs-lookup"><span data-stu-id="37288-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="37288-113">een tabel toocreate, hoeft u alleen tooname uw tabel naam van de kolommen en gegevenstypen voor elke kolom definiëren.</span><span class="sxs-lookup"><span data-stu-id="37288-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="37288-114">Als u hebt de tabellen in andere databases maakt, moet dit bekend tooyou eruitzien.</span><span class="sxs-lookup"><span data-stu-id="37288-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="37288-115">Hallo bovenstaande voorbeeld maakt een tabel met de naam klanten met twee kolommen, voornaam en achternaam.</span><span class="sxs-lookup"><span data-stu-id="37288-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="37288-116">Elke kolom is gedefinieerd met het gegevenstype van VARCHAR(25) Hiermee beperkt u Hallo gegevens too25 tekens.</span><span class="sxs-lookup"><span data-stu-id="37288-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="37288-117">Deze fundamentele kenmerken van een tabel, evenals andere, zijn voornamelijk Hallo hetzelfde als andere databases.</span><span class="sxs-lookup"><span data-stu-id="37288-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="37288-118">Gegevenstypen zijn gedefinieerd voor elke kolom en Hallo integriteit garanderen van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="37288-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="37288-119">Indexen kunnen tooimprove prestaties doordat i/o's worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="37288-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="37288-120">Partities kan worden toegevoegd tooimprove prestaties wanneer u gegevens toomodify nodig.</span><span class="sxs-lookup"><span data-stu-id="37288-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="37288-121">[Naam van] [ RENAME] een tabel met SQL Data Warehouse uitziet:</span><span class="sxs-lookup"><span data-stu-id="37288-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="37288-122">Gedistribueerde tabellen</span><span class="sxs-lookup"><span data-stu-id="37288-122">Distributed tables</span></span>
<span data-ttu-id="37288-123">Een nieuw fundamentele kenmerk geïntroduceerd door gedistribueerde systemen SQL Data Warehouse is Hallo **distributie kolom**.</span><span class="sxs-lookup"><span data-stu-id="37288-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="37288-124">Hallo distributie kolom is te veel wat het klinkt als.</span><span class="sxs-lookup"><span data-stu-id="37288-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="37288-125">Hallo-kolom waarmee wordt bepaald hoe toodistribute, of delen, uw gegevens achter de schermen Hallo.</span><span class="sxs-lookup"><span data-stu-id="37288-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="37288-126">Wanneer u een tabel maken zonder op te geven Hallo distributie kolom, tabel hello wordt automatisch gedistribueerd met behulp van **round-robin**.</span><span class="sxs-lookup"><span data-stu-id="37288-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="37288-127">Round-robin tabellen kunnen zijn voldoende in sommige scenario's, kan definiëren distributiekolommen aanzienlijk minder verplaatsing van gegevens tijdens de query's, waardoor de prestaties optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="37288-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="37288-128">In situaties wanneer er een kleine hoeveelheid gegevens in een tabel, kiezen toocreate Hallo tabel met Hallo **repliceren** Distributietype gegevens tooeach rekenknooppunt kopieert en slaat de verplaatsing van gegevens tijdens het uitvoeren van een query.</span><span class="sxs-lookup"><span data-stu-id="37288-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="37288-129">Zie [distribueren van een tabel] [ Distribute] toolearn meer over hoe u tooselect een distributie-kolom.</span><span class="sxs-lookup"><span data-stu-id="37288-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="37288-130">Indexeren en tabellen te partitioneren</span><span class="sxs-lookup"><span data-stu-id="37288-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="37288-131">Als u bij het gebruik van SQL Data Warehouse worden geavanceerde en toooptimize prestaties, moet u meer informatie over tabelontwerp toolearn.</span><span class="sxs-lookup"><span data-stu-id="37288-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="37288-132">toolearn Zie meer Hallo artikelen op [tabel gegevenstypen][Data Types], [distribueren van een tabel][Distribute], [indexeren van een tabel] [ Index] en [partitioneren van een tabel][Partition].</span><span class="sxs-lookup"><span data-stu-id="37288-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="37288-133">Tabelstatistieken</span><span class="sxs-lookup"><span data-stu-id="37288-133">Table statistics</span></span>
<span data-ttu-id="37288-134">Statistieken zijn een zeer belangrijk toogetting Hallo optimale prestaties buiten uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="37288-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="37288-135">Omdat SQL Data Warehouse nog niet automatisch maken en bijwerken van statistieken voor u, zoals u tooexpect in Azure SQL Database hebt bereikt, leest u het artikel op [statistieken] [ Statistics] is mogelijk een Hallo belangrijkste artikelen u tooensure lezen dat u de beste prestaties Hallo ophalen van uw query.</span><span class="sxs-lookup"><span data-stu-id="37288-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="37288-136">Tijdelijke tabellen</span><span class="sxs-lookup"><span data-stu-id="37288-136">Temporary tables</span></span>
<span data-ttu-id="37288-137">Tijdelijke tabellen zijn tabellen die alleen bestaan voor Hallo duur van uw aanmelding en kunnen niet worden bekeken door andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="37288-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="37288-138">Tijdelijke tabellen een uitstekende manier tooprevent anderen worden vanuit de tijdelijke resultaten en Hallo nodig voor opschoning ook leiden tot minder.</span><span class="sxs-lookup"><span data-stu-id="37288-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="37288-139">Omdat de tijdelijke tabellen ook gebruikmaken van lokale opslag, bieden ze sneller voor bepaalde bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="37288-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="37288-140">Zie Hallo [tijdelijke tabel] [ Temporary] artikelen voor meer informatie over tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="37288-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="37288-141">Externe tabellen</span><span class="sxs-lookup"><span data-stu-id="37288-141">External tables</span></span>
<span data-ttu-id="37288-142">Externe tabellen, ook wel bekend als Polybase tabellen zijn tabellen die kunnen worden opgevraagd van SQL Data Warehouse, maar punt toodata externe uit SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="37288-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="37288-143">Bijvoorbeeld, kunt u een externe tabel welke punten toofiles op Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="37288-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="37288-144">Voor meer informatie over hoe toocreate en de query een externe tabel zien [gegevens laden met Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="37288-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="37288-145">Niet-ondersteunde tabelfuncties</span><span class="sxs-lookup"><span data-stu-id="37288-145">Unsupported table features</span></span>
<span data-ttu-id="37288-146">SQL Data Warehouse bevat veel van dezelfde tabelfuncties die worden aangeboden door andere databases hello, maar er zijn bepaalde functies die nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="37288-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="37288-147">Hieronder volgt een lijst van een aantal Hallo tabelfuncties die nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="37288-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="37288-148">Niet-ondersteunde functies</span><span class="sxs-lookup"><span data-stu-id="37288-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="37288-149">Primaire sleutel, refererende sleutels, unieke- en controle [tabelbeperkingen][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="37288-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="37288-150">[Unieke indexen][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="37288-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="37288-151">[Berekende kolommen][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="37288-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="37288-152">[Sparse kolommen][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="37288-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="37288-153">[Gebruiker gedefinieerde typen][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="37288-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="37288-154">[Reeks][Sequence]</span><span class="sxs-lookup"><span data-stu-id="37288-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="37288-155">[Triggers][Triggers]</span><span class="sxs-lookup"><span data-stu-id="37288-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="37288-156">[Geïndexeerde weergaven][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="37288-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="37288-157">[Synoniemen][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="37288-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="37288-158">Tabel grootte query 's</span><span class="sxs-lookup"><span data-stu-id="37288-158">Table size queries</span></span>
<span data-ttu-id="37288-159">Een eenvoudige manier tooidentify ruimte en rijen die worden gebruikt door een tabel in elk Hallo 60 distributies is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="37288-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="37288-160">Echter kan met behulp van DBCC-opdrachten worden behoorlijk beperken.</span><span class="sxs-lookup"><span data-stu-id="37288-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="37288-161">Dynamische beheerweergaven (DMV's) kunt u toosee veel meer details, evenals hebt u veel meer controle over Hallo queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="37288-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="37288-162">Start op het maken van deze weergave waarnaar wordt verwezen tooby worden veel van onze voorbeelden in deze en andere artikelen.</span><span class="sxs-lookup"><span data-stu-id="37288-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="37288-163">Tabelruimte samenvatting</span><span class="sxs-lookup"><span data-stu-id="37288-163">Table space summary</span></span>
<span data-ttu-id="37288-164">Deze query retourneert Hallo rijen en ruimte door tabel.</span><span class="sxs-lookup"><span data-stu-id="37288-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="37288-165">Het is een uitstekende query toosee welke tabellen zijn uw grootste tabellen en round-robin gerepliceerd of hash gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="37288-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="37288-166">U ziet voor gedistribueerde hash-tabellen ook Hallo distributie kolom.</span><span class="sxs-lookup"><span data-stu-id="37288-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="37288-167">In de meeste gevallen moet de grootste tabellen hash gedistribueerd met een geclusterde columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="37288-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="37288-168">Tabelruimte door Distributietype</span><span class="sxs-lookup"><span data-stu-id="37288-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="37288-169">Tabelruimte door indextype</span><span class="sxs-lookup"><span data-stu-id="37288-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="37288-170">Distributie ruimte samenvatting</span><span class="sxs-lookup"><span data-stu-id="37288-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="37288-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37288-171">Next steps</span></span>
<span data-ttu-id="37288-172">toolearn Zie meer Hallo artikelen op [tabel gegevenstypen][Data Types], [distribueren van een tabel][Distribute], [indexeren van een tabel] [ Index], [Partitioneren van een tabel][Partition], [tabelstatistieken onderhouden] [ Statistics] en [ Tijdelijke tabellen][Temporary].</span><span class="sxs-lookup"><span data-stu-id="37288-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="37288-173">Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="37288-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
