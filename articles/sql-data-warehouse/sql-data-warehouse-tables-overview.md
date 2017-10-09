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
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Overzicht van tabellen in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Gegevenstypen][Data Types]
> * [Distribueren][Distribute]
> * [Index][Index]
> * [Partitie][Partition]
> * [Statistieken][Statistics]
> * [Tijdelijke][Temporary]
> 
> 

Aan de slag met het maken van tabellen in SQL Data Warehouse is eenvoudig.  Hallo basic [CREATE TABLE] [ CREATE TABLE] syntaxis volgt de algemene syntaxis Hallo hoogstwaarschijnlijk al bekend bent met werken met andere databases.  een tabel toocreate, hoeft u alleen tooname uw tabel naam van de kolommen en gegevenstypen voor elke kolom definiëren.  Als u hebt de tabellen in andere databases maakt, moet dit bekend tooyou eruitzien.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Hallo bovenstaande voorbeeld maakt een tabel met de naam klanten met twee kolommen, voornaam en achternaam.  Elke kolom is gedefinieerd met het gegevenstype van VARCHAR(25) Hiermee beperkt u Hallo gegevens too25 tekens.  Deze fundamentele kenmerken van een tabel, evenals andere, zijn voornamelijk Hallo hetzelfde als andere databases.  Gegevenstypen zijn gedefinieerd voor elke kolom en Hallo integriteit garanderen van uw gegevens.  Indexen kunnen tooimprove prestaties doordat i/o's worden toegevoegd.  Partities kan worden toegevoegd tooimprove prestaties wanneer u gegevens toomodify nodig.

[Naam van] [ RENAME] een tabel met SQL Data Warehouse uitziet:

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Gedistribueerde tabellen
Een nieuw fundamentele kenmerk geïntroduceerd door gedistribueerde systemen SQL Data Warehouse is Hallo **distributie kolom**.  Hallo distributie kolom is te veel wat het klinkt als.  Hallo-kolom waarmee wordt bepaald hoe toodistribute, of delen, uw gegevens achter de schermen Hallo.  Wanneer u een tabel maken zonder op te geven Hallo distributie kolom, tabel hello wordt automatisch gedistribueerd met behulp van **round-robin**.  Round-robin tabellen kunnen zijn voldoende in sommige scenario's, kan definiëren distributiekolommen aanzienlijk minder verplaatsing van gegevens tijdens de query's, waardoor de prestaties optimaliseren.  In situaties wanneer er een kleine hoeveelheid gegevens in een tabel, kiezen toocreate Hallo tabel met Hallo **repliceren** Distributietype gegevens tooeach rekenknooppunt kopieert en slaat de verplaatsing van gegevens tijdens het uitvoeren van een query. Zie [distribueren van een tabel] [ Distribute] toolearn meer over hoe u tooselect een distributie-kolom.

## <a name="indexing-and-partitioning-tables"></a>Indexeren en tabellen te partitioneren
Als u bij het gebruik van SQL Data Warehouse worden geavanceerde en toooptimize prestaties, moet u meer informatie over tabelontwerp toolearn.  toolearn Zie meer Hallo artikelen op [tabel gegevenstypen][Data Types], [distribueren van een tabel][Distribute], [indexeren van een tabel] [ Index] en [partitioneren van een tabel][Partition].

## <a name="table-statistics"></a>Tabelstatistieken
Statistieken zijn een zeer belangrijk toogetting Hallo optimale prestaties buiten uw SQL Data Warehouse.  Omdat SQL Data Warehouse nog niet automatisch maken en bijwerken van statistieken voor u, zoals u tooexpect in Azure SQL Database hebt bereikt, leest u het artikel op [statistieken] [ Statistics] is mogelijk een Hallo belangrijkste artikelen u tooensure lezen dat u de beste prestaties Hallo ophalen van uw query.

## <a name="temporary-tables"></a>Tijdelijke tabellen
Tijdelijke tabellen zijn tabellen die alleen bestaan voor Hallo duur van uw aanmelding en kunnen niet worden bekeken door andere gebruikers.  Tijdelijke tabellen een uitstekende manier tooprevent anderen worden vanuit de tijdelijke resultaten en Hallo nodig voor opschoning ook leiden tot minder.  Omdat de tijdelijke tabellen ook gebruikmaken van lokale opslag, bieden ze sneller voor bepaalde bewerkingen.  Zie Hallo [tijdelijke tabel] [ Temporary] artikelen voor meer informatie over tijdelijke tabellen.

## <a name="external-tables"></a>Externe tabellen
Externe tabellen, ook wel bekend als Polybase tabellen zijn tabellen die kunnen worden opgevraagd van SQL Data Warehouse, maar punt toodata externe uit SQL Data Warehouse.  Bijvoorbeeld, kunt u een externe tabel welke punten toofiles op Azure Blob Storage.  Voor meer informatie over hoe toocreate en de query een externe tabel zien [gegevens laden met Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Niet-ondersteunde tabelfuncties
SQL Data Warehouse bevat veel van dezelfde tabelfuncties die worden aangeboden door andere databases hello, maar er zijn bepaalde functies die nog niet ondersteund.  Hieronder volgt een lijst van een aantal Hallo tabelfuncties die nog niet ondersteund.

| Niet-ondersteunde functies |
| --- |
| Primaire sleutel, refererende sleutels, unieke- en controle [tabelbeperkingen][Table Constraints] |
| [Unieke indexen][Unique Indexes] |
| [Berekende kolommen][Computed Columns] |
| [Sparse kolommen][Sparse Columns] |
| [Gebruiker gedefinieerde typen][User-Defined Types] |
| [Reeks][Sequence] |
| [Triggers][Triggers] |
| [Geïndexeerde weergaven][Indexed Views] |
| [Synoniemen][Synonyms] |

## <a name="table-size-queries"></a>Tabel grootte query 's
Een eenvoudige manier tooidentify ruimte en rijen die worden gebruikt door een tabel in elk Hallo 60 distributies is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Echter kan met behulp van DBCC-opdrachten worden behoorlijk beperken.  Dynamische beheerweergaven (DMV's) kunt u toosee veel meer details, evenals hebt u veel meer controle over Hallo queryresultaten.  Start op het maken van deze weergave waarnaar wordt verwezen tooby worden veel van onze voorbeelden in deze en andere artikelen.

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

### <a name="table-space-summary"></a>Tabelruimte samenvatting
Deze query retourneert Hallo rijen en ruimte door tabel.  Het is een uitstekende query toosee welke tabellen zijn uw grootste tabellen en round-robin gerepliceerd of hash gedistribueerd.  U ziet voor gedistribueerde hash-tabellen ook Hallo distributie kolom.  In de meeste gevallen moet de grootste tabellen hash gedistribueerd met een geclusterde columnstore-index.

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

### <a name="table-space-by-distribution-type"></a>Tabelruimte door Distributietype
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

### <a name="table-space-by-index-type"></a>Tabelruimte door indextype
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

### <a name="distribution-space-summary"></a>Distributie ruimte samenvatting
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

## <a name="next-steps"></a>Volgende stappen
toolearn Zie meer Hallo artikelen op [tabel gegevenstypen][Data Types], [distribueren van een tabel][Distribute], [indexeren van een tabel] [ Index], [Partitioneren van een tabel][Partition], [tabelstatistieken onderhouden] [ Statistics] en [ Tijdelijke tabellen][Temporary].  Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
