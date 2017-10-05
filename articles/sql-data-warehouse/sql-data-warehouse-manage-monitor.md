---
title: Uw werkbelasting via DMV's bewaken | Microsoft Docs
description: Informatie over het bewaken van uw werkbelasting via DMV's.
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
ms.openlocfilehash: 7ce6c2cdf1e28852da536414533ccdcdaeb437e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="f686d-103">Monitor your workload using DMVs</span><span class="sxs-lookup"><span data-stu-id="f686d-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="f686d-104">In dit artikel wordt beschreven hoe dynamische beheerweergaven (DMV's) gebruiken om te controleren van uw werkbelasting en onderzoeken van de uitvoering van de query in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f686d-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="f686d-105">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="f686d-105">Permissions</span></span>
<span data-ttu-id="f686d-106">Om te vragen de DMV's in dit artikel, moet u de status van de DATABASE weergeven of BESTURINGSELEMENT gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="f686d-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="f686d-107">STATUS van de DATABASE verlenen weergeven is meestal de voorkeur machtiging omdat dit veel meer beperkende.</span><span class="sxs-lookup"><span data-stu-id="f686d-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="f686d-108">Monitor-verbindingen</span><span class="sxs-lookup"><span data-stu-id="f686d-108">Monitor connections</span></span>
<span data-ttu-id="f686d-109">Alle aanmeldingen met SQL Data Warehouse worden geregistreerd in [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="f686d-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="f686d-110">Deze DMV bevat de laatste 10.000 aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="f686d-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="f686d-111">De session_id de primaire sleutel en sequentieel voor elke nieuwe aanmelding is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f686d-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="f686d-112">Query uitvoeren van de monitor</span><span class="sxs-lookup"><span data-stu-id="f686d-112">Monitor query execution</span></span>
<span data-ttu-id="f686d-113">Alle query's uitgevoerd op de SQL Data Warehouse worden geregistreerd in [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="f686d-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="f686d-114">Deze DMV bevat de laatste 10.000 query's uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f686d-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="f686d-115">De request_id unieke wijze identificeert elke query en is de primaire sleutel voor deze DMV.</span><span class="sxs-lookup"><span data-stu-id="f686d-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="f686d-116">De request_id sequentieel is toegewezen voor elke nieuwe query en wordt voorafgegaan door QID staat voor de query-ID.</span><span class="sxs-lookup"><span data-stu-id="f686d-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="f686d-117">Deze DMV voor een bepaalde session_id opvragen, ziet u alle query's voor een bepaalde aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f686d-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="f686d-118">Opgeslagen procedures meerdere aanvraag-id's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f686d-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="f686d-119">Aanvraag-id's zijn toegewezen in opeenvolgende volgorde.</span><span class="sxs-lookup"><span data-stu-id="f686d-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="f686d-120">Hier volgen de stappen volgen om te onderzoeken queryplannen uitvoering en tijden voor een bepaalde query.</span><span class="sxs-lookup"><span data-stu-id="f686d-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="f686d-121">STAP 1: De query die u wilt onderzoeken identificeren</span><span class="sxs-lookup"><span data-stu-id="f686d-121">STEP 1: Identify the query you wish to investigate</span></span>
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

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="f686d-122">In de voorgaande queryresultaten **Let op de aanvraag-ID** van de query die u wilt onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="f686d-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="f686d-123">Query's in de **onderbroken** status wordt in de wachtrij vanwege gelijktijdigheid limieten.</span><span class="sxs-lookup"><span data-stu-id="f686d-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="f686d-124">Deze query's worden ook weergegeven in de query sys.dm_pdw_waits wacht met het type UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="f686d-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="f686d-125">Zie [gelijktijdigheid en werkbelasting management] [ Concurrency and workload management] voor meer informatie over limieten voor gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="f686d-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="f686d-126">Query's kunnen ook wachten om andere redenen zoals voor het object wordt vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="f686d-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="f686d-127">Als uw query voor een resource wacht, Zie [onderzoeken van query's die wachten op resources] [ Investigating queries waiting for resources] verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="f686d-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="f686d-128">Gebruiken om te vereenvoudigen het opzoeken van een query in de tabel sys.dm_pdw_exec_requests, [LABEL] [ LABEL] een opmerking aan de query die kan worden opgezocht in de weergave sys.dm_pdw_exec_requests toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f686d-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="f686d-129">STAP 2: Het queryplan onderzoeken</span><span class="sxs-lookup"><span data-stu-id="f686d-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="f686d-130">De aanvraag-ID gebruiken voor het ophalen van de query gedistribueerde SQL (DSQL) plan van [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="f686d-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="f686d-131">Wanneer een DSQL plan langer duurt dan verwacht, kan de oorzaak een complexe planning met veel DSQL stappen of slechts één stap duurt lang zijn.</span><span class="sxs-lookup"><span data-stu-id="f686d-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="f686d-132">Als het plan veel stappen met verschillende migratiebewerkingen is, u kunt uw distributies tabel om te beperken van gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="f686d-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="f686d-133">De [tabel distributie] [ Table distribution] artikel wordt uitgelegd waarom de gegevens voor het oplossen van een query moet worden verplaatst en beschrijft een aantal strategieën distributiepunten om te beperken van gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="f686d-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="f686d-134">Voor het onderzoeken van verdere details over één stap, de *operation_type* kolom van de langlopende query stap en Opmerking de **stap Index**:</span><span class="sxs-lookup"><span data-stu-id="f686d-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="f686d-135">Doorgaan met stap 3a voor **SQL-bewerkingen**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="f686d-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="f686d-136">Doorgaan met stap 3b voor **gegevensverplaatsing operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="f686d-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="f686d-137">STAP 3a: SQL van de gedistribueerde databases onderzoeken</span><span class="sxs-lookup"><span data-stu-id="f686d-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="f686d-138">Gebruik van de aanvraag-ID en de Index van de stap voor het ophalen van de details van [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], die informatie van de uitvoering van de stap van de query op alle gedistribueerde databases bevat.</span><span class="sxs-lookup"><span data-stu-id="f686d-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="f686d-139">Wanneer de stap van de query wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] kan worden gebruikt om het plan van SQL Server-geschatte ophalen uit de cache voor het plan van SQL Server voor de stap die wordt uitgevoerd op een specifieke distributiepuntengroep.</span><span class="sxs-lookup"><span data-stu-id="f686d-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="f686d-140">STAP 3b: verplaatsing van gegevens van de gedistribueerde databases onderzoeken</span><span class="sxs-lookup"><span data-stu-id="f686d-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="f686d-141">Gebruik van de aanvraag-ID en de Index van de stap informatie ophalen over een data movement stap uitgevoerd op elke distributie van [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="f686d-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="f686d-142">Controleer de *total_elapsed_time* kolom om te zien als een bepaalde verdeling aanzienlijk langer duurt dan andere voor verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f686d-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="f686d-143">Voor de distributie langlopende controleren de *rows_processed* kolom om te zien als het aantal rijen wordt verplaatst van dit distributiepunt aanzienlijk groter dan andere is.</span><span class="sxs-lookup"><span data-stu-id="f686d-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="f686d-144">Als het geval is, dit kan duiden op verschil van de onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="f686d-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="f686d-145">Als de query wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] kan worden gebruikt voor het geschatte plan van SQL Server ophalen uit het cachegeheugen van de SQL Server-plan voor de huidige actieve stap van de SQL binnen een bepaald distributie.</span><span class="sxs-lookup"><span data-stu-id="f686d-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="f686d-146">Wachten op query's bewaken</span><span class="sxs-lookup"><span data-stu-id="f686d-146">Monitor waiting queries</span></span>
<span data-ttu-id="f686d-147">Als u ontdekt dat de query niet aan te uitgevoerd brengen omdat het wacht op een resource, is dit een query worden alle bronnen wacht op een query.</span><span class="sxs-lookup"><span data-stu-id="f686d-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

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

<span data-ttu-id="f686d-148">Als de query actief op de bronnen van een andere query wachten is, wordt de status van de instelling **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="f686d-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="f686d-149">Als de query de vereiste resources heeft, wordt de status van de instelling **verleend**.</span><span class="sxs-lookup"><span data-stu-id="f686d-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="f686d-150">Monitor tempdb</span><span class="sxs-lookup"><span data-stu-id="f686d-150">Monitor tempdb</span></span>
<span data-ttu-id="f686d-151">Hoge tempdb-gebruik, kan de hoofdoorzaak voor trage prestaties en buiten geheugenproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="f686d-151">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="f686d-152">Controleer eerst of als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en de benodigde acties.</span><span class="sxs-lookup"><span data-stu-id="f686d-152">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="f686d-153">Overweeg het schalen van uw datawarehouse als u de grenzen bereikt tijdens het uitvoeren van query tempdb vinden.</span><span class="sxs-lookup"><span data-stu-id="f686d-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="f686d-154">Hieronder wordt beschreven hoe u tempdb-gebruik per query op elk knooppunt identificeert.</span><span class="sxs-lookup"><span data-stu-id="f686d-154">The following describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="f686d-155">De volgende weergave koppelt u het juiste knooppunt-id voor sys.dm_pdw_sql_requests maken.</span><span class="sxs-lookup"><span data-stu-id="f686d-155">Create the following view to associate the appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="f686d-156">Hierdoor kunt u gebruikmaken van andere Pass Through-DMV's en koppel deze tabellen met sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="f686d-156">This will enable you to leverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
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
<span data-ttu-id="f686d-157">Voer de volgende query voor het bewaken van tempdb:</span><span class="sxs-lookup"><span data-stu-id="f686d-157">Run the following query to monitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="f686d-158">Monitor-geheugen</span><span class="sxs-lookup"><span data-stu-id="f686d-158">Monitor memory</span></span>

<span data-ttu-id="f686d-159">Geheugen mag de hoofdoorzaak voor trage prestaties en buiten geheugenproblemen.</span><span class="sxs-lookup"><span data-stu-id="f686d-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="f686d-160">Controleer eerst of als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en de benodigde acties.</span><span class="sxs-lookup"><span data-stu-id="f686d-160">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="f686d-161">Overweeg het schalen van uw datawarehouse als u SQL Server-geheugengebruik de grenzen bereikt tijdens het uitvoeren van query vinden.</span><span class="sxs-lookup"><span data-stu-id="f686d-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="f686d-162">De volgende query retourneert SQL Server-gebruik en geheugen geheugendruk per knooppunt:</span><span class="sxs-lookup"><span data-stu-id="f686d-162">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="f686d-163">Grootte van de transactie-logboekbestand bewaken</span><span class="sxs-lookup"><span data-stu-id="f686d-163">Monitor transaction log size</span></span>
<span data-ttu-id="f686d-164">De volgende query retourneert de grootte van het transactielogboek op elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="f686d-164">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="f686d-165">Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en de benodigde acties.</span><span class="sxs-lookup"><span data-stu-id="f686d-165">Please check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="f686d-166">Als een van de logboekbestanden 160GB bereikt, moet u rekening houden met schalen van uw exemplaar of de grootte van uw transactie te beperken.</span><span class="sxs-lookup"><span data-stu-id="f686d-166">If one of the log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="f686d-167">Terugdraaien van transactie-logboekbestand bewaken</span><span class="sxs-lookup"><span data-stu-id="f686d-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="f686d-168">Als uw query's zijn mislukt of lang duurt om door te gaan, kunt u controleren en bewaken als er transacties worden teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f686d-168">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f686d-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f686d-169">Next steps</span></span>
<span data-ttu-id="f686d-170">Zie [systeemweergaven] [ System views] voor meer informatie over DMV's.</span><span class="sxs-lookup"><span data-stu-id="f686d-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="f686d-171">Zie [aanbevolen procedures voor SQL Data Warehouse] [ SQL Data Warehouse best practices] voor meer informatie over best practices</span><span class="sxs-lookup"><span data-stu-id="f686d-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
