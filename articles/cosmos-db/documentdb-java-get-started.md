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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>NoSQL-zelfstudie: een DocumentDB-API-Java-consoletoepassing bouwen
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js voor MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Welkom toohello NoSQL-zelfstudie voor Hallo DocumentDB-API voor Azure Cosmos DB Java SDK. Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.

We behandelen de volgende onderwerpen:

* Maken en te verbinden tooan Azure DB die Cosmos-account
* Uw Visual Studio-oplossing configureren
* Een online-database maken
* Een verzameling maken
* JSON-documenten maken
* Hallo verzameling opvragen
* JSON-documenten maken
* Hallo verzameling opvragen
* Een document vervangen
* Een document verwijderen
* Hallo-database verwijderen

Tijd om aan de slag te gaan.

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/). U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.
* [Git](https://git-scm.com/downloads)
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Stap 1: een Azure Cosmos DB-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[kloon Hallo GitHub project](#GitClone). Als u van hello Azure Cosmos DB Emulator gebruikmaakt, stappen Hallo op [Azure Cosmos DB Emulator](local-emulator.md) tooset boven Hallo-emulator en gaat u verder te[kloon Hallo GitHub project](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Stap 2: Kloon Hallo GitHub project
U kunt aan de slag door het klonen van GitHub-opslagplaats voor Hallo [aan de slag met Azure Cosmos DB en Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Bijvoorbeeld: vanuit een lokale map uitvoeren Hallo tooretrieve Hallo voorbeeldproject lokaal te volgen.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Hallo-map bevat een `pom.xml` voor Hallo-project en een `src` map met inbegrip van Java source code `Program.java` waaruit blijkt hoe eenvoudig bewerkingen uitvoeren met Azure Cosmos DB als het maken van documenten en opvragen van gegevens binnen een verzameling. Hallo `pom.xml` bevat een afhankelijkheid op Hallo [DocumentDB Java SDK op Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account
Vervolgens head back-toohello [Azure Portal](https://portal.azure.com) tooretrieve uw eindpunt en de primaire sleutel van de master. Hello Azure DB die Cosmos-eindpunt en de primaire sleutel nodig zijn voor uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.

In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**. Hallo URI van de portal Hallo Kopieer en plak deze in `https://FILLME.documents.azure.com` in Hallo Program.java-bestand. Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een Java-consoletoepassing. Ziet u een Cosmos Azure DB-account met de actieve hub Hallo gemarkeerd, Hallo knop sleutels gemarkeerd op de blade hello Azure DB die Cosmos-account en de waarden URI, primaire sleutel en secundaire sleutel Hallo gemarkeerd op Hallo blade sleutels][keys]

## <a name="step-4-create-a-database"></a>Stap 4: een database maken
Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) methode Hallo **DocumentClient** klasse. Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Stap 5: een verzameling maken
> [!WARNING]
> Met **createCollection** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten. Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.
> 
> 

Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) methode Hallo **DocumentClient** klasse. Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Stap 6: JSON-documenten maken
Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) methode Hallo **DocumentClient** klasse. Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. U kunt nu een of meer documenten invoegen. Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) tooimport Hallo gegevens in een database.

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

## <a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources
Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.  Hallo volgende voorbeeldcode ziet u hoe tooquery documenten in Azure Cosmos DB met behulp van SQL-syntaxis Hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) methode.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen
Azure Cosmos DB ondersteunt bijwerken JSON-documenten met behulp van Hallo [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) methode.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen
Op deze manier Azure Cosmos DB verwijderen JSON-documenten met behulp van Hallo ondersteunt [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) methode.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen
Verwijderen Hallo gemaakt database verwijdert Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Stap 11: uw Java-consoletoepassing volledig uitvoeren
toorun hello toepassing hello-console navigeert toohello projectmap en gecompileerd met behulp van Maven:
    
    mvn package

Met `mvn package` downloadt u de meest recente Azure Cosmos DB-bibliotheek Hallo van Maven en genereert `GetStarted-0.0.1-SNAPSHOT.jar`. Voer vervolgens app Hallo door te voeren:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Gefeliciteerd. U hebt de NoSQL-zelfstudie voltooid en beschikt nu over een werkende Java-consoletoepassing.

## <a name="next-steps"></a>Volgende stappen
* Wilt u een zelfstudie voor Java-web-apps volgen? Zie [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Een Java-web-app maken met Azure Cosmos DB).
* Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
