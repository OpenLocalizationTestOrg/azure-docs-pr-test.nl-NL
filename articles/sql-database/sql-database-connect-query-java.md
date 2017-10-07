---
title: aaaUse Java tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Java toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="ebbd9-103">Gebruik van Java-tooquery een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="ebbd9-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="ebbd9-104">Deze snel starten laat zien hoe toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens vervolgens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebbd9-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ebbd9-105">Prerequisites</span></span>

<span data-ttu-id="ebbd9-106">toocomplete dit snelle zelfstudie starten, zorg er Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="ebbd9-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-107">An Azure SQL database.</span></span> <span data-ttu-id="ebbd9-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="ebbd9-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="ebbd9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="ebbd9-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="ebbd9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="ebbd9-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebbd9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="ebbd9-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="ebbd9-113">U hebt Java en verwante software voor uw besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="ebbd9-114">**Mac OS**: installeer Homebrew en Java, en installeer vervolgens Maven.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="ebbd9-115">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="ebbd9-116">**Ubuntu**: Hallo Java Development Kit installeert en Maven.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="ebbd9-117">Zie [Stap 1.2, 1.3 en 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="ebbd9-118">**Windows**: Hallo Java Development Kit en Maven installeren.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="ebbd9-119">Zie [Stap 1.2 en 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="ebbd9-120">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="ebbd9-120">SQL server connection information</span></span>

<span data-ttu-id="ebbd9-121">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="ebbd9-122">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="ebbd9-123">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ebbd9-124">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="ebbd9-125">Op Hallo **overzicht** pagina voor uw database, controleert u de volledig gekwalificeerde servernaam Hallo zoals weergegeven in Hallo volgende afbeelding: U kunt de muisaanwijzer op Hallo server name toobring up Hallo **toocopy klikt u op** optie.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="ebbd9-127">Als u uw aanmeldingsgegevens server vergeet, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="ebbd9-128">Indien nodig, Hallo-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="ebbd9-129">**Maven-project en -afhankelijkheden maken**</span><span class="sxs-lookup"><span data-stu-id="ebbd9-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="ebbd9-130">Maken van Hallo terminal, een nieuw Maven-project aangeroepen **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="ebbd9-131">Voer **Y** in wanneer u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="ebbd9-132">Wijzig de directory te**sqltest** en open ***pom.xml*** met uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="ebbd9-133">Hallo toevoegen **Microsoft JDBC-stuurprogramma voor SQL Server** tooyour de afhankelijkheden van project met behulp van Hallo volgende code:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="ebbd9-134">Ook ***pom.xml***, Hallo na eigenschappen tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="ebbd9-135">Als u een sectie met eigenschappen niet hebt, kunt u deze na het Hallo-afhankelijkheden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="ebbd9-136">Sla ***pom.xml*** op en sluit het af.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="ebbd9-137">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="ebbd9-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="ebbd9-138">U hebt al een bestand met de naam ***App.java*** in uw Maven-project dat zich bevindt in:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="ebbd9-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="ebbd9-139">Open Hallo-bestand en vervang de inhoud door Hallo volgende code en Hallo juiste waarden toevoegen voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="ebbd9-140">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ebbd9-140">Run hello code</span></span>

1. <span data-ttu-id="ebbd9-141">Voer bij de opdrachtprompt Hallo Hallo opdrachten na:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="ebbd9-142">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ebbd9-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebbd9-143">Next steps</span></span>
- [<span data-ttu-id="ebbd9-144">Uw eerste Azure SQL-database ontwerpen</span><span class="sxs-lookup"><span data-stu-id="ebbd9-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="ebbd9-145">Microsoft JDBC-stuurprogramma voor SQL Server</span><span class="sxs-lookup"><span data-stu-id="ebbd9-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="ebbd9-146">Problemen melden/vragen stellen</span><span class="sxs-lookup"><span data-stu-id="ebbd9-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

