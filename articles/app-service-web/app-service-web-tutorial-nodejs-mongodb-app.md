---
title: Een Node.js en MongoDB web-app in Azure bouwen | Microsoft Docs
description: Informatie over het ophalen van een Node.js-app in Azure, werken met verbinding met een Cosmos-DB-database met een verbindingsreeks voor MongoDB.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Een Node.js en MongoDB web-app in Azure bouwen

Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service. Deze zelfstudie laat zien hoe een Node.js-web-app in Azure maken en te verbinden met een MongoDB-database. Wanneer u bent klaar, hebt u een gemiddelde-toepassing (MongoDB, snelle AngularJS en Node.js) wordt uitgevoerd in [Azure App Service](app-service-web-overview.md). Voor de eenvoud, de voorbeeldtoepassing gebruikt de [MEAN.js webframework](http://meanjs.org/).

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Wat u leert het volgende:

> [!div class="checklist"]
> * Maak een MongoDB-database in Azure
> * Een Node.js-app verbinden met MongoDB
> * De app implementeren in Azure
> * Bijwerken van het gegevensmodel en de app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * De app in de Azure portal beheren

## <a name="prerequisites"></a>Vereisten

Vereisten voor het voltooien van deze zelfstudie:

1. [Git installeren](https://git-scm.com/)
1. [Node.js en NPM installeren](https://nodejs.org/)
1. [Installeer Gulp.js](http://gulpjs.com/) (vereist door de [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Installeren en uitvoeren van MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Test lokale MongoDB

Open de terminalvenster en `cd` naar de `bin` map van de MongoDB-installatie. Alle opdrachten kunt uitvoeren in deze zelfstudie kunt u deze terminalvenster.

Voer `mongo` in de terminal verbinding maken met uw lokale MongoDB-server.

```bash
mongo
```

Als de verbinding geslaagd is, wordt klikt u vervolgens de MongoDB-database al uitgevoerd. Als dit niet het geval is, zorg ervoor dat de lokale MongoDB-database is gestart door de stappen op [Installeer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Vaak MongoDB is geïnstalleerd, maar u moet nog steeds start met `mongod`. 

Wanneer u klaar bent test de MongoDB-database, typ `Ctrl+C` in de terminal. 

## <a name="create-local-nodejs-app"></a>Lokale Node.js-app maken

In deze stap moet u het lokale Node.js-project instellen.

### <a name="clone-the-sample-application"></a>De voorbeeldtoepassing klonen

In het terminalvenster `cd` in een werkmap.  

Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Deze repository voorbeeld bevat een kopie van de [MEAN.js opslagplaats](https://github.com/meanjs/mean). Het is gewijzigd om te worden uitgevoerd op App Service (voor meer informatie raadpleegt u de opslagplaats MEAN.js [Leesmij-bestand](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-the-application"></a>De toepassing uitvoeren

Voer de volgende opdrachten voor het installeren van de vereiste pakketten en de toepassing niet starten.

```bash
cd meanjs
npm install
npm start
```

Wanneer de app volledig wordt geladen is, ziet u iets soortgelijks als in het volgende bericht:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Navigeer naar http://localhost: 3000 in een browser. Klik op **aanmelden** in het bovenste menu en een testgebruiker maken. 

De MEAN.js-voorbeeldtoepassing slaat gebruikersgegevens op in de database. Als u geslaagde in het maken van een gebruiker en aanmelden, kunnen uw app is gegevens schrijven naar de lokale MongoDB-database.

![MEAN.js maakt een geslaagde verbinding met MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Selecteer **Admin > artikelen beheren** sommige artikelen toevoegen.

Als u wilt Node.js op elk gewenst moment stoppen, drukt u op `Ctrl+C` in de terminal. 

## <a name="create-production-mongodb"></a>Productie MongoDB maken

In deze stap maakt u een MongoDB-database in Azure. Wanneer uw app wordt geïmplementeerd naar Azure, wordt deze cloud-database gebruikt.

Voor MongoDB, het gebruik van deze zelfstudie [Azure Cosmos DB](/azure/documentdb/). MongoDB-clientverbindingen biedt ondersteuning voor cosmos DB.

### <a name="log-in-to-azure"></a>Meld u aan bij Azure.

U gebruikt CLI Azure 2.0 om de resources te maken die nodig zijn voor het hosten van uw app in Azure. Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

In het volgende voorbeeld wordt een resourcegroep gemaakt in de regio West-Europa.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Gebruik de [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI-opdracht naar de lijst met beschikbare locaties. 

### <a name="create-a-cosmos-db-account"></a>Een Cosmos-DB-account maken

Maak een Cosmos-DB-account met de [az cosmosdb maken](/cli/azure/cosmosdb#create) opdracht.

In de volgende opdracht te vervangen door een unieke naam van de Cosmos-database voor de  *\<cosmosdb_name >* tijdelijke aanduiding. Deze naam wordt gebruikt als het onderdeel van het eindpunt Cosmos DB `https://<cosmosdb_name>.documents.azure.com/`, zodat de naam moet uniek zijn in alle Cosmos-DB-accounts in Azure. De naam mag alleen kleine letters, cijfers en het koppelteken (-) en moet tussen 3 en 50 tekens bevatten.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

De *--kind MongoDB* parameter zorgt ervoor dat MongoDB-clientverbindingen.

Wanneer de Cosmos-DB-account is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a>App verbinden met productie MongoDB

In deze stap maakt u verbinding maken uw voorbeeldtoepassing MEAN.js naar de Cosmos-DB-database die u zojuist hebt gemaakt, met een verbindingsreeks voor MongoDB. 

### <a name="retrieve-the-database-key"></a>De databasesleutel ophalen

Voor verbinding met de database van de Cosmos-database, moet u de databasesleutel. Gebruik de opdracht [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) om de primaire sleutel op te halen.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

De Azure CLI toont informatie vergelijkbaar met het volgende voorbeeld:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Kopieer de waarde van `primaryMasterKey`. U hebt deze informatie nodig voor de volgende stap.

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a>Configureer de verbindingsreeks in uw Node.js-toepassing

Open in uw opslagplaats MEAN.js _config/env/production.js_.

In de `db` object, werk de waarde van `uri`:

* Vervang de twee  *\<cosmosdb_name >* tijdelijke aanduidingen door de naam van uw Cosmos-DB-database.
* Vervang de  *\<primary_master_key >* aanduiding voor items met de sleutel die u in de vorige stap hebt gekopieerd.

De volgende code toont de `db` object:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

De `ssl=true` optie is vereist omdat [Cosmos DB SSL vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Sla uw wijzigingen op.

### <a name="test-the-application-in-production-mode"></a>Test de toepassing in productiemodus 

Voer de volgende opdracht te minify en scripts voor de productie-omgeving te bundelen. Dit proces wordt gegenereerd voor de bestanden die nodig is voor de productie-omgeving.

```bash
gulp prod
```

Voer de volgende opdracht te gebruiken van de verbindingsreeks die u hebt geconfigureerd in _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Hiermee stelt u de variabele voor de omgeving waarin wordt uitgelegd Node.js om uit te voeren in de productieomgeving.  `node server.js`Hiermee start u de Node.js-server met `server.js` in de hoofdmap van uw opslagplaats. Dit is hoe uw Node.js-toepassing wordt geladen in Azure. 

Wanneer de app wordt geladen, moet u controleren om ervoor te zorgen dat deze wordt uitgevoerd in de productieomgeving:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Ga naar http://localhost:8443 in een browser. Klik op **aanmelden** in het bovenste menu en een testgebruiker maken. Als u geslaagde maken van een gebruiker en aanmelden, kunnen uw app is gegevens schrijven naar de database van de Cosmos-database in Azure. 

In de terminal in stoppen Node.js `Ctrl+C`. 

## <a name="deploy-app-to-azure"></a>App implementeren in Azure

In deze stap maakt implementeren u uw MongoDB verbonden Node.js-toepassing in Azure App Service.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

Maak een App Service-plan met de opdracht [az appservice plan create](/cli/azure/appservice/plan#create). 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Het volgende voorbeeld wordt een App Service-abonnement met de naam _myAppServicePlan_ met behulp van de **vrije** prijscategorie:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Wanneer de App Service-abonnement is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Een webtoepassing maken

Maak een WebApp in de `myAppServicePlan` App Service-abonnement met de [az webapp maken](/cli/azure/webapp#create) opdracht. 

De web-app hebt u een hosting ruimte om uw code te implementeren en biedt een URL op voor u de gedistribueerde toepassing weergeven. Gebruik te maken van de web-app. 

Vervang in de volgende opdracht, de  *\<app_naam >* aanduiding voor items met een unieke app-naam. Deze naam wordt gebruikt als het onderdeel van de standaard-URL voor de web-app zodat de naam moet uniek zijn in alle apps in Azure App Service. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld: 

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

### <a name="configure-an-environment-variable"></a>Configureren van een omgevingsvariabele

Eerder in de zelfstudie hardcoded verbinding met de database in de tekenreeks _config/env/production.js_. Aan best practice bij beveiliging wilt u deze gevoelige gegevens buiten de Git-opslagplaats te behouden. Voor uw app in Azure wordt uitgevoerd, gebruikt u een omgevingsvariabele in plaats daarvan.

In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van de [az webapp config appsettings bijwerken](/cli/azure/webapp/config/appsettings#update) opdracht. 

Het volgende voorbeeld wordt een `MONGODB_URI` app-instelling in uw Azure-web-app. Vervang de  *\<app_naam >*,  *\<cosmosdb_name >*, en  *\<primary_master_key >* tijdelijke aanduidingen.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

In een Node.js-code, opent u deze app-instelling met `process.env.MONGODB_URI`, net zoals u toegang krijgen een omgevingsvariabele tot zou. 

Nu uw wijzigingen ongedaan maken _config/env/production.js_ met de volgende opdracht:

```bash
git checkout -- .
```

Open _config/env/production.js_ opnieuw. Denk eraan dat de standaard MEAN.js-app al is geconfigureerd voor gebruik van de `MONGODB_URI` omgevingsvariabele die u hebt gemaakt.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Lokale Git-implementatie configureren 

Gebruik de [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht voor het maken van referenties voor implementatie.

U kunt uw toepassing in Azure App Service op verschillende manieren, met inbegrip van de FTP-, lokale Git, Visual Studio Team Services, GitHub en BitBucket implementeren. Voor FTP- en lokale Git is het nodig zijn voor een implementatie gebruiker geconfigureerd op de server voor verificatie van uw implementatie. Deze gebruiker implementatie-account-niveau en verschilt van de account van uw Azure-abonnement. Alleen moet u deze implementatie gebruiker één keer te configureren.

Vervang in de volgende opdracht *\<user-name>* en *\<password>* door een nieuwe gebruikersnaam en nieuw wachtwoord. De gebruikersnaam moet uniek zijn. Het wachtwoord moet ten minste acht tekens lang zijn en twee van de volgende drie items bevatten: letters, cijfers, symbolen. Als er een ` 'Conflict'. Details: 409`-fout optreedt, wijzigt u de gebruikersnaam. Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Noteer de gebruikersnaam en het wachtwoord voor gebruik in latere stappen wanneer u de app implementeert.

Gebruik de [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht voor het configureren van lokale Git-toegang tot de Azure-web-app. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Wanneer de gebruiker voor de implementatie is geconfigureerd, ziet u de implementatie-URL voor uw Azure-web-app met de Azure CLI in de volgende indeling:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Kopieer de uitvoer van de terminal zoals deze wordt gebruikt in de volgende stap. 

### <a name="push-to-azure-from-git"></a>Pushen naar Azure vanaf Git

Voeg een externe Azure-instantie toe aan uw lokale Git-opslagplaats. 

```bash
git remote add azure <paste_copied_url_here> 
```

Push naar de Azure-externe om uw Node.js-toepassing te implementeren. U wordt gevraagd naar het wachtwoord dat u eerder hebt opgegeven als onderdeel van het maken van de implementatiegebruiker. 

```bash
git push azure master
```

Azure App Service communiceert tijdens de implementatie van de voortgang met Git.

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

U merkt dat het implementatieproces wordt uitgevoerd [Gulp](http://gulpjs.com/) nadat `npm install`. App Service wordt niet Gulp of knorvis taken uitgevoerd tijdens de implementatie, zodat deze opslagplaats voorbeeld heeft twee extra bestanden in de hoofdmap in te schakelen: 

- _.Deployment_ -dit bestand vertelt App Service om uit te voeren `bash deploy.sh` als het script voor aangepaste implementatie.
- _Deploy.sh_ -het script voor aangepaste implementatie. Als u het bestand bekijkt, ziet u dat deze wordt uitgevoerd `gulp prod` nadat `npm install` en `bower install`. 

Deze aanpak kunt u een stap toevoegen aan uw implementatie op basis van Git. Als u uw Azure-web-app op elk moment opnieuw opstart, wordt niet deze automatiseringstaken opnieuw uitvoeren App Service.

### <a name="browse-to-the-azure-web-app"></a>Blader naar de Azure-web-app 

Blader naar de geïmplementeerde web-app met behulp van uw webbrowser. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Klik op **aanmelden** in het bovenste menu en maak een dummy-gebruiker. 

Als u met succes voltooid zijn en de app automatisch zich bij de gebruiker aanmeldt, heeft uw MEAN.js-app in Azure verbinding met de database MongoDB (Cosmos DB). 

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Selecteer **Admin > artikelen beheren** sommige artikelen toevoegen. 

**Gefeliciteerd!** U uitvoert een gegevensgestuurd Node.js-app in Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Update-gegevensmodel en de implementatie opnieuw uit

In deze stap maakt u wijzigt de `article` data model en de wijziging van uw publiceren naar Azure.

### <a name="update-the-data-model"></a>Bijwerken van het gegevensmodel

Open _modules/articles/server/models/article.server.model.js_.

In `ArticleSchema`, Voeg een `String` type aangeroepen `comment`. Wanneer u bent klaar, ziet uw schema-code als volgt:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a>De code artikelen bijwerken

Bijwerken van de rest van uw `articles` code voor het gebruik `comment`.

Er zijn vijf bestanden die u wilt wijzigen: de server-controller en de weergaven vier client. 

Open _modules/articles/server/controllers/articles.server.controller.js_.

In de `update` werkt, het toevoegen van een toewijzing voor `article.comment`. De volgende code toont de voltooide `update` functie:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Open _modules/articles/client/views/view-article.client.view.html_.

Net boven de afsluitende `</section>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Open _modules/articles/client/views/list-articles.client.view.html_.

Net boven de afsluitende `</a>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Open _modules/articles/client/views/admin/list-articles.client.view.html_.

In de `<div class="list-group">` element en net boven de afsluitende `</a>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Open _modules/articles/client/views/admin/form-article.client.view.html_.

Zoek de `<div class="form-group">` element met de verzendknop, welke ziet er als volgt:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Net boven deze tag toevoegen `<div class="form-group">` element waarmee mensen bewerken de `comment` veld. Uw nieuwe element moet er als volgt uitzien:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Uw wijzigingen lokaal testen

Sla al uw wijzigingen op.

Test uw wijzigingen opnieuw in de productiemodus.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Vergeet niet dat uw _config/env/production.js_ is hersteld, en de `MONGODB_URI` omgevingsvariabele wordt alleen ingesteld in uw Azure-web-app en niet op uw lokale computer. Als u het configuratiebestand bekijkt, kunt u vinden dat de productconfiguratie van de standaard voor het gebruik van een lokale MongoDB-database. Dit zorgt ervoor dat u productiegegevens niet raken als u uw codewijzigingen lokaal testen.

Navigeer naar `http://localhost:8443` in een browser en zorg ervoor dat u bent aangemeld.

Selecteer **Admin > artikelen beheren**, klikt u vervolgens een artikel toevoegen door te selecteren de  **+**  knop.

U ziet de nieuwe `Comment` textbox nu.

![Veld toegevoegde opmerking aan artikelen](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

In de terminal in stoppen Node.js `Ctrl+C`. 

### <a name="publish-changes-to-azure"></a>Wijzigingen publiceren naar Azure

Uw wijzigingen in Git en vervolgens de codewijzigingen pushen naar Azure.

```bash
git commit -am "added article comment"
git push azure master
```

Eenmaal de `git push` is voltooid, gaat u naar uw Azure-web-app en de nieuwe functionaliteit uitproberen.

![Model en de database-wijzigingen die zijn gepubliceerd naar Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Als u alle artikelen die eerder is toegevoegd, kunt u nog steeds zien. Bestaande gegevens in uw Cosmos-database is niet verloren gaan. Ook de updates aan het gegevensschema en uw bestaande gegevens intact blijft.

## <a name="stream-diagnostic-logs"></a>Diagnostische logboeken 

Als uw Node.js-toepassing in Azure App Service wordt uitgevoerd, kunt u de logboeken van de console doorgesluisd naar uw terminal opvragen. Op die manier kunt u de dezelfde diagnostische berichten op te sporen toepassingsfouten ophalen.

Gebruik voor het starten van de streaming-logboek de [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Uw Azure-web-app in de browser om op te halen van sommige webverkeer eenmaal streaming-logboek is gestart, worden vernieuwd. U ziet nu de logboeken van de console is doorgegeven naar de terminal.

Stop log streaming op elk gewenst moment door typen `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga naar de [Azure-portal](https://portal.azure.com) om te zien van de web-app die u hebt gemaakt.

Klik vanuit het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Standaard ziet u de portal voor uw web-app **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. De tabbladen aan de linkerkant van de pagina's worden weergegeven de andere configuratie dat kunt u openen.

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Volgende stappen

Wat u hebt geleerd:

> [!div class="checklist"]
> * Maak een MongoDB-database in Azure
> * Een Node.js-app verbinden met MongoDB
> * De app implementeren in Azure
> * Bijwerken van het gegevensmodel en de app implementeren
> * Logboeken van de stroom van Azure naar uw terminal
> * De app in de Azure portal beheren

Ga naar de volgende zelfstudie voor informatie over het toewijzen van een aangepaste DNS-naam aan uw web-app.

> [!div class="nextstepaction"] 
> [Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps](app-service-web-tutorial-custom-domain.md)
