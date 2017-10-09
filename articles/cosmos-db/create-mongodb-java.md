---
title: 'Azure Cosmos DB: Een met behulp van Java-consoletoepassing bouwen en Hallo MongoDB-API | Microsoft Docs'
description: Geeft het voorbeeld van een Java-code kunt u tooconnect tooand query hello Azure Cosmos DB MongoDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="58b2d-103">Azure Cosmos DB: Bouwen van een console-app van de MongoDB-API met behulp van Java en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="58b2d-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="58b2d-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58b2d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="58b2d-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="58b2d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="58b2d-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="58b2d-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="58b2d-107">U moet vervolgens bouwen en implementeren van een console-app die is gebouwd op Hallo [MongoDB Java stuurprogramma](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="58b2d-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="58b2d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="58b2d-108">Prerequisites</span></span>

* <span data-ttu-id="58b2d-109">Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="58b2d-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="58b2d-110">JDK 1.7+ (voer `apt-get install default-jdk` uit als u niet over JDK beschikt)</span><span class="sxs-lookup"><span data-stu-id="58b2d-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="58b2d-111">Maven (voer `apt-get install maven` uit als u niet over Maven beschikt)</span><span class="sxs-lookup"><span data-stu-id="58b2d-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="58b2d-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="58b2d-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="58b2d-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="58b2d-113">Add a collection</span></span>

<span data-ttu-id="58b2d-114">Geef uw nieuwe database de naam **db**, en uw nieuwe verzameling **verz**.</span><span class="sxs-lookup"><span data-stu-id="58b2d-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="58b2d-115">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="58b2d-115">Clone hello sample application</span></span>

<span data-ttu-id="58b2d-116">Nu we de kloon een MongoDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="58b2d-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="58b2d-117">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="58b2d-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="58b2d-118">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="58b2d-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="58b2d-119">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58b2d-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="58b2d-120">Open het oplossingsbestand Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58b2d-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="58b2d-121">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="58b2d-121">Review hello code</span></span>

<span data-ttu-id="58b2d-122">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="58b2d-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="58b2d-123">Open Hallo `Program.cs` bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="58b2d-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="58b2d-124">Hallo DocumentClient is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="58b2d-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="58b2d-125">Er wordt een nieuwe database en verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58b2d-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="58b2d-126">Een aantal documenten wordt ingevoegd met behulp van `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="58b2d-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="58b2d-127">Een aantal query's wordt uitgevoerd met behulp van `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="58b2d-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="58b2d-128">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="58b2d-128">Update your connection string</span></span>

<span data-ttu-id="58b2d-129">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="58b2d-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="58b2d-130">Selecteer in het Hallo-Account, **Quick Start**, selecteert u Java en Hallo connection string tooyour Klembord kopiëren</span><span class="sxs-lookup"><span data-stu-id="58b2d-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="58b2d-131">Open Hallo `Program.java` bestand, vervang Hallo argument toohello MongoClientURI constructor met Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="58b2d-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="58b2d-132">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="58b2d-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="58b2d-133">Hallo-console-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="58b2d-133">Run hello console app</span></span>

1. <span data-ttu-id="58b2d-134">Voer `mvn package` vereist in een terminal tooinstall npm-modules</span><span class="sxs-lookup"><span data-stu-id="58b2d-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="58b2d-135">Voer `mvn exec:java -D exec.mainClass=GetStarted.Program` in een terminal toostart uw Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="58b2d-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="58b2d-136">U kunt nu [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, wijzigen en werken met deze nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="58b2d-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="58b2d-137">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="58b2d-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="58b2d-138">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="58b2d-138">Clean up resources</span></span>

<span data-ttu-id="58b2d-139">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="58b2d-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="58b2d-140">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58b2d-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="58b2d-141">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="58b2d-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58b2d-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58b2d-142">Next steps</span></span>

<span data-ttu-id="58b2d-143">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een console-app.</span><span class="sxs-lookup"><span data-stu-id="58b2d-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="58b2d-144">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="58b2d-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="58b2d-145">MongoDB-gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="58b2d-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


