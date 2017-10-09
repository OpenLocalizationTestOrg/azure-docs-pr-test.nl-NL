---
title: aaaIndexing tabellen in SQL Data Warehouse | Microsoft Azure
description: Aan de slag met de tabel in Azure SQL Data Warehouse te indexeren.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indexeren van tabellen in SQL Data Warehouse
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

SQL Data Warehouse biedt verschillende opties voor indexeren inclusief [geclusterde kolomopslagindexen][clustered columnstore indexes], [geclusterde indexen en niet-geclusterde indexen][clustered indexes and nonclustered indexes].  Bovendien biedt ook een geen indexoptie ook wel bekend als [heap][heap].  In dit artikel bevat informatie over de voordelen van elk indextype Hallo evenals tips toogetting Hallo meeste prestaties buiten uw indexen. Zie [maken tabelsyntaxis] [ create table syntax] voor meer informatie over het toocreate een tabel in SQL Data Warehouse.

## <a name="clustered-columnstore-indexes"></a>Geclusterde columnstore-indexen
SQL Data Warehouse maakt standaard een geclusterde columnstore-index wanneer er geen indexopties voor zijn opgegeven in een tabel. De geclusterde columnstore-tabellen bieden beide Hallo hoogste niveau van gegevenscompressie, evenals Hallo beste algehele prestaties van query's.  Geclusterde columnstore-tabellen wordt doorgaans leveren betere prestaties dan geclusterde index of heap tabellen en zijn doorgaans de beste keuze Hallo voor grote tabellen.  Daarom geclusterde columnstore is de beste plaats toostart Hallo wanneer u hoe weet tooindex uw tabel.  

toocreate een geclusterde columnstore-tabel simpelweg GECLUSTERDE COLUMNSTORE-INDEX opgeven in de component WITH Hallo of laat u de component WITH Hallo uitgeschakeld:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Er zijn enkele scenario's waar de geclusterde columnstore niet mogelijk een goede optie:

* Columnstore-tabellen ondersteunen geen varchar(max), nvarchar(max) en varbinary(max).  Overweeg in plaats daarvan heap of geclusterde index.
* Columnstore-tabellen zijn mogelijk minder efficiënt voor tijdelijke gegevens.  U kunt heap en kan zelfs tijdelijke tabellen.
* Kleine tabellen met minder dan 100 miljoen rijen.  Houd rekening met heap tabellen.

## <a name="heap-tables"></a>Heap tabellen
Wanneer u zijn tijdelijk gegevens in SQL Data Warehouse aanvoer, kan het gebeuren dat met behulp van een tabel heap zal maken Hallo algehele proces sneller.  Dit is omdat de belasting tooheaps sneller dan tooindex tabellen zijn en in sommige gevallen Hallo lezen uit cache kan worden gedaan.  Als u laadt gegevens alleen toostage voordat u meer transformaties bij het laden van de tabel tooheap Hallo moeten veel sneller dan bij het laden van Hallo gegevens tooa de geclusterde columnstore-tabel. Bovendien tijdens het laden van gegevens tooa [tijdelijke tabel] [ Temporary] ook veel sneller dan bij het laden van een tabel toopermanent opslag wordt geladen.  

Voor kleine opzoektabellen, kleiner dan 100 miljoen rijen, zinvol vaak heap tabellen zijn.  Cluster columnstore-tabellen beginnen tooachieve optimale compressie zodra er meer dan 100 miljoen rijen.

HEAP toocreate een tabel heap gewoon opgeven in de component WITH Hallo:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Geclusterde en niet-geclusterde indexen
Geclusterde indexen kunnen geclusterde columnstore-tabellen beter wanneer één rij toobe snel opgehaald moet.  Voor query's waarin één of een heel weinig rij lookup vereist tooperformance met extreme snelheid is, kunt u een clusterindex of niet-geclusterde index van de secundaire.  Hallo nadeel toousing een geclusterde index is dat er alleen query's die het gebruik van een maximaal selectief filter op Hallo geclusterde indexkolom profiteert.  tooimprove filter van andere kolommen, die een niet-geclusterde index kan worden toegevoegd tooother kolommen.  Elke index die is toegevoegd tooa tabel wordt echter ruimte en verwerken van tijd tooloads toevoegen.

GECLUSTERDE INDEX toocreate een tabel geclusterde index gewoon opgeven in de component WITH Hallo:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd een niet-geclusterde index in een tabel, gebruikt u gewoon Hallo syntaxis:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Geclusterde columnstore-indexen optimaliseren
De geclusterde columnstore-tabellen zijn ingedeeld in de gegevens in segmenten.  Een hoge segment goede is kritieke tooachieving optimale query-prestaties op een columnstore-tabel.  Segment kwaliteit kan worden bepaald door het aantal rijen in een rijgroep gecomprimeerde Hallo.  Segment kwaliteit is optimale wanneer er ten minste 100K rijen per rij gecomprimeerde groeperen en krijgen in prestaties als Hallo aantal rijen per rij groep benadering 1.048.576 rijen, namelijk Hallo meeste rijen in die een rijgroep kan bevatten.

Hallo hieronder weergave kan worden gemaakt en gebruikt op uw systeem toocompute Hallo gemiddelde rijen per rij groeperen en een columnstore-indexen suboptimale cluster identificeren.  Hallo laatste kolom in deze weergave worden de indexen als SQL-instructie die gebruikt toorebuild kan worden gegenereerd.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Nu dat u hebt gemaakt Hallo weergave, voer dan deze query tooidentify tabellen met Rijgroepen met minder dan 100K rijen.  U kunt tooincrease Hallo drempelwaarde van 100K natuurlijk als u meer optimale segment kwaliteit zoekt. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Zodra u Hallo query hebt uitgevoerd kunt u beginnen toolook Hallo gegevens en analyseer de resultaten. Deze tabel wordt uitgelegd welke toolook voor in uw groep rij analyse.

| Kolom | Hoe toouse deze gegevens |
| --- | --- |
| [table_partition_count] |Als Hallo-tabel is gepartitioneerd, kunt u toosee hogere Open groep Rijtellingen kan verwachten. Elke partitie in Hallo distributie kan in theorie een open rijgroep gekoppeld hebben. Dit factor in uw analyse. Een kleine tabel die is is gepartitioneerd kan worden geoptimaliseerd door het verwijderen van Hallo helemaal partitioneren, omdat dit zou leiden tot betere compressie. |
| [row_count_total] |Totale aantal rijen voor Hallo tabel. Bijvoorbeeld, kunt u dit percentage waarde toocalculate rijen Hallo gecomprimeerd status. |
| [row_count_per_distribution_MAX] |Als alle rijen gelijkmatig worden verdeeld deze waarde wordt Hallo doelaantal rijen per distributiepunt. Deze waarde met de Hallo compressed_rowgroup_count vergelijken. |
| [COMPRESSED_rowgroup_rows] |Totale aantal rijen in de indeling voor de tabel Hallo columnstore. |
| [COMPRESSED_rowgroup_rows_AVG] |Als Hallo kunt u het gemiddelde aantal rijen aanzienlijk minder dan hello maximale aantal rijen voor een rijgroep is, kunt u overwegen CTAS of ALTER INDEX REBUILD toorecompress Hallo gegevens |
| [COMPRESSED_rowgroup_count] |Het aantal Rijgroepen columnstore-indeling. Als dit aantal zeer hoog in de tabel toohello relatie is is een indicator Hallo columnstore dichtheid is laag. |
| [COMPRESSED_rowgroup_rows_DELETED] |Rijen zijn logisch in columnstore-indeling verwijderd. Hallo nummer hoge relatieve tootable grootte, dan kunt u Hallo partitie opnieuw te maken of opnieuw opbouwen van Hallo index Hiermee verwijdert u deze fysiek. |
| [COMPRESSED_rowgroup_rows_MIN] |Gebruik dit in combinatie met Hallo AVG en MAX kolommen toounderstand Hallo bereik van waarden voor Hallo Rijgroepen in uw columnstore. Een lage waarde boven de drempelwaarde voor Hallo laden (102,400 per partitie uitgelijnd distributie) wordt voorgesteld dat optimalisaties beschikbaar in Hallo gegevens laden zijn |
| [COMPRESSED_rowgroup_rows_MAX] |Hierboven |
| [OPEN_rowgroup_count] |Open Rijgroepen is normaal. Een verwachten redelijkerwijs één OPEN rijgroep per tabeldistributie (60). Overmatige cijfers voorgesteld meerdere partities het laden van gegevens. Controleer Hallo strategie toomake ervoor dat dit goed partitioneren |
| [OPEN_rowgroup_rows] |Elke rijgroep kan deze als maximaal 1.048.576 rijen hebben. Gebruik deze waarde toosee hoe vol Hallo open Rijgroepen momenteel |
| [OPEN_rowgroup_rows_MIN] |Groepen openen geven aan dat gegevens op in de tabel Hallo nieuwe wordt geladen of die Hallo vorige load overige rijen in deze rijgroep overgeslagen. Gebruik hello, MIN, MAX, AVG kolommen toosee hoeveel gegevens in geopende Rijgroepen is zat. Voor kleine tabellen wordt 100% van alle gegevens van Hallo! In dat geval Hallo ALTER INDEX REBUILD tooforce toocolumnstore gegevens. |
| [OPEN_rowgroup_rows_MAX] |Hierboven |
| [OPEN_rowgroup_rows_AVG] |Hierboven |
| [CLOSED_rowgroup_rows] |Bekijkt hello gesloten rij groep rijen als een controle. |
| [CLOSED_rowgroup_count] |Hallo aantal gesloten Rijgroepen moet laag als een helemaal zijn zichtbaar zijn. Gesloten Rijgroepen mag geconverteerde toocompressed rowg roups Hallo ALTER INDEX met... REORGANISATIE opdracht. Dit is echter niet normaal gesproken vereist. Gesloten groepen zijn automatisch geconverteerd toocolumnstore Rijgroepen door Hallo 'tuple mover' achtergrondproces. |
| [CLOSED_rowgroup_rows_MIN] |Gesloten Rijgroepen moeten een zeer hoge opvulling snelheid hebben. Als percentage van de Hallo opvulling voor een rijgroep gesloten laag is, zijn verdere analyse van Hallo columnstore is vereist. |
| [CLOSED_rowgroup_rows_MAX] |Hierboven |
| [CLOSED_rowgroup_rows_AVG] |Hierboven |
| [Rebuild_Index_SQL] |SQL toorebuild columnstore-index voor een tabel |

## <a name="causes-of-poor-columnstore-index-quality"></a>Oorzaken van slechte columnstore-index kwaliteit
Als u tabellen hebt geïdentificeerd met slechte segment kwaliteit, zult u tooidentify Hallo hoofdoorzaak.  Hieronder vindt u enkele veelvoorkomende oorzaken van slechte segment quaility:

1. Geheugendruk wanneer de index is samengesteld.
2. Groot aantal DML-bewerkingen
3. Kleine of load-bewerkingen doorsijpelen
4. Te veel partities

Deze factoren kunnen leiden tot een columnstore-index toohave aanzienlijk minder dan optimale 1 miljoen rijen per rijgroep Hallo.  Ze kunnen ook rijen toogo toohello delta rijgroep in plaats van een rijgroep gecomprimeerde veroorzaken. 

### <a name="memory-pressure-when-index-was-built"></a>Geheugendruk wanneer de index is samengesteld.
Hallo aantal rijen per rijgroep gecomprimeerde zijn direct gerelateerd toohello breedte van Hallo rij en hoeveelheid geheugen beschikbaar tooprocess rijgroep Hallo Hallo.  Wanneer rijen toocolumnstore tabellen onder geheugendruk geschreven worden, oplopen columnstore segment kwaliteit.  Hallo aanbevolen procedure is daarom toogive Hallo-sessie die is schrijven tooyour columnstore-index tabellen tooas toegang tot veel geheugen mogelijk.  Omdat er een compromis tussen geheugen en gelijktijdigheid, kunt Hallo richtlijnen op de juiste toewijzing is afhankelijk van gegevens in elke rij van de tabel, de hoeveelheid DWU Hallo Hallo u geheugen tooyour system hebt toegewezen en Hallo hoeveelheid gelijktijdigheid sleuven u Hallo toohello geven de sessie die is tooyour gegevenstabel schrijven.  Als een best practice is het raadzaam met xlargerc als u van DW300 gebruikmaakt of minder largerc starten als u DW400 tooDW600 en mediumrc als u van DW1000 gebruikmaakt en hoger.

### <a name="high-volume-of-dml-operations"></a>Groot aantal DML-bewerkingen
Een groot aantal DML-bewerkingen die bijwerken en verwijderen van rijen kunt inefficiëntie in Hallo columnstore introduceren. Dit geldt vooral als Hallo meerderheid van Hallo rijen in de rijgroep van een worden gewijzigd.

* Verwijderen van een rij uit een rijgroep gecomprimeerde alleen logisch Hallo rij worden gemarkeerd als verwijderd. Hallo rij blijft in de gecomprimeerde rijgroep Hallo totdat Hallo partitie of de tabel opnieuw wordt opgebouwd.
* Invoegen van een rij wordt Hallo rij tootooan interne rowstore tabel met de naam van een rij delta groep toegevoegd. Hallo ingevoegd rij is niet geconverteerd toocolumnstore totdat Hallo delta rijgroep vol is en is gemarkeerd als gesloten. Rijgroepen worden gesloten nadat deze Hallo maximale capaciteit van 1.048.576 rijen bereiken. 
* Bijwerken van een rij in de columnstore-indeling wordt verwerkt als een logische verwijderen en vervolgens een INSERT-bewerking. Hallo ingevoegd rij kan worden opgeslagen in Hallo delta-archief.

Update batch verwerkt en voeg de bewerkingen die de drempelwaarde Hallo bulksgewijs 102.400 rijen per partitie uitgelijnde distributie overschrijdt direct toohello columnstore opmaken worden geschreven. Echter, ervan uitgaande dat een gelijkmatige verdeling, moet u toobe meer dan 6.144 miljoen rijen in één bewerking voor deze toooccur wijzigen. Als het aantal rijen voor een bepaalde partitie Hallo uitgelijnd distributie is minder dan 102,400 Hallo rijen toohello delta store gaat en er blijven totdat voldoende rijen zijn ingevoegd of gewijzigde tooclose Hallo rij groep of Hallo-index is opnieuw opgebouwd.

### <a name="small-or-trickle-load-operations"></a>Kleine of load-bewerkingen doorsijpelen
Kleine wordt geladen dat stroom in SQL Data Warehouse worden soms ook wel doorsijpelen laadt. Ze vertegenwoordigen meestal een nabije constante stream met gegevens die wordt ingenomen door Hallo-systeem. Omdat deze stroom in de buurt van wordt is continue Hallo volume van rijen echter niet bijzonder groot. Hallo-gegevens zijn vaak aanzienlijk onder de drempelwaarde van Hallo vereist is voor een directe load toocolumnstore-indeling.

In deze gevallen is vaak beter tooland Hallo gegevens eerst in Azure blob-opslag en laat het verzamelen van eerdere tooloading. Deze techniek is vaak bekend als *micro batchverwerking*.

### <a name="too-many-partitions"></a>Te veel partities
Een andere ding tooconsider is Hallo gevolgen van het partitioneren van uw geclusterde columnstore-tabellen.  Voordat het partitioneren verdeelt SQL Data Warehouse al uw gegevens in 60 databases.  Partitioneren van verdeelt uw gegevens verder.  Als u uw gegevens partitioneren, dan u tooconsider zult die **elke** partitie moet toohave ten minste 1 miljoen rijen toobenefit van een geclusterde columnstore-index.  Als u de tabel in 100 partities partitioneren, moet uw tabel toohave ten minste 6 miljard rijen toobenefit van een geclusterde columnstore-index (60 distributies * 100 partities * 1 miljoen rijen). Als uw 100 partitietabel geen 6 miljard rijen Verminder het aantal partities Hallo of gebruik in plaats hiervan een heap-tabel.

Zodra de tabellen met enkele gegevens zijn geladen, volg Hallo onderstaande stappen tooidentify en tabellen met columnstore-indexen suboptimale cluster opnieuw maken.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Opnieuw opbouwen van indexen tooimprove segment kwaliteit
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Stap 1: Identificeren of gebruiker dat gebruikmaakt van de juiste bronklasse Hallo maken
Een snelle manier tooimmediately segment kwaliteitsverbetering is toorebuild Hallo index.  Hallo SQL geretourneerd door Hallo boven weergave wordt geretourneerd van een instructie ALTER INDEX REBUILD die gebruikt toorebuild worden kan uw indexen.  Wanneer uw indexen opnieuw opbouwen, zorg er dan voor dat voldoende geheugen toohello-sessie die uw index wordt opnieuw toe te wijzen.  toodo deze, toename Hallo bronklasse van een gebruiker met machtigingen toorebuild Hallo index op deze tabel toohello aanbevolen minimum.  De bronklasse Hallo van Hallo eigenaar databasegebruiker kan niet worden gewijzigd, dus als u een gebruiker op Hallo systeem niet hebt gemaakt, u toodo dus eerst moet.  Hallo minimum aangeraden is xlargerc als u van DW300 gebruikmaakt of minder largerc als u DW400 tooDW600 en mediumrc als u van DW1000 gebruikmaakt en hoger.

Hieronder volgt een voorbeeld van hoe tooallocate meer geheugen tooa gebruiker doordat hun bronklasse.  Voor meer informatie over de resource-klassen en hoe toocreate een nieuwe gebruiker kunt u vinden in Hallo [gelijktijdigheid en werkbelasting management] [ Concurrency] artikel.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Stap 2: De geclusterde columnstore-indexen opnieuw samenstellen met hogere resource klasse gebruiker
Aanmelden als Hallo gebruiker uit stap 1 (bijvoorbeeld LoadUser), die wordt nu gebruikt een hogere bronklasse en Hallo ALTER INDEX instructies uitvoeren.  Zorg ervoor dat deze gebruiker heeft ALTER machtiging toohello tabellen waarbij Hallo index wordt opnieuw opgebouwd.  Deze voorbeelden laten zien hoe toorebuild Hallo volledige columnstore-index en hoe toorebuild één partitie. Op grote tabellen is het praktischer toorebuild indexen één partitie op een tijdstip.

In plaats van het Hallo-index bouwen, u ook kan kopiëren Hallo tabel tooa nieuwe tabel via [CTAS][CTAS].  Welke het beste is? Voor grote hoeveelheden gegevens, [CTAS] [ CTAS] is doorgaans sneller dan [ALTER INDEX][ALTER INDEX]. Voor kleinere volumes van gegevens, [ALTER INDEX] [ ALTER INDEX] is eenvoudiger toouse en tooswap uit de tabel Hallo won't vereisen.  Zie **opnieuw opbouwen van indexen met CTAS en partitie overschakelingen** hieronder voor meer informatie over hoe toorebuild met CTAS geïndexeerd.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

Opnieuw opbouwen van een index in SQL Data Warehouse is een offline bewerking.  Zie voor meer informatie over het opnieuw opbouwen van indexen, Hallo ALTER INDEX REBUILD-sectie in [Columnstore-indexen defragmentatie] [ Columnstore Indexes Defragmentation] Hallo syntaxis onderwerp en [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Stap 3: Controleren of de kwaliteit van de geclusterde columnstore-segment is verbeterd
Voer Hallo query die tabel geïdentificeerd met slecht segmenteren kwaliteit en controleer of segment kwaliteit is verbeterd.  Als het segment kwaliteit kon niet worden verbeterd, kan het zijn dat Hallo rijen in de tabel extra breed zijn.  Overweeg het gebruik van een hogere bronklasse of DWU wanneer uw indexen opnieuw opbouwen.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Opnieuw opbouwen van indexen met CTAS en partitie overschakelen
In dit voorbeeld wordt [CTAS] [ CTAS] en partitie toorebuild een partitie van tabel overschakelen. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
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
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
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
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Voor meer informatie over het opnieuw maken met behulp van partities `CTAS`, Zie Hallo [partitie] [ Partition] artikel.

## <a name="next-steps"></a>Volgende stappen
toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Partitioneren van een tabel][Partition], [tabelstatistieken onderhouden] [ Statistics] en [ Tijdelijke tabellen][Temporary].  Zie toolearn meer informatie over aanbevolen procedures [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
