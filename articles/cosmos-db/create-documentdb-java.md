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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Maken van een documentdatabase met behulp van Java en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snelstartgids wordt gemaakt van een document database met Azure portal-hulpprogramma's Hallo voor Azure Cosmos DB. Deze snelstartgids ook ziet u hoe tooquickly maken voor een Java-consoletoepassing met Hallo [DocumentDB Java API](documentdb-sdk-java.md). Hallo-instructies in deze snelstartgids kunnen worden uitgevoerd op elk besturingssysteem waarmee Java uitgevoerd. Door het voltooien van deze snelstartgids zult u bekend bent met het maken en wijzigen van document database bronnen in de Hallo gebruikersinterface of via programmacode, afhankelijk van wat uw voorkeur is.

## <a name="prerequisites"></a>Vereisten

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Voer op Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.
    * Worden ervoor tooset hello JAVA_HOME omgeving variabele toopoint toohello map is waarin Hallo JDK is geïnstalleerd.
* [Download](http://maven.apache.org/download.cgi) en [installeer](http://maven.apache.org/install.html) een binair [Maven](http://maven.apache.org/)-archief
    * Ubuntu, u kunt uitvoeren `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Ubuntu, u kunt uitvoeren `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

Voordat u een documentdatabase maken kunt, moet u een databaseaccount SQL (DocumentDB) met Azure Cosmos DB toocreate.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Een verzameling toevoegen

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Voorbeeldgegevens toevoegen

U kunt nu gegevens tooyour nieuwe verzameling met behulp van Data Explorer toevoegen.

1. In Data Explorer Hallo nieuwe database in deelvenster wordt weergegeven Hallo verzamelingen. Vouw Hallo **taken** database, vouw Hallo **Items** verzameling, klikt u op **documenten**, en klik vervolgens op **nieuwe documenten**. 

   ![Maken van nieuwe documenten in de Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Voeg nu een documentverzameling toohello met Hallo structuur te volgen.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Zodra u hebt toegevoegd Hallo json toohello **documenten** tabblad **opslaan**.

    ![Kopieer in json-gegevens en klik op opslaan in Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Maak een meer document waar u een unieke waarde voor Hallo invoegen en sla `id` eigenschap en andere eigenschappen Hallo wens naar wijzigen. De nieuwe documenten kunnen elke gewenste structuur hebben, omdat in Azure Cosmos DB uw gegevens geen schema krijgen opgelegd.

     U kunt nu gebruik query's in Data Explorer tooretrieve uw gegevens door te klikken op Hallo **-Filter bewerken** en **Filter toepassen** knoppen. Data Explorer gebruikt standaard `SELECT * FROM c` tooretrieve alle documenten in de verzameling hello, maar u kunt wijzigen die andere tooa [SQL-query](documentdb-sql-query.md), zoals `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn alle Hallo documenten in aflopende volgorde op basis van hun timestamp. 
 
     U kunt ook Data Explorer toocreate opgeslagen procedures, UDF's en triggers tooperform-bedrijfslogica server ook gebruiken als de doorvoer van de schaal. Data Explorer toont alle Hallo ingebouwde programmatische toegang tot gegevens beschikbaar zijn in Hallo API's, maar biedt eenvoudige toegang tooyour gegevens in hello Azure-portal.

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we tooworking met code. We gaan een DocumentDB-API-app vanuit GitHub Hallo verbindingsreeks instellen en voer dit klonen. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo `Program.java` bestand van Hallo \src\GetStarted map, en deze regels code die hello Azure Cosmos DB resources maken vinden. 

* Hallo `DocumentClient` is geïnitialiseerd.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Er wordt een nieuwe database gemaakt.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Er wordt een nieuwe verzameling gemaakt.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Er wordt een aantal documenten gemaakt.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Er wordt een SQL-query via JSON uitgevoerd.

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

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app. Hiermee schakelt u de toocommunicate van uw app met uw gehoste-database.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `Program.java` bestand in de volgende stap Hallo.

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. In open Hallo `Program.java` bestand, Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo-waarde van Hallo eindpunt toohello DocumentClient-constructor `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Vervolgens uw primaire sleutelwaarde kopiëren vanuit de portal Hallo en plak dit via 'FILLME', waardoor het Hallo van de tweede parameter in Hallo DocumentClient constructor. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 
    
## <a name="run-hello-app"></a>Hallo-app uitvoeren

1. In Hallo git terminalvenster, `cd` toohello azure-cosmos-db-documentdb-java-getting-started map.

2. Typ in het Hallo git terminalvenster, `mvn package` tooinstall Hallo vereist Java-pakketten.

3. Voer in Hallo git terminalvenster, `mvn exec:java -D exec.mainClass=GetStarted.Program` in Hallo terminalvenster toostart uw Java-toepassing.

    In terminalvenster hello ontvangt u meldingen die Hallo FamilyDB-database is gemaakt en een sleutel toocontinue toopress. Druk op een sleutel toocreate Hallo-database, schakelt u toohello Data Explorer en ziet u dat deze nu een FamilyDB-database bevat. Toopress sleutels toocreate Hallo verzameling en Hallo documenten gaan en vervolgens een query uitvoert. Wanneer het Hallo-project is voltooid, worden Hallo resources verwijderd uit je account. 

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling Hallo Data Explorer gebruikt en uitvoeren van een app toodo Hallo hetzelfde programmatisch. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB](import-data.md)


