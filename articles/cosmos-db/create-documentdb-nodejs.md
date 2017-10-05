---
title: 'Azure Cosmos DB: een toepassing bouwen met Node.js en de DocumentDB API | Microsoft Docs'
description: "Biedt een voorbeeld van Node.js-code dat u kunt gebruiken om verbinding te maken met de DocumentDB API van Azure Cosmos DB en er query’s op uit te voeren"
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
ms.openlocfilehash: 26e3548bf6aacbc60c4c46a5cc88749ca14cec01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="7385e-103">Azure Cosmos DB: een DocumentDB API-app bouwen met Node.js en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7385e-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and the Azure portal</span></span>

<span data-ttu-id="7385e-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7385e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7385e-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7385e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7385e-106">Deze Quick Start laat zien hoe u een Azure Cosmos DB-account, een documentdatabase en een verzameling kunt maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7385e-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="7385e-107">Vervolgens ontwikkelt u een console-app die is gebouwd op de [DocumentDB Node.js-API](documentdb-sdk-node.md) en voert u deze uit.</span><span class="sxs-lookup"><span data-stu-id="7385e-107">You then build and run a console app built on the [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7385e-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7385e-108">Prerequisites</span></span>

* <span data-ttu-id="7385e-109">Voordat u met dit voorbeeld aan de slag gaat, moet u aan de volgende vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="7385e-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="7385e-110">[Node.js](https://nodejs.org/en/) versie v0.10.29 of hoger</span><span class="sxs-lookup"><span data-stu-id="7385e-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="7385e-111">Git</span><span class="sxs-lookup"><span data-stu-id="7385e-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7385e-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="7385e-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7385e-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="7385e-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="7385e-114">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="7385e-114">Clone the sample application</span></span>

<span data-ttu-id="7385e-115">We gaan nu een DocumentDB API-app klonen vanuit GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7385e-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="7385e-116">U zult zien hoe gemakkelijk het is om op een programmatische manier met gegevens te werken.</span><span class="sxs-lookup"><span data-stu-id="7385e-116">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="7385e-117">Open een git-terminalvenster zoals git bash en `CD` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="7385e-117">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="7385e-118">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="7385e-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="7385e-119">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="7385e-119">Review the code</span></span>

<span data-ttu-id="7385e-120">Laten we eens kijken wat er precies gebeurt in de app.</span><span class="sxs-lookup"><span data-stu-id="7385e-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="7385e-121">Open het bestand `app.js` en u zult zien dat deze regels code de Azure Cosmos DB-resources maken.</span><span class="sxs-lookup"><span data-stu-id="7385e-121">Open the `app.js` file and you find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="7385e-122">De `documentClient` is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="7385e-122">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="7385e-123">Er wordt een nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7385e-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7385e-124">Er wordt een nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7385e-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7385e-125">Er wordt een aantal documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7385e-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7385e-126">Er wordt een SQL-query via JSON uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7385e-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="7385e-127">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="7385e-127">Update your connection string</span></span>

<span data-ttu-id="7385e-128">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="7385e-128">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="7385e-129">Klik in [Azure Portal](http://portal.azure.com/), in uw Azure Cosmos DB-account, in het linker navigatiegedeelte op **Sleutels** en klik vervolgens op **Sleutels voor lezen/schrijven**.</span><span class="sxs-lookup"><span data-stu-id="7385e-129">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7385e-130">In de volgende stap gebruikt u de kopieerknoppen aan de rechterkant van het scherm om de URI en primaire sleutel in het bestand `config.js` te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7385e-130">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![Een toegangssleutel bekijken en kopiëren in Azure Portal, blade Sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="7385e-132">Open het bestand `config.js`.</span><span class="sxs-lookup"><span data-stu-id="7385e-132">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="7385e-133">Kopieer uw URI-waarde vanaf de portal (met de kopieerknop) en geef deze als waarde aan de eindpuntsleutel in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="7385e-133">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="7385e-134">Kopieer vervolgens de waarde van uw PRIMAIRE SLEUTEL vanaf de portal en geef deze als waarde aan de `config.primaryKey` in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="7385e-134">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="7385e-135">U hebt uw app nu bijgewerkt met alle informatie die nodig is voor de communicatie met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7385e-135">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="7385e-136">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7385e-136">Run the app</span></span>
1. <span data-ttu-id="7385e-137">Voer `npm install` uit op een terminal zodat de vereiste npm-modules worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7385e-137">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="7385e-138">Voer `node app.js` uit op een terminal om uw knooppunttoepassing te starten.</span><span class="sxs-lookup"><span data-stu-id="7385e-138">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="7385e-139">U kunt nu teruggaan naar Data Explorer en deze nieuwe gegevens bekijken, wijzigen, een query erop uitvoeren of er iets anders mee doen.</span><span class="sxs-lookup"><span data-stu-id="7385e-139">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="7385e-140">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7385e-140">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7385e-141">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="7385e-141">Clean up resources</span></span>

<span data-ttu-id="7385e-142">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="7385e-142">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="7385e-143">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7385e-143">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="7385e-144">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7385e-144">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7385e-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7385e-145">Next steps</span></span>

<span data-ttu-id="7385e-146">In deze Quick Start hebt u geleerd hoe u een Azure Cosmos DB-account kunt maken, hoe u een verzameling kunt maken met Data Explorer en hebt u een app uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7385e-146">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="7385e-147">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="7385e-147">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7385e-148">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7385e-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


