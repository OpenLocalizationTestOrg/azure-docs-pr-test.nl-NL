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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Transparante gegevensversleuteling (TDE) inschakelen voor Stretch Database in Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Azure Portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door het uitvoeren van realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogboekbestanden in rust zonder wijzigingen toohello de toepassing.

TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel. Hallo databaseversleutelingssleutel is beveiligd met een ingebouwde servercertificaat. ingebouwde Hallo-servercertificaat is uniek voor elke Azure-server. Microsoft draait automatisch deze certificaten ten minste om de 90 dagen. Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Codering inschakelen
tooenable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:

1. Verbinding maken met toohello *master* database op Hallo Azure server hosting Hallo-database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo
2. Hallo volgende instructie tooencrypt Hallo database uitvoeren.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Codering uitschakelen
toodisable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:

1. Verbinding maken met toohello *master* database met een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo
2. Hallo volgende instructie tooencrypt Hallo database uitvoeren.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Versleuteling controleren
de coderingsstatus tooverify voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:

1. Verbinding maken met toohello *master* of exemplaar in de database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo
2. Hallo volgende instructie tooencrypt Hallo database uitvoeren.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Een resultaat van ```1``` geeft aan van een versleutelde database ```0``` geeft een niet-versleutelde database.

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
