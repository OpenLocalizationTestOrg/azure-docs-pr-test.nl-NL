---
title: aaaPause, hervatten, schalen met T-SQL in Azure SQL Data Warehouse | Microsoft Docs
description: Transact-SQL (T-SQL) taken tooscale-out-prestaties door dwu's aan te passen. Kosten besparen door te schalen tijdens de niet-piekuren.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Beheren van de rekencapaciteit in Azure SQL Data Warehouse (T-SQL)
> [!div class="op_single_selector"]
> * [Overzicht](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>De huidige DWU-instellingen weergeven
tooview hello huidige DWU-instellingen voor uw databases:

1. Open SQL Server-Objectverkenner in Visual Studio.
2. Verbinding met het maken van de hoofddatabase toohello Hallo logische SQL Database-server gekoppeld.
3. Selecteer in de Hallo sys.database_service_objectives dynamische Beheerweergave. Hier volgt een voorbeeld: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Scale compute
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello dwu's:

1. Verbinding met het maken van de hoofddatabase toohello die zijn gekoppeld aan de logische SQL Database-server.
2. Gebruik Hallo [ALTER DATABASE] [ ALTER DATABASE] TSQL-instructie. Hallo wordt volgende voorbeeld Hallo service level objective tooDW1000 voor Hallo database MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Controleer de voortgang van de status en de werking van de database

1. Verbinding met het maken van de hoofddatabase toohello die zijn gekoppeld aan de logische SQL Database-server.
2. De status van de database toocheck query verzenden

```sql
SELECT *
FROM
sys.databases
```

3. De status van de query toocheck van bewerking verzenden

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Deze DMV retourneert informatie over verschillende bewerkingen op uw SQL Data Warehouse zoals Hallo bewerking en Hallo status van Hallo-bewerking wordt IN_PROGRESS of voltooid.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Volgende stappen
Zie voor andere beheertaken [Beheeroverzicht][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
