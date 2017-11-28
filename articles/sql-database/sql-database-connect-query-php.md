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
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="23189-103">Gebruik PHP tooquery een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="23189-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="23189-104">Deze zelfstudie laat zien hoe toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate een programma tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.</span><span class="sxs-lookup"><span data-stu-id="23189-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23189-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="23189-105">Prerequisites</span></span>

<span data-ttu-id="23189-106">toocomplete dit snelle zelfstudie begint, controleert u of hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="23189-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="23189-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="23189-107">An Azure SQL database.</span></span> <span data-ttu-id="23189-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="23189-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="23189-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="23189-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="23189-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="23189-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="23189-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="23189-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="23189-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="23189-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="23189-113">U hebt PHP en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="23189-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="23189-114">**Mac OS**: Homebrew installeren en PHP, Hallo ODBC-stuurprogramma en SQLCMD installeren en installeer vervolgens Hallo PHP-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="23189-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="23189-115">Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="23189-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="23189-116">**Ubuntu**: Installeer PHP en andere vereiste pakketten en installatie Hallo PHP-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="23189-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="23189-117">Zie [stap 1.2 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="23189-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="23189-118">**Windows**: Installeer Hallo nieuwste versie van PHP voor IIS Express, de nieuwste versie van Microsoft-Drivers voor SQL Server in IIS Express, Chocolatey Hallo ODBC-stuurprogramma en SQLCMD Hallo.</span><span class="sxs-lookup"><span data-stu-id="23189-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="23189-119">Zie [stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="23189-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="23189-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="23189-120">SQL server connection information</span></span>

<span data-ttu-id="23189-121">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="23189-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="23189-122">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="23189-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="23189-123">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="23189-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="23189-124">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="23189-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="23189-125">Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="23189-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="23189-126">U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.</span><span class="sxs-lookup"><span data-stu-id="23189-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="23189-128">Als u uw aanmeldingsgegevens server vergeet, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="23189-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="23189-129">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="23189-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="23189-130">Maak een nieuw bestand in uw favoriete teksteditor **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="23189-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="23189-131">Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="23189-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="23189-132">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="23189-132">Run hello code</span></span>

1. <span data-ttu-id="23189-133">Voer bij de opdrachtprompt Hallo Hallo opdrachten na:</span><span class="sxs-lookup"><span data-stu-id="23189-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="23189-134">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="23189-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23189-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="23189-135">Next steps</span></span>
- [<span data-ttu-id="23189-136">Uw eerste Azure SQL-database ontwerpen</span><span class="sxs-lookup"><span data-stu-id="23189-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="23189-137">Microsoft PHP-stuurprogramma's voor SQL Server</span><span class="sxs-lookup"><span data-stu-id="23189-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="23189-138">Problemen melden of vragen stellen</span><span class="sxs-lookup"><span data-stu-id="23189-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
