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
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="edda2-103">Richtlijnen voor het gebruik van gerepliceerde tabellen in Azure SQL Data Warehouse ontwerpen</span><span class="sxs-lookup"><span data-stu-id="edda2-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="edda2-104">Dit artikel bevat aanbevelingen voor het ontwerpen van gerepliceerde tabellen in uw SQL Data Warehouse-schema.</span><span class="sxs-lookup"><span data-stu-id="edda2-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="edda2-105">Gebruik deze aanbevelingen tooimprove query-prestaties door data movement en query complexiteit te verminderen.</span><span class="sxs-lookup"><span data-stu-id="edda2-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="edda2-106">Hallo gerepliceerde tabelfunctie is momenteel in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="edda2-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="edda2-107">Sommige gedragingen zijn onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="edda2-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="edda2-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edda2-108">Prerequisites</span></span>
<span data-ttu-id="edda2-109">In dit artikel wordt ervan uitgegaan dat u bekend bent met gegevensdistributie en data movement concepten in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edda2-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="edda2-110">Zie voor meer informatie [gedistribueerd gegevens](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="edda2-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="edda2-111">Als onderdeel van tabelontwerp begrijpen zo veel mogelijk over uw gegevens en hoe gegevens hello wordt opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="edda2-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="edda2-112">Neem bijvoorbeeld deze vragen:</span><span class="sxs-lookup"><span data-stu-id="edda2-112">For example, consider these questions:</span></span>

- <span data-ttu-id="edda2-113">Hoe groot is Hallo tabel?</span><span class="sxs-lookup"><span data-stu-id="edda2-113">How large is hello table?</span></span>   
- <span data-ttu-id="edda2-114">Hoe vaak wordt Hallo tabel vernieuwd</span><span class="sxs-lookup"><span data-stu-id="edda2-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="edda2-115">Heb ik feiten- en dimensietabellen tabellen in een datawarehouse?</span><span class="sxs-lookup"><span data-stu-id="edda2-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="edda2-116">Wat is een gerepliceerde tabel?</span><span class="sxs-lookup"><span data-stu-id="edda2-116">What is a replicated table?</span></span>
<span data-ttu-id="edda2-117">Een gerepliceerde tabel heeft een volledige kopie van Hallo tabel toegankelijk is op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="edda2-118">Bezig met het repliceren van een tabel, verwijdert Hallo nodig tootransfer gegevens tussen rekenknooppunten voordat een join of aggregatie.</span><span class="sxs-lookup"><span data-stu-id="edda2-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="edda2-119">Aangezien Hallo tabel meerdere exemplaren heeft, gerepliceerde tabellen werken het beste als Hallo tabelgrootte minder dan 2 GB gecomprimeerd is.</span><span class="sxs-lookup"><span data-stu-id="edda2-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="edda2-120">Hallo toont volgende diagram een gerepliceerde tabel die toegankelijk is op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="edda2-121">In SQL Data Warehouse is Hallo gerepliceerde tabel het volledig gekopieerde tooa distributiedatabase op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="edda2-122">![Gerepliceerde tabel](media/guidance-for-using-replicated-tables/replicated-table.png "gerepliceerde tabel")</span><span class="sxs-lookup"><span data-stu-id="edda2-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="edda2-123">Gerepliceerde tabellen werk geschikt voor kleine dimensietabellen in een sterschema.</span><span class="sxs-lookup"><span data-stu-id="edda2-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="edda2-124">Dimensietabellen zijn meestal met een grootte die het mogelijk toostore maakt en onderhouden van meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="edda2-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="edda2-125">Dimensies opslaan beschrijvende gegevens die traag, zoals de naam van de klant en adres en productgegevens wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="edda2-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="edda2-126">Hallo langzaam wijzigen van de aard van Hallo gegevens leidt toofewer opnieuw worden opgebouwd van Hallo gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="edda2-127">Overweeg het gebruik van een gerepliceerde tabel wanneer:</span><span class="sxs-lookup"><span data-stu-id="edda2-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="edda2-128">Hallo tabelgrootte op schijf is minder dan 2 GB vereist, ongeacht het aantal rijen Hallo.</span><span class="sxs-lookup"><span data-stu-id="edda2-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="edda2-129">toofind hello grootte van een tabel, kunt u Hallo [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) opdracht: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="edda2-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="edda2-130">Hallo-tabel wordt in joins die anders worden verplaatsing van gegevens moeten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="edda2-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="edda2-131">Een join op tabellen hash gedistribueerd is bijvoorbeeld gegevensverplaatsing vereist bij Hallo die kolommen zijn niet Hallo dezelfde kolom van het distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="edda2-132">Als een van de Hallo gedistribueerd van hash-tabellen klein is, kunt u een gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="edda2-133">Een join op een round robin-tabel vereist de verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="edda2-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="edda2-134">U kunt het beste gerepliceerde tabellen in plaats van round robin-tabellen in de meeste gevallen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="edda2-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="edda2-135">Houd rekening met het converteren van een bestaande tabel tooa gerepliceerd gedistribueerd tabel wanneer:</span><span class="sxs-lookup"><span data-stu-id="edda2-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="edda2-136">Query-gebruik data movement-bewerkingen die Hallo gegevens tooall Hallo Compute nodes uitgezonden plannen.</span><span class="sxs-lookup"><span data-stu-id="edda2-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="edda2-137">Hallo BroadcastMoveOperation kostbaar en vertraagt queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="edda2-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="edda2-138">tooview data movement-bewerkingen in queryplannen, gebruik [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="edda2-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="edda2-139">Gerepliceerde tabellen kunnen niet resulteert in het beste queryprestaties Hallo wanneer:</span><span class="sxs-lookup"><span data-stu-id="edda2-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="edda2-140">Hallo tabel heeft frequente invoegen, bijwerken en verwijderen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="edda2-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="edda2-141">Taal (DML) bestandsbewerkingen van deze gegevens vereist opnieuw opbouwen van Hallo gerepliceerd tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="edda2-142">Opnieuw opbouwen vaak kan leiden tot lagere prestaties.</span><span class="sxs-lookup"><span data-stu-id="edda2-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="edda2-143">Hallo datawarehouse wordt vaak geschaald.</span><span class="sxs-lookup"><span data-stu-id="edda2-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="edda2-144">Schalen van een datawarehouse Hallo aantal rekenknooppunten, leidt ertoe dat het opbouwen wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="edda2-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="edda2-145">Hallo tabel heeft een groot aantal kolommen, maar gegevensbewerkingen gewoonlijk toegang tot een klein aantal kolommen.</span><span class="sxs-lookup"><span data-stu-id="edda2-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="edda2-146">In dit scenario wordt in plaats van de gehele tabel hello, repliceren dit effectiever toohash mogelijk Hallo tabel distribueren en maak vervolgens een index op Hallo veelgebruikte kolommen.</span><span class="sxs-lookup"><span data-stu-id="edda2-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="edda2-147">Wanneer een query verplaatsing van gegevens, SQL Data Warehouse vereist alleen de gegevens verplaatst in Hallo aangevraagd kolommen.</span><span class="sxs-lookup"><span data-stu-id="edda2-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="edda2-148">Gerepliceerde tabellen gebruiken met eenvoudige query predicaten</span><span class="sxs-lookup"><span data-stu-id="edda2-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="edda2-149">Voordat u toodistribute kiest of een tabel niet repliceren, moet u Hallo typen query's die u van plan bent toorun tegen Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="edda2-150">Indien mogelijk</span><span class="sxs-lookup"><span data-stu-id="edda2-150">Whenever possible,</span></span>

- <span data-ttu-id="edda2-151">Gerepliceerde tabellen voor query's met eenvoudige query predicaten, zoals gelijkheid of ongelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="edda2-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="edda2-152">Gebruik gedistribueerde tabellen voor query's met predicaten voor complexe query's, zoals ACHTIGE of geen wilt.</span><span class="sxs-lookup"><span data-stu-id="edda2-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="edda2-153">CPU-intensief query's werken het beste als Hallo werk is verdeeld over alle Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="edda2-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="edda2-154">Bijvoorbeeld, sneller query's die berekeningen uitgevoerd op elke rij van een tabel op gedistribueerde tabellen dan gerepliceerde tabellen.</span><span class="sxs-lookup"><span data-stu-id="edda2-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="edda2-155">Omdat een gerepliceerde tabel volledig op elk rekenknooppunt is opgeslagen, wordt een CPU-intensief query op een gerepliceerde tabel uitgevoerd op de gehele tabel Hallo op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="edda2-156">Hallo kunt extra berekening trage prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="edda2-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="edda2-157">Deze query heeft bijvoorbeeld een complexe predikaat.</span><span class="sxs-lookup"><span data-stu-id="edda2-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="edda2-158">Sneller wanneer leverancier een gedistribueerde tabel in plaats van een gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="edda2-159">In dit voorbeeld kan leverancier hash gedistribueerd of round robin gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="edda2-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="edda2-160">Bestaande round robin tabellen tooreplicated tabellen converteren</span><span class="sxs-lookup"><span data-stu-id="edda2-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="edda2-161">Als u al round robin tabellen hebt, raden wij omzetten tooreplicated tabellen als ze voldoen aan met de criteria die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="edda2-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="edda2-162">Gerepliceerde tabellen de prestaties verbeteren van round robin-tabellen, omdat ze Hallo nodig voor gegevensverplaatsing elimineren.</span><span class="sxs-lookup"><span data-stu-id="edda2-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="edda2-163">Een tabel round robin vereist altijd gegevensverplaatsing joins.</span><span class="sxs-lookup"><span data-stu-id="edda2-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="edda2-164">In dit voorbeeld wordt [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabel tooa gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="edda2-165">In dit voorbeeld werkt ongeacht of DimSalesTerritory hash gedistribueerd of round robin.</span><span class="sxs-lookup"><span data-stu-id="edda2-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="edda2-166">Voorbeeld van de query-prestaties round-robin versus gerepliceerd</span><span class="sxs-lookup"><span data-stu-id="edda2-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="edda2-167">Een gerepliceerde tabel vereist geen een verplaatsing van gegevens voor samenvoegingen omdat Hallo gehele tabel al aanwezig op elk rekenknooppunt is.</span><span class="sxs-lookup"><span data-stu-id="edda2-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="edda2-168">Als Hallo dimensietabellen round robin gedistribueerd, kopieert een join Hallo dimensietabel in de volledige tooeach rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="edda2-169">toomove hello gegevens, Hallo queryplan bevat een BroadcastMoveOperation aangeroepen bewerking.</span><span class="sxs-lookup"><span data-stu-id="edda2-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="edda2-170">Dit type verplaatsing van gegevens wordt vertraagd prestaties van query's en met behulp van gerepliceerde tabellen wordt geëlimineerd.</span><span class="sxs-lookup"><span data-stu-id="edda2-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="edda2-171">tooview query plan stappen gebruiken Hallo [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) catalogusweergave systeem.</span><span class="sxs-lookup"><span data-stu-id="edda2-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="edda2-172">Bijvoorbeeld, in de volgende query op Hallo AdventureWorks schema Hallo ` FactInternetSales` tabel is hash worden verdeeld.</span><span class="sxs-lookup"><span data-stu-id="edda2-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="edda2-173">Hallo `DimDate` en `DimSalesTerritory` tabellen zijn kleinere dimensietabellen.</span><span class="sxs-lookup"><span data-stu-id="edda2-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="edda2-174">Deze query retourneert de totale verkoop Hallo in Noord-Amerika voor het fiscale jaar 2004:</span><span class="sxs-lookup"><span data-stu-id="edda2-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="edda2-175">We opnieuw gemaakt `DimDate` en `DimSalesTerritory` round robin-tabellen.</span><span class="sxs-lookup"><span data-stu-id="edda2-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="edda2-176">Als gevolg hiervan bleek Hallo query Hallo queryplan waarvoor meerdere uitzending bewerkingen verplaatsen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edda2-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Round robin queryplan](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="edda2-178">We opnieuw gemaakt `DimDate` en `DimSalesTerritory` als in de gerepliceerde tabellen en Hallo query opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="edda2-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="edda2-179">de resulterende queryplan Hallo veel korter is en niet hebben een uitzendt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="edda2-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Queryplan gerepliceerd](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="edda2-181">Prestatie-overwegingen voor het wijzigen van gerepliceerde tabellen</span><span class="sxs-lookup"><span data-stu-id="edda2-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="edda2-182">SQL Data Warehouse implementeert een gerepliceerde tabel door het onderhouden van een hoofdversie van Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="edda2-183">Hallo hoofdversie tooone distributiedatabase op elk rekenknooppunt worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="edda2-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="edda2-184">Wanneer er een wijziging is, wordt in SQL Data Warehouse eerst Hallo hoofdtabel bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="edda2-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="edda2-185">Klik hiervoor opnieuw opbouwen van Hallo tabellen op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="edda2-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="edda2-186">Opnieuw opbouwen van een gerepliceerde tabel bevat Hallo tabel tooeach rekenknooppunt kopiëren en opnieuw opbouwen van indexen Hallo.</span><span class="sxs-lookup"><span data-stu-id="edda2-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="edda2-187">Opnieuw worden opgebouwd zijn vereist is nadat:</span><span class="sxs-lookup"><span data-stu-id="edda2-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="edda2-188">Gegevens worden geladen of is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="edda2-188">Data is loaded or modified</span></span>
- <span data-ttu-id="edda2-189">Hallo-datawarehouse is geschaald tooa verschillende DWU-instelling</span><span class="sxs-lookup"><span data-stu-id="edda2-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="edda2-190">Definitie van de tabel wordt bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="edda2-190">Table definition is updated</span></span>

<span data-ttu-id="edda2-191">Opnieuw worden opgebouwd zijn niet vereist is nadat:</span><span class="sxs-lookup"><span data-stu-id="edda2-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="edda2-192">Onderbreken is</span><span class="sxs-lookup"><span data-stu-id="edda2-192">Pause operation</span></span>
- <span data-ttu-id="edda2-193">Bewerking hervatten</span><span class="sxs-lookup"><span data-stu-id="edda2-193">Resume operation</span></span>

<span data-ttu-id="edda2-194">Hallo rebuild gebeurt niet onmiddellijk nadat de gegevens worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="edda2-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="edda2-195">In plaats daarvan Hallo opnieuw wordt geactiveerd Hallo eerst een query uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="edda2-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="edda2-196">Zijn stappen toorebuild Hallo gerepliceerde tabel binnen Hallo initiële select-instructie uit Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="edda2-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="edda2-197">Omdat Hallo rebuild binnen Hallo-query is voltooid, kan Hallo impact toohello initiële select-instructie aanzienlijke, afhankelijk van Hallo grootte van de tabel Hallo worden.</span><span class="sxs-lookup"><span data-stu-id="edda2-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="edda2-198">Als er meerdere gerepliceerde tabellen zijn betrokken die opnieuw opbouwen nodig, elk exemplaar opnieuw wordt opgebouwd opeenvolgend als stappen binnen Hallo-instructie.</span><span class="sxs-lookup"><span data-stu-id="edda2-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="edda2-199">de gegevensconsistentie toomaintain tijdens het opnieuw opbouwen Hallo Hallo gerepliceerde tabel die een exclusieve vergrendeling bij het Hallo-tabel meegenomen.</span><span class="sxs-lookup"><span data-stu-id="edda2-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="edda2-200">Hallo vergrendelen voorkomt u dat alle toegang toohello tabel gedurende Hallo Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="edda2-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="edda2-201">Indexen conservatieve gebruiken</span><span class="sxs-lookup"><span data-stu-id="edda2-201">Use indexes conservatively</span></span>
<span data-ttu-id="edda2-202">Standaardprocedures indexering toepassing tooreplicated tabellen.</span><span class="sxs-lookup"><span data-stu-id="edda2-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="edda2-203">SQL Data Warehouse wordt elke gerepliceerde tabelindex als onderdeel van Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="edda2-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="edda2-204">Gebruik alleen indexen wanneer Hallo prestatieverbetering belangrijker is dan Hallo kosten van het Hallo-indexen opnieuw opbouwen.</span><span class="sxs-lookup"><span data-stu-id="edda2-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="edda2-205">Batch gegevens geladen</span><span class="sxs-lookup"><span data-stu-id="edda2-205">Batch data loads</span></span>
<span data-ttu-id="edda2-206">Wanneer gegevens in gerepliceerde tabellen te laden, probeer toominimize opnieuw worden opgebouwd door belasting samen batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="edda2-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="edda2-207">Alle Hallo batch verwerkt belasting uitvoeren voordat u de select-instructies.</span><span class="sxs-lookup"><span data-stu-id="edda2-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="edda2-208">Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen en roept vier opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="edda2-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="edda2-209">Laden van bron 1.</span><span class="sxs-lookup"><span data-stu-id="edda2-209">Load from source 1.</span></span>
- <span data-ttu-id="edda2-210">SELECT-instructie triggers opnieuw opbouwen van 1.</span><span class="sxs-lookup"><span data-stu-id="edda2-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="edda2-211">Laden van bron 2.</span><span class="sxs-lookup"><span data-stu-id="edda2-211">Load from source 2.</span></span>
- <span data-ttu-id="edda2-212">SELECT-instructie triggers opnieuw worden opgebouwd 2.</span><span class="sxs-lookup"><span data-stu-id="edda2-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="edda2-213">Laden van bron 3.</span><span class="sxs-lookup"><span data-stu-id="edda2-213">Load from source 3.</span></span>
- <span data-ttu-id="edda2-214">SELECT-instructie triggers opnieuw opbouwen van 3.</span><span class="sxs-lookup"><span data-stu-id="edda2-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="edda2-215">Laden van bron 4.</span><span class="sxs-lookup"><span data-stu-id="edda2-215">Load from source 4.</span></span>
- <span data-ttu-id="edda2-216">SELECT-instructie triggers 4 opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="edda2-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="edda2-217">Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen, maar roept slechts één opnieuw opbouwen.</span><span class="sxs-lookup"><span data-stu-id="edda2-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="edda2-218">Laden van bron 1.</span><span class="sxs-lookup"><span data-stu-id="edda2-218">Load from source 1.</span></span>
- <span data-ttu-id="edda2-219">Laden van bron 2.</span><span class="sxs-lookup"><span data-stu-id="edda2-219">Load from source 2.</span></span>
- <span data-ttu-id="edda2-220">Laden van bron 3.</span><span class="sxs-lookup"><span data-stu-id="edda2-220">Load from source 3.</span></span>
- <span data-ttu-id="edda2-221">Laden van bron 4.</span><span class="sxs-lookup"><span data-stu-id="edda2-221">Load from source 4.</span></span>
- <span data-ttu-id="edda2-222">SELECT-instructie triggers opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="edda2-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="edda2-223">Opnieuw samenstellen van een gerepliceerde tabel na een batch-belasting</span><span class="sxs-lookup"><span data-stu-id="edda2-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="edda2-224">uitvoeringstijden tooensure consistente query, wordt aangeraden een vernieuwing van Hallo gerepliceerde tabellen na een batch-belasting te forceren.</span><span class="sxs-lookup"><span data-stu-id="edda2-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="edda2-225">De eerste query Hallo moet anders Hallo tabellen toorefresh, waaronder Hallo indexen opnieuw opbouwen wachten.</span><span class="sxs-lookup"><span data-stu-id="edda2-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="edda2-226">Afhankelijk van Hallo grootte en het aantal gerepliceerde tabellen die van invloed op een zijn prestatie-invloed van Hallo verwaarloosbaar.</span><span class="sxs-lookup"><span data-stu-id="edda2-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="edda2-227">Deze query gebruikt Hallo [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist Hallo gerepliceerde tabellen die zijn gewijzigd, maar niet opnieuw opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="edda2-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="edda2-228">tooforce opnieuw opbouwen, uitvoeren van de volgende instructie uit op elke tabel in de voorgaande uitvoer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="edda2-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="edda2-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edda2-229">Next steps</span></span> 
<span data-ttu-id="edda2-230">een gerepliceerde tabel toocreate gebruik een van deze instructies:</span><span class="sxs-lookup"><span data-stu-id="edda2-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="edda2-231">TABEL (Azure SQL datawarehouse) maken</span><span class="sxs-lookup"><span data-stu-id="edda2-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="edda2-232">TABLE AS SELECT (Azure SQL datawarehouse maken</span><span class="sxs-lookup"><span data-stu-id="edda2-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="edda2-233">Zie voor een overzicht van gedistribueerde tabellen [tabellen gedistribueerd](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="edda2-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



