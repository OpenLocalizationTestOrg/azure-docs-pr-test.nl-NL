---
title: aaaGuide voor het gebruik van PolyBase in SQL Data Warehouse | Microsoft Docs
description: Richtlijnen en aanbevelingen voor het gebruik van PolyBase in SQL Data Warehouse-scenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="0cb76-103">Handleiding voor het gebruik van PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0cb76-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="0cb76-104">Deze handleiding biedt praktische informatie voor het gebruik van PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0cb76-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="0cb76-105">tooget gestart, Zie Hallo [gegevens laden met PolyBase] [ Load data with PolyBase] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0cb76-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="0cb76-106">Opslagsleutels draaien</span><span class="sxs-lookup"><span data-stu-id="0cb76-106">Rotating storage keys</span></span>
<span data-ttu-id="0cb76-107">Van tijd tootime zult u om veiligheidsredenen toochange Hallo toegang sleutel tooyour blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="0cb76-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="0cb76-108">Hallo meest elegante manier tooperform die deze taak een proces genaamd is 'hello sleutels roteren' toofollow.</span><span class="sxs-lookup"><span data-stu-id="0cb76-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="0cb76-109">U mogelijk opgevallen dat er twee opslagsleutels voor blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="0cb76-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="0cb76-110">Dit is zodat kunt u overstappen</span><span class="sxs-lookup"><span data-stu-id="0cb76-110">This is so that you can transition</span></span>

<span data-ttu-id="0cb76-111">Roteren van uw sleutels van Azure storage-account is een proces eenvoudige drie stappen</span><span class="sxs-lookup"><span data-stu-id="0cb76-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="0cb76-112">Tweede-scoped databasereferentie op basis van de toegangssleutel voor Hallo secundaire opslag maken</span><span class="sxs-lookup"><span data-stu-id="0cb76-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="0cb76-113">Tweede externe gegevensbron gebaseerd op deze nieuwe referentie maken</span><span class="sxs-lookup"><span data-stu-id="0cb76-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="0cb76-114">Verwijderen en Hallo externe tabel(len) toohello nieuwe externe gegevensbron wijzen maken</span><span class="sxs-lookup"><span data-stu-id="0cb76-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="0cb76-115">Wanneer u alle uw externe tabellen toohello nieuwe externe gegevensbron hebt gemigreerd en vervolgens kunt u uitvoeren opschonen Hallo taken:</span><span class="sxs-lookup"><span data-stu-id="0cb76-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="0cb76-116">Eerste externe gegevensbron verwijderen</span><span class="sxs-lookup"><span data-stu-id="0cb76-116">Drop first external data source</span></span>
2. <span data-ttu-id="0cb76-117">Uitgevallen eerste database-scoped referentie op basis van de toegangssleutel voor Hallo primaire opslag</span><span class="sxs-lookup"><span data-stu-id="0cb76-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="0cb76-118">Meld u aan bij Azure en opnieuw genereren van Hallo primaire toegangssleutel gereed voor Hallo volgende keer</span><span class="sxs-lookup"><span data-stu-id="0cb76-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="0cb76-119">Query uitvoeren op Azure blob storage-gegevens</span><span class="sxs-lookup"><span data-stu-id="0cb76-119">Query Azure blob storage data</span></span>
<span data-ttu-id="0cb76-120">Hallo-tabelnaam een query uitgevoerd naar externe tabellen gewoon gebruiken alsof deze een relationele tabel is.</span><span class="sxs-lookup"><span data-stu-id="0cb76-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="0cb76-121">Een query op een externe tabel mislukken met fout Hallo *'Query afgebroken--Hallo maximale afwijzen drempelwaarde werd bereikt tijdens het lezen van een externe bron'*.</span><span class="sxs-lookup"><span data-stu-id="0cb76-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="0cb76-122">Dit geeft aan dat de externe gegevens bevat *dirty* records.</span><span class="sxs-lookup"><span data-stu-id="0cb76-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="0cb76-123">Een record wordt beschouwd als 'vervuild' als Hallo actuele gegevens typen of aantal kolommen komen niet overeen met de kolomdefinities Hallo van de externe tabel Hallo of als Hallo gegevens toohello opgegeven externe bestandsindeling komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="0cb76-124">toofix, zorg ervoor dat uw externe tabel en het externe bestand indeling definities juist zijn en de externe gegevens conform toothese definities.</span><span class="sxs-lookup"><span data-stu-id="0cb76-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="0cb76-125">Als een subset van externe gegevensrecords zijn gewijzigd, kunt u tooreject deze records voor uw query's met Hallo Weiger de opties in externe tabel-DDL maken.</span><span class="sxs-lookup"><span data-stu-id="0cb76-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="0cb76-126">Gegevens laden vanuit Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="0cb76-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="0cb76-127">In dit voorbeeld worden gegevens geladen uit Azure blob storage tooSQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="0cb76-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="0cb76-128">Opslaan van gegevens rechtstreeks verwijdert Hallo gegevens overdrachtstijd voor query's.</span><span class="sxs-lookup"><span data-stu-id="0cb76-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="0cb76-129">Opslaan van gegevens met een columnstore-index verbetert de prestaties van query's voor analyse van query's door up too10x.</span><span class="sxs-lookup"><span data-stu-id="0cb76-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="0cb76-130">In dit voorbeeld gebruikt tooload gegevens Hallo CREATE TABLE AS SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="0cb76-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="0cb76-131">nieuwe tabel Hallo overgenomen Hallo kolommen met de naam in het Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="0cb76-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="0cb76-132">Hallo-gegevenstypen van die kolommen van de definitie van de externe tabel Hallo worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="0cb76-133">CREATE TABLE AS SELECT is een zeer zodat Transact-SQL-instructie dat wordt geladen Hallo-gegevens in de parallelle tooall Hallo rekenknooppunten van uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0cb76-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="0cb76-134">Het oorspronkelijk is ontwikkeld voor Hallo massively parallelle processing (MPP)-engine in Analytics Platform System en bevindt zich nu in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0cb76-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="0cb76-135">Zie [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="0cb76-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="0cb76-136">Statistieken maken voor zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="0cb76-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="0cb76-137">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="0cb76-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="0cb76-138">Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.</span><span class="sxs-lookup"><span data-stu-id="0cb76-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="0cb76-139">Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="0cb76-140">Hieronder volgt een kort voorbeeld van hoe toocreate statistieken op Hallo ingediend in dit voorbeeld geladen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="0cb76-141">Exporteren van gegevens tooAzure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="0cb76-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="0cb76-142">Deze sectie wordt beschreven hoe tooexport gegevens uit SQL Data Warehouse tooAzure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="0cb76-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="0cb76-143">In dit voorbeeld maakt gebruik van CREATE externe TABLE AS SELECT die een zeer zodat Transact-SQL-instructie tooexport Hallo gegevens parallel uit alle Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="0cb76-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="0cb76-144">Hallo wordt volgende voorbeeld een externe tabel Weblogs2014 met behulp van de kolomdefinities en gegevens van dbo. Weblogboeken tabel.</span><span class="sxs-lookup"><span data-stu-id="0cb76-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="0cb76-145">Hallo externe tabeldefinitie wordt opgeslagen in SQL Data Warehouse en de resultaten Hallo Hallo SELECT-instructie geëxporteerde toohello '/ archiveren/log2014 /' map onder Hallo blob-container door Hallo-gegevensbron opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0cb76-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="0cb76-146">Hallo gegevens Hallo opgegeven tekstbestand geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="0cb76-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="0cb76-147">Het laden van gebruikers isoleren</span><span class="sxs-lookup"><span data-stu-id="0cb76-147">Isolate Loading Users</span></span>
<span data-ttu-id="0cb76-148">Er is vaak een toohave moeten meerdere gebruikers die gegevens in een SQL DW laden kunnen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="0cb76-149">Omdat Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] vereist machtigingen voor beheer van Hallo-database, verschijnt met meerdere gebruikers met toegangsbeheer via alle schema's.</span><span class="sxs-lookup"><span data-stu-id="0cb76-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="0cb76-150">toolimit, kunt u Hallo weigeren CONTROL-instructie.</span><span class="sxs-lookup"><span data-stu-id="0cb76-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="0cb76-151">Voorbeeld: Overweeg database schema's schema_A voor afdeling A en schema_B voor afdeling B laten database gebruikers user_A en user_B worden gebruikers voor PolyBase laden in afdeling A en B, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="0cb76-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="0cb76-152">Ze hebben gekregen BESTURINGSELEMENT databasemachtigingen.</span><span class="sxs-lookup"><span data-stu-id="0cb76-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="0cb76-153">Hallo auteurs van schema A en B vergrendelen nu hun schema's met behulp van weigeren:</span><span class="sxs-lookup"><span data-stu-id="0cb76-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="0cb76-154">Met dit user_A en user_B moeten nu worden vergrendeld van Hallo andere afdeling schema.</span><span class="sxs-lookup"><span data-stu-id="0cb76-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="0cb76-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cb76-155">Next steps</span></span>
<span data-ttu-id="0cb76-156">toolearn meer informatie over het verplaatsen gegevens tooSQL datawarehouse, Zie Hallo [Migratieoverzicht][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="0cb76-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
