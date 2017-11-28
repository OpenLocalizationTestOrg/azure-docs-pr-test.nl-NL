---
title: Via Java verbinding maken met Azure Database voor MySQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van Java-code dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor MySQL-database.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: 6ffcf3b38a3d868dfa10ea2e2a9d097441387d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="dd222-103">Azure Database voor MySQL: Java gebruiken om verbinding te maken en gegevens op te vragen</span><span class="sxs-lookup"><span data-stu-id="dd222-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="dd222-104">In deze snelstartgids ziet u hoe u met behulp van een Java-toepassing verbinding maakt met een Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="dd222-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="dd222-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="dd222-106">In de stappen van dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met Java, maar geen ervaring hebt met het werken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd222-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dd222-107">Prerequisites</span></span>
<span data-ttu-id="dd222-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="dd222-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="dd222-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dd222-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="dd222-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd222-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="dd222-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dd222-111">You also need to:</span></span>
- <span data-ttu-id="dd222-112">Het JDBC-stuurprogramma [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) downloaden</span><span class="sxs-lookup"><span data-stu-id="dd222-112">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="dd222-113">Het JDBC jar-bestand (bijvoorbeeld mysql-connector-java-5.1.42-bin.jar) opnemen in het klassepad van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="dd222-113">Include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="dd222-114">Als u hier problemen mee ervaart, raadpleegt u de documentatie van uw omgeving voor informatie over de klassepaden, zoals [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) of [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="dd222-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="dd222-115">Zorg dat de beveiliging van uw Azure Database voor MySQL-verbinding is geconfigureerd met de firewall geopend en SSL-instellingen aangepast. Anders kan de toepassing geen maken.</span><span class="sxs-lookup"><span data-stu-id="dd222-115">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="dd222-116">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="dd222-116">Get connection information</span></span>
<span data-ttu-id="dd222-117">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="dd222-118">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="dd222-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="dd222-119">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd222-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dd222-120">Klik in het linkerdeelvenster op **Alle resources** en zoek vervolgens naar de server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="dd222-120">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="dd222-121">Klik op de servernaam.</span><span class="sxs-lookup"><span data-stu-id="dd222-121">Click the server name.</span></span>
4. <span data-ttu-id="dd222-122">Selecteer de pagina **Eigenschappen** van de server.</span><span class="sxs-lookup"><span data-stu-id="dd222-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="dd222-123">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="dd222-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="dd222-124">![Naam van Azure Database voor MySQL-server](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="dd222-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="dd222-125">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="dd222-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="dd222-126">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="dd222-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="dd222-127">Gebruik de volgende code om verbinding te maken en de gegevens te laden met de functie met een SQL-instructie **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="dd222-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="dd222-128">De methode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) wordt gebruikt om verbinding te maken met MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="dd222-129">De methoden [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) en execute() worden gebruikt om de tabel te verwijderen en te maken.</span><span class="sxs-lookup"><span data-stu-id="dd222-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="dd222-130">Het object prepareStatement wordt gebruikt voor het bouwen van de INSERT-opdrachten, waarbij setString() en setInt() worden gebruikt om de parameterwaarden te koppelen.</span><span class="sxs-lookup"><span data-stu-id="dd222-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="dd222-131">Met de methode executeUpdate() wordt de opdracht voor elke set parameters uitgevoerd om de waarden in te voegen.</span><span class="sxs-lookup"><span data-stu-id="dd222-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="dd222-132">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="dd222-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="dd222-133">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="dd222-133">Read data</span></span>
<span data-ttu-id="dd222-134">Gebruik de volgende code om de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="dd222-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="dd222-135">De methode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) wordt gebruikt om verbinding te maken met MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="dd222-136">De methoden [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) en executeQuery() worden gebruikt om verbinding te maken en de SELECT-instructie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="dd222-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="dd222-137">De resultaten worden verwerkt met behulp van een [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html)-object.</span><span class="sxs-lookup"><span data-stu-id="dd222-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="dd222-138">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="dd222-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="dd222-139">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="dd222-139">Update data</span></span>
<span data-ttu-id="dd222-140">Gebruik de volgende code om de gegevens te wijzigen met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="dd222-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="dd222-141">De methode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) wordt gebruikt om verbinding te maken met MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="dd222-142">De methoden [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) en executeUpdate() worden gebruikt om de UPDATE-instructie voor te bereiden en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="dd222-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="dd222-143">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="dd222-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="dd222-144">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="dd222-144">Delete data</span></span>
<span data-ttu-id="dd222-145">Gebruik de volgende code om de gegevens te verwijderen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="dd222-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="dd222-146">De methode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) wordt gebruikt om verbinding te maken met MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd222-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="dd222-147">De methoden [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) en executeUpdate() worden gebruikt om de UPDATE-instructie voor te bereiden en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="dd222-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="dd222-148">Vervang de parameters voor host, database, gebruiker en wachtwoord door de waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="dd222-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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

## <a name="next-steps"></a><span data-ttu-id="dd222-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dd222-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="dd222-150">Uw MySQL-database migreren naar Azure Database voor MySQL met behulp van dumpen en terugzetten</span><span class="sxs-lookup"><span data-stu-id="dd222-150">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
