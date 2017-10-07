---
title: aaaUse Node.js tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Node.js toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
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
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="74a33-103">Node.js tooquery een Azure SQL database gebruiken</span><span class="sxs-lookup"><span data-stu-id="74a33-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="74a33-104">Deze zelfstudie laat zien hoe toouse [Node.js](https://nodejs.org/en/) toocreate een programma tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.</span><span class="sxs-lookup"><span data-stu-id="74a33-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74a33-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="74a33-105">Prerequisites</span></span>

<span data-ttu-id="74a33-106">toocomplete dit snelle zelfstudie begint, controleert u of hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="74a33-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="74a33-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="74a33-107">An Azure SQL database.</span></span> <span data-ttu-id="74a33-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="74a33-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="74a33-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="74a33-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="74a33-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="74a33-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="74a33-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="74a33-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="74a33-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="74a33-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="74a33-113">U hebt Node.js en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="74a33-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="74a33-114">**Mac OS**: Homebrew en Node.js installeren en installeer vervolgens Hallo ODBC-stuurprogramma en SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="74a33-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="74a33-115">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="74a33-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="74a33-116">**Ubuntu**: Installeer Node.js en installeer vervolgens Hallo ODBC-stuurprogramma en SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="74a33-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="74a33-117">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="74a33-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="74a33-118">**Windows**: Chocolatey en Node.js installeren en installeer vervolgens Hallo ODBC-stuurprogramma en SQL cmd.exe</span><span class="sxs-lookup"><span data-stu-id="74a33-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="74a33-119">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="74a33-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="74a33-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="74a33-120">SQL server connection information</span></span>

<span data-ttu-id="74a33-121">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="74a33-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="74a33-122">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="74a33-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="74a33-123">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74a33-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="74a33-124">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="74a33-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="74a33-125">Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="74a33-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="74a33-126">U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.</span><span class="sxs-lookup"><span data-stu-id="74a33-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="74a33-128">Als u Hallo aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="74a33-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74a33-129">U moet beschikken over een firewallregel voor het openbare IP-adres Hallo van Hallo-computer waarop u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="74a33-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="74a33-130">Als u zich op een andere computer of een ander openbaar IP-adres hebben, maakt u een [serverniveau firewall-regel met Azure-portal Hallo](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="74a33-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="74a33-131">Een Node.js-project maken</span><span class="sxs-lookup"><span data-stu-id="74a33-131">Create a Node.js project</span></span>

<span data-ttu-id="74a33-132">Open een opdrachtprompt en maak een map met de naam *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="74a33-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="74a33-133">Navigeer toohello map u gemaakt en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="74a33-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="74a33-134">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="74a33-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="74a33-135">Maak een nieuw bestand in uw ontwikkelomgeving of favoriete teksteditor **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="74a33-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="74a33-136">Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="74a33-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
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

   // Attempt tooconnect and execute queries if connection goes through
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
      { console.log('Reading rows from hello Table...');

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

## <a name="run-hello-code"></a><span data-ttu-id="74a33-137">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="74a33-137">Run hello code</span></span>

1. <span data-ttu-id="74a33-138">Voer bij de opdrachtprompt Hallo Hallo opdrachten na:</span><span class="sxs-lookup"><span data-stu-id="74a33-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="74a33-139">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="74a33-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74a33-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74a33-140">Next steps</span></span>

- <span data-ttu-id="74a33-141">Meer informatie over Hallo [Microsoft Node.js Driver voor SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="74a33-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="74a33-142">Meer informatie over hoe te[en verbinding en een Azure SQL database met behulp van .NET core query](sql-database-connect-query-dotnet-core.md) op Windows/Linux/Mac OS.</span><span class="sxs-lookup"><span data-stu-id="74a33-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="74a33-143">Meer informatie over [aan de slag met .NET Core op Windows/Linux/Mac-OS, via de opdrachtregel Hallo](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="74a33-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="74a33-144">Meer informatie over hoe te[ontwerpen van uw eerste Azure SQL database met behulp van SSMS](sql-database-design-first-database.md) of [ontwerpen van uw eerste Azure SQL database met .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="74a33-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="74a33-145">Meer informatie over hoe te[Connect en query met SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="74a33-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="74a33-146">Meer informatie over hoe te[Connect en query met Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="74a33-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


