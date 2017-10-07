---
title: aaaCreate een Cosmos-DB Azure documentdatabase met behulp van Java | Microsoft Docs | Microsoft-Docs
description: Geeft het voorbeeld van een Java-code kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="991d7-103">Azure Cosmos DB: Maken van een documentdatabase met behulp van Java en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="991d7-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="991d7-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="991d7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="991d7-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="991d7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="991d7-106">Deze snelstartgids wordt gemaakt van een document database met Azure portal-hulpprogramma's Hallo voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="991d7-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="991d7-107">Deze snelstartgids ook ziet u hoe tooquickly maken voor een Java-consoletoepassing met Hallo [DocumentDB Java API](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="991d7-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="991d7-108">Hallo-instructies in deze snelstartgids kunnen worden uitgevoerd op elk besturingssysteem waarmee Java uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="991d7-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="991d7-109">Door het voltooien van deze snelstartgids zult u bekend bent met het maken en wijzigen van document database bronnen in de Hallo gebruikersinterface of via programmacode, afhankelijk van wat uw voorkeur is.</span><span class="sxs-lookup"><span data-stu-id="991d7-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="991d7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="991d7-110">Prerequisites</span></span>

* [<span data-ttu-id="991d7-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="991d7-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="991d7-112">Voer op Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="991d7-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="991d7-113">Worden ervoor tooset hello JAVA_HOME omgeving variabele toopoint toohello map is waarin Hallo JDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="991d7-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="991d7-114">[Download](http://maven.apache.org/download.cgi) en [installeer](http://maven.apache.org/install.html) een binair [Maven](http://maven.apache.org/)-archief</span><span class="sxs-lookup"><span data-stu-id="991d7-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="991d7-115">Ubuntu, u kunt uitvoeren `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="991d7-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="991d7-116">Git</span><span class="sxs-lookup"><span data-stu-id="991d7-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="991d7-117">Ubuntu, u kunt uitvoeren `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="991d7-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="991d7-118">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="991d7-118">Create a database account</span></span>

<span data-ttu-id="991d7-119">Voordat u een documentdatabase maken kunt, moet u een databaseaccount SQL (DocumentDB) met Azure Cosmos DB toocreate.</span><span class="sxs-lookup"><span data-stu-id="991d7-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="991d7-120">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="991d7-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="991d7-121">Voorbeeldgegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="991d7-121">Add sample data</span></span>

<span data-ttu-id="991d7-122">U kunt nu gegevens tooyour nieuwe verzameling met behulp van Data Explorer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="991d7-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="991d7-123">In Data Explorer Hallo nieuwe database in deelvenster wordt weergegeven Hallo verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="991d7-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="991d7-124">Vouw Hallo **taken** database, vouw Hallo **Items** verzameling, klikt u op **documenten**, en klik vervolgens op **nieuwe documenten**.</span><span class="sxs-lookup"><span data-stu-id="991d7-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Maken van nieuwe documenten in de Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="991d7-126">Voeg nu een documentverzameling toohello met Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="991d7-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="991d7-127">Zodra u hebt toegevoegd Hallo json toohello **documenten** tabblad **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="991d7-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Kopieer in json-gegevens en klik op opslaan in Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="991d7-129">Maak een meer document waar u een unieke waarde voor Hallo invoegen en sla `id` eigenschap en andere eigenschappen Hallo wens naar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="991d7-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="991d7-130">De nieuwe documenten kunnen elke gewenste structuur hebben, omdat in Azure Cosmos DB uw gegevens geen schema krijgen opgelegd.</span><span class="sxs-lookup"><span data-stu-id="991d7-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="991d7-131">U kunt nu gebruik query's in Data Explorer tooretrieve uw gegevens door te klikken op Hallo **-Filter bewerken** en **Filter toepassen** knoppen.</span><span class="sxs-lookup"><span data-stu-id="991d7-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="991d7-132">Data Explorer gebruikt standaard `SELECT * FROM c` tooretrieve alle documenten in de verzameling hello, maar u kunt wijzigen die andere tooa [SQL-query](documentdb-sql-query.md), zoals `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn alle Hallo documenten in aflopende volgorde op basis van hun timestamp.</span><span class="sxs-lookup"><span data-stu-id="991d7-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="991d7-133">U kunt ook Data Explorer toocreate opgeslagen procedures, UDF's en triggers tooperform-bedrijfslogica server ook gebruiken als de doorvoer van de schaal.</span><span class="sxs-lookup"><span data-stu-id="991d7-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="991d7-134">Data Explorer toont alle Hallo ingebouwde programmatische toegang tot gegevens beschikbaar zijn in Hallo API's, maar biedt eenvoudige toegang tooyour gegevens in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="991d7-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="991d7-135">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="991d7-135">Clone hello sample application</span></span>

<span data-ttu-id="991d7-136">Nu gaan we tooworking met code.</span><span class="sxs-lookup"><span data-stu-id="991d7-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="991d7-137">We gaan een DocumentDB-API-app vanuit GitHub Hallo verbindingsreeks instellen en voer dit klonen.</span><span class="sxs-lookup"><span data-stu-id="991d7-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="991d7-138">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="991d7-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="991d7-139">Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="991d7-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="991d7-140">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="991d7-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="991d7-141">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="991d7-141">Review hello code</span></span>

<span data-ttu-id="991d7-142">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="991d7-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="991d7-143">Open Hallo `Program.java` bestand van Hallo \src\GetStarted map, en deze regels code die hello Azure Cosmos DB resources maken vinden.</span><span class="sxs-lookup"><span data-stu-id="991d7-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="991d7-144">Hallo `DocumentClient` is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="991d7-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="991d7-145">Er wordt een nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="991d7-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="991d7-146">Er wordt een nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="991d7-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="991d7-147">Er wordt een aantal documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="991d7-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="991d7-148">Er wordt een SQL-query via JSON uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="991d7-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="991d7-149">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="991d7-149">Update your connection string</span></span>

<span data-ttu-id="991d7-150">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="991d7-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="991d7-151">Hiermee schakelt u de toocommunicate van uw app met uw gehoste-database.</span><span class="sxs-lookup"><span data-stu-id="991d7-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="991d7-152">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="991d7-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="991d7-153">U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `Program.java` bestand in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="991d7-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="991d7-155">In open Hallo `Program.java` bestand, Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo-waarde van Hallo eindpunt toohello DocumentClient-constructor `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="991d7-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="991d7-156">Vervolgens uw primaire sleutelwaarde kopiëren vanuit de portal Hallo en plak dit via 'FILLME', waardoor het Hallo van de tweede parameter in Hallo DocumentClient constructor.</span><span class="sxs-lookup"><span data-stu-id="991d7-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="991d7-157">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="991d7-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="991d7-158">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="991d7-158">Run hello app</span></span>

1. <span data-ttu-id="991d7-159">In Hallo git terminalvenster, `cd` toohello azure-cosmos-db-documentdb-java-getting-started map.</span><span class="sxs-lookup"><span data-stu-id="991d7-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="991d7-160">Typ in het Hallo git terminalvenster, `mvn package` tooinstall Hallo vereist Java-pakketten.</span><span class="sxs-lookup"><span data-stu-id="991d7-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="991d7-161">Voer in Hallo git terminalvenster, `mvn exec:java -D exec.mainClass=GetStarted.Program` in Hallo terminalvenster toostart uw Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="991d7-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="991d7-162">In terminalvenster hello ontvangt u meldingen die Hallo FamilyDB-database is gemaakt en een sleutel toocontinue toopress.</span><span class="sxs-lookup"><span data-stu-id="991d7-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="991d7-163">Druk op een sleutel toocreate Hallo-database, schakelt u toohello Data Explorer en ziet u dat deze nu een FamilyDB-database bevat.</span><span class="sxs-lookup"><span data-stu-id="991d7-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="991d7-164">Toopress sleutels toocreate Hallo verzameling en Hallo documenten gaan en vervolgens een query uitvoert.</span><span class="sxs-lookup"><span data-stu-id="991d7-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="991d7-165">Wanneer het Hallo-project is voltooid, worden Hallo resources verwijderd uit je account.</span><span class="sxs-lookup"><span data-stu-id="991d7-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="991d7-167">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="991d7-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="991d7-168">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="991d7-168">Clean up resources</span></span>

<span data-ttu-id="991d7-169">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="991d7-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="991d7-170">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="991d7-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="991d7-171">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="991d7-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="991d7-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="991d7-172">Next steps</span></span>

<span data-ttu-id="991d7-173">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling Hallo Data Explorer gebruikt en uitvoeren van een app toodo Hallo hetzelfde programmatisch.</span><span class="sxs-lookup"><span data-stu-id="991d7-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="991d7-174">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="991d7-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="991d7-175">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="991d7-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


