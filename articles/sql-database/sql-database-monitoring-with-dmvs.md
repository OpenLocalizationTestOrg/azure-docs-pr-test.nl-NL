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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Bewaking van Azure SQL-database met behulp van de dynamische beheerweergave
Microsoft Azure SQL Database maakt een subset van de dynamische Beheerweergave weergaven toodiagnose prestatieproblemen, die kunnen worden veroorzaakt door geblokkeerde of langdurige query's, resourceknelpunten en slechte queryplannen. In dit onderwerp bevat informatie over hoe u veelvoorkomende prestatieproblemen met behulp van dynamische beheerweergaven toodetect.

SQL Database ondersteunt gedeeltelijk drie categorieën van dynamische beheerweergaven:

* Database-gerelateerde dynamische beheerweergaven.
* Uitvoering-gerelateerde dynamische beheerweergaven.
* Transactie-gerelateerde dynamische beheerweergaven.

Zie voor gedetailleerde informatie over dynamische beheerweergaven [functies (Transact-SQL) en dynamische beheerweergaven](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.

## <a name="permissions"></a>Machtigingen
In SQL-Database vereist voor het opvragen van een dynamische Beheerweergave **DATABASE WEERGAVESTATUS** machtigingen. Hallo **DATABASE WEERGAVESTATUS** machtiging retourneert informatie over alle objecten in de huidige database Hallo.
Hallo toogrant **DATABASE WEERGAVESTATUS** machtiging tooa specifieke databasegebruiker, Hallo volgende query worden uitgevoerd:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

In een lokale SQL Server-exemplaar retourneren dynamische beheerweergaven informatie over de status van de server. Deze retourneren informatie met betrekking tot alleen de huidige logische database in SQL-Database.

## <a name="calculating-database-size"></a>Berekenen van de grootte van de database
Hallo retourneert volgende query Hallo grootte van de database (in megabytes):

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Hallo retourneert volgende query Hallo grootte van afzonderlijke objecten (in MB) in de database:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Controleren van verbindingen
U kunt Hallo [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve informatie weergeven over Hallo verbindingen tooa specifieke Azure SQL Database-server en Hallo details van elke verbinding. Bovendien Hallo [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) weergave is handig bij het ophalen van informatie over alle actieve gebruikersverbindingen en interne taken.
Hallo haalt volgende query informatie op de huidige verbinding Hallo:

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
> Bij het uitvoeren van Hallo **sys.dm_exec_requests** en **sys.dm_exec_sessions weergaven**, hebt u **DATABASE WEERGAVESTATUS** machtiging op Hallo-database u ziet alle uitvoeren sessies op Hallo-database. anders ziet u alleen Hallo huidige sessie.
> 
> 

## <a name="monitoring-query-performance"></a>Queryprestaties bewaken
Traag of lang u query's uitvoert, kan dit aanzienlijke systeembronnen gebruiken. Deze sectie wordt gedemonstreerd hoe dynamische Beheerweergave toouse weergaven toodetect enkele algemene query prestatieproblemen. De verwijzing naar een oudere, maar nog steeds handig voor het oplossen van problemen is Hallo [het oplossen van prestatieproblemen in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artikel op Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Top N-query's te zoeken
Hallo retourneert volgende voorbeeld informatie over Hallo top vijf-query's die door het gemiddelde CPU-tijd is gerangschikt. In dit voorbeeld aggregeert Hallo query's volgens tootheir hash van de query, zodat logisch gelijkwaardige query's zijn gegroepeerd op hun cumulatieve resourceverbruik.

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

### <a name="monitoring-blocked-queries"></a>Bewaking van geblokkeerde query 's
Trage of langdurige query's kunnen bijdragen tooexcessive brongebruik en Hallo gevolg van een geblokkeerde query's worden. Hallo oorzaak van het blokkeren van Hallo kan worden toepassingen die niet goed ontwerp, onjuiste queryplannen, Hallo gebrek aan nuttig indexen, enzovoort. U kunt Hallo sys.dm_tran_locks weergave tooget informatie over de huidige vergrendelingsfout activiteit hello gebruiken in uw Azure SQL Database. Bijvoorbeeld code, Zie [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.

### <a name="monitoring-query-plans"></a>Bewaking van queryplannen
Een inefficiënte queryplan kan ook CPU-verbruik verhogen. Hallo volgende voorbeeld wordt Hallo [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) toodetermine welke query de meest cumulatieve CPU Hallo gebruikt weergeven.

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

## <a name="see-also"></a>Zie ook
[Inleiding tooSQL Database](sql-database-technical-overview.md)

