---
title: een Azure Cosmos DB .NET-toepassing gebruikt aaaBuild Hallo Graph API | Microsoft Docs
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query uitvoeren op Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: Een .NET-toepassing hello Graph API met bouwen

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe toocreate een Cosmos-DB Azure-account, database en het gebruik van de grafiek (container) hello Azure-portal. U vervolgens bouwen en uitvoeren van een console-app die is gebouwd op Hallo [Graph API](graph-sdk-dotnet.md) (preview).  

## <a name="prerequisites"></a>Vereisten

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Een graaf toevoegen

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we kloon een Graph-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Open Visual Studio en open Hallo oplossingsbestand. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Het bestand Program.cs Open Hallo en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo DocumentClient is geïnitialiseerd. Hallo-Preview toegevoegd we extensie graph API op Hallo Azure DB die Cosmos-client. We werken op een zelfstandige grafiek client ontkoppeld van hello Azure DB die Cosmos-client en -bronnen.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Er wordt een nieuwe database gemaakt.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Er wordt en nieuwe graaf gemaakt.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Een reeks Gremlin stappen worden uitgevoerd met Hallo `CreateGremlinQuery` methode.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. Open in Visual Studio-2017 Hallo App.config-bestand. 

2. Klik in hello Azure-portal in uw Azure DB die Cosmos-account op **sleutels** in Hallo linkernavigatiebalk. 

    ![Bekijken en kopiëren van een primaire sleutel in hello Azure-portal op Hallo sleutels pagina](./media/create-graph-dotnet/keys.png)

3. Kopieer uw **URI** waarde uit de portal hello, waardoor het Hallo Hallo eindpunt sleutelwaarde in App.config. Kunt u de knop kopiëren Hallo zoals weergegeven in Hallo vóór schermafbeelding toocopy Hallo waarde.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Kopieer uw **primaire sleutel** waarde uit de Hallo-portal en maken het Hallo Hallo AuthKey sleutelwaarde in App.config en sla vervolgens uw wijzigingen. 

    `<add key="AuthKey" value="FILLME" />`

U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

## <a name="run-hello-console-app"></a>Hallo-console-app uitvoeren

1. In Visual Studio met de rechtermuisknop op Hallo **GraphGetStarted** project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**. 

2. In Hallo NuGet **Bladeren** in het vak *Microsoft.Azure.Graphs* en controleer Hallo **bevat voorlopige versie** vak. 

3. Installeren in Hallo resultaten Hallo **Microsoft.Azure.Graphs** bibliotheek. Hiermee installeert u hello Azure Cosmos DB grafiek uitbreidingspakket-bibliotheek en alle afhankelijkheden.

    Als u een bericht krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**. Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.

4. Klik op CTRL + F5 toorun Hallo-toepassing.

   Hallo-consolevenster geeft Hallo hoekpunten en randen toohello grafiek worden toegevoegd. Wanneer Hallo-script is voltooid, druk op ENTER tweemaal tooclose Hallo consolevenster. 

## <a name="browse-using-hello-data-explorer"></a>Bladeren met behulp van Hallo Data Explorer

U kunt nu gaat u terug tooData Explorer in hello Azure-portal en bladeren en de nieuwe grafiekgegevens zoeken.

1. In Data Explorer Hallo nieuwe database in deelvenster wordt weergegeven Hallo grafieken. Vouw **graphdb**, **graphcollz** uit en klik vervolgens op **Grafiek**.

2. Klik op Hallo **Filter toepassen** knop toouse Hallo standaard query tooview alle Hallo verticies in Hallo-grafiek. Hallo-gegevens die zijn gegenereerd door Hallo voorbeeld-app wordt weergegeven in Hallo grafieken deelvenster.

    U kunt in-en uitzoomen Hallo grafiek, kunt u Hallo grafiek ruimte voor de weergave uitvouwen, extra verticies toevoegen en verplaatsen verticies op Hallo weergeven voor aanvallen.

    ![Grafiek in Data Explorer Hallo in hello Azure-portal weergeven](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen: 

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account maken van een grafiek met Hallo Data Explorer en een app uitvoeren. U kunt nu complexere query's maken en met Gremlin krachtige logica implementeren om door een graaf te gaan. 

> [!div class="nextstepaction"]
> [Query’s uitvoeren met Gremlin](tutorial-query-graph.md)

