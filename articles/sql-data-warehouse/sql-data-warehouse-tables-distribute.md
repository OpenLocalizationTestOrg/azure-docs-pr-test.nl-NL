---
title: aaaDistributing tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met het distribueren van tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distributie van tabellen in SQL Data Warehouse
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

SQL Data Warehouse is een gedistribueerd MPP-databasesysteem (Massively Parallel Processing).  Door gegevens- en processorcapaciteit over meerdere knooppunten te verdelen, kan SQL Data Warehouse grote schaalbaarheid bieden, veel groter dan enkel ander systeem.  Bepalen hoe toodistribute uw gegevens in uw SQL Data Warehouse is een van de belangrijkste Hallo factoren tooachieving optimale prestaties.   Hallo sleutel toooptimal prestaties is voor het minimaliseren van verplaatsing van gegevens en op zijn beurt Hallo sleutel toominimizing gegevensverplaatsing Hallo rechts distributiestrategie selecteert.

## <a name="understanding-data-movement"></a>Understanding gegevensverplaatsing
Hallo-gegevens van elke tabel is in een systeem MPP verdeeld over verschillende onderliggende databases.  Hallo meest geoptimaliseerde query's op een MPP-systeem kunnen eenvoudig worden doorgegeven via tooexecute Hallo afzonderlijke gedistribueerde databases zonder interactie tussen Hallo andere databases.  Stel dat u hebt een database met verkoopgegevens die twee tabellen, verkoop en klanten bevat.  Als u een query die toojoin uw verkoop tooyour klantentabel nodig hebt en u uw verkoop- en de klantentabellen up door klantnummer deelt, plaatsen van elke klant in een aparte database, kunnen alle query's die lid van de verkoop- en worden opgelost binnen elke database met zonder enige kennis van Hallo andere databases.  Daarentegen als u uw verkoopgegevens gedeeld door het nummer en de gegevens van de klant op klantnummer van de, vervolgens een bepaalde database geen bijbehorende Hallo-gegevens voor elke klant en dus als u uw klantgegevens van verkoopgegevens tooyour toojoin wilt, moet u tooget hello gegevens voor elke klant van Hallo andere databases.  In dit voorbeeld tweede moet gegevensverplaatsing toooccur toomove Hallo gegevens toohello verkoop klantgegevens, zodat Hallo twee tabellen kunnen worden gekoppeld.  

Verplaatsing van gegevens niet altijd slecht, soms is het nodig toosolve een query.  Maar nadat deze extra stap kan worden vermeden, natuurlijk uw query wordt sneller worden uitgevoerd.  Verplaatsing van gegevens ontstaat meestal als tabellen zijn gekoppeld of aggregaties worden uitgevoerd.  U moet vaak toodo beide, dus terwijl u mogelijk toooptimize voor een scenario, zoals een join, u nog moet data movement toohelp u oplossen voor Hallo ander scenario, zoals een aggregatie.  Hallo truc uitzoeken wat minder werk is.  In de meeste gevallen is distribueren grote feitentabellen op een algemeen lid kolom Hallo meest effectieve methode voor het beperken van Hallo meeste gegevensverplaatsing.  Distributie van gegevens op de join-kolommen is een meer algemene methode tooreduce verplaatsing van gegevens dan het distribueren van gegevens voor kolommen die zijn betrokken bij een aggregatie.

## <a name="select-distribution-method"></a>De methode distributiepunten selecteren
Uw gegevens worden in SQL Data Warehouse achter de schermen Hallo worden opgedeeld in 60 databases.  Elke individuele database waarnaar wordt verwezen tooas is een **distributie**.  Wanneer gegevens in elke tabel is geladen, is SQL Data Warehouse tooknow hoe toodivide van uw gegevens over deze 60 verdelingen.  

Hallo distributiemethode is gedefinieerd op Hallo tabelniveau en er zijn momenteel twee mogelijkheden:

1. **Round robin** die gegevens distribueren gelijkmatig maar willekeurig.
2. **Hash-gedistribueerde** die gegevens op basis van het hash-waarden uit één kolom distribueert

Standaard, wanneer u een distributiemethode gegevens niet definieert uw tabel worden gedistribueerd met behulp van Hallo **round-robin** distributiemethode.  Echter, naarmate u meer geavanceerde in uw implementatie, zult u met behulp van tooconsider **hash gedistribueerd** toominimize gegevensverplaatsing die op zijn beurt queryprestaties optimaliseert tabellen.

### <a name="round-robin-tables"></a>Round Robin tabellen
Gebruik van Hallo Round Robin-methode voor het distribueren van gegevens is zeer veel hoe het klinkt.  Als uw gegevens zijn geladen, wordt elke rij gewoon toohello volgende distributiepunt verzonden.  Deze methode van het distribueren van Hallo gegevens wordt altijd willekeurig Hallo gegevens zeer gelijkmatig verdelen over alle Hallo-distributies.  Er is geen sorteren gereed tijdens Hallo round robin-proces waarop uw gegevens geplaatst.  Een round robin-distributie is wel een willekeurige hash om deze reden.  Met een gedistribueerde tabel round robin-zijn er geen noodzaak toounderstand Hallo gegevens.  Round-Robin met tabellen kunnen daarom vaak goed laden doelen.

Standaard als er geen distributiemethode is gekozen, wordt hello distributiemethode round-robin gebruikt.  Terwijl round-robin tabellen eenvoudig toouse zijn omdat gegevens willekeurig is verdeeld over Hallo system dit betekent dat Hallo systeem biedt geen garantie van welke distributiepunten moet elke rij is echter op.  Als gevolg hiervan zijn soms Hallo system tooinvoke nodig heeft om een data movement bewerking toobetter uw gegevens delen voordat het oplossen van een query.  Deze extra stap kan uw query's vertragen.

Overweeg het gebruik van Round Robin distributie voor uw tabel in Hallo volgen scenario's:

* Wanneer aan de slag als een eenvoudige beginpunt
* Als er geen duidelijke die sleutel is
* Als er geen kolom met een goede kandidaat voor hash-tabel Hallo distribueren
* Als hello delen tabel niet een gemeenschappelijke join-sleutel met andere tabellen
* Als Hallo join is een minder belangrijke dan andere joins in Hallo-query
* Wanneer Hallo-tabel is een tijdelijke tabel fasering

Beide voorbeelden maakt een tabel Round Robin:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Tijdens een round-robin wordt Hallo tabel standaardtype expliciete in uw DDL wordt beschouwd als best practice zodat Hallo bedoelingen van de indeling van de tabel wissen tooothers zijn.
>
>

### <a name="hash-distributed-tables"></a>Hash-tabellen gedistribueerde
Met behulp van een **Hash gedistribueerd** algoritme toodistribute uw tabellen kunnen de prestaties verbeteren voor veel scenario's door verplaatsing van gegevens op het moment dat de query.  Hash gedistribueerde tabellen zijn tabellen die zijn verdeeld over de Hallo gedistribueerde databases met een hash-algoritme in één kolom die u selecteert.  Hallo distributie kolom is wat bepaalt hoe gegevens Hallo is verdeeld over uw gedistribueerde databases.  Hallo hash-functie maakt gebruik van Hallo distributie kolom tooassign rijen toodistributions.  Hallo hash-algoritme en de resulterende distributie is deterministisch.  Dat wil Hallo dezelfde waarde altijd hetzelfde gegevenstype wordt Hello toohello heeft hetzelfde distributiepunt.    

In dit voorbeeld maakt een tabel die wordt gedistribueerd bij-id:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>De kolom distributiepunten selecteren
Als u ervoor kiest te**hash distribueren** een tabel, moet u een kolom voor één distributiepunt tooselect.  Wanneer u een distributie-kolom selecteert, zijn er drie belangrijke factoren tooconsider.  

Selecteer één kolom die wordt:

1. Niet worden bijgewerkt
2. Verdelen gegevens, gegevens scheeftrekken voorkomen
3. Verplaatsing van gegevens beperken

### <a name="select-distribution-column-which-will-not-be-updated"></a>Distributiepunten selecteren kolom die wordt niet bijgewerkt
Distributiekolommen kunnen niet worden bijgewerkt, dus, selecteert u een kolom met statische waarden.  Als een kolom toobe bijgewerkt moet, wordt dit doorgaans niet goed distributiepunt geschikt is.  Als er een aanvraag waarin u een distributie-kolom moet bijwerken, kunt u dit doen door eerst Hallo rij te verwijderen en voegt vervolgens een nieuwe rij.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Distributiepunten selecteren kolom die gegevens wordt gelijkmatig verdelen
Omdat alleen als de traagste distributie snel een gedistribueerd systeem wordt uitgevoerd, is het belangrijk toodivide Hallo werk gelijkmatig over Hallo distributies in volgorde tooachieve met gelijke taakverdeling worden uitgevoerd in Hallo-systeem.  Hallo manier Hallo werk is onderverdeeld in een gedistribueerde systeem is gebaseerd op waar gegevens voor elke distributie Hallo woont.  Dit maakt het heel belangrijk tooselect Hallo rechts distributie kolom voor het distribueren van Hallo gegevens, zodat elke verdeling gelijk werk heeft en zal nemen Hallo dezelfde tijd toocomplete het gedeelte van het Hallo werk.  Wanneer het werk goed is onderverdeeld in Hallo-systeem, wordt Hallo gegevens gelijkmatig over Hallo-distributies.  Wanneer gegevens niet gelijkmatig wordt verdeeld, noemen we dit **gegevens tijdverschil**.  

toodivide gegevens gelijkmatig en te voorkomen dat gegevens scheeftrekken, Hallo volgende denken bij het selecteren van de kolom distributie:

1. Selecteer een kolom die een groot aantal afzonderlijke waarden bevat.
2. Vermijd het distribueren van gegevens voor kolommen met een aantal afzonderlijke waarden.
3. Vermijd het distribueren van gegevens voor kolommen met een hoge frequentie van null-waarden.
4. Vermijd het distribueren van gegevens op datumkolommen.

Omdat elke waarde hash too1 van 60 distributies, zelfs distributie tooachieve zult u tooselect een kolom die maximaal uniek is en meer dan 60 unieke waarden bevat.  tooillustrate, een situatie waarin een kolom alleen 40 unieke waarden bevat.  Als deze kolom is geselecteerd als de distributiesleutel hello, zou Hallo-gegevens voor die tabel neerzetten op 40 distributies maximaal 20-distributies die met geen gegevens en geen toodo verwerking.  Als u daarentegen er hello andere 40 distributies meer werk toodo dat als hello gegevens is gelijkmatig verspreid over 60 distributies.  Dit scenario is een voorbeeld van gegevens scheeftrekken.

In de MPP-systeem, elke stap van de query wordt gewacht op alle distributies toocomplete hun aandeel van Hallo werk.  Als een distributiepunt meer werk dan Hallo anderen, wordt de bron van het Hallo Hallo worden andere distributies in wezen NET wachten op Hallo bezet distributie verspild.  Wanneer het werk niet gelijkmatig verdeeld over alle distributies, noemen we dit **verwerking scheeftrekken**.  Verwerking tijdverschil zorgt ervoor dat de query's toorun langzamer dan als Hallo werkbelasting gelijkmatig kan worden verspreid via Hallo-distributies.  Gegevens tijdverschil leidt tooprocessing scheeftrekken.

Vermijd distribueren op maximaal kolom zoals Hallo null-waarden worden alle land op Hallo dezelfde distributie. Distribueren op een datumkolom kan ook worden veroorzaakt verwerking scheeftrekken omdat alle gegevens voor een gegeven datum komt dan uit op Hallo dezelfde distributie. Als het uitvoeren van meerdere gebruikers worden query's alle filteren op Hallo dezelfde datum is, en vervolgens alleen 1 van 60 distributies Hallo al Hallo werk doen gaan aangezien een gegeven datum wordt slechts op één distributiepunt. Hallo-query's in dit scenario wordt waarschijnlijk 60 keer langzamer dan als Hallo gegevens gelijkmatig zijn verdeeld over alle Hallo distributies uitgevoerd.

Als er geen goede kandidaat kolommen bestaan, klikt u vervolgens kunt u overwegen round-robin als Hallo distributiemethode.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Distributiepunten selecteren kolom verplaatsing van gegevens te minimaliseren
Verplaatsing van gegevens voor het minimaliseren Hallo rechts distributie kolom te selecteren, is een van de Hallo belangrijkste strategieën voor het optimaliseren van de prestaties van uw SQL Data Warehouse.  Verplaatsing van gegevens ontstaat meestal als tabellen zijn gekoppeld of aggregaties worden uitgevoerd.  Kolommen die worden gebruikt `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` en `HAVING` componenten alle maken voor **goed** hash-kandidaten voor distributie.

Op Hallo daarentegen kolommen in Hallo `WHERE` component komen **niet** maken voor goede hash-kolom kandidaten omdat zij welke distributies deelnemen Hallo query beperken, waardoor verwerking scheeftrekken.  Een goed voorbeeld van een kolom die mogelijk verleidelijk toodistribute op, maar vaak kan leiden tot deze scheeftrekken verwerking is een datumkolom.

In het algemeen hebt u twee grote feitentabellen vaak die betrokken zijn in een join, krijgt u Hallo meeste prestaties door het distribueren van beide tabellen op een van de Hallo join-kolommen.  Als u een tabel die nooit gekoppelde tooanother grote feitentabel hebt, en zoek vervolgens toocolumns die vaak in Hallo `GROUP BY` component.

Er zijn enkele belangrijke criteria wordt voldaan tooavoid gegevensverplaatsing tijdens een join:

1. Hallo tabellen die zijn betrokken Hallo join moet hash gedistribueerd bij **één** Hallo kolommen die deel uitmaken van Hallo join.
2. Hallo gegevenstypen van Hallo join-kolommen moeten tussen beide tabellen overeenkomen.
3. Hallo-kolommen moeten worden toegevoegd met een operator equals.
4. Hallo jointype niet mogelijk een `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Analytische gegevens scheeftrekken
Wanneer tabelgegevens worden gedistribueerd met behulp van Hallo distributiemethode voor hash-er is vervormd een kans dat een aantal distributies wordt toohave niet goed meer gegevens dan andere. Veel gegevens scheeftrekken kan gevolgen voor queryprestaties omdat Hallo uiteindelijke resultaat van een gedistribueerde query Hallo langste actieve distributie toofinish moet wachten. Afhankelijk van de Hallo mate van Hallo gegevens scheeftrekken dat tooaddress moet u mogelijk het.

### <a name="identifying-skew"></a>Tijdverschil identificeren
Een eenvoudige manier tooidentify een tabel als vervormd is toouse `DBCC PDW_SHOWSPACEUSED`.  Dit is een zeer snelle en eenvoudige manier toosee Hallo aantal rijen die zijn opgeslagen in elk Hallo 60 distributies van uw database.  Houd er rekening mee dat voor de prestaties van de meest met gelijke taakverdeling Hallo Hallo rijen in een gedistribueerde moeten worden gelijkmatig verdeeld over alle Hallo-distributies.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Als u een query hello Azure SQL Data Warehouse dynamische beheerweergaven (DMV) kunt u een meer gedetailleerde analyse uitvoeren.  toostart, Hallo weergave maken [dbo.vTableSizes] [ dbo.vTableSizes] bekijken met behulp van SQL van Hallo [tabel overzicht] [ Overview] artikel.  Zodra Hallo weergave is gemaakt, worden deze query tooidentify welke tabellen meer dan 10% gegevens tijdverschil hebben uitgevoerd.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Het omzetten van gegevens scheeftrekken
Niet alle scheeftrekken is voldoende toowarrant een oplossing.  In sommige gevallen Hallo prestaties van een tabel in sommige query's kan bieden, opwegen tegen Hallo beschadiging van gegevens scheeftrekken.  toodecide als u gegevens moet oplossen scheeftrekken in een tabel, moet u weten zo veel mogelijk over gegevensvolumes Hallo en query's in uw workload.   Eenzijdige toolook op Hallo gevolgen van het tijdverschil is toouse Hallo stappen in Hallo [Query bewaking] [ Query Monitoring] artikel toomonitor Hallo gevolgen van het scheeftrekken op de prestaties van query's en specifiek Hallo impact toohow lange query's toocomplete ondernemen Hallo afzonderlijke distributies.

Distributie van gegevens is een kwestie van het zoeken naar de juiste balans Hallo tussen gegevens tijdverschil minimaliseren en de verplaatsing van gegevens voor het minimaliseren. Deze doelstellingen kunnen tegengestelde en soms is het verstandig tookeep gegevens scheeftrekken in volgorde tooreduce gegevensverplaatsing. Bijvoorbeeld, wanneer de Hallo distributie kolom is vaak Hallo gedeelde kolom in samenvoegingen en aggregaties, zal u worden minimaliseren verplaatsing van gegevens. Hallo voordeel dat de minimale gegevensverplaatsing Hallo kan bieden, opwegen tegen Hallo impact van leiden tot onjuiste gegevens.

de gebruikelijke manier Hallo tooresolve gegevens tijdverschil toore is-Hallo-tabel maken met een ander distributiepunt-kolom. Omdat er geen enkele manier toochange Hallo distributie kolom op een bestaande tabel, Hallo manier toochange Hallo distributie van een tabel deze toorecreate deze met een [CTAS] [].  Hier vindt u twee voorbeelden van hoe u gegevens scheeftrekken oplossen:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Voorbeeld 1: Opnieuw Hallo tabel met een nieuwe kolom voor distributie maken
In dit voorbeeld wordt [CTAS] [] toore-Maak een tabel met een andere hash-distributie-kolom.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Voorbeeld 2: Maak Hallo-tabel met behulp van round robin distributie
In dit voorbeeld wordt [CTAS] [] toore-Maak een tabel met round-robin in plaats van een hash-distributiepunt. Deze wijziging wordt zelfs gegevensdistributie Hallo kosten van de verplaatsing van grotere hoeveelheden gegevens produceren.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het ontwerp van de tabel Zie Hallo [distribueren][Distribute], [Index][Index], [partitie] [ Partition], [Gegevenstypen][Data Types], [statistieken] [ Statistics] en [tijdelijke tabellen] [ Temporary] artikelen.

Zie voor een overzicht van best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
