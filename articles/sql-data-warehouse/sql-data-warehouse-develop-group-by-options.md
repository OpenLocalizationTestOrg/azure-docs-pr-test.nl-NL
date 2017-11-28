---
title: aaaGroup door de opties in SQL Data Warehouse | Microsoft Docs
description: Tips voor het implementeren van de groep door de opties in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="dc281-103">Groeperen op opties in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dc281-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="dc281-104">Hallo [GROUP BY] [ GROUP BY] component wordt gebruikt tooaggregate tooa samenvatting gegevensset van rijen.</span><span class="sxs-lookup"><span data-stu-id="dc281-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="dc281-105">Er wordt ook een aantal opties die de functionaliteit die nodig toobe gewerkt rond als ze niet rechtstreeks worden ondersteund door Azure SQL Data Warehouse uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="dc281-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="dc281-106">Deze opties zijn</span><span class="sxs-lookup"><span data-stu-id="dc281-106">These options are</span></span>

* <span data-ttu-id="dc281-107">GROUP BY met UPDATEPAKKET</span><span class="sxs-lookup"><span data-stu-id="dc281-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="dc281-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="dc281-108">GROUPING SETS</span></span>
* <span data-ttu-id="dc281-109">GROUP BY met kubus</span><span class="sxs-lookup"><span data-stu-id="dc281-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="dc281-110">Rollup en grouping sets-opties</span><span class="sxs-lookup"><span data-stu-id="dc281-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="dc281-111">Hallo eenvoudigste optie hier is toouse `UNION ALL` in plaats daarvan tooperform Hallo updatepakket in plaats van vertrouwen op Hallo expliciete syntaxis.</span><span class="sxs-lookup"><span data-stu-id="dc281-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="dc281-112">Hallo-resultaat is exact dezelfde Hallo</span><span class="sxs-lookup"><span data-stu-id="dc281-112">hello result is exactly hello same</span></span>

<span data-ttu-id="dc281-113">Hieronder volgt een voorbeeld van een groep door Hallo-instructie `ROLLUP` optie:</span><span class="sxs-lookup"><span data-stu-id="dc281-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="dc281-114">Met behulp van UPDATEPAKKET hebben we Hallo na aggregaties aangevraagd:</span><span class="sxs-lookup"><span data-stu-id="dc281-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="dc281-115">Land en regio</span><span class="sxs-lookup"><span data-stu-id="dc281-115">Country and Region</span></span>
* <span data-ttu-id="dc281-116">Land</span><span class="sxs-lookup"><span data-stu-id="dc281-116">Country</span></span>
* <span data-ttu-id="dc281-117">Eindtotaal</span><span class="sxs-lookup"><span data-stu-id="dc281-117">Grand Total</span></span>

<span data-ttu-id="dc281-118">tooreplace dit moet u toouse `UNION ALL`; Hallo aggregaties vereist het expliciet opgeven tooreturn Hallo dezelfde resultaten:</span><span class="sxs-lookup"><span data-stu-id="dc281-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="dc281-119">Voor GROUPING SETS we toodo hoeft vast Hallo dezelfde principal, maar alleen UNION ALL secties voor Hallo aggregatie niveaus maken willen we toosee</span><span class="sxs-lookup"><span data-stu-id="dc281-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="dc281-120">Kubusopties voor de</span><span class="sxs-lookup"><span data-stu-id="dc281-120">Cube options</span></span>
<span data-ttu-id="dc281-121">Het is mogelijk toocreate een groep met WITH CUBE met Hallo UNION ALL benadering.</span><span class="sxs-lookup"><span data-stu-id="dc281-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="dc281-122">Hallo-probleem is Hallo code kan al gauw omslachtig en onhandig.</span><span class="sxs-lookup"><span data-stu-id="dc281-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="dc281-123">toomitigate dit kunt u deze meer geavanceerde benadering.</span><span class="sxs-lookup"><span data-stu-id="dc281-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="dc281-124">We gebruiken Hallo in bovenstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="dc281-124">Let's use hello example above.</span></span>

<span data-ttu-id="dc281-125">de eerste stap Hallo is toodefine Hallo kubus, die alle Hallo niveaus van aggregatie willen we toocreate definieert.</span><span class="sxs-lookup"><span data-stu-id="dc281-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="dc281-126">Het is belangrijk tootake Opmerking Hallo CROSS JOIN van Hallo twee afgeleide tabellen.</span><span class="sxs-lookup"><span data-stu-id="dc281-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="dc281-127">Hiermee wordt alle Hallo niveaus gegenereerd voor ons.</span><span class="sxs-lookup"><span data-stu-id="dc281-127">This generates all hello levels for us.</span></span> <span data-ttu-id="dc281-128">Hallo rest Hallo code is echt er voor opmaak.</span><span class="sxs-lookup"><span data-stu-id="dc281-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="dc281-129">Hallo-resultaten van Hallo CTAS ziet u hieronder:</span><span class="sxs-lookup"><span data-stu-id="dc281-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="dc281-130">Hallo tweede stap is het resultaat is een doel tabel toostore tussentijds toospecify:</span><span class="sxs-lookup"><span data-stu-id="dc281-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="dc281-131">de derde stap Hallo is tooloop over onze kubus van kolommen Hallo aggregatie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="dc281-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="dc281-132">Hallo-query wordt eenmaal uitvoeren voor elke rij in de tijdelijke tabel Hallo #Cube en Hallo resultaten op te slaan in de tijdelijke tabel Hallo #Results</span><span class="sxs-lookup"><span data-stu-id="dc281-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="dc281-133">Ten slotte kunt we Hallo resultaten terugkeren door gewoon lezen van de tijdelijke tabel Hallo #Results</span><span class="sxs-lookup"><span data-stu-id="dc281-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="dc281-134">Hallo-code in de secties splitsen en het genereren van een samenvoegartikel constructie Hallo wordt code beheerd en meer bruikbaar.</span><span class="sxs-lookup"><span data-stu-id="dc281-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc281-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc281-135">Next steps</span></span>
<span data-ttu-id="dc281-136">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="dc281-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
