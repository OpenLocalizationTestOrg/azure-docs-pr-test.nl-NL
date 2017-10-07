---
title: aaaStore ongestructureerde gegevens met behulp van Azure Functions en Cosmos-DB
description: Ongestructureerde gegevens opslaan met behulp van Azure Functions en Cosmos DB
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: Azure Functions, functies, gebeurtenisverwerking, Cosmos DB, dynamisch berekenen, architectuur zonder server
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Ongestructureerde gegevens opslaan met behulp van Azure Functions en Cosmos DB

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is een uitstekende manier toostore ongestructureerde en JSON-gegevens. Cosmos DB biedt, in combinatie met Azure Functions, een snelle en eenvoudige manier om gegevens op te slaan met veel minder code dan nodig is voor het opslaan van gegevens in een relationele database.

Azure Functions geeft invoer en uitvoer bindingen u een declaratieve manier tooconnect tooexternal servicegegevens uit een functie. In dit onderwerp informatie over hoe tooupdate een bestaande C# functioneren tooadd een uitvoer-binding die niet-gestructureerde gegevens opslaat in een Cosmos-DB-document. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Een uitvoerbinding toevoegen

1. Vouw de functie-app en de functie uit.

1. Selecteer **integreren** en **+ nieuw uitvoer**, die is op Hallo rechts op de pagina Hallo top. Kies **Azure Cosmos DB**, en klik op **Selecteren**.

    ![Een Cosmos DB-uitvoerbinding toevoegen](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Gebruik Hallo **Azure Cosmos DB uitvoer** instellingen zoals opgegeven in de tabel Hallo: 

    ![Cosmos DB-uitvoerbinding configureren](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Instelling      | Voorgestelde waarde  | Beschrijving                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Parameternaam van document** | taskDocument | De naam die toohello Cosmos-DB-object in de code verwijst. |
    | **Databasenaam** | taskDatabase | Naam van de database toosave documenten. |
    | **Naam van verzameling** | TaskCollection | Naam van verzameling met Cosmos DB-databases. |
    | **Indien waar, maakt Hallo Cosmos-DB-database en verzameling** | Geselecteerd | Hallo-verzameling niet al bestaat, zodat deze maken. |

4. Selecteer **nieuw** volgende toohello **Cosmos document databaseverbinding** label en selecteer **+ nieuw**. 

5. Gebruik Hallo **nieuwe account** instellingen zoals opgegeven in de tabel Hallo: 

    ![Cosmos DB-verbinding configureren](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Instelling      | Voorgestelde waarde  | Beschrijving                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **ID** | Naam van de database | Unieke ID voor de database van Hallo Cosmos-DB  |
    | **API** | SQL (DocumentDB) | Hallo document database API selecteren.  |
    | **Abonnement** | Azure-abonnement | Azure-abonnement  |
    | **Resourcegroep** | myResourceGroup |  Hallo bestaande resourcegroep gebruiken die uw app functie bevat. |
    | **Locatie**  | West-Europa | Selecteer een locatie in de buurt tooeither uw functie-app of tooother-apps die gebruikmaken van Hallo opgeslagen documenten.  |

6. Klik op **OK** toocreate Hallo-database. Het duurt enkele minuten toocreate Hallo-database. Nadat het Hallo-database is gemaakt, wordt Hallo databaseverbindingsreeks opgeslagen als een functie app-instelling. Hallo-naam van deze appinstelling wordt ingevoegd in **Cosmos-DB-account verbinding**. 
 
8. Nadat het Hallo-verbindingsreeks is ingesteld, selecteert u **opslaan** toocreate Hallo binding.

## <a name="update-hello-function-code"></a>Hallo functiecode bijwerken

Hallo bestaande C# functiecode vervangen door Hallo code te volgen:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
Dit codevoorbeeld Hallo HTTP-aanvraag queryreeksen leest en wijst deze toofields in Hallo `taskDocument` object. Hallo `taskDocument` binding stuurt Hallo objectgegevens uit deze binding parameter toobe opgeslagen in Hallo gebonden documentdatabase. Hallo-database wordt gemaakt van Hallo eerst Hallo-functie wordt uitgevoerd.

## <a name="test-hello-function-and-database"></a>Test Hallo functie en de database

1. Vouw het rechtervenster Hallo en selecteer **Test**. Onder **Query**, klikt u op **+ parameter toevoegen** en voeg de volgende parameters toohello queryreeks Hallo:

    + `name`
    + `task`
    + `duedate`

2. Klik op **Uitvoeren** en controleer of een 200-status wordt geretourneerd.

    ![Cosmos DB-uitvoerbinding configureren](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. Vouw Hallo pictogram-balk op Hallo linkerkant Hallo Azure-portal, type `cosmos` in Hallo zoeken veld en selecteert u een **Azure Cosmos DB**.

    ![Zoeken naar Hallo Cosmos-DB-service](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Selecteer Hallo-database die u hebt gemaakt, selecteer vervolgens **Data Explorer**. Vouw Hallo **verzamelingen** knooppunten, selecteer Nieuw document Hallo en Bevestig dat document Hallo uw tekenreekswaarden query samen met enkele aanvullende metagegevens bevat. 

    ![Cosmos DB-vermelding controleren](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

U hebt een binding tooyour HTTP-trigger die niet-gestructureerde gegevens in een Cosmos-DB-database opslaat toegevoegd.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Zie voor meer informatie over binding tooa Cosmos DB database [bindingen van Azure Functions Cosmos DB](functions-bindings-documentdb.md).
