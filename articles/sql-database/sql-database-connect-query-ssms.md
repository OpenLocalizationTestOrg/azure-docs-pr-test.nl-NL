---
title: 'SSMS: verbinding maken met Azure SQL Database en query''s uitvoeren voor gegevens | Microsoft Docs'
description: Meer informatie over hoe tooconnect tooSQL-Database in Azure met behulp van SQL Server Management Studio (SSMS). Voer (T-SQL) Transact-SQL-instructies tooquery en bewerken van gegevens.
metacanonical: 
keywords: verbinding maken met database toosql, sql server management studio
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a>Azure SQL Database: Gebruik SQL Server Management Studio tooconnect en query-gegevens

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is een geïntegreerde omgeving voor het beheren van elke SQL-infrastructuur van tooSQL van SQL Server-Database voor Microsoft Windows. Deze snel starten laat zien hoe toouse SSMS tooconnect tooan Azure SQL database en vervolgens gebruik Transact-SQL-instructies tooquery, invoegen, bijwerken en verwijderen van gegevens in Hallo-database. 

## <a name="prerequisites"></a>Vereisten

Deze snel starten wordt gebruikt als het eerste punt Hallo resources gemaakt in een van deze snel aan de slag:

- [Database maken - Portal](sql-database-get-started-portal.md)
- [Database maken - CLI](sql-database-get-started-cli.md)
- [Database maken - PowerShell](sql-database-get-started-powershell.md)

Voordat u begint, moet u de nieuwste versie Hallo van hebben geïnstalleerd [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald. U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 
3. Op Hallo **overzicht** pagina voor uw database, controleert u de volledig gekwalificeerde servernaam Hallo zoals weergegeven in onderstaande afbeelding voor Hallo. U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.

   ![verbindingsgegevens](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u Hallo aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo. 

## <a name="connect-tooyour-database"></a>Verbinding maken met database tooyour

Gebruik SQL Server Management Studio tooestablish een verbinding tooyour Azure SQL Database-server. 

> [!IMPORTANT]
> Een logische Azure SQL Database-server luistert naar poort 1433. Als u tooconnect tooan Azure SQL Database logische server vanuit een bedrijfsfirewall probeert, moet deze poort openen in de bedrijfsfirewall Hallo voor u toosuccessfully verbinding maken.
>

1. Open SQL Server Management Studio.

2. In Hallo **tooServer verbinding** dialoogvenster Voer Hallo volgende informatie:

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertype** | Database-engine | Deze waarde is verplicht. |
   | **Servernaam** | de volledig gekwalificeerde servernaam Hallo | Hallo naam moet er ongeveer als volgt: **mynewserver20170313.database.windows.net**. |
   | **Verificatie** | SQL Server-verificatie | SQL-verificatie is Hallo alleen verificatie die we in deze zelfstudie hebt geconfigureerd. |
   | **Aanmelding** | Hallo server-beheerdersaccount | Dit is Hallo-account die u hebt opgegeven tijdens het Hallo-server maken. |
   | **Wachtwoord** | Hallo-wachtwoord voor uw server admin-account | Dit is Hallo wachtwoord die u hebt opgegeven tijdens het Hallo-server maken. |

   ![verbinding maken met tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. Klik op **opties** in Hallo **tooserver verbinding** in het dialoogvenster. In Hallo **verbinding toodatabase** sectie, voert u **mySampleDatabase** tooconnect toothis database.

   ![verbinding maken met toodb op server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Klik op **Verbinden**. Hallo Object Explorer-venster wordt geopend in SSMS. 

   ![verbonden tooserver](./media/sql-database-connect-query-ssms/connected.png)  

5. Vouw in Object Explorer **Databases** en vouw vervolgens **mySampleDatabase** tooview Hallo objecten in Hallo-voorbeelddatabase.

## <a name="query-data"></a>Querygegevens

Gebruik Hallo volgende code tooquery voor Hallo top 20 producten per categorie met Hallo [Selecteer](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL-instructie.

1. Klik in Objectverkenner met de rechtermuisknop op **mySampleDatabase** en klik vervolgens op **Nieuwe query**. Een lege queryvenster wordt geopend die verbonden tooyour database.
2. Voer in het queryvenster hello, Hallo query te volgen:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. Op de werkbalk Hallo **Execute** tooretrieve gegevens uit Hallo Product en ProductCategory.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Gegevens invoegen

Gebruik Hallo volgende code tooinsert een nieuw product in Hallo SalesLT.Product tabel met Hallo [invoegen](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL-instructie.

1. In het queryvenster hello, kunt u Hallo vorige query vervangen door Hallo query te volgen:

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. Op de werkbalk Hallo **Execute** tooinsert een nieuwe rij in de tabel Hallo-Product.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Gegevens bijwerken

Gebruik Hallo volgende code tooupdate Hallo nieuw product dat u eerder hebt toegevoegd met behulp van Hallo [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL-instructie.

1. In het queryvenster hello, kunt u Hallo vorige query vervangen door Hallo query te volgen:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Op de werkbalk Hallo **Execute** tooupdate Hallo opgegeven rij in de tabel Hallo-Product.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Gegevens verwijderen

Gebruik Hallo volgende code toodelete Hallo nieuw product dat u eerder hebt toegevoegd met behulp van Hallo [verwijderen](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL-instructie.

1. In het queryvenster hello, kunt u Hallo vorige query vervangen door Hallo query te volgen:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Op de werkbalk Hallo **Execute** toodelete Hallo opgegeven rij in de tabel Hallo-Product.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Volgende stappen

- toolearn over het maken en beheren van servers en databases met Transact-SQL, Zie [meer informatie over Azure SQL Database-servers en databases](sql-database-servers-databases.md).
- Zie [SQL Server Management Studio gebruiken](https://msdn.microsoft.com/library/ms174173.aspx) voor meer informatie over SSMS.
- Zie tooconnect en query met Visual Studio Code [Connect en query met Visual Studio Code](sql-database-connect-query-vscode.md).
- Zie tooconnect en query met .NET, [Connect en query met .NET](sql-database-connect-query-dotnet.md).
- Zie tooconnect en query met PHP, [Connect en query met PHP](sql-database-connect-query-php.md).
- Zie tooconnect en query met behulp van Node.js, [Connect en query met behulp van Node.js](sql-database-connect-query-nodejs.md).
- Zie tooconnect en query met Java, [Connect en query met Java](sql-database-connect-query-java.md).
- Zie tooconnect en query met behulp van Python, [Connect en query met behulp van Python](sql-database-connect-query-python.md).
- Zie tooconnect en query met Ruby, [Connect en query met Ruby](sql-database-connect-query-ruby.md).
