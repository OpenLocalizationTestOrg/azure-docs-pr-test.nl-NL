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
# <a name="monitor-your-workload-using-dmvs"></a>Monitor your workload using DMVs
Dit artikel wordt beschreven hoe toouse dynamische beheerweergaven (DMV's) toomonitor uw werkbelasting en onderzoek de uitvoering van de query in Azure SQL Data Warehouse.

## <a name="permissions"></a>Machtigingen
tooquery hello DMV's in dit artikel, moet u de status van de DATABASE weergeven of BESTURINGSELEMENT machtiging. STATUS van de DATABASE verlenen weergeven is meestal Hallo voorkeur machtiging omdat dit veel meer beperkende.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Monitor-verbindingen
Alle aanmeldingen tooSQL Data Warehouse te worden geregistreerd[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Deze DMV bevat Hallo laatste 10.000 aanmeldingen.  Hallo session_id Hallo primaire sleutel en sequentieel voor elke nieuwe aanmelding is toegewezen.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Query uitvoeren van de monitor
Alle query's voor SQL Data Warehouse uitgevoerd te worden geregistreerd[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Deze DMV bevat Hallo laatste 10.000 query's die worden uitgevoerd.  Hallo request_id identificeert elke query uniek en primaire sleutel voor deze DMV Hallo.  Hallo request_id sequentieel is toegewezen voor elke nieuwe query en wordt voorafgegaan door QID staat voor de query-ID.  Deze DMV voor een bepaalde session_id opvragen, ziet u alle query's voor een bepaalde aanmelding.

> [!NOTE]
> Opgeslagen procedures meerdere aanvraag-id's gebruiken.  Aanvraag-id's zijn toegewezen in opeenvolgende volgorde. 
> 
> 

Hier vindt u stappen toofollow tooinvestigate queryplannen-uitvoering en tijden voor een bepaalde query.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>STAP 1: Hallo-query die u wenst dat tooinvestigate identificeren
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

Van Hallo voorafgaand aan de resultaten van de query, **Opmerking Hallo aanvraag-ID** van dat u tooinvestigate wilt Hallo-query.

Query's in Hallo **onderbroken** status wordt in de wachtrij vanwege tooconcurrency limieten. Deze query's worden ook weergegeven in Hallo sys.dm_pdw_waits wacht query met een type UserConcurrencyResourceType. Zie [gelijktijdigheid en werkbelasting management] [ Concurrency and workload management] voor meer informatie over limieten voor gelijktijdigheid van taken. Query's kunnen ook wachten om andere redenen zoals voor het object wordt vergrendeld.  Als uw query voor een resource wacht, Zie [onderzoeken van query's die wachten op resources] [ Investigating queries waiting for resources] verderop in dit artikel.

toosimplify hello opzoeken van een query in Hallo sys.dm_pdw_exec_requests tabel, gebruik [LABEL] [ LABEL] tooassign een opmerking tooyour-query die kan worden opgezocht in Hallo sys.dm_pdw_exec_requests weergave.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>STAP 2: Het queryplan Hallo onderzoeken
Gebruik Hallo aanvraag-ID tooretrieve Hallo van gedistribueerde SQL (DSQL) queryplan van [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

Als een DSQL plan langer duurt dan verwacht, worden Hallo oorzaak een complexe planning met veel DSQL stappen of slechts één stap lang duurt.  Hallo plan veel stappen met verschillende migratiebewerkingen, dan kunt u uw distributies tooreduce gegevensverplaatsing optimaliseren. Hallo [tabel distributie] [ Table distribution] artikel wordt uitgelegd waarom gegevens verplaatst toosolve een query moet worden en sommige gegevensverplaatsing distributie strategieën toominimize wordt uitgelegd.

tooinvestigate meer informatie over één stap hello *operation_type* kolom Hallo langlopende query stap en Opmerking Hallo **stap Index**:

* Doorgaan met stap 3a voor **SQL-bewerkingen**: OnOperation, RemoteOperation, ReturnOperation.
* Doorgaan met stap 3b voor **gegevensverplaatsing operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>STAP 3a: SQL op Hallo gedistribueerde databases onderzoeken
Gebruik Hallo aanvraag-ID en Hallo stap Index tooretrieve details van [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], bevat informatie van de uitvoering van Hallo query stap op Hallo van alle databases gedistribueerd.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Wanneer de Hallo query stap wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] gebruikte tooretrieve Hallo SQL Server geschatte plan van SQL Server-plancache voor Hallo stap uitgevoerd op een bepaalde Hallo kan zijn distributie.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>STAP 3b: gegevensverplaatsing-on Hallo gedistribueerde databases onderzoeken
Gebruik Hallo aanvraag-ID en Hallo stap Index tooretrieve informatie over een data movement stap uitgevoerd op elke distributie van [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Controleer de Hallo *total_elapsed_time* toosee kolom als een bepaalde verdeling aanzienlijk langer dan andere voor verplaatsing van gegevens duurt.
* Controleer voor Hallo langlopende distributie, Hallo *rows_processed* kolom toosee als Hallo aantal rijen wordt verplaatst van dit distributiepunt aanzienlijk groter dan andere is. Als het geval is, dit kan duiden op verschil van de onderliggende gegevens.

Als het Hallo-query wordt uitgevoerd, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] gebruikte tooretrieve Hallo SQL Server geschatte plan van de plancache SQL Server voor SQL-stap momenteel worden uitgevoerd binnen een bepaalde Hallo Hallo kan zijn distributie.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Wachten op query's bewaken
Als u ontdekt dat de query niet aan te uitgevoerd brengen omdat het wacht op een resource, is dit een query waarin alle Hallo-bronnen wacht op een query.

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

Als Hallo query actief op bronnen van een andere query wacht, wordt de Hallo sessiestatus **AcquireResources**.  Als Hallo query alle resources voor Hallo vereist heeft, wordt de Hallo sessiestatus **verleend**.

## <a name="monitor-tempdb"></a>Monitor tempdb
Hoge tempdb-gebruik kan worden Hallo hoofdoorzaak voor trage prestaties en buiten geheugenproblemen. Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en voert u de juiste acties Hallo eerst. Overweeg het schalen van uw datawarehouse als u de grenzen bereikt tijdens het uitvoeren van query tempdb vinden. Hallo hieronder wordt beschreven hoe tooidentify tempdb gebruik per query op elk knooppunt. 

Hallo volgende weergave tooassociate Hallo juiste knooppunt-id voor sys.dm_pdw_sql_requests maken. Dit zal u tooleverage andere Pass Through-DMV's inschakelen en koppel deze tabellen met sys.dm_pdw_sql_requests.

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
Voer Hallo query toomonitor tempdb te volgen:

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
## <a name="monitor-memory"></a>Monitor-geheugen

Geheugen kan worden Hallo hoofdoorzaak voor trage prestaties en buiten geheugenproblemen. Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en voert u de juiste acties Hallo eerst. Overweeg het schalen van uw datawarehouse als u SQL Server-geheugengebruik de grenzen bereikt tijdens het uitvoeren van query vinden.

Hallo na query retourneert SQL Server-gebruik en geheugen geheugendruk per knooppunt: 
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
## <a name="monitor-transaction-log-size"></a>Grootte van de transactie-logboekbestand bewaken
Hallo retourneert volgende query Hallo transactielogboekgrootte op elk distributiepunt. Controleer als u gegevens kwaliteit scheeftrekken of slechte rowgroups hebben en Hallo-passende maatregelen. Als een van de logboekbestanden Hallo 160GB bereikt, moet u rekening houden met schalen van uw exemplaar of de grootte van uw transactie te beperken. 
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
## <a name="monitor-transaction-log-rollback"></a>Terugdraaien van transactie-logboekbestand bewaken
Als uw query's mislukken of een tooproceed lang duurt, u kunt controleren en controleren als er transacties worden teruggedraaid.
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

## <a name="next-steps"></a>Volgende stappen
Zie [systeemweergaven] [ System views] voor meer informatie over DMV's.
Zie [aanbevolen procedures voor SQL Data Warehouse] [ SQL Data Warehouse best practices] voor meer informatie over best practices

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
