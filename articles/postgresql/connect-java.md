---
title: Met Java verbinding maken met Azure Database voor PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van Java-code die u kunt gebruiken om verbinding te maken met en query's uit te voeren voor gegevens uit een Azure Database voor PostgreSQL.
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
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="aa7ef-103">Azure Database voor PostgreSQL: Java gebruiken om verbinding te maken en query's voor gegevens uit te voeren</span><span class="sxs-lookup"><span data-stu-id="aa7ef-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="aa7ef-104">In deze snelstartgids ziet u hoe u met behulp van een Java-toepassing verbinding maakt met een Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="aa7ef-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="aa7ef-106">In de stappen van dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Java, maar geen ervaring hebt met het werken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa7ef-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa7ef-107">Prerequisites</span></span>
<span data-ttu-id="aa7ef-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="aa7ef-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="aa7ef-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="aa7ef-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="aa7ef-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aa7ef-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="aa7ef-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="aa7ef-111">You also need to:</span></span>
- <span data-ttu-id="aa7ef-112">Download het [PostgreSQL JDBC-stuurprogramma](https://jdbc.postgresql.org/download.html) dat hoort bij uw versie van Java en de Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="aa7ef-113">Neem het PostgreSQL JDBC jar-bestand (bijvoorbeeld postgresql-42.1.1.jar) op in het klassepad van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="aa7ef-114">Zie de [gegevens van het klassepad](https://jdbc.postgresql.org/documentation/head/classpath.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="aa7ef-115">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="aa7ef-115">Get connection information</span></span>
<span data-ttu-id="aa7ef-116">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="aa7ef-117">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="aa7ef-118">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aa7ef-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aa7ef-119">Klik in het menu links in Azure Portal op **Alle resources** en zoek de server die u hebt gemaakt (bijvoorbeeld **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="aa7ef-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="aa7ef-120">Klik op de servernaam **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="aa7ef-121">Selecteer de pagina **Overzicht** van de server.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="aa7ef-122">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="aa7ef-123">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="aa7ef-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="aa7ef-124">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="aa7ef-125">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="aa7ef-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="aa7ef-126">Gebruik de volgende code om verbinding te maken en de gegevens te laden met de functie met een SQL-instructie **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="aa7ef-127">De methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) en [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) worden gebruikt om verbinding maken met de tabel, de tabel neer te zetten en de tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="aa7ef-128">Het object [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) wordt gebruikt voor het bouwen van de INSERT-opdrachten, waarbij setString() en setInt() worden gebruikt om de parameterwaarden te koppelen.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="aa7ef-129">Met de methode [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) wordt de opdracht voor elke set parameters uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="aa7ef-130">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="aa7ef-131">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="aa7ef-131">Read data</span></span>
<span data-ttu-id="aa7ef-132">Gebruik de volgende code om de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="aa7ef-133">De methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) en [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) worden gebruikt om verbinding te maken met de SELECT-instructie en deze te maken en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="aa7ef-134">De resultaten worden verwerkt met behulp van een [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html)-object.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="aa7ef-135">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="aa7ef-136">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="aa7ef-136">Update data</span></span>
<span data-ttu-id="aa7ef-137">Gebruik de volgende code om de gegevens te wijzigen met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="aa7ef-138">De methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) en [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) worden gebruikt om verbinding te maken en de UPDATE-instructie voor te bereiden en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="aa7ef-139">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="aa7ef-140">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="aa7ef-140">Delete data</span></span>
<span data-ttu-id="aa7ef-141">Gebruik de volgende code om de gegevens te verwijderen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="aa7ef-142">De methoden [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) en [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) worden gebruikt om verbinding te maken en de UPDATE-instructie voor te bereiden, uit te voeren en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="aa7ef-143">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="aa7ef-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="aa7ef-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa7ef-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="aa7ef-145">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="aa7ef-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
