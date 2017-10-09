---
title: 'Azure Cosmos DB: Bouwen van een app met behulp van Python en DocumentDB API Hallo | Microsoft Docs'
description: Geeft een Python-codevoorbeeld kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Azure Cosmos DB: Een DocumentDB-API-App met behulp van Python en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U vervolgens bouwen en uitvoeren van een console-app die is gebouwd op Hallo [DocumentDB Python API](documentdb-sdk-python.md).

## <a name="prerequisites"></a>Vereisten

* Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:
    * [Visual Studio 2015](http://www.visualstudio.com/) of hoger.
    * Python Tools for Visual Studio van [GitHub](http://microsoft.github.io/PTVS/). In deze zelfstudie wordt gebruikgemaakt van Python Tools for VS 2015.
    * Python 2.7 van [python.org](https://www.python.org/downloads/release/python-2712/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Een verzameling toevoegen

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu we de kloon een DocumentDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo DocumentDBGetStarted.py bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 


* Hallo DocumentClient is geïnitialiseerd.

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* Er wordt een nieuwe database gemaakt.

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* Er wordt een nieuwe verzameling gemaakt.

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* Er wordt een aantal documenten gemaakt.

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* Een query wordt uitgevoerd met behulp van SQL.

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `DocumentDBGetStarted.py` bestand in de volgende stap Hallo.

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. In Open Hallo `DocumentDBGetStarted.py` bestand. 

3. Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in `DocumentDBGetStarted.py`. 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en deze waarde Hallo Hallo `config.MASTERKEY` in `DocumentDBGetStarted.py`. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>Hallo-app uitvoeren
1. In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer**, selecteer Hallo huidige Python-omgeving en klik met de rechtermuisknop.

2. Selecteer Python-pakket installeren en typ vervolgens **pydocumentdb**

3. F5 toorun Hallo toepassing uitvoeren. Uw app wordt in uw browser weergegeven. 

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
> [Gegevens importeren in Azure Cosmos DB voor Hallo DocumentDB-API](import-data.md)


