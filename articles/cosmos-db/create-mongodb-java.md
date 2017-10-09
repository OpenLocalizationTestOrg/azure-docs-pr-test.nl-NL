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
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB: Bouwen van een console-app van de MongoDB-API met behulp van Java en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U moet vervolgens bouwen en implementeren van een console-app die is gebouwd op Hallo [MongoDB Java stuurprogramma](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Vereisten

* Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:
   * JDK 1.7+ (voer `apt-get install default-jdk` uit als u niet over JDK beschikt)
   * Maven (voer `apt-get install maven` uit als u niet over Maven beschikt)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Een verzameling toevoegen

Geef uw nieuwe database de naam **db**, en uw nieuwe verzameling **verz**.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu we de kloon een MongoDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Open het oplossingsbestand Hallo in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo `Program.cs` bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo DocumentClient is geïnitialiseerd.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Er wordt een nieuwe database en verzameling gemaakt.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Een aantal documenten wordt ingevoegd met behulp van `MongoCollection.insertOne`

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Een aantal query's wordt uitgevoerd met behulp van `MongoCollection.find`

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. Selecteer in het Hallo-Account, **Quick Start**, selecteert u Java en Hallo connection string tooyour Klembord kopiëren

2. Open Hallo `Program.java` bestand, vervang Hallo argument toohello MongoClientURI constructor met Hallo-verbindingsreeks. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 
    
## <a name="run-hello-console-app"></a>Hallo-console-app uitvoeren

1. Voer `mvn package` vereist in een terminal tooinstall npm-modules

2. Voer `mvn exec:java -D exec.mainClass=GetStarted.Program` in een terminal toostart uw Java-toepassing.

U kunt nu [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, wijzigen en werken met deze nieuwe gegevens.

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een console-app. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [MongoDB-gegevens importeren in Azure Cosmos DB](mongodb-migrate.md)


