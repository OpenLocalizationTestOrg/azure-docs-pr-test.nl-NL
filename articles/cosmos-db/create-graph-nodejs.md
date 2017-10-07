---
title: een Azure Cosmos DB Node.js-toepassing met behulp van Graph API aaaBuild | Microsoft Docs
description: Geeft het voorbeeld van een Node.js-code kunt u tooconnect tooand query uitvoeren op Azure Cosmos-DB
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: een Node.js-toepassing ontwikkelen met de Graph API

Azure Cosmos DB is Hallo globaal gedistribueerd met meerdere modellen database-service van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

In dit artikel snel starten laat zien hoe een Cosmos Azure DB toocreate administratief Graph API (preview), de database en de grafiek met behulp van hello Azure-portal. U vervolgens bouwen en uitvoeren van een console-app met behulp van Hallo open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) stuurprogramma.  

> [!NOTE]
> Hallo npm-module `gremlin-secure` is een gewijzigde versie van `gremlin` module met ondersteuning voor SSL en SASL vereist om verbinding te maken met Azure Cosmos DB. Broncode is beschikbaar op [GitHub](https://github.com/CosmosDB/gremlin-javascript).
>

## <a name="prerequisites"></a>Vereisten

Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:
* [Node.js](https://nodejs.org/en/) versie v0.10.29 of hoger
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Een graaf toevoegen

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we kloon een Graph-API-app vanuit GitHub Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een Git-terminalvenster zoals Git Bash en wijzig (via `cd` opdracht) tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Open het oplossingsbestand Hallo in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo `app.js` -bestand en u vindt Hallo volgende regels code. 

* Hallo Gremlin client wordt gemaakt.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Hallo configuraties bevinden zich allemaal in `config.js`, die we in de volgende sectie Hallo bewerken.

* Een reeks Gremlin stappen worden uitgevoerd met een Hallo `client.execute` methode.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

1. Open Hallo bestand config.js file. 

2. In het bestand config.js, vult u Hallo config.endpoint sleutel met de Hallo **Gremlin URI** waarde van Hallo **overzicht** pagina Hallo Azure-portal. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-graph-nodejs/gremlin-uri.png)

   Als hello **Gremlin URI** waarde leeg is, kunt u Hallo waarde genereren van Hallo **sleutels** pagina in Hallo-portal, met Hallo **URI** waarde, https:// te verwijderen of wijzigen documenten toographs.

   Hallo Gremlin eindpunt moet alleen Hallo hostnaam zonder Hallo protocol/poortnummer, zoals `mygraphdb.graphs.azure.com` (geen `https://mygraphdb.graphs.azure.com` of `mygraphdb.graphs.azure.com:433`).

3. In config.js, vult u Hallo config.primaryKey waarde met de Hallo **primaire sleutel** waarde van Hallo **sleutels** pagina Hallo Azure-portal. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hallo blade van Azure portal sleutels](./media/create-graph-nodejs/keys.png)

4. Hallo-databasenaam en de grafieknaam van de (container) voor Hallo-waarde van config.database en config.collection invoeren. 

Hier volgt een voorbeeld van hoe het voltooide bestand config.js eruit moet zien:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Hallo-console-app uitvoeren

1. Open een terminalvenster en wijzig (via `cd` opdracht) installatiemap toohello voor Hallo package.json-bestand dat opgenomen in het Hallo-project.  

2. Voer `npm install` tooinstall Hallo vereist npm-modules, waaronder `gremlin-secure`.

3. Voer `node app.js` in een terminal toostart uw knooppunttoepassing.

## <a name="browse-with-data-explorer"></a>Bladeren met Data Explorer

U kunt nu gaat u terug tooData Explorer in Azure portal tooview hello, query, wijzigen en werken met uw nieuwe grafiekgegevens.

In Data Explorer Hallo nieuwe database wordt weergegeven in Hallo **grafieken** deelvenster. Hallo-database, gevolgd door de verzameling hello, uitbreiden en klik vervolgens op **grafiek**.

Hallo-gegevens die zijn gegenereerd door Hallo voorbeeld-app wordt weergegeven in de Volgend deelvenster binnen Hallo Hallo **grafiek** wanneer u klikt op tabblad **Filter toepassen**.

Probeer voltooien `g.V()` met `.has('firstName', 'Thomas')` tootest Hallo filter. Houd er rekening mee dat de waarde Hallo hoofdlettergevoelig is.

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Uw resources opschonen

Als u niet van plan gebruik van deze app toocontinue bent, verwijdert u alle resources die u hebt gemaakt in dit artikel door Hallo volgende te doen: 

1. Klik in de Azure-portal op Hallo linkernavigatievenster menu Hallo op **resourcegroepen**, en klik vervolgens op Hallo-naam van Hallo resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toobe verwijderd en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u geleerd hoe toocreate een Cosmos-DB Azure-account maken van een grafiek met behulp van Data Explorer en een app uitvoert. U kunt nu complexere query's maken en met Gremlin krachtige logica implementeren om door een graaf te gaan. 

> [!div class="nextstepaction"]
> [Query’s uitvoeren met Gremlin](tutorial-query-graph.md)
