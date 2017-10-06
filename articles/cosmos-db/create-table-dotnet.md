---
title: een Azure Cosmos DB .NET-toepassing gebruikt aaaBuild Hallo tabel-API | Microsoft Docs
description: Aan de slag met de Table-API van Azure Cosmos DB met behulp van .NET
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a>Azure Cosmos DB: Een .NET-toepassing hello tabel API met bouwen

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze snel starten laat zien hoe toocreate een Cosmos Azure DB account en het maken van een tabel in dat account met behulp van hello Azure-portal. U moet vervolgens schrijven van code tooinsert, update en delete-entiteiten en enkele query's met Hallo nieuwe [Windows Azure-opslag Premium Table](https://aka.ms/premiumtablenuget) (preview)-pakket van NuGet. Deze bibliotheek heeft Hallo dezelfde klassen- en handtekeningen als Hallo openbaar [Windows Azure-opslag-SDK](https://www.nuget.org/packages/WindowsAzure.Storage), maar heeft ook Hallo mogelijkheid tooconnect tooAzure Cosmos DB accounts met Hallo [tabel API](table-introduction.md) (preview). 

## <a name="prerequisites"></a>Vereisten

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>Een tabel toevoegen

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>Voorbeeldgegevens toevoegen

U kunt nu gegevens tooyour nieuwe tabel met behulp van Data Explorer (Preview) toevoegen.

1. Vouw in Data Explorer **sample-table** uit, klik op **Entiteiten** en klik vervolgens op **Entiteit toevoegen**.

   ![Maken van nieuwe entiteiten in de Data Explorer in hello Azure-portal](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. Nu gegevens toohello PartitionKey waarde vakken en RowKey waarde toevoegen en klik op **entiteit toevoegen**.

   ![Stel Hallo partitie en sleutel van de rij voor een nieuwe entiteit](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    U kunt nu meer entiteiten tooyour tabel toevoegen, bewerken van uw entiteiten of de gegevens in Data Explorer zoeken. Data Explorer is ook kunt u uw doorvoer schalen en opgeslagen procedures, door de gebruiker gedefinieerde functies en triggers tooyour tabel toevoegen.

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we een tabel-app vanuit github Hallo verbindingsreeks instellen en voer dit klonen. U ziet hoe eenvoudig het is toowork met gegevens via een programma. 

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. Open het oplossingsbestand Hallo in Visual Studio. 

## <a name="review-hello-code"></a>Hallo code bekijken

We maken een kort overzicht van wat in Hallo-app gebeurt er. Het bestand Program.cs Open Hallo en u vindt dat deze regels code hello Azure Cosmos DB resources maken. 

* Hallo CloudTableClient is geïnitialiseerd.

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* Er wordt een nieuwe tabel gemaakt als er nog geen tabel bestaat.

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* Er wordt een nieuwe Table-container gemaakt. Hier ziet u deze code vergelijkbaar tooregular Azure Table storage SDK. 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu ontvangt updates verbindingsreeksgegevens Hallo zodat uw app tooAzure Cosmos DB kan communiceren. 

1. Open in Visual Studio Hallo app.config-bestand. 

2. In Hallo [Azure-portal](http://portal.azure.com/), in hello Azure Cosmos DB navigatiemenu links, klikt u op **verbindingsreeks**. Klik vervolgens in het nieuwe deelvenster Hallo op knop voor het kopiëren voor de verbindingsreeks Hallo Hallo. 

    ![Bekijken en kopiëren Hallo eindpunt en Accountsleutel in Hallo verbindingsreeks deelvenster](./media/create-table-dotnet/keys.png)

3. Hallo-waarde in Hallo app.config-bestand als de waarde Hallo Hallo PremiumStorageConnectionString plakken. 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    U kunt laten Hallo StandardStorageConnectionString is.

U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB. 

## <a name="run-hello-web-app"></a>Hallo-web-app uitvoeren

1. In Visual Studio met de rechtermuisknop op Hallo **PremiumTableGetStarted** project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**. 

2. In Hallo NuGet **Bladeren** in het vak *WindowsAzure.Storage PremiumTable*.

3. Controleer de Hallo **Include prerelease** vak. 

4. Installeren in Hallo resultaten Hallo **WindowsAzure.Storage PremiumTable** bibliotheek. Hiermee installeert u Hallo preview pakket Azure Cosmos DB tabel API, evenals alle afhankelijkheden. Houd er rekening mee dat dit een andere NuGet-pakket dan Hallo Windows Azure Storage-pakket wordt gebruikt door Azure Table storage is. 

5. Klik op CTRL + F5 toorun Hallo-toepassing.

    Hallo-consolevenster weergegeven Hallo gegevens wordt toegevoegd, opgehaald, opgevraagd, vervangen en verwijderd uit de tabel Hallo. Wanneer het Hallo-script is voltooid, drukt u op elke sleutel tooclose Hallo-consolevenster. 
    
    ![Console-uitvoer van Hallo Quick Start](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. Als u wilt dat toosee Hallo nieuwe entiteiten in Data Explorer alleen commentaar regels 188 208 in program.cs zodat ze niet worden verwijderd, Voer Hallo voorbeeld opnieuw. 

    U kunt nu teruggaan tooData Explorer, klikt u op **vernieuwen**, vouw Hallo **mensen** tabel en klik op **entiteiten**, en werk met deze nieuwe gegevens. 

    ![Nieuwe entiteiten in Data Explorer](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Sla's bekijken in hello Azure-portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen: 

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een tabel maken met de Hallo Data Explorer en een app uitvoert.  U kunt nu uw gegevens dankzij Hallo tabel API opvragen.  

> [!div class="nextstepaction"]
> [Query met Hallo tabel-API](tutorial-query-table.md)

