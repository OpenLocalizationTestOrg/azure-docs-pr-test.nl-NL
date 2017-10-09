---
title: 'Azure Cosmos DB: een web-app ontwikkelen met Xamarin en Facebook-authenticatie | Microsoft-documenten'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query uitvoeren op Azure Cosmos-DB
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: een web-app ontwikkelen met .NET, Xamarin, en Facebook-authenticatie

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal. U moet vervolgens bouwen en implementeren van een WebApp voor takenlijstjes gebouwd op Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), en hello Azure Cosmos DB autorisatie-engine. Hallo todo lijst web-app implementeert een per gebruiker gegevenspatroon waarmee gebruikers toologin met Facebook Auth en beheren hun eigen toodo-items.

## <a name="prerequisites"></a>Vereisten

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

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
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Open vervolgens Hallo DocumentDBTodo.sln bestand uit Hallo samples/xamarin/UserItems/xamarin.forms map in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

Hallo-code in Hallo Xamarin map bevat:

* Xamarin-app. Hallo app slaat van Hallo gebruiker todo-items in een gepartitioneerde verzameling met de naam UserItems.
* Resourcetokenbroker-API. Een eenvoudige ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello aangemelde gebruikers van Hallo-app. Resource-tokens zijn tijdelijke toegangstokens waarmee Hallo app Hallo toegang toohello gegevens van een gebruiker aangemeld.

Hallo-verificatie en de gegevensstroom wordt weergegeven in Hallo diagram hieronder.

* Hallo UserItems verzameling is gemaakt met de partitiesleutel Hallo ' / userid'. Het opgeven van dat een partitiesleutel voor een verzameling kunt u Azure Cosmos DB tooscale oneindig als Hallo aantal gebruikers en items groeit.
* Hallo Xamarin-app kan gebruikers toologin met Facebook-referenties.
* Hallo Xamarin-app maakt gebruik van Facebook access token tooauthenticate met ResourceTokenBroker API
* Hallo resource token broker API verifieert Hallo-aanvraag met de App Service Auth-functie en vraagt een token van de resource Azure Cosmos DB met lezen/schrijven toegang tooall documenten delen partitiesleutel Hallo geverifieerde gebruiker.
* Resource token broker retourneert Hallo resource token toohello client-app.
* Hallo-app heeft toegang tot van Hallo gebruiker todo-items met Hallo resource-token.

![Taken-app met voorbeeldgegevens](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. U gebruikt in Web.config-bestand in de volgende stap Hallo HALLO hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel.

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-xamarin-dotnet/keys.png)

2. Open in Visual Studio-2017 Hallo Web.config-bestand in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker map. 

3. Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo-waarde van Hallo accountUrl in Web.config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en maken het Hallo-waarde van Hallo accountKey in Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

## <a name="build-and-deploy-hello-web-app"></a>Hallo-web-app bouwen en implementeren

1. In hello Azure-portal, maakt u een App Service-website toohost Hallo Resource token broker API.
2. Open in hello Azure-portal, Hallo App-instellingen blade van Hallo Resource token broker API-website. Vul Hallo volgende app-instellingen:

    * accountUrl - hello Azure Cosmos DB account-URL op Hallo sleutels tabblad van uw Azure DB die Cosmos-account.
    * accountKey - hello Azure Cosmos DB account hoofdsleutel Hallo sleutels tabblad van uw Azure DB die Cosmos-account.
    * databaseId en collectionId van de database en verzameling die u hebt gemaakt

3. Publiceer Hallo ResourceTokenBroker oplossing tooyour website gemaakt.

4. Open Hallo Xamarin-project en tooTodoItemManager.cs navigeren. Hallo-waarden voor accountURL, collectionId, databaseId, evenals resourceTokenBrokerURL vult als Hallo base https-url voor Hallo resource token broker website.

5. Volledige Hallo [hoe tooconfigure uw App Service-toepassing toouse Facebook aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) zelfstudie toosetup Facebook verificatie Hallo ResourceTokenBroker-website configureert.

    Hallo Xamarin-app uitvoeren.

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen: 

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van Hallo-resource die u zojuist hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en bouwen en implementeren van een Xamarin-app. U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB](import-data.md)
