---
title: Web-app met table storage (Node.js) | Microsoft Docs
description: Een zelfstudie bouwt op de Web-App met snelle zelfstudie voort door toevoeging van Azure Storage-services en de Azure-module.
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
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="7bfed-103">Node.js-webtoepassing met opslag</span><span class="sxs-lookup"><span data-stu-id="7bfed-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="7bfed-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7bfed-104">Overview</span></span>
<span data-ttu-id="7bfed-105">In deze zelfstudie wordt u uitbreiden van de toepassing gemaakt de [Node.js-webtoepassing met een snelle] zelfstudie met behulp van de Microsoft Azure-clientbibliotheken voor Node.js werken met data management-services.</span><span class="sxs-lookup"><span data-stu-id="7bfed-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="7bfed-106">U kunt uw toepassing een webgebaseerde takenlijst-toepassing die u naar Azure implementeren kunt maken wordt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="7bfed-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="7bfed-107">De takenlijst kan een gebruiker taken ophalen, het toevoegen van nieuwe taken en taken te markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="7bfed-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="7bfed-108">De items worden opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7bfed-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="7bfed-109">Azure Storage biedt niet-gestructureerde gegevensopslag die fouttolerante en maximaal beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="7bfed-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="7bfed-110">Azure Storage bevat verschillende gegevensstructuren waarin u kunt opslaan en toegang tot gegevens en u van de storage-services van de API's opgenomen in de Azure SDK voor Node.js of via de REST-API's gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="7bfed-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="7bfed-111">Zie voor meer informatie [opslaan en toegang tot gegevens in Azure].</span><span class="sxs-lookup"><span data-stu-id="7bfed-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="7bfed-112">Deze zelfstudie wordt ervan uitgegaan dat u hebt voltooid de [Node.js-webtoepassing] en [Node.js snelle][Node.js-webtoepassing met een snelle] zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="7bfed-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="7bfed-113">U leert:</span><span class="sxs-lookup"><span data-stu-id="7bfed-113">You will learn:</span></span>

* <span data-ttu-id="7bfed-114">Werken met de engine Jade sjabloon</span><span class="sxs-lookup"><span data-stu-id="7bfed-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="7bfed-115">Werken met Azure Data Management-services</span><span class="sxs-lookup"><span data-stu-id="7bfed-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="7bfed-116">Een schermopname van de voltooide toepassing lager is dan:</span><span class="sxs-lookup"><span data-stu-id="7bfed-116">A screenshot of the completed application is below:</span></span>

![De voltooide webpagina in internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="7bfed-118">Storage-referenties instelling in het bestand Web.Config</span><span class="sxs-lookup"><span data-stu-id="7bfed-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="7bfed-119">U moet doorgeven in de storage-referenties voor toegang tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7bfed-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="7bfed-120">U doet dit door u toepassingsinstellingen web.config gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7bfed-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="7bfed-121">Deze instellingen worden doorgegeven als omgevingsvariabelen knooppunt, die vervolgens worden gelezen door de Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="7bfed-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7bfed-122">Storage-referenties worden alleen gebruikt wanneer de toepassing wordt geïmplementeerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfed-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="7bfed-123">Wanneer in de emulator wordt uitgevoerd, wordt de toepassing de opslagemulator gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7bfed-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="7bfed-124">Voer de volgende stappen uit om de opslagaccountreferenties ophalen en toe te voegen aan het web.config-instellingen:</span><span class="sxs-lookup"><span data-stu-id="7bfed-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="7bfed-125">Als deze nog niet is geopend, start u de Azure PowerShell uit de **Start** menu door het uitbreiden van **alle programma's, Azure**, met de rechtermuisknop op **Azure PowerShell**, en selecteer vervolgens **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="7bfed-126">Wijzig de mappen in de map met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bfed-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="7bfed-127">Bijvoorbeeld: C:\\knooppunt\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="7bfed-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="7bfed-128">Voer de volgende cmdlet om op te halen van de accountgegevens voor de opslag van de Azure Powershell-venster:</span><span class="sxs-lookup"><span data-stu-id="7bfed-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="7bfed-129">Hiermee haalt de lijst met opslagaccounts en sleutels die zijn gekoppeld aan de gehoste service-account.</span><span class="sxs-lookup"><span data-stu-id="7bfed-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7bfed-130">Omdat de Azure SDK een opslagaccount maakt wanneer u een service implementeert, moet al een opslagaccount van het implementeren van uw toepassing in de vorige handleidingen bestaan.</span><span class="sxs-lookup"><span data-stu-id="7bfed-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="7bfed-131">Open de **ServiceDefinition.csdef** bestand met de omgevingsinstellingen die worden gebruikt wanneer de toepassing wordt geïmplementeerd naar Azure:</span><span class="sxs-lookup"><span data-stu-id="7bfed-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="7bfed-132">Voeg het volgende blok onder **omgeving** element, vervangen door {OPSLAGACCOUNT} en {TOEGANGSSLEUTEL voor opslag} met de accountnaam en de primaire sleutel voor het opslagaccount dat u wilt gebruiken voor implementatie:</span><span class="sxs-lookup"><span data-stu-id="7bfed-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![De inhoud van het bestand web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="7bfed-134">Sla het bestand op en sluit Kladblok.</span><span class="sxs-lookup"><span data-stu-id="7bfed-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="7bfed-135">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="7bfed-135">Install additional modules</span></span>
1. <span data-ttu-id="7bfed-136">Gebruik de volgende opdracht voor het installeren van de [azure] [knooppunt-uuid] [nconf] en [asynchrone] modules lokaal ook om op te slaan een vermelding voor hen de **package.json** bestand:</span><span class="sxs-lookup"><span data-stu-id="7bfed-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="7bfed-137">De uitvoer van deze opdracht ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="7bfed-137">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="7bfed-138">De tabel-service in een knooppunttoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="7bfed-138">Using the Table service in a node application</span></span>
<span data-ttu-id="7bfed-139">In deze sectie kunt u de basistoepassing die is gemaakt door wordt uitgebreide de **snelle** door toe te voegen opdracht een **task.js** bestand waarin het model voor uw taken.</span><span class="sxs-lookup"><span data-stu-id="7bfed-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="7bfed-140">Ook wijzigt u de bestaande **app.js** en maak een nieuwe **tasklist.js** bestand dat gebruikmaakt van het model.</span><span class="sxs-lookup"><span data-stu-id="7bfed-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="7bfed-141">Het model maken</span><span class="sxs-lookup"><span data-stu-id="7bfed-141">Create the model</span></span>
1. <span data-ttu-id="7bfed-142">In de **WebRole1** directory, maak een nieuwe map met de naam **modellen**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="7bfed-143">In de **modellen** directory, maak een nieuw bestand met de naam **task.js**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="7bfed-144">Dit bestand bevat het model voor de taken die zijn gemaakt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bfed-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="7bfed-145">Aan het begin van de **task.js** bestand, voeg de volgende code om te verwijzen naar de vereiste bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="7bfed-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="7bfed-146">Vervolgens voegt u code toe om het taakobject te definiëren en te exporteren.</span><span class="sxs-lookup"><span data-stu-id="7bfed-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="7bfed-147">Dit object is verantwoordelijk voor het verbinden met de tabel.</span><span class="sxs-lookup"><span data-stu-id="7bfed-147">This object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="7bfed-148">Vervolgens voegt u de volgende code om aanvullende methoden voor het taakobject te definiëren waardoor er interactie met gegevens die zijn opgeslagen in de tabel:</span><span class="sxs-lookup"><span data-stu-id="7bfed-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
    ```

6. <span data-ttu-id="7bfed-149">Sla op en sluit de **task.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7bfed-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="7bfed-150">De controller maken</span><span class="sxs-lookup"><span data-stu-id="7bfed-150">Create the controller</span></span>
1. <span data-ttu-id="7bfed-151">In de **WebRole1/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7bfed-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="7bfed-152">Voeg de volgende code toe aan het bestand **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="7bfed-153">Dit wordt geladen met de azure- en async-modules die worden gebruikt door **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="7bfed-154">Hiermee ook definieert u de **TaskList** functie die wordt doorgegeven een exemplaar van de **taak** object eerder:</span><span class="sxs-lookup"><span data-stu-id="7bfed-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="7bfed-155">Blijven toevoegen aan de **tasklist.js** bestand door het toevoegen van de methoden voor **showTasks**, **addTask**, en **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="7bfed-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="7bfed-156">Sla de **tasklist.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7bfed-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="7bfed-157">App.js wijzigen</span><span class="sxs-lookup"><span data-stu-id="7bfed-157">Modify app.js</span></span>
1. <span data-ttu-id="7bfed-158">In de **WebRole1** directory, open de **app.js** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7bfed-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="7bfed-159">Voeg de volgende voor het laden van de azure-module en stel de sleutel van naam en partitie in de tabel aan het begin van het bestand:</span><span class="sxs-lookup"><span data-stu-id="7bfed-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="7bfed-160">In het bestand app.js, bladert u omlaag naar waar u de volgende regel zien:</span><span class="sxs-lookup"><span data-stu-id="7bfed-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="7bfed-161">Vervang de bovenstaande regels door de code hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7bfed-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="7bfed-162">Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding met uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="7bfed-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="7bfed-163">Dit wordt doorgegeven aan de <strong>TaskList</strong>, die wordt gebruikt om communicatie met de tabel-service:</span><span class="sxs-lookup"><span data-stu-id="7bfed-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="7bfed-164">Sla de **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7bfed-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="7bfed-165">Wijzig de weergave index</span><span class="sxs-lookup"><span data-stu-id="7bfed-165">Modify the index view</span></span>
1. <span data-ttu-id="7bfed-166">Wijzig de mappen op de **weergaven** directory en open de **index.jade** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7bfed-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="7bfed-167">Vervang de inhoud van de **index.jade** bestand met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="7bfed-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="7bfed-168">Hiermee definieert u de weergave voor het weergeven van bestaande taken, evenals een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="7bfed-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="7bfed-169">Opslaan en sluiten **index.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="7bfed-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="7bfed-170">De indeling van de globale wijzigen</span><span class="sxs-lookup"><span data-stu-id="7bfed-170">Modify the global layout</span></span>
<span data-ttu-id="7bfed-171">Het bestand **layout.jade** in de map **views** wordt gebruikt als een algemeen sjabloon voor andere **.jade**-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7bfed-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="7bfed-172">In deze stap wordt het bestand aangepast voor het gebruik van [Twitter Bootstrap](https://github.com/twbs/bootstrap). Dit is een werkset waarmee u eenvoudig een aantrekkelijk ogende website kunt maken.</span><span class="sxs-lookup"><span data-stu-id="7bfed-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="7bfed-173">Downloaden en uitpakken van de bestanden voor [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="7bfed-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="7bfed-174">Kopieer de **bootstrap.min.css** bestand van de **bootstrap\\verdeling\\css** map de **openbare\\stylesheets** map van uw toepassing tasklist.</span><span class="sxs-lookup"><span data-stu-id="7bfed-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="7bfed-175">Van de **weergaven** map, open de **layout.jade** in een teksteditor en vervang de inhoud door het volgende:</span><span class="sxs-lookup"><span data-stu-id="7bfed-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="7bfed-176">DOCTYPE HTML-html head titel = Titelkoppeling (rel = 'stylesheet', href='/stylesheets/bootstrap.min.css') koppeling (rel = 'stylesheet', href='/stylesheets/style.css') body.app nav.navbar.navbar-standaard div.navbar-header a.navbar-brand(href='/') inhoud van mijn taken blokkeren</span><span class="sxs-lookup"><span data-stu-id="7bfed-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="7bfed-177">Sla de **layout.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="7bfed-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="7bfed-178">De toepassing wordt uitgevoerd in de Emulator</span><span class="sxs-lookup"><span data-stu-id="7bfed-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="7bfed-179">Gebruik de volgende opdracht voor het starten van de toepassing in de emulator.</span><span class="sxs-lookup"><span data-stu-id="7bfed-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="7bfed-180">De browser wordt geopend en de volgende pagina wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7bfed-180">The browser will open and displays the following page:</span></span>

![Een web wisselbaar geheugen: met de titel van mijn takenlijst met een tabel met taken en velden in om een nieuwe taak toevoegen.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="7bfed-182">Gebruik het formulier items toevoegen of verwijderen van bestaande items door deze te markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="7bfed-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="7bfed-183">Publiceren van de toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="7bfed-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="7bfed-184">Aanroepen in de Windows PowerShell-venster de volgende cmdlet als u wilt uw gehoste service in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="7bfed-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="7bfed-185">Vervang **myuniquename** met een unieke naam voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bfed-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="7bfed-186">Vervang **datacentername** met de naam van een Azure-Datacenter, zoals **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="7bfed-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="7bfed-187">Nadat de implementatie voltooid is, ziet u een reactie vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="7bfed-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="7bfed-188">Als voorheen omdat u opgegeven de **-starten** optie, de browser wordt geopend en geeft u uw toepassing in Azure wordt uitgevoerd als het publiceren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7bfed-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Een browservenster met de pagina Mijn takenlijst.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="7bfed-191">Stoppen en verwijderen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="7bfed-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="7bfed-192">Na implementatie van uw toepassing, wilt u mogelijk uitgeschakeld zodat u kunt kosten voorkomen of bouwen en implementeren van andere toepassingen binnen de periode voor de gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="7bfed-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="7bfed-193">Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="7bfed-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="7bfed-194">Er wordt servertijd verbruikt zodra de toepassing is geïmplementeerd, zelfs als de exemplaren niet worden uitgevoerd en de gestopte status hebben.</span><span class="sxs-lookup"><span data-stu-id="7bfed-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="7bfed-195">De volgende stappen laten zien hoe om te stoppen en verwijderen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bfed-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="7bfed-196">In het Windows PowerShell-venster stopt u de service-implementatie die u in de vorige sectie hebt gemaakt, met de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7bfed-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="7bfed-197">Het kan enkele minuten duren voordat de service is gestopt.</span><span class="sxs-lookup"><span data-stu-id="7bfed-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="7bfed-198">Als de service is gestopt, krijgt u een bericht waarin dit wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="7bfed-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="7bfed-199">Als u de service wilt verwijderen, roept u de volgende cmdlet aan:</span><span class="sxs-lookup"><span data-stu-id="7bfed-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="7bfed-200">Wanneer dit wordt gevraagd, typt u **Y** om de service te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7bfed-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="7bfed-201">Het kan enkele minuten duren voordat de service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7bfed-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="7bfed-202">Als de service is verwijderd, krijgt u een bericht waarin dit wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="7bfed-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="7bfed-203">[Node.js-webtoepassing met een snelle]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="7bfed-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="7bfed-204">[opslaan en toegang tot gegevens in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="7bfed-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="7bfed-205">[Node.js-webtoepassing]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="7bfed-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


