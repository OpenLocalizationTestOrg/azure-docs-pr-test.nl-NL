---
title: Verbinding maken met Database tooAzure voor MySQL met Java | Microsoft Docs
description: Deze snelstartgids bevat een Java-codevoorbeeld u kunt gebruiken tooconnect en opvragen van gegevens uit een Azure-Database voor de MySQL-database.
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
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="2c8ca-103">Azure MySQL-Database: Java gebruiken tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="2c8ca-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="2c8ca-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor MySQL met behulp van een Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="2c8ca-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="2c8ca-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen van u Java gebruikt, en dat u een nieuwe tooworking met Azure-Database voor MySQL bent.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c8ca-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c8ca-107">Prerequisites</span></span>
<span data-ttu-id="2c8ca-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2c8ca-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2c8ca-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2c8ca-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2c8ca-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2c8ca-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="2c8ca-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="2c8ca-111">You also need to:</span></span>
- <span data-ttu-id="2c8ca-112">Hallo JDBC-stuurprogramma downloaden [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="2c8ca-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="2c8ca-113">Hallo JDBC jar-bestand (bijvoorbeeld mysql-connector-java-5.1.42-bin.jar) opnemen in uw toepassing klassepad.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="2c8ca-114">Als u hier problemen mee ervaart, raadpleegt u de documentatie van uw omgeving voor informatie over de klassepaden, zoals [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) of [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="2c8ca-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="2c8ca-115">Zorg ervoor dat uw Azure-Database voor beveiliging van de MySQL-verbinding is geconfigureerd met Hallo firewall is geopend en SSL-instellingen is voor uw toepassing tooconnect is aangepast.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2c8ca-116">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="2c8ca-116">Get connection information</span></span>
<span data-ttu-id="2c8ca-117">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="2c8ca-118">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2c8ca-119">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2c8ca-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2c8ca-120">Klik in het linkerdeelvenster Hallo **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="2c8ca-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="2c8ca-121">Klik op Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-121">Click hello server name.</span></span>
4. <span data-ttu-id="2c8ca-122">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="2c8ca-123">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2c8ca-124">![Naam van Azure Database voor MySQL-server](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="2c8ca-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="2c8ca-125">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2c8ca-126">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="2c8ca-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="2c8ca-127">Gebruik Hallo code tooconnect en Hallo gegevens laden met behulp van de functie Hallo met na een **invoegen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="2c8ca-128">Hallo [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) methode gebruikte tooconnect tooMySQL is.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="2c8ca-129">Methoden [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) en execute() gebruikte toodrop zijn en Hallo-tabel maken.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="2c8ca-130">Hallo prepareStatement-object is gebruikte toobuild Hallo insert-opdrachten, met setString() en setInt() toobind Hallo parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="2c8ca-131">Methode executeUpdate() Hallo-opdracht voor elke set parameters tooinsert Hallo waarden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="2c8ca-132">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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

## <a name="read-data"></a><span data-ttu-id="2c8ca-133">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="2c8ca-133">Read data</span></span>
<span data-ttu-id="2c8ca-134">Gebruik Hallo volgende code tooread Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="2c8ca-135">Hallo [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) methode gebruikte tooconnect tooMySQL is.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="2c8ca-136">Hallo methoden [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) en executeQuery() gebruikte tooconnect zijn en Hallo select-instructie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="2c8ca-137">Hallo resultaten worden verwerkt met behulp van een [resultatenset](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="2c8ca-138">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="2c8ca-139">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="2c8ca-139">Update data</span></span>
<span data-ttu-id="2c8ca-140">Gebruik Hallo volgende code toochange Hallo gegevens met een **UPDATE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="2c8ca-141">Hallo [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) methode gebruikte tooconnect tooMySQL is.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="2c8ca-142">Hallo methoden [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) en executeUpdate() gebruikte tooprepare zijn en Hallo update-instructie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="2c8ca-143">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
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

## <a name="delete-data"></a><span data-ttu-id="2c8ca-144">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="2c8ca-144">Delete data</span></span>
<span data-ttu-id="2c8ca-145">Gebruik Hallo volgende code tooremove gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="2c8ca-146">Hallo [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) methode gebruikte tooconnect tooMySQL is.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="2c8ca-147">Hallo methoden [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) en executeUpdate() gebruikte tooprepare zijn en Hallo update-instructie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="2c8ca-148">Vervangen door Hallo host, database, gebruiker en wachtwoordparameters Hallo-waarden die u hebt opgegeven tijdens het maken van uw eigen server en database.</span><span class="sxs-lookup"><span data-stu-id="2c8ca-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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
        
        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
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

## <a name="next-steps"></a><span data-ttu-id="2c8ca-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c8ca-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2c8ca-150">Migreren van uw MySQL-database tooAzure Database voor MySQL met behulp van de dump en terugzetten</span><span class="sxs-lookup"><span data-stu-id="2c8ca-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
