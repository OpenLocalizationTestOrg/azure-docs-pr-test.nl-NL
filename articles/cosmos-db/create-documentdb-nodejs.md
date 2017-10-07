---
title: 'Azure Cosmos DB: Bouwen van een app met behulp van Node.js en DocumentDB API Hallo | Microsoft Docs'
description: Geeft het voorbeeld van een Node.js-code kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="11039-103">Azure Cosmos DB: Een DocumentDB-API-app met behulp van Node.js bouwen en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="11039-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="11039-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="11039-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="11039-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="11039-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="11039-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="11039-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="11039-107">U vervolgens bouwen en uitvoeren van een console-app die is gebouwd op Hallo [DocumentDB Node.js-API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="11039-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11039-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="11039-108">Prerequisites</span></span>

* <span data-ttu-id="11039-109">Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="11039-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="11039-110">[Node.js](https://nodejs.org/en/) versie v0.10.29 of hoger</span><span class="sxs-lookup"><span data-stu-id="11039-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="11039-111">Git</span><span class="sxs-lookup"><span data-stu-id="11039-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="11039-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="11039-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="11039-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="11039-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="11039-114">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="11039-114">Clone hello sample application</span></span>

<span data-ttu-id="11039-115">Nu we de kloon een DocumentDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="11039-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="11039-116">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="11039-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="11039-117">Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="11039-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="11039-118">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11039-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="11039-119">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="11039-119">Review hello code</span></span>

<span data-ttu-id="11039-120">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="11039-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="11039-121">Open Hallo `app.js` bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="11039-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="11039-122">Hallo `documentClient` is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="11039-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="11039-123">Er wordt een nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11039-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="11039-124">Er wordt een nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11039-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="11039-125">Er wordt een aantal documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11039-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="11039-126">Er wordt een SQL-query via JSON uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11039-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
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
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="11039-127">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="11039-127">Update your connection string</span></span>

<span data-ttu-id="11039-128">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="11039-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="11039-129">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="11039-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="11039-130">U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `config.js` bestand in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="11039-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="11039-132">In Open Hallo `config.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="11039-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="11039-133">Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="11039-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="11039-134">Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en deze waarde Hallo Hallo `config.primaryKey` in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="11039-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="11039-135">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="11039-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="11039-136">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="11039-136">Run hello app</span></span>
1. <span data-ttu-id="11039-137">Voer `npm install` vereist in een terminal tooinstall npm-modules</span><span class="sxs-lookup"><span data-stu-id="11039-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="11039-138">Voer `node app.js` in een terminal toostart uw knooppunttoepassing.</span><span class="sxs-lookup"><span data-stu-id="11039-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="11039-139">U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met deze nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="11039-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="11039-140">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="11039-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="11039-141">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="11039-141">Clean up resources</span></span>

<span data-ttu-id="11039-142">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11039-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="11039-143">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11039-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="11039-144">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="11039-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11039-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11039-145">Next steps</span></span>

<span data-ttu-id="11039-146">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een app.</span><span class="sxs-lookup"><span data-stu-id="11039-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="11039-147">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="11039-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="11039-148">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="11039-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


