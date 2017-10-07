---
title: aaaNode.js web-app met behulp van hello Azure Table-Service
description: Deze zelfstudie leert u hoe toouse hello Azure Table service toostore gegevens van een Node.js-toepassing die wordt gehost in Azure App Service Web Apps.
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Node.js web-app met behulp van hello Azure Table-Service
## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe de tabelservice toouse geleverd door Azure Data Management toostore en toegang tot gegevens uit een [knooppunt] toepassing wordt gehost [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps. Deze zelfstudie wordt ervan uitgegaan dat u hebt enige ervaring met knooppunt en [Git].

U leert:

* Hoe toouse npm (Pakketbeheer knooppunt) tooinstall Hallo knooppunt modules
* Hoe toowork met hello Azure Table-service
* Hoe toouse hello Azure CLI toocreate een web-app.

Door deze zelfstudie te volgen, bouwt u een eenvoudige web gebaseerde 'takenlijst'-toepassing die u kunt maken, ophalen en uitvoeren van taken. Hallo-taken worden opgeslagen in Hallo tabel-service.

Dit is de toepassing hello voltooid:

![Een webpagina een leeg tasklist weergeven][node-table-finished]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat er Hallo volgende zijn geïnstalleerd voordat Hallo-instructies in dit artikel:

* [knooppunt] versie 0.10.24 of hoger
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Een opslagaccount maken
Een Azure-opslagaccount maken. Hallo-app gebruikt deze account toostore Hallo-taakitems.

1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).
2. Klik op Hallo **nieuw** pictogram op Hallo onder, links van de Hallo-portal, klikt u op **gegevens en opslag** > **opslag**. Hallo storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.
   
      ![Knop Nieuw](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Wanneer Hallo storage-account is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en blade Hallo van het opslagaccount is geopend dat deze deel uitmaakt van de nieuwe resource toohello tooshow groep die u hebt gemaakt.
3. Klik op Hallo van het opslagaccount blade **instellingen** > **sleutels**. Hallo primaire sleutel toohello Klembord kopiëren.
   
    ![Toegangstoets][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Modules installeren en steigers genereren
In deze sectie wordt u een nieuw knooppunttoepassing maken en npm tooadd module pakketten. Voor deze toepassing gaat u Hallo [Express] en [Azure] modules. Hallo Express-module biedt een framework Model-View-Controller voor knooppunt, tijdens het Hallo Azure modules connectivity toohello tabel-service biedt.

### <a name="install-express-and-generate-scaffolding"></a>Express installeren en steigers genereren
1. Maak een nieuwe map met de naam vanaf de opdrachtregel Hallo **tasklist** en switch toothat directory.  
2. Voer Hallo opdracht tooinstall Hallo Express module te volgen.
   
        npm install express-generator@4.2.0 -g
   
    Afhankelijk van het Hallo-besturingssysteem moet u tooput 'sudo ' uitgebreid voor Hallo-opdracht:
   
        sudo npm install express-generator@4.2.0 -g
   
    Hallo-uitvoer wordt weergegeven vergelijkbaar toohello voorbeeld te volgen:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Hallo '-g' parameter Hallo module globaal installeert. Op die manier kunnen we gebruiken **snelle** toogenerate web app steigers zonder tootype in extra padinformatie.
   > 
   > 
3. toocreate hello steigers voor toepassing hello, Voer Hallo **snelle** opdracht:
   
        express
   
    Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    U hebt nu verschillende nieuwe mappen en bestanden in Hallo **tasklist** directory.

### <a name="install-additional-modules"></a>Aanvullende modules installeren
Een van de Hallo bestanden die **snelle** maakt is **package.json**. Dit bestand bevat een lijst met afhankelijkheden van de module. Later, wanneer u Hallo toepassing tooApp Service Web Apps implementeert, bepaalt dit bestand welke modules moeten toobe geïnstalleerd op Azure.

Van Hallo opdrachtregelprogramma, Voer Hallo na de opdracht tooinstall Hallo modules dat wordt beschreven in Hallo **package.json** bestand. Mogelijk moet u toouse 'sudo ' uitgebreid.

    npm install

Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Geef vervolgens de volgende opdracht tooinstall Hallo Hallo [azure], [knooppunt uuid], [nconf] en [asynchrone] modules:

    npm install azure-storage node-uuid async nconf --save

Hallo **--opslaan** vlag voegt vermeldingen voor deze modules toohello **package.json** bestand.

Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Hallo-toepassing maken
Nu we klaar toobuild Hallo-toepassing.

### <a name="create-a-model"></a>Een model maken
Een *model* is een object dat de gegevens in uw toepassing hello vertegenwoordigt. Hallo alleen model is voor de toepassing hello, een taakobject een item in de takenlijst Hallo vertegenwoordigt. Taken een Hallo velden te volgen:

* PartitionKey
* RowKey
* naam (tekenreeks)
* categorie (tekenreeks)
* voltooid (Booleaanse waarde)

**PartitionKey** en **RowKey** worden gebruikt door Hallo Tabelservice als tabelsleutels. Zie voor meer informatie [Understanding Hallo Tabelservice-gegevensmodel](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. In Hallo **tasklist** directory, maak een nieuwe map met de naam **modellen**.
2. In Hallo **modellen** directory, maak een nieuw bestand met de naam **task.js**. Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door uw toepassing.
3. Aan begin Hallo Hallo **task.js** bestand, het toevoegen van Hallo code tooreference vereist bibliotheken te volgen:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Hallo volgende toodefine code en exporteren van het taakobject Hallo toevoegen. Dit object is verantwoordelijk voor het verbinden van toohello tabel.
   
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
5. Toevoegen Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in de tabel Hallo:
   
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
            // use entityGenerator tooset types
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
6. Opslaan en sluiten Hallo **task.js** bestand.

### <a name="create-a-controller"></a>Maak een domeincontroller
Een *controller* HTTP-aanvragen worden verwerkt en rendert Hallo HTML-antwoord.

1. In Hallo **tasklist/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.
2. Hallo code te volgen toevoegen**tasklist.js**. Dit wordt geladen hello azure en async-modules die worden gebruikt door **tasklist.js**. Hiermee definieert u ook Hallo **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** object eerder:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Definieer een **TaskList** object.
   
        function TaskList(task) {
          this.task = task;
        }
4. Toevoegen van de volgende methoden te Hallo**TaskList**:
   
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
1. Van Hallo **tasklist** directory, open Hallo **app.js** bestand. Dit bestand is gemaakt door het uitvoeren van Hallo **snelle** opdracht.
2. Toevoegen aan het begin van de Hallo van Hallo-bestand, Hallo tooload hello azure module, set Hallo tabelnaam partitiesleutel en set Hallo opslag referenties op die in dit voorbeeld te volgen:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf laadt Hallo configuratiewaarden van omgevingsvariabelen of Hallo **config.json** bestand, dat we later gaan maken.
   > 
   > 
3. In het bestand app.js hello, schuif naar beneden toowhere u ziet Hallo volgende regel:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Hallo boven regels vervangen door Hallo-code hieronder wordt weergegeven. Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding tooyour storage-account. Dit wordt doorgegeven toohello <strong>TaskList</strong>, welke gebruiken deze toocommunicate Hello tabelservice:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Hallo opslaan **app.js** bestand.

### <a name="modify-hello-index-view"></a>Hallo index weergave wijzigen
1. Open Hallo **tasklist/views/index.jade** bestand in een teksteditor.
2. Vervang de volledige inhoud van de Hallo van Hallo-bestand met de volgende code Hallo. Hiermee definieert u een weergave die bestaande taken weergegeven en bevat een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.
   
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

### <a name="modify-hello-global-layout"></a>Hallo globale indeling wijzigen
Hallo **layout.jade** bestand in Hallo **weergaven** map is een algemene sjabloon voor andere **.jade** bestanden. In deze stap wijzigt u deze toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign nice ogende web-app.

Downloaden en uitpakken van bestanden voor Hallo [Twitter Bootstrap](http://getbootstrap.com/). Kopiëren Hallo **bootstrap.min.css** bestand van Hallo Bootstrap **css** map in Hallo **openbare/stylesheets** map van uw toepassing.

Van Hallo **weergaven** map, open **layout.jade** en vervang de volledige inhoud Hallo door Hallo volgende:

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
Hallo-app lokaal toorun we je Azure Storage-referenties in een configuratiebestand plaatsen. Maak een bestand met de naam **config.json* * Hello JSON te volgen:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Vervang **opslagaccountnaam** rekening met de naam van opslag Hallo Hallo u eerder hebt gemaakt en vervang **toegangssleutel voor opslag** met Hallo primaire toegangssleutel voor uw opslagaccount. Bijvoorbeeld:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Sla dit bestand *hoger niveau van één map* dan Hallo **tasklist** map als volgt:

    parent/
      |-- config.json
      |-- tasklist/

Hallo reden om dit te doen is tooavoid Hallo-configuratiebestand controleren in broncodebeheer, waar mogelijk komen openbare. Wanneer we Hallo app tooAzure implementeert, gebruiken we omgevingsvariabelen in plaats van een configuratiebestand.

## <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
tootest hello toepassing op uw lokale machine uitvoeren Hallo stappen te volgen:

1. Wijzig vanaf de opdrachtregel Hallo, mappen toohello **tasklist** directory.
2. Gebruik Hallo opdracht toolaunch Hallo toepassing lokaal te volgen:
   
        npm start
3. Open een webbrowser en navigeer toohttp://127.0.0.1:3000.
   
    Een webpagina vergelijkbare toohello volgende voorbeeld wordt weergegeven.
   
    ![Een webpagina een leeg tasklist weergeven][node-table-finished]
4. een nieuwe taakitem toocreate Voer een naam en categorie en klik op **Item toevoegen**. 
5. een taak als voltooid, Controleer toomark **Complete** en klik op **taken bijwerken**.
   
    ![Een afbeelding van Hallo nieuw item in de lijst Hallo van taken][node-table-list-items]

Hoewel Hallo toepassing lokaal wordt uitgevoerd, wordt het opslaan van gegevens van Hallo in hello Azure Table-service.

## <a name="deploy-your-application-tooazure"></a>Uw toepassing tooAzure implementeren
Hallo stappen in deze sectie hello Azure-opdrachtregelprogramma's toocreate een nieuwe web-app in App Service gebruiken en gebruik vervolgens Git toodeploy uw toepassing. tooperform deze stappen hebt u een Azure-abonnement.

> [!NOTE]
> Deze stappen kunnen ook worden uitgevoerd met behulp van Hallo [Azure Portal](https://portal.azure.com/). Zie [bouwen en implementeren van een Node.js-web-app in Azure App Service].
> 
> Als dit Hallo eerste web-app die u hebt gemaakt, moet u deze toepassing hello Azure Portal toodeploy gebruiken.
> 
> 

tooget gestart, installeer Hallo [Azure CLI] hiertoe de volgende opdracht uit vanaf de opdrachtregel Hallo Hallo:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Publicatie-instellingen importeren
In deze stap downloadt u een bestand met gegevens over uw abonnement.

1. Voer Hallo volgende opdracht:
   
        azure login
   
    Deze opdracht wordt gestart van een browser en toohello downloadpagina navigeert. Als u wordt gevraagd, kunt u aanmelden met Hallo-account die is gekoppeld aan uw Azure-abonnement.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    Hallo-bestand downloaden begint automatisch; Als dit niet het geval is, kunt u op Hallo begin van Hallo toomanually downloaden Hallo wisselbestand Hallo-koppeling. Hallo bestands- en Opmerking Hallo bestandspad opslaan.
2. Voer Hallo opdracht tooimport Hallo-instellingen te volgen:
   
        azure account import <path-to-file>
   
    Hallo pad en de naam van de door u gedownloade instellingenbestand publiceren in de vorige stap Hallo Hallo opgeven.
3. Nadat het Hallo-instellingen worden geïmporteerd, verwijdert u Hallo bestand publicatie-instellingen. Het is niet meer nodig en gevoelige informatie met betrekking tot uw Azure-abonnement bevat.

### <a name="create-an-app-service-web-app"></a>Een App Service-web-app maken
1. Wijzig vanaf de opdrachtregel Hallo, mappen toohello **tasklist** directory.
2. Gebruik Hallo opdracht toocreate een nieuwe web-app te volgen.
   
        azure site create --git
   
    U wordt gevraagd voor Hallo web-app-naam en locatie. Geef een unieke naam en selecteer Hallo dezelfde geografische locatie bevinden als uw Azure Storage-account.
   
    Hallo `--git` parameter maakt u een Git-opslagplaats in Azure voor deze web-app. Deze ook een Git-opslagplaats in de huidige map Hallo initialiseert als er geen bestaat en voegt een [Git remote] met de naam 'azure', die de gebruikte toopublish Hallo toepassing tooAzure is. Ten slotte wordt het maken van een **web.config** bestand, dat instellingen die worden gebruikt door Azure toohost knooppunt toepassingen bevat. Als u Hallo weglaat `--git` parameter, maar Hallo directory bevat een Git-opslagplaats, Hallo opdracht maakt nog steeds 'azure' hello afstand.
   
    Zodra deze opdracht is voltooid, ziet u uitvoer vergelijkbare toohello volgende. Houd er rekening mee dat Hallo regels die beginnen met **Website gemaakt op** Hallo-URL voor Hallo web-app bevat.
   
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
   > Als dit Hallo eerste App Service web-app voor uw abonnement, kunt u zich gebruiksaanwijzing toouse hello Azure Portal toocreate Hallo web-app. Zie voor meer informatie [bouwen en implementeren van een Node.js-web-app in Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>De omgevingsvariabelen instellen
In deze stap voegt u configuratie voor de omgeving variabelen tooyour web-app in Azure.
Voer vanaf de opdrachtregel Hallo Hallo volgende in:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Vervang  **<storage account name>**  rekening met de naam van opslag Hallo Hallo u eerder hebt gemaakt en vervang  **<storage access key>**  met Hallo primaire toegangssleutel voor uw opslagaccount. (Gebruik Hallo dezelfde waarden als Hallo config.json-bestand dat u eerder hebt gemaakt.)

U kunt ook omgevingsvariabelen instellen in Hallo [Azure Portal](https://portal.azure.com/):

1. Hallo van web-app-blade geopend door te klikken op **Bladeren** > **Web-Apps** > de naam van uw web-app.
2. Klik op de blade van uw web-app **alle instellingen** > **toepassingsinstellingen**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Schuif omlaag toohello **appinstellingen** sectie en Hallo sleutel/waarde-paren toe te voegen.
   
     ![App-instellingen](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Klik op **OPSLAAN**.

### <a name="publish-hello-application"></a>Hallo toepassing publiceren
toopublish hello app Hallo code bestanden tooGit doorvoeren en vervolgens push tooazure/master.

1. Stel de implementatiereferenties van uw.
   
        azure site deployment user set <name> <password>
2. Toevoegen en uw toepassingsbestanden worden doorgevoerd.
   
        git add .
        git commit -m "adding files"
3. Push Hallo doorvoeren toohello App Service-web-app:
   
        git push azure master
   
    Gebruik **master** als Hallo doel vertakking. Aan het einde van de Hallo Hallo-implementatie ziet u een instructie vergelijkbare toohello voorbeeld te volgen:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Zodra Hallo push-bewerking is voltooid, bladeren toohello web app-URL die eerder geretourneerd door Hallo `azure create site` opdracht tooview uw toepassing.

## <a name="next-steps"></a>Volgende stappen
Tijdens het Hallo-stappen in dit artikel wordt beschreven met behulp van Hallo Tabelservice toostore gegevens, kunt u ook gebruiken [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Aanvullende bronnen
[Azure CLI]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
