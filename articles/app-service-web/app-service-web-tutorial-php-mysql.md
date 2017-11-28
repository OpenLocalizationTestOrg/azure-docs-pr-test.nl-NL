---
title: Een PHP- en MySQL web-app in Azure bouwen | Microsoft Docs
description: Informatie over het ophalen van een PHP-app in Azure, met verbinding met een MySQL-database in Azure AD werkt.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="f61a2-103">Een PHP- en MySQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="f61a2-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="f61a2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f61a2-105">Deze zelfstudie laat zien hoe een PHP-web-app in Azure maken en te verbinden met een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="f61a2-106">Wanneer u klaar bent, hebt u een [Laravel](https://laravel.com/) app uitgevoerd op Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f61a2-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="f61a2-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="f61a2-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f61a2-109">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="f61a2-110">Een PHP-app verbinden met MySQL</span><span class="sxs-lookup"><span data-stu-id="f61a2-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="f61a2-111">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f61a2-112">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f61a2-113">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f61a2-114">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="f61a2-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f61a2-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f61a2-115">Prerequisites</span></span>

<span data-ttu-id="f61a2-116">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="f61a2-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="f61a2-117">Git installeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="f61a2-118">Installeren van PHP 5.6.4 of hoger</span><span class="sxs-lookup"><span data-stu-id="f61a2-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="f61a2-119">Composer installeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="f61a2-120">De volgende Laravel behoeften van de PHP-uitbreidingen inschakelen: OpenSSL, PDO MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="f61a2-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="f61a2-121">Installeren en starten van MySQL</span><span class="sxs-lookup"><span data-stu-id="f61a2-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="f61a2-122">Lokale MySQL voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f61a2-122">Prepare local MySQL</span></span>

<span data-ttu-id="f61a2-123">In deze stap maakt u een database in uw lokale MySQL-server voor gebruik in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="f61a2-124">Verbinding maken met lokale MySQL-server</span><span class="sxs-lookup"><span data-stu-id="f61a2-124">Connect to local MySQL server</span></span>

<span data-ttu-id="f61a2-125">In een terminalvenster verbinding maken met uw lokale MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="f61a2-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="f61a2-126">Alle opdrachten kunt uitvoeren in deze zelfstudie kunt u deze terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="f61a2-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="f61a2-127">Als u wordt gevraagd om een wachtwoord, voert u het wachtwoord voor de `root` account.</span><span class="sxs-lookup"><span data-stu-id="f61a2-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="f61a2-128">Als je het wachtwoord van je root-account, Zie [MySQL: het opnieuw instellen van het hoofdwachtwoord](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="f61a2-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="f61a2-129">Als uw opdracht is uitgevoerd, wordt uw MySQL-server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f61a2-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="f61a2-130">Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart door de [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="f61a2-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="f61a2-131">Lokaal een database maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-131">Create a database locally</span></span>

<span data-ttu-id="f61a2-132">Op de `mysql` vragen, maakt u een database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="f61a2-133">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="f61a2-134">Een PHP-app lokaal maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-134">Create a PHP app locally</span></span>
<span data-ttu-id="f61a2-135">In deze stap een voorbeeldtoepassing Laravel ophalen, de databaseverbinding configureren en het lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f61a2-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="f61a2-136">Klonen van de steekproef</span><span class="sxs-lookup"><span data-stu-id="f61a2-136">Clone the sample</span></span>

<span data-ttu-id="f61a2-137">In het terminalvenster `cd` in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="f61a2-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="f61a2-138">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="f61a2-139">`cd`de gekloonde-adreslijst.</span><span class="sxs-lookup"><span data-stu-id="f61a2-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="f61a2-140">Installeer de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="f61a2-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="f61a2-141">MySQL-verbinding configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-141">Configure MySQL connection</span></span>

<span data-ttu-id="f61a2-142">Maak een bestand met de naam in de hoofdmap van de opslagplaats *.env*.</span><span class="sxs-lookup"><span data-stu-id="f61a2-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="f61a2-143">Kopieer de volgende variabelen in de *.env* bestand.</span><span class="sxs-lookup"><span data-stu-id="f61a2-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="f61a2-144">Vervang de  _&lt;root_password >_ aanduiding voor items met de MySQL-hoofdgebruiker wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f61a2-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="f61a2-145">Voor informatie over hoe Laravel gebruikt de _.env_ bestand, Zie [Laravel omgeving configuratie](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="f61a2-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="f61a2-146">Het voorbeeld lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-146">Run the sample locally</span></span>

<span data-ttu-id="f61a2-147">Voer [Laravel database migraties](https://laravel.com/docs/5.4/migrations) moeten de toepassing van de tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="f61a2-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="f61a2-148">Als u wilt zien welke tabellen worden gemaakt in de migratie, zoeken in de _database/migraties_ map in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f61a2-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="f61a2-149">Genereer een nieuwe sleutel van de Laravel-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a2-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="f61a2-150">Voer de toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="f61a2-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="f61a2-151">Ga naar `http://localhost:8000` in een browser.</span><span class="sxs-lookup"><span data-stu-id="f61a2-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="f61a2-152">Een paar taken op de pagina toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-152">Add a few tasks in the page.</span></span>

![PHP verbonden is met MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="f61a2-154">Typ om te stoppen PHP, `Ctrl + C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="f61a2-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="f61a2-155">MySQL in Azure maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-155">Create MySQL in Azure</span></span>

<span data-ttu-id="f61a2-156">In deze stap maakt u een MySQL-database in [Azure Database voor MySQL (Preview)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="f61a2-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="f61a2-157">Later kunt configureren u de PHP-toepassing verbinding maken met deze database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f61a2-158">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="f61a2-159">Een MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-159">Create a MySQL server</span></span>

<span data-ttu-id="f61a2-160">Een server in Azure-Database voor MySQL (Preview) te maken met de [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="f61a2-161">Vervang de naam van uw MySQL-server waarin u ziet in de volgende opdracht de  _&lt;mysql_server_name >_ tijdelijke aanduiding (geldige tekens zijn `a-z`, `0-9`, en `-`).</span><span class="sxs-lookup"><span data-stu-id="f61a2-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="f61a2-162">Deze naam maakt deel uit van de MySQL-server de hostnaam (`<mysql_server_name>.database.windows.net`), moet worden globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="f61a2-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="f61a2-163">Wanneer de MySQL-server is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f61a2-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="f61a2-164">Een firewall configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-164">Configure server firewall</span></span>

<span data-ttu-id="f61a2-165">Maken van een firewallregel voor uw MySQL-server clientverbindingen toestaat met behulp van de [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="f61a2-166">Azure-Database voor MySQL (Preview) biedt geen momenteel verbindingen alleen voor Azure-services beperken.</span><span class="sxs-lookup"><span data-stu-id="f61a2-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="f61a2-167">Zoals IP-adressen in Azure dynamisch toegewezen worden, is het beter om te zorgen dat alle IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="f61a2-168">De service zich in preview.</span><span class="sxs-lookup"><span data-stu-id="f61a2-168">The service is in preview.</span></span> <span data-ttu-id="f61a2-169">Betere methoden voor het beveiligen van uw database zijn gepland.</span><span class="sxs-lookup"><span data-stu-id="f61a2-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="f61a2-170">Verbinding maken met lokaal MySQL-server in productie</span><span class="sxs-lookup"><span data-stu-id="f61a2-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="f61a2-171">In het terminalvenster verbinding maken met de server MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="f61a2-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="f61a2-172">Gebruik de waarde die u eerder hebt opgegeven voor  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="f61a2-173">Wanneer u wordt gevraagd om een wachtwoord, gebruiken _tr0ngPa $$ w0rd!_, die u hebt opgegeven toen u de database hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f61a2-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="f61a2-174">Een productiedatabase maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-174">Create a production database</span></span>

<span data-ttu-id="f61a2-175">Op de `mysql` vragen, maakt u een database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="f61a2-176">Een gebruiker met machtigingen maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-176">Create a user with permissions</span></span>

<span data-ttu-id="f61a2-177">Maken van een databasegebruiker aangeroepen _phpappuser_ en geef deze alle bevoegdheden in de `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="f61a2-178">De verbinding met de sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="f61a2-179">App verbinden met Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="f61a2-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="f61a2-180">In deze stap maakt u verbinding maakt het PHP-toepassing aan de MySQL-database die u hebt gemaakt in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="f61a2-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="f61a2-181">Verbinding met de database configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-181">Configure the database connection</span></span>

<span data-ttu-id="f61a2-182">Maak in de hoofdmap van de opslagplaats een _. env.production_ -bestand en kopieer de volgende variabelen in de App.</span><span class="sxs-lookup"><span data-stu-id="f61a2-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="f61a2-183">Vervang de tijdelijke aanduiding  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="f61a2-184">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="f61a2-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="f61a2-185">Dit bestand is voor het beveiligen van uw MySQL-verbindingsgegevens al uitgesloten van de Git-opslagplaats (Zie _.gitignore_ in de hoofdmap van de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="f61a2-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="f61a2-186">Later kunt u informatie over het configureren van omgevingsvariabelen in App Service verbinding maken met uw database in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="f61a2-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="f61a2-187">Met omgevingsvariabelen, hoeft u niet de *.env* bestand in App Service.</span><span class="sxs-lookup"><span data-stu-id="f61a2-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="f61a2-188">SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-188">Configure SSL certificate</span></span>

<span data-ttu-id="f61a2-189">Azure-Database voor MySQL afgedwongen standaard SSL-verbindingen van clients.</span><span class="sxs-lookup"><span data-stu-id="f61a2-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="f61a2-190">Voor verbinding met uw MySQL-database in Azure, moet u een _.pem_ SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="f61a2-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="f61a2-191">Open _config/database.php_ en voeg de _sslmode_ en _opties_ parameters `connections.mysql`, zoals wordt weergegeven in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="f61a2-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="f61a2-192">Voor informatie over het genereren van dit _certificate.pem_, Zie [configureren van SSL-verbindingen in uw toepassing veilig verbinding kunnen maken met Azure-Database voor MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f61a2-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="f61a2-193">Het pad _/ssl/certificate.pem_ verwijst naar een bestaand _certificate.pem_ bestand in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f61a2-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="f61a2-194">Dit bestand is voor uw gemak geleverd in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="f61a2-195">Voor de beste praktijken, u moet niet worden doorgevoerd uw _.pem_ certificaten in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="f61a2-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="f61a2-196">De toepassing lokaal testen</span><span class="sxs-lookup"><span data-stu-id="f61a2-196">Test the application locally</span></span>

<span data-ttu-id="f61a2-197">Voer Laravel database migraties met _. env.production_ als het bestand omgeving maken van de tabellen in uw MySQL-database in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="f61a2-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="f61a2-198">Vergeet niet dat _. env.production_ heeft de verbindingsgegevens wilt toevoegen aan uw MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="f61a2-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="f61a2-199">_. env.production_ nog een geldige App-sleutel niet is voorzien.</span><span class="sxs-lookup"><span data-stu-id="f61a2-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="f61a2-200">Een nieuw wachtwoord voor het genereren in de terminal.</span><span class="sxs-lookup"><span data-stu-id="f61a2-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="f61a2-201">Uitvoeren van de voorbeeldtoepassing met _. env.production_ als het bestand omgeving.</span><span class="sxs-lookup"><span data-stu-id="f61a2-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="f61a2-202">Navigeer naar `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="f61a2-203">Als de pagina wordt geladen zonder fouten, wordt de PHP-toepassing maakt verbinding met de MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="f61a2-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="f61a2-204">Een paar taken op de pagina toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-204">Add a few tasks in the page.</span></span>

![PHP wel verbinding kunt maken met Azure-Database voor MySQL (Preview)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="f61a2-206">Typ om te stoppen PHP, `Ctrl + C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="f61a2-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="f61a2-207">Uw wijzigingen</span><span class="sxs-lookup"><span data-stu-id="f61a2-207">Commit your changes</span></span>

<span data-ttu-id="f61a2-208">Voer de volgende Git-opdrachten uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="f61a2-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="f61a2-209">Uw app is gereed om te worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f61a2-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="f61a2-210">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-210">Deploy to Azure</span></span>

<span data-ttu-id="f61a2-211">In deze stap maakt implementeren u de MySQL verbonden PHP-toepassing in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f61a2-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="f61a2-212">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="f61a2-213">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="f61a2-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="f61a2-214">De versie PHP instellen</span><span class="sxs-lookup"><span data-stu-id="f61a2-214">Set the PHP version</span></span>

<span data-ttu-id="f61a2-215">Stel de PHP-versie die vereist zijn voor de toepassing met behulp van de [az webapp configuratieset](/cli/azure/webapp/config#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="f61a2-216">De volgende opdracht stelt u de PHP-versie op _7.0_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="f61a2-217">Database-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-217">Configure database settings</span></span>

<span data-ttu-id="f61a2-218">Zoals eerder uiteengezet, kunt u verbinding met uw Azure-MySQL-database met omgevingsvariabelen in App Service.</span><span class="sxs-lookup"><span data-stu-id="f61a2-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="f61a2-219">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van de [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="f61a2-220">De volgende opdracht uit de app-instellingen configureert `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, en `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="f61a2-221">Vervang de tijdelijke aanduidingen  _&lt;appname >_ en  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="f61a2-222">U kunt de PHP [getenv](http://www.php.net/manual/function.getenv.php) methode voor toegang tot de instellingen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="f61a2-223">de code Laravel gebruikt een [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper boven de PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="f61a2-224">Bijvoorbeeld, de MySQL-configuratie in _config/database.php_ vergelijkbaar is met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f61a2-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="f61a2-225">Omgevingsvariabelen Laravel configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="f61a2-226">Laravel moet de sleutel van een toepassing in App Service.</span><span class="sxs-lookup"><span data-stu-id="f61a2-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="f61a2-227">U kunt deze configureren met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-227">You can configure it with app settings.</span></span>

<span data-ttu-id="f61a2-228">Gebruik `php artisan` voor het genereren van een nieuwe Toepassingssleutel zonder op te slaan naar _.env_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="f61a2-229">Stel de Toepassingssleutel in de App Service web-app met behulp van de [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="f61a2-230">Vervang de tijdelijke aanduidingen  _&lt;appname >_ en  _&lt;outputofphpartisankey: genereren >_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="f61a2-231">`APP_DEBUG="true"`Hiermee geeft u Laravel foutopsporing om informatie te retourneren wanneer de geïmplementeerde web-app fouten optreden.</span><span class="sxs-lookup"><span data-stu-id="f61a2-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="f61a2-232">Als een productietoepassing wordt uitgevoerd, stelt u deze naar `false`, die is veiliger.</span><span class="sxs-lookup"><span data-stu-id="f61a2-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="f61a2-233">Het pad van de virtuele toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="f61a2-233">Set the virtual application path</span></span>

<span data-ttu-id="f61a2-234">Het pad van de virtuele toepassing voor de web-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f61a2-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="f61a2-235">Deze stap is vereist omdat de [Laravel toepassing lifecycle](https://laravel.com/docs/5.4/lifecycle) begint in de _openbare_ map in plaats van de hoofdmap van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a2-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="f61a2-236">Andere PHP-frameworks waarvan de levenscyclus van starten in de hoofdmap werken zonder handmatige configuratie van het pad van de virtuele toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a2-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="f61a2-237">Pad van de virtuele toepassing instellen via de [az resource update](/cli/azure/resource#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="f61a2-238">Vervang de  _&lt;appname >_ tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="f61a2-238">Replace the _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="f61a2-239">Azure App Service wijst standaard het hoofdpad voor de virtuele toepassing (_/_) naar de hoofdmap van de geïmplementeerde toepassing-bestanden (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="f61a2-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="f61a2-240">Een implementatiegebruiker configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="f61a2-241">Lokale Git-implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="f61a2-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="f61a2-242">Pushen naar Azure vanaf Git</span><span class="sxs-lookup"><span data-stu-id="f61a2-242">Push to Azure from Git</span></span>

<span data-ttu-id="f61a2-243">Voeg een externe Azure-instantie toe aan uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f61a2-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="f61a2-244">Push naar de Azure-externe voor het implementeren van de PHP-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a2-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="f61a2-245">U wordt gevraagd om het wachtwoord dat u eerder hebt opgegeven als onderdeel van het maken van de gebruiker voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="f61a2-246">Azure App Service communiceert tijdens de implementatie van de voortgang met Git.</span><span class="sxs-lookup"><span data-stu-id="f61a2-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="f61a2-247">U merkt dat het implementatieproces installeert [Composer](https://getcomposer.org/) pakketten aan het einde.</span><span class="sxs-lookup"><span data-stu-id="f61a2-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="f61a2-248">App Service kan niet worden uitgevoerd deze automatische tijdens de standaardimplementatie van de, zodat deze opslagplaats voorbeeld heeft drie extra bestanden in de hoofdmap in te schakelen:</span><span class="sxs-lookup"><span data-stu-id="f61a2-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="f61a2-249">`.deployment`-Dit bestand vertelt App Service om uit te voeren `bash deploy.sh` als het script voor aangepaste implementatie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="f61a2-250">`deploy.sh`-Het script voor aangepaste implementatie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="f61a2-251">Als u het bestand bekijkt, ziet u dat deze wordt uitgevoerd `php composer.phar install` nadat `npm install`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="f61a2-252">`composer.phar`-De Composer-Pakketbeheer.</span><span class="sxs-lookup"><span data-stu-id="f61a2-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="f61a2-253">Deze aanpak kunt u een stap toevoegen aan uw implementatie op basis van Git in App Service.</span><span class="sxs-lookup"><span data-stu-id="f61a2-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="f61a2-254">Zie voor meer informatie [aangepaste implementatiescript](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="f61a2-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="f61a2-255">Blader naar de Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="f61a2-255">Browse to the Azure web app</span></span>

<span data-ttu-id="f61a2-256">Blader naar `http://<app_name>.azurewebsites.net` en een paar taken toevoegen aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="f61a2-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="f61a2-258">Gefeliciteerd, u een PHP-gegevensgestuurde app in Azure App Service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f61a2-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="f61a2-259">Lokaal model bijwerken en implementeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-259">Update model locally and redeploy</span></span>

<span data-ttu-id="f61a2-260">In deze stap maakt u een eenvoudige wijziging in de `task` gegevensmodel en de Web-App en de update vervolgens publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="f61a2-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="f61a2-261">Voor het scenario taken wijzigen u de toepassing, zodat u kunt een taak als voltooid markeren.</span><span class="sxs-lookup"><span data-stu-id="f61a2-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="f61a2-262">Een kolom toevoegen</span><span class="sxs-lookup"><span data-stu-id="f61a2-262">Add a column</span></span>

<span data-ttu-id="f61a2-263">Ga in de terminal naar de hoofdmap van de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f61a2-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="f61a2-264">Genereren van de databasemigratie van een nieuwe voor de `tasks` tabel:</span><span class="sxs-lookup"><span data-stu-id="f61a2-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="f61a2-265">Deze opdracht geeft u de naam van de migratiebestand dat wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f61a2-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="f61a2-266">Dit bestand in _database/migraties_ en open het bestand.</span><span class="sxs-lookup"><span data-stu-id="f61a2-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="f61a2-267">Vervang de `up` methode met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f61a2-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="f61a2-268">De bovenstaande code wordt toegevoegd een Booleaanse kolom in de `tasks` tabel met de naam `complete`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="f61a2-269">Vervang de `down` methode met de volgende code voor de actie ongedaan maken:</span><span class="sxs-lookup"><span data-stu-id="f61a2-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="f61a2-270">Voer in de terminal Laravel database migraties om de wijziging in de lokale database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="f61a2-271">Op basis van de [Laravel naamgevingsconventie](https://laravel.com/docs/5.4/eloquent#defining-models), het model `Task` (Zie _app/Task.php_) wordt toegewezen aan de `tasks` tabel standaard.</span><span class="sxs-lookup"><span data-stu-id="f61a2-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="f61a2-272">Logica van de toepassing bijwerken</span><span class="sxs-lookup"><span data-stu-id="f61a2-272">Update application logic</span></span>

<span data-ttu-id="f61a2-273">Open de *routes/web.php* bestand.</span><span class="sxs-lookup"><span data-stu-id="f61a2-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="f61a2-274">De toepassing definieert de routes en zakelijke logica hier.</span><span class="sxs-lookup"><span data-stu-id="f61a2-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="f61a2-275">Toevoegen aan het einde van het bestand een route met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f61a2-275">At the end of the file, add a route with the following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="f61a2-276">De bovenstaande code maakt een eenvoudige update naar het gegevensmodel door het uitschakelen van de waarde van `complete`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="f61a2-277">De weergave bijwerken</span><span class="sxs-lookup"><span data-stu-id="f61a2-277">Update the view</span></span>

<span data-ttu-id="f61a2-278">Open de *resources/views/tasks.blade.php* bestand.</span><span class="sxs-lookup"><span data-stu-id="f61a2-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="f61a2-279">Zoek de `<tr>` tag te openen en vervang ze door:</span><span class="sxs-lookup"><span data-stu-id="f61a2-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="f61a2-280">De bovenstaande code wordt de rijkleur, afhankelijk van of de taak voltooid is.</span><span class="sxs-lookup"><span data-stu-id="f61a2-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="f61a2-281">U hebt de volgende code in de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="f61a2-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="f61a2-282">Vervang de volledige regel door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f61a2-282">Replace the entire line with the following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="f61a2-283">De bovenstaande code wordt toegevoegd voor de verzendknop die verwijst naar de route die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f61a2-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="f61a2-284">De wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="f61a2-284">Test the changes locally</span></span>

<span data-ttu-id="f61a2-285">Voer de ontwikkelaarsserver uit de hoofddirectory van de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f61a2-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="f61a2-286">Om te zien van de status van de taak wijzigen, gaat u naar `http://localhost:8000` en schakel het selectievakje.</span><span class="sxs-lookup"><span data-stu-id="f61a2-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Toegevoegde selectievakje in als de taak](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="f61a2-288">Typ om te stoppen PHP, `Ctrl + C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="f61a2-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="f61a2-289">Wijzigingen publiceren naar Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-289">Publish changes to Azure</span></span>

<span data-ttu-id="f61a2-290">Voer in de terminal Laravel database migraties met de productie-verbindingsreeks te maken van de wijziging in de Azure-database.</span><span class="sxs-lookup"><span data-stu-id="f61a2-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="f61a2-291">Voer de wijzigingen in Git en vervolgens de codewijzigingen pushen naar Azure.</span><span class="sxs-lookup"><span data-stu-id="f61a2-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="f61a2-292">Eenmaal de `git push` is voltooid, gaat u naar de Azure-web-app en testen van de nieuwe functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="f61a2-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Model en de database-wijzigingen die zijn gepubliceerd naar Azure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="f61a2-294">Als u alle taken toegevoegd, worden ze in de database bewaard.</span><span class="sxs-lookup"><span data-stu-id="f61a2-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="f61a2-295">Updates voor het schema van de laten bestaande gegevens intact.</span><span class="sxs-lookup"><span data-stu-id="f61a2-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="f61a2-296">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="f61a2-296">Stream diagnostic logs</span></span>

<span data-ttu-id="f61a2-297">Als de PHP-toepassing in Azure App Service wordt uitgevoerd, kunt u de logboeken van de console doorgesluisd naar uw terminal opvragen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="f61a2-298">Op die manier kunt u de dezelfde diagnostische berichten op te sporen toepassingsfouten ophalen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="f61a2-299">Gebruik voor het starten van de streaming-logboek de [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f61a2-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="f61a2-300">Eenmaal streaming-logboek is gestart, vernieuwt u de Azure-web-app in de browser sommige webverkeer ophalen.</span><span class="sxs-lookup"><span data-stu-id="f61a2-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="f61a2-301">U ziet nu de logboeken van de console is doorgegeven naar de terminal.</span><span class="sxs-lookup"><span data-stu-id="f61a2-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="f61a2-302">Als u de logboeken van console onmiddellijk niet ziet, controleert u opnieuw in 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="f61a2-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="f61a2-303">Typ om te stoppen met het logboek op elk gewenst moment op streaming, `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="f61a2-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="f61a2-304">Een PHP-toepassing kunt gebruiken de standaard [error_log()](http://php.net/manual/function.error-log.php) naar uitvoer naar de console.</span><span class="sxs-lookup"><span data-stu-id="f61a2-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="f61a2-305">De voorbeeldtoepassing gebruikt deze benadering in _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="f61a2-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="f61a2-306">Als een kader web [Laravel gebruikt Monolog](https://laravel.com/docs/5.4/errors) als de provider voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="f61a2-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="f61a2-307">Zie voor het ophalen van Monolog uitvoer berichten naar de console [PHP: het gebruik van monolog aan te melden console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="f61a2-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="f61a2-308">De Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="f61a2-308">Manage the Azure web app</span></span>

<span data-ttu-id="f61a2-309">Ga naar [Azure Portal](https://portal.azure.com) om de web-app te beheren die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f61a2-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="f61a2-310">Klik in het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="f61a2-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="f61a2-312">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f61a2-312">You see your web app's Overview page.</span></span> <span data-ttu-id="f61a2-313">Hier kunt u eenvoudige beheertaken zoals stoppen, starten, opnieuw opstarten, bladeren en verwijderen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f61a2-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="f61a2-314">Het menu links biedt pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="f61a2-314">The left menu provides pages for configuring your app.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="f61a2-316">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f61a2-316">Next steps</span></span>

<span data-ttu-id="f61a2-317">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="f61a2-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f61a2-318">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="f61a2-319">Een PHP-app verbinden met MySQL</span><span class="sxs-lookup"><span data-stu-id="f61a2-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="f61a2-320">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f61a2-321">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="f61a2-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f61a2-322">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="f61a2-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f61a2-323">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="f61a2-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="f61a2-324">Ga naar de volgende zelfstudie voor informatie over het toewijzen van een aangepaste DNS-naam aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="f61a2-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f61a2-325">Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="f61a2-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
