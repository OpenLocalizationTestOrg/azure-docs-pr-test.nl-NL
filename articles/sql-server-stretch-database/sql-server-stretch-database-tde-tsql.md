---
title: Transparent Data Encryption voor Stretch Database TSQL - Azure aaaEnable | Microsoft Docs
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
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="6ccbf-103">Transparante gegevensversleuteling (TDE) inschakelen voor Stretch Database in Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="6ccbf-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ccbf-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ccbf-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="6ccbf-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6ccbf-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="6ccbf-106">Transparent Data Encryption (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door het uitvoeren van realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogboekbestanden in rust zonder wijzigingen toohello de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="6ccbf-107">TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="6ccbf-108">Hallo databaseversleutelingssleutel is beveiligd met een ingebouwde servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="6ccbf-109">ingebouwde Hallo-servercertificaat is uniek voor elke Azure-server.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="6ccbf-110">Microsoft draait automatisch deze certificaten ten minste om de 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="6ccbf-111">Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="6ccbf-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="6ccbf-112">Codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ccbf-112">Enabling Encryption</span></span>
<span data-ttu-id="6ccbf-113">tooenable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ccbf-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="6ccbf-114">Verbinding maken met toohello *master* database op Hallo Azure server hosting Hallo-database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="6ccbf-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="6ccbf-115">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="6ccbf-116">Codering uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6ccbf-116">Disabling Encryption</span></span>
<span data-ttu-id="6ccbf-117">toodisable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ccbf-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="6ccbf-118">Verbinding maken met toohello *master* database met een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="6ccbf-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="6ccbf-119">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="6ccbf-120">Versleuteling controleren</span><span class="sxs-lookup"><span data-stu-id="6ccbf-120">Verifying Encryption</span></span>
<span data-ttu-id="6ccbf-121">de coderingsstatus tooverify voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ccbf-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="6ccbf-122">Verbinding maken met toohello *master* of exemplaar in de database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="6ccbf-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="6ccbf-123">Hallo volgende instructie tooencrypt Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="6ccbf-124">Een resultaat van ```1``` geeft aan van een versleutelde database ```0``` geeft een niet-versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="6ccbf-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
