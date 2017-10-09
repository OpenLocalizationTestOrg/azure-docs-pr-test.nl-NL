---
title: aaaWeb app met table storage (Node.js) | Microsoft Docs
description: Een zelfstudie die is gebaseerd op Hallo van Web-App met snelle zelfstudie door Azure Storage-services toe te voegen en hello Azure-module.
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>Node.js-webtoepassing met opslag
## <a name="overview"></a>Overzicht
In deze zelfstudie wordt u uitbreiden Hallo toepassing gemaakt in de [Node.js-webtoepassing met een snelle] zelfstudie via Hallo Microsoft Azure-clientbibliotheken voor Node.js toowork met data management-services. Een web gebaseerde takenlijst toepassing dat u tooAzure kunt implementeren, gaat u uw toepassing toocreate uitbreiden. Hallo takenlijst kan een gebruiker taken ophalen, het toevoegen van nieuwe taken en taken te markeren als voltooid.

Hallo taakitems worden opgeslagen in Azure Storage. Azure Storage biedt niet-gestructureerde gegevensopslag die fouttolerante en maximaal beschikbaar is. Azure Storage bevat verschillende gegevensstructuren waarin u kunt opslaan en toegang tot gegevens en u van de opslagservices Hallo van Hallo API's die zijn opgenomen in hello Azure SDK voor Node.js of via de REST-API's gebruikmaken kunt. Zie voor meer informatie [opslaan en toegang tot gegevens in Azure].

Deze zelfstudie wordt ervan uitgegaan dat u Hallo hebt voltooid [Node.js-webtoepassing] en [Node.js snelle][Node.js-webtoepassing met een snelle] zelfstudies.

U leert:

* Hoe toowork met Jade sjabloon engine Hallo
* Hoe toowork met Azure Data Management-services

Een schermopname van de toepassing hello voltooid lager is dan:

![Hallo voltooid webpagina in internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Storage-referenties instelling in het bestand Web.Config
tooaccess Azure Storage, moet u toopass in de storage-referenties. toodo, gebruikmaken van web.config toepassingsinstellingen.
Deze instellingen worden doorgegeven als omgeving variabelen tooNode, die vervolgens worden gelezen door hello Azure SDK.

> [!NOTE]
> Storage-referenties worden alleen gebruikt wanneer de toepassing hello geïmplementeerde tooAzure. Wanneer in Hallo-emulator wordt uitgevoerd, wordt Hallo toepassing hello-opslagemulator gebruiken.
>
>

Uitvoeren van de volgende stappen tooretrieve hello opslagaccountreferenties Hallo en toohello web.config-instellingen toevoegen:

1. Als deze nog niet is geopend, start u hello Azure PowerShell vanuit Hallo **Start** menu door het uitbreiden van **alle programma's, Azure**, met de rechtermuisknop op **Azure PowerShell**, en selecteer vervolgens  **Als Administrator uitvoeren**.
2. Mappen toohello map wijzigen met uw toepassing. Bijvoorbeeld: C:\\knooppunt\\tasklist\\WebRole1.
3. Voer vanuit hello Azure Powershell-venster Hallo cmdlet tooretrieve Hallo-opslag-accountgegevens te volgen:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Hiermee haalt Hallo lijst van storage-accounts en sleutels die zijn gekoppeld aan de gehoste service-account.

   > [!NOTE]
   > Omdat hello Azure SDK een opslagaccount maakt wanneer u een service implementeert, moet al een opslagaccount van het implementeren van uw toepassing in de vorige handleidingen Hallo bestaan.
   >
   >
4. Open Hallo **ServiceDefinition.csdef** bestand met Hallo omgevingsinstellingen die worden gebruikt wanneer de toepassing hello geïmplementeerde tooAzure:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. INSERT Hallo volgende blokkeren onder **omgeving** element, vervangen door {OPSLAGACCOUNT} en {TOEGANGSSLEUTEL voor opslag} met Hallo-accountnaam en de primaire sleutel Hallo voor Hallo storage-account wilt van toouse voor de implementatie:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Hallo web.cloud.config bestandsinhoud](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. Hallo-bestand opslaan en sluit Kladblok.

### <a name="install-additional-modules"></a>Aanvullende modules installeren
1. Gebruik Hallo na de opdracht tooinstall Hallo [azure], [knooppunt-uuid] [nconf] en [asynchrone] modules lokaal alsmede toosave een vermelding voor hen toohello **package.json** bestand:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  Hallo-uitvoer van deze opdracht moet vergelijkbaar toohello volgende weergegeven:

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a>Hallo tabel-service in een knooppunttoepassing gebruiken
In deze sectie wordt u Hallo eenvoudige toepassing gemaakt door Hallo uitbreiden **snelle** door toe te voegen opdracht een **task.js** bestand waarin Hallo-model voor uw taken. U wordt ook wijzigen Hallo bestaande **app.js** en maak een nieuwe **tasklist.js** bestand dat gebruikmaakt van Hallo-model.

### <a name="create-hello-model"></a>Hallo-model maken
1. In Hallo **WebRole1** directory, maak een nieuwe map met de naam **modellen**.
2. In Hallo **modellen** directory, maak een nieuw bestand met de naam **task.js**. Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door uw toepassing.
3. Aan begin Hallo Hallo **task.js** bestand, het toevoegen van Hallo code tooreference vereist bibliotheken te volgen:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Vervolgens moet u code toodefine toevoegen en Hallo taakobject exporteren. Dit object is verantwoordelijk voor het verbinden van toohello tabel.

    ```nodejs
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
    ```

5. Vervolgens voegt u Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in de tabel Hallo:

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. Opslaan en sluiten Hallo **task.js** bestand.

### <a name="create-hello-controller"></a>Hallo controller maken
1. In Hallo **WebRole1/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.
2. Hallo code te volgen toevoegen**tasklist.js**. Dit wordt geladen hello azure en async-modules die worden gebruikt door **tasklist.js**. Hiermee definieert u ook Hallo **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** object eerder:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Doorgaan met het toevoegen van toohello **tasklist.js** bestand door toe te voegen Hallo methoden te**showTasks**, **addTask**, en **completeTasks**:

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. Hallo opslaan **tasklist.js** bestand.

### <a name="modify-appjs"></a>App.js wijzigen
1. In Hallo **WebRole1** directory, open Hallo **app.js** bestand in een teksteditor.
2. Aan het begin van de Hallo van Hallo-bestand, Hallo na tooload hello azure module toevoegen en instellen van naam en partitie-sleutel van tabel Hallo:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. In het bestand app.js hello, schuif naar beneden toowhere u ziet Hallo volgende regel:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Hallo boven regels vervangen door Hallo-code hieronder wordt weergegeven. Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding tooyour storage-account. Dit wordt doorgegeven toohello <strong>TaskList</strong>, welke gebruiken deze toocommunicate Hello tabelservice:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Hallo opslaan **app.js** bestand.

### <a name="modify-hello-index-view"></a>Hallo index weergave wijzigen
1. Wijzig de mappen toohello **weergaven** directory en open Hallo **index.jade** bestand in een teksteditor.
2. Vervang de inhoud Hallo Hallo **index.jade** bestand met de Hallo-code hieronder. Hiermee definieert u Hallo weergave voor het weergeven van bestaande taken, evenals een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.

    ```
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
          if tasks != []
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
    ```

3. Opslaan en sluiten **index.jade** bestand.

### <a name="modify-hello-global-layout"></a>Hallo globale indeling wijzigen
Hallo **layout.jade** bestand in Hallo **weergaven** directory wordt gebruikt als een algemeen sjabloon voor andere **.jade** bestanden. In deze stap wijzigt u deze toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign een aantrekkelijk ogende website.

1. Downloaden en uitpakken van bestanden voor Hallo [Twitter Bootstrap](http://getbootstrap.com/). Kopiëren Hallo **bootstrap.min.css** bestand van Hallo **bootstrap\\verdeling\\css** map toohello **openbare\\stylesheets** map van uw toepassing tasklist.
2. Van Hallo **weergaven** map, open Hallo **layout.jade** in uw editor en vervang Hallo tekstinhoud door Hallo volgende:

    DOCTYPE HTML-html head titel = Titelkoppeling (rel = 'stylesheet', href='/stylesheets/bootstrap.min.css') koppeling (rel = 'stylesheet', href='/stylesheets/style.css') body.app nav.navbar.navbar-standaard div.navbar-header a.navbar-brand(href='/') inhoud van mijn taken blokkeren

3. Hallo opslaan **layout.jade** bestand.

### <a name="running-hello-application-in-hello-emulator"></a>Hallo toepassing uitgevoerd in de Emulator Hallo
Gebruik Hallo volgende opdracht toostart Hallo toepassing in Hallo-emulator.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

Hallo-browser wordt geopend en wordt na pagina Hallo weergegeven:

![Een web-wisselbare getiteld mijn takenlijst met een tabel met taken en velden tooadd een nieuwe taak.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

Hallo formulier tooadd items gebruiken of verwijderen van bestaande items door deze te markeren als voltooid.

## <a name="publishing-hello-application-tooazure"></a>Publishing Hallo toepassing tooAzure
Aanroepen in de Windows PowerShell-venster Hallo Hallo cmdlet tooredeploy na uw tooAzure gehoste service.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Vervang **myuniquename** met een unieke naam voor deze toepassing. Vervang **datacentername** met Hallo-naam van een Azure-Datacenter, zoals **VS-West**.

Nadat het Hallo-implementatie is voltooid, ziet u een reactie vergelijkbaar toohello volgende:

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

Als voorheen omdat u Hallo opgegeven **-starten** optie Hallo browser wordt geopend en wordt uw toepassing in Azure wordt uitgevoerd als het publiceren is voltooid.

![Een browservenster Hallo mijn takenlijst pagina weergeven. Hallo URL geeft Hallo pagina nu wordt gehost op Azure.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Stoppen en verwijderen van uw toepassing
Na implementatie van uw toepassing, kunt u toodisable zodat u kunt voorkomen kosten of bouwen en implementeren van andere toepassingen binnen Hallo gratis proefabonnement periode.

Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht.
Er wordt servertijd verbruikt zodra uw toepassing is geïmplementeerd, zelfs als de exemplaren niet worden uitgevoerd en met de status Hallo gestopt.

Hallo volgende stappen ziet u hoe toostop en verwijderen van uw toepassing.

1. In Hallo Windows PowerShell-venster stopt Hallo service-implementatie gemaakt in de vorige sectie Hallo Hello volgende cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Hallo-service wordt gestopt, kan dit enkele minuten duren. Wanneer het Hallo-service wordt gestopt, krijgt u een bericht weergegeven dat aangeeft dat deze is gestopt.

2. toodelete hello service aanroep Hallo volgende cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-service.

   Verwijderen van Hallo-service kan enkele minuten duren. U ontvangt een bericht weergegeven dat aangeeft dat het Hallo-service is verwijderd nadat het Hallo-service is verwijderd.

[Node.js-webtoepassing met een snelle]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[opslaan en toegang tot gegevens in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js-webtoepassing]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


