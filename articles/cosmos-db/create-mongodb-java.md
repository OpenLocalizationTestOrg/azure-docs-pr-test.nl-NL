---
title: 'Azure Cosmos DB: een console-app ontwikkelen met Java en de MongoDB-API | Microsoft Docs'
description: "Biedt een voorbeeld van Java-code dat u kunt gebruiken om verbinding te maken met de MongoDB-API van Azure Cosmos DB en er query’s op uit te voeren"
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
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="a14af-103">Azure Cosmos DB: een MongoDB-API-console-app ontwikkelen met Java en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a14af-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="a14af-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a14af-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a14af-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a14af-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a14af-106">Deze Quick Start laat zien hoe u een Azure Cosmos DB-account, een documentdatabase en een verzameling kunt maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a14af-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="a14af-107">U gaat vervolgens een console-app ontwikkelen en implementeren op het [MongoDB Java-stuurprogramma](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="a14af-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a14af-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a14af-108">Prerequisites</span></span>

* <span data-ttu-id="a14af-109">Voordat u met dit voorbeeld aan de slag gaat, moet u aan de volgende vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="a14af-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="a14af-110">JDK 1.7+ (voer `apt-get install default-jdk` uit als u niet over JDK beschikt)</span><span class="sxs-lookup"><span data-stu-id="a14af-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="a14af-111">Maven (voer `apt-get install maven` uit als u niet over Maven beschikt)</span><span class="sxs-lookup"><span data-stu-id="a14af-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="a14af-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="a14af-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="a14af-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="a14af-113">Add a collection</span></span>

<span data-ttu-id="a14af-114">Geef uw nieuwe database de naam **db**, en uw nieuwe verzameling **verz**.</span><span class="sxs-lookup"><span data-stu-id="a14af-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="a14af-115">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="a14af-115">Clone the sample application</span></span>

<span data-ttu-id="a14af-116">We gaan nu een MongoDB API-app klonen vanaf GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a14af-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="a14af-117">U zult zien hoe gemakkelijk het is om op een programmatische manier met gegevens te werken.</span><span class="sxs-lookup"><span data-stu-id="a14af-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a14af-118">Open een venster in een git-terminal zoals git bash en `cd` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="a14af-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="a14af-119">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="a14af-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="a14af-120">Open vervolgens het oplossingenbestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a14af-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="a14af-121">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="a14af-121">Review the code</span></span>

<span data-ttu-id="a14af-122">Laten we eens kijken wat er precies gebeurt in de app.</span><span class="sxs-lookup"><span data-stu-id="a14af-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="a14af-123">Open het bestand `Program.cs` en u zult zien dat deze regels code de Azure Cosmos DB-resources maken.</span><span class="sxs-lookup"><span data-stu-id="a14af-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="a14af-124">De DocumentClient wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="a14af-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="a14af-125">Er wordt een nieuwe database en verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a14af-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="a14af-126">Een aantal documenten wordt ingevoegd met behulp van `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="a14af-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="a14af-127">Een aantal query's wordt uitgevoerd met behulp van `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="a14af-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="a14af-128">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="a14af-128">Update your connection string</span></span>

<span data-ttu-id="a14af-129">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="a14af-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="a14af-130">Selecteer in het account **Quick Start**, selecteer Java en kopieer vervolgens de verbindingsreeks naar het klembord</span><span class="sxs-lookup"><span data-stu-id="a14af-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="a14af-131">Open het bestand `Program.java`, vervang het argument voor de MongoClientURI-constructor door de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="a14af-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="a14af-132">U hebt uw app nu bijgewerkt met alle informatie die nodig is voor de communicatie met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a14af-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="a14af-133">De app console uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a14af-133">Run the console app</span></span>

1. <span data-ttu-id="a14af-134">Voer `mvn package` uit op een terminal zodat de vereiste npm-modules worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a14af-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="a14af-135">Voer `mvn exec:java -D exec.mainClass=GetStarted.Program` uit op een terminal om uw Java-toepassing te starten.</span><span class="sxs-lookup"><span data-stu-id="a14af-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="a14af-136">U kunt nu [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) gebruiken om query’s op deze nieuwe gegevens uit te voeren, ze te wijzigen en er op een ander manier mee te werken.</span><span class="sxs-lookup"><span data-stu-id="a14af-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a14af-137">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a14af-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a14af-138">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="a14af-138">Clean up resources</span></span>

<span data-ttu-id="a14af-139">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a14af-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="a14af-140">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a14af-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="a14af-141">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="a14af-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a14af-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a14af-142">Next steps</span></span>

<span data-ttu-id="a14af-143">In deze Quick Start hebt u geleerd hoe u een Azure Cosmos DB-account kunt maken, hoe u een verzameling kunt maken met Data Explorer en hebt u een console-app uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a14af-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="a14af-144">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="a14af-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a14af-145">MongoDB-gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a14af-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


