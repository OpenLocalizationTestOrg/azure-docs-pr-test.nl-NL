---
title: Groeperen op opties in SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="06fc1-103">Groeperen op opties in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="06fc1-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="06fc1-104">De [GROUP BY] [ GROUP BY] component wordt gebruikt voor een overzicht set rijen van cumulatieve gegevens.</span><span class="sxs-lookup"><span data-stu-id="06fc1-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="06fc1-105">Er wordt ook een aantal opties die de functionaliteit die moet worden besteed uitbreiden rond als ze niet rechtstreeks worden ondersteund door Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06fc1-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="06fc1-106">Deze opties zijn</span><span class="sxs-lookup"><span data-stu-id="06fc1-106">These options are</span></span>

* <span data-ttu-id="06fc1-107">GROUP BY met UPDATEPAKKET</span><span class="sxs-lookup"><span data-stu-id="06fc1-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="06fc1-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="06fc1-108">GROUPING SETS</span></span>
* <span data-ttu-id="06fc1-109">GROUP BY met kubus</span><span class="sxs-lookup"><span data-stu-id="06fc1-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="06fc1-110">Rollup en grouping sets-opties</span><span class="sxs-lookup"><span data-stu-id="06fc1-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="06fc1-111">De eenvoudigste optie hier is het gebruik `UNION ALL` in plaats daarvan de rollup uitvoeren in plaats van te vertrouwen op de expliciete syntaxis.</span><span class="sxs-lookup"><span data-stu-id="06fc1-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="06fc1-112">Het resultaat is precies hetzelfde</span><span class="sxs-lookup"><span data-stu-id="06fc1-112">The result is exactly the same</span></span>

<span data-ttu-id="06fc1-113">Hieronder volgt een voorbeeld van een groep met behulp van de instructie de `ROLLUP` optie:</span><span class="sxs-lookup"><span data-stu-id="06fc1-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

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

<span data-ttu-id="06fc1-114">Met behulp van UPDATEPAKKET hebben we de volgende aggregaties aangevraagd:</span><span class="sxs-lookup"><span data-stu-id="06fc1-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="06fc1-115">Land en regio</span><span class="sxs-lookup"><span data-stu-id="06fc1-115">Country and Region</span></span>
* <span data-ttu-id="06fc1-116">Land</span><span class="sxs-lookup"><span data-stu-id="06fc1-116">Country</span></span>
* <span data-ttu-id="06fc1-117">Eindtotaal</span><span class="sxs-lookup"><span data-stu-id="06fc1-117">Grand Total</span></span>

<span data-ttu-id="06fc1-118">Dit u wilt gebruiken vervangen `UNION ALL`; aggregaties vereist expliciet om dezelfde resultaten weer te geven:</span><span class="sxs-lookup"><span data-stu-id="06fc1-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

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

<span data-ttu-id="06fc1-119">Voor GROUPING SETS alle we moeten doen is dezelfde principal vast maar UNION ALL secties voor de aggregatie niveaus die we wilt zien alleen maken</span><span class="sxs-lookup"><span data-stu-id="06fc1-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="06fc1-120">Kubusopties voor de</span><span class="sxs-lookup"><span data-stu-id="06fc1-120">Cube options</span></span>
<span data-ttu-id="06fc1-121">Het is mogelijk een groep door met de kubus maken met de UNION ALL benadering.</span><span class="sxs-lookup"><span data-stu-id="06fc1-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="06fc1-122">Het probleem is de code kan al gauw omslachtig en onhandig.</span><span class="sxs-lookup"><span data-stu-id="06fc1-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="06fc1-123">Als oplossing hiervoor kunt u deze meer geavanceerde benadering.</span><span class="sxs-lookup"><span data-stu-id="06fc1-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="06fc1-124">We gaan gebruiken in het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="06fc1-124">Let's use the example above.</span></span>

<span data-ttu-id="06fc1-125">De eerste stap is voor het definiëren van de 'kubus' waarin alle niveaus van aggregatie die we willen maken.</span><span class="sxs-lookup"><span data-stu-id="06fc1-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="06fc1-126">Het is belangrijk te nemen van de CROSS JOIN van de twee afgeleide tabellen.</span><span class="sxs-lookup"><span data-stu-id="06fc1-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="06fc1-127">Hiermee wordt alle niveaus gegenereerd voor ons.</span><span class="sxs-lookup"><span data-stu-id="06fc1-127">This generates all the levels for us.</span></span> <span data-ttu-id="06fc1-128">De rest van de code is echt er voor opmaak.</span><span class="sxs-lookup"><span data-stu-id="06fc1-128">The rest of the code is really there for formatting.</span></span>

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

<span data-ttu-id="06fc1-129">Hieronder ziet u de resultaten van de CTAS:</span><span class="sxs-lookup"><span data-stu-id="06fc1-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="06fc1-130">De tweede stap is om op te geven van een doeltabel voor het opslaan van tijdelijke resultaten:</span><span class="sxs-lookup"><span data-stu-id="06fc1-130">The second step is to specify a target table to store interim results:</span></span>

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

<span data-ttu-id="06fc1-131">De derde stap is het doorlopen van onze kubus van kolommen uitvoeren van de aggregatie.</span><span class="sxs-lookup"><span data-stu-id="06fc1-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="06fc1-132">De query wordt eenmaal uitvoeren voor elke rij in de tijdelijke tabel #Cube en de resultaten op te slaan in de tijdelijke tabel #Results</span><span class="sxs-lookup"><span data-stu-id="06fc1-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

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

<span data-ttu-id="06fc1-133">Ten slotte kunt we de resultaten terugkeren door gewoon lezen van de tijdelijke tabel #Results</span><span class="sxs-lookup"><span data-stu-id="06fc1-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="06fc1-134">De code wordt door de code in de secties splitsen en het genereren van een samenvoegartikel constructie beter beheerbaar en bruikbaar.</span><span class="sxs-lookup"><span data-stu-id="06fc1-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06fc1-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06fc1-135">Next steps</span></span>
<span data-ttu-id="06fc1-136">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="06fc1-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
