---
title: Onderbreken, hervatten, schalen met T-SQL in Azure SQL Data Warehouse | Microsoft Docs
description: (T-SQL) Transact-SQL-taken voor de prestaties van de scale-out door dwu's aan te passen. Kosten besparen door te schalen tijdens de niet-piekuren.
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
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="ca440-104">Beheren van de rekencapaciteit in Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="ca440-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca440-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ca440-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="ca440-106">Portal</span><span class="sxs-lookup"><span data-stu-id="ca440-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="ca440-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca440-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="ca440-108">REST</span><span class="sxs-lookup"><span data-stu-id="ca440-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="ca440-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="ca440-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="ca440-110">De huidige DWU-instellingen weergeven</span><span class="sxs-lookup"><span data-stu-id="ca440-110">View current DWU settings</span></span>
<span data-ttu-id="ca440-111">De huidige DWU-instellingen voor uw databases weergeven:</span><span class="sxs-lookup"><span data-stu-id="ca440-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="ca440-112">Open SQL Server-Objectverkenner in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca440-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="ca440-113">Verbinding maken met de database master is gekoppeld aan de logische SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="ca440-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="ca440-114">Selecteer in de weergave van de dynamische Beheerweergave sys.database_service_objectives.</span><span class="sxs-lookup"><span data-stu-id="ca440-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="ca440-115">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ca440-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="ca440-116">Scale compute</span><span class="sxs-lookup"><span data-stu-id="ca440-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="ca440-117">Het aantal dwu's wijzigen:</span><span class="sxs-lookup"><span data-stu-id="ca440-117">To change the DWUs:</span></span>

1. <span data-ttu-id="ca440-118">Verbinding maken met de database master die zijn gekoppeld aan de logische SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="ca440-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="ca440-119">Gebruik de [ALTER DATABASE] [ ALTER DATABASE] TSQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="ca440-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="ca440-120">Het volgende voorbeeld wordt de serviceniveaudoelstelling ingesteld op DW1000 voor de database MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="ca440-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="ca440-121">Controleer de voortgang van de status en de werking van de database</span><span class="sxs-lookup"><span data-stu-id="ca440-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="ca440-122">Verbinding maken met de database master die zijn gekoppeld aan de logische SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="ca440-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="ca440-123">Query voor het controleren van de status van de database verzenden</span><span class="sxs-lookup"><span data-stu-id="ca440-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="ca440-124">Indienen van query om te controleren van de status van bewerking</span><span class="sxs-lookup"><span data-stu-id="ca440-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="ca440-125">Deze DMV retourneert informatie over verschillende bewerkingen op uw SQL Data Warehouse zoals de werking en de status van de bewerking wordt IN_PROGRESS of voltooid.</span><span class="sxs-lookup"><span data-stu-id="ca440-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="ca440-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca440-126">Next steps</span></span>
<span data-ttu-id="ca440-127">Zie voor andere beheertaken [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="ca440-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
