---
title: 'VS Code: verbinding maken met Azure SQL Database en query''s uitvoeren voor gegevens | Microsoft Docs'
description: Meer informatie over hoe tooconnect tooSQL-Database in Azure met behulp van Visual Studio Code. Voer (T-SQL) Transact-SQL-instructies tooquery en bewerken van gegevens.
metacanonical: 
keywords: verbinding maken met database toosql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Azure SQL Database: Gebruik Visual Studio Code tooconnect en query-gegevens

[Visual Studio Code](https://code.visualstudio.com/docs) is een grafische code-editor voor Linux, Mac OS, en Windows die ondersteuning biedt voor extensies, met inbegrip Hallo [mssql-extensie](https://aka.ms/mssql-marketplace) voor query's in Microsoft SQL Server, Azure SQL Database en SQL Data Warehouse. Deze snel starten laat zien hoe toouse Visual Studio Code tooconnect tooan Azure SQL database en vervolgens gebruik Transact-SQL-instructies tooquery, invoegen, bijwerken en verwijderen van gegevens in Hallo-database.

## <a name="prerequisites"></a>Vereisten

Deze snel starten wordt gebruikt als het eerste punt Hallo resources gemaakt in een van deze snel aan de slag:

- [Database maken - Portal](sql-database-get-started-portal.md)
- [Database maken - CLI](sql-database-get-started-cli.md)
- [Database maken - PowerShell](sql-database-get-started-powershell.md)

Voordat u begint, moet u de nieuwste versie Hallo van hebben geïnstalleerd [Visual Studio Code](https://code.visualstudio.com/Download) en geladen hello [mssql-extensie](https://aka.ms/mssql-marketplace). Zie voor instructies voor Hallo mssql extensie installatie [VS-Code installeren](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) en Zie [mssql voor Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>VS-code configureren 

### <a name="mac-os"></a>**Mac OS**
Voor Mac OS moet u tooinstall OpenSSL die een bij vereisten voor DotNet Core die mssql-extensie gebruikt. Open de terminal en Voer Hallo opdrachten tooinstall na **brew** en **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Er is geen speciale configuratie vereist.

### <a name="windows"></a>**Windows**

Er is geen speciale configuratie vereist.

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald. U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 
3. Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen. U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.

   ![verbindingsgegevens](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u Hallo aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo. 

## <a name="set-language-mode-toosql"></a>Set language modus tooSQL

Hallo taalmodus is ingesteld, te**SQL** in Visual Studio Code tooenable mssql opdrachten en IntelliSense T-SQL.

1. Open een nieuw Visual Studio Code venster. 

2. Klik op **tekst zonder opmaak** in Hallo rechterbenedenhoek van de statusbalk Hallo.
3. In Hallo **modus van de geselecteerde taal** vervolgkeuzelijst dat wordt geopend, type **SQL**, en druk vervolgens op **ENTER** tooset Hallo taal modus tooSQL. 

   ![SQL-taalmodus](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Verbinding maken met database tooyour

Gebruik Visual Studio Code tooestablish een verbinding tooyour Azure SQL Database-server.

> [!IMPORTANT]
> Voordat u doorgaat, zorgt u ervoor dat u uw server-, database- en aanmeldingsgegevens bij de hand hebt. Nadat u begint met Hallo-verbindingsgegevens profiel invoeren als u de focus van Visual Studio Code wijzigt, hebt u toorestart maken Hallo-verbindingsprofiel.
>

1. Druk in VS-Code op **CTRL + SHIFT + P** (of **F1**) tooopen Hallo opdracht palet.

2. Typ **sqlcon** en druk op **ENTER**.

3. Druk op **ENTER** tooselect **verbindingsprofiel maken**. Hiermee wordt een verbindingsprofiel gemaakt voor uw exemplaar van SQL Server.

4. Ga als volgt Hallo prompts toospecify Hallo verbindingseigenschappen voor de nieuwe verbindingsprofiel Hallo. Druk na elke waarde opgeeft, op **ENTER** toocontinue. 

   | Instelling       | Voorgestelde waarde | Beschrijving |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servernaam | de volledig gekwalificeerde servernaam Hallo | Hallo naam moet er ongeveer als volgt: **mynewserver20170313.database.windows.net**. |
   | **Databasenaam** | mySampleDatabase | Hallo-naam van Hallo database toowhich tooconnect. |
   | **Verificatie** | SQL-aanmelding| SQL-verificatie is Hallo alleen verificatie die we in deze zelfstudie hebt geconfigureerd. |
   | **Gebruikersnaam** | Hallo server-beheerdersaccount | Dit is Hallo-account die u hebt opgegeven tijdens het Hallo-server maken. |
   | **Wachtwoord (SQL-aanmelding)** | Hallo-wachtwoord voor uw server admin-account | Dit is Hallo wachtwoord die u hebt opgegeven tijdens het Hallo-server maken. |
   | **Wachtwoord opslaan?** | Ja of nee | Selecteer Ja als u dat tooenter Hallo wachtwoord niet elke keer wilt. |
   | **Voer een naam in voor dit profiel** | Een profielnaam, zoals **mySampleDatabase** | Een opgeslagen profiel zorgt ervoor dat de verbinding sneller tot stand komt bij toekomstige aanmeldingen. | 

5. Druk op Hallo **ESC** key tooclose Hallo infobericht wordt gemeld dat Hallo-profiel is gemaakt en is verbonden.

6. Controleer of de verbinding in de statusbalk Hallo.

   ![Verbindingsstatus](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Querygegevens

Gebruik Hallo volgende code tooquery voor Hallo top 20 producten per categorie met Hallo [Selecteer](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL-instructie.

1. In Hallo **Editor** venster, voer de volgende query in de lege queryvenster Hallo Hallo:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Druk op **CTRL + SHIFT + E** tooretrieve gegevens uit Hallo Product en ProductCategory.

    ![Query’s uitvoeren](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Gegevens invoegen

Gebruik Hallo volgende code tooinsert een nieuw product in Hallo SalesLT.Product tabel met Hallo [invoegen](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL-instructie.

1. In Hallo **Editor** venster Hallo vorige query en Voer Hallo query te volgen:

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

2. Druk op **CTRL + SHIFT + E** tooinsert een nieuwe rij in de tabel Hallo-Product.

## <a name="update-data"></a>Gegevens bijwerken

Gebruik Hallo volgende code tooupdate Hallo nieuw product dat u eerder hebt toegevoegd met behulp van Hallo [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL-instructie.

1.  In Hallo **Editor** venster Hallo vorige query en Voer Hallo query te volgen:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Druk op **CTRL + SHIFT + E** tooupdate Hallo opgegeven rij in de tabel Hallo-Product.

## <a name="delete-data"></a>Gegevens verwijderen

Gebruik Hallo volgende code toodelete Hallo nieuw product dat u eerder hebt toegevoegd met behulp van Hallo [verwijderen](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL-instructie.

1. In Hallo **Editor** venster Hallo vorige query en Voer Hallo query te volgen:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Druk op **CTRL + SHIFT + E** toodelete Hallo opgegeven rij in de tabel Hallo-Product.

## <a name="next-steps"></a>Volgende stappen

- Zie tooconnect en query met SQL Server Management Studio [Connect en query met SSMS](sql-database-connect-query-ssms.md).
- Zie het blogbericht [Create a database IDE with MSSQL extension](https://msdn.microsoft.com/magazine/mt809115) voor een MSDN-artikel over het gebruik van Visual Studio Code.
