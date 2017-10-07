---
title: aaaUse PHP tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse PHP toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>Gebruik PHP tooquery een Azure SQL database

Deze zelfstudie laat zien hoe toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate een programma tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.

## <a name="prerequisites"></a>Vereisten

toocomplete dit snelle zelfstudie begint, controleert u of hebt u de volgende Hallo:

- Een Azure SQL-database. Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten: 

   - [Database maken - Portal](sql-database-get-started-portal.md)
   - [Database maken - CLI](sql-database-get-started-cli.md)
   - [Database maken - PowerShell](sql-database-get-started-powershell.md)

- Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.

- U hebt PHP en verwante software voor uw besturingssysteem geïnstalleerd.

    - **Mac OS**: Homebrew installeren en PHP, Hallo ODBC-stuurprogramma en SQLCMD installeren en installeer vervolgens Hallo PHP-stuurprogramma voor SQL Server. Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: Installeer PHP en andere vereiste pakketten en installatie Hallo PHP-stuurprogramma voor SQL Server. Zie [stap 1.2 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: Installeer Hallo nieuwste versie van PHP voor IIS Express, de nieuwste versie van Microsoft-Drivers voor SQL Server in IIS Express, Chocolatey Hallo ODBC-stuurprogramma en SQLCMD Hallo. Zie [stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald. U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 
3. Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen. U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u uw aanmeldingsgegevens server vergeet, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.     
    
## <a name="insert-code-tooquery-sql-database"></a>Code tooquery SQL-database invoegen

1. Maak een nieuw bestand in uw favoriete teksteditor **sqltest.php**.  

2. Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a>Hallo code uitvoeren

1. Voer bij de opdrachtprompt Hallo Hallo opdrachten na:

   ```php
   php sqltest.php
   ```

2. Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.

## <a name="next-steps"></a>Volgende stappen
- [Uw eerste Azure SQL-database ontwerpen](sql-database-design-first-database.md)
- [Microsoft PHP-stuurprogramma's voor SQL Server](https://github.com/Microsoft/msphpsql/)
- [Problemen melden of vragen stellen](https://github.com/Microsoft/msphpsql/issues)
