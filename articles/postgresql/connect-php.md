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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Azure-Database voor PostgreSQL: gebruik PHP tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van PostgreSQL een [PHP](http://php.net/manual/intro-whatis.php) toepassing. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van PHP, maar dat u nieuwe tooworking met Azure-Database voor PostgreSQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Database maken - Portal](quickstart-create-server-database-portal.md)
- [Database maken - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>PHP installeren
Installeer PHP op uw eigen server of maak een Azure-[web-app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) die PHP omvat.

### <a name="windows"></a>Windows
- [PHP versie 7.1.4 non-thread safe (x64)](http://windows.php.net/download#php-7.1) downloaden
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.windows.php) voor verdere configuratie
- Hallo code gebruikt Hallo **pgsql** klasse (ext/php_pgsql.dll) die is opgenomen in Hallo PHP-installatie. 
- Ingeschakelde Hallo **pgsql** extensie door Hallo php.ini-configuratiebestand, gewoonlijk bevindt op bewerken `C:\Program Files\PHP\v7.1\php.ini`. Hallo-configuratiebestand moet een regel met tekst hello bevatten `extension=php_pgsql.so`. Als dit niet wordt weergegeven, Hallo tekst toevoegen en sla Hallo-bestand. Als tekst hello aanwezig is, maar met een voorvoegsel puntkomma Opmerking Opmerking verwijderen hello tekst door het verwijderen van Hallo puntkomma.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- [PHP versie 7.1.4 non-thread safe (x64)](http://php.net/downloads.php) downloaden 
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.unix.php) voor verdere configuratie
- Hallo code gebruikt Hallo **pgsql** klasse (php_pgsql.so). Installeer deze door `sudo apt-get install php-pgsql` uit te voeren.
- Ingeschakelde Hallo **pgsql** uitbreiding door Hallo bewerken `/etc/php/7.0/mods-available/pgsql.ini` configuratiebestand. Hallo-configuratiebestand moet een regel met tekst hello bevatten `extension=php_pgsql.so`. Als dit niet wordt weergegeven, Hallo tekst toevoegen en sla Hallo-bestand. Als tekst hello aanwezig is, maar met een voorvoegsel puntkomma Opmerking Opmerking verwijderen hello tekst door het verwijderen van Hallo puntkomma.

### <a name="macos"></a>MacOS
- [PHP versie 7.1.4](http://php.net/downloads.php) downloaden
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.macosx.php) voor verdere configuratie

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.
3. Klik op de servernaam Hallo **mypgserver 20170401**.
4. Selecteer Hallo-server **overzicht** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-php/1-connection-string.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="connect-and-create-a-table"></a>Verbinding maken en een tabel maken
Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.

Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL. Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) meerdere keren toorun verschillende opdrachten en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden in elke keer. Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.

Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden. 

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

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

 Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL. Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Hallo SELECT-opdracht, waarbij u Hallo resultaten in een resultatenset en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden.  tooread hello resultaatset, methode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) wordt aangeroepen in een lus zodra per rij en Hallo rij gegevens in een matrix is opgehaald `$row`, met één waarde per kolom in elke matrixpositie.  toofree hello resultaatset, methode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) wordt aangeroepen. Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.

Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden. 

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

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.

Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database voor PostgreSQL. Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun een opdracht en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden. Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.

Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden. 

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


## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. 

 Hallo code aanroep van methode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect te Azure-Database voor PostgreSQL. Vervolgens deze methode roept [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun een opdracht en [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hallo details als een fout opgetreden. Vervolgens deze methode roept [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose Hallo verbinding.

Vervang Hallo `$host`, `$database`, `$user`, en `$password` parameters met uw eigen waarden. 

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

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./howto-migrate-using-export-and-import.md)
