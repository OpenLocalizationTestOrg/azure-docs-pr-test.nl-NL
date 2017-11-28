---
title: een Node.js-web-app voor Azure Cosmos DB aaaBuild | Microsoft Docs
description: Voor deze zelfstudie behandelt hoe toouse Microsoft Azure Cosmos DB toostore en toegang tot gegevens van een Node.js Express-webtoepassing gehost op Azure Websites.
keywords: Toepassingsontwikkeling, zelfstudie, node.js, node.js-zelfstudie leren
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="f7a0a-104"><a name="_Toc395783175"></a>Een Node.js-webtoepassing bouwen met Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f7a0a-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7a0a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f7a0a-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f7a0a-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f7a0a-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f7a0a-107">Java</span><span class="sxs-lookup"><span data-stu-id="f7a0a-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f7a0a-108">Python</span><span class="sxs-lookup"><span data-stu-id="f7a0a-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f7a0a-109">Voor deze zelfstudie ziet u hoe toouse Azure Cosmos DB en DocumentDB API toostore en toegang tot gegevens van een Node.js Express-toepassing hello op Azure Websites gehost.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="f7a0a-110">U bouwt een eenvoudige webtoepassing voor taakbeheer, een taken-app, waarmee u taken kunt maken, ophalen en voltooien.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="f7a0a-111">Hallo-taken worden opgeslagen als JSON-documenten in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="f7a0a-112">Deze zelfstudie wordt u begeleid bij Hallo maken en implementeren van Hallo-app en wordt uitgelegd wat er gebeurt in elke codefragment.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Schermopname van het Hallo toepassing My Todo List die in deze zelfstudie hebt gemaakt](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="f7a0a-114">Geen tijd toocomplete Hallo zelfstudie hebben en kunnen alleen wilt tooget Hallo volledige oplossing?</span><span class="sxs-lookup"><span data-stu-id="f7a0a-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="f7a0a-115">Geen probleem, kunt u complete Voorbeeldoplossing Hallo van krijgen [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="f7a0a-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="f7a0a-116">Hallo lezen alleen [Leesmij](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) -bestand voor instructies over hoe toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="f7a0a-117"><a name="_Toc395783176"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="f7a0a-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="f7a0a-118">Voor deze zelfstudie wordt ervan uitgegaan dat u ervaring hebt met Node.js en Azure Websites</span><span class="sxs-lookup"><span data-stu-id="f7a0a-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="f7a0a-119">Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="f7a0a-120">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-120">An active Azure account.</span></span> <span data-ttu-id="f7a0a-121">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f7a0a-122">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="f7a0a-123">OF</span><span class="sxs-lookup"><span data-stu-id="f7a0a-123">OR</span></span>

   <span data-ttu-id="f7a0a-124">Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md) (alleen Windows).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="f7a0a-125">[Node.js][Node.js] versie v0.10.29 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="f7a0a-126">[Express generator](http://www.expressjs.com/starter/generator.html) (te installeren via `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="f7a0a-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="f7a0a-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="f7a0a-127">[Git][Git].</span></span>

## <span data-ttu-id="f7a0a-128"><a name="_Toc395637761"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="f7a0a-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f7a0a-129">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="f7a0a-130">Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: Maak een nieuwe Node.js-toepassing](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="f7a0a-131"><a name="_Toc395783178"></a>Stap 2: Maak een nieuwe Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="f7a0a-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="f7a0a-132">Nu gaan we een eenvoudige Hello World Node.js-project met Hallo meer toocreate [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="f7a0a-133">Open uw favoriete terminal, zoals Hallo Node.js-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="f7a0a-134">Navigeer toohello directory waarin u toostore Hallo nieuwe toepassing wilt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="f7a0a-135">Hallo express-generator toogenerate aangeroepen voor een nieuwe toepassing gebruiken **todo**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="f7a0a-136">Open de nieuwe map **todo** en installeer afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="f7a0a-137">Voer uw nieuwe toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="f7a0a-138">U kunt uw nieuwe toepassing weergeven door uw browser te navigeren[http://localhost: 3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Node.js leren - schermopname van de toepassing in een browservenster Hallo wereld Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="f7a0a-140">Vervolgens toostop toepassing hello, druk op CTRL + C in Hallo terminalvenster en klik op **y** tooterminate Hallo batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f7a0a-141"><a name="_Toc395783179"></a>Stap 3: Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="f7a0a-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="f7a0a-142">Hallo **package.json** bestand is een Hallo-bestanden die zijn gemaakt in de hoofdmap Hallo van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="f7a0a-143">Dit bestand bevat een lijst met aanvullende modules die u nodig hebt voor uw Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="f7a0a-144">Later, wanneer u deze toepassing tooAzure Websites implementeert, is dit bestand gebruikt toodetermine welke modules moeten toobe geïnstalleerd op Azure toosupport uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="f7a0a-145">Er moet nog steeds tooinstall twee pakketten voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="f7a0a-146">Terug in terminal hello, installeert u Hallo **asynchrone** module via npm.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="f7a0a-147">Hallo installeren **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="f7a0a-148">Dit is Hallo module waar alle hello Azure DB die Cosmos-magie plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="f7a0a-149">Een snelle controle van Hallo **package.json** bestand van de toepassing hello moet worden weergegeven Hallo aanvullende modules.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="f7a0a-150">Dit bestand wordt vertelt Azure welke pakketten toodownload en geïnstalleerd wanneer uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="f7a0a-151">Het bestand is vergelijkbaar Hallo in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-151">It should resemble hello example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="f7a0a-152">Hiermee wordt bij Node (en later bij Azure) aangegeven dat de toepassing afhankelijk is van deze aanvullende modules.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="f7a0a-153"><a name="_Toc395783180"></a>Stap 4: Hello Azure DB die Cosmos-service in een knooppunttoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="f7a0a-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="f7a0a-154">Dat zorgt voor alle Hallo eerste installatie en configuratie, nu gaan we get omlaag toowhy we, en dat sommige code met behulp van Azure DB die Cosmos toowrite is.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="f7a0a-155">Hallo-model maken</span><span class="sxs-lookup"><span data-stu-id="f7a0a-155">Create hello model</span></span>
1. <span data-ttu-id="f7a0a-156">In de projectmap hello, maakt u een nieuwe map met de naam **modellen** in Hallo dezelfde directory als Hallo package.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="f7a0a-157">In Hallo **modellen** directory, maak een nieuw bestand met de naam **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="f7a0a-158">Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="f7a0a-159">Hallo in dezelfde **modellen** directory, maakt u een ander nieuw bestand met de naam **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="f7a0a-160">Dit bestand bevat enkele handige, opnieuw bruikbare codefragmenten die we voor de hele toepassing zullen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="f7a0a-161">Kopiëren Hallo volgende code te**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="f7a0a-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="f7a0a-162">Opslaan en sluiten Hallo **docdbUtils.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="f7a0a-163">Aan begin Hallo Hallo **taskDao.js** bestand, het toevoegen van de volgende code tooreference Hallo Hallo **DocumentDBClient** en Hallo **docdbUtils.js** die eerder is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="f7a0a-164">Vervolgens moet u code toodefine toevoegen en Hallo taakobject exporteren.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="f7a0a-165">Dit is verantwoordelijk voor het taakobject geïnitialiseerd en het instellen van Hallo-Database en verzameling van documenten, zullen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="f7a0a-166">Voeg vervolgens Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="f7a0a-167">Opslaan en sluiten Hallo **taskDao.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="f7a0a-168">Hallo controller maken</span><span class="sxs-lookup"><span data-stu-id="f7a0a-168">Create hello controller</span></span>
1. <span data-ttu-id="f7a0a-169">In Hallo **routes** directory van uw project, maak een nieuw bestand met de naam **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="f7a0a-170">Hallo code te volgen toevoegen**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="f7a0a-171">Dit wordt geladen Hallo DocumentDBClient en async-modules die worden gebruikt door **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="f7a0a-172">Dit ook Hallo gedefinieerd **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** object eerder:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="f7a0a-173">Doorgaan met het toevoegen van toohello **tasklist.js** bestand door toe te voegen Hallo methoden te**showTasks, addTask**, en **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="f7a0a-174">Opslaan en sluiten Hallo **tasklist.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="f7a0a-175">Config.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7a0a-175">Add config.js</span></span>
1. <span data-ttu-id="f7a0a-176">Maak een nieuw bestand met de naam **config.js** in uw projectmap.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="f7a0a-177">Hallo te volgende toevoegen**config.js**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="f7a0a-178">Hiermee definieert u configuratie-instellingen en waarden die nodig zijn voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="f7a0a-179">In Hallo **config.js** -bestand, update Hallo waarden voor HOST en auth_key bij door met behulp van Hallo waarden gevonden in de blade van Hallo-sleutels van uw Azure DB die Cosmos-account op Hallo [Microsoft Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="f7a0a-180">Opslaan en sluiten Hallo **config.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="f7a0a-181">App.js wijzigen</span><span class="sxs-lookup"><span data-stu-id="f7a0a-181">Modify app.js</span></span>
1. <span data-ttu-id="f7a0a-182">Open in de projectmap Hallo Hallo **app.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="f7a0a-183">Dit bestand is gemaakt toen de Express-webtoepassing Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="f7a0a-184">Hallo na code toohello bovenaan toevoegen **app.js**</span><span class="sxs-lookup"><span data-stu-id="f7a0a-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="f7a0a-185">Deze code definieert Hallo config bestand toobe gebruikt en tooread waarden buiten dit bestand in sommige variabelen we binnenkort gebruiken verloopt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="f7a0a-186">Vervangen van de volgende twee regels in Hallo **app.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="f7a0a-187">Hello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-187">with hello following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="f7a0a-188">Deze regels definiëren een nieuw exemplaar van onze **TaskDao** object met een nieuwe verbinding tooAzure Cosmos-DB (met behulp van Hallo waarden lezen uit Hallo **config.js**), initialiseren Hallo taakobject en bindt de formulieracties toomethods op onze **TaskList** controller.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="f7a0a-189">Ten slotte opslaan en sluiten Hallo **app.js** -bestand, bijna klaar.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="f7a0a-190"><a name="_Toc395783181"></a>Stap 5: Een gebruikersinterface maken</span><span class="sxs-lookup"><span data-stu-id="f7a0a-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="f7a0a-191">Nu gaan we onze aandacht toobuilding Hallo-gebruikersinterface, zodat een gebruiker daadwerkelijk communiceren met de toepassing communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="f7a0a-192">Express-toepassing die is gemaakt, gebruikt Hallo **Jade** als Hallo weergave-engine.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="f7a0a-193">Voor meer informatie over Jade Raadpleeg te[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="f7a0a-194">Hallo **layout.jade** bestand in Hallo **weergaven** directory wordt gebruikt als een algemeen sjabloon voor andere **.jade** bestanden.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="f7a0a-195">In deze stap wijzigt u deze toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign een aantrekkelijk ogende website.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="f7a0a-196">Open Hallo **layout.jade** bestand gevonden in Hallo **weergaven** inhoud in de map en vervang de Hallo met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="f7a0a-197">Zodoende weet Hallo **Jade** engine toorender HTML-code voor onze toepassing en maakt een **blok** aangeroepen **inhoud** waarmee we Hallo lay-out voor onze inhoud kunt leveren pagina's.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="f7a0a-198">Sla het bestand **layout.jade** op en sluit het bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="f7a0a-199">Open nu Hallo **index.jade** bestand, Hallo weergave die wordt gebruikt door de toepassing en het Hallo-inhoud van Hallo bestand vervangen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
        extends layout
        block content
           h1 #{title}
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
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="f7a0a-200">Dit breidt lay-out en inhoud biedt voor Hallo **inhoud** tijdelijke aanduiding hebt gezien in Hallo **layout.jade** bestand.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="f7a0a-201">In deze lay-out hebben we twee HTML-formulieren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="f7a0a-202">Hallo eerste formulier bevat een tabel voor onze gegevens en een knop waarmee we tooupdate items door boeken te**/completetask** methode van de controller.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="f7a0a-203">Hallo tweede formulier bevat twee invoervelden en een knop waarmee een nieuw item toocreate door boeken te**/addtask** methode van de controller.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="f7a0a-204">Dit is alles wat we nodig hebben om onze toepassing toowork.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="f7a0a-205"><a name="_Toc395783181"></a>Stap 6: De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f7a0a-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="f7a0a-206">tootest hello toepassing op uw lokale machine uitgevoerd `npm start` in terminal toostart uw toepassing hello en vernieuw vervolgens de [http://localhost: 3000](http://localhost:3000) browserpagina.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="f7a0a-207">Hallo pagina ziet er nu als Hallo in onderstaande afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f7a0a-207">hello page should now look like hello image below:</span></span>
   
    ![Schermafbeelding van de toepassing MyTodo List in een browservenster Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="f7a0a-209">Als u een foutbericht over Hallo streepje in Hallo layout.jade hello index.jade bestand of ontvangt, zorg ervoor dat de eerste twee regels Hallo in beide bestanden links gerechtvaardigd is, zonder spaties.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="f7a0a-210">Als er spaties vóór de eerste twee regels hello, verwijder ze, beide bestanden opslaan en vernieuw het browservenster.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="f7a0a-211">Hallo-Item, itemnaam en categorie velden tooenter een nieuwe taak en klik vervolgens op **Item toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="f7a0a-212">Hiermee maakt u in Azure Cosmos DB een document met deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="f7a0a-213">Hallo pagina moet bijwerken toodisplay Hallo nieuw item in de takenlijst Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Schermopname van de toepassing hello met een nieuw item in de takenlijst Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="f7a0a-215">toocomplete een taak Hallo gewoon selectievakje van in de kolom voor Hallo voltooid en klik vervolgens op **taken bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="f7a0a-216">Deze updates Hallo al gemaakte document.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="f7a0a-217">toostop hello toepassing, druk op CTRL + C in Hallo terminalvenster en klik vervolgens op **Y** tooterminate Hallo batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f7a0a-218"><a name="_Toc395783182"></a>Stap 7: Uw toepassing ontwikkelen project tooAzure Websites implementeren</span><span class="sxs-lookup"><span data-stu-id="f7a0a-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="f7a0a-219">Als dit nog niet hebt gedaan, schakelt u een git-opslagplaats voor uw Azure-website in.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="f7a0a-220">U vindt instructies over het toodo dit op Hallo [lokale Git-implementatie tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="f7a0a-221">Voeg uw Azure-website toe als een externe git.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="f7a0a-222">Door te pushen toohello externe implementeren.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="f7a0a-223">Binnen een paar seconden zal git publicatie van uw webtoepassing voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!</span><span class="sxs-lookup"><span data-stu-id="f7a0a-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="f7a0a-224">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-224">Congratulations!</span></span> <span data-ttu-id="f7a0a-225">U hebt zojuist uw eerste Node.js Express-webtoepassing met behulp van Azure DB die Cosmos gebouwd en gepubliceerd tooAzure Websites.</span><span class="sxs-lookup"><span data-stu-id="f7a0a-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="f7a0a-226">Als u wilt dat toodownload of raadpleegt u de volledige referentietoepassing toohello voor deze zelfstudie, kan worden gedownload van [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="f7a0a-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="f7a0a-227"><a name="_Toc395637775"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7a0a-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="f7a0a-228">Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f7a0a-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="f7a0a-229">Zie [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) (Prestaties en schaal testen met Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="f7a0a-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="f7a0a-230">Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f7a0a-231">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f7a0a-232">Hallo verkennen [Azure Cosmos DB documentatie](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f7a0a-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

