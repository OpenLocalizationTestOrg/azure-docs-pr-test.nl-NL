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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Een PHP- en MySQL web-app in Azure bouwen

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie. Deze zelfstudie laat zien hoe een PHP-toocreate web-app in Azure en verbindt u deze tooa MySQL-database. Wanneer u klaar bent, hebt u een [Laravel](https://laravel.com/) app uitgevoerd op Azure App Service Web Apps.

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een MySQL-database maken in Azure
> * Verbinding maken met een PHP-app tooMySQL
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * Hallo-app in hello Azure-portal beheren

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

* [Git installeren](https://git-scm.com/)
* [Installeren van PHP 5.6.4 of hoger](http://php.net/downloads.php)
* [Composer installeren](https://getcomposer.org/doc/00-intro.md)
* Hallo na PHP-uitbreidingen Laravel moet inschakelen: OpenSSL, PDO MySQL, Mbstring, Tokenizer, XML
* [Installeren en starten van MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Lokale MySQL voorbereiden

In deze stap maakt u een database in uw lokale MySQL-server voor gebruik in deze zelfstudie.

### <a name="connect-toolocal-mysql-server"></a>Verbinding maken met toolocal MySQL-server

In een terminalvenster verbinding tooyour lokale MySQL-server. U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.

```bash
mysql -u root -p
```

Als u wordt gevraagd om een wachtwoord, hello wachtwoord invoeren voor Hallo `root` account. Als je het wachtwoord van je root-account, Zie [MySQL: hoe tooReset hoofdwachtwoord Hallo](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Als uw opdracht is uitgevoerd, wordt uw MySQL-server uitgevoerd. Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart met de volgende Hallo [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Lokaal een database maken

Op Hallo `mysql` vragen, maakt u een database.

```sql 
CREATE DATABASE sampledb;
```

Uw serververbinding sluiten door te typen `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Een PHP-app lokaal maken
In deze stap een voorbeeldtoepassing Laravel ophalen, de databaseverbinding configureren en het lokaal uitvoeren. 

### <a name="clone-hello-sample"></a>Kloon Hallo-voorbeeld

In het terminalvenster hello, `cd` tooa werkmap.

Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`tooyour gekloonde map.
Vereist hello-pakketten installeren.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>MySQL-verbinding configureren

In de hoofdmap van de opslagplaats hello, maakt u een bestand met de naam *.env*. Kopiëren Hallo variabelen te volgen in Hallo *.env* bestand. Vervang Hallo  _&lt;root_password >_ aanduiding voor items met Hallo MySQL hoofdmap het wachtwoord van gebruiker.

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

Voor informatie over hoe Laravel Hallo gebruikt _.env_ bestand, Zie [Laravel omgeving configuratie](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Hallo voorbeeld lokaal uitvoeren

Voer [Laravel database migraties](https://laravel.com/docs/5.4/migrations) toocreate Hallo behoeften van de toepassing hello tabellen. welke tabellen worden gemaakt in Hallo migraties, zoekt u naar in Hallo toosee _database/migraties_ map in Hallo Git-opslagplaats.

```bash
php artisan migrate
```

Genereer een nieuwe sleutel van de Laravel-toepassing.

```bash
php artisan key:generate
```

Hallo-toepassing uitvoeren.

```bash
php artisan serve
```

Navigeer te`http://localhost:8000` in een browser. Een paar taken op Hallo pagina toevoegen.

![PHP verbinding maakt met succes tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, typ `Ctrl + C` in Hallo terminal.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>MySQL in Azure maken

In deze stap maakt u een MySQL-database in [Azure Database voor MySQL (Preview)](/azure/mysql). Later kunt configureren u Hallo PHP tooconnect toothis toepassingsdatabase.

### <a name="create-a-resource-group"></a>Een resourcegroep maken

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Een MySQL-server maken

Maken van een server in Azure-Database voor MySQL (Preview) Hello [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.

In Hallo volgende opdracht, vervangt u de naam van uw MySQL-server waar u Hallo zien  _&lt;mysql_server_name >_ tijdelijke aanduiding (geldige tekens zijn `a-z`, `0-9`, en `-`). Deze naam maakt deel uit van de hostnaam van de Hallo MySQL synchronisatieserver (`<mysql_server_name>.database.windows.net`), moet u toobe globaal uniek zijn.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Wanneer Hallo MySQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

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

### <a name="configure-server-firewall"></a>Een firewall configureren

Een firewallregel maken voor uw MySQL server tooallow client verbindingen via Hallo [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure-Database voor MySQL (Preview) biedt geen verbindingen alleen tooAzure services momenteel beperkt. Zoals IP-adressen in Azure dynamisch toegewezen worden, is het beter tooenable alle IP-adressen. Hallo-service is een Preview-versie. Betere methoden voor het beveiligen van uw database zijn gepland.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Verbinding maken met lokaal tooproduction MySQL-server

In het terminalvenster hello, toohello MySQL server in Azure te verbinden. Hallo-waarde die u eerder hebt opgegeven voor  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Wanneer u wordt gevraagd om een wachtwoord, gebruiken _tr0ngPa $$ w0rd!_, die u hebt opgegeven toen u het Hallo-database gemaakt.

### <a name="create-a-production-database"></a>Een productiedatabase maken

Op Hallo `mysql` vragen, maakt u een database.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Een gebruiker met machtigingen maken

Maken van een databasegebruiker aangeroepen _phpappuser_ en geef deze alle bevoegdheden in Hallo `sampledb` database.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Hallo-serververbinding sluiten door te typen `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Verbinding maken met de app tooAzure MySQL

In deze stap maakt verbinding u Hallo PHP-toepassing toohello MySQL-database die u hebt gemaakt in Azure-Database voor MySQL (Preview).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Hallo-databaseverbinding configureren

Maak in de hoofdmap van de opslagplaats hello, een _. env.production_ -bestand en kopieer Hallo variabelen in de App te volgen. Vervang Hallo tijdelijke aanduiding voor  _&lt;mysql_server_name >_.

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

Hallo wijzigingen opslaan.

> [!TIP]
> toosecure uw MySQL-verbindingsgegevens dit bestand al van Hallo Git-opslagplaats uitgesloten is (Zie _.gitignore_ in de hoofdmap van de opslagplaats Hallo). Later kunt u meer informatie over hoe tooconfigure omgevingsvariabelen in App Service tooconnect tooyour-database in Azure-Database voor MySQL (Preview). Met omgevingsvariabelen, hoeft u niet Hallo *.env* bestand in App Service.
>

### <a name="configure-ssl-certificate"></a>SSL-certificaat configureren

Azure-Database voor MySQL afgedwongen standaard SSL-verbindingen van clients. tooconnect tooyour MySQL-database in Azure, moet u een _.pem_ SSL-certificaat.

Open _config/database.php_ en voeg Hallo _sslmode_ en _opties_ parameters te`connections.mysql`, zoals weergegeven in de volgende code Hallo.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn hoe toogenerate dit _certificate.pem_, Zie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> Hallo pad _/ssl/certificate.pem_ verwijst tooan bestaande _certificate.pem_ bestand in Hallo Git-opslagplaats. Dit bestand is voor uw gemak geleverd in deze zelfstudie. Voor de beste praktijken, u moet niet worden doorgevoerd uw _.pem_ certificaten in broncodebeheer. 
>

### <a name="test-hello-application-locally"></a>Hallo-toepassing lokaal testen

Voer Laravel database migraties met _. env.production_ zoals hello omgeving bestand toocreate Hallo tabellen in uw MySQL-database in Azure-Database voor MySQL (Preview). Vergeet niet dat _. env.production_ heeft Hallo verbinding informatie tooyour MySQL-database in Azure.

```bash
php artisan migrate --env=production --force
```

_. env.production_ nog een geldige App-sleutel niet is voorzien. Een nieuw wachtwoord voor het genereren in Hallo terminal.

```bash
php artisan key:generate --env=production --force
```

Uitvoeren van de voorbeeldtoepassing Hallo met _. env.production_ als Hallo omgeving-bestand.

```bash
php artisan serve --env=production
```

Navigeer te`http://localhost:8000`. Als Hallo pagina wordt geladen zonder fouten, maakt de PHP-toepassing hello toohello MySQL-database in Azure verbinding.

Een paar taken op Hallo pagina toevoegen.

![PHP voor verbinding maakt met succes tooAzure Database MySQL (Preview)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, typ `Ctrl + C` in Hallo terminal.

### <a name="commit-your-changes"></a>Uw wijzigingen

Voer de volgende Hallo Git-opdrachten toocommit uw wijzigingen:

```bash
git add .
git commit -m "database.php updates"
```

Uw app is gereed toobe geïmplementeerd.

## <a name="deploy-tooazure"></a>TooAzure implementeren

In deze stap maakt implementeren u Hallo MySQL verbonden PHP-toepassing tooAzure App Service.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Een webtoepassing maken

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Set Hallo PHP-versie

Set Hallo PHP-versie die toepassing hello vereist via Hallo [az webapp configuratieset](/cli/azure/webapp/config#set) opdracht.

Hallo stelt volgende opdracht Hallo PHP versie too_7.0_.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Database-instellingen configureren

Zoals eerder uiteengezet, kunt u tooyour Azure MySQL-database met omgevingsvariabelen in App Service.

In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht.

Hallo volgende opdracht configureert u instellingen van de app Hallo `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, en `DB_PASSWORD`. Vervang de tijdelijke aanduidingen Hallo  _&lt;appname >_ en  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

U kunt PHP Hallo [getenv](http://www.php.net/manual/function.getenv.php) methode tooaccess Hallo instellingen. Hallo Laravel code maakt gebruik van een [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper boven Hallo PHP `getenv`. Bijvoorbeeld, Hallo MySQL configuratie in _config/database.php_ eruit Hallo code te volgen:

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

### <a name="configure-laravel-environment-variables"></a>Omgevingsvariabelen Laravel configureren

Laravel moet de sleutel van een toepassing in App Service. U kunt deze configureren met app-instellingen.

Gebruik `php artisan` toogenerate een nieuwe Toepassingssleutel zonder op te slaan too_.env_.

```bash
php artisan key:generate --show
```

Sleutel van de toepassing hello Hallo App Service web-app met instellen Hallo [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) opdracht. Vervang de tijdelijke aanduidingen Hallo  _&lt;appname >_ en  _&lt;outputofphpartisankey: genereren >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`Hiermee geeft u fouten optreden foutopsporingsgegevens van de tooreturn Laravel wanneer Hallo web-app geïmplementeerd. Als een productietoepassing wordt uitgevoerd, stelt deze te`false`, die is veiliger.

### <a name="set-hello-virtual-application-path"></a>Pad van virtuele toepassing hello instellen

Hallo virtuele toepassingspad voor de web-app Hallo instellen. Deze stap is vereist omdat Hallo [Laravel toepassing lifecycle](https://laravel.com/docs/5.4/lifecycle) begint in Hallo _openbare_ in plaats van de hoofdmap van de toepassing hello map. Andere PHP-frameworks waarvan de levenscyclus van starten in de hoofdmap Hallo werken zonder handmatige configuratie van het pad van de virtuele toepassing hello.

Pad naar de virtuele toepassing set Hallo via Hallo [az resource update](/cli/azure/resource#update) opdracht. Vervang Hallo  _&lt;appname >_ tijdelijke aanduiding.

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

Azure App Service wijst standaard hoofdpad voor virtuele toepassing hello (_/_) toohello hoofdmap Hallo geïmplementeerd toepassingsbestanden (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Een implementatiegebruiker configureren

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Lokale Git-implementatie configureren

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>TooAzure van Git push

Een Azure externe tooyour lokale Git-opslagplaats toevoegen.

```bash
git remote add azure <paste_copied_url_here>
```

Push-toohello Azure externe toodeploy Hallo PHP-toepassing. U wordt gevraagd om Hallo wachtwoord die u eerder hebt opgegeven als onderdeel van Hallo maken van Hallo implementatie gebruiker.

```bash
git push azure master
```

Azure App Service communiceert tijdens de implementatie van de voortgang met Git.

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
> Merkt u dat met het implementatieproces Hallo geïnstalleerd [Composer](https://getcomposer.org/) pakketten aan Hallo einde. App Service automatische van deze bewerking kan niet worden uitgevoerd tijdens de standaardimplementatie van de, zodat deze opslagplaats voorbeeld heeft drie extra bestanden in de hoofdmap directory tooenable:
>
> - `.deployment`-Dit bestand vertelt App Service-toorun `bash deploy.sh` als Hallo aangepaste implementatiescript.
> - `deploy.sh`-script voor aangepaste implementatie Hallo. Als u hello bestand bekijkt, ziet u dat deze wordt uitgevoerd `php composer.phar install` nadat `npm install`.
> - `composer.phar`-Hallo Composer Pakketbeheer.
>
> U kunt deze benadering tooadd elke stap tooyour implementatie op basis van Git tooApp Service gebruiken. Zie voor meer informatie [aangepaste implementatiescript](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure-web-app bladeren

Te bladeren`http://<app_name>.azurewebsites.net` en enkele taken toohello lijst toevoegen.

![PHP-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Gefeliciteerd, u een PHP-gegevensgestuurde app in Azure App Service uitvoert.

## <a name="update-model-locally-and-redeploy"></a>Lokaal model bijwerken en implementeren

In deze stap maakt u een eenvoudige wijziging toohello `task` gegevens model Hallo webapp en vervolgens publiceren Hallo update tooAzure.

Hallo taken scenario wijzigt u Hallo toepassing, zodat u kunt een taak als voltooid markeren.

### <a name="add-a-column"></a>Een kolom toevoegen

Ga in de terminal hello, toohello hoofdmap van Hallo Git-opslagplaats.

Genereren van de databasemigratie van een nieuwe voor Hallo `tasks` tabel:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Deze opdracht geeft Hallo van naam van Hallo migratie-bestand dat wordt gegenereerd. Dit bestand in _database/migraties_ en open het bestand.

Vervang Hallo `up` methode Hello code te volgen:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Hallo voorafgaande code Booleaanse voegt een kolom toe in Hallo `tasks` tabel met de naam `complete`.

Vervang Hallo `down` methode Hello code voor Hallo terugdraaien van de actie te volgen:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

In terminal Hallo, Laravel database migraties toomake Hallo wijzigen in de lokale database Hallo worden uitgevoerd.

```bash
php artisan migrate
```

Op basis van Hallo [Laravel naamgevingsconventie](https://laravel.com/docs/5.4/eloquent#defining-models), Hallo model `Task` (Zie _app/Task.php_) toegewezen toohello `tasks` tabel standaard.

### <a name="update-application-logic"></a>Logica van de toepassing bijwerken

Open Hallo *routes/web.php* bestand. Hallo toepassing definieert de routes en zakelijke logica hier.

Toevoegen aan het einde van de Hallo van Hallo-bestand, een route met de volgende code Hallo:

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

Hallo voorafgaande code maakt een eenvoudige update toohello-gegevensmodel door met de knop Hallo-waarde van `complete`.

### <a name="update-hello-view"></a>Hallo weergave bijwerken

Open Hallo *resources/views/tasks.blade.php* bestand. Hallo zoeken `<tr>` tag te openen en vervang ze door:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Hallo voorafgaand aan een andere code rijkleur hello, afhankelijk van of Hallo-taak voltooid is.

In de volgende regel hello hebt u Hallo code te volgen:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Volledige regel Hallo vervangen door Hallo code te volgen:

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

Hallo bovenstaande code wordt toegevoegd Hallo verzendknop die verwijst naar Hallo route die u eerder hebt gedefinieerd.

### <a name="test-hello-changes-locally"></a>Hallo wijzigingen lokaal testen

Uit de hoofddirectory Hallo van Hallo Git-opslagplaats, Hallo ontwikkelingsserver wordt uitgevoerd.

```bash
php artisan serve
```

toosee hello statuswijziging taak, te navigeren`http://localhost:8000` en selecteer Hallo selectievakje in.

![Toegevoegde selectievakje tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

toostop PHP, typ `Ctrl + C` in Hallo terminal.

### <a name="publish-changes-tooazure"></a>TooAzure wijzigingen publiceren

Voer in terminal hello, Laravel database migraties met Hallo productie connection string toomake Hallo wijziging in hello Azure-database.

```bash
php artisan migrate --env=production --force
```

Alle Hallo wijzigingen in Git doorvoeren en vervolgens push Hallo code wijzigingen tooAzure.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Eenmaal Hallo `git push` is voltooid, gaat u toohello Azure-web-app en test Hallo nieuwe functionaliteit.

![Model en de database wijzigingen tooAzure gepubliceerd](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Als u alle taken toegevoegd, worden ze in de database Hallo bewaard. Updates toohello gegevensschema laat de bestaande gegevens intact.

## <a name="stream-diagnostic-logs"></a>Diagnostische logboeken

Tijdens het Hallo PHP-toepassing in Azure App Service wordt uitgevoerd, kunt u Hallo console logboeken doorgesluisd tooyour terminal ophalen. Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.

toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Eenmaal streaming-logboek is gestart, sommige webverkeer vernieuwen in Hallo browser tooget hello Azure-web-app. U ziet nu console logboeken doorgesluisd toohello terminal. Als u de logboeken van console onmiddellijk niet ziet, controleert u opnieuw in 30 seconden.

toostop logboek streaming op elk gewenst moment, type `Ctrl` + `C`.

> [!TIP]
> Een PHP-toepassing kunt Hallo standaard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello-console. Hallo-voorbeeldtoepassing gebruikt deze benadering in _app/Http/routes.php_.
>
> Als een kader web [Laravel gebruikt Monolog](https://laravel.com/docs/5.4/errors) als Hallo logboekregistratie provider. toosee hoe tooget Monolog toooutput berichten toohello console raadpleegt [PHP: hoe toouse toolog tooconsole (php://out) monolog](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Hello Azure-web-app beheren

Ga toohello [Azure-portal](https://portal.azure.com) toomanage Hallo web-app die u hebt gemaakt.

In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

De pagina Overzicht van uw web-app wordt weergegeven. Hier kunt u eenvoudige beheertaken zoals stoppen, starten, opnieuw opstarten, bladeren en verwijderen uitvoeren.

Hallo linkermenu biedt pagina's voor het configureren van uw app.

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Een MySQL-database maken in Azure
> * Verbinding maken met een PHP-app tooMySQL
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * Hallo-app in hello Azure-portal beheren

De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooa web-app.

> [!div class="nextstepaction"]
> [Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md)
