---
title: aaaTransparent gegevensversleuteling in SQL Data Warehouse (T-SQL) | Microsoft Docs
description: Transparante gegevensversleuteling (TDE) in SQL datawarehouse (T-SQL)
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="17031-103">Aan de slag met Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="17031-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17031-104">Overzicht van beveiliging</span><span class="sxs-lookup"><span data-stu-id="17031-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="17031-105">Verificatie</span><span class="sxs-lookup"><span data-stu-id="17031-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="17031-106">Versleuteling (Portal)</span><span class="sxs-lookup"><span data-stu-id="17031-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="17031-107">Versleuteling (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="17031-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="17031-108">Vereiste bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="17031-108">Required Permssions</span></span>
<span data-ttu-id="17031-109">tooenable Transparent Data Encryption (TDE), moet u een beheerder of lid zijn van Hallo dbmanager rol.</span><span class="sxs-lookup"><span data-stu-id="17031-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="17031-110">Codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="17031-110">Enabling Encryption</span></span>
<span data-ttu-id="17031-111">Volg deze stappen tooenable TDE voor een SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="17031-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="17031-112">Verbinding maken met toohello *master* database op Hallo-server die als host fungeert voor Hallo-database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="17031-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="17031-113">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="17031-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="17031-114">Codering uitschakelen</span><span class="sxs-lookup"><span data-stu-id="17031-114">Disabling Encryption</span></span>
<span data-ttu-id="17031-115">Volg deze stappen toodisable TDE voor een SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="17031-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="17031-116">Verbinding maken met toohello *master* database met een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="17031-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="17031-117">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="17031-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="17031-118">Een onderbroken SQL Data Warehouse moet voordat u wijzigingen aanbrengt toohello TDE instellingen worden hervat.</span><span class="sxs-lookup"><span data-stu-id="17031-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="17031-119">Versleuteling controleren</span><span class="sxs-lookup"><span data-stu-id="17031-119">Verifying Encryption</span></span>
<span data-ttu-id="17031-120">de coderingsstatus tooverify voor een SQL Data Warehouse Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="17031-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="17031-121">Verbinding maken met toohello *master* of exemplaar in de database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="17031-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="17031-122">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="17031-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="17031-123">Een resultaat van ```1``` geeft aan van een versleutelde database ```0``` geeft een niet-versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="17031-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="17031-124">Versleuteling DMV 's</span><span class="sxs-lookup"><span data-stu-id="17031-124">Encryption DMVs</span></span>
* <span data-ttu-id="17031-125">[sys.databases.][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="17031-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="17031-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="17031-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
