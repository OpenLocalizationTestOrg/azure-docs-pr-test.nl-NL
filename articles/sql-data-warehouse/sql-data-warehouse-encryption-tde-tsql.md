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
# <a name="get-started-with-transparent-data-encryption-tde"></a>Aan de slag met Transparent Data Encryption (TDE)
> [!div class="op_single_selector"]
> * [Overzicht van beveiliging](sql-data-warehouse-overview-manage-security.md)
> * [Verificatie](sql-data-warehouse-authentication.md)
> * [Versleuteling (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Versleuteling (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Vereiste bevoegdheden
tooenable Transparent Data Encryption (TDE), moet u een beheerder of lid zijn van Hallo dbmanager rol.

## <a name="enabling-encryption"></a>Codering inschakelen
Volg deze stappen tooenable TDE voor een SQL Data Warehouse:

1. Verbinding maken met toohello *master* database op Hallo-server die als host fungeert voor Hallo-database met behulp van een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo
2. Hallo volgende instructie tooencrypt Hallo database uitvoeren.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Codering uitschakelen
Volg deze stappen toodisable TDE voor een SQL Data Warehouse:

1. Verbinding maken met toohello *master* database met een aanmelding die een beheerder of als lid van Hallo **dbmanager** rol in de hoofddatabase Hallo
2. Hallo volgende instructie tooencrypt Hallo database uitvoeren.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Een onderbroken SQL Data Warehouse moet voordat u wijzigingen aanbrengt toohello TDE instellingen worden hervat.
> 
> 

## <a name="verifying-encryption"></a>Versleuteling controleren
de coderingsstatus tooverify voor een SQL Data Warehouse Hallo volgende stappen:

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

## <a name="encryption-dmvs"></a>Versleuteling DMV 's
* [sys.databases.][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
