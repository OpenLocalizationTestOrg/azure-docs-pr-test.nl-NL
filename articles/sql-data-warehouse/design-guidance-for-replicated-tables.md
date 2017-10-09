---
title: aaaDesign richtlijnen voor gerepliceerde tabellen - Azure SQL Data Warehouse | Microsoft Docs
description: Aanbevelingen voor het ontwerpen van gerepliceerde tabellen in uw Azure SQL Data Warehouse-schema.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Richtlijnen voor het gebruik van gerepliceerde tabellen in Azure SQL Data Warehouse ontwerpen
Dit artikel bevat aanbevelingen voor het ontwerpen van gerepliceerde tabellen in uw SQL Data Warehouse-schema. Gebruik deze aanbevelingen tooimprove query-prestaties door data movement en query complexiteit te verminderen.

> [!NOTE]
> Hallo gerepliceerde tabelfunctie is momenteel in de openbare preview. Sommige gedragingen zijn onderwerp toochange.
> 

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u bekend bent met gegevensdistributie en data movement concepten in SQL Data Warehouse.  Zie voor meer informatie [gedistribueerd gegevens](sql-data-warehouse-distributed-data.md). 

Als onderdeel van tabelontwerp begrijpen zo veel mogelijk over uw gegevens en hoe gegevens hello wordt opgevraagd.  Neem bijvoorbeeld deze vragen:

- Hoe groot is Hallo tabel?   
- Hoe vaak wordt Hallo tabel vernieuwd   
- Heb ik feiten- en dimensietabellen tabellen in een datawarehouse?   

## <a name="what-is-a-replicated-table"></a>Wat is een gerepliceerde tabel?
Een gerepliceerde tabel heeft een volledige kopie van Hallo tabel toegankelijk is op elk rekenknooppunt. Bezig met het repliceren van een tabel, verwijdert Hallo nodig tootransfer gegevens tussen rekenknooppunten voordat een join of aggregatie. Aangezien Hallo tabel meerdere exemplaren heeft, gerepliceerde tabellen werken het beste als Hallo tabelgrootte minder dan 2 GB gecomprimeerd is.

Hallo toont volgende diagram een gerepliceerde tabel die toegankelijk is op elk rekenknooppunt. In SQL Data Warehouse is Hallo gerepliceerde tabel het volledig gekopieerde tooa distributiedatabase op elk rekenknooppunt. 

![Gerepliceerde tabel](media/guidance-for-using-replicated-tables/replicated-table.png "gerepliceerde tabel")  

Gerepliceerde tabellen werk geschikt voor kleine dimensietabellen in een sterschema. Dimensietabellen zijn meestal met een grootte die het mogelijk toostore maakt en onderhouden van meerdere exemplaren. Dimensies opslaan beschrijvende gegevens die traag, zoals de naam van de klant en adres en productgegevens wijzigingen. Hallo langzaam wijzigen van de aard van Hallo gegevens leidt toofewer opnieuw worden opgebouwd van Hallo gerepliceerde tabel. 

Overweeg het gebruik van een gerepliceerde tabel wanneer:

- Hallo tabelgrootte op schijf is minder dan 2 GB vereist, ongeacht het aantal rijen Hallo. toofind hello grootte van een tabel, kunt u Hallo [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) opdracht: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Hallo-tabel wordt in joins die anders worden verplaatsing van gegevens moeten gebruikt. Een join op tabellen hash gedistribueerd is bijvoorbeeld gegevensverplaatsing vereist bij Hallo die kolommen zijn niet Hallo dezelfde kolom van het distributiepunt. Als een van de Hallo gedistribueerd van hash-tabellen klein is, kunt u een gerepliceerde tabel. Een join op een round robin-tabel vereist de verplaatsing van gegevens. U kunt het beste gerepliceerde tabellen in plaats van round robin-tabellen in de meeste gevallen gebruikt. 


Houd rekening met het converteren van een bestaande tabel tooa gerepliceerd gedistribueerd tabel wanneer:

- Query-gebruik data movement-bewerkingen die Hallo gegevens tooall Hallo Compute nodes uitgezonden plannen. Hallo BroadcastMoveOperation kostbaar en vertraagt queryprestaties. tooview data movement-bewerkingen in queryplannen, gebruik [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Gerepliceerde tabellen kunnen niet resulteert in het beste queryprestaties Hallo wanneer:

- Hallo tabel heeft frequente invoegen, bijwerken en verwijderen van bewerkingen. Taal (DML) bestandsbewerkingen van deze gegevens vereist opnieuw opbouwen van Hallo gerepliceerd tabel. Opnieuw opbouwen vaak kan leiden tot lagere prestaties.
- Hallo datawarehouse wordt vaak geschaald. Schalen van een datawarehouse Hallo aantal rekenknooppunten, leidt ertoe dat het opbouwen wordt gewijzigd.
- Hallo tabel heeft een groot aantal kolommen, maar gegevensbewerkingen gewoonlijk toegang tot een klein aantal kolommen. In dit scenario wordt in plaats van de gehele tabel hello, repliceren dit effectiever toohash mogelijk Hallo tabel distribueren en maak vervolgens een index op Hallo veelgebruikte kolommen. Wanneer een query verplaatsing van gegevens, SQL Data Warehouse vereist alleen de gegevens verplaatst in Hallo aangevraagd kolommen. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Gerepliceerde tabellen gebruiken met eenvoudige query predicaten
Voordat u toodistribute kiest of een tabel niet repliceren, moet u Hallo typen query's die u van plan bent toorun tegen Hallo tabel. Indien mogelijk

- Gerepliceerde tabellen voor query's met eenvoudige query predicaten, zoals gelijkheid of ongelijk gebruiken.
- Gebruik gedistribueerde tabellen voor query's met predicaten voor complexe query's, zoals ACHTIGE of geen wilt.

CPU-intensief query's werken het beste als Hallo werk is verdeeld over alle Hallo rekenknooppunten. Bijvoorbeeld, sneller query's die berekeningen uitgevoerd op elke rij van een tabel op gedistribueerde tabellen dan gerepliceerde tabellen. Omdat een gerepliceerde tabel volledig op elk rekenknooppunt is opgeslagen, wordt een CPU-intensief query op een gerepliceerde tabel uitgevoerd op de gehele tabel Hallo op elk rekenknooppunt. Hallo kunt extra berekening trage prestaties van query's.

Deze query heeft bijvoorbeeld een complexe predikaat.  Sneller wanneer leverancier een gedistribueerde tabel in plaats van een gerepliceerde tabel. In dit voorbeeld kan leverancier hash gedistribueerd of round robin gedistribueerd.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Bestaande round robin tabellen tooreplicated tabellen converteren
Als u al round robin tabellen hebt, raden wij omzetten tooreplicated tabellen als ze voldoen aan met de criteria die in dit artikel wordt beschreven. Gerepliceerde tabellen de prestaties verbeteren van round robin-tabellen, omdat ze Hallo nodig voor gegevensverplaatsing elimineren.  Een tabel round robin vereist altijd gegevensverplaatsing joins. 

In dit voorbeeld wordt [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabel tooa gerepliceerde tabel. In dit voorbeeld werkt ongeacht of DimSalesTerritory hash gedistribueerd of round robin.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Voorbeeld van de query-prestaties round-robin versus gerepliceerd 

Een gerepliceerde tabel vereist geen een verplaatsing van gegevens voor samenvoegingen omdat Hallo gehele tabel al aanwezig op elk rekenknooppunt is. Als Hallo dimensietabellen round robin gedistribueerd, kopieert een join Hallo dimensietabel in de volledige tooeach rekenknooppunt. toomove hello gegevens, Hallo queryplan bevat een BroadcastMoveOperation aangeroepen bewerking. Dit type verplaatsing van gegevens wordt vertraagd prestaties van query's en met behulp van gerepliceerde tabellen wordt geëlimineerd. tooview query plan stappen gebruiken Hallo [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) catalogusweergave systeem. 

Bijvoorbeeld, in de volgende query op Hallo AdventureWorks schema Hallo ` FactInternetSales` tabel is hash worden verdeeld. Hallo `DimDate` en `DimSalesTerritory` tabellen zijn kleinere dimensietabellen. Deze query retourneert de totale verkoop Hallo in Noord-Amerika voor het fiscale jaar 2004:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
We opnieuw gemaakt `DimDate` en `DimSalesTerritory` round robin-tabellen. Als gevolg hiervan bleek Hallo query Hallo queryplan waarvoor meerdere uitzending bewerkingen verplaatsen te volgen: 
 
![Round robin queryplan](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

We opnieuw gemaakt `DimDate` en `DimSalesTerritory` als in de gerepliceerde tabellen en Hallo query opnieuw is gestart. de resulterende queryplan Hallo veel korter is en niet hebben een uitzendt verplaatst.

![Queryplan gerepliceerd](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Prestatie-overwegingen voor het wijzigen van gerepliceerde tabellen
SQL Data Warehouse implementeert een gerepliceerde tabel door het onderhouden van een hoofdversie van Hallo tabel. Hallo hoofdversie tooone distributiedatabase op elk rekenknooppunt worden gekopieerd. Wanneer er een wijziging is, wordt in SQL Data Warehouse eerst Hallo hoofdtabel bijgewerkt. Klik hiervoor opnieuw opbouwen van Hallo tabellen op elk rekenknooppunt. Opnieuw opbouwen van een gerepliceerde tabel bevat Hallo tabel tooeach rekenknooppunt kopiëren en opnieuw opbouwen van indexen Hallo.

Opnieuw worden opgebouwd zijn vereist is nadat:
- Gegevens worden geladen of is gewijzigd
- Hallo-datawarehouse is geschaald tooa verschillende DWU-instelling
- Definitie van de tabel wordt bijgewerkt

Opnieuw worden opgebouwd zijn niet vereist is nadat:
- Onderbreken is
- Bewerking hervatten

Hallo rebuild gebeurt niet onmiddellijk nadat de gegevens worden gewijzigd. In plaats daarvan Hallo opnieuw wordt geactiveerd Hallo eerst een query uit Hallo tabel geselecteerd.  Zijn stappen toorebuild Hallo gerepliceerde tabel binnen Hallo initiële select-instructie uit Hallo tabel.  Omdat Hallo rebuild binnen Hallo-query is voltooid, kan Hallo impact toohello initiële select-instructie aanzienlijke, afhankelijk van Hallo grootte van de tabel Hallo worden.  Als er meerdere gerepliceerde tabellen zijn betrokken die opnieuw opbouwen nodig, elk exemplaar opnieuw wordt opgebouwd opeenvolgend als stappen binnen Hallo-instructie.  de gegevensconsistentie toomaintain tijdens het opnieuw opbouwen Hallo Hallo gerepliceerde tabel die een exclusieve vergrendeling bij het Hallo-tabel meegenomen.  Hallo vergrendelen voorkomt u dat alle toegang toohello tabel gedurende Hallo Hallo opnieuw maken. 

### <a name="use-indexes-conservatively"></a>Indexen conservatieve gebruiken
Standaardprocedures indexering toepassing tooreplicated tabellen. SQL Data Warehouse wordt elke gerepliceerde tabelindex als onderdeel van Hallo opnieuw maken. Gebruik alleen indexen wanneer Hallo prestatieverbetering belangrijker is dan Hallo kosten van het Hallo-indexen opnieuw opbouwen.  
 
### <a name="batch-data-loads"></a>Batch gegevens geladen
Wanneer gegevens in gerepliceerde tabellen te laden, probeer toominimize opnieuw worden opgebouwd door belasting samen batchverwerking. Alle Hallo batch verwerkt belasting uitvoeren voordat u de select-instructies.

Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen en roept vier opnieuw worden opgebouwd. 

- Laden van bron 1.
- SELECT-instructie triggers opnieuw opbouwen van 1.
- Laden van bron 2.
- SELECT-instructie triggers opnieuw worden opgebouwd 2.
- Laden van bron 3.
- SELECT-instructie triggers opnieuw opbouwen van 3.
- Laden van bron 4.
- SELECT-instructie triggers 4 opnieuw worden opgebouwd.

Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen, maar roept slechts één opnieuw opbouwen.

- Laden van bron 1.
- Laden van bron 2.
- Laden van bron 3.
- Laden van bron 4.
- SELECT-instructie triggers opnieuw worden opgebouwd.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Opnieuw samenstellen van een gerepliceerde tabel na een batch-belasting
uitvoeringstijden tooensure consistente query, wordt aangeraden een vernieuwing van Hallo gerepliceerde tabellen na een batch-belasting te forceren. De eerste query Hallo moet anders Hallo tabellen toorefresh, waaronder Hallo indexen opnieuw opbouwen wachten. Afhankelijk van Hallo grootte en het aantal gerepliceerde tabellen die van invloed op een zijn prestatie-invloed van Hallo verwaarloosbaar.  

Deze query gebruikt Hallo [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist Hallo gerepliceerde tabellen die zijn gewijzigd, maar niet opnieuw opgebouwd.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce opnieuw opbouwen, uitvoeren van de volgende instructie uit op elke tabel in de voorgaande uitvoer Hallo Hallo. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Volgende stappen 
een gerepliceerde tabel toocreate gebruik een van deze instructies:

- [TABEL (Azure SQL datawarehouse) maken](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [TABLE AS SELECT (Azure SQL datawarehouse maken](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Zie voor een overzicht van gedistribueerde tabellen [tabellen gedistribueerd](sql-data-warehouse-tables-distribute.md).



