---
title: PHP gebruiken om een query uit te voeren voor een Azure SQL-database | Microsoft Docs
description: In dit onderwerp ziet u hoe u PHP gebruikt om een programma te maken dat is verbonden met een Azure SQL-database, en hoe u een query voor deze database uitvoert met behulp van Transact-SQL-instructies.
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
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a>PHP gebruiken om een query uit te voeren voor een Azure SQL-database

In deze beknopte zelfstudie wordt gedemonstreerd hoe u [PHP](http://php.net/manual/en/intro-whatis.php) gebruikt om een programma te maken dat verbinding maakt met een Azure SQL-database, en hoe u Transact-SQL-instructies gebruikt om een query uit te voeren voor gegevens.

## <a name="prerequisites"></a>Vereisten

Zorg ervoor dat u over het volgende beschikt om deze beknopte zelfstudie te voltooien:

- Een Azure SQL-database. In deze zelfstudie worden de resources gebruikt die u hebt gemaakt in een van deze Quick Starts: 

   - [Database maken - Portal](sql-database-get-started-portal.md)
   - [Database maken - CLI](sql-database-get-started-cli.md)
   - [Database maken - PowerShell](sql-database-get-started-powershell.md)

- Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor het openbare IP-adres van de computer die u gebruikt voor deze beknopte zelfstudie.

- U hebt PHP en verwante software voor uw besturingssysteem geïnstalleerd.

    - **MacOS**: installeer Homebrew en PHP, installeer het ODBC-stuurprogramma en SQLCMD, en installeer vervolgens het PHP-stuurprogramma voor SQL Server. Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: installeer PHP en andere vereiste pakketten, en installeer vervolgens het PHP-stuurprogramma voor SQL Server. Zie [stap 1.2 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: installeer de nieuwste versie van PHP voor IIS Express, de nieuwste versie van Microsoft-stuurprogramma's voor SQL Server in IIS Express, Chocolatey, het ODBC-stuurprogramma en SQLCMD. Zie [stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database. U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.

1. Meld u aan bij [Azure Portal](https://portal.azure.com/).
2. Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**. 
3. Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de volgende afbeelding wordt weergegeven. U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen.  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u de aanmeldingsgegevens voor de server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven en, indien nodig, het wachtwoord opnieuw in te stellen.     
    
## <a name="insert-code-to-query-sql-database"></a>Code invoegen om een query uit te voeren voor een SQL-database

1. Maak een nieuw bestand in uw favoriete teksteditor **sqltest.php**.  

2. Vervang de inhoud door de volgende code en voeg de juiste waarden toe voor de server, de database, de gebruiker en het wachtwoord.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
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

## <a name="run-the-code"></a>De code uitvoeren

1. Voer bij de opdrachtprompt de volgende opdrachten uit:

   ```php
   php sqltest.php
   ```

2. Controleer of de bovenste 20 rijen worden geretourneerd, en sluit vervolgens het toepassingsvenster.

## <a name="next-steps"></a>Volgende stappen
- [Uw eerste Azure SQL-database ontwerpen](sql-database-design-first-database.md)
- [Microsoft PHP-stuurprogramma's voor SQL Server](https://github.com/Microsoft/msphpsql/)
- [Problemen melden of vragen stellen](https://github.com/Microsoft/msphpsql/issues)
