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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="c1858-104">Beheren van de rekencapaciteit in Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="c1858-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1858-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c1858-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c1858-106">Portal</span><span class="sxs-lookup"><span data-stu-id="c1858-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c1858-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1858-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c1858-108">REST</span><span class="sxs-lookup"><span data-stu-id="c1858-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c1858-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="c1858-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="c1858-110">De huidige DWU-instellingen weergeven</span><span class="sxs-lookup"><span data-stu-id="c1858-110">View current DWU settings</span></span>
<span data-ttu-id="c1858-111">tooview hello huidige DWU-instellingen voor uw databases:</span><span class="sxs-lookup"><span data-stu-id="c1858-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="c1858-112">Open SQL Server-Objectverkenner in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1858-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="c1858-113">Verbinding met het maken van de hoofddatabase toohello Hallo logische SQL Database-server gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c1858-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="c1858-114">Selecteer in de Hallo sys.database_service_objectives dynamische Beheerweergave.</span><span class="sxs-lookup"><span data-stu-id="c1858-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="c1858-115">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c1858-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="c1858-116">Scale compute</span><span class="sxs-lookup"><span data-stu-id="c1858-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="c1858-117">toochange hello dwu's:</span><span class="sxs-lookup"><span data-stu-id="c1858-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="c1858-118">Verbinding met het maken van de hoofddatabase toohello die zijn gekoppeld aan de logische SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="c1858-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c1858-119">Gebruik Hallo [ALTER DATABASE] [ ALTER DATABASE] TSQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="c1858-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="c1858-120">Hallo wordt volgende voorbeeld Hallo service level objective tooDW1000 voor Hallo database MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="c1858-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="c1858-121">Controleer de voortgang van de status en de werking van de database</span><span class="sxs-lookup"><span data-stu-id="c1858-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="c1858-122">Verbinding met het maken van de hoofddatabase toohello die zijn gekoppeld aan de logische SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="c1858-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c1858-123">De status van de database toocheck query verzenden</span><span class="sxs-lookup"><span data-stu-id="c1858-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="c1858-124">De status van de query toocheck van bewerking verzenden</span><span class="sxs-lookup"><span data-stu-id="c1858-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="c1858-125">Deze DMV retourneert informatie over verschillende bewerkingen op uw SQL Data Warehouse zoals Hallo bewerking en Hallo status van Hallo-bewerking wordt IN_PROGRESS of voltooid.</span><span class="sxs-lookup"><span data-stu-id="c1858-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c1858-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1858-126">Next steps</span></span>
<span data-ttu-id="c1858-127">Zie voor andere beheertaken [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="c1858-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
