---
title: aaaBuild een Docker Python en PostgreSQL web-app in Azure | Microsoft Docs
description: Meer informatie over hoe tooget een Docker-Python-app in Azure AD werkt met verbinding tooa PostgreSQL-database.
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Een Docker Python en PostgreSQL web-app in Azure bouwen

Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service. Deze zelfstudie laat zien hoe een basic Docker-Python toocreate web-app in Azure. U maakt verbinding met deze app tooa PostgreSQL-database. Wanneer u bent klaar, hebt u een Python Flask-toepassing uitgevoerd binnen een Docker-container op [Azure App Service Web Apps](app-service-web-overview.md).

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

U kunt stappen Hallo hieronder op Mac OS. Instructies voor Linux en Windows zijn hetzelfde in de meeste gevallen hello, maar Hallo verschillen niet worden beschreven in deze zelfstudie.
 
## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

1. [Git installeren](https://git-scm.com/)
1. [Python installeren](https://www.python.org/downloads/)
1. [Installeren en uitvoeren van PostgreSQL](https://www.postgresql.org/download/)
1. [Docker-Community Edition installeren](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Lokale PostgreSQL-installatie testen en een database maken

Open Hallo terminalvenster en voer `psql postgres` tooconnect tooyour lokale PostgreSQL-server.

```bash
psql postgres
```

Als de verbinding geslaagd is, wordt uw PostgreSQL-database wordt uitgevoerd. Als dit niet het geval is, zorg ervoor dat de lokale PostgresQL-database is gestart door Hallo stappen op te volgen [Downloads - PostgreSQL Core distributie](https://www.postgresql.org/download/).

Maken van een database met de naam *eventregistration* en instellen van de gebruiker van een aparte database met de naam *manager* met wachtwoord *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Type *\q* tooexit hello PostgreSQL-client. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Lokale Python Flask-toepassing maken

In deze stap maakt instellen u lokaal Python Flask-project Hallo.

### <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Open Hallo terminalvenster, en `CD` tooa werkmap.  

Voer Hallo deze opdrachten tooclone Hallo voorbeeld opslagplaats en gaat u naar toohello *0,1 initialapp* release.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Deze repository voorbeeld bevat een [Flask](http://flask.pocoo.org/) toepassing. 

### <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

> [!NOTE] 
> In een latere stap kunt u dit proces met het bouwen van een toouse Docker-container met de productiedatabase Hallo vereenvoudigen.

Vereist hello-pakketten installeren en start de toepassing hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Toohttp://127.0.0.1:5000 in een browser navigeren. Klik op **registreren!** en een testgebruiker maken.

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

Hallo Flask-voorbeeldtoepassing slaat gebruikersgegevens in Hallo-database. Als u succesvol bij het registreren van een gebruiker, wordt uw app gegevens toohello lokale PostgreSQL-database geschreven.

toostop hello Flask-server op elk gewenst moment, typt u Ctrl + C in Hallo terminal. 

## <a name="create-a-production-postgresql-database"></a>Een productie-PostgreSQL-database maken

In deze stap maakt u een PostgreSQL-database in Azure. Wanneer uw app geïmplementeerde tooAzure is, wordt deze cloud-database gebruikt.

### <a name="log-in-tooazure"></a>Meld u bij tooAzure

U bent nu gaat toouse hello Azure CLI 2.0 toocreate Hallo resources die nodig toohost uw toepassing Python in Azure App Service zijn.  Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) Hello [az groep maken](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hallo volgende voorbeeld wordt een resourcegroep in de regio VS-West Hallo:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI opdracht toolist beschikbare locaties.

### <a name="create-an-azure-database-for-postgresql-server"></a>Een Azure-database voor PostgreSQL-server maken

Een PostgreSQL-server maken met de Hallo [az postgres server maken](/cli/azure/documentdb#create) opdracht.

In Hallo volgende opdracht, vervangt u een unieke naam voor Hallo  *\<postgresql_name >* tijdelijke aanduiding en een gebruikersnaam voor Hallo  *\<admin_username >* tijdelijke aanduiding voor . Hallo-servernaam wordt gebruikt als onderdeel van uw eindpunt PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), zodat het Hallo-naam moet toobe unieke op alle servers in Azure. Hallo-gebruikersnaam is voor Hallo initiële database admin-gebruikersaccount. U bent na vragen aan gebruiker toopick een wachtwoord voor deze gebruiker.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Wanneer hello Azure Database voor PostgreSQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Een firewallregel voor hello Azure Database voor PostgreSQL-server maken

Hallo volgende Azure CLI opdracht tooallow access toohello-database uit alle IP-adressen worden uitgevoerd.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello Azure CLI bevestigt Hallo firewall-regel maken met uitvoer vergelijkbare toohello voorbeeld te volgen:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Verbinding maken met uw database Python Flask-toepassing toohello

In deze stap maakt u verbinding maken uw Python Flask-voorbeeld toepassing toohello Azure Database voor PostgreSQL-server die u hebt gemaakt.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Een lege database maken en een nieuwe gebruiker van de database-toepassing instellen

Maak een databasegebruiker met toegang tooa enkele database alleen. U gebruikt deze referenties tooavoid geeft volledige toegang Hallo-toohello toepassingsserver.

Verbinding maken met toohello-database (u wordt gevraagd om uw wachtwoord admin).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Hallo-database en de gebruikersgegevens van Hallo PostgreSQL CLI maken.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Type *\q* tooexit hello PostgreSQL-client.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Hallo toepassing testen lokaal op Hallo Azure PostgreSQL-database 

Ga terug nu toohello *app* map Hallo gekloond Github-opslagplaats, kunt u Hallo Python Flask-toepassing uitvoeren door omgevingsvariabelen Hallo-database bij te werken.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Toohttp://127.0.0.1:5000 in een browser navigeren. Klik op **registreren!** en maak de registratie van een test. U schrijft gegevens toohello database nu in Azure.

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Hallo toepassing uitvoert vanuit een Docker-Container

Hallo Docker-container installatiekopie maken.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker geeft een bevestiging die it gemaakt Hallo-container.

```bash
Successfully built 7548f983a36b
```

Toevoegen van de omgeving variabelen tooan omgeving variabele databasebestand *db.env*. Hallo-app verbinding toohello PostgreSQL-productiedatabase in Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Hallo-app uit Hallo Docker-container wordt uitgevoerd. Hallo volgende opdracht geeft Hallo omgeving variabele bestand en Hallo Flask poort 5000 toolocal standaardpoort 5000 wordt toegewezen.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

Hallo-uitvoer is vergelijkbaar toowhat die u eerder hebt gezien. Echter Hallo initiële database wilt migreren niet langer nodig heeft toobe uitgevoerd en daarom wordt overgeslagen.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

Hallo-database bevat al Hallo registratie die u eerder hebt gemaakt.

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Hallo Docker-container tooa container register uploaden

In deze stap maakt uploaden u Hallo Docker-container tooa container register. Gebruikt u Azure Container register, maar u kunt ook andere populaire protocollen zoals Docker-Hub.

### <a name="create-an-azure-container-registry"></a>Een Azure Container Registry maken

Vervang in Hallo na de opdracht toocreate een container register  *\<registry_name >* met een unieke Azure container register-naam van uw keuze.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Uitvoer
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Hallo register referenties voor pushen en installatiekopieën van Docker binnenhalen ophalen

tooshow register referenties, schakel eerst Administrator-modus.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Ziet u twee wachtwoorden. Noteer Hallo-gebruikersnaam en het Hallo eerste wachtwoord.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Upload uw Docker-container tooAzure Container register

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Hallo Docker Python Flask-toepassing tooAzure implementeren

In deze stap maakt implementeren u uw tooAzure in Docker-container gebaseerde door toepassing Python Flask-App Service.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hallo volgende voorbeeld wordt een op basis van Linux-App Service-plan met de naam *myAppServicePlan* Hallo S1 prijscategorie met:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Een webtoepassing maken

Een web-app maken in Hallo *myAppServicePlan* App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht. 

Hallo web app geeft u een hosting-ruimte toodeploy uw code en biedt een URL voor u tooview Hallo toepassing geïmplementeerd. Gebruik toocreate Hallo web-app. 

Hallo opdracht, na Vervang in Hallo  *\<app_naam >* aanduiding voor items met een unieke app-naam. Deze naam is onderdeel van Hallo standaard-URL voor de web-app hello, zodat het Hallo-naam moet toobe uniek zijn in alle apps in Azure App Service. 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Wanneer het Hallo-web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-hello-database-environment-variables"></a>Omgevingsvariabelen Hallo-database configureren

Eerder in de zelfstudie hello, moet u omgeving variabelen tooconnect tooyour PostgreSQL-database gedefinieerd.

In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings set](/cli/azure/webapp/config#set) opdracht. 

Hallo geeft volgende voorbeeld Hallo database Verbindingsdetails als app-instellingen. Gebruikt ook Hallo *poort* variabele toomap poort 5000 van uw Docker-Container tooreceive HTTP-verkeer op poort 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Docker-container implementatie configureren 

AppService kan automatisch downloaden en uitvoeren van een Docker-container.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Wanneer u Hallo Docker-container bijwerken of Hallo instellingen wijzigt, start u Hallo app opnieuw. Opnieuw opstarten zorgt ervoor dat alle instellingen worden toegepast en de meest recente container Hallo vandaan Hallo register.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure-web-app bladeren 

Bladeren toohello geïmplementeerd web-app met uw webbrowser. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Hallo-web-app duurt langer tooload omdat Hallo container toobe gedownload en gestart nadat het Hallo-container configuratie wordt gewijzigd.

Er is eerder geregistreerde gasten die toohello Azure productiedatabase zijn opgeslagen in de vorige stap Hallo.

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Gefeliciteerd!** U uitvoert een Docker-container gebaseerde Python Flask-app in Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Update-gegevensmodel en de implementatie opnieuw uit

In deze stap kunt u het aantal deelnemers tooeach gebeurtenisregistratie Hallo toevoegen door Hallo Gast model bij te werken.

Bekijk Hallo *0,2 migratie* release Hello volgende git-opdracht:

```bash
git checkout tags/0.2-migration
```

Deze release Hallo noodzakelijke wijzigingen tooviews, domeincontrollers en model al is gedaan. Dit omvat ook de databasemigratie van een gegenereerd *alembic* (`flask db migrate`). Hier ziet u alle wijzigingen die via Hallo volgende git-opdracht:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Uw wijzigingen lokaal testen

Hallo opdrachten tootest na uw wijzigingen lokaal uitvoeren door waarop Hallo flask-server.

Mac / Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Navigeer toohttp://127.0.0.1:5000 in uw browser tooview Hallo wijzigingen. Een test maken.

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>TooAzure wijzigingen publiceren

Hallo nieuwe docker-installatiekopie bouwen, dit toohello container register doorgeven en start Hallo app opnieuw.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Navigeer tooyour Azure-web-app en nieuwe functionaliteit Hallo opnieuw uitproberen. Maak een andere gebeurtenisregistratie.

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt.

In het linkermenu hello, klikt u op **App Services**, klikt u op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Standaard Hallo portal uw web-app toont **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen.

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Volgende stappen

De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooyour web-app.

> [!div class="nextstepaction"] 
> [Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md)
