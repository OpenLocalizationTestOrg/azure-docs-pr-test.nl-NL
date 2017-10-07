---
title: aaaMonitor uw werkbelasting via DMV's | Microsoft Docs
description: Meer informatie over hoe toomonitor uw werkbelasting via DMV's.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="a7a1c-103">Monitor your workload using DMVs</span><span class="sxs-lookup"><span data-stu-id="a7a1c-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="a7a1c-104">Dit artikel wordt beschreven hoe toouse dynamische beheerweergaven (DMV's) toomonitor uw werkbelasting en onderzoek de uitvoering van de query in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="a7a1c-105">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="a7a1c-105">Permissions</span></span>
<span data-ttu-id="a7a1c-106">tooquery hello DMV's in dit artikel, moet u de status van de DATABASE weergeven of BESTURINGSELEMENT machtiging.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="a7a1c-107">STATUS van de DATABASE verlenen weergeven is meestal Hallo voorkeur machtiging omdat dit veel meer beperkende.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="a7a1c-108">Monitor-verbindingen</span><span class="sxs-lookup"><span data-stu-id="a7a1c-108">Monitor connections</span></span>
<span data-ttu-id="a7a1c-109">Alle aanmeldingen tooSQL Data Warehouse te worden geregistreerd[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="a7a1c-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="a7a1c-110">Deze DMV bevat Hallo laatste 10.000 aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="a7a1c-111">Hallo session_id Hallo primaire sleutel en sequentieel voor elke nieuwe aanmelding is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="a7a1c-112">Query uitvoeren van de monitor</span><span class="sxs-lookup"><span data-stu-id="a7a1c-112">Monitor query execution</span></span>
<span data-ttu-id="a7a1c-113">Alle query's voor SQL Data Warehouse uitgevoerd te worden geregistreerd[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="a7a1c-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="a7a1c-114">Deze DMV bevat Hallo laatste 10.000 query's die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="a7a1c-115">Hallo request_id identificeert elke query uniek en primaire sleutel voor deze DMV Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="a7a1c-116">Hallo request_id sequentieel is toegewezen voor elke nieuwe query en wordt voorafgegaan door QID staat voor de query-ID.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="a7a1c-117">Deze DMV voor een bepaalde session_id opvragen, ziet u alle query's voor een bepaalde aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="a7a1c-118">Opgeslagen procedures meerdere aanvraag-id's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="a7a1c-119">Aanvraag-id's zijn toegewezen in opeenvolgende volgorde.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="a7a1c-120">Hier vindt u stappen toofollow tooinvestigate queryplannen-uitvoering en tijden voor een bepaalde query.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="a7a1c-121">STAP 1: Hallo-query die u wenst dat tooinvestigate identificeren</span><span class="sxs-lookup"><span data-stu-id="a7a1c-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="a7a1c-122">Van Hallo voorafgaand aan de resultaten van de query, **Opmerking Hallo aanvraag-ID** van dat u tooinvestigate wilt Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="a7a1c-123">Query's in Hallo **onderbroken** status wordt in de wachtrij vanwege tooconcurrency limieten.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="a7a1c-124">Deze query's worden ook weergegeven in Hallo sys.dm_pdw_waits wacht query met een type UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="a7a1c-125">Zie [gelijktijdigheid en werkbelasting management] [ Concurrency and workload management] voor meer informatie over limieten voor gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="a7a1c-126">Query's kunnen ook wachten om andere redenen zoals voor het object wordt vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="a7a1c-127">Als uw query voor een resource wacht, Zie [onderzoeken van query's die wachten op resources] [ Investigating queries waiting for resources] verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="a7a1c-128">toosimplify hello opzoeken van een query in Hallo sys.dm_pdw_exec_requests tabel, gebruik [LABEL] [ LABEL] tooassign een opmerking tooyour-query die kan worden opgezocht in Hallo sys.dm_pdw_exec_requests weergave.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="a7a1c-129">STAP 2: Het queryplan Hallo onderzoeken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="a7a1c-130">Gebruik Hallo aanvraag-ID tooretrieve Hallo van gedistribueerde SQL (DSQL) queryplan van [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="a7a1c-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="a7a1c-131">Als een DSQL plan langer duurt dan verwacht, worden Hallo oorzaak een complexe planning met veel DSQL stappen of slechts één stap lang duurt.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="a7a1c-132">Hallo plan veel stappen met verschillende migratiebewerkingen, dan kunt u uw distributies tooreduce gegevensverplaatsing optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="a7a1c-133">Hallo [tabel distributie] [ Table distribution] artikel wordt uitgelegd waarom gegevens verplaatst toosolve een query moet worden en sommige gegevensverplaatsing distributie strategieën toominimize wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="a7a1c-134">tooinvestigate meer informatie over één stap hello *operation_type* kolom Hallo langlopende query stap en Opmerking Hallo **stap Index**:</span><span class="sxs-lookup"><span data-stu-id="a7a1c-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="a7a1c-135">Doorgaan met stap 3a voor **SQL-bewerkingen**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="a7a1c-136">Doorgaan met stap 3b voor **gegevensverplaatsing operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="a7a1c-137">STAP 3a: SQL op Hallo gedistribueerde databases onderzoeken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="a7a1c-138">Gebruik Hallo aanvraag-ID en Hallo stap Index tooretrieve details van [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], bevat informatie van de uitvoering van Hallo query stap op Hallo van alle databases gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="a7a1c-139">Wanneer de Hallo query stap wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] gebruikte tooretrieve Hallo SQL Server geschatte plan van SQL Server-plancache voor Hallo stap uitgevoerd op een bepaalde Hallo kan zijn distributie.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="a7a1c-140">STAP 3b: gegevensverplaatsing-on Hallo gedistribueerde databases onderzoeken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="a7a1c-141">Gebruik Hallo aanvraag-ID en Hallo stap Index tooretrieve informatie over een data movement stap uitgevoerd op elke distributie van [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="a7a1c-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="a7a1c-142">Controleer de Hallo *total_elapsed_time* toosee kolom als een bepaalde verdeling aanzienlijk langer dan andere voor verplaatsing van gegevens duurt.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="a7a1c-143">Controleer voor Hallo langlopende distributie, Hallo *rows_processed* kolom toosee als Hallo aantal rijen wordt verplaatst van dit distributiepunt aanzienlijk groter dan andere is.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="a7a1c-144">Als het geval is, dit kan duiden op verschil van de onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="a7a1c-145">Als het Hallo-query wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] gebruikte tooretrieve Hallo SQL Server geschatte plan van de plancache SQL Server voor SQL-stap momenteel worden uitgevoerd binnen een bepaalde Hallo Hallo kan zijn distributie.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="a7a1c-146">Wachten op query's bewaken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-146">Monitor waiting queries</span></span>
<span data-ttu-id="a7a1c-147">Als u ontdekt dat de query niet aan te uitgevoerd brengen omdat het wacht op een resource, is dit een query waarin alle Hallo-bronnen wacht op een query.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="a7a1c-148">Als Hallo query actief op bronnen van een andere query wacht, wordt de Hallo sessiestatus **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="a7a1c-149">Als Hallo query alle resources voor Hallo vereist heeft, wordt de Hallo sessiestatus **verleend**.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="a7a1c-150">Monitor tempdb</span><span class="sxs-lookup"><span data-stu-id="a7a1c-150">Monitor tempdb</span></span>
<span data-ttu-id="a7a1c-151">Hoge tempdb-gebruik kan worden Hallo hoofdoorzaak voor trage prestaties en buiten geheugenproblemen.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a7a1c-152">Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en voert u de juiste acties Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a7a1c-153">Overweeg het schalen van uw datawarehouse als u de grenzen bereikt tijdens het uitvoeren van query tempdb vinden.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="a7a1c-154">Hallo hieronder wordt beschreven hoe tooidentify tempdb gebruik per query op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="a7a1c-155">Hallo volgende weergave tooassociate Hallo juiste knooppunt-id voor sys.dm_pdw_sql_requests maken.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="a7a1c-156">Dit zal u tooleverage andere Pass Through-DMV's inschakelen en koppel deze tabellen met sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="a7a1c-157">Voer Hallo query toomonitor tempdb te volgen:</span><span class="sxs-lookup"><span data-stu-id="a7a1c-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="a7a1c-158">Monitor-geheugen</span><span class="sxs-lookup"><span data-stu-id="a7a1c-158">Monitor memory</span></span>

<span data-ttu-id="a7a1c-159">Geheugen kan worden Hallo hoofdoorzaak voor trage prestaties en buiten geheugenproblemen.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a7a1c-160">Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en voert u de juiste acties Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a7a1c-161">Overweeg het schalen van uw datawarehouse als u SQL Server-geheugengebruik de grenzen bereikt tijdens het uitvoeren van query vinden.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="a7a1c-162">Hallo na query retourneert SQL Server-gebruik en geheugen geheugendruk per knooppunt:</span><span class="sxs-lookup"><span data-stu-id="a7a1c-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="a7a1c-163">Grootte van de transactie-logboekbestand bewaken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-163">Monitor transaction log size</span></span>
<span data-ttu-id="a7a1c-164">Hallo retourneert volgende query Hallo transactielogboekgrootte op elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="a7a1c-165">Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en Hallo-passende maatregelen.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a7a1c-166">Als een van de logboekbestanden Hallo 160GB bereikt, moet u rekening houden met schalen van uw exemplaar of de grootte van uw transactie te beperken.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="a7a1c-167">Terugdraaien van transactie-logboekbestand bewaken</span><span class="sxs-lookup"><span data-stu-id="a7a1c-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="a7a1c-168">Als uw query's mislukken of een tooproceed lang duurt, u kunt controleren en controleren als er transacties worden teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="a7a1c-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7a1c-169">Next steps</span></span>
<span data-ttu-id="a7a1c-170">Zie [systeemweergaven] [ System views] voor meer informatie over DMV's.</span><span class="sxs-lookup"><span data-stu-id="a7a1c-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="a7a1c-171">Zie [aanbevolen procedures voor SQL Data Warehouse] [ SQL Data Warehouse best practices] voor meer informatie over best practices</span><span class="sxs-lookup"><span data-stu-id="a7a1c-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
