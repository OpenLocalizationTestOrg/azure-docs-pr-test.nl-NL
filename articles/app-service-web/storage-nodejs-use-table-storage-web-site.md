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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="7abcd-103">Node.js web-app met behulp van hello Azure Table-Service</span><span class="sxs-lookup"><span data-stu-id="7abcd-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="7abcd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7abcd-104">Overview</span></span>
<span data-ttu-id="7abcd-105">Deze zelfstudie leert u hoe de tabelservice toouse geleverd door Azure Data Management toostore en toegang tot gegevens uit een [knooppunt] toepassing wordt gehost [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="7abcd-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="7abcd-106">Deze zelfstudie wordt ervan uitgegaan dat u hebt enige ervaring met knooppunt en [Git].</span><span class="sxs-lookup"><span data-stu-id="7abcd-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="7abcd-107">U leert:</span><span class="sxs-lookup"><span data-stu-id="7abcd-107">You will learn:</span></span>

* <span data-ttu-id="7abcd-108">Hoe toouse npm (Pakketbeheer knooppunt) tooinstall Hallo knooppunt modules</span><span class="sxs-lookup"><span data-stu-id="7abcd-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="7abcd-109">Hoe toowork met hello Azure Table-service</span><span class="sxs-lookup"><span data-stu-id="7abcd-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="7abcd-110">Hoe toouse hello Azure CLI toocreate een web-app.</span><span class="sxs-lookup"><span data-stu-id="7abcd-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="7abcd-111">Door deze zelfstudie te volgen, bouwt u een eenvoudige web gebaseerde 'takenlijst'-toepassing die u kunt maken, ophalen en uitvoeren van taken.</span><span class="sxs-lookup"><span data-stu-id="7abcd-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="7abcd-112">Hallo-taken worden opgeslagen in Hallo tabel-service.</span><span class="sxs-lookup"><span data-stu-id="7abcd-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="7abcd-113">Dit is de toepassing hello voltooid:</span><span class="sxs-lookup"><span data-stu-id="7abcd-113">Here is hello completed application:</span></span>

![Een webpagina een leeg tasklist weergeven][node-table-finished]

> [!NOTE]
> <span data-ttu-id="7abcd-115">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="7abcd-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7abcd-116">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7abcd-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7abcd-117">Prerequisites</span></span>
<span data-ttu-id="7abcd-118">Zorg ervoor dat er Hallo volgende zijn geïnstalleerd voordat Hallo-instructies in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="7abcd-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="7abcd-119">[knooppunt] versie 0.10.24 of hoger</span><span class="sxs-lookup"><span data-stu-id="7abcd-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="7abcd-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="7abcd-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="7abcd-121">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7abcd-121">Create a storage account</span></span>
<span data-ttu-id="7abcd-122">Een Azure-opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="7abcd-122">Create an Azure storage account.</span></span> <span data-ttu-id="7abcd-123">Hallo-app gebruikt deze account toostore Hallo-taakitems.</span><span class="sxs-lookup"><span data-stu-id="7abcd-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="7abcd-124">Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7abcd-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7abcd-125">Klik op Hallo **nieuw** pictogram op Hallo onder, links van de Hallo-portal, klikt u op **gegevens en opslag** > **opslag**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="7abcd-126">Hallo storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.</span><span class="sxs-lookup"><span data-stu-id="7abcd-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Knop Nieuw](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="7abcd-128">Wanneer Hallo storage-account is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en blade Hallo van het opslagaccount is geopend dat deze deel uitmaakt van de nieuwe resource toohello tooshow groep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7abcd-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="7abcd-129">Klik op Hallo van het opslagaccount blade **instellingen** > **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="7abcd-130">Hallo primaire sleutel toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7abcd-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Toegangstoets][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="7abcd-132">Modules installeren en steigers genereren</span><span class="sxs-lookup"><span data-stu-id="7abcd-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="7abcd-133">In deze sectie wordt u een nieuw knooppunttoepassing maken en npm tooadd module pakketten.</span><span class="sxs-lookup"><span data-stu-id="7abcd-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="7abcd-134">Voor deze toepassing gaat u Hallo [Express] en [Azure] modules.</span><span class="sxs-lookup"><span data-stu-id="7abcd-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="7abcd-135">Hallo Express-module biedt een framework Model-View-Controller voor knooppunt, tijdens het Hallo Azure modules connectivity toohello tabel-service biedt.</span><span class="sxs-lookup"><span data-stu-id="7abcd-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="7abcd-136">Express installeren en steigers genereren</span><span class="sxs-lookup"><span data-stu-id="7abcd-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="7abcd-137">Maak een nieuwe map met de naam vanaf de opdrachtregel Hallo **tasklist** en switch toothat directory.</span><span class="sxs-lookup"><span data-stu-id="7abcd-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="7abcd-138">Voer Hallo opdracht tooinstall Hallo Express module te volgen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="7abcd-139">Afhankelijk van het Hallo-besturingssysteem moet u tooput 'sudo ' uitgebreid voor Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="7abcd-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="7abcd-140">Hallo-uitvoer wordt weergegeven vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="7abcd-141">Hallo '-g' parameter Hallo module globaal installeert.</span><span class="sxs-lookup"><span data-stu-id="7abcd-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="7abcd-142">Op die manier kunnen we gebruiken **snelle** toogenerate web app steigers zonder tootype in extra padinformatie.</span><span class="sxs-lookup"><span data-stu-id="7abcd-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="7abcd-143">toocreate hello steigers voor toepassing hello, Voer Hallo **snelle** opdracht:</span><span class="sxs-lookup"><span data-stu-id="7abcd-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="7abcd-144">Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7abcd-144">hello output of this command appears similar toohello following example:</span></span>
   
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
   
    <span data-ttu-id="7abcd-145">U hebt nu verschillende nieuwe mappen en bestanden in Hallo **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="7abcd-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="7abcd-146">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="7abcd-146">Install additional modules</span></span>
<span data-ttu-id="7abcd-147">Een van de Hallo bestanden die **snelle** maakt is **package.json**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="7abcd-148">Dit bestand bevat een lijst met afhankelijkheden van de module.</span><span class="sxs-lookup"><span data-stu-id="7abcd-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="7abcd-149">Later, wanneer u Hallo toepassing tooApp Service Web Apps implementeert, bepaalt dit bestand welke modules moeten toobe geïnstalleerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="7abcd-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="7abcd-150">Van Hallo opdrachtregelprogramma, Voer Hallo na de opdracht tooinstall Hallo modules dat wordt beschreven in Hallo **package.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="7abcd-151">Mogelijk moet u toouse 'sudo ' uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="7abcd-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="7abcd-152">Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7abcd-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="7abcd-153">Geef vervolgens de volgende opdracht tooinstall Hallo Hallo [azure], [knooppunt uuid], [nconf] en [asynchrone] modules:</span><span class="sxs-lookup"><span data-stu-id="7abcd-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="7abcd-154">Hallo **--opslaan** vlag voegt vermeldingen voor deze modules toohello **package.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="7abcd-155">Hallo-uitvoer van deze opdracht wordt vergelijkbaar toohello volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7abcd-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="7abcd-156">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="7abcd-156">Create hello application</span></span>
<span data-ttu-id="7abcd-157">Nu we klaar toobuild Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7abcd-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="7abcd-158">Een model maken</span><span class="sxs-lookup"><span data-stu-id="7abcd-158">Create a model</span></span>
<span data-ttu-id="7abcd-159">Een *model* is een object dat de gegevens in uw toepassing hello vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="7abcd-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="7abcd-160">Hallo alleen model is voor de toepassing hello, een taakobject een item in de takenlijst Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="7abcd-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="7abcd-161">Taken een Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="7abcd-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7abcd-162">PartitionKey</span></span>
* <span data-ttu-id="7abcd-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="7abcd-163">RowKey</span></span>
* <span data-ttu-id="7abcd-164">naam (tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="7abcd-164">name (string)</span></span>
* <span data-ttu-id="7abcd-165">categorie (tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="7abcd-165">category (string)</span></span>
* <span data-ttu-id="7abcd-166">voltooid (Booleaanse waarde)</span><span class="sxs-lookup"><span data-stu-id="7abcd-166">completed (Boolean)</span></span>

<span data-ttu-id="7abcd-167">**PartitionKey** en **RowKey** worden gebruikt door Hallo Tabelservice als tabelsleutels.</span><span class="sxs-lookup"><span data-stu-id="7abcd-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="7abcd-168">Zie voor meer informatie [Understanding Hallo Tabelservice-gegevensmodel](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="7abcd-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="7abcd-169">In Hallo **tasklist** directory, maak een nieuwe map met de naam **modellen**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="7abcd-170">In Hallo **modellen** directory, maak een nieuw bestand met de naam **task.js**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="7abcd-171">Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7abcd-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="7abcd-172">Aan begin Hallo Hallo **task.js** bestand, het toevoegen van Hallo code tooreference vereist bibliotheken te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="7abcd-173">Hallo volgende toodefine code en exporteren van het taakobject Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="7abcd-174">Dit object is verantwoordelijk voor het verbinden van toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="7abcd-174">This object is responsible for connecting toohello table.</span></span>
   
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
5. <span data-ttu-id="7abcd-175">Toevoegen Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in de tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="7abcd-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
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
6. <span data-ttu-id="7abcd-176">Opslaan en sluiten Hallo **task.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="7abcd-177">Maak een domeincontroller</span><span class="sxs-lookup"><span data-stu-id="7abcd-177">Create a controller</span></span>
<span data-ttu-id="7abcd-178">Een *controller* HTTP-aanvragen worden verwerkt en rendert Hallo HTML-antwoord.</span><span class="sxs-lookup"><span data-stu-id="7abcd-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="7abcd-179">In Hallo **tasklist/routes** directory, maak een nieuw bestand met de naam **tasklist.js** en open het in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7abcd-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="7abcd-180">Hallo code te volgen toevoegen**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="7abcd-181">Dit wordt geladen hello azure en async-modules die worden gebruikt door **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="7abcd-182">Hiermee definieert u ook Hallo **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** object eerder:</span><span class="sxs-lookup"><span data-stu-id="7abcd-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="7abcd-183">Definieer een **TaskList** object.</span><span class="sxs-lookup"><span data-stu-id="7abcd-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="7abcd-184">Toevoegen van de volgende methoden te Hallo**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="7abcd-184">Add hello following methods too**TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="7abcd-185">App.js wijzigen</span><span class="sxs-lookup"><span data-stu-id="7abcd-185">Modify app.js</span></span>
1. <span data-ttu-id="7abcd-186">Van Hallo **tasklist** directory, open Hallo **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="7abcd-187">Dit bestand is gemaakt door het uitvoeren van Hallo **snelle** opdracht.</span><span class="sxs-lookup"><span data-stu-id="7abcd-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="7abcd-188">Toevoegen aan het begin van de Hallo van Hallo-bestand, Hallo tooload hello azure module, set Hallo tabelnaam partitiesleutel en set Hallo opslag referenties op die in dit voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="7abcd-189">nconf laadt Hallo configuratiewaarden van omgevingsvariabelen of Hallo **config.json** bestand, dat we later gaan maken.</span><span class="sxs-lookup"><span data-stu-id="7abcd-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="7abcd-190">In het bestand app.js hello, schuif naar beneden toowhere u ziet Hallo volgende regel:</span><span class="sxs-lookup"><span data-stu-id="7abcd-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="7abcd-191">Hallo boven regels vervangen door Hallo-code hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7abcd-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="7abcd-192">Hiermee wordt een exemplaar van initialiseren <strong>taak</strong> met een verbinding tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="7abcd-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="7abcd-193">Dit wordt doorgegeven toohello <strong>TaskList</strong>, welke gebruiken deze toocommunicate Hello tabelservice:</span><span class="sxs-lookup"><span data-stu-id="7abcd-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="7abcd-194">Hallo opslaan **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="7abcd-195">Hallo index weergave wijzigen</span><span class="sxs-lookup"><span data-stu-id="7abcd-195">Modify hello index view</span></span>
1. <span data-ttu-id="7abcd-196">Open Hallo **tasklist/views/index.jade** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7abcd-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="7abcd-197">Vervang de volledige inhoud van de Hallo van Hallo-bestand met de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="7abcd-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="7abcd-198">Hiermee definieert u een weergave die bestaande taken weergegeven en bevat een formulier voor het toevoegen van nieuwe taken en bestaande bestanden markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="7abcd-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="7abcd-199">Opslaan en sluiten **index.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="7abcd-200">Hallo globale indeling wijzigen</span><span class="sxs-lookup"><span data-stu-id="7abcd-200">Modify hello global layout</span></span>
<span data-ttu-id="7abcd-201">Hallo **layout.jade** bestand in Hallo **weergaven** map is een algemene sjabloon voor andere **.jade** bestanden.</span><span class="sxs-lookup"><span data-stu-id="7abcd-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="7abcd-202">In deze stap wijzigt u deze toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign nice ogende web-app.</span><span class="sxs-lookup"><span data-stu-id="7abcd-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="7abcd-203">Downloaden en uitpakken van bestanden voor Hallo [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="7abcd-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="7abcd-204">Kopiëren Hallo **bootstrap.min.css** bestand van Hallo Bootstrap **css** map in Hallo **openbare/stylesheets** map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7abcd-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="7abcd-205">Van Hallo **weergaven** map, open **layout.jade** en vervang de volledige inhoud Hallo door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7abcd-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="7abcd-206">Een configuratiebestand maken</span><span class="sxs-lookup"><span data-stu-id="7abcd-206">Create a config file</span></span>
<span data-ttu-id="7abcd-207">Hallo-app lokaal toorun we je Azure Storage-referenties in een configuratiebestand plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="7abcd-208">Maak een bestand met de naam **config.json* * Hello JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="7abcd-209">Vervang **opslagaccountnaam** rekening met de naam van opslag Hallo Hallo u eerder hebt gemaakt en vervang **toegangssleutel voor opslag** met Hallo primaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7abcd-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="7abcd-210">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7abcd-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="7abcd-211">Sla dit bestand *hoger niveau van één map* dan Hallo **tasklist** map als volgt:</span><span class="sxs-lookup"><span data-stu-id="7abcd-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="7abcd-212">Hallo reden om dit te doen is tooavoid Hallo-configuratiebestand controleren in broncodebeheer, waar mogelijk komen openbare.</span><span class="sxs-lookup"><span data-stu-id="7abcd-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="7abcd-213">Wanneer we Hallo app tooAzure implementeert, gebruiken we omgevingsvariabelen in plaats van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="7abcd-214">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7abcd-214">Run hello application locally</span></span>
<span data-ttu-id="7abcd-215">tootest hello toepassing op uw lokale machine uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="7abcd-216">Wijzig vanaf de opdrachtregel Hallo, mappen toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="7abcd-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="7abcd-217">Gebruik Hallo opdracht toolaunch Hallo toepassing lokaal te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="7abcd-218">Open een webbrowser en navigeer toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="7abcd-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="7abcd-219">Een webpagina vergelijkbare toohello volgende voorbeeld wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7abcd-219">A web page similar toohello following example appears.</span></span>
   
    ![Een webpagina een leeg tasklist weergeven][node-table-finished]
4. <span data-ttu-id="7abcd-221">een nieuwe taakitem toocreate Voer een naam en categorie en klik op **Item toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="7abcd-222">een taak als voltooid, Controleer toomark **Complete** en klik op **taken bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Een afbeelding van Hallo nieuw item in de lijst Hallo van taken][node-table-list-items]

<span data-ttu-id="7abcd-224">Hoewel Hallo toepassing lokaal wordt uitgevoerd, wordt het opslaan van gegevens van Hallo in hello Azure Table-service.</span><span class="sxs-lookup"><span data-stu-id="7abcd-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="7abcd-225">Uw toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="7abcd-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="7abcd-226">Hallo stappen in deze sectie hello Azure-opdrachtregelprogramma's toocreate een nieuwe web-app in App Service gebruiken en gebruik vervolgens Git toodeploy uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7abcd-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="7abcd-227">tooperform deze stappen hebt u een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7abcd-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7abcd-228">Deze stappen kunnen ook worden uitgevoerd met behulp van Hallo [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7abcd-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7abcd-229">Zie [bouwen en implementeren van een Node.js-web-app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="7abcd-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="7abcd-230">Als dit Hallo eerste web-app die u hebt gemaakt, moet u deze toepassing hello Azure Portal toodeploy gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7abcd-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="7abcd-231">tooget gestart, installeer Hallo [Azure CLI] hiertoe de volgende opdracht uit vanaf de opdrachtregel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="7abcd-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="7abcd-232">Publicatie-instellingen importeren</span><span class="sxs-lookup"><span data-stu-id="7abcd-232">Import publishing settings</span></span>
<span data-ttu-id="7abcd-233">In deze stap downloadt u een bestand met gegevens over uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7abcd-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="7abcd-234">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7abcd-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="7abcd-235">Deze opdracht wordt gestart van een browser en toohello downloadpagina navigeert.</span><span class="sxs-lookup"><span data-stu-id="7abcd-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="7abcd-236">Als u wordt gevraagd, kunt u aanmelden met Hallo-account die is gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7abcd-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="7abcd-237">Hallo-bestand downloaden begint automatisch; Als dit niet het geval is, kunt u op Hallo begin van Hallo toomanually downloaden Hallo wisselbestand Hallo-koppeling.</span><span class="sxs-lookup"><span data-stu-id="7abcd-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="7abcd-238">Hallo bestands- en Opmerking Hallo bestandspad opslaan.</span><span class="sxs-lookup"><span data-stu-id="7abcd-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="7abcd-239">Voer Hallo opdracht tooimport Hallo-instellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="7abcd-240">Hallo pad en de naam van de door u gedownloade instellingenbestand publiceren in de vorige stap Hallo Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="7abcd-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="7abcd-241">Nadat het Hallo-instellingen worden geïmporteerd, verwijdert u Hallo bestand publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="7abcd-242">Het is niet meer nodig en gevoelige informatie met betrekking tot uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="7abcd-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="7abcd-243">Een App Service-web-app maken</span><span class="sxs-lookup"><span data-stu-id="7abcd-243">Create an App Service web app</span></span>
1. <span data-ttu-id="7abcd-244">Wijzig vanaf de opdrachtregel Hallo, mappen toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="7abcd-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="7abcd-245">Gebruik Hallo opdracht toocreate een nieuwe web-app te volgen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="7abcd-246">U wordt gevraagd voor Hallo web-app-naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="7abcd-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="7abcd-247">Geef een unieke naam en selecteer Hallo dezelfde geografische locatie bevinden als uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="7abcd-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="7abcd-248">Hallo `--git` parameter maakt u een Git-opslagplaats in Azure voor deze web-app.</span><span class="sxs-lookup"><span data-stu-id="7abcd-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="7abcd-249">Deze ook een Git-opslagplaats in de huidige map Hallo initialiseert als er geen bestaat en voegt een [Git remote] met de naam 'azure', die de gebruikte toopublish Hallo toepassing tooAzure is.</span><span class="sxs-lookup"><span data-stu-id="7abcd-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="7abcd-250">Ten slotte wordt het maken van een **web.config** bestand, dat instellingen die worden gebruikt door Azure toohost knooppunt toepassingen bevat.</span><span class="sxs-lookup"><span data-stu-id="7abcd-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="7abcd-251">Als u Hallo weglaat `--git` parameter, maar Hallo directory bevat een Git-opslagplaats, Hallo opdracht maakt nog steeds 'azure' hello afstand.</span><span class="sxs-lookup"><span data-stu-id="7abcd-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="7abcd-252">Zodra deze opdracht is voltooid, ziet u uitvoer vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="7abcd-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="7abcd-253">Houd er rekening mee dat Hallo regels die beginnen met **Website gemaakt op** Hallo-URL voor Hallo web-app bevat.</span><span class="sxs-lookup"><span data-stu-id="7abcd-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
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
   > <span data-ttu-id="7abcd-254">Als dit Hallo eerste App Service web-app voor uw abonnement, kunt u zich gebruiksaanwijzing toouse hello Azure Portal toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="7abcd-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="7abcd-255">Zie voor meer informatie [bouwen en implementeren van een Node.js-web-app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="7abcd-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="7abcd-256">De omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="7abcd-256">Set environment variables</span></span>
<span data-ttu-id="7abcd-257">In deze stap voegt u configuratie voor de omgeving variabelen tooyour web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="7abcd-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="7abcd-258">Voer vanaf de opdrachtregel Hallo Hallo volgende in:</span><span class="sxs-lookup"><span data-stu-id="7abcd-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="7abcd-259">Vervang  **<storage account name>**  rekening met de naam van opslag Hallo Hallo u eerder hebt gemaakt en vervang  **<storage access key>**  met Hallo primaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7abcd-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="7abcd-260">(Gebruik Hallo dezelfde waarden als Hallo config.json-bestand dat u eerder hebt gemaakt.)</span><span class="sxs-lookup"><span data-stu-id="7abcd-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="7abcd-261">U kunt ook omgevingsvariabelen instellen in Hallo [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="7abcd-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="7abcd-262">Hallo van web-app-blade geopend door te klikken op **Bladeren** > **Web-Apps** > de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7abcd-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="7abcd-263">Klik op de blade van uw web-app **alle instellingen** > **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="7abcd-264">Schuif omlaag toohello **appinstellingen** sectie en Hallo sleutel/waarde-paren toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="7abcd-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![App-instellingen](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="7abcd-266">Klik op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="7abcd-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="7abcd-267">Hallo toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="7abcd-267">Publish hello application</span></span>
<span data-ttu-id="7abcd-268">toopublish hello app Hallo code bestanden tooGit doorvoeren en vervolgens push tooazure/master.</span><span class="sxs-lookup"><span data-stu-id="7abcd-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="7abcd-269">Stel de implementatiereferenties van uw.</span><span class="sxs-lookup"><span data-stu-id="7abcd-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="7abcd-270">Toevoegen en uw toepassingsbestanden worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7abcd-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="7abcd-271">Push Hallo doorvoeren toohello App Service-web-app:</span><span class="sxs-lookup"><span data-stu-id="7abcd-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="7abcd-272">Gebruik **master** als Hallo doel vertakking.</span><span class="sxs-lookup"><span data-stu-id="7abcd-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="7abcd-273">Aan het einde van de Hallo Hallo-implementatie ziet u een instructie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7abcd-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="7abcd-274">Zodra Hallo push-bewerking is voltooid, bladeren toohello web app-URL die eerder geretourneerd door Hallo `azure create site` opdracht tooview uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7abcd-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7abcd-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7abcd-275">Next steps</span></span>
<span data-ttu-id="7abcd-276">Tijdens het Hallo-stappen in dit artikel wordt beschreven met behulp van Hallo Tabelservice toostore gegevens, kunt u ook gebruiken [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="7abcd-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7abcd-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7abcd-277">Additional resources</span></span>
<span data-ttu-id="7abcd-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="7abcd-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="7abcd-279">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="7abcd-279">What's changed</span></span>
* <span data-ttu-id="7abcd-280">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7abcd-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
