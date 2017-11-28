---
title: Bewaking van Azure SQL Database met dynamische beheerweergaven | Microsoft Docs
description: Informatie over het detecteren en onderzoeken van veelvoorkomende prestatieproblemen met behulp van dynamische beheerweergaven voor het bewaken van Microsoft Azure SQL Database.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="140e9-103">Azure SQL Database controleren met dynamische beheerweergaven</span><span class="sxs-lookup"><span data-stu-id="140e9-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="140e9-104">Microsoft Azure SQL Database kunt een subset van de dynamische Beheerweergave weergaven voor het onderzoeken van prestatieproblemen, wordt door geblokkeerde of langdurige query's, resourceknelpunten en slechte queryplannen veroorzaakt mogelijk.</span><span class="sxs-lookup"><span data-stu-id="140e9-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="140e9-105">Dit onderwerp bevat informatie over het detecteren van veelvoorkomende prestatieproblemen met behulp van dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="140e9-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="140e9-106">SQL Database ondersteunt gedeeltelijk drie categorieën van dynamische beheerweergaven:</span><span class="sxs-lookup"><span data-stu-id="140e9-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="140e9-107">Database-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="140e9-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="140e9-108">Uitvoering-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="140e9-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="140e9-109">Transactie-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="140e9-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="140e9-110">Zie voor gedetailleerde informatie over dynamische beheerweergaven [functies (Transact-SQL) en dynamische beheerweergaven](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="140e9-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="140e9-111">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="140e9-111">Permissions</span></span>
<span data-ttu-id="140e9-112">In SQL-Database vereist voor het opvragen van een dynamische Beheerweergave **DATABASE WEERGAVESTATUS** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="140e9-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="140e9-113">De **DATABASE WEERGAVESTATUS** machtiging retourneert informatie over alle objecten in de huidige database.</span><span class="sxs-lookup"><span data-stu-id="140e9-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="140e9-114">Toe te kennen de **DATABASE WEERGAVESTATUS** machtiging aan een gebruiker specifieke database, voer de volgende query:</span><span class="sxs-lookup"><span data-stu-id="140e9-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="140e9-115">In een lokale SQL Server-exemplaar retourneren dynamische beheerweergaven informatie over de status van de server.</span><span class="sxs-lookup"><span data-stu-id="140e9-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="140e9-116">Deze retourneren informatie met betrekking tot alleen de huidige logische database in SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="140e9-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="140e9-117">Berekenen van de grootte van de database</span><span class="sxs-lookup"><span data-stu-id="140e9-117">Calculating database size</span></span>
<span data-ttu-id="140e9-118">De volgende query retourneert de grootte van de database (in megabytes):</span><span class="sxs-lookup"><span data-stu-id="140e9-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="140e9-119">De volgende query retourneert de grootte van afzonderlijke objecten (in MB) in de database:</span><span class="sxs-lookup"><span data-stu-id="140e9-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="140e9-120">Controleren van verbindingen</span><span class="sxs-lookup"><span data-stu-id="140e9-120">Monitoring connections</span></span>
<span data-ttu-id="140e9-121">U kunt de [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) weergave informatie ophalen over de verbindingen met een specifieke Azure SQL Database-server en de details van elke verbinding.</span><span class="sxs-lookup"><span data-stu-id="140e9-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="140e9-122">Bovendien de [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) weergave is handig bij het ophalen van informatie over alle actieve gebruikersverbindingen en interne taken.</span><span class="sxs-lookup"><span data-stu-id="140e9-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="140e9-123">De volgende query haalt informatie over de huidige verbinding:</span><span class="sxs-lookup"><span data-stu-id="140e9-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="140e9-124">Bij het uitvoeren van de **sys.dm_exec_requests** en **sys.dm_exec_sessions weergaven**, hebt u **DATABASE WEERGAVESTATUS** machtiging op de database u ziet alle uitvoeren sessies op de database. anders ziet u alleen de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="140e9-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="140e9-125">Queryprestaties bewaken</span><span class="sxs-lookup"><span data-stu-id="140e9-125">Monitoring query performance</span></span>
<span data-ttu-id="140e9-126">Traag of lang u query's uitvoert, kan dit aanzienlijke systeembronnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="140e9-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="140e9-127">Deze sectie wordt gedemonstreerd hoe u met dynamische beheerweergaven enkele algemene query prestatieproblemen detecteren.</span><span class="sxs-lookup"><span data-stu-id="140e9-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="140e9-128">Een verwijzing naar een oudere, maar nog steeds handig voor het oplossen van problemen, is de [het oplossen van prestatieproblemen in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artikel op Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="140e9-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="140e9-129">Top N-query's te zoeken</span><span class="sxs-lookup"><span data-stu-id="140e9-129">Finding top N queries</span></span>
<span data-ttu-id="140e9-130">Het volgende voorbeeld retourneert informatie over de bovenste vijf query basis van het gemiddelde CPU-tijd.</span><span class="sxs-lookup"><span data-stu-id="140e9-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="140e9-131">In dit voorbeeld maakt een aggregatie van de query's volgens de query-hash, zodat logisch gelijkwaardige query's zijn gegroepeerd op hun cumulatieve resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="140e9-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="140e9-132">Bewaking van geblokkeerde query 's</span><span class="sxs-lookup"><span data-stu-id="140e9-132">Monitoring blocked queries</span></span>
<span data-ttu-id="140e9-133">Trage of langdurige query's kunnen bijdragen tot overmatige brongebruik en het gevolg was van geblokkeerde query's.</span><span class="sxs-lookup"><span data-stu-id="140e9-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="140e9-134">De oorzaak van de blokkering kan worden toepassingen die niet goed ontwerp, onjuiste queryplannen, het gebrek aan nuttig indexen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="140e9-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="140e9-135">Voor informatie over de huidige activiteit van de vergrendeling in uw Azure SQL Database kunt u de weergave sys.dm_tran_locks.</span><span class="sxs-lookup"><span data-stu-id="140e9-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="140e9-136">Bijvoorbeeld code, Zie [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="140e9-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="140e9-137">Bewaking van queryplannen</span><span class="sxs-lookup"><span data-stu-id="140e9-137">Monitoring query plans</span></span>
<span data-ttu-id="140e9-138">Een inefficiënte queryplan kan ook CPU-verbruik verhogen.</span><span class="sxs-lookup"><span data-stu-id="140e9-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="140e9-139">Het volgende voorbeeld wordt de [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) weergeven om te bepalen welke query gebruikt de meest cumulatieve CPU.</span><span class="sxs-lookup"><span data-stu-id="140e9-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="140e9-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="140e9-140">See also</span></span>
[<span data-ttu-id="140e9-141">Inleiding tot SQL Database</span><span class="sxs-lookup"><span data-stu-id="140e9-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

