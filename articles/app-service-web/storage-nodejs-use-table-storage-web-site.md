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
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="d545c-103">Node.js-web-app met de Azure-tabelservice</span><span class="sxs-lookup"><span data-stu-id="d545c-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="d545c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d545c-104">Overview</span></span>
<span data-ttu-id="d545c-105">Deze zelfstudie leert u hoe u tabel-service van Azure Data Management opslaan en gebruiken van gegevens uit een [knooppunt] toepassing wordt gehost [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="d545c-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="d545c-106">Deze zelfstudie wordt ervan uitgegaan dat u hebt enige ervaring met knooppunt en [Git].</span><span class="sxs-lookup"><span data-stu-id="d545c-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="d545c-107">U leert:</span><span class="sxs-lookup"><span data-stu-id="d545c-107">You will learn:</span></span>

* <span data-ttu-id="d545c-108">Hoe de knooppunt-modules installeren met npm (Pakketbeheer knooppunt)</span><span class="sxs-lookup"><span data-stu-id="d545c-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="d545c-109">Werken met de Azure Table-service</span><span class="sxs-lookup"><span data-stu-id="d545c-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="d545c-110">Het gebruik van de Azure CLI voor het maken van een web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="d545c-111">Door deze zelfstudie te volgen, bouwt u een eenvoudige web gebaseerde 'takenlijst'-toepassing die u kunt maken, ophalen en uitvoeren van taken.</span><span class="sxs-lookup"><span data-stu-id="d545c-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="d545c-112">De taken worden opgeslagen in de tabel-service.</span><span class="sxs-lookup"><span data-stu-id="d545c-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="d545c-113">Hier volgt de voltooide toepassing:</span><span class="sxs-lookup"><span data-stu-id="d545c-113">Here is the completed application:</span></span>

![Een webpagina een leeg tasklist weergeven][node-table-finished]

> [!NOTE]
> <span data-ttu-id="d545c-115">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="d545c-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d545c-116">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="d545c-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d545c-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d545c-117">Prerequisites</span></span>
<span data-ttu-id="d545c-118">Voordat u de instructies in dit artikel uitvoert, zorg ervoor dat u het volgende zijn geïnstalleerd hebt:</span><span class="sxs-lookup"><span data-stu-id="d545c-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="d545c-119">[knooppunt] versie 0.10.24 of hoger</span><span class="sxs-lookup"><span data-stu-id="d545c-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="d545c-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="d545c-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="d545c-121">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="d545c-121">Create a storage account</span></span>
<span data-ttu-id="d545c-122">Een Azure-opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="d545c-122">Create an Azure storage account.</span></span> <span data-ttu-id="d545c-123">De app wordt dit account gebruiken voor het opslaan van de taakitems.</span><span class="sxs-lookup"><span data-stu-id="d545c-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="d545c-124">Meld u aan bij de [Azure-Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d545c-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d545c-125">Klik op de **nieuw** pictogram aan de onderkant van de portal links, klikt u op **gegevens en opslag** > **opslag**.</span><span class="sxs-lookup"><span data-stu-id="d545c-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="d545c-126">Geef het storage-account een unieke naam en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.</span><span class="sxs-lookup"><span data-stu-id="d545c-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Knop Nieuw](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="d545c-128">Wanneer het opslagaccount is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en het opslagaccount blade geopend om weer te geven dat hoort bij de nieuwe resourcegroep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d545c-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="d545c-129">Klik op het opslagaccount blade **instellingen** > **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="d545c-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="d545c-130">De primaire toegangssleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d545c-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Toegangstoets][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="d545c-132">Modules installeren en steigers genereren</span><span class="sxs-lookup"><span data-stu-id="d545c-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="d545c-133">In deze sectie wordt u een nieuw knooppunttoepassing maken en npm module pakketten moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d545c-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="d545c-134">Voor deze toepassing gebruikt u de [Express] en [Azure] modules.</span><span class="sxs-lookup"><span data-stu-id="d545c-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="d545c-135">De Express-module biedt een framework Model-View-Controller voor knooppunt terwijl de modules die Azure biedt verbinding met de tabel-service.</span><span class="sxs-lookup"><span data-stu-id="d545c-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="d545c-136">Express installeren en steigers genereren</span><span class="sxs-lookup"><span data-stu-id="d545c-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="d545c-137">Maak een nieuwe map met de naam vanaf de opdrachtregel **tasklist** en Ga naar de map.</span><span class="sxs-lookup"><span data-stu-id="d545c-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="d545c-138">Voer de volgende opdracht voor het installeren van de Express-module.</span><span class="sxs-lookup"><span data-stu-id="d545c-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="d545c-139">Afhankelijk van het besturingssysteem moet u mogelijk plaatsen 'sudo ' uitgebreid voor de opdracht:</span><span class="sxs-lookup"><span data-stu-id="d545c-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="d545c-140">De uitvoer lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d545c-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="d545c-141">De '-g' parameter wordt de module globaal geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d545c-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="d545c-142">Op die manier kunnen we gebruiken **snelle** voor het genereren van web-app steigers zonder aanvullende padinformatie typen.</span><span class="sxs-lookup"><span data-stu-id="d545c-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="d545c-143">Voer voor het maken van de steiger voor de toepassing de **snelle** opdracht:</span><span class="sxs-lookup"><span data-stu-id="d545c-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="d545c-144">De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="d545c-144">The output of this command appears similar to the following example:</span></span>
   
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
   
    <span data-ttu-id="d545c-145">U hebt nu verschillende nieuwe mappen en bestanden in de **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="d545c-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="d545c-146">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="d545c-146">Install additional modules</span></span>
<span data-ttu-id="d545c-147">Een van de bestanden die **snelle** maakt is **package.json**.</span><span class="sxs-lookup"><span data-stu-id="d545c-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="d545c-148">Dit bestand bevat een lijst met afhankelijkheden van de module.</span><span class="sxs-lookup"><span data-stu-id="d545c-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="d545c-149">Later, wanneer u de toepassing naar App Service Web Apps implementeert, bepaalt dit bestand welke modules moeten worden geïnstalleerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="d545c-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="d545c-150">Vanaf de opdrachtregel, voer de volgende opdracht voor het installeren van de modules die zijn beschreven in de **package.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="d545c-151">U wilt gebruiken 'sudo ' uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="d545c-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="d545c-152">De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="d545c-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="d545c-153">Geef vervolgens de volgende opdracht voor het installeren van de [azure], [knooppunt uuid], [nconf] en [asynchrone] modules:</span><span class="sxs-lookup"><span data-stu-id="d545c-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="d545c-154">De **--opslaan** vlag voegt vermeldingen voor deze modules naar de **package.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="d545c-155">De uitvoer van deze opdracht ziet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="d545c-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="d545c-156">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="d545c-156">Create the application</span></span>
<span data-ttu-id="d545c-157">Nu we gaan de toepassing te bouwen.</span><span class="sxs-lookup"><span data-stu-id="d545c-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="d545c-158">Een model maken</span><span class="sxs-lookup"><span data-stu-id="d545c-158">Create a model</span></span>
<span data-ttu-id="d545c-159">Een *model* is een object dat de gegevens in uw toepassing vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="d545c-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="d545c-160">Het enige model is voor de toepassing een taakobject een item in de takenlijst vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="d545c-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="d545c-161">Taken hebben de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="d545c-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="d545c-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="d545c-162">PartitionKey</span></span>
* <span data-ttu-id="d545c-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="d545c-163">RowKey</span></span>
* <span data-ttu-id="d545c-164">naam (tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="d545c-164">name (string)</span></span>
* <span data-ttu-id="d545c-165">categorie (tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="d545c-165">category (string)</span></span>
* <span data-ttu-id="d545c-166">voltooid (Booleaanse waarde)</span><span class="sxs-lookup"><span data-stu-id="d545c-166">completed (Boolean)</span></span>

<span data-ttu-id="d545c-167">**PartitionKey** en **RowKey** als tabelsleutels worden gebruikt door de Tabelservice.</span><span class="sxs-lookup"><span data-stu-id="d545c-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="d545c-168">Zie voor meer informatie [inzicht in het Tabelservice-gegevensmodel](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="d545c-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="d545c-169">In de **tasklist** directory, maak een nieuwe map met de naam **modellen**.</span><span class="sxs-lookup"><span data-stu-id="d545c-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="d545c-170">In de **modellen** directory, maak een nieuw bestand met de naam **task.js**.</span><span class="sxs-lookup"><span data-stu-id="d545c-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="d545c-171">Dit bestand bevat het model voor de taken die zijn gemaakt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d545c-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="d545c-172">Aan het begin van de **task.js** bestand, voeg de volgende code om te verwijzen naar de vereiste bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="d545c-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="d545c-173">Voeg de volgende code om te definiëren en exporteren van het taakobject.</span><span class="sxs-lookup"><span data-stu-id="d545c-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="d545c-174">Dit object is verantwoordelijk voor het verbinden met de tabel.</span><span class="sxs-lookup"><span data-stu-id="d545c-174">This object is responsible for connecting to the table.</span></span>
   
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
5. <span data-ttu-id="d545c-175">Voeg de volgende code om te definiëren van aanvullende methoden voor het taakobject waardoor er interactie met gegevens die zijn opgeslagen in de tabel:</span><span class="sxs-lookup"><span data-stu-id="d545c-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
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
6. <span data-ttu-id="d545c-176">Sla op en sluit de **task.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="d545c-177">Maak een domeincontroller</span><span class="sxs-lookup"><span data-stu-id="d545c-177">Create a controller</span></span>
<span data-ttu-id="d545c-178">Een *controller* HTTP-aanvragen worden verwerkt op en geeft u het HTML-antwoord.</span><span class="sxs-lookup"><span data-stu-id="d545c-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="d545c-179">In de **tasklist/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="d545c-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="d545c-180">Voeg de volgende code toe aan het bestand **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="d545c-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="d545c-181">Dit wordt geladen met de azure- en async-modules die worden gebruikt door **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="d545c-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="d545c-182">Hiermee ook definieert u de **TaskList** functie die wordt doorgegeven een exemplaar van de **taak** object eerder:</span><span class="sxs-lookup"><span data-stu-id="d545c-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="d545c-183">Definieer een **TaskList** object.</span><span class="sxs-lookup"><span data-stu-id="d545c-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="d545c-184">Voeg de volgende methoden om te **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="d545c-184">Add the following methods to **TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="d545c-185">App.js wijzigen</span><span class="sxs-lookup"><span data-stu-id="d545c-185">Modify app.js</span></span>
1. <span data-ttu-id="d545c-186">Van de **tasklist** directory, open de **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="d545c-187">Dit bestand is gemaakt door het uitvoeren van de **snelle** opdracht.</span><span class="sxs-lookup"><span data-stu-id="d545c-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="d545c-188">Toevoegen aan het begin van het bestand, het volgende om te laden van de azure-module, de naam van de tabel, partitiesleutel en de storage-referenties die worden gebruikt door het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d545c-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="d545c-189">nconf laadt de configuratiewaarden van beide omgevingsvariabelen of de **config.json** bestand, dat we later gaan maken.</span><span class="sxs-lookup"><span data-stu-id="d545c-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="d545c-190">In het bestand app.js, bladert u omlaag naar waar u de volgende regel zien:</span><span class="sxs-lookup"><span data-stu-id="d545c-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="d545c-191">Vervang de bovenstaande regels door de code hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d545c-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="d545c-192">Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding met uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="d545c-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="d545c-193">Dit wordt doorgegeven aan de <strong>TaskList</strong>, die wordt gebruikt om communicatie met de tabel-service:</span><span class="sxs-lookup"><span data-stu-id="d545c-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="d545c-194">Sla de **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="d545c-195">Wijzig de weergave index</span><span class="sxs-lookup"><span data-stu-id="d545c-195">Modify the index view</span></span>
1. <span data-ttu-id="d545c-196">Open de **tasklist/views/index.jade** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="d545c-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="d545c-197">Vervang de volledige inhoud van het bestand door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="d545c-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="d545c-198">Hiermee definieert u een weergave die bestaande taken weergegeven en bevat een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="d545c-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="d545c-199">Opslaan en sluiten **index.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="d545c-200">De indeling van de globale wijzigen</span><span class="sxs-lookup"><span data-stu-id="d545c-200">Modify the global layout</span></span>
<span data-ttu-id="d545c-201">De **layout.jade** bestand de **weergaven** map is een algemene sjabloon voor andere **.jade** bestanden.</span><span class="sxs-lookup"><span data-stu-id="d545c-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="d545c-202">In deze stap wijzigt u het gebruik van [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u gemakkelijk voor het ontwerpen van een nice ogende web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="d545c-203">Downloaden en uitpakken van de bestanden voor [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="d545c-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="d545c-204">Kopieer de **bootstrap.min.css** bestand van de Bootstrap **css** map in de **openbare/stylesheets** map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d545c-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="d545c-205">Van de **weergaven** map, open **layout.jade** en vervang de volledige inhoud door het volgende:</span><span class="sxs-lookup"><span data-stu-id="d545c-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="d545c-206">Een configuratiebestand maken</span><span class="sxs-lookup"><span data-stu-id="d545c-206">Create a config file</span></span>
<span data-ttu-id="d545c-207">Als u wilt uitvoeren van de app hebt we lokaal, Azure Storage-referenties in een configuratiebestand plaatsen.</span><span class="sxs-lookup"><span data-stu-id="d545c-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="d545c-208">Maak een bestand met de naam **config.json* * met de volgende JSON:</span><span class="sxs-lookup"><span data-stu-id="d545c-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="d545c-209">Vervang **opslagaccountnaam** rekening met de naam van de opslag die u eerder hebt gemaakt en vervang **toegangssleutel voor opslag** met de primaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d545c-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="d545c-210">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d545c-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="d545c-211">Sla dit bestand *hoger niveau van één map* dan de **tasklist** map als volgt:</span><span class="sxs-lookup"><span data-stu-id="d545c-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="d545c-212">De reden hiervoor is om te voorkomen dat het configuratiebestand controleren in broncodebeheer, waar mogelijk komen openbare.</span><span class="sxs-lookup"><span data-stu-id="d545c-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="d545c-213">Wanneer we de app in Azure implementeert, gebruiken we omgevingsvariabelen in plaats van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d545c-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="d545c-214">De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d545c-214">Run the application locally</span></span>
<span data-ttu-id="d545c-215">Testen van de toepassing op uw lokale computer, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d545c-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="d545c-216">Vanaf de opdrachtregel, wijzig de mappen op de **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="d545c-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="d545c-217">Gebruik de volgende opdracht om de toepassing lokaal te starten:</span><span class="sxs-lookup"><span data-stu-id="d545c-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="d545c-218">Open een webbrowser en navigeer naar http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="d545c-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="d545c-219">Een webpagina die vergelijkbaar is met het volgende voorbeeld wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d545c-219">A web page similar to the following example appears.</span></span>
   
    ![Een webpagina een leeg tasklist weergeven][node-table-finished]
4. <span data-ttu-id="d545c-221">Voer een naam en categorie voor het maken van een nieuwe taakitem en klik op **Item toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d545c-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="d545c-222">Voor een taak markeren als voltooid, Controleer **Complete** en klik op **taken bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="d545c-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Een installatiekopie van het nieuwe item in de lijst met taken][node-table-list-items]

<span data-ttu-id="d545c-224">Zelfs als de toepassing lokaal wordt uitgevoerd, wordt het opslaan van gegevens in de Azure Table-service.</span><span class="sxs-lookup"><span data-stu-id="d545c-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="d545c-225">Uw toepassing in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="d545c-225">Deploy your application to Azure</span></span>
<span data-ttu-id="d545c-226">De stappen in deze sectie de Azure-opdrachtregelprogramma's gebruiken om u te maken van een nieuwe web-app in App Service, en gebruik vervolgens Git om uw toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="d545c-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="d545c-227">U moet een Azure-abonnement hebben om deze stappen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d545c-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d545c-228">Deze stappen kunnen ook worden uitgevoerd met behulp van de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d545c-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d545c-229">Zie [bouwen en implementeren van een Node.js-web-app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="d545c-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="d545c-230">Als dit de eerste web-app die u hebt gemaakt, moet u de Azure Portal gebruiken om deze toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="d545c-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="d545c-231">Om te beginnen, installeert u de [Azure CLI] met de volgende opdracht vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="d545c-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="d545c-232">Publicatie-instellingen importeren</span><span class="sxs-lookup"><span data-stu-id="d545c-232">Import publishing settings</span></span>
<span data-ttu-id="d545c-233">In deze stap downloadt u een bestand met gegevens over uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d545c-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="d545c-234">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="d545c-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="d545c-235">Met deze opdracht wordt gestart van een browser en gaat u naar de downloadpagina.</span><span class="sxs-lookup"><span data-stu-id="d545c-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="d545c-236">Als u wordt gevraagd, meldt u zich aan met het account dat is gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d545c-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="d545c-237">Downloaden van het bestand begint automatisch; Als dit niet het geval is, kunt u de koppeling aan het begin van de pagina handmatig het bestand te downloaden.</span><span class="sxs-lookup"><span data-stu-id="d545c-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="d545c-238">Sla het bestand op en noteer het pad.</span><span class="sxs-lookup"><span data-stu-id="d545c-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="d545c-239">Voer de volgende opdracht om de instellingen te importeren:</span><span class="sxs-lookup"><span data-stu-id="d545c-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="d545c-240">Geef het pad en de naam van het gedownloade instellingenbestand publishing in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="d545c-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="d545c-241">Als de instellingen worden geïmporteerd, verwijdert u het instellingenbestand publiceren.</span><span class="sxs-lookup"><span data-stu-id="d545c-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="d545c-242">Het is niet meer nodig en gevoelige informatie met betrekking tot uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="d545c-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="d545c-243">Een App Service-web-app maken</span><span class="sxs-lookup"><span data-stu-id="d545c-243">Create an App Service web app</span></span>
1. <span data-ttu-id="d545c-244">Vanaf de opdrachtregel, wijzig de mappen op de **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="d545c-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="d545c-245">Gebruik de volgende opdracht voor het maken van een nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="d545c-246">U wordt gevraagd om de web-app-naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="d545c-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="d545c-247">Geef een unieke naam en selecteer dezelfde geografische locatie als uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="d545c-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="d545c-248">De `--git` parameter maakt u een Git-opslagplaats in Azure voor deze web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="d545c-249">Deze ook een Git-opslagplaats in de huidige map initialiseert als er geen bestaat en voegt een [Git remote] met de naam 'azure', waarmee de toepassing publiceren in Azure.</span><span class="sxs-lookup"><span data-stu-id="d545c-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="d545c-250">Ten slotte wordt het maken van een **web.config** bestand, dat instellingen die door Azure worden gebruikt om als host knooppunt toepassingen bevat.</span><span class="sxs-lookup"><span data-stu-id="d545c-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="d545c-251">Als u weglaat de `--git` parameter, maar de map bevat een Git-opslagplaats, de opdracht wordt nog steeds maken 'azure' externe.</span><span class="sxs-lookup"><span data-stu-id="d545c-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="d545c-252">Zodra deze opdracht is voltooid, ziet u uitvoer ziet er als volgt.</span><span class="sxs-lookup"><span data-stu-id="d545c-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="d545c-253">Houd er rekening mee dat de regel die beginnen met **Website gemaakt op** de URL voor de web-app bevat.</span><span class="sxs-lookup"><span data-stu-id="d545c-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
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
   > <span data-ttu-id="d545c-254">Als dit de eerste App Service web-app voor uw abonnement, wordt u gevraagd de Azure Portal gebruiken om te maken van de web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="d545c-255">Zie voor meer informatie [bouwen en implementeren van een Node.js-web-app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="d545c-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="d545c-256">De omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="d545c-256">Set environment variables</span></span>
<span data-ttu-id="d545c-257">In deze stap maakt toevoegt u omgevingsvariabelen aan de configuratie van uw web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="d545c-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="d545c-258">Voer de volgende gegevens vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="d545c-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="d545c-259">Vervang  **<storage account name>**  rekening met de naam van de opslag die u eerder hebt gemaakt en vervang  **<storage access key>**  met de primaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d545c-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="d545c-260">(Gebruik dezelfde waarden als de config.json-bestand dat u eerder hebt gemaakt.)</span><span class="sxs-lookup"><span data-stu-id="d545c-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="d545c-261">U kunt ook omgevingsvariabelen instellen de [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="d545c-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="d545c-262">De web-app-blade geopend door te klikken op **Bladeren** > **Web-Apps** > de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="d545c-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="d545c-263">Klik op de blade van uw web-app **alle instellingen** > **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="d545c-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="d545c-264">Schuif omlaag naar de **appinstellingen** sectie en de sleutel/waarde-paren toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d545c-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![App-instellingen](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="d545c-266">Klik op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="d545c-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="d545c-267">De toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="d545c-267">Publish the application</span></span>
<span data-ttu-id="d545c-268">De codebestanden doorvoeren in Git en vervolgens push naar azure/master voor het publiceren van de app.</span><span class="sxs-lookup"><span data-stu-id="d545c-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="d545c-269">Stel de implementatiereferenties van uw.</span><span class="sxs-lookup"><span data-stu-id="d545c-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="d545c-270">Toevoegen en uw toepassingsbestanden worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d545c-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="d545c-271">Push het doorvoeren naar de App Service-web-app:</span><span class="sxs-lookup"><span data-stu-id="d545c-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="d545c-272">Gebruik **master** als de doel-vertakking.</span><span class="sxs-lookup"><span data-stu-id="d545c-272">Use **master** as the target branch.</span></span> <span data-ttu-id="d545c-273">Aan het einde van de implementatie ziet u een instructie die vergelijkbaar is met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d545c-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="d545c-274">Zodra de push-bewerking is voltooid, bladert u naar de web-app-URL die eerder zijn geretourneerd door de `azure create site` opdracht om uw toepassing weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d545c-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d545c-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d545c-275">Next steps</span></span>
<span data-ttu-id="d545c-276">Hoewel de stappen in dit artikel wordt beschreven met behulp van de tabel-Service gegevens op te slaan, kunt u ook gebruiken [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="d545c-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d545c-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d545c-277">Additional resources</span></span>
<span data-ttu-id="d545c-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="d545c-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d545c-279">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="d545c-279">What's changed</span></span>
* <span data-ttu-id="d545c-280">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d545c-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="d545c-281">[bouwen en implementeren van een Node.js-web-app in Azure App Service]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="d545c-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="d545c-282">[knooppunt]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="d545c-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="d545c-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="d545c-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="d545c-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="d545c-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="d545c-285">[Git remote]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="d545c-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="d545c-286">[Azure CLI]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="d545c-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="d545c-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="d545c-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="d545c-288">[knooppunt uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="d545c-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="d545c-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="d545c-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="d545c-290">[asynchrone]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="d545c-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
