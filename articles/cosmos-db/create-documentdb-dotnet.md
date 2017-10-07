---
title: 'Azure Cosmos DB: Een web-app met .NET bouwen en DocumentDB API Hallo | Microsoft Docs'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Een DocumentDB-API-web-app met .NET bouwen en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U moet vervolgens bouwen en implementeren van een WebApp voor takenlijstjes gebouwd op Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md), zoals weergegeven in de volgende schermafbeelding Hallo. 

![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Vereisten

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     U kunt uw gegevens nu query's in Data Explorer tooretrieve. Data Explorer gebruikt standaard `SELECT * FROM c` tooretrieve alle documenten in de verzameling hello, maar u kunt wijzigen die andere tooa [SQL-query](documentdb-sql-query.md), zoals `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn alle Hallo documenten in aflopende volgorde op basis van hun timestamp.
 
     U kunt ook Data Explorer toocreate opgeslagen procedures, UDF's en triggers tooperform-bedrijfslogica server ook gebruiken als de doorvoer van de schaal. Data Explorer toont alle Hallo ingebouwde programmatische toegang tot gegevens beschikbaar zijn in Hallo API's, maar biedt eenvoudige toegang tooyour gegevens in hello Azure-portal.

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we tooworking met code. We gaan een DocumentDB-API-app vanuit GitHub Hallo verbindingsreeks instellen en voer dit klonen. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Open vervolgens Hallo todo oplossingsbestand in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo DocumentDBRepository.cs bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo DocumentClient op regel 73 is geïnitialiseerd.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Er wordt een nieuwe database gemaakt op regel 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Er wordt een nieuwe verzameling gemaakt op regel 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. U gebruikt in web.config-bestand in de volgende stap Hallo HALLO hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel.

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. Open in Visual Studio-2017 Hallo web.config-bestand. 

3. Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in web.config. 

    `<add key="endpoint" value="FILLME" />`

4. Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en maken het Hallo-waarde van Hallo authKey in web.config. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Hallo-web-app uitvoeren
1. In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**. 

2. In Hallo NuGet **Bladeren** in het vak *DocumentDB*.

3. Installeren in Hallo resultaten Hallo **Microsoft.Azure.DocumentDB** bibliotheek. Hiermee installeert u Hallo Microsoft.Azure.DocumentDB pakket, evenals alle afhankelijkheden.

4. Klik op CTRL + F5 toorun Hallo-toepassing. Uw app wordt in uw browser weergegeven. 

5. Klik op **nieuw** in de browser Hallo en enkele nieuwe taken in uw app taak maken.

   ![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met deze nieuwe gegevens. 

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een web-app. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB](import-data.md)


