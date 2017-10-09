---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor DocumentDB-API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo DocumentDB-API.
services: cosmos-db
keywords: globale distributie, documentdb
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo DocumentDB-API

In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo DocumentDB-API.

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Configureren van de algemene distributie op basis van Hallo [DocumentDB APIs](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>De voorkeursregio tooa hello DocumentDB API met verbinding te maken

In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven. Dit kan worden gedaan door in te stellen Hallo verbindingsbeleid. Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst opgegeven, Hallo meeste optimale eindpunt wordt gekozen door Hallo DocumentDB SDK tooperform operations lezen en schrijven.

Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de Hallo DocumentDB SDK's. Hallo SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.

Hallo SDK worden automatisch alle schrijfbewerkingen toohello huidige schrijven regio verzonden.

De eerste beschikbare regio toohello wordt alle leesbewerkingen verzonden in Hallo PreferredLocations lijst. Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort.

Hallo SDK's proberen enkel tooread uit Hallo regio's die zijn opgegeven in PreferredLocations. Dus bijvoorbeeld kunnen als Hallo databaseaccount beschikbaar in drie gebieden is, maar het Hallo-client alleen twee Hallo niet schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten Hallo schrijven regio, zelfs in geval van Hallo van failover.

Hallo-toepassing kunt Hallo huidige schrijven endpoint controleren en lezen eindpunt gekozen door Hallo SDK door te controleren of twee eigenschappen WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger.

Als Hallo PreferredLocations-eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.

## <a name="net-sdk"></a>.NET SDK
Hallo SDK kan worden gebruikt zonder codewijzigingen. In dit geval Hallo SDK automatisch wordt verwezen beide leest en schrijft toohello huidige schrijven regio.

In versie 1.8 en hoger van .NET SDK hello heeft Hallo ConnectionPolicy parameter voor Hallo DocumentClient constructor de eigenschap Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations aangeroepen. Deze eigenschap is van het type verzameling `<string>` en een lijst met regionamen moeten bevatten. Hallo tekenreekswaarden zijn geformatteerd per Hallo regionaam kolom op Hallo [Azure-gebieden] [ regions] pagina, zonder spaties vóór of na Hallo eerste en laatste teken respectievelijk.

Hallo huidige schrijven en lezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.WriteEndpoint en DocumentClient.ReadEndpoint.

> [!NOTE]
> Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten. Hallo-service kan deze op elk gewenst moment bijwerken. Hallo SDK verwerkt deze wijziging automatisch.
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS, JavaScript en Python SDK 's
Hallo SDK kan worden gebruikt zonder codewijzigingen. In dit geval Hallo die SDK automatisch wordt doorverwezen zowel leest en schrijft toohello huidige schrijven regio.

In versie 1.8 en hoger van elke SDK Hallo ConnectionPolicy parameter voor Hallo DocumentClient constructor een nieuwe eigenschap DocumentClient.ConnectionPolicy.PreferredLocations aangeroepen. Dit is de parameter is een matrix met tekenreeksen die een lijst met regionamen neemt. Hallo-namen zijn geformatteerd per Hallo regionaam kolom in Hallo [Azure-gebieden] [ regions] pagina. U kunt ook vooraf gedefinieerde Hallo constanten in Hallo gemak object AzureDocuments.Regions gebruiken

Hallo huidige schrijven en lezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.getWriteEndpoint en DocumentClient.getReadEndpoint.

> [!NOTE]
> Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten. Hallo-service kan deze op elk gewenst moment bijwerken. Hallo SDK wordt deze wijziging automatisch verwerkt.
>
>

Hieronder volgt een voorbeeld van code voor NodeJS/Javascript. Python en Java Hallo volgen hetzelfde patroon.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Zodra een databaseaccount beschikbaar is gesteld in meerdere regio's, kunnen clients de beschikbaarheid opvragen door het uitvoeren van een aanvraag voor ophalen op Hallo URI te volgen.

    https://{databaseaccount}.documents.azure.com/

Hallo-service retourneert een lijst met regio's en hun bijbehorende Azure DB die Cosmos-eindpunt URI's voor Hallo replica's. Hallo huidige schrijven regio wordt aangegeven in het Hallo-antwoord. Hallo-client kan vervolgens als volgt selecteren Hallo juiste eindpunt voor alle verdere REST-API-aanvragen.

Voorbeeld van een antwoord

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* PUT, POST en DELETE-aanvragen moeten gaan toohello aangegeven schrijven URI
* Alle opgehaald en andere aanvragen (bijvoorbeeld query's) met het kenmerk alleen-lezen gaat tooany eindpunt van de keuze van Hallo client

Schrijven tooread alleen-lezen regio's aanvragen mislukt met foutcode HTTP 403 ('verboden').

Als Hallo schrijven regio wordt gewijzigd na schrijft Hallo-client de initiële detectie fase daaropvolgende toohello vorige schrijven regio mislukt met foutcode HTTP 403 ('verboden'). Hallo-client vervolgens krijgt Hallo lijst met regio's opnieuw tooget Hallo bijgewerkte schrijven regio.

Dat is, die in deze zelfstudie is voltooid. U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md). En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Globale distributie op basis van Hallo DocumentDB APIs configureren

U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.

> [!div class="nextstepaction"]
> [Lokaal ontwikkelen met Hallo emulator](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

