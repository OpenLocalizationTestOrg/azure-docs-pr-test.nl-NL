---
title: Node.js-web-app met de Azure-tabelservice
description: Deze zelfstudie leert u hoe de Azure Table-service gebruiken voor het opslaan van gegevens van een Node.js-toepassing die wordt gehost in Azure App Service Web Apps.
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a>Node.js-web-app met de Azure-tabelservice
## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe u tabel-service van Azure Data Management opslaan en gebruiken van gegevens uit een [knooppunt] toepassing wordt gehost [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps. Deze zelfstudie wordt ervan uitgegaan dat u hebt enige ervaring met knooppunt en [Git].

U leert:

* Hoe de knooppunt-modules installeren met npm (Pakketbeheer knooppunt)
* Werken met de Azure Table-service
* Het gebruik van de Azure CLI voor het maken van een web-app.

Door deze zelfstudie te volgen, bouwt u een eenvoudige web gebaseerde 'takenlijst'-toepassing die u kunt maken, ophalen en uitvoeren van taken. De taken worden opgeslagen in de tabel-service.

Hier volgt de voltooide toepassing:

![Een webpagina een leeg tasklist weergeven][node-table-finished]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="prerequisites"></a>Vereisten
Voordat u de instructies in dit artikel uitvoert, zorg ervoor dat u het volgende zijn geïnstalleerd hebt:

* [knooppunt] versie 0.10.24 of hoger
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Een opslagaccount maken
Een Azure-opslagaccount maken. De app wordt dit account gebruiken voor het opslaan van de taakitems.

1. Meld u aan bij de [Azure-Portal](https://portal.azure.com/).
2. Klik op de **nieuw** pictogram aan de onderkant van de portal links, klikt u op **gegevens en opslag** > **opslag**. Geef het storage-account een unieke naam en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.
   
      ![Knop Nieuw](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Wanneer het opslagaccount is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en het opslagaccount blade geopend om weer te geven dat hoort bij de nieuwe resourcegroep die u hebt gemaakt.
3. Klik op het opslagaccount blade **instellingen** > **sleutels**. De primaire toegangssleutel naar het Klembord kopiëren.
   
    ![Toegangstoets][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Modules installeren en steigers genereren
In deze sectie wordt u een nieuw knooppunttoepassing maken en npm module pakketten moeten worden toegevoegd. Voor deze toepassing gebruikt u de [Express] en [Azure] modules. De Express-module biedt een framework Model-View-Controller voor knooppunt terwijl de modules die Azure biedt verbinding met de tabel-service.

### <a name="install-express-and-generate-scaffolding"></a>Express installeren en steigers genereren
1. Maak een nieuwe map met de naam vanaf de opdrachtregel **tasklist** en Ga naar de map.  
2. Voer de volgende opdracht voor het installeren van de Express-module.
   
        npm install express-generator@4.2.0 -g
   
    Afhankelijk van het besturingssysteem moet u mogelijk plaatsen 'sudo ' uitgebreid voor de opdracht:
   
        sudo npm install express-generator@4.2.0 -g
   
    De uitvoer lijkt op het volgende voorbeeld:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > De '-g' parameter wordt de module globaal geïnstalleerd. Op die manier kunnen we gebruiken **snelle** voor het genereren van web-app steigers zonder aanvullende padinformatie typen.
   > 
   > 
3. Voer voor het maken van de steiger voor de toepassing de **snelle** opdracht:
   
        express
   
    De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    U hebt nu verschillende nieuwe mappen en bestanden in de **tasklist** directory.

### <a name="install-additional-modules"></a>Aanvullende modules installeren
Een van de bestanden die **snelle** maakt is **package.json**. Dit bestand bevat een lijst met afhankelijkheden van de module. Later, wanneer u de toepassing naar App Service Web Apps implementeert, bepaalt dit bestand welke modules moeten worden geïnstalleerd op Azure.

Vanaf de opdrachtregel, voer de volgende opdracht voor het installeren van de modules die zijn beschreven in de **package.json** bestand. U wilt gebruiken 'sudo ' uitgebreid.

    npm install

De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Geef vervolgens de volgende opdracht voor het installeren van de [azure], [knooppunt uuid], [nconf] en [asynchrone] modules:

    npm install azure-storage node-uuid async nconf --save

De **--opslaan** vlag voegt vermeldingen voor deze modules naar de **package.json** bestand.

De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a>De toepassing maken
Nu we gaan de toepassing te bouwen.

### <a name="create-a-model"></a>Een model maken
Een *model* is een object dat de gegevens in uw toepassing vertegenwoordigt. Het enige model is voor de toepassing een taakobject een item in de takenlijst vertegenwoordigt. Taken hebben de volgende velden:

* PartitionKey
* RowKey
* naam (tekenreeks)
* categorie (tekenreeks)
* voltooid (Booleaanse waarde)

**PartitionKey** en **RowKey** als tabelsleutels worden gebruikt door de Tabelservice. Zie voor meer informatie [inzicht in het Tabelservice-gegevensmodel](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. In de **tasklist** directory, maak een nieuwe map met de naam **modellen**.
2. In de **modellen** directory, maak een nieuw bestand met de naam **task.js**. Dit bestand bevat het model voor de taken die zijn gemaakt door uw toepassing.
3. Aan het begin van de **task.js** bestand, voeg de volgende code om te verwijzen naar de vereiste bibliotheken:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Voeg de volgende code om te definiëren en exporteren van het taakobject. Dit object is verantwoordelijk voor het verbinden met de tabel.
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. Voeg de volgende code om te definiëren van aanvullende methoden voor het taakobject waardoor er interactie met gegevens die zijn opgeslagen in de tabel:
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. Sla op en sluit de **task.js** bestand.

### <a name="create-a-controller"></a>Maak een domeincontroller
Een *controller* HTTP-aanvragen worden verwerkt op en geeft u het HTML-antwoord.

1. In de **tasklist/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.
2. Voeg de volgende code toe aan het bestand **tasklist.js**. Dit wordt geladen met de azure- en async-modules die worden gebruikt door **tasklist.js**. Hiermee ook definieert u de **TaskList** functie die wordt doorgegeven een exemplaar van de **taak** object eerder:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Definieer een **TaskList** object.
   
        function TaskList(task) {
          this.task = task;
        }
4. Voeg de volgende methoden om te **TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a>App.js wijzigen
1. Van de **tasklist** directory, open de **app.js** bestand. Dit bestand is gemaakt door het uitvoeren van de **snelle** opdracht.
2. Toevoegen aan het begin van het bestand, het volgende om te laden van de azure-module, de naam van de tabel, partitiesleutel en de storage-referenties die worden gebruikt door het volgende voorbeeld:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf laadt de configuratiewaarden van beide omgevingsvariabelen of de **config.json** bestand, dat we later gaan maken.
   > 
   > 
3. In het bestand app.js, bladert u omlaag naar waar u de volgende regel zien:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Vervang de bovenstaande regels door de code hieronder wordt weergegeven. Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding met uw storage-account. Dit wordt doorgegeven aan de <strong>TaskList</strong>, die wordt gebruikt om communicatie met de tabel-service:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Sla de **app.js** bestand.

### <a name="modify-the-index-view"></a>Wijzig de weergave index
1. Open de **tasklist/views/index.jade** bestand in een teksteditor.
2. Vervang de volledige inhoud van het bestand door de volgende code. Hiermee definieert u een weergave die bestaande taken weergegeven en bevat een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. Opslaan en sluiten **index.jade** bestand.

### <a name="modify-the-global-layout"></a>De indeling van de globale wijzigen
De **layout.jade** bestand de **weergaven** map is een algemene sjabloon voor andere **.jade** bestanden. In deze stap wijzigt u het gebruik van [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u gemakkelijk voor het ontwerpen van een nice ogende web-app.

Downloaden en uitpakken van de bestanden voor [Twitter Bootstrap](http://getbootstrap.com/). Kopieer de **bootstrap.min.css** bestand van de Bootstrap **css** map in de **openbare/stylesheets** map van uw toepassing.

Van de **weergaven** map, open **layout.jade** en vervang de volledige inhoud door het volgende:

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Een configuratiebestand maken
Als u wilt uitvoeren van de app hebt we lokaal, Azure Storage-referenties in een configuratiebestand plaatsen. Maak een bestand met de naam **config.json* * met de volgende JSON:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Vervang **opslagaccountnaam** rekening met de naam van de opslag die u eerder hebt gemaakt en vervang **toegangssleutel voor opslag** met de primaire toegangssleutel voor uw opslagaccount. Bijvoorbeeld:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Sla dit bestand *hoger niveau van één map* dan de **tasklist** map als volgt:

    parent/
      |-- config.json
      |-- tasklist/

De reden hiervoor is om te voorkomen dat het configuratiebestand controleren in broncodebeheer, waar mogelijk komen openbare. Wanneer we de app in Azure implementeert, gebruiken we omgevingsvariabelen in plaats van een configuratiebestand.

## <a name="run-the-application-locally"></a>De toepassing lokaal uitvoeren
Testen van de toepassing op uw lokale computer, moet u de volgende stappen uitvoeren:

1. Vanaf de opdrachtregel, wijzig de mappen op de **tasklist** directory.
2. Gebruik de volgende opdracht om de toepassing lokaal te starten:
   
        npm start
3. Open een webbrowser en navigeer naar http://127.0.0.1:3000.
   
    Een webpagina die vergelijkbaar is met het volgende voorbeeld wordt weergegeven.
   
    ![Een webpagina een leeg tasklist weergeven][node-table-finished]
4. Voer een naam en categorie voor het maken van een nieuwe taakitem en klik op **Item toevoegen**. 
5. Voor een taak markeren als voltooid, Controleer **Complete** en klik op **taken bijwerken**.
   
    ![Een installatiekopie van het nieuwe item in de lijst met taken][node-table-list-items]

Zelfs als de toepassing lokaal wordt uitgevoerd, wordt het opslaan van gegevens in de Azure Table-service.

## <a name="deploy-your-application-to-azure"></a>Uw toepassing in Azure implementeren
De stappen in deze sectie de Azure-opdrachtregelprogramma's gebruiken om u te maken van een nieuwe web-app in App Service, en gebruik vervolgens Git om uw toepassing te implementeren. U moet een Azure-abonnement hebben om deze stappen uitvoert.

> [!NOTE]
> Deze stappen kunnen ook worden uitgevoerd met behulp van de [Azure Portal](https://portal.azure.com/). Zie [bouwen en implementeren van een Node.js-web-app in Azure App Service].
> 
> Als dit de eerste web-app die u hebt gemaakt, moet u de Azure Portal gebruiken om deze toepassing te implementeren.
> 
> 

Om te beginnen, installeert u de [Azure CLI] met de volgende opdracht vanaf de opdrachtregel:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Publicatie-instellingen importeren
In deze stap downloadt u een bestand met gegevens over uw abonnement.

1. Voer de volgende opdracht in:
   
        azure login
   
    Met deze opdracht wordt gestart van een browser en gaat u naar de downloadpagina. Als u wordt gevraagd, meldt u zich aan met het account dat is gekoppeld aan uw Azure-abonnement.
   
    <!-- ![The download page][download-publishing-settings] -->
   
    Downloaden van het bestand begint automatisch; Als dit niet het geval is, kunt u de koppeling aan het begin van de pagina handmatig het bestand te downloaden. Sla het bestand op en noteer het pad.
2. Voer de volgende opdracht om de instellingen te importeren:
   
        azure account import <path-to-file>
   
    Geef het pad en de naam van het gedownloade instellingenbestand publishing in de vorige stap.
3. Als de instellingen worden geïmporteerd, verwijdert u het instellingenbestand publiceren. Het is niet meer nodig en gevoelige informatie met betrekking tot uw Azure-abonnement bevat.

### <a name="create-an-app-service-web-app"></a>Een App Service-web-app maken
1. Vanaf de opdrachtregel, wijzig de mappen op de **tasklist** directory.
2. Gebruik de volgende opdracht voor het maken van een nieuwe web-app.
   
        azure site create --git
   
    U wordt gevraagd om de web-app-naam en locatie. Geef een unieke naam en selecteer dezelfde geografische locatie als uw Azure Storage-account.
   
    De `--git` parameter maakt u een Git-opslagplaats in Azure voor deze web-app. Deze ook een Git-opslagplaats in de huidige map initialiseert als er geen bestaat en voegt een [Git remote] met de naam 'azure', waarmee de toepassing publiceren in Azure. Ten slotte wordt het maken van een **web.config** bestand, dat instellingen die door Azure worden gebruikt om als host knooppunt toepassingen bevat. Als u weglaat de `--git` parameter, maar de map bevat een Git-opslagplaats, de opdracht wordt nog steeds maken 'azure' externe.
   
    Zodra deze opdracht is voltooid, ziet u uitvoer ziet er als volgt. Houd er rekening mee dat de regel die beginnen met **Website gemaakt op** de URL voor de web-app bevat.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > Als dit de eerste App Service web-app voor uw abonnement, wordt u gevraagd de Azure Portal gebruiken om te maken van de web-app. Zie voor meer informatie [bouwen en implementeren van een Node.js-web-app in Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>De omgevingsvariabelen instellen
In deze stap maakt toevoegt u omgevingsvariabelen aan de configuratie van uw web-app in Azure.
Voer de volgende gegevens vanaf de opdrachtregel:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Vervang  **<storage account name>**  rekening met de naam van de opslag die u eerder hebt gemaakt en vervang  **<storage access key>**  met de primaire toegangssleutel voor uw opslagaccount. (Gebruik dezelfde waarden als de config.json-bestand dat u eerder hebt gemaakt.)

U kunt ook omgevingsvariabelen instellen de [Azure Portal](https://portal.azure.com/):

1. De web-app-blade geopend door te klikken op **Bladeren** > **Web-Apps** > de naam van uw web-app.
2. Klik op de blade van uw web-app **alle instellingen** > **toepassingsinstellingen**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Schuif omlaag naar de **appinstellingen** sectie en de sleutel/waarde-paren toe te voegen.
   
     ![App-instellingen](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Klik op **OPSLAAN**.

### <a name="publish-the-application"></a>De toepassing publiceren
De codebestanden doorvoeren in Git en vervolgens push naar azure/master voor het publiceren van de app.

1. Stel de implementatiereferenties van uw.
   
        azure site deployment user set <name> <password>
2. Toevoegen en uw toepassingsbestanden worden doorgevoerd.
   
        git add .
        git commit -m "adding files"
3. Push het doorvoeren naar de App Service-web-app:
   
        git push azure master
   
    Gebruik **master** als de doel-vertakking. Aan het einde van de implementatie ziet u een instructie die vergelijkbaar is met het volgende voorbeeld:
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Zodra de push-bewerking is voltooid, bladert u naar de web-app-URL die eerder zijn geretourneerd door de `azure create site` opdracht om uw toepassing weer te geven.

## <a name="next-steps"></a>Volgende stappen
Hoewel de stappen in dit artikel wordt beschreven met behulp van de tabel-Service gegevens op te slaan, kunt u ook gebruiken [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Aanvullende bronnen
[Azure CLI]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[bouwen en implementeren van een Node.js-web-app in Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[knooppunt]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remote]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[knooppunt uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[asynchrone]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
