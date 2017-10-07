---
title: 'Azure Cosmos DB: Bouwen van een app met behulp van Node.js en DocumentDB API Hallo | Microsoft Docs'
description: Geeft het voorbeeld van een Node.js-code kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Azure Cosmos DB: Een DocumentDB-API-app met behulp van Node.js bouwen en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U vervolgens bouwen en uitvoeren van een console-app die is gebouwd op Hallo [DocumentDB Node.js-API](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Vereisten

* Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:
    * [Node.js](https://nodejs.org/en/) versie v0.10.29 of hoger
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Een verzameling toevoegen

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu we de kloon een DocumentDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo `app.js` bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo `documentClient` is geïnitialiseerd.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* Er wordt een nieuwe database gemaakt.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Er wordt een nieuwe verzameling gemaakt.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Er wordt een aantal documenten gemaakt.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Er wordt een SQL-query via JSON uitgevoerd.

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `config.js` bestand in de volgende stap Hallo.

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. In Open Hallo `config.js` bestand. 

3. Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en deze waarde Hallo Hallo `config.primaryKey` in `config.js`. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Hallo-app uitvoeren
1. Voer `npm install` vereist in een terminal tooinstall npm-modules

2. Voer `node app.js` in een terminal toostart uw knooppunttoepassing.

U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met deze nieuwe gegevens. 

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een app. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB](import-data.md)


