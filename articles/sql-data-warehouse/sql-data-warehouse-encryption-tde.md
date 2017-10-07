---
title: aaaTransparent gegevensversleuteling in SQL Data Warehouse (Portal) | Microsoft Docs
description: Transparante gegevensversleuteling (TDE) in SQL datawarehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Aan de slag met Transparent Data Encryption (TDE) in SQL Data Warehouse
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
tooenable TDE voor een SQL Data Warehouse Hallo volgende stappen:

1. Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)
2. Klik op Hallo databaseblade Hallo **instellingen** knop
3. Selecteer Hallo **transparante gegevensversleuteling** optie![][1]
4. Selecteer Hallo **op** instelling![][2]
5. Selecteer **opslaan**
   ![][3]  

## <a name="disabling-encryption"></a>Codering uitschakelen
toodisable TDE voor een SQL Data Warehouse Hallo volgende stappen:

1. Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)
2. Klik op Hallo databaseblade Hallo **instellingen** knop
3. Selecteer Hallo **transparante gegevensversleuteling** optie![][1]
4. Selecteer Hallo **uit** instelling![][4]
5. Selecteer **opslaan**
   ![][5]  

## <a name="encryption-dmvs"></a>Versleuteling DMV 's
Versleuteling kan worden bevestigd door hello DMV's te volgen:

* [sys.databases.]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases.]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
