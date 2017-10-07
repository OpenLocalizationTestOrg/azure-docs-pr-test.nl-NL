---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor MongoDB-API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo MongoDB-API.
services: cosmos-db
keywords: globale distributie, MongoDB
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo MongoDB-API

In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo MongoDB-API.

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Configureren van de algemene distributie op basis van Hallo [MongoDB-API](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Verifiëren van de regionale instellingen met behulp van Hallo MongoDB-API
de eenvoudigste manier Hallo van uw globale configuratie binnen API controleren voor MongoDB toorun Hallo is dubbel *isMaster()* opdracht Hallo Mongo-Shell.

Vanuit de Mongo-Shell:

   ```
      db.isMaster()
   ```
   
Voorbeeld van resultaten:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Verbinding maken met tooa voorkeursregio met Hallo MongoDB-API

Hallo MongoDB-API kunt u toospecify lezen voorkeur voor een globaal gedistribueerde database voor uw verzameling. Voor beide lage latentie leest en globale hoge beschikbaarheid, wordt aangeraden uw verzameling lezen voorkeur te stellen*dichtstbijzijnde*. Een voorkeur voor het lezen *dichtstbijzijnde* geconfigureerde tooread van Hallo dichtstbijzijnde regio is.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Voor toepassingen met een primaire lezen/schrijven regio en een secundaire regio voor noodherstel (DR) scenario's, wordt aangeraden dat uw verzameling lezen voorkeur te stellen*secundaire voorkeur*. Een voorkeur voor het lezen *secundaire voorkeur* geconfigureerde tooread van de secundaire regio Hallo is wanneer Hallo primaire regio niet beschikbaar is.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Ten slotte, als zoals toomanually u uw lezen regio's geeft. Hallo regio Tag kunt u binnen uw voorkeur lezen instellen.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
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
