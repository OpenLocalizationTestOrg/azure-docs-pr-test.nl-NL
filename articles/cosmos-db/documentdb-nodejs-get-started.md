---
title: zelfstudie voor DocumentDB-API voor Azure Cosmos DB Hallo aaaNode.js | Microsoft Docs
description: Een Node.js-zelfstudie waarmee een Cosmos-database met Hallo DocumentDB-API maakt.
keywords: node.js zelfstudie, knooppuntdatabase
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="64be4-104">Node.js-zelfstudie: gebruik Hallo DocumentDB API in Azure Cosmos DB toocreate een Node.js-consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="64be4-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64be4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="64be4-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="64be4-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="64be4-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="64be4-107">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="64be4-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="64be4-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="64be4-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="64be4-109">Java</span><span class="sxs-lookup"><span data-stu-id="64be4-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="64be4-110">C++</span><span class="sxs-lookup"><span data-stu-id="64be4-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="64be4-111">Welkom toohello Node.js-zelfstudie voor hello Azure Cosmos DB Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="64be4-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="64be4-112">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="64be4-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="64be4-113">De volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="64be4-113">We'll cover:</span></span>

* <span data-ttu-id="64be4-114">Maken en te verbinden tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="64be4-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="64be4-115">Uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="64be4-115">Setting up your application</span></span>
* <span data-ttu-id="64be4-116">Een knooppuntdatabase maken</span><span class="sxs-lookup"><span data-stu-id="64be4-116">Creating a node database</span></span>
* <span data-ttu-id="64be4-117">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="64be4-117">Creating a collection</span></span>
* <span data-ttu-id="64be4-118">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="64be4-118">Creating JSON documents</span></span>
* <span data-ttu-id="64be4-119">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="64be4-119">Querying hello collection</span></span>
* <span data-ttu-id="64be4-120">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="64be4-120">Replacing a document</span></span>
* <span data-ttu-id="64be4-121">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="64be4-121">Deleting a document</span></span>
* <span data-ttu-id="64be4-122">Hallo-knooppuntdatabase verwijderen</span><span class="sxs-lookup"><span data-stu-id="64be4-122">Deleting hello node database</span></span>

<span data-ttu-id="64be4-123">Hebt u geen tijd?</span><span class="sxs-lookup"><span data-stu-id="64be4-123">Don't have time?</span></span> <span data-ttu-id="64be4-124">Geen probleem.</span><span class="sxs-lookup"><span data-stu-id="64be4-124">Don't worry!</span></span> <span data-ttu-id="64be4-125">Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="64be4-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="64be4-126">Zie [ophalen van de volledige oplossing Hallo](#GetSolution) voor beknopte instructies.</span><span class="sxs-lookup"><span data-stu-id="64be4-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="64be4-127">Nadat u Hallo Node.js-zelfstudie hebt voltooid, stemknoppen Controleer gebruik Hallo Hallo boven en onder aan deze pagina toogive ons feedback.</span><span class="sxs-lookup"><span data-stu-id="64be4-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="64be4-128">Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="64be4-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="64be4-129">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="64be4-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="64be4-130">Vereisten voor Hallo Node.js-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="64be4-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="64be4-131">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="64be4-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="64be4-132">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="64be4-132">An active Azure account.</span></span> <span data-ttu-id="64be4-133">Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64be4-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="64be4-134">U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="64be4-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="64be4-135">[Node.js](https://nodejs.org/) versie v0.10.29 of hoger.</span><span class="sxs-lookup"><span data-stu-id="64be4-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="64be4-136">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="64be4-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="64be4-137">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="64be4-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="64be4-138">Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Node.js-toepassing instellen](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="64be4-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="64be4-139">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Node.js-toepassing instellen](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="64be4-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="64be4-140"><a id="SetupNode"></a>Stap 2: Uw Node.js-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="64be4-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="64be4-141">Open uw favoriete terminal.</span><span class="sxs-lookup"><span data-stu-id="64be4-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="64be4-142">Zoek Hallo map of directory waarin u toosave wilt dat uw Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="64be4-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="64be4-143">Maak twee lege JavaScript-bestanden met Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="64be4-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="64be4-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="64be4-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="64be4-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="64be4-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="64be4-146">Installeer Hallo documentdb-module via npm.</span><span class="sxs-lookup"><span data-stu-id="64be4-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="64be4-147">Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="64be4-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="64be4-148">Goed gedaan.</span><span class="sxs-lookup"><span data-stu-id="64be4-148">Great!</span></span> <span data-ttu-id="64be4-149">U bent klaar met het instellen. U gaat nu aan de slag met het schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="64be4-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="64be4-150"><a id="Config"></a>Stap 3: de configuratie van de app instellen</span><span class="sxs-lookup"><span data-stu-id="64be4-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="64be4-151">Open ```config.js``` in uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="64be4-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="64be4-152">Vervolgens, kopiëren en plakken Hallo onderstaande codefragment en eigenschappen instellen ```config.endpoint``` en ```config.primaryKey``` tooyour Azure Cosmos DB eindpunt-uri en primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="64be4-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="64be4-153">Deze beide configuraties vindt u in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64be4-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Node.js-zelfstudie - schermopname van het Azure-portal, met een account Azure Cosmos DB met actieve hub Hallo Hallo gemarkeerd, knop Hallo-sleutels gemarkeerd op hello Azure DB die Cosmos-accountblade en Hallo URI, primaire sleutel waarden en secundaire sleutel gemarkeerd op Hallo De blade sleutels - knooppuntdatabase][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="64be4-155">Kopieer en plak Hallo ```database id```, ```collection id```, en ```JSON documents``` tooyour ```config``` object waarin u instellen onder uw ```config.endpoint``` en ```config.authKey``` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="64be4-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="64be4-156">Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) in plaats van Hallo documentdefinities toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="64be4-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="64be4-157">Hallo-database, de verzameling en de documentdefinities zal fungeren als uw Azure-Cosmos-DB ```database id```, ```collection id```, documentgegevens.</span><span class="sxs-lookup"><span data-stu-id="64be4-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="64be4-158">Ten slotte exporteert uw ```config``` object, zodat u ernaar binnen Hallo verwijzen kunt ```app.js``` bestand.</span><span class="sxs-lookup"><span data-stu-id="64be4-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="64be4-159"><a id="Connect"></a>Stap 4: Tooan Azure DB die Cosmos-account koppelen</span><span class="sxs-lookup"><span data-stu-id="64be4-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="64be4-160">Open uw lege ```app.js``` bestand in de teksteditor Hallo.</span><span class="sxs-lookup"><span data-stu-id="64be4-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="64be4-161">Kopieer en plak de code Hallo hieronder tooimport hello ```documentdb``` module en de zojuist gemaakte ```config``` module.</span><span class="sxs-lookup"><span data-stu-id="64be4-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="64be4-162">Kopieer en plak Hallo code toouse Hallo eerder opgeslagen ```config.endpoint``` en ```config.primaryKey``` toocreate een nieuwe DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="64be4-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="64be4-163">Nu dat u Hallo code tooinitialize hello Azure Cosmos DB client hebt, gaat u nu kijken werken met Azure DB die Cosmos-resources.</span><span class="sxs-lookup"><span data-stu-id="64be4-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="64be4-164">Stap 5: een knooppuntdatabase maken</span><span class="sxs-lookup"><span data-stu-id="64be4-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="64be4-165">Kopieer en plak Hallo-code hieronder tooset Hallo HTTP-status voor niet gevonden, Hallo database-url en Hallo verzameling url.</span><span class="sxs-lookup"><span data-stu-id="64be4-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="64be4-166">Deze URL's zijn hoe hello Azure Cosmos DB client vindt Hallo juiste database en verzameling.</span><span class="sxs-lookup"><span data-stu-id="64be4-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="64be4-167">Een [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="64be4-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="64be4-168">Een database is Hallo logische container voor documentopslag, gepartitioneerd in verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="64be4-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="64be4-169">Kopieer en plak Hallo **getDatabase** functie voor het maken van de nieuwe database in Hallo app.js bestand Hello ```id``` opgegeven in Hallo ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="64be4-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="64be4-170">Hallo functie wordt gecontroleerd of database Hallo Hello dezelfde ```FamilyRegistry``` -id al bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="64be4-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="64be4-171">Als er al een database met dezelfde id bestaat, wordt die database geretourneerd en wordt er geen nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="64be4-172">Code kopiëren en plakken Hallo onderstaande waarin het instellen van Hallo **getDatabase** tooadd Hallo Help-functie werken **sluiten** die worden afsluiten het Hallo-bericht en Hallo aanroep te afgedrukt**getDatabase** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-173">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-174">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-174">Congratulations!</span></span> <span data-ttu-id="64be4-175">U hebt een Azure Cosmos DB-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="64be4-176"><a id="CreateColl"></a>Stap 6: een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="64be4-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="64be4-177">Met **CreateDocumentCollectionAsync** maakt u een nieuwe verzameling, wat gevolgen heeft voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="64be4-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="64be4-178">Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="64be4-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="64be4-179">Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="64be4-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="64be4-180">Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="64be4-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="64be4-181">Kopieer en plak Hallo **getCollection** functie onder Hallo **getDatabase** werken in Hallo app.js bestand toocreate uw nieuwe verzameling Hello ```id``` opgegeven in Hallo ```config```object.</span><span class="sxs-lookup"><span data-stu-id="64be4-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="64be4-182">Er wordt opnieuw gecontroleerd toomake ervoor dat een verzameling met dezelfde Hallo ```FamilyCollection``` -id al bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="64be4-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="64be4-183">Als er al een verzameling met dezelfde id bestaat, wordt die verzameling geretourneerd en wordt er geen nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="64be4-184">Code kopiëren en plakken Hallo onder Hallo aanroep te**getDatabase** tooexecute hello **getCollection** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-185">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-186">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-186">Congratulations!</span></span> <span data-ttu-id="64be4-187">U hebt een Azure DB die Cosmos-verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="64be4-188"><a id="CreateDoc"></a>Stap 7: een document maken</span><span class="sxs-lookup"><span data-stu-id="64be4-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="64be4-189">Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="64be4-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="64be4-190">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="64be4-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="64be4-191">U kunt nu een document invoegen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="64be4-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="64be4-192">Kopieer en plak Hallo **getFamilyDocument** functie onder Hallo **getCollection** functie voor het maken van Hallo-documenten met de Hallo JSON-gegevens opgeslagen in Hallo ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="64be4-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="64be4-193">Er wordt opnieuw gecontroleerd toomake ervoor dat een document met Hallo dezelfde id nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="64be4-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="64be4-194">Code kopiëren en plakken Hallo onder Hallo aanroep te**getCollection** tooexecute hello **getFamilyDocument** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-195">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-196">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-196">Congratulations!</span></span> <span data-ttu-id="64be4-197">U hebt een Azure DB die Cosmos-document gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js-zelfstudie: Diagram ter illustratie van Hallo hiërarchische relatie tussen Hallo-account, Hallo database Hallo verzameling en Hallo documenten - knooppuntdatabase](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="64be4-199"><a id="Query"></a>Stap 8: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="64be4-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="64be4-200">Azure Cosmos DB biedt ondersteuning voor [uitgebreide query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="64be4-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="64be4-201">Hallo ziet volgende voorbeeldcode u een query die u op Hallo documenten in uw verzameling uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="64be4-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="64be4-202">Kopieer en plak Hallo **queryCollection** functie onder Hallo **getFamilyDocument** functie in Hallo app.js-bestand.</span><span class="sxs-lookup"><span data-stu-id="64be4-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="64be4-203">Azure Cosmos DB ondersteunt SQL-achtige query's, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64be4-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="64be4-204">Bekijk voor meer informatie over het bouwen van complexe query's Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo) en Hallo [querydocumentatie](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="64be4-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="64be4-205">Hallo volgende diagram ziet u hoe u hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64be4-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Node.js-zelfstudie: Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query - knooppuntdatabase](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="64be4-207">Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn.</span><span class="sxs-lookup"><span data-stu-id="64be4-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="64be4-208">Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam.</span><span class="sxs-lookup"><span data-stu-id="64be4-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="64be4-209">Azure Cosmos DB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.</span><span class="sxs-lookup"><span data-stu-id="64be4-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="64be4-210">Code kopiëren en plakken Hallo onder Hallo aanroep te**getFamilyDocument** tooexecute hello **queryCollection** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-211">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-212">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-212">Congratulations!</span></span> <span data-ttu-id="64be4-213">U hebt een query uitgevoerd op Azure Cosmos DB-documenten.</span><span class="sxs-lookup"><span data-stu-id="64be4-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="64be4-214"><a id="ReplaceDocument"></a>Stap 9: een document vervangen</span><span class="sxs-lookup"><span data-stu-id="64be4-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="64be4-215">Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="64be4-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="64be4-216">Kopieer en plak Hallo **replaceFamilyDocument** functie onder Hallo **queryCollection** functie in Hallo app.js-bestand.</span><span class="sxs-lookup"><span data-stu-id="64be4-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="64be4-217">Code kopiëren en plakken Hallo onder Hallo aanroep te**queryCollection** tooexecute hello **replaceDocument** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="64be4-218">Hallo code toocall ook toe te voegen **queryCollection** opnieuw tooverify dat document Hallo is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="64be4-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-219">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-220">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-220">Congratulations!</span></span> <span data-ttu-id="64be4-221">U hebt een Azure Cosmos DB-document vervangen.</span><span class="sxs-lookup"><span data-stu-id="64be4-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="64be4-222"><a id="DeleteDocument"></a>Stap 10: een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="64be4-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="64be4-223">Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="64be4-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="64be4-224">Kopieer en plak Hallo **deleteFamilyDocument** functie onder Hallo **replaceFamilyDocument** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="64be4-225">Code kopiëren en plakken Hallo hieronder Hallo aanroep toohello tweede **queryCollection** tooexecute hello **deleteDocument** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-226">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-227">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-227">Congratulations!</span></span> <span data-ttu-id="64be4-228">U hebt een Azure Cosmos DB-document verwijderd.</span><span class="sxs-lookup"><span data-stu-id="64be4-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="64be4-229"><a id="DeleteDatabase"></a>Stap 11: Hallo-knooppuntdatabase verwijderen</span><span class="sxs-lookup"><span data-stu-id="64be4-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="64be4-230">Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).</span><span class="sxs-lookup"><span data-stu-id="64be4-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="64be4-231">Kopieer en plak Hallo **opschonen** functie onder Hallo **deleteFamilyDocument** functioneren tooremove Hallo database en alle onderliggende resources van Hallo.</span><span class="sxs-lookup"><span data-stu-id="64be4-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="64be4-232">Code kopiëren en plakken Hallo onder Hallo aanroep te**deleteFamilyDocument** tooexecute hello **opschonen** functie.</span><span class="sxs-lookup"><span data-stu-id="64be4-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="64be4-233"><a id="Run"></a>Stap 12: uw Note.js-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64be4-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="64be4-234">Helemaal er Hallo volgorde voor het aanroepen van uw functies als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="64be4-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="64be4-235">Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="64be4-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="64be4-236">U ziet de uitvoer Hallo van uw getstarted-app.</span><span class="sxs-lookup"><span data-stu-id="64be4-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="64be4-237">Hallo-uitvoer moet overeenkomen met de onderstaande Hallo voorbeeldtekst.</span><span class="sxs-lookup"><span data-stu-id="64be4-237">hello output should match hello example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

<span data-ttu-id="64be4-238">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="64be4-238">Congratulations!</span></span> <span data-ttu-id="64be4-239">U hebt gemaakt dat u Hallo Node.js-zelfstudie hebt voltooid en u hebt uw eerste Azure DB die Cosmos-consoletoepassing!</span><span class="sxs-lookup"><span data-stu-id="64be4-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="64be4-240"><a id="GetSolution"></a>Hallo volledige Node.js-zelfstudieoplossing ophalen</span><span class="sxs-lookup"><span data-stu-id="64be4-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="64be4-241">Als u geen tijd toocomplete Hallo stappen in deze zelfstudie of gewoon wilt toodownload Hallo code hebt, kunt u het krijgen van [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="64be4-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="64be4-242">toorun hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="64be4-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="64be4-243">[Azure Cosmos DB-account][create-account].</span><span class="sxs-lookup"><span data-stu-id="64be4-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="64be4-244">Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) oplossing is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="64be4-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="64be4-245">Hallo installeren **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="64be4-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="64be4-246">Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="64be4-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="64be4-247">Vervolgens gaat u naar Hallo ```config.js``` bestand, Hallo update de waarden config.endpoint en config.authKey zoals beschreven in [stap 3: de configuraties van uw app instellen](#Config).</span><span class="sxs-lookup"><span data-stu-id="64be4-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="64be4-248">Ga vervolgens in de terminal naar uw ```app.js``` -bestand en voert u de opdracht Hallo: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="64be4-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="64be4-249">Dat is alles, bouw nu de oplossing. Succes!</span><span class="sxs-lookup"><span data-stu-id="64be4-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="64be4-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64be4-250">Next steps</span></span>
* <span data-ttu-id="64be4-251">Wilt u een complexer Node.js-voorbeeld?</span><span class="sxs-lookup"><span data-stu-id="64be4-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="64be4-252">Zie [Een Node.js-webtoepassing bouwen met Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="64be4-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="64be4-253">Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="64be4-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="64be4-254">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="64be4-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="64be4-255">Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="64be4-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
