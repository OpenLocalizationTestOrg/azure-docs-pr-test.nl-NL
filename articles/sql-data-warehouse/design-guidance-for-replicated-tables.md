---
title: Richtlijnen voor gerepliceerde tabellen - Azure SQL Data Warehouse ontwerpen | Microsoft Docs
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
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="f8ac9-103">Richtlijnen voor het gebruik van gerepliceerde tabellen in Azure SQL Data Warehouse ontwerpen</span><span class="sxs-lookup"><span data-stu-id="f8ac9-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f8ac9-104">Dit artikel bevat aanbevelingen voor het ontwerpen van gerepliceerde tabellen in uw SQL Data Warehouse-schema.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="f8ac9-105">Gebruik deze aanbevelingen voor het verbeteren van prestaties van query's door gegevens verplaatsing en query complexiteit te verminderen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="f8ac9-106">De gerepliceerde tabel-functie is momenteel in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="f8ac9-107">Sommige gedragingen nog worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="f8ac9-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f8ac9-108">Prerequisites</span></span>
<span data-ttu-id="f8ac9-109">In dit artikel wordt ervan uitgegaan dat u bekend bent met gegevensdistributie en data movement concepten in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="f8ac9-110">Zie voor meer informatie [gedistribueerd gegevens](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="f8ac9-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="f8ac9-111">Als onderdeel van tabelontwerp begrijpen zo veel mogelijk over uw gegevens en hoe de gegevens wordt opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="f8ac9-112">Neem bijvoorbeeld deze vragen:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-112">For example, consider these questions:</span></span>

- <span data-ttu-id="f8ac9-113">Hoe groot is de tabel?</span><span class="sxs-lookup"><span data-stu-id="f8ac9-113">How large is the table?</span></span>   
- <span data-ttu-id="f8ac9-114">Hoe vaak wordt de tabel vernieuwd</span><span class="sxs-lookup"><span data-stu-id="f8ac9-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="f8ac9-115">Heb ik feiten- en dimensietabellen tabellen in een datawarehouse?</span><span class="sxs-lookup"><span data-stu-id="f8ac9-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="f8ac9-116">Wat is een gerepliceerde tabel?</span><span class="sxs-lookup"><span data-stu-id="f8ac9-116">What is a replicated table?</span></span>
<span data-ttu-id="f8ac9-117">Een gerepliceerde tabel heeft een volledige kopie van de tabel die toegankelijk is op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="f8ac9-118">Bezig met het repliceren van een tabel verwijdert de behoefte om over te dragen van gegevens tussen rekenknooppunten voordat een join of aggregatie.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="f8ac9-119">Aangezien de tabel meerdere exemplaren heeft, gerepliceerde tabellen werken het beste als de grootte van de tabel minder dan 2 GB gecomprimeerd is.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="f8ac9-120">Het volgende diagram toont een gerepliceerde tabel die toegankelijk is op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="f8ac9-121">In SQL Data Warehouse, wordt de gerepliceerde tabel volledig gekopieerd naar een distributiedatabase op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="f8ac9-122">![Gerepliceerde tabel](media/guidance-for-using-replicated-tables/replicated-table.png "gerepliceerde tabel")</span><span class="sxs-lookup"><span data-stu-id="f8ac9-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="f8ac9-123">Gerepliceerde tabellen werk geschikt voor kleine dimensietabellen in een sterschema.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="f8ac9-124">Dimensietabellen zijn meestal met een grootte die het mogelijk voor het opslaan en onderhouden van meerdere exemplaren maakt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="f8ac9-125">Dimensies opslaan beschrijvende gegevens die traag, zoals de naam van de klant en adres en productgegevens wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="f8ac9-126">De langzaam veranderende aard van de gegevens leidt tot de gerepliceerde tabel minder opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="f8ac9-127">Overweeg het gebruik van een gerepliceerde tabel wanneer:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="f8ac9-128">De grootte van de tabel op schijf is minder dan 2 GB vereist, ongeacht het aantal rijen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="f8ac9-129">Als u wilt de grootte van een tabel vinden, kunt u de [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) opdracht: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="f8ac9-130">De tabel wordt gebruikt in samenvoegingen die anders worden verplaatsing van gegevens moeten.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="f8ac9-131">Bijvoorbeeld vereist een join op tabellen hash gedistribueerd gegevensverplaatsing wanneer de kolommen die niet gelijk zijn aan dezelfde kolom van het distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="f8ac9-132">Als een van de tabellen hash gedistribueerd klein is, kunt u een gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="f8ac9-133">Een join op een round robin-tabel vereist de verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="f8ac9-134">U kunt het beste gerepliceerde tabellen in plaats van round robin-tabellen in de meeste gevallen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="f8ac9-135">Houd rekening met het converteren van een bestaande gedistribueerde tabel naar een gerepliceerde tabel wanneer:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="f8ac9-136">Query-gebruik data movement-bewerkingen die de gegevens in de rekenknooppunten uitgezonden plannen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="f8ac9-137">De BroadcastMoveOperation kostbaar en vertraagt queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="f8ac9-138">Als u wilt gegevens movement-bewerkingen in queryplannen bekijkt, gebruik [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="f8ac9-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="f8ac9-139">Gerepliceerde tabellen kunnen niet resulteert in de beste queryprestaties wanneer:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="f8ac9-140">De tabel heeft frequente invoegen, bijwerken en verwijderen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="f8ac9-141">Taal (DML) bestandsbewerkingen van deze gegevens vereist opnieuw opbouwen van de gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="f8ac9-142">Opnieuw opbouwen vaak kan leiden tot lagere prestaties.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="f8ac9-143">Het datawarehouse wordt vaak geschaald.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="f8ac9-144">Het aantal rekenknooppunten, leidt ertoe dat opnieuw opbouwen schalen van een datawarehouse worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="f8ac9-145">De tabel heeft een groot aantal kolommen, maar gegevensbewerkingen gewoonlijk toegang tot een klein aantal kolommen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="f8ac9-146">In dit scenario wordt in plaats van de gehele tabel repliceren mogelijk effectiever op hash distribueren van de tabel en maak vervolgens een index in de veelgebruikte kolommen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="f8ac9-147">Als u een query moet de verplaatsing van gegevens, verplaatst SQL Data Warehouse alleen gegevens in de gevraagde kolommen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="f8ac9-148">Gerepliceerde tabellen gebruiken met eenvoudige query predicaten</span><span class="sxs-lookup"><span data-stu-id="f8ac9-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="f8ac9-149">Voordat u wilt distribueren of een tabel niet repliceren, moet u over de typen query's die u van plan bent om uit te voeren op de tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="f8ac9-150">Indien mogelijk</span><span class="sxs-lookup"><span data-stu-id="f8ac9-150">Whenever possible,</span></span>

- <span data-ttu-id="f8ac9-151">Gerepliceerde tabellen voor query's met eenvoudige query predicaten, zoals gelijkheid of ongelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="f8ac9-152">Gebruik gedistribueerde tabellen voor query's met predicaten voor complexe query's, zoals ACHTIGE of geen wilt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="f8ac9-153">CPU-intensief query's werken het beste als het werk verdeeld over alle van de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="f8ac9-154">Bijvoorbeeld, sneller query's die berekeningen uitgevoerd op elke rij van een tabel op gedistribueerde tabellen dan gerepliceerde tabellen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="f8ac9-155">Omdat een gerepliceerde tabel volledig op elk rekenknooppunt is opgeslagen, wordt een CPU-intensief query op een gerepliceerde tabel uitgevoerd op de gehele tabel op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="f8ac9-156">De extra berekening kan queryprestaties kan afnemen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="f8ac9-157">Deze query heeft bijvoorbeeld een complexe predikaat.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="f8ac9-158">Sneller wanneer leverancier een gedistribueerde tabel in plaats van een gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="f8ac9-159">In dit voorbeeld kan leverancier hash gedistribueerd of round robin gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="f8ac9-160">Bestaande round robin tabellen omzetten in gerepliceerde tabellen</span><span class="sxs-lookup"><span data-stu-id="f8ac9-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="f8ac9-161">Als u al round robin-tabellen, wordt u aangeraden deze te converteren naar gerepliceerde tabellen als ze voldoen aan met de criteria die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="f8ac9-162">Gerepliceerde tabellen de prestaties verbeteren van round robin-tabellen, omdat ze niet meer hoeft te verplaatsen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="f8ac9-163">Een tabel round robin vereist altijd gegevensverplaatsing joins.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="f8ac9-164">In dit voorbeeld wordt [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) te wijzigen van de tabel DimSalesTerritory in een gerepliceerde tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="f8ac9-165">In dit voorbeeld werkt ongeacht of DimSalesTerritory hash gedistribueerd of round robin.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="f8ac9-166">Voorbeeld van de query-prestaties round-robin versus gerepliceerd</span><span class="sxs-lookup"><span data-stu-id="f8ac9-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="f8ac9-167">Een gerepliceerde tabel vereist geen een verplaatsing van gegevens voor samenvoegingen omdat de gehele tabel al aanwezig op elk rekenknooppunt is.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="f8ac9-168">Als de dimensietabellen round robin gedistribueerd, kopieert een join de dimensietabel volledig naar elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="f8ac9-169">Als u wilt de gegevens verplaatst, bevat het queryplan een BroadcastMoveOperation aangeroepen bewerking.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="f8ac9-170">Dit type verplaatsing van gegevens wordt vertraagd prestaties van query's en met behulp van gerepliceerde tabellen wordt geëlimineerd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="f8ac9-171">Als u wilt weergeven van query plan stappen, gebruiken de [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) catalogusweergave systeem.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="f8ac9-172">Bijvoorbeeld, in de volgende query op de AdventureWorks-schema, de ` FactInternetSales` tabel is hash worden verdeeld.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="f8ac9-173">De `DimDate` en `DimSalesTerritory` tabellen zijn kleinere dimensietabellen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="f8ac9-174">Deze query retourneert de totale verkoop in Noord-Amerika voor het fiscale jaar 2004:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="f8ac9-175">We opnieuw gemaakt `DimDate` en `DimSalesTerritory` round robin-tabellen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="f8ac9-176">De query bleek daardoor het volgende queryplan waarvoor meerdere uitzending bewerkingen verplaatsen:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![Round robin queryplan](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="f8ac9-178">We opnieuw gemaakt `DimDate` en `DimSalesTerritory` als in de gerepliceerde tabellen en de query opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="f8ac9-179">Het resulterende queryplan veel korter is en niet hebben een uitzendt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Queryplan gerepliceerd](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="f8ac9-181">Prestatie-overwegingen voor het wijzigen van gerepliceerde tabellen</span><span class="sxs-lookup"><span data-stu-id="f8ac9-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="f8ac9-182">SQL Data Warehouse implementeert een gerepliceerde tabel door het onderhouden van een hoofdversie van de tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="f8ac9-183">De hoofdversie gekopieerd naar een distributiedatabase op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="f8ac9-184">Wanneer er een wijziging is, wordt in SQL Data Warehouse eerst de hoofdtabel bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="f8ac9-185">Klik hiervoor opnieuw opbouwen van de tabellen op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="f8ac9-186">Opnieuw opbouwen van een gerepliceerde tabel bevat de tabel kopiëren naar elk rekenknooppunt en de indexen opnieuw samenstellen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="f8ac9-187">Opnieuw worden opgebouwd zijn vereist is nadat:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="f8ac9-188">Gegevens worden geladen of is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="f8ac9-188">Data is loaded or modified</span></span>
- <span data-ttu-id="f8ac9-189">Het datawarehouse is geschaald naar een andere DWU-instelling</span><span class="sxs-lookup"><span data-stu-id="f8ac9-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="f8ac9-190">Definitie van de tabel wordt bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="f8ac9-190">Table definition is updated</span></span>

<span data-ttu-id="f8ac9-191">Opnieuw worden opgebouwd zijn niet vereist is nadat:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="f8ac9-192">Onderbreken is</span><span class="sxs-lookup"><span data-stu-id="f8ac9-192">Pause operation</span></span>
- <span data-ttu-id="f8ac9-193">Bewerking hervatten</span><span class="sxs-lookup"><span data-stu-id="f8ac9-193">Resume operation</span></span>

<span data-ttu-id="f8ac9-194">Het opnieuw bouwen gebeurt niet onmiddellijk nadat de gegevens worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="f8ac9-195">Het opnieuw bouwen wordt in plaats daarvan de eerste keer dat een query wordt geselecteerd in de tabel geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="f8ac9-196">Zijn de stappen voor het bouwen van de gerepliceerde tabel binnen de eerste select-instructie uit de tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="f8ac9-197">Omdat het opnieuw bouwen binnen de query wordt uitgevoerd, kan impact op de eerste instructie select verwaarloosbaar zijn afhankelijk van de grootte van de tabel zijn.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="f8ac9-198">Als er meerdere gerepliceerde tabellen zijn betrokken die opnieuw opbouwen moeten, wordt elke kopie als de stappen in de instructie opnieuw opeenvolgend opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="f8ac9-199">Als u wilt behouden van gegevens consistentie tijdens het opnieuw opbouwen van de gerepliceerde tabel een exclusieve vergrendeling meegenomen bij de tabel.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="f8ac9-200">De vergrendeling voorkomt alle toegang tot de tabel voor de duur van het opnieuw bouwen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="f8ac9-201">Indexen conservatieve gebruiken</span><span class="sxs-lookup"><span data-stu-id="f8ac9-201">Use indexes conservatively</span></span>
<span data-ttu-id="f8ac9-202">Standaardprocedures indexering van toepassing op gerepliceerde tabellen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="f8ac9-203">SQL Data Warehouse wordt elke gerepliceerde tabelindex als onderdeel van het opnieuw bouwen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="f8ac9-204">Gebruik alleen indexen wanneer de prestatieverbetering belangrijker is dan de kosten van de indexen opnieuw opbouwen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="f8ac9-205">Batch gegevens geladen</span><span class="sxs-lookup"><span data-stu-id="f8ac9-205">Batch data loads</span></span>
<span data-ttu-id="f8ac9-206">Wanneer gegevens in gerepliceerde tabellen te laden, probeer het opnieuw worden opgebouwd minimaliseren door batchverwerking belasting samen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="f8ac9-207">De batch belasting uitvoeren voordat u de select-instructies.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="f8ac9-208">Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen en roept vier opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="f8ac9-209">Laden van bron 1.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-209">Load from source 1.</span></span>
- <span data-ttu-id="f8ac9-210">SELECT-instructie triggers opnieuw opbouwen van 1.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="f8ac9-211">Laden van bron 2.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-211">Load from source 2.</span></span>
- <span data-ttu-id="f8ac9-212">SELECT-instructie triggers opnieuw worden opgebouwd 2.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="f8ac9-213">Laden van bron 3.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-213">Load from source 3.</span></span>
- <span data-ttu-id="f8ac9-214">SELECT-instructie triggers opnieuw opbouwen van 3.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="f8ac9-215">Laden van bron 4.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-215">Load from source 4.</span></span>
- <span data-ttu-id="f8ac9-216">SELECT-instructie triggers 4 opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="f8ac9-217">Bijvoorbeeld, dit patroon load gegevens worden geladen uit vier bronnen, maar roept slechts één opnieuw opbouwen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="f8ac9-218">Laden van bron 1.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-218">Load from source 1.</span></span>
- <span data-ttu-id="f8ac9-219">Laden van bron 2.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-219">Load from source 2.</span></span>
- <span data-ttu-id="f8ac9-220">Laden van bron 3.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-220">Load from source 3.</span></span>
- <span data-ttu-id="f8ac9-221">Laden van bron 4.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-221">Load from source 4.</span></span>
- <span data-ttu-id="f8ac9-222">SELECT-instructie triggers opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="f8ac9-223">Opnieuw samenstellen van een gerepliceerde tabel na een batch-belasting</span><span class="sxs-lookup"><span data-stu-id="f8ac9-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="f8ac9-224">Om ervoor te zorgen uitvoeringstijden consistente query, wordt u aangeraden forceren van een vernieuwing van de gerepliceerde tabellen na een batch-belasting.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="f8ac9-225">Anders wordt moet de eerste query wachten tot de tabellen wilt vernieuwen, waaronder de indexen opnieuw opbouwen.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="f8ac9-226">Afhankelijk van de grootte en een aantal gerepliceerde tabellen die van invloed op zijn de prestatie-invloed verwaarloosbaar.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="f8ac9-227">Deze query gebruikt de [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV voor een lijst met de gerepliceerde tabellen die zijn gewijzigd, maar niet opnieuw opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="f8ac9-228">Als u wilt afdwingen opnieuw opbouwen, voer de volgende instructie voor elke tabel in de bovenstaande uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f8ac9-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="f8ac9-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8ac9-229">Next steps</span></span> 
<span data-ttu-id="f8ac9-230">Gebruik een van deze instructies voor het maken van een gerepliceerde tabel:</span><span class="sxs-lookup"><span data-stu-id="f8ac9-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="f8ac9-231">TABEL (Azure SQL datawarehouse) maken</span><span class="sxs-lookup"><span data-stu-id="f8ac9-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="f8ac9-232">TABLE AS SELECT (Azure SQL datawarehouse maken</span><span class="sxs-lookup"><span data-stu-id="f8ac9-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="f8ac9-233">Zie voor een overzicht van gedistribueerde tabellen [tabellen gedistribueerd](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="f8ac9-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



