---
title: aaaUse MongoDB APIs toobuild een Azure DB die Cosmos-app | Microsoft Docs
description: Een zelfstudie waarmee u maakt een online-database met behulp van hello Azure Cosmos DB API's voor MongoDB.
keywords: Voorbeelden van mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="3bc02-104">Een Cosmos Azure DB bouwen:-API voor MongoDB-app met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="3bc02-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bc02-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3bc02-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="3bc02-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3bc02-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="3bc02-107">Java</span><span class="sxs-lookup"><span data-stu-id="3bc02-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="3bc02-108">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="3bc02-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="3bc02-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="3bc02-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="3bc02-110">C++</span><span class="sxs-lookup"><span data-stu-id="3bc02-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="3bc02-111">In dit voorbeeld ziet u hoe een Cosmos Azure DB toobuild:-API voor MongoDB-console-app met behulp van Node.js.</span><span class="sxs-lookup"><span data-stu-id="3bc02-111">This example shows you how toobuild an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="3bc02-112">toouse in dit voorbeeld moet:</span><span class="sxs-lookup"><span data-stu-id="3bc02-112">toouse this example, you must:</span></span>

* <span data-ttu-id="3bc02-113">[Maak](create-mongodb-dotnet.md#create-account) een Cosmos Azure DB: API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="3bc02-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="3bc02-114">Ophalen van uw MongoDB [verbindingsreeks](connect-mongodb-account.md) informatie.</span><span class="sxs-lookup"><span data-stu-id="3bc02-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-hello-app"></a><span data-ttu-id="3bc02-115">Hallo-app maken</span><span class="sxs-lookup"><span data-stu-id="3bc02-115">Create hello app</span></span>

1. <span data-ttu-id="3bc02-116">Maak een *app.js* bestand en kopiëren en plakken Hallo-code hieronder.</span><span class="sxs-lookup"><span data-stu-id="3bc02-116">Create a *app.js* file and copy & paste hello code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into hello families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="3bc02-117">Wijzigen van de volgende variabelen in Hallo Hallo *app.js* bestand per uw accountinstellingen (meer informatie hoe toofind uw [verbindingsreeks](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="3bc02-117">Modify hello following variables in hello *app.js* file per your account settings (Learn how toofind your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="3bc02-118">Open uw favoriete terminal, voert u **npm Installeer mongodb--opslaan**, Voer uw app met **knooppunt app.js**</span><span class="sxs-lookup"><span data-stu-id="3bc02-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bc02-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bc02-119">Next steps</span></span>
* <span data-ttu-id="3bc02-120">Meer informatie over hoe te[MongoChef gebruiken](mongodb-mongochef.md) met uw Azure-Cosmos-DB: API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="3bc02-120">Learn how too[use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
