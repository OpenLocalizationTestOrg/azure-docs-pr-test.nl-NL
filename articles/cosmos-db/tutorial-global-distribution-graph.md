---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor Graph API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo Graph API.
services: cosmos-db
keywords: globale distributie, grafiek, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo Graph API

In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo Graph API (preview).

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Configureren van de algemene distributie op basis van Hallo [Graph API's](graph-introduction.md) (preview)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Verbinding maken met Hallo Graph API Hallo .NET SDK met de voorkeursregio tooa

Hallo Graph API wordt weergegeven als een extensiebibliotheek boven op Hallo DocumentDB SDK.

In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven. Dit kan worden gedaan door in te stellen Hallo verbindingsbeleid. Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst opgegeven, Hallo meeste optimale eindpunt wordt gekozen door Hallo SDK tooperform schrijven en lees-en schrijfopdrachten.

Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de Hallo SDK's. Hallo SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.

* **Schrijft**: Hallo SDK automatisch naar alle verzonden wordt schrijft toohello huidige schrijven regio.
* **Leest**: alle leesbewerkingen worden de eerste beschikbare regio toohello in Hallo PreferredLocations lijst verzonden. Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort. Hallo SDK's proberen enkel tooread uit Hallo regio's die zijn opgegeven in PreferredLocations. Dus bijvoorbeeld kunnen als Hallo Cosmos-DB-account beschikbaar in drie gebieden is, maar het Hallo-client alleen twee Hallo niet schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten Hallo schrijven regio, zelfs in geval van Hallo van failover.

Hallo-toepassing kunt Hallo huidige schrijven endpoint controleren en lezen eindpunt gekozen door Hallo SDK door te controleren of twee eigenschappen WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger. Als Hallo PreferredLocations-eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.

### <a name="using-hello-sdk"></a>Met behulp van Hallo SDK

Bijvoorbeeld in Hallo .NET SDK, Hallo `ConnectionPolicy` parameter voor Hallo `DocumentClient` constructor heeft een eigenschap genaamd `PreferredLocations`. Deze eigenschap kan worden ingesteld als tooa lijst met regionamen. Hallo weergeven voor de namen van [Azure-gebieden] [ regions] kan worden opgegeven als onderdeel van `PreferredLocations`.

> [!NOTE]
> Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten. Hallo-service kan deze op elk gewenst moment bijwerken. Hallo SDK verwerkt deze wijziging automatisch.
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

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

