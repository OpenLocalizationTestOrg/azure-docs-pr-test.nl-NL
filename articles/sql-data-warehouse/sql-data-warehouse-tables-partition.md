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
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Tabellen in SQL Data Warehouse partitioneren
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

Partitioneren wordt ondersteund op alle SQL Data Warehouse tabeltypen; inclusief geclusterde columnstore geclusterde index en heap.  Partitioneren wordt ook ondersteund voor alle typen distributiepunten, inclusief zowel hash of round-robin gedistribueerd.  Partitioneren, kunt u uw gegevens in kleinere groepen van gegevens en in de meeste gevallen partitioneren is uitgevoerd op een datumkolom toodivide.

## <a name="benefits-of-partitioning"></a>Voordelen van het partitioneren
Partitioneren, profiteert gegevens onderhoud en query-prestaties.  Hiermee wordt aangegeven of deze voordelen biedt voor beide of slechts één is afhankelijk van hoe gegevens worden geladen en of hello dezelfde kolom kan worden gebruikt voor beide doeleinden, omdat het partitioneren kan alleen worden uitgevoerd op één kolom.

### <a name="benefits-tooloads"></a>Voordelen tooloads
Hallo belangrijkste voordeel van het partitioneren in SQL datawarehouse is verbeteren Hallo efficiëntie en prestaties van het laden van gegevens via het gebruik van de partitie verwijderen, overschakelen en samenvoegen.  Kolom die nauw gekoppeld in de meeste gevallen gegevens op een datum is gepartitioneerd toohello volgorde welke Hallo-gegevens geladen toohello database zijn.  Een van de grootste voordelen van het gebruik van partities toomaintain gegevens het vermijden van transactielogboeken Hallo Hallo.  Gewoon invoegen, bijwerken of verwijderen van gegevens kan de eenvoudigste manier Hallo met een beetje gedachte en moeite, zijn met behulp van partities tijdens het laadproces aanzienlijk prestaties kan verbeteren.

Overschakelen van de partitie kan gebruikte tooquickly verwijderen of een gedeelte van een tabel te vervangen.  Bijvoorbeeld, een verkoop feitentabel bevat mogelijk alleen gegevens voor Hallo afgelopen 36 maanden.  Aan het einde van de Hallo van elke maand, wordt hello oudste maand verkoopgegevens verwijderd uit Hallo tabel.  Deze gegevens kan worden verwijderd met behulp van een delete-instructie toodelete Hallo-gegevens voor Hallo oudste maand.  Echter kan verwijderen van een grote hoeveelheid gegevens per rij met een delete-instructie erg lang duren, evenals Hallo risico van grote transacties die een toorollback lang duren kan als er iets mis gaat maken.  Een meer optimale aanpak is toosimply neerzetten Hallo oudste partitie van gegevens.  Waar verwijderen van afzonderlijke rijen Hallo kan uren duren, kan verwijderen van een volledige partitie seconden duren.

### <a name="benefits-tooqueries"></a>Voordelen tooqueries
Gebruikte tooimprove queryprestaties kan ook worden veroorzaakt partitioneren.  Als een query wordt een filter op een gepartitioneerde kolom toegepast, kan dit Hallo scan tooonly Hallo in aanmerking komende partities die mogelijk een veel kleinere subset uit Hallo gegevens, waardoor het voorkomen van een volledige tabelscan beperken.  Met Hallo introductie van geclusterde kolomopslagindexen, Hallo predikaat eliminatie prestatievoordelen minder nuttige, maar in sommige gevallen kan er een voordeel tooqueries.  Bijvoorbeeld, als Hallo verkoop feitentabel in 36 maanden met behulp van de verkoop datumveld Hallo is gepartitioneerd, kunnen vervolgens query's die op Hallo Verkoopdatum filteren overslaan zoeken in partities die niet overeenkomen met de Hallo filter.

## <a name="partition-sizing-guidance"></a>Richtlijn voor partitie
Bij het partitioneren van prestaties van de gebruikte tooimprove sommige scenario's voor het maken van een tabel met kan worden **te veel** partities prestaties in bepaalde omstandigheden kunnen schaden.  Deze problemen zijn vooral voor geclusterde columnstore-tabellen.  Voor het partitioneren toobe handig zijn, is het belangrijk toounderstand wanneer toouse partitionerings- en Hallo aantal partities toocreate.  Er is geen vaste snelle regel als toohow veel partities zijn te veel, dit is afhankelijk van uw gegevens en het aantal partities u toosimultaneously laadt.  Maar als een algemene vuistregel Denk toe te voegen per 10 too100s met partities, niet 1000s.

Bij het maken van partities op **geclusterde columnstore** tabellen, het is belangrijk tooconsider komt dan uit hoeveel rijen in elke partitie.  Voor optimale compressie en prestaties van de geclusterde columnstore-tabellen, is een minimum van 1 miljoen rijen per partitie distributie en het nodig.  Voordat partities worden gemaakt, wordt elke tabel al verdeeld met SQL Data Warehouse in 60 gedistribueerde databases.  Elke partitionering toegevoegde tooa-tabel is bovendien toohello distributies achter de schermen Hallo gemaakt.  In dit voorbeeld gebruiken als Hallo verkoop feitentabel 36 maandelijkse partities bevat, en het gezien het feit dat SQL Data Warehouse 60 distributies is vervolgens Hallo verkoop feit tabel 60 miljoen rijen per maand of 2.1 miljard rijen moet bevatten wanneer alle maanden worden ingevuld.  Als een tabel aanzienlijk minder rijen dan Hallo minimum aantal rijen per partitie aanbevolen bevat, kunt u overwegen minder partities in volgorde toomake toename Hallo aantal rijen per partitie.  Zie ook Hallo [indexering] [ Index] artikel waaronder query's die kunnen worden uitgevoerd op de SQL Data Warehouse tooassess Hallo kwaliteit van de cluster columnstore-indexen.

## <a name="syntax-difference-from-sql-server"></a>Syntaxis verschil van SQL Server
SQL Data Warehouse introduceert een vereenvoudigde definitie van de partities die enigszins van SQL Server verschilt.  Partitionering functies en schema's worden niet gebruikt in SQL Data Warehouse omdat ze zich in SQL Server.  In plaats daarvan toodo hoeft u gepartitioneerde punten voor kolom- en Hallo grens te identificeren.  Tijdens het Hallo-syntaxis van het partitioneren van mogelijk enigszins afwijken van de SQL Server, worden de basisconcepten Hallo Hallo dezelfde.  SQL Server en SQL Data Warehouse ondersteuning voor één partitiekolom per tabel, wat kan varieerde partitie.  toolearn meer informatie over partitioneren, Zie [gepartitioneerde tabellen en indexen][Partitioned Tables and Indexes].

Hallo onderstaand voorbeeld van een SQL Data Warehouse gepartitioneerd [CREATE TABLE] [ CREATE TABLE] -instructie partities Hallo heeft tabel op de Hallo OrderDateKey kolom:

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

## <a name="migrating-partitioning-from-sql-server"></a>Partitioneren van SQL-Server migreren
SQL Server toomigrate partitie definities tooSQL Data Warehouse gewoon:

* Hallo SQL Server elimineren [partitieschema][partition scheme].
* Hallo toevoegen [partitiefunctie] [ partition function] definitie tooyour tabel maken.

Als u een gepartitioneerde tabel van een SQL Server-exemplaar Hallo hieronder SQL migreert kunt u toointerrogate Hallo aantal rijen dat in elke partitie.  Houd er rekening mee dat als hello dezelfde partitionering granulariteit wordt gebruikt in SQL Data Warehouse, het aantal rijen per partitie Hallo met een factor van 60 neemt.  

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

## <a name="workload-management"></a>Werklastbeheer
Is een sluitstuk overweging toofactor in toohello tabel partitie besluit [werkbelasting management][workload management].  Beheer van de werkbelasting in SQL Data Warehouse is voornamelijk Hallo beheer van geheugen en een gelijktijdigheid van taken.  Maximaal geheugen toegewezen tooeach distributie tijdens de uitvoering van de query is in SQL Data Warehouse Hallo geregeld resource klassen.  De partities wordt in het ideale geval worden aangepast met het oog andere factoren zoals Hallo geheugenvereisten van het bouwen van de geclusterde columnstore-indexen.  Geclusterde columnstore-indexen voordeel aanzienlijk wanneer ze meer geheugen worden toegewezen.  Daarom wilt u tooensure die een index met partitie opnieuw maken is niet tekort komt geheugen. Uitbreiding Hallo en de hoeveelheid geheugen beschikbaar tooyour query kan worden bereikt door het overschakelen van standaardrol hello, smallrc, tooone van andere functies, zoals largerc Hallo.

Informatie over het Hallo-toewijzing van geheugen per distributie is beschikbaar door het uitvoeren van query's Hallo resource gouverneur dynamische beheerweergaven. In werkelijkheid wordt uw geheugentoekenning niet kleiner zijn dan Hallo onderstaande afbeeldingen. Dit biedt echter een niveau van de richtlijnen die u gebruiken kunt wanneer het formaat van partities voor gegevens beheerbewerkingen.  Probeer het formaat van uw partities groter dan Hallo geheugentoekenning geleverd door de extra grote resourceklasse hello tooavoid. Als uw partities afgezien van deze afbeelding groeien loopt u Hallo risico van geheugendruk wat op zijn beurt tooless optimale compressie leidt.

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

## <a name="partition-switching"></a>Partitie overschakelen
SQL Data Warehouse ondersteunt partitie splitsen en overschakelen samenvoegen. Elk van deze functies is excuted met Hallo [ALTER TABLE] [ ALTER TABLE] instructie.

tooswitch partities tussen twee tabellen, die u ervoor zorgen moet dat Hallo partities zijn uitgelijnd op hun respectieve grenzen en Hallo tabeldefinities overeen met. Als de check-beperkingen zijn niet beschikbaar tooenforce Hallo bereik van waarden in de brontabel van een tabel Hallo Hallo moet bevatten dezelfde partitie grenzen als Hallo doeltabel. Als dit niet Hallo geval mislukken Hallo partitie switch als Hallo partitiemetagegevens niet gesynchroniseerd.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Hoe toosplit een partitie die gegevens bevat
Hallo efficiëntste methode toosplit een partitie die al gegevens bevat is toouse een `CTAS` instructie. Als Hallo gepartitioneerde tabel een geclusterde columnstore moet vervolgens Hallo tabel partitie niet leeg zijn voordat deze kan worden gesplitst.

Hieronder volgt een voorbeeld-gepartitioneerde columnstore-tabel met één rij in elke partitie:

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
> Door Creating Hallo statistiek object, zorgen wij ervoor dat tabelmetagegevens nauwkeuriger zijn. Als we het maken van statistieken weglaat, wordt SQL Data Warehouse standaardwaarden gebruikt. Voor meer informatie over statistieken Controleer [statistieken][statistics].
> 
> 

We kunnen vervolgens zoeken naar aantal Hallo-rijen met Hallo `sys.partitions` catalogusweergave:

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

Als we toosplit deze tabel probeert, verschijnt er een fout:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Bericht 35346, 15 niveau 1 staat, regel 44 GESPLITST component van de instructie ALTER PARTITION is mislukt omdat het Hallo-partitie is niet leeg.  Alleen lege partities kunnen worden gesplitst wanneer een columnstore-index op Hallo tabel bestaat. Houd rekening met het uitschakelen van de columnstore-index Hallo voordat u de instructie ALTER PARTITION Hallo geeft en bouw vervolgens de columnstore-index Hallo nadat ALTER PARTITION voltooid is.

We kunnen echter gebruiken `CTAS` toocreate een nieuwe tabel toohold onze gegevens.

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

Een switch is toegestaan als Hallo partitiegrenzen worden uitgelijnd. Dit betekent dat de brontabel Hallo met een lege partitie die we later kunt verdelen.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Het enige dat blijft toodo tooalign nieuwe partitie grenzen met onze gegevens toohello is `CTAS` en onze gegevens terug in de hoofdtabel toohello-switch

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

Als u klaar bent Hallo verkeer van Hallo gegevens is een goed idee toorefresh Hallo statistieken op Hallo doel tabel tooensure ze nauwkeurig Hallo nieuwe verdeling van gegevens in hun respectieve partities Hallo weergeven:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Tabel broncodebeheer partitioneren
tooavoid de tabeldefinitie van de van **roesten** in uw bronbeheersysteem kunt u tooconsider Hallo benadering te volgen:

1. Hallo-tabel maken als een gepartitioneerde tabel, maar geen waarden partitie

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

1. `SPLIT`Hallo tabel als onderdeel van het implementatieproces Hallo:

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

Met deze benadering Hallo code in broncodebeheer statische blijft en Hallo partitionering waarden zijn toegestaan toobe dynamische; ontwikkeling met Hallo warehouse gedurende een bepaalde periode.

## <a name="next-steps"></a>Volgende stappen
toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [tabelstatistieken onderhouden] [ Statistics] en [ Tijdelijke tabellen][Temporary].  Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
