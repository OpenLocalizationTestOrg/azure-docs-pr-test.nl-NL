---
title: Transparante gegevensversleuteling in SQL datawarehouse (T-SQL) | Microsoft Docs
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="ec999-103">Aan de slag met Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="ec999-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec999-104">Overzicht van beveiliging</span><span class="sxs-lookup"><span data-stu-id="ec999-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="ec999-105">Verificatie</span><span class="sxs-lookup"><span data-stu-id="ec999-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="ec999-106">Versleuteling (Portal)</span><span class="sxs-lookup"><span data-stu-id="ec999-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="ec999-107">Versleuteling (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="ec999-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="ec999-108">Vereiste bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="ec999-108">Required Permssions</span></span>
<span data-ttu-id="ec999-109">U moet een beheerder of als lid van de rol dbmanager zijn zodat Transparent Data Encryption (TDE).</span><span class="sxs-lookup"><span data-stu-id="ec999-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ec999-110">Codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="ec999-110">Enabling Encryption</span></span>
<span data-ttu-id="ec999-111">Volg deze stappen voor het inschakelen van TDE voor een SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ec999-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="ec999-112">Verbinding maken met de *master* database op de server die als host fungeert voor de database met een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="ec999-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ec999-113">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="ec999-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="ec999-114">Codering uitschakelen</span><span class="sxs-lookup"><span data-stu-id="ec999-114">Disabling Encryption</span></span>
<span data-ttu-id="ec999-115">Volg deze stappen voor het uitschakelen van TDE voor een SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ec999-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="ec999-116">Verbinding maken met de *master* database met een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="ec999-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ec999-117">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="ec999-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="ec999-118">Een onderbroken SQL Data Warehouse moet voordat u wijzigingen aanbrengt in de instellingen van TDE worden hervat.</span><span class="sxs-lookup"><span data-stu-id="ec999-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="ec999-119">Versleuteling controleren</span><span class="sxs-lookup"><span data-stu-id="ec999-119">Verifying Encryption</span></span>
<span data-ttu-id="ec999-120">Om te controleren coderingsstatus voor een SQL Data Warehouse, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="ec999-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="ec999-121">Verbinding maken met de *master* of exemplaar in de database met behulp van een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="ec999-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ec999-122">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="ec999-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="ec999-123">Een resultaat van ```1``` geeft aan van een versleutelde database ```0``` geeft een niet-versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="ec999-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="ec999-124">Versleuteling DMV 's</span><span class="sxs-lookup"><span data-stu-id="ec999-124">Encryption DMVs</span></span>
* <span data-ttu-id="ec999-125">[sys.databases.][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="ec999-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="ec999-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="ec999-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
