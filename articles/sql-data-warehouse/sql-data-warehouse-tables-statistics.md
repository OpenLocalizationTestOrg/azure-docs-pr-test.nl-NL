---
title: aaaManaging statistieken over tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met statistieken over tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Het beheren van statistieken over tabellen in SQL Data Warehouse
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

Hallo meer SQL Data Warehouse weet over uw gegevens hello sneller kunnen worden uitgevoerd een query uitgevoerd op uw gegevens.  Hallo-manier waarop u SQL Data Warehouse vertellen over uw gegevens, is door het verzamelen van statistieken over uw gegevens.  Statistieken over voor uw gegevens is een van de belangrijkste zaken Hallo kunt u toooptimize uw query's uitvoeren.  Statistieken helpen SQL Data Warehouse Hallo optimale plan voor uw query's maken.  Dit is omdat Hallo SQL Data Warehouse query optimaliseren is kosten op basis van optimaliseren.  Dat wil zeggen, het Hallo kosten van verschillende queryplannen vergelijkt en vervolgens kiest Hallo plan met de laagste kosten hello, moet ook Hallo-plan dat Hallo snelste wordt uitgevoerd.

Statistieken kunnen worden gemaakt op één kolom, meerdere kolommen of op een index van een tabel.  Statistieken worden opgeslagen in een histogram Hallo bereik en selectiviteit van waarden bevat.  Dit is met name van belang wanneer Hallo optimaliseren tooevaluate JOINs, GROUP BY, HAVING moet en WHERE-componenten in een query.  Bijvoorbeeld als Hallo optimaliseren maakt een schatting van dat Hallo datum die u hebt gefilterd in uw query retourneert 1 rij, kunnen ervoor kiezen een heel andere plannen dan als deze maakt een schatting datum die u hebt geselecteerd wordt 1 miljoen rijen worden geretourneerd.  Tijdens het maken van statistieken is zeer belangrijk, is het belangrijk dat statistieken *nauwkeurig* Hallo huidige status van de tabel Hallo weerspiegelen.  Met up-to-date statistieken zorgt ervoor dat het een goed plan is geselecteerd door Hallo optimaliseren.  Hallo plannen die zijn gemaakt door optimalisatie van Hallo zijn alleen nuttig als Hallo statistieken over uw gegevens.

Hallo-proces van het maken en bijwerken van statistieken is op dit moment een handmatig proces, maar het is zeer eenvoudig toodo.  Dit is in tegenstelling tot SQL Server die automatisch wordt gemaakt en statistieken over één kolommen en indexen bijgewerkt.  Met behulp van Hallo informatie hieronder kunt u aanzienlijk Hallo beheer van Hallo statistieken automatiseren voor uw gegevens. 

## <a name="getting-started-with-statistics"></a>Aan de slag met statistieken
 Steekproef statistieken maken voor elke kolom is een eenvoudige manier tooget gestart met statistieken.  Omdat het even belangrijk tookeep statistieken up-to-date voorzichtig kan worden tooupdate uw statistieken dagelijks of na elke load. Er zijn altijd verschillen tussen de prestaties en Hallo kosten toocreate en update statistics.  Als u dat het duurt te lang toomaintain alle van de statistieken vindt, kunt u tootry toobe meer selectieve over welke kolommen hebben statistieken of welke kolommen regelmatig hoeft te worden bijgewerkt.  Bijvoorbeeld, kunt u tooupdate datumkolommen dagelijks nieuwe waarden kunnen worden toegevoegd in plaats van na elke load. Opnieuw, krijgt u Hallo profiteren doordat de statistieken voor kolommen die zijn betrokken in JOINs, GROUP BY, HAVING en de component WHERE.  Als u een tabel met een groot aantal hebt kolommen die alleen worden gebruikt in Hallo SELECT-component, statistieken voor deze kolommen kunnen niet help en nog iets meer moeite tooidentify uitgaven alleen Hallo kolommen waarin statistieken helpt, inkorten Hallo tijd toomaintain uw statistieken .

## <a name="multi-column-statistics"></a>Statistieken met meerdere kolommen
Bovendien toocreating statistieken voor één kolommen, merkt u dat uw query's van meerdere kolomstatistieken profiteren.  Statistieken met meerdere kolommen worden statistieken gemaakt op een lijst met kolommen.  Ze één kolomstatistieken over de eerste kolom Hallo opnemen in lijst hello, plus informatie cross-kolom correlatie dichtheden aangeroepen.  Bijvoorbeeld, als er een tabel met twee kolommen tooanother koppelt, wellicht dat SQL Data Warehouse beter Hallo plan optimaliseren kunt wordt begrepen Hallo relatie tussen twee kolommen.   Statistieken met meerdere kolommen kunnen query's sneller voor bepaalde bewerkingen zoals joins samengestelde en gegroepeerd.

## <a name="updating-statistics"></a>Bijwerken van statistieken
Bijwerken van statistieken is een belangrijk onderdeel van uw database management routine.  Als de distributie van gegevens in de database Hallo Hallo verandert, moeten statistieken toobe bijgewerkt.  Verouderde statistieken leidt toosub optimale query-prestaties.

Een aanbevolen procedure is tooupdate statistieken over datumkolommen elke dag als nieuwe datums worden toegevoegd.  Elke keer nieuwe rijen zijn geladen in het datawarehouse hello, worden nieuwe load datums of transactiedatums toegevoegd. Deze wijzigen Hallo gegevensdistributie en Hallo statistieken verouderd wilt maken. Als u daarentegen statistieken over een land-kolom in een tabel van de klant nooit moet mogelijk toobe bijgewerkt, zoals Hallo distributie van de waarden in het algemeen niet wijzigen. Ervan uitgaande dat Hallo distributie constant tussen klanten, het toevoegen van nieuwe rijen toohello tabel variatie is niet op het punt toochange Hallo gegevensdistributie. Echter, als uw datawarehouse alleen een bepaald land bevat en u Importeer gegevens vanuit een nieuw land, wat resulteert in gegevens uit meerdere landen worden opgeslagen, zeker moet u tooupdate statistieken op Hallo land kolom.

Een van de Hallo eerste vragen tooask wanneer het oplossen van een query, 'Hallo statistieken actueel zijn?"

Deze vraag is niet een die kunnen worden beantwoord door Hallo leeftijd van de Hallo-gegevens. Een up-to-date toodate statistieken-object kan worden oude als er is geen aanzienlijke wijzigingen toohello onderliggende gegevens. Wanneer het aantal rijen Hallo aanzienlijk is gewijzigd of er is een belangrijke wijziging in Hallo verdeling van waarden voor een bepaalde kolom *vervolgens* tooupdate statistieken is.  

Ter referentie: **SQL Server** (geen SQL Data Warehouse) automatisch bijgewerkt statistieken voor deze situaties:

* Als er geen rijen in de tabel hello, wanneer u rijen toevoegt, krijgt u een automatische update van statistieken
* Wanneer u meer dan 500 rijen tooa tabel beginnen met minder dan 500 rijen toevoegen (bijvoorbeeld aan begin u 499 hebben en voegt vervolgens 500 rijen tooa totaal 999 rijen), krijgt u een automatische update 
* Als u meer dan 500 rijen klaar hebt uitgevoerd, 500 extra rijen tooadd + 20% van de grootte van tabel Hallo Hallo voordat u een automatische update op Hallo-statistieken ziet

Omdat er geen toodetermine DMV als gegevens binnen het Hallo-tabel is gewijzigd sinds de laatste tijdstatistieken Hallo zijn bijgewerkt, kunt weten Hallo leeftijd van de statistieken u kennismaken met onderdeel van Hallo-afbeelding.  Kunt u Hallo query toodetermine Hallo laatste keer dat de statistieken te volgen waarbij bijgewerkt op elke tabel.  

> [!NOTE]
> Vergeet niet dat als er een aanzienlijke wijzigingen in Hallo verdeling van waarden voor een bepaalde kolom, moet u bijwerken statistieken ongeacht Hallo laatste keer dat ze zijn bijgewerkt.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Datumkolommen in een datawarehouse bijvoorbeeld meestal regelmatig hoeft te worden statistieken updates. Elke keer nieuwe rijen zijn geladen in het datawarehouse hello, worden nieuwe load datums of transactiedatums toegevoegd. Deze wijzigen Hallo gegevensdistributie en Hallo statistieken verouderd wilt maken.  Als u daarentegen statistieken voor een kolom geslacht in een klantentabel mogelijk nooit toobe bijgewerkt. Ervan uitgaande dat Hallo distributie constant tussen klanten, het toevoegen van nieuwe rijen toohello tabel variatie is niet op het punt toochange Hallo gegevensdistributie. Echter als uw datawarehouse slechts één geslacht en een nieuwe vereiste resultaten in meerdere geslachten bevat moet beslist u tooupdate statistieken op Hallo geslacht kolom.

Zie voor verdere uitleg [statistieken] [ Statistics] op MSDN.

## <a name="implementing-statistics-management"></a>Implementatie van statistieken management
Het is vaak een goed idee tooextend uw gegevens te laden proces tooensure die statistieken worden bijgewerkt op Hallo end Hallo belast. laden van gegevens Hallo is wanneer tabellen meest hun grootte en/of de distributie van de waarden wijzigen. Daarom is dit een logische plaats tooimplement bepaalde processen voor Apparaatbeheer.

Sommige principes zijn hieronder beschikbaar voor het bijwerken van de statistieken tijdens het laden van Hallo:

* Zorg ervoor dat elke geladen tabel ten minste één statistieken-object bijgewerkt. Deze updates Hallo-informatie over de grootte (aantal rijen en aantal pagina's) als onderdeel van Hallo statistieken update tabellen.
* Richt u op de kolommen die deel uitmaken van JOIN, GROUP BY, ORDER BY en DISTINCT-componenten
* Houd rekening met het bijwerken van kolommen 'oplopende sleutel' zoals transactie vaker als deze waarden niet in Hallo statistieken histogram opgenomen worden datums.
* U kunt statische distributiekolommen minder vaak bijwerken.
* Vergeet niet dat elk object statistiek is bijgewerkt in de reeks. Gewoon implementeren `UPDATE STATISTICS <TABLE_NAME>` mogelijk niet ideaal - vooral voor grote tabellen met veel objecten zijn statistieken.

> [!NOTE]
> Raadpleeg voor meer informatie over [sleutel oplopende] toohello SQL Server 2014 kardinaliteitsschatting model technisch document.
> 
> 

Zie voor verdere uitleg [Kardinaliteitsschatting] [ Cardinality Estimation] op MSDN.

## <a name="examples-create-statistics"></a>Voorbeelden: Statistieken maken
Deze voorbeelden laten zien hoe toouse verschillende opties voor het maken van statistieken. Hallo-opties die u voor elke kolom gebruiken, is afhankelijk van Hallo kenmerken van uw gegevens en hoe Hallo-kolom worden gebruikt in query's.

### <a name="a-create-single-column-statistics-with-default-options"></a>A. Statistieken voor één kolom maken met de standaardopties
statistieken voor een kolom toocreate verstrek een naam voor Hallo statistieken object en het Hallo-naam van Hallo kolom.

Deze syntaxis gebruikt alle Hallo standaardopties te gebruiken. Standaard wordt in SQL Data Warehouse 20 procent van de tabel Hallo voorbeelden bij het maken van statistieken.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Bijvoorbeeld:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Maken van statistieken voor één kolom aan de hand van elke rij
Hallo standaard samplefrequentie van 20 procent is voldoende voor de meeste situaties. U kunt echter Hallo samplingfrequentie aanpassen.

toosample hello volledige tabel, gebruik de volgende syntaxis:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Bijvoorbeeld:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Statistieken voor één kolom maken door te geven van de grootte van de steekproef Hallo
U kunt ook de samplegrootte Hallo opgeven als een percentage:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Maken van statistieken voor één kolom op slechts een deel van Hallo rijen
Een andere optie kunt u statistieken op een gedeelte van Hallo rijen in de tabel. Dit is een gefilterde statistieken genoemd.

U kunt gefilterde statistieken bijvoorbeeld bij het plannen van een specifieke partitie van een grote gepartitioneerde tabel tooquery. Door het maken van statistieken op alleen Hallo partitie waarden, nauwkeurigheid Hallo Hallo statistieken wordt te verbeteren, en daarom queryprestaties verbeteren.

In dit voorbeeld maakt statistieken op een bereik met waarden. Hallo-waarden kunnen eenvoudig worden gedefinieerd toomatch Hallo bereik van waarden in een partitie.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Voor Hallo query optimaliseren tooconsider met gefilterde statistieken wanneer het Hallo gedistribueerde queryplan kiest, moet de Hallo query binnen Hallo definitie van Hallo statistieken object passen. Hallo vorige voorbeeld Hallo van de query waarin component toospecify col1 waarden tussen 2000101 en 20001231 moet gebruiken.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Statistieken voor één kolom maken met alle Hallo-opties
U kunt, natuurlijk Hallo opties samen combineren. Hallo in het volgende voorbeeld wordt een gefilterde statistieken-object gemaakt met een aangepaste samplegrootte:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Zie voor volledige naslaginformatie Hallo [CREATE STATISTICS] [ CREATE STATISTICS] op MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Statistieken met meerdere kolommen maken
toocreate een statistieken met meerdere kolommen gewoon gebruiken Hallo eerdere voorbeelden, maar meer kolommen opgeven.

> [!NOTE]
> Hallo histogram die wordt gebruikt tooestimate aantal rijen in het queryresultaat hello, is alleen beschikbaar voor de eerste kolom Hallo die worden vermeld in de objectdefinitie van Hallo statistieken.
> 
> 

In dit voorbeeld Hallo histogram is op *product\_categorie*. Statistieken voor cross-kolom worden berekend op *product\_categorie* en *product\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Omdat er een correlatie tussen *product\_categorie* en *product\_sub\_categorie*, een stat met meerdere kolommen kan nuttig zijn als deze kolommen zijn toegankelijk op Hallo hetzelfde moment.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Statistieken maken voor alle Hallo kolommen in een tabel
Eenzijdige toocreate statistieken is tooissues CREATE STATISTICS opdrachten na het Hallo-tabel maken.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Een opgeslagen procedure toocreate statistieken voor alle kolommen in een database gebruiken
SQL Data Warehouse heeft geen een equivalent van de opgeslagen procedure systeem te [sp_create_stats] [] in SQL Server. Deze opgeslagen procedure maakt een object van de statistieken één kolom voor elke kolom van het Hallo-database die nog geen statistieken.

Dit helpt u aan de slag met het ontwerp van de database. Gratis tooadapt van mening bent dat deze tooyour nodig heeft.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

statistieken voor alle kolommen in tabel met deze procedure Hallo toocreate aanroep gewoon Hallo procedure.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Voorbeelden: update statistics
statistieken over tooupdate, kunt u:

1. Een object van de statistieken worden bijgewerkt. Hallo-naam van Hallo statistieken object dat u tooupdate wilt opgeven.
2. Werk alle statistieken objecten in een tabel. Hallo-naam van het Hallo-tabel in plaats van één specifieke statistieken-object opgeven.

### <a name="a-update-one-specific-statistics-object"></a>A. Object voor een specifieke statistieken bijwerken
Gebruik Hallo syntaxis tooupdate een specifieke statistieken-object te volgen:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Bijvoorbeeld:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Door het bijwerken van statistieken voor specifieke objecten, kunt u statistieken voor Hallo tijd en hulpbronnen vereist toomanage minimaliseren. Hiervoor moet dat een aantal beschouwd, echter toochoose Hallo best statistieken objecten tooupdate.

### <a name="b-update-all-statistics-on-a-table"></a>B. Bijwerken van alle statistische gegevens in een tabel
Hier wordt een eenvoudige methode voor het bijwerken van alle Hallo statistieken objecten in een tabel.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Bijvoorbeeld:

```sql
UPDATE STATISTICS dbo.table1;
```

Deze instructie is eenvoudig toouse. Vergeet niet dit alle statistische gegevens op tabel Hallo-updates en meer werk dan noodzakelijk is daarom mogelijk uitvoeren. Als geen Hallo prestaties een probleem is, is dit zeker Hallo eenvoudigste en meest volledige manier tooguarantee statistieken bijgewerkt zijn.

> [!NOTE]
> Wanneer alle statistische gegevens in een tabel wordt bijgewerkt, wordt in SQL Data Warehouse scan toosample Hallo table voor elke statistieken bevat. Als de tabel Hallo groot is, kan heeft veel kolommen en veel statistieken, dat efficiënter tooupdate afzonderlijke statistieken op basis van behoeften.
> 
> 

Voor een implementatie van een `UPDATE STATISTICS` procedure Zie Hallo [tijdelijke tabellen] [ Temporary] artikel. Hallo implementatie methode is iets anders toohello `CREATE STATISTICS` bovenstaande procedure maar Hallo eindresultaat is dezelfde Hallo.

Zie voor de volledige syntaxis hello, [Update Statistics] [ Update Statistics] op MSDN.

## <a name="statistics-metadata"></a>Statistieken metagegevens
Er zijn verschillende systeemweergave en functies waarmee u informatie over statistieken toofind kunt. U kunt bijvoorbeeld zien als een object statistieken mogelijk verouderd met behulp van Hallo statistieken datum functie toosee wanneer statistieken laatste zijn gemaakt of bijgewerkt.

### <a name="catalog-views-for-statistics"></a>Catalogusweergaven voor statistieken
Deze systeemweergaven bevatten informatie over statistieken:

| Catalogusweergave | Beschrijving |
|:--- |:--- |
| [sys.Columns][sys.columns] |Een rij voor elke kolom. |
| [sys.Objects][sys.objects] |Een rij voor elk object in het Hallo-database. |
| [sys.schemas][sys.schemas] |Een rij voor elk schema in Hallo-database. |
| [sys.Stats][sys.stats] |Een rij voor elk object statistieken. |
| [sys.stats_columns][sys.stats_columns] |Een rij voor elke kolom in Hallo statistieken object. Teruggekoppeld toosys.columns. |
| [sys.Tables][sys.tables] |Een rij voor elke tabel (inclusief externe tabellen). |
| [sys.table_types][sys.table_types] |Een rij voor elk gegevenstype. |

### <a name="system-functions-for-statistics"></a>Systeemfuncties voor statistieken
Deze systeemfuncties zijn nuttig voor het werken met statistieken:

| De systeemfunctie | Beschrijving |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Datum Hallo statistieken object het laatst is bijgewerkt. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Samenvatting niveau en gedetailleerde informatie over de distributie van de waarden Hallo biedt begrepen door Hallo statistieken object. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Functies en statistieken kolommen combineren in één weergave
Deze weergave worden de kolommen die betrekking toostatistics en de resultaten van Hallo [STATS_DATE()] [] functie samen hebben.

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>DBCC SHOW_STATISTICS()-voorbeelden
DBCC SHOW_STATISTICS() toont Hallo-gegevens die zijn opgeslagen in een object van statistieken. Deze gegevens zijn afkomstig uit drie delen.

1. Koptekst
2. Dichtheid Vector
3. Histogram

Hallo-header metagegevens over Hallo statistieken. Hallo histogram geeft Hallo distributie van de waarden in Hallo eerste sleutelkolom van Hallo statistieken object. Hallo dichtheid vector metingen cross-kolom correlatie. SQLDW berekent kardinaliteit maakt een schatting met Hallo-gegevens in Hallo statistieken-object.

### <a name="show-header-density-and-histogram"></a>Koptekst, dichtheid en histogram weergeven
Dit eenvoudige voorbeeld toont alle drie onderdelen van een object statistieken.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Bijvoorbeeld:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Een of meer onderdelen van DBCC SHOW_STATISTICS(); weergeven
Als u alleen geïnteresseerd bent in specifieke onderdelen weer te geven, gebruikt u Hallo `WITH` component en geef op welke onderdelen u wilt dat toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Bijvoorbeeld:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>DBCC SHOW_STATISTICS() verschillen
DBCC SHOW_STATISTICS() is meer strikt in SQL Data Warehouse vergeleken tooSQL Server geïmplementeerd.

1. Niet-gedocumenteerde functies worden niet ondersteund
2. Stats_stream kan niet worden gebruikt.
3. Resultaten voor specifieke subreeksen van statistische gegevens bijvoorbeeld niet koppelen (STAT_HEADER JOIN DENSITY_VECTOR)
4. NO_INFOMSGS kan niet worden ingesteld voor bericht onderdrukken
5. Vierkante haken om de namen van statistieken kan niet worden gebruikt.
6. Kolom namen tooidentify statistieken objecten kan niet worden gebruikt.
7. Aangepaste fout 2767 wordt niet ondersteund

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] op MSDN.  toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel] [ Partition] en [ Tijdelijke tabellen][Temporary].  Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
