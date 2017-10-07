---
title: 'Azure Cosmos DB: Een web-app met .NET bouwen en Hallo MongoDB-API | Microsoft Docs'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query hello Azure Cosmos DB MongoDB-API
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Een web-app van de MongoDB-API met .NET bouwen en hello Azure-portal

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U vervolgens bouwen en implementeren van een taken lijst web-app gebouwd op Hallo [MongoDB .NET stuurprogramma](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Vereisten

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu we de kloon een MongoDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Open het oplossingsbestand Hallo in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo **Dal.cs** bestand onder Hallo **DAL** directory en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo Mongo-Client initialiseren.

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* Hallo-database en verzameling Hallo ophalen.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Haal alle documenten op.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **verbindingsreeks**, en klik vervolgens op **lezen-schrijven sleutels**. U gebruikt in Hallo Dal.cs bestand in de volgende stap Hallo Hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo gebruikersnaam, wachtwoord en Host.

2. Open Hallo **Dal.cs** bestand in Hallo **DAL** directory. 

3. Kopieer uw **gebruikersnaam** waarde uit de Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het waarde Hallo Hallo **gebruikersnaam** in uw **Dal.cs** bestand. 

4. Kopieer uw **host** waarde uit de portal hello, waardoor het Hallo-waarde van Hallo **host** in uw **Dal.cs** bestand. 

5. Ten slotte Kopieer uw **wachtwoord** waarde uit de portal hello, waardoor het Hallo waarde Hallo **wachtwoord** in uw **Dal.cs** bestand. 

U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 
    
## <a name="run-hello-web-app"></a>Hallo-web-app uitvoeren

1. In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**. 

2. In Hallo NuGet **Bladeren** in het vak *MongoDB.Driver*.

3. Installeren in Hallo resultaten Hallo **MongoDB.Driver** bibliotheek. Hiermee installeert u Hallo MongoDB.Driver pakket, evenals alle afhankelijkheden.

4. Klik op CTRL + F5 toorun Hallo-toepassing. Uw app wordt in uw browser weergegeven. 

5. Klik op **maken** in de browser Hallo en enkele nieuwe taken in uw app van de lijst taak maken.

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account en voer een app met Hallo API voor MongoDB. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB voor Hallo MongoDB-API](mongodb-migrate.md)

