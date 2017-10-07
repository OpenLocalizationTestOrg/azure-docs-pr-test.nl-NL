---
title: een Node.js en MongoDB web-app in Azure aaaBuild | Microsoft Docs
description: Meer informatie over hoe een Node.js-app in Azure AD werkt met verbinding tooa Cosmos DB database met een verbindingsreeks MongoDB tooget.
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
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Een Node.js en MongoDB web-app in Azure bouwen

Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service. Deze zelfstudie laat zien hoe toocreate een Node.js web-app in Azure en verbinding maken met het tooa MongoDB-database. Wanneer u bent klaar, hebt u een gemiddelde-toepassing (MongoDB, snelle AngularJS en Node.js) wordt uitgevoerd in [Azure App Service](app-service-web-overview.md). Voor het gemak, Hallo-voorbeeldtoepassing gebruikt Hallo [MEAN.js webframework](http://meanjs.org/).

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Wat u leert het volgende:

> [!div class="checklist"]
> * Maak een MongoDB-database in Azure
> * Verbinding maken met een Node.js-app tooMongoDB
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * Hallo-app in hello Azure-portal beheren

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

1. [Git installeren](https://git-scm.com/)
1. [Node.js en NPM installeren](https://nodejs.org/)
1. [Installeer Gulp.js](http://gulpjs.com/) (vereist door de [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Installeren en uitvoeren van MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Test lokale MongoDB

Open Hallo terminalvenster en `cd` toohello `bin` map van de MongoDB-installatie. U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.

Voer `mongo` in Hallo terminal tooconnect tooyour lokale MongoDB-server.

```bash
mongo
```

Als de verbinding geslaagd is, wordt klikt u vervolgens de MongoDB-database al uitgevoerd. Als dit niet het geval is, zorg ervoor dat uw lokale MongoDB-database is gestart door de stappen op Hallo [Installeer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Vaak MongoDB is geïnstalleerd, maar u moet nog steeds toostart het door het uitvoeren van `mongod`. 

Wanneer u klaar bent test de MongoDB-database, typ `Ctrl+C` in Hallo terminal. 

## <a name="create-local-nodejs-app"></a>Lokale Node.js-app maken

In deze stap maakt instellen u lokaal Node.js-project Hallo.

### <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

In het terminalvenster hello, `cd` tooa werkmap.  

Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Deze repository voorbeeld bevat een kopie van Hallo [MEAN.js opslagplaats](https://github.com/meanjs/mean). Het gewijzigde toorun op App Service is (Zie voor meer informatie, Hallo MEAN.js opslagplaats [Leesmij-bestand](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Voer Hallo opdrachten tooinstall vereist hello-pakketten te volgen en Hallo toepassing starten.

```bash
cd meanjs
npm install
npm start
```

Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:

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

Toohttp://localhost:3000 in een browser navigeren. Klik op **aanmelden** in Hallo bovenste menu en een testgebruiker maken. 

Hallo MEAN.js voorbeeldtoepassing slaat gebruikersgegevens in Hallo-database. Als u geslaagde in het maken van een gebruiker en aanmelden, wordt uw app gegevens toohello lokale MongoDB-database geschreven.

![MEAN.js verbinding maakt met succes tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Selecteer **Admin > artikelen beheren** tooadd sommige artikelen.

Druk op toostop Node.js op elk gewenst moment `Ctrl+C` in Hallo terminal. 

## <a name="create-production-mongodb"></a>Productie MongoDB maken

In deze stap maakt u een MongoDB-database in Azure. Wanneer uw app geïmplementeerd tooAzure is, gebruikt deze cloud-database.

Voor MongoDB, het gebruik van deze zelfstudie [Azure Cosmos DB](/azure/documentdb/). MongoDB-clientverbindingen biedt ondersteuning voor cosmos DB.

### <a name="log-in-tooazure"></a>Meld u bij tooAzure

U gebruikt hello Azure CLI 2.0 toocreate Hallo benodigde resources toohost uw app in Azure. Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hallo maakt volgende voorbeeld een resourcegroep in de regio West-Europa Hallo.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI opdracht toolist beschikbare locaties. 

### <a name="create-a-cosmos-db-account"></a>Een Cosmos-DB-account maken

Een Cosmos-DB-account maken met de Hallo [az cosmosdb maken](/cli/azure/cosmosdb#create) opdracht.

In Hallo volgende opdracht, vervangt u een unieke naam van de Cosmos-DB voor Hallo  *\<cosmosdb_name >* tijdelijke aanduiding. Deze naam wordt gebruikt als onderdeel van het eindpunt van de Cosmos-DB hello, Hallo `https://<cosmosdb_name>.documents.azure.com/`, zodat het Hallo-naam moet toobe unieke alle Cosmos-DB-accounts in Azure. Hallo-naam mag alleen kleine letters, cijfers en Hallo koppelteken (-) en moet tussen 3 en 50 tekens bevatten.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Hallo *--kind MongoDB* parameter zorgt ervoor dat MongoDB-clientverbindingen.

Wanneer Hallo Cosmos-DB-account is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

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

## <a name="connect-app-tooproduction-mongodb"></a>Verbinding maken met app-tooproduction MongoDB

In deze stap maakt u verbinding maken uw MEAN.js toepassing toohello Cosmos DB voorbeelddatabase die u zojuist hebt gemaakt, met een verbindingsreeks voor MongoDB. 

### <a name="retrieve-hello-database-key"></a>Hallo databasesleutel ophalen

tooconnect toohello Cosmos-DB-database, moet u Hallo databasesleutel. Gebruik Hallo [az cosmosdb lijst-sleutels](/cli/azure/cosmosdb#list-keys) opdracht tooretrieve Hallo primaire sleutel.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello Azure CLI ziet u informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Hallo-waarde van kopiëren `primaryMasterKey`. U moet deze informatie in de volgende stap Hallo.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Hallo-verbindingsreeks configureren in uw Node.js-toepassing

Open in uw opslagplaats MEAN.js _config/env/production.js_.

In Hallo `db` object, werk Hallo-waarde van `uri`:

* Vervang Hallo twee  *\<cosmosdb_name >* tijdelijke aanduidingen door de naam van uw Cosmos-DB-database.
* Vervang Hallo  *\<primary_master_key >* tijdelijke aanduiding met Hallo-sleutel die u in de vorige stap Hallo hebt gekopieerd.

Hallo volgende code toont Hallo `db` object:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Hallo `ssl=true` optie is vereist omdat [Cosmos DB SSL vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Sla uw wijzigingen op.

### <a name="test-hello-application-in-production-mode"></a>Hallo-toepassing in de productiemodus testen 

Na de opdracht toominify en de bundel scripts voor de productieomgeving Hallo Hallo worden uitgevoerd. Dit proces Hallo-bestanden die nodig is voor productie-omgeving Hallo gegenereerd.

```bash
gulp prod
```

Voer Hallo opdracht toouse Hallo verbindingsreeks u hebt geconfigureerd in volgende _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Hiermee stelt u Hallo omgevingsvariabele waarin wordt uitgelegd Node.js toorun in Hallo-productieomgeving.  `node server.js`Start Hallo Node.js-server met `server.js` in de hoofdmap van uw opslagplaats. Dit is hoe uw Node.js-toepassing wordt geladen in Azure. 

Wanneer de app hello wordt geladen, controleert u ervoor dat deze wordt uitgevoerd in de productieomgeving Hallo toomake:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Toohttp://localhost:8443 in een browser navigeren. Klik op **aanmelden** in Hallo bovenste menu en een testgebruiker maken. Als u geslaagde maken van een gebruiker en aanmelden, kunnen uw app is gegevens toohello Cosmos DB database schrijven in Azure. 

In terminal hello, stopt u Node.js door `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>App-tooAzure implementeren

In deze stap maakt implementeren u uw toepassing tooAzure voor MongoDB verbonden Node.js-App Service.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hallo volgende voorbeeld maakt u een App Service-abonnement met de naam _myAppServicePlan_ met Hallo **vrije** prijscategorie:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

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

Een web-app maken in Hallo `myAppServicePlan` App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht. 

Hallo web app geeft u een hosting-ruimte toodeploy uw code en biedt een URL voor u tooview Hallo toepassing geïmplementeerd. Gebruik toocreate Hallo web-app. 

Hallo opdracht, na Vervang in Hallo  *\<app_naam >* aanduiding voor items met een unieke app-naam. Deze naam wordt gebruikt als onderdeel van de standaard-URL Hallo Hallo voor Hallo web-app, zodat het Hallo-naam moet toobe uniek zijn in alle apps in Azure App Service. 

```azurecli-interactive
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

### <a name="configure-an-environment-variable"></a>Configureren van een omgevingsvariabele

Eerder in Hallo zelfstudie, u hardcoded Hallo databaseverbindingsreeks in _config/env/production.js_. Aan de aanbevolen beveiligingsprocedure wilt u tookeep deze gevoelige gegevens buiten de Git-opslagplaats. Voor uw app in Azure wordt uitgevoerd, gebruikt u een omgevingsvariabele in plaats daarvan.

In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings bijwerken](/cli/azure/webapp/config/appsettings#update) opdracht. 

Hallo volgende voorbeeld wordt een `MONGODB_URI` app-instelling in uw Azure-web-app. Vervang Hallo  *\<app_naam >*,  *\<cosmosdb_name >*, en  *\<primary_master_key >* tijdelijke aanduidingen.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

In een Node.js-code, opent u deze app-instelling met `process.env.MONGODB_URI`, net zoals u toegang krijgen een omgevingsvariabele tot zou. 

Nu uw too_config/env/production.js_ wijzigingen ongedaan Hello volgende opdracht:

```bash
git checkout -- .
```

Open _config/env/production.js_ opnieuw. Houd er rekening mee dat Hallo standaard MEAN.js app is al geconfigureerde toouse Hallo `MONGODB_URI` omgevingsvariabele die u hebt gemaakt.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Lokale Git-implementatie configureren 

Gebruik Hallo [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht toocreate referenties voor implementatie.

U kunt uw toepassing tooAzure App Service op verschillende manieren, met inbegrip van de FTP-, lokale Git, Visual Studio Team Services, GitHub en BitBucket implementeren. Voor de FTP- en lokale Git, is het noodzakelijk toohave implementatie van een gebruiker geconfigureerd op Hallo server tooauthenticate uw implementatie. Deze gebruiker implementatie-account-niveau en verschilt van de account van uw Azure-abonnement. U hoeft alleen tooconfigure deze implementatie gebruiker één keer.

Hallo opdracht, na Vervang in  *\<gebruikersnaam >* en  *\<wachtwoord >* met een nieuwe gebruikersnaam en wachtwoord. Hallo-gebruikersnaam moet uniek zijn. Hallo wachtwoord moet ten minste acht tekens lang zijn, met twee Hallo na drie elementen: letters, cijfers, symbolen. Als u krijgt een ` 'Conflict'. Details: 409` fout, wijziging Hallo gebruikersnaam. Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Record Hallo-gebruikersnaam en wachtwoord voor gebruik in latere stappen wanneer u Hallo app implementeert.

Gebruik Hallo [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht tooconfigure lokale Git access toohello Azure-web-app. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Wanneer Hallo implementatie gebruiker is geconfigureerd, wordt het hello Azure CLI Hallo implementatie URL voor uw Azure-web-app in Hallo volgende indeling:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

De uitvoer van Hallo terminal Hallo kopiëren wordt dit gebruikt in de volgende stap Hallo. 

### <a name="push-tooazure-from-git"></a>TooAzure van Git push

Een Azure externe tooyour lokale Git-opslagplaats toevoegen. 

```bash
git remote add azure <paste_copied_url_here> 
```

Push toohello Azure externe toodeploy uw Node.js-toepassing. U wordt gevraagd om Hallo wachtwoord die u eerder hebt opgegeven als onderdeel van Hallo maken van Hallo implementatie gebruiker. 

```bash
git push azure master
```

Azure App Service communiceert tijdens de implementatie van de voortgang met Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

U merkt dat het implementatieproces hello wordt uitgevoerd [Gulp](http://gulpjs.com/) nadat `npm install`. App Service Gulp of knorvis taken kan niet worden uitgevoerd tijdens de implementatie, zodat deze opslagplaats voorbeeld heeft twee extra bestanden in de hoofdmap directory tooenable: 

- _.Deployment_ -dit bestand vertelt App Service-toorun `bash deploy.sh` als Hallo aangepaste implementatiescript.
- _Deploy.sh_ -script voor aangepaste implementatie Hallo. Als u hello bestand bekijkt, ziet u dat deze wordt uitgevoerd `gulp prod` nadat `npm install` en `bower install`. 

U kunt deze benadering tooadd elke stap tooyour implementatie op basis van Git gebruiken. Als u uw Azure-web-app op elk moment opnieuw opstart, wordt niet deze automatiseringstaken opnieuw uitvoeren App Service.

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure-web-app bladeren 

Bladeren toohello geïmplementeerd web-app met uw webbrowser. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Klik op **aanmelden** in Hallo bovenste menu en maak een dummy-gebruiker. 

Als u geslaagde en Hallo app automatisch aanmeldt heeft toohello gebruiker en vervolgens uw app MEAN.js gemaakt in Azure connectiviteit toohello MongoDB (Cosmos DB)-database. 

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Selecteer **Admin > artikelen beheren** tooadd sommige artikelen. 

**Gefeliciteerd!** U uitvoert een gegevensgestuurd Node.js-app in Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Update-gegevensmodel en de implementatie opnieuw uit

In deze stap maakt u Hallo wijzigen `article` data model en publiceren van uw tooAzure wijzigen.

### <a name="update-hello-data-model"></a>Hallo-gegevensmodel bijwerken

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

### <a name="update-hello-articles-code"></a>Hallo artikelen code bijwerken

Bijwerken van Hallo rest van uw `articles` toouse code `comment`.

Er zijn vijf bestanden die u nodig hebt toomodify: Hallo server domeincontroller en Hallo vier client weergaven. 

Open _modules/articles/server/controllers/articles.server.controller.js_.

In Hallo `update` werkt, het toevoegen van een toewijzing voor `article.comment`. Hallo volgende code toont Hallo voltooid `update` functie:

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

Hallo sluiten erboven `</section>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Open _modules/articles/client/views/list-articles.client.view.html_.

Hallo sluiten erboven `</a>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Open _modules/articles/client/views/admin/list-articles.client.view.html_.

Hallo binnen `<div class="list-group">` element en erboven Hallo sluiten `</a>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Open _modules/articles/client/views/admin/form-article.client.view.html_.

Hallo zoeken `<div class="form-group">` element met de verzendknop hello, welke ziet er als volgt:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Net boven deze tag toevoegen `<div class="form-group">` element waarmee mensen Hallo bewerken `comment` veld. Uw nieuwe element moet er als volgt uitzien:

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
> Vergeet niet dat uw _config/env/production.js_ is hersteld en Hallo `MONGODB_URI` omgevingsvariabele wordt alleen ingesteld in uw Azure-web-app en niet op uw lokale computer. Als u het configuratiebestand Hallo bekijkt, vindt u die Hallo productconfiguratie standaard toouse een lokale MongoDB-database. Dit zorgt ervoor dat u productiegegevens niet raken als u uw codewijzigingen lokaal testen.

Navigeer te`http://localhost:8443` in een browser en zorg ervoor dat u bent aangemeld.

Selecteer **Admin > artikelen beheren**, klikt u vervolgens een artikel toevoegen door te selecteren van Hallo  **+**  knop.

U ziet Hallo nieuwe `Comment` textbox nu.

![Toegevoegde opmerking veld tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

In terminal hello, stopt u Node.js door `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>TooAzure wijzigingen publiceren

Uw wijzigingen in Git en push ze Hallo code wijzigingen tooAzure.

```bash
git commit -am "added article comment"
git push azure master
```

Eenmaal Hallo `git push` is voltooid, gaat u tooyour Azure-web-app en de nieuwe functionaliteit Hallo uitproberen.

![Model en de database wijzigingen tooAzure gepubliceerd](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Als u alle artikelen die eerder is toegevoegd, kunt u nog steeds zien. Bestaande gegevens in uw Cosmos-database is niet verloren gaan. Bovendien uw updates toohello gegevensschema en uw bestaande gegevens intact blijft.

## <a name="stream-diagnostic-logs"></a>Diagnostische logboeken 

Als uw Node.js-toepassing in Azure App Service wordt uitgevoerd, kunt u Hallo console logboeken doorgesluisd tooyour terminal opvragen. Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.

toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Eenmaal streaming-logboek is gestart, worden uw Azure-web-app in Hallo browser tooget sommige webverkeer vernieuwd. U ziet nu de logboeken van console doorgesluisd tooyour terminal.

Stop log streaming op elk gewenst moment door typen `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt.

In het linkermenu hello, klikt u op **App Services**, klikt u op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Standaard Hallo portal uw web-app toont **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen.

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Volgende stappen

Wat u hebt geleerd:

> [!div class="checklist"]
> * Maak een MongoDB-database in Azure
> * Verbinding maken met een Node.js-app tooMongoDB
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Logboeken van de stroom van Azure tooyour terminal
> * Hallo-app in hello Azure-portal beheren

De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooyour web-app.

> [!div class="nextstepaction"] 
> [Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md)
