---
title: Transparante gegevensversleuteling inschakelt voor Stretch-Database TSQL - Azure | Microsoft Docs
description: Transparante gegevensversleuteling (TDE) voor SQL Server Stretch Database in Azure TSQL inschakelen
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="595ec-103">Transparante gegevensversleuteling (TDE) inschakelen voor Stretch Database in Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="595ec-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="595ec-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="595ec-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="595ec-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="595ec-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="595ec-106">Transparent Data Encryption (TDE) beschermt tegen de dreiging van schadelijke activiteiten door realtime versleuteling en ontsleuteling van de database, gekoppelde back-ups en transactielogboekbestanden in rust in te voeren zonder dat wijzigingen in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="595ec-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="595ec-107">TDE versleutelt de opslag van een volledige database met behulp van een symmetrische sleutel, naam van de databaseversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="595ec-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="595ec-108">De databaseversleutelingssleutel is beveiligd met een ingebouwde servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="595ec-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="595ec-109">Het ingebouwde servercertificaat is uniek voor elke Azure-server.</span><span class="sxs-lookup"><span data-stu-id="595ec-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="595ec-110">Microsoft draait automatisch deze certificaten ten minste om de 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="595ec-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="595ec-111">Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="595ec-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="595ec-112">Codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="595ec-112">Enabling Encryption</span></span>
<span data-ttu-id="595ec-113">Zodat TDE voor een Azure-database die de gegevens opslaat die zijn gemigreerd vanuit een Stretch geschikte SQL Server-database, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="595ec-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="595ec-114">Verbinding maken met de *master* database op de Azure-server die als host fungeert voor de database met een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="595ec-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="595ec-115">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="595ec-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="595ec-116">Codering uitschakelen</span><span class="sxs-lookup"><span data-stu-id="595ec-116">Disabling Encryption</span></span>
<span data-ttu-id="595ec-117">Schakel TDE voor een Azure-database die de gegevens worden opgeslagen die zijn gemigreerd vanuit Stretch geschikte SQL Server-database, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="595ec-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="595ec-118">Verbinding maken met de *master* database met een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="595ec-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="595ec-119">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="595ec-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="595ec-120">Versleuteling controleren</span><span class="sxs-lookup"><span data-stu-id="595ec-120">Verifying Encryption</span></span>
<span data-ttu-id="595ec-121">Om te controleren of coderingsstatus voor een Azure-database met opslaan van de gegevens gemigreerd vanuit een Stretch geschikte SQL Server-database, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="595ec-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="595ec-122">Verbinding maken met de *master* of exemplaar in de database met behulp van een aanmelding die een beheerder of als lid van de **dbmanager** rol in de database master</span><span class="sxs-lookup"><span data-stu-id="595ec-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="595ec-123">Voer de volgende instructie voor het versleutelen van de database.</span><span class="sxs-lookup"><span data-stu-id="595ec-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="595ec-124">Een resultaat van ```1``` geeft aan van een versleutelde database ```0``` geeft een niet-versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="595ec-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="595ec-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="595ec-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
