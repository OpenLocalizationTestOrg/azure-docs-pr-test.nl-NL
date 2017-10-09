---
title: een PHP- en MySQL web-app in Azure aaaBuild | Microsoft Docs
description: Meer informatie over hoe tooget een PHP-app in Azure AD werkt met verbinding tooa MySQL-database in Azure.
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
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="e1284-103">Een PHP- en MySQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="e1284-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="e1284-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="e1284-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e1284-105">Deze zelfstudie laat zien hoe een PHP-toocreate web-app in Azure en verbindt u deze tooa MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="e1284-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="e1284-106">Wanneer u klaar bent, hebt u een [Laravel](https://laravel.com/) app uitgevoerd op Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="e1284-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="e1284-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="e1284-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1284-109">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="e1284-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e1284-110">Verbinding maken met een PHP-app tooMySQL</span><span class="sxs-lookup"><span data-stu-id="e1284-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="e1284-111">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e1284-112">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e1284-113">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="e1284-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e1284-114">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e1284-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1284-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e1284-115">Prerequisites</span></span>

<span data-ttu-id="e1284-116">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="e1284-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="e1284-117">Git installeren</span><span class="sxs-lookup"><span data-stu-id="e1284-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="e1284-118">Installeren van PHP 5.6.4 of hoger</span><span class="sxs-lookup"><span data-stu-id="e1284-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="e1284-119">Composer installeren</span><span class="sxs-lookup"><span data-stu-id="e1284-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="e1284-120">Hallo na PHP-uitbreidingen Laravel moet inschakelen: OpenSSL, PDO MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="e1284-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="e1284-121">Installeren en starten van MySQL</span><span class="sxs-lookup"><span data-stu-id="e1284-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="e1284-122">Lokale MySQL voorbereiden</span><span class="sxs-lookup"><span data-stu-id="e1284-122">Prepare local MySQL</span></span>

<span data-ttu-id="e1284-123">In deze stap maakt u een database in uw lokale MySQL-server voor gebruik in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e1284-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="e1284-124">Verbinding maken met toolocal MySQL-server</span><span class="sxs-lookup"><span data-stu-id="e1284-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="e1284-125">In een terminalvenster verbinding tooyour lokale MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="e1284-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="e1284-126">U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e1284-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e1284-127">Als u wordt gevraagd om een wachtwoord, hello wachtwoord invoeren voor Hallo `root` account.</span><span class="sxs-lookup"><span data-stu-id="e1284-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="e1284-128">Als je het wachtwoord van je root-account, Zie [MySQL: hoe tooReset hoofdwachtwoord Hallo](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="e1284-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="e1284-129">Als uw opdracht is uitgevoerd, wordt uw MySQL-server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="e1284-130">Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart met de volgende Hallo [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="e1284-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="e1284-131">Lokaal een database maken</span><span class="sxs-lookup"><span data-stu-id="e1284-131">Create a database locally</span></span>

<span data-ttu-id="e1284-132">Op Hallo `mysql` vragen, maakt u een database.</span><span class="sxs-lookup"><span data-stu-id="e1284-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="e1284-133">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="e1284-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="e1284-134">Een PHP-app lokaal maken</span><span class="sxs-lookup"><span data-stu-id="e1284-134">Create a PHP app locally</span></span>
<span data-ttu-id="e1284-135">In deze stap een voorbeeldtoepassing Laravel ophalen, de databaseverbinding configureren en het lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e1284-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="e1284-136">Kloon Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e1284-136">Clone hello sample</span></span>

<span data-ttu-id="e1284-137">In het terminalvenster hello, `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="e1284-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="e1284-138">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="e1284-139">`cd`tooyour gekloonde map.</span><span class="sxs-lookup"><span data-stu-id="e1284-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="e1284-140">Vereist hello-pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="e1284-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="e1284-141">MySQL-verbinding configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-141">Configure MySQL connection</span></span>

<span data-ttu-id="e1284-142">In de hoofdmap van de opslagplaats hello, maakt u een bestand met de naam *.env*.</span><span class="sxs-lookup"><span data-stu-id="e1284-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="e1284-143">Kopiëren Hallo variabelen te volgen in Hallo *.env* bestand.</span><span class="sxs-lookup"><span data-stu-id="e1284-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="e1284-144">Vervang Hallo  _&lt;root_password >_ aanduiding voor items met Hallo MySQL hoofdmap het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e1284-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="e1284-145">Voor informatie over hoe Laravel Hallo gebruikt _.env_ bestand, Zie [Laravel omgeving configuratie](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="e1284-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="e1284-146">Hallo voorbeeld lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e1284-146">Run hello sample locally</span></span>

<span data-ttu-id="e1284-147">Voer [Laravel database migraties](https://laravel.com/docs/5.4/migrations) toocreate Hallo behoeften van de toepassing hello tabellen.</span><span class="sxs-lookup"><span data-stu-id="e1284-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="e1284-148">welke tabellen worden gemaakt in Hallo migraties, zoekt u naar in Hallo toosee _database/migraties_ map in Hallo Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e1284-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="e1284-149">Genereer een nieuwe sleutel van de Laravel-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1284-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="e1284-150">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e1284-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="e1284-151">Navigeer te`http://localhost:8000` in een browser.</span><span class="sxs-lookup"><span data-stu-id="e1284-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="e1284-152">Een paar taken op Hallo pagina toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e1284-152">Add a few tasks in hello page.</span></span>

![PHP verbinding maakt met succes tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="e1284-154">toostop PHP, typ `Ctrl + C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="e1284-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="e1284-155">MySQL in Azure maken</span><span class="sxs-lookup"><span data-stu-id="e1284-155">Create MySQL in Azure</span></span>

<span data-ttu-id="e1284-156">In deze stap maakt u een MySQL-database in [Azure Database voor MySQL (Preview)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="e1284-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="e1284-157">Later kunt configureren u Hallo PHP tooconnect toothis toepassingsdatabase.</span><span class="sxs-lookup"><span data-stu-id="e1284-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="e1284-158">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e1284-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="e1284-159">Een MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="e1284-159">Create a MySQL server</span></span>

<span data-ttu-id="e1284-160">Maken van een server in Azure-Database voor MySQL (Preview) Hello [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="e1284-161">In Hallo volgende opdracht, vervangt u de naam van uw MySQL-server waar u Hallo zien  _&lt;mysql_server_name >_ tijdelijke aanduiding (geldige tekens zijn `a-z`, `0-9`, en `-`).</span><span class="sxs-lookup"><span data-stu-id="e1284-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e1284-162">Deze naam maakt deel uit van de hostnaam van de Hallo MySQL synchronisatieserver (`<mysql_server_name>.database.windows.net`), moet u toobe globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="e1284-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="e1284-163">Wanneer Hallo MySQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="e1284-164">Een firewall configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-164">Configure server firewall</span></span>

<span data-ttu-id="e1284-165">Een firewallregel maken voor uw MySQL server tooallow client verbindingen via Hallo [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="e1284-166">Azure-Database voor MySQL (Preview) biedt geen verbindingen alleen tooAzure services momenteel beperkt.</span><span class="sxs-lookup"><span data-stu-id="e1284-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="e1284-167">Zoals IP-adressen in Azure dynamisch toegewezen worden, is het beter tooenable alle IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="e1284-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="e1284-168">Hallo-service is een Preview-versie.</span><span class="sxs-lookup"><span data-stu-id="e1284-168">hello service is in preview.</span></span> <span data-ttu-id="e1284-169">Betere methoden voor het beveiligen van uw database zijn gepland.</span><span class="sxs-lookup"><span data-stu-id="e1284-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="e1284-170">Verbinding maken met lokaal tooproduction MySQL-server</span><span class="sxs-lookup"><span data-stu-id="e1284-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="e1284-171">In het terminalvenster hello, toohello MySQL server in Azure te verbinden.</span><span class="sxs-lookup"><span data-stu-id="e1284-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="e1284-172">Hallo-waarde die u eerder hebt opgegeven voor  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="e1284-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="e1284-173">Wanneer u wordt gevraagd om een wachtwoord, gebruiken _tr0ngPa $$ w0rd!_, die u hebt opgegeven toen u het Hallo-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e1284-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="e1284-174">Een productiedatabase maken</span><span class="sxs-lookup"><span data-stu-id="e1284-174">Create a production database</span></span>

<span data-ttu-id="e1284-175">Op Hallo `mysql` vragen, maakt u een database.</span><span class="sxs-lookup"><span data-stu-id="e1284-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="e1284-176">Een gebruiker met machtigingen maken</span><span class="sxs-lookup"><span data-stu-id="e1284-176">Create a user with permissions</span></span>

<span data-ttu-id="e1284-177">Maken van een databasegebruiker aangeroepen _phpappuser_ en geef deze alle bevoegdheden in Hallo `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="e1284-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="e1284-178">Hallo-serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="e1284-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="e1284-179">Verbinding maken met de app tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="e1284-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="e1284-180">In deze stap maakt verbinding u Hallo PHP-toepassing toohello MySQL-database die u hebt gemaakt in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="e1284-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="e1284-181">Hallo-databaseverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-181">Configure hello database connection</span></span>

<span data-ttu-id="e1284-182">Maak in de hoofdmap van de opslagplaats hello, een _. env.production_ -bestand en kopieer Hallo variabelen in de App te volgen.</span><span class="sxs-lookup"><span data-stu-id="e1284-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="e1284-183">Vervang Hallo tijdelijke aanduiding voor  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="e1284-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="e1284-184">Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="e1284-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="e1284-185">toosecure uw MySQL-verbindingsgegevens dit bestand al van Hallo Git-opslagplaats uitgesloten is (Zie _.gitignore_ in de hoofdmap van de opslagplaats Hallo).</span><span class="sxs-lookup"><span data-stu-id="e1284-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="e1284-186">Later kunt u meer informatie over hoe tooconfigure omgevingsvariabelen in App Service tooconnect tooyour-database in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="e1284-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="e1284-187">Met omgevingsvariabelen, hoeft u niet Hallo *.env* bestand in App Service.</span><span class="sxs-lookup"><span data-stu-id="e1284-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="e1284-188">SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-188">Configure SSL certificate</span></span>

<span data-ttu-id="e1284-189">Azure-Database voor MySQL afgedwongen standaard SSL-verbindingen van clients.</span><span class="sxs-lookup"><span data-stu-id="e1284-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="e1284-190">tooconnect tooyour MySQL-database in Azure, moet u een _.pem_ SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="e1284-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="e1284-191">Open _config/database.php_ en voeg Hallo _sslmode_ en _opties_ parameters te`connections.mysql`, zoals weergegeven in de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="e1284-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="e1284-192">toolearn hoe toogenerate dit _certificate.pem_, Zie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e1284-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="e1284-193">Hallo pad _/ssl/certificate.pem_ verwijst tooan bestaande _certificate.pem_ bestand in Hallo Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e1284-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="e1284-194">Dit bestand is voor uw gemak geleverd in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e1284-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="e1284-195">Voor de beste praktijken, u moet niet worden doorgevoerd uw _.pem_ certificaten in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="e1284-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="e1284-196">Hallo-toepassing lokaal testen</span><span class="sxs-lookup"><span data-stu-id="e1284-196">Test hello application locally</span></span>

<span data-ttu-id="e1284-197">Voer Laravel database migraties met _. env.production_ zoals hello omgeving bestand toocreate Hallo tabellen in uw MySQL-database in Azure-Database voor MySQL (Preview).</span><span class="sxs-lookup"><span data-stu-id="e1284-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="e1284-198">Vergeet niet dat _. env.production_ heeft Hallo verbinding informatie tooyour MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="e1284-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="e1284-199">_. env.production_ nog een geldige App-sleutel niet is voorzien.</span><span class="sxs-lookup"><span data-stu-id="e1284-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="e1284-200">Een nieuw wachtwoord voor het genereren in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="e1284-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="e1284-201">Uitvoeren van de voorbeeldtoepassing Hallo met _. env.production_ als Hallo omgeving-bestand.</span><span class="sxs-lookup"><span data-stu-id="e1284-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="e1284-202">Navigeer te`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="e1284-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="e1284-203">Als Hallo pagina wordt geladen zonder fouten, maakt de PHP-toepassing hello toohello MySQL-database in Azure verbinding.</span><span class="sxs-lookup"><span data-stu-id="e1284-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="e1284-204">Een paar taken op Hallo pagina toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e1284-204">Add a few tasks in hello page.</span></span>

![PHP voor verbinding maakt met succes tooAzure Database MySQL (Preview)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="e1284-206">toostop PHP, typ `Ctrl + C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="e1284-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="e1284-207">Uw wijzigingen</span><span class="sxs-lookup"><span data-stu-id="e1284-207">Commit your changes</span></span>

<span data-ttu-id="e1284-208">Voer de volgende Hallo Git-opdrachten toocommit uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="e1284-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="e1284-209">Uw app is gereed toobe geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="e1284-210">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-210">Deploy tooAzure</span></span>

<span data-ttu-id="e1284-211">In deze stap maakt implementeren u Hallo MySQL verbonden PHP-toepassing tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="e1284-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e1284-212">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="e1284-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="e1284-213">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e1284-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="e1284-214">Set Hallo PHP-versie</span><span class="sxs-lookup"><span data-stu-id="e1284-214">Set hello PHP version</span></span>

<span data-ttu-id="e1284-215">Set Hallo PHP-versie die toepassing hello vereist via Hallo [az webapp configuratieset](/cli/azure/webapp/config#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="e1284-216">Hallo stelt volgende opdracht Hallo PHP versie too_7.0_.</span><span class="sxs-lookup"><span data-stu-id="e1284-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="e1284-217">Database-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-217">Configure database settings</span></span>

<span data-ttu-id="e1284-218">Zoals eerder uiteengezet, kunt u tooyour Azure MySQL-database met omgevingsvariabelen in App Service.</span><span class="sxs-lookup"><span data-stu-id="e1284-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="e1284-219">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="e1284-220">Hallo volgende opdracht configureert u instellingen van de app Hallo `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, en `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="e1284-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="e1284-221">Vervang de tijdelijke aanduidingen Hallo  _&lt;appname >_ en  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="e1284-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="e1284-222">U kunt PHP Hallo [getenv](http://www.php.net/manual/function.getenv.php) methode tooaccess Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="e1284-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="e1284-223">Hallo Laravel code maakt gebruik van een [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper boven Hallo PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="e1284-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="e1284-224">Bijvoorbeeld, Hallo MySQL configuratie in _config/database.php_ eruit Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="e1284-225">Omgevingsvariabelen Laravel configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="e1284-226">Laravel moet de sleutel van een toepassing in App Service.</span><span class="sxs-lookup"><span data-stu-id="e1284-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="e1284-227">U kunt deze configureren met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e1284-227">You can configure it with app settings.</span></span>

<span data-ttu-id="e1284-228">Gebruik `php artisan` toogenerate een nieuwe Toepassingssleutel zonder op te slaan too_.env_.</span><span class="sxs-lookup"><span data-stu-id="e1284-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="e1284-229">Sleutel van de toepassing hello Hallo App Service web-app met instellen Hallo [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="e1284-230">Vervang de tijdelijke aanduidingen Hallo  _&lt;appname >_ en  _&lt;outputofphpartisankey: genereren >_.</span><span class="sxs-lookup"><span data-stu-id="e1284-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="e1284-231">`APP_DEBUG="true"`Hiermee geeft u fouten optreden foutopsporingsgegevens van de tooreturn Laravel wanneer Hallo web-app geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="e1284-232">Als een productietoepassing wordt uitgevoerd, stelt deze te`false`, die is veiliger.</span><span class="sxs-lookup"><span data-stu-id="e1284-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="e1284-233">Pad van virtuele toepassing hello instellen</span><span class="sxs-lookup"><span data-stu-id="e1284-233">Set hello virtual application path</span></span>

<span data-ttu-id="e1284-234">Hallo virtuele toepassingspad voor de web-app Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="e1284-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="e1284-235">Deze stap is vereist omdat Hallo [Laravel toepassing lifecycle](https://laravel.com/docs/5.4/lifecycle) begint in Hallo _openbare_ in plaats van de hoofdmap van de toepassing hello map.</span><span class="sxs-lookup"><span data-stu-id="e1284-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="e1284-236">Andere PHP-frameworks waarvan de levenscyclus van starten in de hoofdmap Hallo werken zonder handmatige configuratie van het pad van de virtuele toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e1284-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="e1284-237">Pad naar de virtuele toepassing set Hallo via Hallo [az resource update](/cli/azure/resource#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="e1284-238">Vervang Hallo  _&lt;appname >_ tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="e1284-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="e1284-239">Azure App Service wijst standaard hoofdpad voor virtuele toepassing hello (_/_) toohello hoofdmap Hallo geïmplementeerd toepassingsbestanden (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="e1284-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="e1284-240">Een implementatiegebruiker configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="e1284-241">Lokale Git-implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="e1284-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="e1284-242">TooAzure van Git push</span><span class="sxs-lookup"><span data-stu-id="e1284-242">Push tooAzure from Git</span></span>

<span data-ttu-id="e1284-243">Een Azure externe tooyour lokale Git-opslagplaats toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e1284-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="e1284-244">Push-toohello Azure externe toodeploy Hallo PHP-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1284-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="e1284-245">U wordt gevraagd om Hallo wachtwoord die u eerder hebt opgegeven als onderdeel van Hallo maken van Hallo implementatie gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e1284-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="e1284-246">Azure App Service communiceert tijdens de implementatie van de voortgang met Git.</span><span class="sxs-lookup"><span data-stu-id="e1284-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
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
> <span data-ttu-id="e1284-247">Merkt u dat met het implementatieproces Hallo geïnstalleerd [Composer](https://getcomposer.org/) pakketten aan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="e1284-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="e1284-248">App Service automatische van deze bewerking kan niet worden uitgevoerd tijdens de standaardimplementatie van de, zodat deze opslagplaats voorbeeld heeft drie extra bestanden in de hoofdmap directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="e1284-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="e1284-249">`.deployment`-Dit bestand vertelt App Service-toorun `bash deploy.sh` als Hallo aangepaste implementatiescript.</span><span class="sxs-lookup"><span data-stu-id="e1284-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="e1284-250">`deploy.sh`-script voor aangepaste implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e1284-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="e1284-251">Als u hello bestand bekijkt, ziet u dat deze wordt uitgevoerd `php composer.phar install` nadat `npm install`.</span><span class="sxs-lookup"><span data-stu-id="e1284-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="e1284-252">`composer.phar`-Hallo Composer Pakketbeheer.</span><span class="sxs-lookup"><span data-stu-id="e1284-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="e1284-253">U kunt deze benadering tooadd elke stap tooyour implementatie op basis van Git tooApp Service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e1284-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="e1284-254">Zie voor meer informatie [aangepaste implementatiescript](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="e1284-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="e1284-255">Toohello Azure-web-app bladeren</span><span class="sxs-lookup"><span data-stu-id="e1284-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="e1284-256">Te bladeren`http://<app_name>.azurewebsites.net` en enkele taken toohello lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e1284-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="e1284-258">Gefeliciteerd, u een PHP-gegevensgestuurde app in Azure App Service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e1284-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="e1284-259">Lokaal model bijwerken en implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-259">Update model locally and redeploy</span></span>

<span data-ttu-id="e1284-260">In deze stap maakt u een eenvoudige wijziging toohello `task` gegevens model Hallo webapp en vervolgens publiceren Hallo update tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1284-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="e1284-261">Hallo taken scenario wijzigt u Hallo toepassing, zodat u kunt een taak als voltooid markeren.</span><span class="sxs-lookup"><span data-stu-id="e1284-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="e1284-262">Een kolom toevoegen</span><span class="sxs-lookup"><span data-stu-id="e1284-262">Add a column</span></span>

<span data-ttu-id="e1284-263">Ga in de terminal hello, toohello hoofdmap van Hallo Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e1284-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="e1284-264">Genereren van de databasemigratie van een nieuwe voor Hallo `tasks` tabel:</span><span class="sxs-lookup"><span data-stu-id="e1284-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="e1284-265">Deze opdracht geeft Hallo van naam van Hallo migratie-bestand dat wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="e1284-266">Dit bestand in _database/migraties_ en open het bestand.</span><span class="sxs-lookup"><span data-stu-id="e1284-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="e1284-267">Vervang Hallo `up` methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="e1284-268">Hallo voorafgaande code Booleaanse voegt een kolom toe in Hallo `tasks` tabel met de naam `complete`.</span><span class="sxs-lookup"><span data-stu-id="e1284-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="e1284-269">Vervang Hallo `down` methode Hello code voor Hallo terugdraaien van de actie te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="e1284-270">In terminal Hallo, Laravel database migraties toomake Hallo wijzigen in de lokale database Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="e1284-271">Op basis van Hallo [Laravel naamgevingsconventie](https://laravel.com/docs/5.4/eloquent#defining-models), Hallo model `Task` (Zie _app/Task.php_) toegewezen toohello `tasks` tabel standaard.</span><span class="sxs-lookup"><span data-stu-id="e1284-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="e1284-272">Logica van de toepassing bijwerken</span><span class="sxs-lookup"><span data-stu-id="e1284-272">Update application logic</span></span>

<span data-ttu-id="e1284-273">Open Hallo *routes/web.php* bestand.</span><span class="sxs-lookup"><span data-stu-id="e1284-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="e1284-274">Hallo toepassing definieert de routes en zakelijke logica hier.</span><span class="sxs-lookup"><span data-stu-id="e1284-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="e1284-275">Toevoegen aan het einde van de Hallo van Hallo-bestand, een route met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="e1284-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="e1284-276">Hallo voorafgaande code maakt een eenvoudige update toohello-gegevensmodel door met de knop Hallo-waarde van `complete`.</span><span class="sxs-lookup"><span data-stu-id="e1284-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="e1284-277">Hallo weergave bijwerken</span><span class="sxs-lookup"><span data-stu-id="e1284-277">Update hello view</span></span>

<span data-ttu-id="e1284-278">Open Hallo *resources/views/tasks.blade.php* bestand.</span><span class="sxs-lookup"><span data-stu-id="e1284-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="e1284-279">Hallo zoeken `<tr>` tag te openen en vervang ze door:</span><span class="sxs-lookup"><span data-stu-id="e1284-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="e1284-280">Hallo voorafgaand aan een andere code rijkleur hello, afhankelijk van of Hallo-taak voltooid is.</span><span class="sxs-lookup"><span data-stu-id="e1284-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="e1284-281">In de volgende regel hello hebt u Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="e1284-282">Volledige regel Hallo vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1284-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="e1284-283">Hallo bovenstaande code wordt toegevoegd Hallo verzendknop die verwijst naar Hallo route die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="e1284-284">Hallo wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="e1284-284">Test hello changes locally</span></span>

<span data-ttu-id="e1284-285">Uit de hoofddirectory Hallo van Hallo Git-opslagplaats, Hallo ontwikkelingsserver wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1284-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="e1284-286">toosee hello statuswijziging taak, te navigeren`http://localhost:8000` en selecteer Hallo selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="e1284-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Toegevoegde selectievakje tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="e1284-288">toostop PHP, typ `Ctrl + C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="e1284-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="e1284-289">TooAzure wijzigingen publiceren</span><span class="sxs-lookup"><span data-stu-id="e1284-289">Publish changes tooAzure</span></span>

<span data-ttu-id="e1284-290">Voer in terminal hello, Laravel database migraties met Hallo productie connection string toomake Hallo wijziging in hello Azure-database.</span><span class="sxs-lookup"><span data-stu-id="e1284-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="e1284-291">Alle Hallo wijzigingen in Git doorvoeren en vervolgens push Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1284-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="e1284-292">Eenmaal Hallo `git push` is voltooid, gaat u toohello Azure-web-app en test Hallo nieuwe functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="e1284-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Model en de database wijzigingen tooAzure gepubliceerd](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="e1284-294">Als u alle taken toegevoegd, worden ze in de database Hallo bewaard.</span><span class="sxs-lookup"><span data-stu-id="e1284-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="e1284-295">Updates toohello gegevensschema laat de bestaande gegevens intact.</span><span class="sxs-lookup"><span data-stu-id="e1284-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="e1284-296">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="e1284-296">Stream diagnostic logs</span></span>

<span data-ttu-id="e1284-297">Tijdens het Hallo PHP-toepassing in Azure App Service wordt uitgevoerd, kunt u Hallo console logboeken doorgesluisd tooyour terminal ophalen.</span><span class="sxs-lookup"><span data-stu-id="e1284-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="e1284-298">Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.</span><span class="sxs-lookup"><span data-stu-id="e1284-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="e1284-299">toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1284-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="e1284-300">Eenmaal streaming-logboek is gestart, sommige webverkeer vernieuwen in Hallo browser tooget hello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="e1284-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="e1284-301">U ziet nu console logboeken doorgesluisd toohello terminal.</span><span class="sxs-lookup"><span data-stu-id="e1284-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="e1284-302">Als u de logboeken van console onmiddellijk niet ziet, controleert u opnieuw in 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="e1284-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="e1284-303">toostop logboek streaming op elk gewenst moment, type `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="e1284-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="e1284-304">Een PHP-toepassing kunt Hallo standaard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello-console.</span><span class="sxs-lookup"><span data-stu-id="e1284-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="e1284-305">Hallo-voorbeeldtoepassing gebruikt deze benadering in _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="e1284-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="e1284-306">Als een kader web [Laravel gebruikt Monolog](https://laravel.com/docs/5.4/errors) als Hallo logboekregistratie provider.</span><span class="sxs-lookup"><span data-stu-id="e1284-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="e1284-307">toosee hoe tooget Monolog toooutput berichten toohello console raadpleegt [PHP: hoe toouse toolog tooconsole (php://out) monolog](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="e1284-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="e1284-308">Hello Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="e1284-308">Manage hello Azure web app</span></span>

<span data-ttu-id="e1284-309">Ga toohello [Azure-portal](https://portal.azure.com) toomanage Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e1284-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="e1284-310">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="e1284-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="e1284-312">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e1284-312">You see your web app's Overview page.</span></span> <span data-ttu-id="e1284-313">Hier kunt u eenvoudige beheertaken zoals stoppen, starten, opnieuw opstarten, bladeren en verwijderen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e1284-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="e1284-314">Hallo linkermenu biedt pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="e1284-314">hello left menu provides pages for configuring your app.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e1284-316">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e1284-316">Next steps</span></span>

<span data-ttu-id="e1284-317">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="e1284-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1284-318">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="e1284-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e1284-319">Verbinding maken met een PHP-app tooMySQL</span><span class="sxs-lookup"><span data-stu-id="e1284-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="e1284-320">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e1284-321">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="e1284-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e1284-322">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="e1284-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e1284-323">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e1284-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="e1284-324">De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooa web-app.</span><span class="sxs-lookup"><span data-stu-id="e1284-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1284-325">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="e1284-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
