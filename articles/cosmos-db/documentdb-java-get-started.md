---
title: 'NoSQL-zelfstudie: DocumentDB API voor Azure Cosmos DB Java SDK | Microsoft Docs'
description: Een NoSQL-zelfstudie waarmee u maakt een online database en Java-consoletoepassing met de DocumentDB-API voor Azure Cosmos DB. Azure DocumentDB is een NoSQL-database voor JSON.
keywords: nosql zelfstudie, onlinedatabase, java-consoletoepassing
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="2516d-105">NoSQL-zelfstudie: een DocumentDB-API-Java-consoletoepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="2516d-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2516d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2516d-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="2516d-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2516d-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="2516d-108">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="2516d-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="2516d-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="2516d-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="2516d-110">Java</span><span class="sxs-lookup"><span data-stu-id="2516d-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="2516d-111">C++</span><span class="sxs-lookup"><span data-stu-id="2516d-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="2516d-112">Welkom bij de NoSQL-zelfstudie over de DocumentDB-API voor Azure Cosmos DB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="2516d-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="2516d-113">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2516d-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="2516d-114">We behandelen de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="2516d-114">We cover:</span></span>

* <span data-ttu-id="2516d-115">Een Azure Cosmos DB-account maken en er verbinding mee maken</span><span class="sxs-lookup"><span data-stu-id="2516d-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="2516d-116">Uw Visual Studio-oplossing configureren</span><span class="sxs-lookup"><span data-stu-id="2516d-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="2516d-117">Een online-database maken</span><span class="sxs-lookup"><span data-stu-id="2516d-117">Creating an online database</span></span>
* <span data-ttu-id="2516d-118">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="2516d-118">Creating a collection</span></span>
* <span data-ttu-id="2516d-119">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="2516d-119">Creating JSON documents</span></span>
* <span data-ttu-id="2516d-120">Query's uitvoeren op de verzameling</span><span class="sxs-lookup"><span data-stu-id="2516d-120">Querying the collection</span></span>
* <span data-ttu-id="2516d-121">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="2516d-121">Creating JSON documents</span></span>
* <span data-ttu-id="2516d-122">Query's uitvoeren op de verzameling</span><span class="sxs-lookup"><span data-stu-id="2516d-122">Querying the collection</span></span>
* <span data-ttu-id="2516d-123">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="2516d-123">Replacing a document</span></span>
* <span data-ttu-id="2516d-124">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="2516d-124">Deleting a document</span></span>
* <span data-ttu-id="2516d-125">De database verwijderen</span><span class="sxs-lookup"><span data-stu-id="2516d-125">Deleting the database</span></span>

<span data-ttu-id="2516d-126">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="2516d-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2516d-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2516d-127">Prerequisites</span></span>
<span data-ttu-id="2516d-128">Zorg ervoor dat u over de volgende zaken beschikt:</span><span class="sxs-lookup"><span data-stu-id="2516d-128">Make sure you have the following:</span></span>

* <span data-ttu-id="2516d-129">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2516d-129">An active Azure account.</span></span> <span data-ttu-id="2516d-130">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2516d-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="2516d-131">U kunt voor deze zelfstudie ook de [Azure Cosmos DB-emulator](local-emulator.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2516d-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="2516d-132">Git</span><span class="sxs-lookup"><span data-stu-id="2516d-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="2516d-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2516d-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="2516d-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="2516d-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="2516d-135">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="2516d-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2516d-136">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="2516d-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="2516d-137">Als u al een account hebt dat u wilt gebruiken, kunt u verder naar de stap [Het GitHub-project klonen](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="2516d-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="2516d-138">Als u de Azure Cosmos DB-emulator gebruikt, volgt u de stappen in [Azure Cosmos DB-emulator](local-emulator.md) om de emulator in te stellen en meteen naar [Het GitHub-project klonen](#GitClone) te gaan.</span><span class="sxs-lookup"><span data-stu-id="2516d-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2516d-139"><a id="GitClone"></a>Stap 2: het GitHub-project klonen</span><span class="sxs-lookup"><span data-stu-id="2516d-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="2516d-140">Kloon eerst de GitHub-opslagplaats voor [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started) (Aan de slag met Azure Cosmos DB en Java).</span><span class="sxs-lookup"><span data-stu-id="2516d-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="2516d-141">Voer bijvoorbeeld vanuit een lokale map het volgende uit als u het voorbeeldproject lokaal wilt ophalen.</span><span class="sxs-lookup"><span data-stu-id="2516d-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="2516d-142">De map bevat een `pom.xml` voor het project en een `src` map met inbegrip van Java source code `Program.java` waaruit blijkt hoe eenvoudig bewerkingen uitvoeren met Azure Cosmos DB als het maken van documenten en gegevens binnen een verzameling opvragen .</span><span class="sxs-lookup"><span data-stu-id="2516d-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="2516d-143">De `pom.xml` bevat een afhankelijkheid van de [DocumentDB Java SDK op Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="2516d-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="2516d-144"><a id="Connect"></a>Stap 3: verbinding maken met een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="2516d-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="2516d-145">Ga vervolgens terug naar [Azure Portal](https://portal.azure.com) om uw eindpunt en primaire hoofdsleutel op te halen.</span><span class="sxs-lookup"><span data-stu-id="2516d-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="2516d-146">Uw toepassing heeft het Azure Cosmos DB-eindpunt en de primaire sleutel nodig om te bepalen waarmee verbinding moet worden gemaakt en om ervoor te zorgen dat Azure Cosmos DB de verbinding van uw toepassing vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="2516d-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="2516d-147">Navigeer in Azure Portal naar uw Azure Cosmos DB-account en klik daarna op **Sleutels**.</span><span class="sxs-lookup"><span data-stu-id="2516d-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="2516d-148">Kopieer in de portal de URI en plak deze in `https://FILLME.documents.azure.com` in het bestand Program.java.</span><span class="sxs-lookup"><span data-stu-id="2516d-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="2516d-149">Kopieer vervolgens de PRIMAIRE SLEUTEL van de portal en plak deze in `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="2516d-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Schermopname van Azure Portal die voor de NoSQL-zelfstudie wordt gebruikt om een Java-consoletoepassing te maken.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="2516d-152">Stap 4: een database maken</span><span class="sxs-lookup"><span data-stu-id="2516d-152">Step 4: Create a database</span></span>
<span data-ttu-id="2516d-153">Uw Azure Cosmos DB-[database](documentdb-resources.md#databases) kan worden gemaakt met de methode [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) van de klasse **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2516d-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2516d-154">Een database is een logische container voor een JSON-documentopslag, gepartitioneerd in verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="2516d-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="2516d-155"><a id="CreateColl"></a>Stap 5: een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="2516d-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="2516d-156">Met **createCollection** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="2516d-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="2516d-157">Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2516d-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="2516d-158">U kunt een [verzameling](documentdb-resources.md#collections) maken met de methode [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) van de klasse **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2516d-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2516d-159">Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="2516d-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="2516d-160"><a id="CreateDoc"></a>Stap 6: JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="2516d-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="2516d-161">U kunt een [document](documentdb-resources.md#documents) maken met de methode [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) van de klasse **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2516d-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2516d-162">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="2516d-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2516d-163">U kunt nu een of meer documenten invoegen.</span><span class="sxs-lookup"><span data-stu-id="2516d-163">We can now insert one or more documents.</span></span> <span data-ttu-id="2516d-164">Als u gegevens die u wilt opslaan in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) importeren van de gegevens in een database.</span><span class="sxs-lookup"><span data-stu-id="2516d-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagram waarin u de hiërarchische relatie ziet tussen het account, de online database, de verzameling en de documenten die in de NoSQL-zelfstudie worden gebruikt om een Java-consoletoepassing te maken](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="2516d-166"><a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="2516d-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="2516d-167">Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="2516d-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="2516d-168">De volgende voorbeeldcode laat zien hoe u query's kunt toepassen op documenten in Azure Cosmos DB met behulp van de SQL-syntaxis met de methode [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="2516d-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="2516d-169"><a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen</span><span class="sxs-lookup"><span data-stu-id="2516d-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="2516d-170">Azure Cosmos DB ondersteunt het bijwerken van JSON-documenten met behulp van de methode [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="2516d-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="2516d-171"><a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen</span><span class="sxs-lookup"><span data-stu-id="2516d-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="2516d-172">Azure Cosmos DB ondersteunt ook het verwijderen van JSON-documenten met behulp van de methode [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="2516d-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="2516d-173"><a id="DeleteDatabase"></a>Stap 10: de database verwijderen</span><span class="sxs-lookup"><span data-stu-id="2516d-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="2516d-174">Als u de gemaakte database verwijdert, worden de database en alle onderliggende resources (verzamelingen, documenten enz.) verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2516d-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="2516d-175"><a id="Run"></a>Stap 11: uw Java-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2516d-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="2516d-176">Voor de toepassing uitvoeren vanaf de console, gaat u naar de projectmap en gecompileerd met behulp van Maven:</span><span class="sxs-lookup"><span data-stu-id="2516d-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="2516d-177">Als u `mvn package` uitvoert, wordt de nieuwste Azure Cosmos DB-bibliotheek vanuit Maven gedownload en wordt `GetStarted-0.0.1-SNAPSHOT.jar` geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="2516d-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="2516d-178">Voer vervolgens de app uit door het volgende uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2516d-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="2516d-179">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="2516d-179">Congratulations!</span></span> <span data-ttu-id="2516d-180">U hebt de NoSQL-zelfstudie voltooid en beschikt nu over een werkende Java-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="2516d-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="2516d-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2516d-181">Next steps</span></span>
* <span data-ttu-id="2516d-182">Wilt u een zelfstudie voor Java-web-apps volgen?</span><span class="sxs-lookup"><span data-stu-id="2516d-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="2516d-183">Zie [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Een Java-web-app maken met Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="2516d-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="2516d-184">Leer hoe het [bewaken van een Azure Cosmos DB-account](monitor-accounts.md) werkt.</span><span class="sxs-lookup"><span data-stu-id="2516d-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="2516d-185">Voer query's uit op onze voorbeeldgegevensset in de [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2516d-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2516d-186">Meer informatie over het programmeermodel vindt u in de sectie Ontwikkelen van de [pagina met Azure Cosmos DB-documentatie](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2516d-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
