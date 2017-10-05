---
title: Met PHP verbinding maken met Azure Database voor PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van PHP-code dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="a004f-103">Azure Database voor PostgreSQL: PHP gebruiken om verbinding te maken en gegevens op te vragen</span><span class="sxs-lookup"><span data-stu-id="a004f-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="a004f-104">In deze snelstartgids ziet u hoe u met behulp van een [PHP](http://php.net/manual/intro-whatis.php)-toepassing verbinding maakt met een Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="a004f-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a004f-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="a004f-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met PHP, maar geen ervaring hebt met het werken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a004f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a004f-107">Prerequisites</span></span>
<span data-ttu-id="a004f-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a004f-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="a004f-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="a004f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="a004f-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a004f-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="a004f-111">PHP installeren</span><span class="sxs-lookup"><span data-stu-id="a004f-111">Install PHP</span></span>
<span data-ttu-id="a004f-112">Installeer PHP op uw eigen server of maak een Azure-[web-app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) die PHP omvat.</span><span class="sxs-lookup"><span data-stu-id="a004f-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="a004f-113">Windows</span><span class="sxs-lookup"><span data-stu-id="a004f-113">Windows</span></span>
- <span data-ttu-id="a004f-114">[PHP versie 7.1.4 non-thread safe (x64)](http://windows.php.net/download#php-7.1) downloaden</span><span class="sxs-lookup"><span data-stu-id="a004f-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="a004f-115">PHP installeren en de [PHP-handleiding](http://php.net/manual/install.windows.php) bekijken voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="a004f-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="a004f-116">In de code wordt de klasse **pgsql** (ext/php_pgsql.dll) gebruikt; deze is opgenomen in de PHP-installatie.</span><span class="sxs-lookup"><span data-stu-id="a004f-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="a004f-117">Schakel de **pgsql**-extensie in door het configuratiebestand php.ini te bewerken. Dit staat gewoonlijk in `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="a004f-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="a004f-118">Het configuratiebestand moet een regel bevatten met de tekst `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="a004f-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="a004f-119">Als deze niet wordt weergegeven, voegt u de tekst toe en slaat u het bestand op.</span><span class="sxs-lookup"><span data-stu-id="a004f-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="a004f-120">Als de tekst aanwezig is, maar met behulp van het voorvoegsel puntkomma als opmerking is gemarkeerd, haalt u de puntkomma weg zodat de tekst geen opmerking meer is.</span><span class="sxs-lookup"><span data-stu-id="a004f-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="a004f-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="a004f-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="a004f-122">[PHP versie 7.1.4 non-thread safe (x64)](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="a004f-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="a004f-123">PHP installeren en de [PHP-handleiding](http://php.net/manual/install.unix.php) bekijken voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="a004f-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="a004f-124">In de code wordt de **pgsql** klasse (php_pgsql.so) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a004f-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="a004f-125">Installeer deze door `sudo apt-get install php-pgsql` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a004f-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="a004f-126">Schakel de **pgsql**-extensie in door het configuratiebestand php.ini te bewerken. Dit staat doorgaans in `/etc/php/7.0/mods-available/pgsql.ini`.</span><span class="sxs-lookup"><span data-stu-id="a004f-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="a004f-127">Het configuratiebestand moet een regel bevatten met de tekst `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="a004f-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="a004f-128">Als deze niet wordt weergegeven, voegt u de tekst toe en slaat u het bestand op.</span><span class="sxs-lookup"><span data-stu-id="a004f-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="a004f-129">Als de tekst aanwezig is, maar met behulp van het voorvoegsel puntkomma als opmerking is gemarkeerd, haalt u de puntkomma weg zodat de tekst geen opmerking meer is.</span><span class="sxs-lookup"><span data-stu-id="a004f-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="a004f-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="a004f-130">MacOS</span></span>
- <span data-ttu-id="a004f-131">[PHP versie 7.1.4](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="a004f-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="a004f-132">PHP installeren en de [PHP-handleiding](http://php.net/manual/install.macosx.php) bekijken voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="a004f-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a004f-133">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="a004f-133">Get connection information</span></span>
<span data-ttu-id="a004f-134">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a004f-135">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="a004f-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a004f-136">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a004f-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a004f-137">Klik in het menu links in Azure Portal op **Alle resources** en zoek de server die u hebt gemaakt (bijvoorbeeld **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="a004f-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="a004f-138">Klik op de servernaam **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="a004f-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="a004f-139">Selecteer de pagina **Overzicht** van de server.</span><span class="sxs-lookup"><span data-stu-id="a004f-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="a004f-140">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="a004f-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a004f-141">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="a004f-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="a004f-142">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="a004f-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="a004f-143">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="a004f-143">Connect and create a table</span></span>
<span data-ttu-id="a004f-144">Gebruik de volgende code om een tabel te verbinden en te maken met de SQL-instructie **CREATE TABLE**, gevolgd door **INSERT INTO**-instructies om rijen in de tabel toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a004f-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="a004f-145">In de code wordt methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a004f-146">Vervolgens wordt methode [pg_query()](http://php.net/manual/en/function.pg-query.php) een aantal keer aangeroepen om diverse opdrachten uit te voeren, en wordt [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) aangeroepen om de details te controleren telkens wanneer er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a004f-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="a004f-147">Vervolgens wordt methode [pg_close()](http://php.net/manual/en/function.pg-close.php) aangeroepen om de verbinding te sluiten.</span><span class="sxs-lookup"><span data-stu-id="a004f-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="a004f-148">Vervang de parameters `$host`, `$database`, `$user` en `$password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="a004f-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="a004f-149">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="a004f-149">Read data</span></span>
<span data-ttu-id="a004f-150">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="a004f-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="a004f-151">In de code wordt methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a004f-152">Vervolgens wordt methode [pg_query()](http://php.net/manual/en/function.pg-query.php) aangeroepen om de SELECT-opdracht uit te voeren, waarbij de resultaten worden vastgehouden in een resultatenset, en wordt [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) uitgevoerd om de details te controleren als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a004f-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="a004f-153">Om de resultatenset te lezen, wordt methode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) in een lus aangeroepen, eenmaal per rij, en worden de rijgegevens opgehaald in een matrix `$row`, met één waarde per kolom in elke matrixpositie.</span><span class="sxs-lookup"><span data-stu-id="a004f-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="a004f-154">Methode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) wordt aangeroepen om de resultatenset vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="a004f-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="a004f-155">Vervolgens wordt methode [pg_close()](http://php.net/manual/en/function.pg-close.php) aangeroepen om de verbinding te sluiten.</span><span class="sxs-lookup"><span data-stu-id="a004f-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="a004f-156">Vervang de parameters `$host`, `$database`, `$user` en `$password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="a004f-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="a004f-157">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="a004f-157">Update data</span></span>
<span data-ttu-id="a004f-158">Gebruik de volgende code om verbinding te maken en de gegevens bij te werken met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="a004f-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="a004f-159">In de code wordt methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a004f-160">Vervolgens wordt methode [pg_query()](http://php.net/manual/en/function.pg-query.php) een aantal keer aangeroepen om een opdracht uit te voeren, en wordt [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) aangeroepen om de details te controleren als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a004f-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="a004f-161">Vervolgens wordt methode [pg_close()](http://php.net/manual/en/function.pg-close.php) aangeroepen om de verbinding te sluiten.</span><span class="sxs-lookup"><span data-stu-id="a004f-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="a004f-162">Vervang de parameters `$host`, `$database`, `$user` en `$password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="a004f-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="a004f-163">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="a004f-163">Delete data</span></span>
<span data-ttu-id="a004f-164">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="a004f-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="a004f-165">In de code wordt methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a004f-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a004f-166">Vervolgens wordt methode [pg_query()](http://php.net/manual/en/function.pg-query.php) een aantal keer aangeroepen om een opdracht uit te voeren, en wordt [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) aangeroepen om de details te controleren als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a004f-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="a004f-167">Vervolgens wordt methode [pg_close()](http://php.net/manual/en/function.pg-close.php) aangeroepen om de verbinding te sluiten.</span><span class="sxs-lookup"><span data-stu-id="a004f-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="a004f-168">Vervang de parameters `$host`, `$database`, `$user` en `$password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="a004f-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="a004f-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a004f-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a004f-170">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="a004f-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
