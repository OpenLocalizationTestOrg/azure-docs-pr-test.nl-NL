---
title: Azure SQL Database met behulp van dynamische beheerweergaven aaaMonitoring | Microsoft Docs
description: Meer informatie over hoe toodetect en onderzoeken van veelvoorkomende prestatieproblemen met behulp van de dynamische Beheerweergave weergaven toomonitor Microsoft Azure SQL Database.
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="edcfc-103">Bewaking van Azure SQL-database met behulp van de dynamische beheerweergave</span><span class="sxs-lookup"><span data-stu-id="edcfc-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="edcfc-104">Microsoft Azure SQL Database maakt een subset van de dynamische Beheerweergave weergaven toodiagnose prestatieproblemen, die kunnen worden veroorzaakt door geblokkeerde of langdurige query's, resourceknelpunten en slechte queryplannen.</span><span class="sxs-lookup"><span data-stu-id="edcfc-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="edcfc-105">In dit onderwerp bevat informatie over hoe u veelvoorkomende prestatieproblemen met behulp van dynamische beheerweergaven toodetect.</span><span class="sxs-lookup"><span data-stu-id="edcfc-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="edcfc-106">SQL Database ondersteunt gedeeltelijk drie categorieën van dynamische beheerweergaven:</span><span class="sxs-lookup"><span data-stu-id="edcfc-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="edcfc-107">Database-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="edcfc-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="edcfc-108">Uitvoering-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="edcfc-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="edcfc-109">Transactie-gerelateerde dynamische beheerweergaven.</span><span class="sxs-lookup"><span data-stu-id="edcfc-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="edcfc-110">Zie voor gedetailleerde informatie over dynamische beheerweergaven [functies (Transact-SQL) en dynamische beheerweergaven](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="edcfc-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="edcfc-111">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="edcfc-111">Permissions</span></span>
<span data-ttu-id="edcfc-112">In SQL-Database vereist voor het opvragen van een dynamische Beheerweergave **DATABASE WEERGAVESTATUS** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="edcfc-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="edcfc-113">Hallo **DATABASE WEERGAVESTATUS** machtiging retourneert informatie over alle objecten in de huidige database Hallo.</span><span class="sxs-lookup"><span data-stu-id="edcfc-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="edcfc-114">Hallo toogrant **DATABASE WEERGAVESTATUS** machtiging tooa specifieke databasegebruiker, Hallo volgende query worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="edcfc-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="edcfc-115">In een lokale SQL Server-exemplaar retourneren dynamische beheerweergaven informatie over de status van de server.</span><span class="sxs-lookup"><span data-stu-id="edcfc-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="edcfc-116">Deze retourneren informatie met betrekking tot alleen de huidige logische database in SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="edcfc-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="edcfc-117">Berekenen van de grootte van de database</span><span class="sxs-lookup"><span data-stu-id="edcfc-117">Calculating database size</span></span>
<span data-ttu-id="edcfc-118">Hallo retourneert volgende query Hallo grootte van de database (in megabytes):</span><span class="sxs-lookup"><span data-stu-id="edcfc-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="edcfc-119">Hallo retourneert volgende query Hallo grootte van afzonderlijke objecten (in MB) in de database:</span><span class="sxs-lookup"><span data-stu-id="edcfc-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="edcfc-120">Controleren van verbindingen</span><span class="sxs-lookup"><span data-stu-id="edcfc-120">Monitoring connections</span></span>
<span data-ttu-id="edcfc-121">U kunt Hallo [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve informatie weergeven over Hallo verbindingen tooa specifieke Azure SQL Database-server en Hallo details van elke verbinding.</span><span class="sxs-lookup"><span data-stu-id="edcfc-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="edcfc-122">Bovendien Hallo [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) weergave is handig bij het ophalen van informatie over alle actieve gebruikersverbindingen en interne taken.</span><span class="sxs-lookup"><span data-stu-id="edcfc-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="edcfc-123">Hallo haalt volgende query informatie op de huidige verbinding Hallo:</span><span class="sxs-lookup"><span data-stu-id="edcfc-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="edcfc-124">Bij het uitvoeren van Hallo **sys.dm_exec_requests** en **sys.dm_exec_sessions weergaven**, hebt u **DATABASE WEERGAVESTATUS** machtiging op Hallo-database u ziet alle uitvoeren sessies op Hallo-database. anders ziet u alleen Hallo huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="edcfc-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="edcfc-125">Queryprestaties bewaken</span><span class="sxs-lookup"><span data-stu-id="edcfc-125">Monitoring query performance</span></span>
<span data-ttu-id="edcfc-126">Traag of lang u query's uitvoert, kan dit aanzienlijke systeembronnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="edcfc-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="edcfc-127">Deze sectie wordt gedemonstreerd hoe dynamische Beheerweergave toouse weergaven toodetect enkele algemene query prestatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="edcfc-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="edcfc-128">De verwijzing naar een oudere, maar nog steeds handig voor het oplossen van problemen is Hallo [het oplossen van prestatieproblemen in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artikel op Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="edcfc-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="edcfc-129">Top N-query's te zoeken</span><span class="sxs-lookup"><span data-stu-id="edcfc-129">Finding top N queries</span></span>
<span data-ttu-id="edcfc-130">Hallo retourneert volgende voorbeeld informatie over Hallo top vijf-query's die door het gemiddelde CPU-tijd is gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="edcfc-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="edcfc-131">In dit voorbeeld aggregeert Hallo query's volgens tootheir hash van de query, zodat logisch gelijkwaardige query's zijn gegroepeerd op hun cumulatieve resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="edcfc-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="edcfc-132">Bewaking van geblokkeerde query 's</span><span class="sxs-lookup"><span data-stu-id="edcfc-132">Monitoring blocked queries</span></span>
<span data-ttu-id="edcfc-133">Trage of langdurige query's kunnen bijdragen tooexcessive brongebruik en Hallo gevolg van een geblokkeerde query's worden.</span><span class="sxs-lookup"><span data-stu-id="edcfc-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="edcfc-134">Hallo oorzaak van het blokkeren van Hallo kan worden toepassingen die niet goed ontwerp, onjuiste queryplannen, Hallo gebrek aan nuttig indexen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="edcfc-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="edcfc-135">U kunt Hallo sys.dm_tran_locks weergave tooget informatie over de huidige vergrendelingsfout activiteit hello gebruiken in uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="edcfc-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="edcfc-136">Bijvoorbeeld code, Zie [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="edcfc-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="edcfc-137">Bewaking van queryplannen</span><span class="sxs-lookup"><span data-stu-id="edcfc-137">Monitoring query plans</span></span>
<span data-ttu-id="edcfc-138">Een inefficiënte queryplan kan ook CPU-verbruik verhogen.</span><span class="sxs-lookup"><span data-stu-id="edcfc-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="edcfc-139">Hallo volgende voorbeeld wordt Hallo [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) toodetermine welke query de meest cumulatieve CPU Hallo gebruikt weergeven.</span><span class="sxs-lookup"><span data-stu-id="edcfc-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="edcfc-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="edcfc-140">See also</span></span>
[<span data-ttu-id="edcfc-141">Inleiding tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="edcfc-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

