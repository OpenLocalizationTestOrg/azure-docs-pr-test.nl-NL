---
title: aaaUse Ruby tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Ruby toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="68eac-103">Ruby tooquery een Azure SQL database gebruiken</span><span class="sxs-lookup"><span data-stu-id="68eac-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="68eac-104">Deze zelfstudie laat zien hoe toouse [Ruby](https://www.ruby-lang.org) toocreate een programma tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.</span><span class="sxs-lookup"><span data-stu-id="68eac-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68eac-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="68eac-105">Prerequisites</span></span>

<span data-ttu-id="68eac-106">toocomplete dit snelle zelfstudie starten, zorg er Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="68eac-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="68eac-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="68eac-107">An Azure SQL database.</span></span> <span data-ttu-id="68eac-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="68eac-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="68eac-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="68eac-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="68eac-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="68eac-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="68eac-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="68eac-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="68eac-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="68eac-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="68eac-113">U hebt Ruby en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="68eac-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="68eac-114">**Mac OS**: installeer Homebrew, installeer rbenv en ruby-build, installeer Ruby en installeer vervolgens FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="68eac-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="68eac-115">Zie [Stap 1.2, 1.3, 1.4 en 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="68eac-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="68eac-116">**Ubuntu**: installeer de vereisten voor Ruby, installeer rbenv en ruby-build, installeer Ruby en installeer vervolgens FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="68eac-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="68eac-117">Zie [Stap 1.2, 1.3, 1.4 en 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="68eac-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="68eac-118">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="68eac-118">SQL server connection information</span></span>

<span data-ttu-id="68eac-119">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="68eac-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="68eac-120">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="68eac-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="68eac-121">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68eac-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68eac-122">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="68eac-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="68eac-123">Op Hallo **overzicht** pagina voor uw database, controleert u de volledig gekwalificeerde servernaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="68eac-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="68eac-124">U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie, zoals wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="68eac-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="68eac-126">Als u Hallo aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="68eac-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68eac-127">U moet beschikken over een firewallregel voor het openbare IP-adres Hallo van Hallo-computer waarop u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="68eac-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="68eac-128">Als u zich op een andere computer of een ander openbaar IP-adres hebben, maakt u een [serverniveau firewall-regel met Azure-portal Hallo](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="68eac-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="68eac-129">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="68eac-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="68eac-130">Maak een nieuw bestand in uw favoriete teksteditor **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="68eac-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="68eac-131">Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="68eac-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a><span data-ttu-id="68eac-132">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="68eac-132">Run hello code</span></span>

1. <span data-ttu-id="68eac-133">Voer bij de opdrachtprompt Hallo Hallo opdrachten na:</span><span class="sxs-lookup"><span data-stu-id="68eac-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="68eac-134">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="68eac-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="68eac-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68eac-135">Next Steps</span></span>
- [<span data-ttu-id="68eac-136">Uw eerste Azure SQL-database ontwerpen</span><span class="sxs-lookup"><span data-stu-id="68eac-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="68eac-137">GitHub-opslagplaats voor TinyTDS</span><span class="sxs-lookup"><span data-stu-id="68eac-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="68eac-138">Problemen melden of vragen over TinyTDS stellen</span><span class="sxs-lookup"><span data-stu-id="68eac-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="68eac-139">Ruby-stuurprogramma's voor SQL Server</span><span class="sxs-lookup"><span data-stu-id="68eac-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
