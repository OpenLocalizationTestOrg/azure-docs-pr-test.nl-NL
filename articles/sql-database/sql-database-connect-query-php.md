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
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="8c2fb-103">PHP gebruiken om een query uit te voeren voor een Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="8c2fb-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="8c2fb-104">In deze beknopte zelfstudie wordt gedemonstreerd hoe u [PHP](http://php.net/manual/en/intro-whatis.php) gebruikt om een programma te maken dat verbinding maakt met een Azure SQL-database, en hoe u Transact-SQL-instructies gebruikt om een query uit te voeren voor gegevens.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c2fb-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c2fb-105">Prerequisites</span></span>

<span data-ttu-id="8c2fb-106">Zorg ervoor dat u over het volgende beschikt om deze beknopte zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="8c2fb-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="8c2fb-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-107">An Azure SQL database.</span></span> <span data-ttu-id="8c2fb-108">In deze zelfstudie worden de resources gebruikt die u hebt gemaakt in een van deze Quick Starts:</span><span class="sxs-lookup"><span data-stu-id="8c2fb-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8c2fb-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="8c2fb-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8c2fb-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="8c2fb-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8c2fb-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c2fb-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8c2fb-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor het openbare IP-adres van de computer die u gebruikt voor deze beknopte zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="8c2fb-113">U hebt PHP en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="8c2fb-114">**MacOS**: installeer Homebrew en PHP, installeer het ODBC-stuurprogramma en SQLCMD, en installeer vervolgens het PHP-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="8c2fb-115">Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="8c2fb-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="8c2fb-116">**Ubuntu**: installeer PHP en andere vereiste pakketten, en installeer vervolgens het PHP-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="8c2fb-117">Zie [stap 1.2 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="8c2fb-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="8c2fb-118">**Windows**: installeer de nieuwste versie van PHP voor IIS Express, de nieuwste versie van Microsoft-stuurprogramma's voor SQL Server in IIS Express, Chocolatey, het ODBC-stuurprogramma en SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="8c2fb-119">Zie [stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="8c2fb-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="8c2fb-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="8c2fb-120">SQL server connection information</span></span>

<span data-ttu-id="8c2fb-121">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="8c2fb-122">U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="8c2fb-123">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8c2fb-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8c2fb-124">Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="8c2fb-125">Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de volgende afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="8c2fb-126">U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8c2fb-128">Als u de aanmeldingsgegevens voor de server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven en, indien nodig, het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="8c2fb-129">Code invoegen om een query uit te voeren voor een SQL-database</span><span class="sxs-lookup"><span data-stu-id="8c2fb-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="8c2fb-130">Maak een nieuw bestand in uw favoriete teksteditor **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="8c2fb-131">Vervang de inhoud door de volgende code en voeg de juiste waarden toe voor de server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="8c2fb-132">De code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8c2fb-132">Run the code</span></span>

1. <span data-ttu-id="8c2fb-133">Voer bij de opdrachtprompt de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="8c2fb-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="8c2fb-134">Controleer of de bovenste 20 rijen worden geretourneerd, en sluit vervolgens het toepassingsvenster.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c2fb-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c2fb-135">Next steps</span></span>
- [<span data-ttu-id="8c2fb-136">Uw eerste Azure SQL-database ontwerpen</span><span class="sxs-lookup"><span data-stu-id="8c2fb-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="8c2fb-137">Microsoft PHP-stuurprogramma's voor SQL Server</span><span class="sxs-lookup"><span data-stu-id="8c2fb-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="8c2fb-138">Problemen melden of vragen stellen</span><span class="sxs-lookup"><span data-stu-id="8c2fb-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
