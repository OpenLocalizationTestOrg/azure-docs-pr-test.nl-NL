---
title: 'NoSQL-zelfstudie: DocumentDB API voor Azure Cosmos DB Java SDK | Microsoft Docs'
description: Een NoSQL-zelfstudie waarmee u maakt een online database en Java-consoletoepassing met Hallo DocumentDB-API voor Azure Cosmos DB. Azure DocumentDB is een NoSQL-database voor JSON.
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
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="fcdff-105">NoSQL-zelfstudie: een DocumentDB-API-Java-consoletoepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="fcdff-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcdff-106">.NET</span><span class="sxs-lookup"><span data-stu-id="fcdff-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="fcdff-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fcdff-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="fcdff-108">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="fcdff-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="fcdff-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="fcdff-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="fcdff-110">Java</span><span class="sxs-lookup"><span data-stu-id="fcdff-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="fcdff-111">C++</span><span class="sxs-lookup"><span data-stu-id="fcdff-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="fcdff-112">Welkom toohello NoSQL-zelfstudie voor Hallo DocumentDB-API voor Azure Cosmos DB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="fcdff-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="fcdff-113">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fcdff-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="fcdff-114">We behandelen de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="fcdff-114">We cover:</span></span>

* <span data-ttu-id="fcdff-115">Maken en te verbinden tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="fcdff-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="fcdff-116">Uw Visual Studio-oplossing configureren</span><span class="sxs-lookup"><span data-stu-id="fcdff-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="fcdff-117">Een online-database maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-117">Creating an online database</span></span>
* <span data-ttu-id="fcdff-118">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-118">Creating a collection</span></span>
* <span data-ttu-id="fcdff-119">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-119">Creating JSON documents</span></span>
* <span data-ttu-id="fcdff-120">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="fcdff-120">Querying hello collection</span></span>
* <span data-ttu-id="fcdff-121">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-121">Creating JSON documents</span></span>
* <span data-ttu-id="fcdff-122">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="fcdff-122">Querying hello collection</span></span>
* <span data-ttu-id="fcdff-123">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="fcdff-123">Replacing a document</span></span>
* <span data-ttu-id="fcdff-124">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="fcdff-124">Deleting a document</span></span>
* <span data-ttu-id="fcdff-125">Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="fcdff-125">Deleting hello database</span></span>

<span data-ttu-id="fcdff-126">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="fcdff-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcdff-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcdff-127">Prerequisites</span></span>
<span data-ttu-id="fcdff-128">Zorg ervoor dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="fcdff-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="fcdff-129">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="fcdff-129">An active Azure account.</span></span> <span data-ttu-id="fcdff-130">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fcdff-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fcdff-131">U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="fcdff-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="fcdff-132">Git</span><span class="sxs-lookup"><span data-stu-id="fcdff-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="fcdff-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="fcdff-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="fcdff-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="fcdff-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="fcdff-135">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="fcdff-136">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="fcdff-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="fcdff-137">Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[kloon Hallo GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="fcdff-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="fcdff-138">Als u van hello Azure Cosmos DB Emulator gebruikmaakt, stappen Hallo op [Azure Cosmos DB Emulator](local-emulator.md) tooset boven Hallo-emulator en gaat u verder te[kloon Hallo GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="fcdff-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="fcdff-139"><a id="GitClone"></a>Stap 2: Kloon Hallo GitHub project</span><span class="sxs-lookup"><span data-stu-id="fcdff-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="fcdff-140">U kunt aan de slag door het klonen van GitHub-opslagplaats voor Hallo [aan de slag met Azure Cosmos DB en Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="fcdff-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="fcdff-141">Bijvoorbeeld: vanuit een lokale map uitvoeren Hallo tooretrieve Hallo voorbeeldproject lokaal te volgen.</span><span class="sxs-lookup"><span data-stu-id="fcdff-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="fcdff-142">Hallo-map bevat een `pom.xml` voor Hallo-project en een `src` map met inbegrip van Java source code `Program.java` waaruit blijkt hoe eenvoudig bewerkingen uitvoeren met Azure Cosmos DB als het maken van documenten en opvragen van gegevens binnen een verzameling.</span><span class="sxs-lookup"><span data-stu-id="fcdff-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="fcdff-143">Hallo `pom.xml` bevat een afhankelijkheid op Hallo [DocumentDB Java SDK op Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="fcdff-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="fcdff-144"><a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="fcdff-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="fcdff-145">Vervolgens head back-toohello [Azure Portal](https://portal.azure.com) tooretrieve uw eindpunt en de primaire sleutel van de master.</span><span class="sxs-lookup"><span data-stu-id="fcdff-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="fcdff-146">Hello Azure DB die Cosmos-eindpunt en de primaire sleutel nodig zijn voor uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.</span><span class="sxs-lookup"><span data-stu-id="fcdff-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="fcdff-147">In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="fcdff-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="fcdff-148">Hallo URI van de portal Hallo Kopieer en plak deze in `https://FILLME.documents.azure.com` in Hallo Program.java-bestand.</span><span class="sxs-lookup"><span data-stu-id="fcdff-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="fcdff-149">Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="fcdff-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een Java-consoletoepassing.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="fcdff-152">Stap 4: een database maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-152">Step 4: Create a database</span></span>
<span data-ttu-id="fcdff-153">Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="fcdff-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fcdff-154">Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="fcdff-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="fcdff-155"><a id="CreateColl"></a>Stap 5: een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="fcdff-156">Met **createCollection** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="fcdff-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="fcdff-157">Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fcdff-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="fcdff-158">Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="fcdff-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fcdff-159">Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="fcdff-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="fcdff-160"><a id="CreateDoc"></a>Stap 6: JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="fcdff-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="fcdff-161">Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="fcdff-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fcdff-162">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="fcdff-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="fcdff-163">U kunt nu een of meer documenten invoegen.</span><span class="sxs-lookup"><span data-stu-id="fcdff-163">We can now insert one or more documents.</span></span> <span data-ttu-id="fcdff-164">Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) tooimport Hallo gegevens in een database.</span><span class="sxs-lookup"><span data-stu-id="fcdff-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

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

![Diagram ter illustratie Hallo hiërarchische relatie tussen Hallo-account, onlinedatabase Hallo Hallo verzameling en Hallo documenten die worden gebruikt door Hallo NoSQL-zelfstudie toocreate een Java-consoletoepassing](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="fcdff-166"><a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="fcdff-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="fcdff-167">Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="fcdff-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="fcdff-168">Hallo volgende voorbeeldcode ziet u hoe tooquery documenten in Azure Cosmos DB met behulp van SQL-syntaxis Hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) methode.</span><span class="sxs-lookup"><span data-stu-id="fcdff-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="fcdff-169"><a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen</span><span class="sxs-lookup"><span data-stu-id="fcdff-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="fcdff-170">Azure Cosmos DB ondersteunt bijwerken JSON-documenten met behulp van Hallo [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) methode.</span><span class="sxs-lookup"><span data-stu-id="fcdff-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="fcdff-171"><a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen</span><span class="sxs-lookup"><span data-stu-id="fcdff-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="fcdff-172">Op deze manier Azure Cosmos DB verwijderen JSON-documenten met behulp van Hallo ondersteunt [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) methode.</span><span class="sxs-lookup"><span data-stu-id="fcdff-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="fcdff-173"><a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="fcdff-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="fcdff-174">Verwijderen Hallo gemaakt database verwijdert Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).</span><span class="sxs-lookup"><span data-stu-id="fcdff-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="fcdff-175"><a id="Run"></a>Stap 11: uw Java-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fcdff-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="fcdff-176">toorun hello toepassing hello-console navigeert toohello projectmap en gecompileerd met behulp van Maven:</span><span class="sxs-lookup"><span data-stu-id="fcdff-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="fcdff-177">Met `mvn package` downloadt u de meest recente Azure Cosmos DB-bibliotheek Hallo van Maven en genereert `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="fcdff-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="fcdff-178">Voer vervolgens app Hallo door te voeren:</span><span class="sxs-lookup"><span data-stu-id="fcdff-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="fcdff-179">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="fcdff-179">Congratulations!</span></span> <span data-ttu-id="fcdff-180">U hebt de NoSQL-zelfstudie voltooid en beschikt nu over een werkende Java-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="fcdff-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcdff-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcdff-181">Next steps</span></span>
* <span data-ttu-id="fcdff-182">Wilt u een zelfstudie voor Java-web-apps volgen?</span><span class="sxs-lookup"><span data-stu-id="fcdff-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="fcdff-183">Zie [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Een Java-web-app maken met Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="fcdff-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="fcdff-184">Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="fcdff-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="fcdff-185">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="fcdff-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="fcdff-186">Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="fcdff-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
