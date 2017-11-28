---
title: aaaConnect tooAzure Database voor PostgreSQL met PHP | Microsoft Docs
description: Deze snelstartgids bevat een PHP-codevoorbeeld kunt u een query over gegevens uit Azure-Database voor PostgreSQL en tooconnect gebruiken.
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="29cad-103">Azure-Database voor PostgreSQL: gebruik PHP tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="29cad-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="29cad-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van PostgreSQL een [PHP](http://php.net/manual/intro-whatis.php) toepassing.</span><span class="sxs-lookup"><span data-stu-id="29cad-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="29cad-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="29cad-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="29cad-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van PHP, maar dat u nieuwe tooworking met Azure-Database voor PostgreSQL zijn.</span><span class="sxs-lookup"><span data-stu-id="29cad-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29cad-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="29cad-107">Prerequisites</span></span>
<span data-ttu-id="29cad-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="29cad-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="29cad-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="29cad-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="29cad-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="29cad-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="29cad-111">PHP installeren</span><span class="sxs-lookup"><span data-stu-id="29cad-111">Install PHP</span></span>
<span data-ttu-id="29cad-112">Installeer PHP op uw eigen server of maak een Azure-[web-app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) die PHP omvat.</span><span class="sxs-lookup"><span data-stu-id="29cad-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="29cad-113">Windows</span><span class="sxs-lookup"><span data-stu-id="29cad-113">Windows</span></span>
- <span data-ttu-id="29cad-114">[PHP versie 7.1.4 non-thread safe (x64)](http://windows.php.net/download#php-7.1) downloaden</span><span class="sxs-lookup"><span data-stu-id="29cad-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="29cad-115">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.windows.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="29cad-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="29cad-116">Hallo code gebruikt Hallo **pgsql** klasse (ext/php_pgsql.dll) die is opgenomen in Hallo PHP-installatie.</span><span class="sxs-lookup"><span data-stu-id="29cad-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="29cad-117">Ingeschakelde Hallo **pgsql** extensie door Hallo php.ini-configuratiebestand, gewoonlijk bevindt op bewerken `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="29cad-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="29cad-118">Hallo-configuratiebestand moet een regel met tekst hello bevatten `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="29cad-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="29cad-119">Als dit niet wordt weergegeven, Hallo tekst toevoegen en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="29cad-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="29cad-120">Als tekst hello aanwezig is, maar met een voorvoegsel puntkomma Opmerking Opmerking verwijderen hello tekst door het verwijderen van Hallo puntkomma.</span><span class="sxs-lookup"><span data-stu-id="29cad-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="29cad-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="29cad-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="29cad-122">[PHP versie 7.1.4 non-thread safe (x64)](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="29cad-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="29cad-123">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.unix.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="29cad-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="29cad-124">Hallo code gebruikt Hallo **pgsql** klasse (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="29cad-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="29cad-125">Installeer deze door `sudo apt-get install php-pgsql` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="29cad-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="29cad-126">Ingeschakelde Hallo **pgsql** uitbreiding door Hallo bewerken `/etc/php/7.0/mods-available/pgsql.ini` configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="29cad-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="29cad-127">Hallo-configuratiebestand moet een regel met tekst hello bevatten `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="29cad-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="29cad-128">Als dit niet wordt weergegeven, Hallo tekst toevoegen en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="29cad-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="29cad-129">Als tekst hello aanwezig is, maar met een voorvoegsel puntkomma Opmerking Opmerking verwijderen hello tekst door het verwijderen van Hallo puntkomma.</span><span class="sxs-lookup"><span data-stu-id="29cad-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="29cad-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="29cad-130">MacOS</span></span>
- <span data-ttu-id="29cad-131">[PHP versie 7.1.4](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="29cad-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="29cad-132">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.macosx.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="29cad-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="29cad-133">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="29cad-133">Get connection information</span></span>
<span data-ttu-id="29cad-134">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="29cad-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="29cad-135">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="29cad-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="29cad-136">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="29cad-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="29cad-137">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="29cad-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="29cad-138">Klik op de servernaam Hallo **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="29cad-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="29cad-139">Selecteer Hallo-server **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="29cad-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="29cad-140">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="29cad-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="29cad-141">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="29cad-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="29cad-142">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="29cad-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="29cad-143">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="29cad-143">Connect and create a table</span></span>
<span data-ttu-id="29cad-144">Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="29cad-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="29cad-145">Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="29cad-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="29cad-146">Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) meerdere keren toorun verschillende opdrachten en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden in elke keer.</span><span class="sxs-lookup"><span data-stu-id="29cad-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="29cad-147">Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="29cad-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="29cad-148">Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="29cad-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="29cad-149">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="29cad-149">Read data</span></span>
<span data-ttu-id="29cad-150">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29cad-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="29cad-151">Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="29cad-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="29cad-152">Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Hallo SELECT-opdracht, waarbij u Hallo resultaten in een resultatenset en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="29cad-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="29cad-153">tooread hello resultaatset, methode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) wordt aangeroepen in een lus zodra per rij en Hallo rij gegevens in een matrix is opgehaald `$row`, met één waarde per kolom in elke matrixpositie.</span><span class="sxs-lookup"><span data-stu-id="29cad-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="29cad-154">toofree hello resultaatset, methode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="29cad-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="29cad-155">Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="29cad-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="29cad-156">Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="29cad-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a><span data-ttu-id="29cad-157">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="29cad-157">Update data</span></span>
<span data-ttu-id="29cad-158">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29cad-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="29cad-159">Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="29cad-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="29cad-160">Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun een opdracht en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="29cad-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="29cad-161">Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="29cad-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="29cad-162">Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="29cad-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="29cad-163">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="29cad-163">Delete data</span></span>
<span data-ttu-id="29cad-164">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29cad-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="29cad-165">Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect te Azure-Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="29cad-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="29cad-166">Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun een opdracht en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="29cad-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="29cad-167">Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="29cad-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="29cad-168">Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="29cad-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="29cad-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29cad-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="29cad-170">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="29cad-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
