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
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="2f81f-103">Tijdelijke tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2f81f-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2f81f-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="2f81f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="2f81f-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="2f81f-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="2f81f-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="2f81f-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="2f81f-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="2f81f-107">[Index][Index]</span></span>
> * <span data-ttu-id="2f81f-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="2f81f-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="2f81f-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="2f81f-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="2f81f-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="2f81f-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="2f81f-111">Tijdelijke tabellen zijn zeer nuttig bij het verwerken van gegevens - met name tijdens transformatie waar Hallo tussenliggende resultaten tijdelijke zijn.</span><span class="sxs-lookup"><span data-stu-id="2f81f-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="2f81f-112">In SQL Data Warehouse bestaan tijdelijke tabellen op Hallo sessie niveau.</span><span class="sxs-lookup"><span data-stu-id="2f81f-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="2f81f-113">Ze zijn alleen zichtbaar toohello tijdens de sessie waarin ze zijn gemaakt en worden automatisch verwijderd wanneer die sessie zich afmeldt.</span><span class="sxs-lookup"><span data-stu-id="2f81f-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="2f81f-114">Tijdelijke tabellen bieden een prestatievoordelen omdat hun resultaten toolocal in plaats van externe opslag zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="2f81f-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="2f81f-115">Tijdelijke tabellen zijn enigszins afwijken in Azure SQL Data Warehouse Azure SQL Database, omdat ze toegankelijk zijn vanuit een willekeurige plaats in het Hallo-sessie, inclusief zowel binnen als buiten een opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="2f81f-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="2f81f-116">In dit artikel bevat essentiële instructies voor het gebruik van tijdelijke tabellen en markeert Hallo principes van de sessie niveau tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="2f81f-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="2f81f-117">Met behulp van Hallo-informatie in dit artikel kunt u modularize uw code, zowel hergebruik en het gemak van onderhoud van uw code te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="2f81f-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="2f81f-118">Maak een tijdelijke tabel</span><span class="sxs-lookup"><span data-stu-id="2f81f-118">Create a temporary table</span></span>
<span data-ttu-id="2f81f-119">Tijdelijke tabellen zijn gemaakt door Mining gewoon de tabelnaam van uw met een `#`.</span><span class="sxs-lookup"><span data-stu-id="2f81f-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="2f81f-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f81f-120">For example:</span></span>

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

<span data-ttu-id="2f81f-121">Tijdelijke tabellen kunnen ook worden gemaakt met een `CTAS` precies dezelfde manier met behulp van Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f81f-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="2f81f-122">`CTAS`is een zeer krachtige opdracht en is toegevoegd Hallo voordeel van zeer efficiënte tijdens het gebruik van ruimte voor transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="2f81f-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="2f81f-123">Tijdelijke tabellen verwijderen</span><span class="sxs-lookup"><span data-stu-id="2f81f-123">Dropping temporary tables</span></span>
<span data-ttu-id="2f81f-124">Wanneer een nieuwe sessie wordt gemaakt, moeten er zijn geen tijdelijke tabellen bestaan.</span><span class="sxs-lookup"><span data-stu-id="2f81f-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="2f81f-125">Echter, als u aanroept Hallo dezelfde opgeslagen procedure, die wordt gemaakt een tijdelijke Hello dezelfde naam, tooensure die uw `CREATE TABLE` -instructies zijn geslaagd een eenvoudige vooraf bestaan uit met een `DROP` kan worden gebruikt zoals in Hallo onderstaand voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f81f-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="2f81f-126">Voor het coderen van de consistentiecontrole is een goede oefenen toouse dit patroon voor tabellen en tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="2f81f-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="2f81f-127">Het is ook een goed idee toouse `DROP TABLE` tooremove tijdelijke tabellen wanneer u klaar bent met hen in uw code.</span><span class="sxs-lookup"><span data-stu-id="2f81f-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="2f81f-128">In de ontwikkeling van de opgeslagen procedure is het gebruikelijk toosee Hallo opdrachten drop samen gebundeld aan Hallo einde van een procedure tooensure dat deze objecten worden opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="2f81f-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="2f81f-129">Modularizing code</span><span class="sxs-lookup"><span data-stu-id="2f81f-129">Modularizing code</span></span>
<span data-ttu-id="2f81f-130">Omdat de tijdelijke tabellen ziet u een willekeurige plaats in een gebruikerssessie, kan dit worden misbruikte toohelp modularize van uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="2f81f-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="2f81f-131">Bijvoorbeeld: hello opgeslagen procedure die hieronder samenbrengt Hallo aanbevolen procedures voor boven het toogenerate DDL die alle statistische gegevens in Hallo-database wordt bijgewerkt door de naam van statistieken.</span><span class="sxs-lookup"><span data-stu-id="2f81f-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="2f81f-132">In deze fase is de enige actie die Hallo dat is opgetreden Hallo maken van een opgeslagen procedure die wordt gegenereerd gewoon een tijdelijke tabel #stats_ddl, met de DDL-instructies.</span><span class="sxs-lookup"><span data-stu-id="2f81f-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="2f81f-133">Deze opgeslagen procedure wordt #stats_ddl verwijderen als er tooensure de query niet mislukt als meer dan één keer worden uitgevoerd in een sessie al bestaat.</span><span class="sxs-lookup"><span data-stu-id="2f81f-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="2f81f-134">Echter, omdat er geen `DROP TABLE` aan het einde van de Hallo van Hallo opgeslagen procedure, wanneer hello opgeslagen procedure is voltooid, het verlaat tabel Hallo gemaakt zodat deze buiten Hallo opgeslagen procedure kan worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="2f81f-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="2f81f-135">In SQL Data Warehouse is in tegenstelling tot andere SQL Server-databases, het mogelijk toouse Hallo tijdelijke tabel buiten Hallo procedure waarvan deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f81f-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="2f81f-136">SQL Data Warehouse tijdelijke tabellen kunnen worden gebruikt **overal** binnen Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="2f81f-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="2f81f-137">Dit kan leiden toomore modulaire en beheerbare code zoals in Hallo onderstaand voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f81f-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="2f81f-138">Beperkingen van de tijdelijke tabel</span><span class="sxs-lookup"><span data-stu-id="2f81f-138">Temporary table limitations</span></span>
<span data-ttu-id="2f81f-139">SQL Data Warehouse een aantal beperkingen opleggen bij het implementeren van tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="2f81f-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="2f81f-140">Op dit moment alleen tijdens de sessie bereik tijdelijke tabellen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2f81f-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="2f81f-141">Globale tijdelijke tabellen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2f81f-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="2f81f-142">Bovendien kunnen niet weergaven worden gemaakt op tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="2f81f-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f81f-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f81f-143">Next steps</span></span>
<span data-ttu-id="2f81f-144">toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel] [ Partition] en [ Het onderhouden van de tabelstatistieken][Statistics].</span><span class="sxs-lookup"><span data-stu-id="2f81f-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="2f81f-145">Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2f81f-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
