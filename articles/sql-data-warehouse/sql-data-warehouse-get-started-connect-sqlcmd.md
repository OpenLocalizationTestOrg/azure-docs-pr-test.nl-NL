---
title: aaaConnect tooAzure SQL Data Warehouse sqlcmd | Microsoft Docs
description: Gebruik [sqlcmd] [sqlcmd] opdrachtregelprogramma tooconnect tooand query een Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Verbinding maken met tooSQL Data Warehouse met sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Gebruik [sqlcmd] [ sqlcmd] opdrachtregelprogramma tooconnect tooand query uitvoeren op een Azure SQL Data Warehouse.  

## <a name="1-connect"></a>1. Verbinding maken
tooget gestart met [sqlcmd][sqlcmd], open Hallo-opdrachtprompt en voer **sqlcmd** gevolgd door de verbindingsreeks Hallo voor uw SQL Data Warehouse-database. Hallo-verbindingsreeks vereist Hallo volgende parameters:

* **Server (-S):** Server in de vorm Hallo `<`servernaam`>`. database.windows.net
* **Database (-d):** databasenaam.
* **Id's tussen aanhalingstekens inschakelen (-I):** id's tussen aanhalingstekens moet worden ingeschakeld tooconnect tooa SQL Data Warehouse-exemplaar.

toouse SQL Server-verificatie, moet u tooadd Hallo gebruikersnaam en wachtwoord parameters:

* **Gebruiker (-U):** Servergebruiker in de vorm Hallo `<`gebruiker`>`
* **Wachtwoord (-P):** wachtwoord Hallo gebruiker gekoppeld.

De verbindingsreeks kan er bijvoorbeeld Hallo volgende uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Azure Active Directory Integrated authentication toouse, moet u tooadd hello Azure Active Directory-parameters:

* **Azure Active Directory Authentication (-G):** Azure Active Directory gebruiken voor verificatie

De verbindingsreeks kan er bijvoorbeeld Hallo volgende uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> U moet te[Azure Active Directory-verificatie inschakelen](sql-data-warehouse-authentication.md) tooauthenticate met Active Directory.
> 
> 

## <a name="2-query"></a>2. Query’s uitvoeren
Nadat de verbinding, kunt u elke ondersteunde Transact-SQL-instructie voor Hallo exemplaar uitgeven.  In dit voorbeeld worden query's in de interactieve modus verzonden.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Deze volgende voorbeelden laten zien hoe u uw query's in de batchmodus Hallo -Q gebruiken of uw SQL-toosqlcmd sluizen kunt uitvoeren.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Volgende stappen
Zie [sqlcmd-documentatie] [ sqlcmd] voor meer informatie over informatie over opties voor Hallo beschikbaar in sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
