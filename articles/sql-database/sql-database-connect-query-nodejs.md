---
title: Node.js gebruiken om een query uit te voeren voor een Azure SQL-database | Microsoft Docs
description: In dit onderwerp ziet u hoe u Node.js gebruikt om een programma te maken dat is verbonden met een Azure SQL-database, en hoe u een query voor deze database uitvoert met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 1907a95df9132c059d7985b6d5cd913536bf3403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-nodejs-to-query-an-azure-sql-database"></a><span data-ttu-id="dc341-103">Node.js gebruiken om een query uit te voeren voor een Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="dc341-103">Use Node.js to query an Azure SQL database</span></span>

<span data-ttu-id="dc341-104">In deze beknopte zelfstudie wordt gedemonstreerd hoe u [Node.js](https://nodejs.org/en/) gebruikt om een programma te maken dat verbinding maakt met een Azure SQL-database, en hoe u Transact-SQL-instructies gebruikt om een query uit te voeren voor gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc341-104">This quick start tutorial demonstrates how to use [Node.js](https://nodejs.org/en/) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc341-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dc341-105">Prerequisites</span></span>

<span data-ttu-id="dc341-106">Zorg ervoor dat u over het volgende beschikt om deze beknopte zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="dc341-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="dc341-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="dc341-107">An Azure SQL database.</span></span> <span data-ttu-id="dc341-108">In deze zelfstudie worden de resources gebruikt die u hebt gemaakt in een van deze Quick Starts:</span><span class="sxs-lookup"><span data-stu-id="dc341-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="dc341-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="dc341-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="dc341-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="dc341-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="dc341-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc341-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="dc341-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor het openbare IP-adres van de computer die u gebruikt voor deze beknopte zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dc341-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="dc341-113">U hebt Node.js en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc341-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="dc341-114">**MacOS**: installeer Homebrew en Node.js, en installeer vervolgens het ODBC-stuurprogramma en SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="dc341-114">**MacOS**: Install Homebrew and Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="dc341-115">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="dc341-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="dc341-116">**Ubuntu**: installeer Node.js en installeer vervolgens het ODBC-stuurprogramma en SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="dc341-116">**Ubuntu**: Install Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="dc341-117">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="dc341-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="dc341-118">**Windows**: installeer Chocolatey en Node.js, en installeer vervolgens het ODBC-stuurprogramma en SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="dc341-118">**Windows**: Install Chocolatey and Node.js, and then install the ODBC driver and SQL CMD.</span></span> <span data-ttu-id="dc341-119">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="dc341-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="dc341-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="dc341-120">SQL server connection information</span></span>

<span data-ttu-id="dc341-121">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="dc341-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="dc341-122">U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.</span><span class="sxs-lookup"><span data-stu-id="dc341-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="dc341-123">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dc341-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dc341-124">Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="dc341-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="dc341-125">Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de volgende afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dc341-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="dc341-126">U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen.</span><span class="sxs-lookup"><span data-stu-id="dc341-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="dc341-128">Als u de aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven en, indien nodig, het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="dc341-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc341-129">U moet een firewallregel hebben ingesteld voor het openbare IP-adres van de computer waarop u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="dc341-129">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="dc341-130">Als u een andere computer gebruikt of een ander openbaar IP-adres hebt, maakt u een [firewallregel op serverniveau met behulp van Azure Portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="dc341-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="dc341-131">Een Node.js-project maken</span><span class="sxs-lookup"><span data-stu-id="dc341-131">Create a Node.js project</span></span>

<span data-ttu-id="dc341-132">Open een opdrachtprompt en maak een map met de naam *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="dc341-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="dc341-133">Navigeer naar de map die u hebt gemaakt, en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="dc341-133">Navigate to the folder you created and run the following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="dc341-134">Code invoegen om een query uit te voeren voor een SQL-database</span><span class="sxs-lookup"><span data-stu-id="dc341-134">Insert code to query SQL database</span></span>

1. <span data-ttu-id="dc341-135">Maak een nieuw bestand in uw ontwikkelomgeving of favoriete teksteditor **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="dc341-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="dc341-136">Vervang de inhoud door de volgende code en voeg de juiste waarden toe voor de server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="dc341-136">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection to database
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt to connect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from the Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-the-code"></a><span data-ttu-id="dc341-137">De code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="dc341-137">Run the code</span></span>

1. <span data-ttu-id="dc341-138">Voer bij de opdrachtprompt de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="dc341-138">At the command prompt, run the following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="dc341-139">Controleer of de bovenste 20 rijen worden geretourneerd, en sluit vervolgens het toepassingsvenster.</span><span class="sxs-lookup"><span data-stu-id="dc341-139">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc341-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc341-140">Next steps</span></span>

- <span data-ttu-id="dc341-141">Meer informatie over het [Microsoft-stuurprogramma Node.js voor SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="dc341-141">Learn about the [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="dc341-142">Meer informatie over [verbinding maken met en een query uitvoeren voor een Azure SQL-database met behulp van .NET Core](sql-database-connect-query-dotnet-core.md) in Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="dc341-142">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="dc341-143">Meer informatie over [Aan de slag met .NET Core in Windows/Linux/macOS met behulp van de opdrachtregel](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="dc341-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="dc341-144">Meer informatie over [Uw eerste Azure SQL-database ontwerpen met behulp van SSMS](sql-database-design-first-database.md) of [Uw eerste Azure SQL-database ontwerpen met behulp van .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="dc341-144">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="dc341-145">Meer informatie over [Verbinding maken en query's uitvoeren met SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="dc341-145">Learn how to [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="dc341-146">Meer informatie over [Verbinding maken en query's uitvoeren met Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="dc341-146">Learn how to [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


