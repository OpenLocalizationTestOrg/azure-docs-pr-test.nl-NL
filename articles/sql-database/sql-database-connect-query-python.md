---
title: aaaUse Python tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Python toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="15d40-103">Gebruik van Python tooquery een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="15d40-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="15d40-104">Deze snel starten laat zien hoe toouse [Python](https://python.org) tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.</span><span class="sxs-lookup"><span data-stu-id="15d40-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15d40-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="15d40-105">Prerequisites</span></span>

<span data-ttu-id="15d40-106">toocomplete dit snelle zelfstudie begint, controleert u of hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="15d40-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="15d40-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="15d40-107">An Azure SQL database.</span></span> <span data-ttu-id="15d40-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="15d40-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="15d40-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="15d40-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="15d40-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="15d40-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="15d40-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="15d40-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="15d40-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="15d40-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="15d40-113">U hebt Python en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="15d40-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="15d40-114">**Mac OS**: Homebrew installeren en Python, Hallo ODBC-stuurprogramma en SQLCMD installeren en installeer vervolgens Hallo Python-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="15d40-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="15d40-115">Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="15d40-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="15d40-116">**Ubuntu**: Python installeren en andere vereiste pakketten en installatie Hallo Python-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="15d40-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="15d40-117">Zie [stap 1.2, 1.3 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="15d40-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="15d40-118">**Windows**: Hallo nieuwste versie van Python (omgevingsvariabele is nu geconfigureerd voor u) installeren, Hallo ODBC-stuurprogramma en SQLCMD installeren en installeer vervolgens Hallo Python-stuurprogramma voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="15d40-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="15d40-119">Zie [Stap 1.2, 1.3 en 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="15d40-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="15d40-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="15d40-120">SQL server connection information</span></span>

<span data-ttu-id="15d40-121">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="15d40-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="15d40-122">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="15d40-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="15d40-123">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="15d40-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="15d40-124">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="15d40-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="15d40-125">Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="15d40-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="15d40-126">U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.</span><span class="sxs-lookup"><span data-stu-id="15d40-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="15d40-128">Als u uw aanmeldingsgegevens server vergeet, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="15d40-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="15d40-129">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="15d40-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="15d40-130">Maak een nieuw bestand in uw favoriete teksteditor **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="15d40-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="15d40-131">Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="15d40-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="15d40-132">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="15d40-132">Run hello code</span></span>

1. <span data-ttu-id="15d40-133">Voer bij de opdrachtprompt Hallo Hallo opdrachten na:</span><span class="sxs-lookup"><span data-stu-id="15d40-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="15d40-134">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="15d40-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15d40-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15d40-135">Next steps</span></span>

- [<span data-ttu-id="15d40-136">Uw eerste Azure SQL-database ontwerpen</span><span class="sxs-lookup"><span data-stu-id="15d40-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="15d40-137">Microsoft Python-stuurprogramma's voor SQL Server</span><span class="sxs-lookup"><span data-stu-id="15d40-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="15d40-138">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="15d40-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

