---
title: aaaPause, hervatten, schalen met REST in Azure SQL Data Warehouse | Microsoft Docs
description: De rekencapaciteit in SQL Data Warehouse via REST, T-SQL en PowerShell beheren.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="22b78-103">Rekencapaciteit in Azure SQL Data Warehouse (REST) beheren</span><span class="sxs-lookup"><span data-stu-id="22b78-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22b78-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="22b78-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="22b78-105">Portal</span><span class="sxs-lookup"><span data-stu-id="22b78-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="22b78-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22b78-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="22b78-107">REST</span><span class="sxs-lookup"><span data-stu-id="22b78-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="22b78-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="22b78-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="22b78-109">De rekencapaciteit schaal</span><span class="sxs-lookup"><span data-stu-id="22b78-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="22b78-110">toochange hello dwu's, gebruiken Hallo [maken of bijwerken Database] [ Create or Update Database] REST-API.</span><span class="sxs-lookup"><span data-stu-id="22b78-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="22b78-111">Hallo volgende voorbeeld wordt Hallo service level objective tooDW1000 voor Hallo database MySQLDW die wordt gehost op de server MijnServer.</span><span class="sxs-lookup"><span data-stu-id="22b78-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="22b78-112">Hallo-server in een Azure-resourcegroep genaamd ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="22b78-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="22b78-113">De rekencapaciteit onderbreken</span><span class="sxs-lookup"><span data-stu-id="22b78-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="22b78-114">een database toopause gebruiken Hallo [Database onderbreken] [ Pause Database] REST-API.</span><span class="sxs-lookup"><span data-stu-id="22b78-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="22b78-115">Hallo onderbroken volgende voorbeeld een database met naam Database02 gehost op een server met de naam Server01.</span><span class="sxs-lookup"><span data-stu-id="22b78-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="22b78-116">Hallo-server in een Azure-resourcegroep genaamd ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="22b78-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="22b78-117">Compute hervatten</span><span class="sxs-lookup"><span data-stu-id="22b78-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="22b78-118">een database toostart gebruiken Hallo [Database hervatten] [ Resume Database] REST-API.</span><span class="sxs-lookup"><span data-stu-id="22b78-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="22b78-119">Hallo wordt volgende voorbeeld een database met naam Database02 gehost op een server met de naam Server01.</span><span class="sxs-lookup"><span data-stu-id="22b78-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="22b78-120">Hallo-server in een Azure-resourcegroep genaamd ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="22b78-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="22b78-121">Controleer de databasestatus van de</span><span class="sxs-lookup"><span data-stu-id="22b78-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="22b78-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22b78-122">Next steps</span></span>
<span data-ttu-id="22b78-123">Zie voor andere beheertaken [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="22b78-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
