---
title: Verbinding maken met Database tooAzure voor PostgreSQL met Java | Microsoft Docs
description: Deze snelstartgids bevat een Java-codevoorbeeld kunt u een query over gegevens uit Azure-Database voor PostgreSQL en tooconnect gebruiken.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="6ad40-103">Azure-Database voor PostgreSQL: Java gebruiken tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="6ad40-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="6ad40-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor PostgreSQL met behulp van een Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ad40-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="6ad40-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="6ad40-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="6ad40-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen van u Java gebruikt, en dat u een nieuwe tooworking met Azure-Database voor PostgreSQL bent.</span><span class="sxs-lookup"><span data-stu-id="6ad40-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ad40-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ad40-107">Prerequisites</span></span>
<span data-ttu-id="6ad40-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6ad40-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="6ad40-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="6ad40-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="6ad40-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ad40-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="6ad40-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6ad40-111">You also need to:</span></span>
- <span data-ttu-id="6ad40-112">Hallo downloaden [PostgreSQL JDBC-stuurprogramma](https://jdbc.postgresql.org/download.html) die overeenkomt met uw versie van Java en Hallo Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6ad40-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="6ad40-113">Hallo PostgreSQL JDBC jar-bestand (bijvoorbeeld postgresql-42.1.1.jar) in uw toepassing klassepad opnemen.</span><span class="sxs-lookup"><span data-stu-id="6ad40-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="6ad40-114">Zie de [gegevens van het klassepad](https://jdbc.postgresql.org/documentation/head/classpath.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="6ad40-115">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="6ad40-115">Get connection information</span></span>
<span data-ttu-id="6ad40-116">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="6ad40-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="6ad40-117">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="6ad40-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6ad40-118">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ad40-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6ad40-119">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="6ad40-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="6ad40-120">Klik op de servernaam Hallo **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="6ad40-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="6ad40-121">Selecteer Hallo-server **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="6ad40-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="6ad40-122">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="6ad40-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6ad40-123">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="6ad40-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="6ad40-124">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ad40-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="6ad40-125">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="6ad40-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="6ad40-126">Gebruik Hallo code tooconnect en Hallo gegevens laden met behulp van de functie Hallo met na een **invoegen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="6ad40-127">Hallo methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), en [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) zijn gebruikte tooconnect verwijderen en Hallo tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="6ad40-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="6ad40-128">Hallo [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) -object is gebruikte toobuild Hallo insert-opdrachten, met setString() en setInt() toobind Hallo parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="6ad40-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="6ad40-129">Methode [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) wordt uitgevoerd Hallo opdracht voor elke set van parameters.</span><span class="sxs-lookup"><span data-stu-id="6ad40-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="6ad40-130">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="6ad40-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="6ad40-131">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="6ad40-131">Read data</span></span>
<span data-ttu-id="6ad40-132">Gebruik Hallo volgende code tooread Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="6ad40-133">Hallo methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), en [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) zijn gebruikte tooconnect maken en uitvoeren van Hallo select-instructie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="6ad40-134">Hallo resultaten worden verwerkt met behulp van een [resultatenset](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span><span class="sxs-lookup"><span data-stu-id="6ad40-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="6ad40-135">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="6ad40-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="6ad40-136">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="6ad40-136">Update data</span></span>
<span data-ttu-id="6ad40-137">Gebruik Hallo volgende code toochange Hallo gegevens met een **UPDATE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="6ad40-138">Hallo methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), en [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) gebruikte tooconnect zijn voorbereiden en voer de instructie update Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ad40-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="6ad40-139">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="6ad40-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="6ad40-140">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="6ad40-140">Delete data</span></span>
<span data-ttu-id="6ad40-141">Gebruik Hallo volgende code tooremove gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6ad40-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="6ad40-142">Hallo methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), en [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) gebruikte tooconnect zijn voorbereiden en voer de instructie delete Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ad40-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="6ad40-143">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="6ad40-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="6ad40-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ad40-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6ad40-145">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="6ad40-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
