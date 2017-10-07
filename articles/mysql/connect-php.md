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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="074bf-103">Azure MySQL-Database: gebruik PHP tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="074bf-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="074bf-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL een [PHP](http://php.net/manual/intro-whatis.php) toepassing.</span><span class="sxs-lookup"><span data-stu-id="074bf-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="074bf-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="074bf-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="074bf-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van PHP, maar dat u nieuwe tooworking met Azure-Database voor MySQL zijn.</span><span class="sxs-lookup"><span data-stu-id="074bf-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="074bf-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="074bf-107">Prerequisites</span></span>
<span data-ttu-id="074bf-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="074bf-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="074bf-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="074bf-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="074bf-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="074bf-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="074bf-111">PHP installeren</span><span class="sxs-lookup"><span data-stu-id="074bf-111">Install PHP</span></span>
<span data-ttu-id="074bf-112">Installeer PHP op uw eigen server of maak een Azure-[web-app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) die PHP omvat.</span><span class="sxs-lookup"><span data-stu-id="074bf-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="074bf-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="074bf-113">MacOS</span></span>
- <span data-ttu-id="074bf-114">[PHP versie 7.1.4](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="074bf-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="074bf-115">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.macosx.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="074bf-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="074bf-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="074bf-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="074bf-117">[PHP versie 7.1.4 non-thread safe (x64)](http://php.net/downloads.php) downloaden</span><span class="sxs-lookup"><span data-stu-id="074bf-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="074bf-118">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.unix.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="074bf-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="074bf-119">Windows</span><span class="sxs-lookup"><span data-stu-id="074bf-119">Windows</span></span>
- <span data-ttu-id="074bf-120">[PHP versie 7.1.4 non-thread safe (x64)](http://windows.php.net/download#php-7.1) downloaden</span><span class="sxs-lookup"><span data-stu-id="074bf-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="074bf-121">Installeer PHP en Raadpleeg toohello [PHP handmatig](http://php.net/manual/install.windows.php) voor verdere configuratie</span><span class="sxs-lookup"><span data-stu-id="074bf-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="074bf-122">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="074bf-122">Get connection information</span></span>
<span data-ttu-id="074bf-123">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="074bf-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="074bf-124">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="074bf-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="074bf-125">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="074bf-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="074bf-126">Klik in het linkerdeelvenster Hallo **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="074bf-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="074bf-127">Klik op Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="074bf-127">Click hello server name.</span></span>
4. <span data-ttu-id="074bf-128">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="074bf-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="074bf-129">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="074bf-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="074bf-130">![Naam van Azure Database voor MySQL-server](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="074bf-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="074bf-131">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="074bf-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="074bf-132">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="074bf-132">Connect and create a table</span></span>
<span data-ttu-id="074bf-133">Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="074bf-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="074bf-134">Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP.</span><span class="sxs-lookup"><span data-stu-id="074bf-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="074bf-135">Hallo code aanroep methoden [mysqli_init](http://php.net/manual/mysqli.init.php) en [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="074bf-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="074bf-136">Vervolgens deze methode roept [mysqli_query](http://php.net/manual/mysqli.query.php) toorun Hallo query.</span><span class="sxs-lookup"><span data-stu-id="074bf-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="074bf-137">Vervolgens deze methode roept [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="074bf-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="074bf-138">Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="074bf-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="074bf-139">Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="074bf-139">Insert data</span></span>
<span data-ttu-id="074bf-140">Gebruik Hallo volgende tooconnect code en voeg gegevens met een **invoegen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="074bf-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="074bf-141">Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP.</span><span class="sxs-lookup"><span data-stu-id="074bf-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="074bf-142">Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide instructie in te voegen en vervolgens bindingen Hallo parameters op voor elke waarde in de ingevoegde kolom met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="074bf-143">Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="074bf-144">Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="074bf-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="074bf-145">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="074bf-145">Read data</span></span>
<span data-ttu-id="074bf-146">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="074bf-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="074bf-147">Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP.</span><span class="sxs-lookup"><span data-stu-id="074bf-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="074bf-148">Hallo code gebruikt methode [mysqli_query](http://php.net/manual/mysqli.query.php) uitvoeren Hallo sql-query en maakt gebruik van [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) methode toofetch Hallo resulterende rijen.</span><span class="sxs-lookup"><span data-stu-id="074bf-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="074bf-149">Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="074bf-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="074bf-150">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="074bf-150">Update data</span></span>
<span data-ttu-id="074bf-151">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="074bf-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="074bf-152">Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP.</span><span class="sxs-lookup"><span data-stu-id="074bf-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="074bf-153">Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide update-instructie vervolgens bindt Hallo parameters op voor elke waarde in de bijgewerkte kolom met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="074bf-154">Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="074bf-155">Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="074bf-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="074bf-156">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="074bf-156">Delete data</span></span>
<span data-ttu-id="074bf-157">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="074bf-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="074bf-158">Hallo code gebruikt Hallo **MySQL verbeterde extensie** (mysqli)-klasse die in PHP.</span><span class="sxs-lookup"><span data-stu-id="074bf-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="074bf-159">Hallo code gebruikt methode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate een voorbereide instructie verwijderen en vervolgens bindingen Hallo parameters op voor het Hallo waar-component in Hallo-instructie met methode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="074bf-160">Hallo-code wordt uitgevoerd met methode Hallo-instructie [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) en daarna wordt gesloten met methode instructie Hallo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="074bf-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="074bf-161">Hallo-host, gebruikersnaam, wachtwoord en db_name parameters vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="074bf-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="074bf-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="074bf-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="074bf-163">Een PHP- en MySQL-web-app bouwen in Azure</span><span class="sxs-lookup"><span data-stu-id="074bf-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
