---
title: aaaCreate tabel selecteert (CTAS) in SQL Data Warehouse | Microsoft Docs
description: Tips voor het coderen van Hello maken tabel selecteert u de instructie (CTAS) in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="05838-103">Table As Select (CTAS) in SQL datawarehouse maken</span><span class="sxs-lookup"><span data-stu-id="05838-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="05838-104">Maken van de tabel als selecteren of `CTAS` is een van de Hallo belangrijkste T-SQL-functies die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="05838-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="05838-105">Het is een volledig parallelized bewerking die u een nieuwe tabel op basis van het Hallo-uitvoer van een SELECT-instructie maakt.</span><span class="sxs-lookup"><span data-stu-id="05838-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="05838-106">`CTAS`Hallo snelste en eenvoudigste manier toocreate is een kopie van een tabel.</span><span class="sxs-lookup"><span data-stu-id="05838-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="05838-107">Dit document bevat zowel voorbeelden en aanbevolen procedures voor `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="05838-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="05838-108">SELECTEREN... IN de vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="05838-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="05838-109">U kunt overwegen `CTAS` Super bedrag versie van `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="05838-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="05838-110">Hieronder volgt een voorbeeld van een eenvoudige `SELECT..INTO` instructie:</span><span class="sxs-lookup"><span data-stu-id="05838-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="05838-111">In bovenstaande Hallo voorbeeld `[dbo].[FactInternetSales_new]` zou worden gemaakt als ROUND_ROBIN gedistribueerde tabel met deze functie een door de GECLUSTERDE COLUMNSTORE-INDEX, omdat dit Hallo tabel standaardinstellingen in Azure SQL Data Warehouse zijn.</span><span class="sxs-lookup"><span data-stu-id="05838-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="05838-112">`SELECT..INTO`echter kunt u niet toochange typt u ofwel Hallo distributie methode of Hallo index als onderdeel van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="05838-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="05838-113">Dit is wanneer `CTAS` van pas komt.</span><span class="sxs-lookup"><span data-stu-id="05838-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="05838-114">tooconvert Hallo hierboven te`CTAS` is heel eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="05838-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="05838-115">Met `CTAS` u kunnen toochange zijn beide distributie van het Hallo-tabelgegevens, evenals een tabeltype Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="05838-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="05838-116">Als u alleen probeert toochange Hallo index in uw `CTAS` bewerking en Hallo brontabel is gedistribueerd-hash en vervolgens uw `CTAS` bewerking voert aanbevolen als u dezelfde kolom en gegevens Distributietype Hallo.</span><span class="sxs-lookup"><span data-stu-id="05838-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="05838-117">Dit voorkomt cross-distributie gegevensverplaatsing tijdens efficiënter is Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="05838-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="05838-118">Met behulp van CTAS toocopy een tabel</span><span class="sxs-lookup"><span data-stu-id="05838-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="05838-119">Mogelijk een van de meest voorkomende Hallo maakt gebruik van `CTAS` is een exemplaar maken van een tabel zodat u Hallo DDL kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="05838-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="05838-120">Als u bijvoorbeeld uw tabel als oorspronkelijk maakte `ROUND_ROBIN` en nu wilt wijzigen tooa tabel gedistribueerd op een kolom `CTAS` is hoe u Hallo distributie kolom wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="05838-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="05838-121">`CTAS`gebruikte toochange kan partitioneren, te indexeren of kolom typen ook worden.</span><span class="sxs-lookup"><span data-stu-id="05838-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="05838-122">Stel dat u deze tabel met Hallo standaardtype distributie van gemaakt `ROUND_ROBIN` gedistribueerd omdat er geen distributiepunt-kolom is opgegeven in Hallo `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="05838-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="05838-123">U kunt nu toocreate een nieuw exemplaar van deze tabel met een geclusterde Columnstore-Index zodat u van Hallo prestaties van de geclusterde Columnstore-tabellen profiteren kunt.</span><span class="sxs-lookup"><span data-stu-id="05838-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="05838-124">Wilt u ook toodistribute deze tabel op ProductKey omdat u zijn anticiperen op verbindingen in deze kolom en gegevensverplaatsing tooavoid tijdens joins op ProductKey wilt.</span><span class="sxs-lookup"><span data-stu-id="05838-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="05838-125">Tot slot wilt u ook tooadd partitioneren op OrderDateKey zodat u snel kunt u oude gegevens verwijderen door het verwijderen van oude partities.</span><span class="sxs-lookup"><span data-stu-id="05838-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="05838-126">Hier volgt Hallo CTAS instructie waarmee uw oude tabel in een nieuwe tabel wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="05838-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="05838-127">Ten slotte kunt u Wijzig de naam van uw tooswap tabellen in de nieuwe tabel en vervolgens uw oude tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="05838-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="05838-128">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="05838-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="05838-129">Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.</span><span class="sxs-lookup"><span data-stu-id="05838-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="05838-130">Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="05838-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="05838-131">Met behulp van CTAS toowork rond de niet-ondersteunde functies</span><span class="sxs-lookup"><span data-stu-id="05838-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="05838-132">`CTAS`gebruikte toowork rond een aantal onderstaande Hallo niet-ondersteunde functies kan ook worden veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="05838-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="05838-133">Dit kan vaak tonen dat toobe een situatie win/win niet alleen uw code compatibel worden, maar dit wordt vaak sneller uitgevoerd op de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="05838-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="05838-134">Dit is als gevolg van het ontwerp van de volledig parallelized.</span><span class="sxs-lookup"><span data-stu-id="05838-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="05838-135">Scenario's die kunnen worden uitgevoerd om met CTAS omvatten:</span><span class="sxs-lookup"><span data-stu-id="05838-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="05838-136">ANSI JOINS op UPDATEs</span><span class="sxs-lookup"><span data-stu-id="05838-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="05838-137">ANSI-verbindingen in verwijderen</span><span class="sxs-lookup"><span data-stu-id="05838-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="05838-138">MERGE-instructie</span><span class="sxs-lookup"><span data-stu-id="05838-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="05838-139">Probeer toothink ' CTAS eerste '.</span><span class="sxs-lookup"><span data-stu-id="05838-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="05838-140">Als u denkt dat u kunt ook een probleem met oplossen `CTAS` is dat doorgaans de beste manier tooapproach Hallo deze - zelfs als u meer gegevens als gevolg hiervan worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="05838-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="05838-141">ANSI join vervanging voor update-instructies</span><span class="sxs-lookup"><span data-stu-id="05838-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="05838-142">U merkt dat u hebt een complexe update waar lid van meer dan twee tabellen samen met ANSI-syntaxis tooperform Hallo toevoegen, bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="05838-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="05838-143">Stel dat u deze tabel tooupdate had:</span><span class="sxs-lookup"><span data-stu-id="05838-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="05838-144">de oorspronkelijke query Hallo kan hebt gezien ongeveer het volgende:</span><span class="sxs-lookup"><span data-stu-id="05838-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="05838-145">Omdat SQL Data Warehouse biedt geen ondersteuning voor ANSI joins in Hallo `FROM` -component van een `UPDATE` instructie, u kunt deze code via niet kopiëren zonder dat een enigszins gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="05838-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="05838-146">U kunt een combinatie van een `CTAS` en een impliciete tooreplace deze code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="05838-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="05838-147">ANSI join vervanging voor delete-instructies</span><span class="sxs-lookup"><span data-stu-id="05838-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="05838-148">Hallo aanbevolen benadering voor het verwijderen van gegevens is soms toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="05838-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="05838-149">Selecteer de gewenste tookeep Hallo-gegevens in plaats van een eenvoudig hello gegevens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="05838-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="05838-150">Deze vooral voor `DELETE` instructies die gebruikmaken van ansi-syntaxis koppelen omdat SQL Data Warehouse biedt geen ondersteuning voor ANSI joins in Hallo `FROM` -component van een `DELETE` instructie.</span><span class="sxs-lookup"><span data-stu-id="05838-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="05838-151">Hieronder vindt u een voorbeeld van een geconverteerde DELETE-instructie:</span><span class="sxs-lookup"><span data-stu-id="05838-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="05838-152">Vervang merge-instructies</span><span class="sxs-lookup"><span data-stu-id="05838-152">Replace merge statements</span></span>
<span data-ttu-id="05838-153">Merge-instructies kunnen worden vervangen, ten minste gedeeltelijk met behulp van `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="05838-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="05838-154">U kunt consolideren Hallo `INSERT` en Hallo `UPDATE` in één instructie.</span><span class="sxs-lookup"><span data-stu-id="05838-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="05838-155">Verwijderde records moet toobe in een tweede instructie afgesloten.</span><span class="sxs-lookup"><span data-stu-id="05838-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="05838-156">Een voorbeeld van een `UPSERT` hieronder:</span><span class="sxs-lookup"><span data-stu-id="05838-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="05838-157">CTAS aanbeveling: status expliciet gegevenstype en null-waarden van uitvoer</span><span class="sxs-lookup"><span data-stu-id="05838-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="05838-158">Bij het migreren van code is het wellicht tegenkomen van dit type codering patroon:</span><span class="sxs-lookup"><span data-stu-id="05838-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="05838-159">U kunt instinctief overwegen, moet u deze code tooa CTAS migreren en u niet juist.</span><span class="sxs-lookup"><span data-stu-id="05838-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="05838-160">Er is echter een verborgen probleem hier.</span><span class="sxs-lookup"><span data-stu-id="05838-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="05838-161">Hallo volgende code wordt niet resulteert Hallo hetzelfde resultaat:</span><span class="sxs-lookup"><span data-stu-id="05838-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="05838-162">U ziet dat Hallo kolom 'resultaat' doorsturen Hallo type en nullability gegevenswaarden van Hallo expressie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="05838-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="05838-163">Dit kan toosubtle afwijkingen leiden waarden in als u niet zorgvuldig.</span><span class="sxs-lookup"><span data-stu-id="05838-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="05838-164">Voer een van de volgende Hallo als een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="05838-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="05838-165">Hallo waarde die is opgeslagen voor resultaat verschilt.</span><span class="sxs-lookup"><span data-stu-id="05838-165">hello value stored for result is different.</span></span> <span data-ttu-id="05838-166">Hallo persistente waarde in Hallo resultatenkolom gebruikt in andere wordt expressies Hallo fout nog meer belangrijke.</span><span class="sxs-lookup"><span data-stu-id="05838-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="05838-167">Dit is vooral belangrijk voor migraties van gegevens.</span><span class="sxs-lookup"><span data-stu-id="05838-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="05838-168">Er is een probleem ondanks dat de tweede query Hallo weliswaar nauwkeuriger is.</span><span class="sxs-lookup"><span data-stu-id="05838-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="05838-169">Hallo gegevens zou verschillende vergeleken toohello bronsysteem en die tooquestions van integriteit leidt Hallo-migratie.</span><span class="sxs-lookup"><span data-stu-id="05838-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="05838-170">Dit is een van deze zeldzame gevallen waarbij 'verkeerde' Hallo-antwoord daadwerkelijk Hallo rechts een is!</span><span class="sxs-lookup"><span data-stu-id="05838-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="05838-171">Hallo reden zien we deze verschillen tussen de twee Hallo resultaten niet actief is tooimplicit casten typt.</span><span class="sxs-lookup"><span data-stu-id="05838-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="05838-172">Eerste voorbeeld Hallo tabel definieert in Hallo Hallo-kolomdefinitie.</span><span class="sxs-lookup"><span data-stu-id="05838-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="05838-173">Er treedt een impliciete conversie op Hallo rij wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="05838-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="05838-174">In het tweede voorbeeld Hallo is er geen impliciete typeconversie zoals Hallo expressie gegevenstype van kolom Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="05838-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="05838-175">U ziet dat ook dat Hallo-kolom in het tweede voorbeeld Hallo is gedefinieerd als een kolom waarvoor null is toegestaan dat in het eerste voorbeeld Hallo deze niet heeft.</span><span class="sxs-lookup"><span data-stu-id="05838-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="05838-176">Wanneer het Hallo-tabel is gemaakt met Hallo eerste voorbeeld kolom nullability is expliciet is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="05838-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="05838-177">In het tweede voorbeeld Hallo is het alleen toohello expressie linker- en standaard dit zou leiden tot een NULL-definitie.</span><span class="sxs-lookup"><span data-stu-id="05838-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="05838-178">tooresolve deze problemen die u moet expliciet Hallo typeconversie en null-waarden instellen in Hallo `SELECT` gedeelte Hallo `CTAS` instructie.</span><span class="sxs-lookup"><span data-stu-id="05838-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="05838-179">U kunt deze niet instellen eigenschappen in Hallo deel van de tabel maken.</span><span class="sxs-lookup"><span data-stu-id="05838-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="05838-180">Hallo in het volgende voorbeeld laat zien hoe toofix Hallo code:</span><span class="sxs-lookup"><span data-stu-id="05838-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="05838-181">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="05838-181">Note hello following:</span></span>

* <span data-ttu-id="05838-182">CAST of CONVERT kan zijn gebruikt</span><span class="sxs-lookup"><span data-stu-id="05838-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="05838-183">ISNULL is gebruikte tooforce null-waarden niet COALESCE</span><span class="sxs-lookup"><span data-stu-id="05838-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="05838-184">ISNULL is buitenste Hallo-functie</span><span class="sxs-lookup"><span data-stu-id="05838-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="05838-185">tweede deel van de Hallo Hallo ISNULL is een constante bijv. 0</span><span class="sxs-lookup"><span data-stu-id="05838-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="05838-186">Voor correct wordt ingesteld in Hallo nullability toobe is essentieel toouse `ISNULL` en niet `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="05838-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="05838-187">`COALESCE`is geen deterministische functie en dus Hallo resultaat van het Hallo-expressie wordt altijd null-waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="05838-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="05838-188">`ISNULL`verschilt.</span><span class="sxs-lookup"><span data-stu-id="05838-188">`ISNULL` is different.</span></span> <span data-ttu-id="05838-189">Het is deterministisch.</span><span class="sxs-lookup"><span data-stu-id="05838-189">It is deterministic.</span></span> <span data-ttu-id="05838-190">Daarom wanneer Hallo secondegedeelte van Hallo `ISNULL` functie is een constante zijn of een letterlijke waarde en vervolgens de resulterende waarde Hallo NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="05838-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="05838-191">Deze tip is niet alleen nuttig voor het garanderen van Hallo integriteit van de berekeningen.</span><span class="sxs-lookup"><span data-stu-id="05838-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="05838-192">Het is ook belangrijk voor het overschakelen van de tabel-partitie.</span><span class="sxs-lookup"><span data-stu-id="05838-192">It is also important for table partition switching.</span></span> <span data-ttu-id="05838-193">Stel, dat u hebt deze tabel die is gedefinieerd als uw fact:</span><span class="sxs-lookup"><span data-stu-id="05838-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="05838-194">Waardeveld Hallo is echter een berekende-expressie is niet deel uitmaakt van de brongegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="05838-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="05838-195">toocreate uw gepartitioneerde gegevensset kunt u toodo dit:</span><span class="sxs-lookup"><span data-stu-id="05838-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="05838-196">Hallo-query uitgevoerd geen bezwaar.</span><span class="sxs-lookup"><span data-stu-id="05838-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="05838-197">Hallo probleem wordt geleverd wanneer u tooperform Hallo partitie switch probeert.</span><span class="sxs-lookup"><span data-stu-id="05838-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="05838-198">Hallo tabeldefinities komen niet overeen.</span><span class="sxs-lookup"><span data-stu-id="05838-198">hello table definitions do not match.</span></span> <span data-ttu-id="05838-199">toomake hello tabeldefinities overeen met de Hallo die CTAS toobe gewijzigd moet.</span><span class="sxs-lookup"><span data-stu-id="05838-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="05838-200">U kunt daarom zien type consistentie en onderhouden van null-waarde bevat eigenschappen van een CTAS wordt goed engineering aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="05838-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="05838-201">Het helpt toomaintain integriteit in uw berekeningen en zorgt er ook voor dat het overschakelen van de partitie mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="05838-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="05838-202">Raadpleeg voor meer informatie over het gebruik van de tooMSDN [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="05838-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="05838-203">Het is een van de belangrijkste overzichten Hallo in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="05838-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="05838-204">Zorg ervoor dat grondig begrijpen.</span><span class="sxs-lookup"><span data-stu-id="05838-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05838-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05838-205">Next steps</span></span>
<span data-ttu-id="05838-206">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="05838-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
