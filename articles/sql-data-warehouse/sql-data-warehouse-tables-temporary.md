---
title: aaaTemporary tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met tijdelijke tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a>Tijdelijke tabellen in SQL Data Warehouse
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

Tijdelijke tabellen zijn zeer nuttig bij het verwerken van gegevens - met name tijdens transformatie waar Hallo tussenliggende resultaten tijdelijke zijn. In SQL Data Warehouse bestaan tijdelijke tabellen op Hallo sessie niveau.  Ze zijn alleen zichtbaar toohello tijdens de sessie waarin ze zijn gemaakt en worden automatisch verwijderd wanneer die sessie zich afmeldt.  Tijdelijke tabellen bieden een prestatievoordelen omdat hun resultaten toolocal in plaats van externe opslag zijn geschreven.  Tijdelijke tabellen zijn enigszins afwijken in Azure SQL Data Warehouse Azure SQL Database, omdat ze toegankelijk zijn vanuit een willekeurige plaats in het Hallo-sessie, inclusief zowel binnen als buiten een opgeslagen procedure.

In dit artikel bevat essentiële instructies voor het gebruik van tijdelijke tabellen en markeert Hallo principes van de sessie niveau tijdelijke tabellen. Met behulp van Hallo-informatie in dit artikel kunt u modularize uw code, zowel hergebruik en het gemak van onderhoud van uw code te verbeteren.

## <a name="create-a-temporary-table"></a>Maak een tijdelijke tabel
Tijdelijke tabellen zijn gemaakt door Mining gewoon de tabelnaam van uw met een `#`.  Bijvoorbeeld:

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

Tijdelijke tabellen kunnen ook worden gemaakt met een `CTAS` precies dezelfde manier met behulp van Hallo:

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> `CTAS`is een zeer krachtige opdracht en is toegevoegd Hallo voordeel van zeer efficiënte tijdens het gebruik van ruimte voor transactielogboeken. 
> 
> 

## <a name="dropping-temporary-tables"></a>Tijdelijke tabellen verwijderen
Wanneer een nieuwe sessie wordt gemaakt, moeten er zijn geen tijdelijke tabellen bestaan.  Echter, als u aanroept Hallo dezelfde opgeslagen procedure, die wordt gemaakt een tijdelijke Hello dezelfde naam, tooensure die uw `CREATE TABLE` -instructies zijn geslaagd een eenvoudige vooraf bestaan uit met een `DROP` kan worden gebruikt zoals in Hallo onderstaand voorbeeld:

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Voor het coderen van de consistentiecontrole is een goede oefenen toouse dit patroon voor tabellen en tijdelijke tabellen.  Het is ook een goed idee toouse `DROP TABLE` tooremove tijdelijke tabellen wanneer u klaar bent met hen in uw code.  In de ontwikkeling van de opgeslagen procedure is het gebruikelijk toosee Hallo opdrachten drop samen gebundeld aan Hallo einde van een procedure tooensure dat deze objecten worden opgeschoond.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularizing code
Omdat de tijdelijke tabellen ziet u een willekeurige plaats in een gebruikerssessie, kan dit worden misbruikte toohelp modularize van uw toepassingscode.  Bijvoorbeeld: hello opgeslagen procedure die hieronder samenbrengt Hallo aanbevolen procedures voor boven het toogenerate DDL die alle statistische gegevens in Hallo-database wordt bijgewerkt door de naam van statistieken.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

In deze fase is de enige actie die Hallo dat is opgetreden Hallo maken van een opgeslagen procedure die wordt gegenereerd gewoon een tijdelijke tabel #stats_ddl, met de DDL-instructies.  Deze opgeslagen procedure wordt #stats_ddl verwijderen als er tooensure de query niet mislukt als meer dan één keer worden uitgevoerd in een sessie al bestaat.  Echter, omdat er geen `DROP TABLE` aan het einde van de Hallo van Hallo opgeslagen procedure, wanneer hello opgeslagen procedure is voltooid, het verlaat tabel Hallo gemaakt zodat deze buiten Hallo opgeslagen procedure kan worden gelezen.  In SQL Data Warehouse is in tegenstelling tot andere SQL Server-databases, het mogelijk toouse Hallo tijdelijke tabel buiten Hallo procedure waarvan deze is gemaakt.  SQL Data Warehouse tijdelijke tabellen kunnen worden gebruikt **overal** binnen Hallo-sessie. Dit kan leiden toomore modulaire en beheerbare code zoals in Hallo onderstaand voorbeeld:

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a>Beperkingen van de tijdelijke tabel
SQL Data Warehouse een aantal beperkingen opleggen bij het implementeren van tijdelijke tabellen.  Op dit moment alleen tijdens de sessie bereik tijdelijke tabellen worden ondersteund.  Globale tijdelijke tabellen worden niet ondersteund.  Bovendien kunnen niet weergaven worden gemaakt op tijdelijke tabellen.

## <a name="next-steps"></a>Volgende stappen
toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel] [ Partition] en [ Het onderhouden van de tabelstatistieken][Statistics].  Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].

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

<!--MSDN references-->

<!--Other Web references-->
