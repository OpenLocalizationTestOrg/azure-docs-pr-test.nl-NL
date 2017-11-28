---
title: aaaWeb app met table storage (Node.js) | Microsoft Docs
description: Een zelfstudie die is gebaseerd op Hallo van Web-App met snelle zelfstudie door Azure Storage-services toe te voegen en hello Azure-module.
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="bc8c5-103">Node.js-webtoepassing met opslag</span><span class="sxs-lookup"><span data-stu-id="bc8c5-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="bc8c5-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bc8c5-104">Overview</span></span>
<span data-ttu-id="bc8c5-105">In deze zelfstudie Hallo toepassing die u hebt gemaakt in de [Node.js-webtoepassing met een snelle] zelfstudie wordt uitgebreid met Hallo Microsoft Azure-clientbibliotheken voor Node.js toowork met data management-services.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="bc8c5-106">U kunt uw toepassing uitbreiden door het maken van een web gebaseerde takenlijst toepassing dat u tooAzure kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="bc8c5-107">Hallo takenlijst kan een gebruiker taken ophalen, het toevoegen van nieuwe taken en taken te markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="bc8c5-108">Hallo taakitems worden opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="bc8c5-109">Azure Storage biedt niet-gestructureerde gegevensopslag die fouttolerante en maximaal beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="bc8c5-110">Azure Storage bevat verschillende gegevensstructuren waar u kunt opslaan en toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="bc8c5-111">U kunt de opslagservices Hallo van Hallo API's die zijn opgenomen in hello Azure SDK voor Node.js of via de REST-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="bc8c5-112">Zie voor meer informatie [opslaan en toegang tot gegevens in Azure].</span><span class="sxs-lookup"><span data-stu-id="bc8c5-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="bc8c5-113">Deze zelfstudie wordt ervan uitgegaan dat u Hallo hebt voltooid [Node.js-webtoepassing] en [Node.js snelle][Node.js-webtoepassing met een snelle] zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="bc8c5-114">Hallo volgende informatie bevat:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-114">It contains hello following information:</span></span>

* <span data-ttu-id="bc8c5-115">Hoe toowork met Jade sjabloon engine Hallo</span><span class="sxs-lookup"><span data-stu-id="bc8c5-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="bc8c5-116">Hoe toowork met Azure Data Management-services</span><span class="sxs-lookup"><span data-stu-id="bc8c5-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="bc8c5-117">Hallo volgende schermafbeelding ziet u de toepassing hello voltooid:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-117">hello following screenshot shows hello completed application:</span></span>

![Hallo voltooid webpagina in internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="bc8c5-119">Storage-referenties instelling in het bestand Web.Config</span><span class="sxs-lookup"><span data-stu-id="bc8c5-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="bc8c5-120">U moet doorgeven in opslag referenties tooaccess Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="bc8c5-121">Dit wordt gedaan door het gebruik van Hallo web.config toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="bc8c5-122">Hallo web.config-instellingen worden doorgegeven als omgeving variabelen tooNode, die vervolgens worden gelezen door hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="bc8c5-123">Storage-referenties worden alleen gebruikt wanneer de toepassing hello geïmplementeerde tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="bc8c5-124">Wanneer in Hallo-emulator wordt uitgevoerd, gebruikt Hallo toepassing hello opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="bc8c5-125">Uitvoeren van de volgende stappen tooretrieve hello opslagaccountreferenties Hallo en toohello web.config-instellingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="bc8c5-126">Als deze nog niet is geopend, start u hello Azure PowerShell vanuit Hallo **Start** menu door het uitbreiden van **alle programma's, Azure**, met de rechtermuisknop op **Azure PowerShell**, en selecteer vervolgens  **Als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="bc8c5-127">Mappen toohello map wijzigen met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="bc8c5-128">Bijvoorbeeld: C:\\knooppunt\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="bc8c5-129">Voer vanuit hello Azure Powershell-venster, Hallo cmdlet tooretrieve Hallo-opslag-accountgegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="bc8c5-130">Hallo haalt voorgaande cmdlet Hallo lijst met storage-accounts en sleutels die zijn gekoppeld aan de gehoste service.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc8c5-131">Omdat hello Azure SDK een opslagaccount maakt wanneer u een service implementeert, moet al een opslagaccount van het implementeren van uw toepassing in de vorige handleidingen Hallo bestaan.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="bc8c5-132">Open Hallo **ServiceDefinition.csdef** bestand met Hallo omgevingsinstellingen die worden gebruikt wanneer de toepassing hello geïmplementeerde tooAzure:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="bc8c5-133">INSERT Hallo volgende blokkeren onder **omgeving** element, vervangen door {OPSLAGACCOUNT} en {TOEGANGSSLEUTEL voor opslag} met Hallo-accountnaam en de primaire sleutel Hallo voor Hallo storage-account wilt van toouse voor de implementatie:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Hallo web.cloud.config bestandsinhoud](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="bc8c5-135">Hallo-bestand opslaan en sluit Kladblok.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="bc8c5-136">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="bc8c5-136">Install additional modules</span></span>
1. <span data-ttu-id="bc8c5-137">Gebruik Hallo na de opdracht tooinstall Hallo [azure], [knooppunt-uuid] [nconf] en [asynchrone] modules lokaal alsmede toosave een vermelding voor hen toohello **package.json** bestand:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="bc8c5-138">Hallo-uitvoer van deze opdracht moet vergelijkbaar toohello volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-138">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="bc8c5-139">Hallo tabel-service in een knooppunttoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="bc8c5-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="bc8c5-140">In deze sectie Hallo basistoepassing gemaakt door Hallo **snelle** opdracht wordt uitgebreid door toe te voegen een **task.js** -bestand met de Hallo-model voor uw taken.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="bc8c5-141">Wijzig Hallo bestaande **app.js** -bestand en maak een nieuwe **tasklist.js** bestand dat gebruikmaakt van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="bc8c5-142">Hallo-model maken</span><span class="sxs-lookup"><span data-stu-id="bc8c5-142">Create hello model</span></span>
1. <span data-ttu-id="bc8c5-143">In Hallo **WebRole1** directory, maak een nieuwe map met de naam **modellen**.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="bc8c5-144">In Hallo **modellen** directory, maak een nieuw bestand met de naam **task.js**.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="bc8c5-145">Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="bc8c5-146">Aan begin Hallo Hallo **task.js** bestand, het toevoegen van Hallo code tooreference vereist bibliotheken te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="bc8c5-147">Vervolgens code toodefine toevoegen en Hallo taakobject exporteren.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="bc8c5-148">Hallo-taakobject is verantwoordelijk voor het verbinden van toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-148">hello Task object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="bc8c5-149">Vervolgens voegt u Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in de tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="bc8c5-150">Opslaan en sluiten Hallo **task.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="bc8c5-151">Hallo controller maken</span><span class="sxs-lookup"><span data-stu-id="bc8c5-151">Create hello controller</span></span>
1. <span data-ttu-id="bc8c5-152">In Hallo **WebRole1/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="bc8c5-153">Hallo code te volgen toevoegen**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="bc8c5-154">Deze code wordt geladen hello azure- en async-modules, die worden gebruikt door **tasklist.js** en definieert Hallo **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** we object eerder hebt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="bc8c5-155">Doorgaan met het toevoegen van toohello **tasklist.js** bestand door toe te voegen Hallo methoden te**showTasks**, **addTask**, en **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="bc8c5-156">Hallo opslaan **tasklist.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="bc8c5-157">App.js wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc8c5-157">Modify app.js</span></span>
1. <span data-ttu-id="bc8c5-158">In Hallo **WebRole1** directory, open Hallo **app.js** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="bc8c5-159">Aan het begin van de Hallo van Hallo-bestand, Hallo na tooload hello azure module toevoegen en instellen van naam en partitie-sleutel van tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="bc8c5-160">In het bestand app.js hello, schuif naar beneden toowhere u ziet Hallo volgende regel:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="bc8c5-161">Hallo vóór regels met de volgende code Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="bc8c5-162">Deze code initialiseert een exemplaar van <strong>taak</strong> met een verbinding tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="bc8c5-163">Hallo <strong>taak</strong> toohello wordt doorgegeven <strong>TaskList</strong>, waarin deze toocommunicate met Hallo tabel-service:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="bc8c5-164">Hallo opslaan **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="bc8c5-165">Hallo index weergave wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc8c5-165">Modify hello index view</span></span>
1. <span data-ttu-id="bc8c5-166">Wijzig de mappen toohello **weergaven** directory en open Hallo **index.jade** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="bc8c5-167">Vervang de inhoud Hallo Hallo **index.jade** bestand met de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="bc8c5-168">Deze code definieert Hallo weergave voor het weergeven van bestaande taken en definieert een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="bc8c5-169">Opslaan en sluiten **index.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="bc8c5-170">Hallo globale indeling wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc8c5-170">Modify hello global layout</span></span>
<span data-ttu-id="bc8c5-171">Hallo **layout.jade** bestand in Hallo **weergaven** directory wordt gebruikt als een algemeen sjabloon voor andere **.jade** bestanden.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="bc8c5-172">In deze stap wijzigen Hallo **layout.jade** bestand toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign een aantrekkelijk ogende website.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="bc8c5-173">Downloaden en uitpakken van bestanden voor Hallo [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="bc8c5-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="bc8c5-174">Kopiëren Hallo **bootstrap.min.css** bestand van Hallo **bootstrap\\verdeling\\css** map toohello **openbare\\stylesheets** map van uw toepassing tasklist.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="bc8c5-175">Van Hallo **weergaven** map, open Hallo **layout.jade** -bestand in een teksteditor en vervang Hallo inhoud door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="bc8c5-176">DOCTYPE HTML-html head titel = Titelkoppeling (rel = 'stylesheet', href='/stylesheets/bootstrap.min.css') koppeling (rel = 'stylesheet', href='/stylesheets/style.css') body.app nav.navbar.navbar-standaard div.navbar-header a.navbar-brand(href='/') inhoud van mijn taken blokkeren</span><span class="sxs-lookup"><span data-stu-id="bc8c5-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="bc8c5-177">Hallo opslaan **layout.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="bc8c5-178">Hallo toepassing uitgevoerd in de Emulator Hallo</span><span class="sxs-lookup"><span data-stu-id="bc8c5-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="bc8c5-179">Gebruik Hallo volgende opdracht toostart Hallo toepassing in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="bc8c5-180">Hallo-browser wordt geopend en Hallo na pagina wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-180">hello browser opens and displays hello following page:</span></span>

![Een web-wisselbare getiteld mijn takenlijst met een tabel met taken en velden tooadd een nieuwe taak.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="bc8c5-182">Hallo formulier tooadd items gebruiken of verwijderen van bestaande items door deze te markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="bc8c5-183">Publishing Hallo toepassing tooAzure</span><span class="sxs-lookup"><span data-stu-id="bc8c5-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="bc8c5-184">Aanroepen in de Windows PowerShell-venster Hallo Hallo cmdlet tooredeploy na uw tooAzure gehoste service.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="bc8c5-185">Vervang **myuniquename** met een unieke naam voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="bc8c5-186">Vervang **datacentername** met Hallo-naam van een Azure-Datacenter, zoals **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="bc8c5-187">Nadat het Hallo-implementatie is voltooid, ziet u een reactie vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="bc8c5-188">Door op te geven Hallo **-starten** optie in de vorige cmdlet hello, Hallo browser wordt geopend en wordt uw toepassing in Azure wordt uitgevoerd als het publiceren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Een browservenster Hallo mijn takenlijst pagina weergeven.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="bc8c5-191">Stoppen en verwijderen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="bc8c5-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="bc8c5-192">Na implementatie van uw toepassing, kunt u toodisable zodat u kunt voorkomen kosten of bouwen en implementeren van andere toepassingen binnen Hallo gratis proefabonnement periode.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="bc8c5-193">Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="bc8c5-194">Er wordt servertijd verbruikt zodra uw toepassing is geïmplementeerd, zelfs als de exemplaren niet worden uitgevoerd en met de status Hallo gestopt.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="bc8c5-195">Hallo volgende stappen ziet u hoe toostop en verwijderen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="bc8c5-196">In Hallo Windows PowerShell-venster stopt Hallo service-implementatie gemaakt in de vorige sectie Hallo Hello volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="bc8c5-197">Hallo-service wordt gestopt, kan dit enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="bc8c5-198">Wanneer het Hallo-service wordt gestopt, krijgt u een bericht weergegeven dat aangeeft dat deze is gestopt.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="bc8c5-199">toodelete hello service aanroep Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bc8c5-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="bc8c5-200">Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="bc8c5-201">Verwijderen van Hallo-service kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="bc8c5-202">Nadat het Hallo-service is verwijderd, ontvangt u een bericht weergegeven dat aangeeft dat het Hallo-service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="bc8c5-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[Node.js-webtoepassing met een snelle]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[opslaan en toegang tot gegevens in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js-webtoepassing]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


