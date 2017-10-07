---
title: Verbinding maken met Database tooAzure voor MySQL met PHP | Microsoft Docs
description: Deze snelstartgids bevat meerdere PHP-codevoorbeelden kunt u een query over gegevens uit Azure-Database voor MySQL en tooconnect gebruiken.
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruik PHP tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL een [PHP](http://php.net/manual/intro-whatis.php) toepassing. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van PHP, maar dat u nieuwe tooworking met Azure-Database voor MySQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>PHP installeren
Installeer PHP op uw eigen server of maak een Azure-[web-app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) die PHP omvat.

### <a name="macos"></a>MacOS
- [PHP versie 7.1.4](http://php.net/downloads.php) downloaden
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.macosx.php) voor verdere configuratie

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- [PHP versie 7.1.4 non-thread safe (x64)](http://php.net/downloads.php) downloaden
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.unix.php) voor verdere configuratie

### <a name="windows"></a>Windows
- [PHP versie 7.1.4 non-thread safe (x64)](http://windows.php.net/download#php-7.1) downloaden
- Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.windows.php) voor verdere configuratie

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik in het linkerdeelvenster Hallo **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).
3. Klik op Hallo servernaam.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Naam van Azure Database voor MySQL-server](./media/connect-php/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="connect-and-create-a-table"></a>Verbinding maken en een tabel maken
Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie. 

Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP. Hallo code aanroep methoden [mysqli_init](http://php.net/manual/mysqli.init.php) en [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Vervolgens deze methode roept [mysqli_query](http://php.net/manual/mysqli.query.php) toorun Hallo query. Vervolgens deze methode roept [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose Hallo verbinding.

Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Gegevens invoegen
Gebruik Hallo volgende tooconnect code en voeg gegevens met een **invoegen** SQL-instructie.

Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP. Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide instructie in te voegen en vervolgens bindingen Hallo parameters op voor elke waarde in de ingevoegde kolom met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.  Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP. Hallo code gebruikt methode [mysqli_query](http://php.net/manual/mysqli.query.php) uitvoeren Hallo sql-query en maakt gebruik van [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) methode toofetch Hallo resulterende rijen.

Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.

Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP. Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide update-instructie vervolgens bindt Hallo parameters op voor elke waarde in de bijgewerkte kolom met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. 

Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP. Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide instructie verwijderen en vervolgens bindingen Hallo parameters op voor het Hallo waar-component in Hallo-instructie met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een PHP- en MySQL-web-app bouwen in Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
