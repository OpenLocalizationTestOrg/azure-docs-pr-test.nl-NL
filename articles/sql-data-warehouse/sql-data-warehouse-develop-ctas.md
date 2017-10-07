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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Table As Select (CTAS) in SQL datawarehouse maken
Maken van de tabel als selecteren of `CTAS` is een van de Hallo belangrijkste T-SQL-functies die beschikbaar zijn. Het is een volledig parallelized bewerking die u een nieuwe tabel op basis van het Hallo-uitvoer van een SELECT-instructie maakt. `CTAS`Hallo snelste en eenvoudigste manier toocreate is een kopie van een tabel. Dit document bevat zowel voorbeelden en aanbevolen procedures voor `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECTEREN... IN de vs. CTAS
U kunt overwegen `CTAS` Super bedrag versie van `SELECT..INTO`.

Hieronder volgt een voorbeeld van een eenvoudige `SELECT..INTO` instructie:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

In bovenstaande Hallo voorbeeld `[dbo].[FactInternetSales_new]` zou worden gemaakt als ROUND_ROBIN gedistribueerde tabel met deze functie een door de GECLUSTERDE COLUMNSTORE-INDEX, omdat dit Hallo tabel standaardinstellingen in Azure SQL Data Warehouse zijn.

`SELECT..INTO`echter kunt u niet toochange typt u ofwel Hallo distributie methode of Hallo index als onderdeel van Hallo-bewerking. Dit is wanneer `CTAS` van pas komt.

tooconvert Hallo hierboven te`CTAS` is heel eenvoudig:

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

Met `CTAS` u kunnen toochange zijn beide distributie van het Hallo-tabelgegevens, evenals een tabeltype Hallo Hallo. 

> [!NOTE]
> Als u alleen probeert toochange Hallo index in uw `CTAS` bewerking en Hallo brontabel is gedistribueerd-hash en vervolgens uw `CTAS` bewerking voert aanbevolen als u dezelfde kolom en gegevens Distributietype Hallo. Dit voorkomt cross-distributie gegevensverplaatsing tijdens efficiënter is Hallo-bewerking.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Met behulp van CTAS toocopy een tabel
Mogelijk een van de meest voorkomende Hallo maakt gebruik van `CTAS` is een exemplaar maken van een tabel zodat u Hallo DDL kunt wijzigen. Als u bijvoorbeeld uw tabel als oorspronkelijk maakte `ROUND_ROBIN` en nu wilt wijzigen tooa tabel gedistribueerd op een kolom `CTAS` is hoe u Hallo distributie kolom wilt wijzigen. `CTAS`gebruikte toochange kan partitioneren, te indexeren of kolom typen ook worden.

Stel dat u deze tabel met Hallo standaardtype distributie van gemaakt `ROUND_ROBIN` gedistribueerd omdat er geen distributiepunt-kolom is opgegeven in Hallo `CREATE TABLE`.

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

U kunt nu toocreate een nieuw exemplaar van deze tabel met een geclusterde Columnstore-Index zodat u van Hallo prestaties van de geclusterde Columnstore-tabellen profiteren kunt. Wilt u ook toodistribute deze tabel op ProductKey omdat u zijn anticiperen op verbindingen in deze kolom en gegevensverplaatsing tooavoid tijdens joins op ProductKey wilt. Tot slot wilt u ook tooadd partitioneren op OrderDateKey zodat u snel kunt u oude gegevens verwijderen door het verwijderen van oude partities. Hier volgt Hallo CTAS instructie waarmee uw oude tabel in een nieuwe tabel wilt kopiëren.

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

Ten slotte kunt u Wijzig de naam van uw tooswap tabellen in de nieuwe tabel en vervolgens uw oude tabel verwijderen.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.  Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.  Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Met behulp van CTAS toowork rond de niet-ondersteunde functies
`CTAS`gebruikte toowork rond een aantal onderstaande Hallo niet-ondersteunde functies kan ook worden veroorzaakt. Dit kan vaak tonen dat toobe een situatie win/win niet alleen uw code compatibel worden, maar dit wordt vaak sneller uitgevoerd op de SQL Data Warehouse. Dit is als gevolg van het ontwerp van de volledig parallelized. Scenario's die kunnen worden uitgevoerd om met CTAS omvatten:

* ANSI JOINS op UPDATEs
* ANSI-verbindingen in verwijderen
* MERGE-instructie

> [!NOTE]
> Probeer toothink ' CTAS eerste '. Als u denkt dat u kunt ook een probleem met oplossen `CTAS` is dat doorgaans de beste manier tooapproach Hallo deze - zelfs als u meer gegevens als gevolg hiervan worden geschreven.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>ANSI join vervanging voor update-instructies
U merkt dat u hebt een complexe update waar lid van meer dan twee tabellen samen met ANSI-syntaxis tooperform Hallo toevoegen, bijwerken of verwijderen.

Stel dat u deze tabel tooupdate had:

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

de oorspronkelijke query Hallo kan hebt gezien ongeveer het volgende:

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

Omdat SQL Data Warehouse biedt geen ondersteuning voor ANSI joins in Hallo `FROM` -component van een `UPDATE` instructie, u kunt deze code via niet kopiëren zonder dat een enigszins gewijzigd.

U kunt een combinatie van een `CTAS` en een impliciete tooreplace deze code toevoegen:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>ANSI join vervanging voor delete-instructies
Hallo aanbevolen benadering voor het verwijderen van gegevens is soms toouse `CTAS`. Selecteer de gewenste tookeep Hallo-gegevens in plaats van een eenvoudig hello gegevens verwijderen. Deze vooral voor `DELETE` instructies die gebruikmaken van ansi-syntaxis koppelen omdat SQL Data Warehouse biedt geen ondersteuning voor ANSI joins in Hallo `FROM` -component van een `DELETE` instructie.

Hieronder vindt u een voorbeeld van een geconverteerde DELETE-instructie:

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

## <a name="replace-merge-statements"></a>Vervang merge-instructies
Merge-instructies kunnen worden vervangen, ten minste gedeeltelijk met behulp van `CTAS`. U kunt consolideren Hallo `INSERT` en Hallo `UPDATE` in één instructie. Verwijderde records moet toobe in een tweede instructie afgesloten.

Een voorbeeld van een `UPSERT` hieronder:

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>CTAS aanbeveling: status expliciet gegevenstype en null-waarden van uitvoer
Bij het migreren van code is het wellicht tegenkomen van dit type codering patroon:

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

U kunt instinctief overwegen, moet u deze code tooa CTAS migreren en u niet juist. Er is echter een verborgen probleem hier.

Hallo volgende code wordt niet resulteert Hallo hetzelfde resultaat:

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

U ziet dat Hallo kolom 'resultaat' doorsturen Hallo type en nullability gegevenswaarden van Hallo expressie uitvoert. Dit kan toosubtle afwijkingen leiden waarden in als u niet zorgvuldig.

Voer een van de volgende Hallo als een voorbeeld:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

Hallo waarde die is opgeslagen voor resultaat verschilt. Hallo persistente waarde in Hallo resultatenkolom gebruikt in andere wordt expressies Hallo fout nog meer belangrijke.

![][1]

Dit is vooral belangrijk voor migraties van gegevens. Er is een probleem ondanks dat de tweede query Hallo weliswaar nauwkeuriger is. Hallo gegevens zou verschillende vergeleken toohello bronsysteem en die tooquestions van integriteit leidt Hallo-migratie. Dit is een van deze zeldzame gevallen waarbij 'verkeerde' Hallo-antwoord daadwerkelijk Hallo rechts een is!

Hallo reden zien we deze verschillen tussen de twee Hallo resultaten niet actief is tooimplicit casten typt. Eerste voorbeeld Hallo tabel definieert in Hallo Hallo-kolomdefinitie. Er treedt een impliciete conversie op Hallo rij wordt ingevoegd. In het tweede voorbeeld Hallo is er geen impliciete typeconversie zoals Hallo expressie gegevenstype van kolom Hallo definieert. U ziet dat ook dat Hallo-kolom in het tweede voorbeeld Hallo is gedefinieerd als een kolom waarvoor null is toegestaan dat in het eerste voorbeeld Hallo deze niet heeft. Wanneer het Hallo-tabel is gemaakt met Hallo eerste voorbeeld kolom nullability is expliciet is gedefinieerd. In het tweede voorbeeld Hallo is het alleen toohello expressie linker- en standaard dit zou leiden tot een NULL-definitie.  

tooresolve deze problemen die u moet expliciet Hallo typeconversie en null-waarden instellen in Hallo `SELECT` gedeelte Hallo `CTAS` instructie. U kunt deze niet instellen eigenschappen in Hallo deel van de tabel maken.

Hallo in het volgende voorbeeld laat zien hoe toofix Hallo code:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Let op Hallo volgende:

* CAST of CONVERT kan zijn gebruikt
* ISNULL is gebruikte tooforce null-waarden niet COALESCE
* ISNULL is buitenste Hallo-functie
* tweede deel van de Hallo Hallo ISNULL is een constante bijv. 0

> [!NOTE]
> Voor correct wordt ingesteld in Hallo nullability toobe is essentieel toouse `ISNULL` en niet `COALESCE`. `COALESCE`is geen deterministische functie en dus Hallo resultaat van het Hallo-expressie wordt altijd null-waarden bevatten. `ISNULL`verschilt. Het is deterministisch. Daarom wanneer Hallo secondegedeelte van Hallo `ISNULL` functie is een constante zijn of een letterlijke waarde en vervolgens de resulterende waarde Hallo NOT NULL.
> 
> 

Deze tip is niet alleen nuttig voor het garanderen van Hallo integriteit van de berekeningen. Het is ook belangrijk voor het overschakelen van de tabel-partitie. Stel, dat u hebt deze tabel die is gedefinieerd als uw fact:

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

Waardeveld Hallo is echter een berekende-expressie is niet deel uitmaakt van de brongegevens Hallo.

toocreate uw gepartitioneerde gegevensset kunt u toodo dit:

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

Hallo-query uitgevoerd geen bezwaar. Hallo probleem wordt geleverd wanneer u tooperform Hallo partitie switch probeert. Hallo tabeldefinities komen niet overeen. toomake hello tabeldefinities overeen met de Hallo die CTAS toobe gewijzigd moet.

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

U kunt daarom zien type consistentie en onderhouden van null-waarde bevat eigenschappen van een CTAS wordt goed engineering aanbevolen. Het helpt toomaintain integriteit in uw berekeningen en zorgt er ook voor dat het overschakelen van de partitie mogelijk is.

Raadpleeg voor meer informatie over het gebruik van de tooMSDN [CTAS][CTAS]. Het is een van de belangrijkste overzichten Hallo in Azure SQL Data Warehouse. Zorg ervoor dat grondig begrijpen.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
