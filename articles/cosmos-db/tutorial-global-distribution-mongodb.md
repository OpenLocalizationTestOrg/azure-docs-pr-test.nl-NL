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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="99e90-104">Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="99e90-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="99e90-105">In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo MongoDB-API.</span><span class="sxs-lookup"><span data-stu-id="99e90-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="99e90-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="99e90-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="99e90-107">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="99e90-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="99e90-108">Configureren van de algemene distributie op basis van Hallo [MongoDB-API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="99e90-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="99e90-109">Verifiëren van de regionale instellingen met behulp van Hallo MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="99e90-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="99e90-110">de eenvoudigste manier Hallo van uw globale configuratie binnen API controleren voor MongoDB toorun Hallo is dubbel *isMaster()* opdracht Hallo Mongo-Shell.</span><span class="sxs-lookup"><span data-stu-id="99e90-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="99e90-111">Vanuit de Mongo-Shell:</span><span class="sxs-lookup"><span data-stu-id="99e90-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="99e90-112">Voorbeeld van resultaten:</span><span class="sxs-lookup"><span data-stu-id="99e90-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="99e90-113">Verbinding maken met tooa voorkeursregio met Hallo MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="99e90-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="99e90-114">Hallo MongoDB-API kunt u toospecify lezen voorkeur voor een globaal gedistribueerde database voor uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="99e90-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="99e90-115">Voor beide lage latentie leest en globale hoge beschikbaarheid, wordt aangeraden uw verzameling lezen voorkeur te stellen*dichtstbijzijnde*.</span><span class="sxs-lookup"><span data-stu-id="99e90-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="99e90-116">Een voorkeur voor het lezen *dichtstbijzijnde* geconfigureerde tooread van Hallo dichtstbijzijnde regio is.</span><span class="sxs-lookup"><span data-stu-id="99e90-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="99e90-117">Voor toepassingen met een primaire lezen/schrijven regio en een secundaire regio voor noodherstel (DR) scenario's, wordt aangeraden dat uw verzameling lezen voorkeur te stellen*secundaire voorkeur*.</span><span class="sxs-lookup"><span data-stu-id="99e90-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="99e90-118">Een voorkeur voor het lezen *secundaire voorkeur* geconfigureerde tooread van de secundaire regio Hallo is wanneer Hallo primaire regio niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="99e90-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="99e90-119">Ten slotte, als zoals toomanually u uw lezen regio's geeft.</span><span class="sxs-lookup"><span data-stu-id="99e90-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="99e90-120">Hallo regio Tag kunt u binnen uw voorkeur lezen instellen.</span><span class="sxs-lookup"><span data-stu-id="99e90-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="99e90-121">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="99e90-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="99e90-122">U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="99e90-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="99e90-123">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="99e90-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e90-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99e90-124">Next steps</span></span>

<span data-ttu-id="99e90-125">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="99e90-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99e90-126">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="99e90-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="99e90-127">Globale distributie op basis van Hallo DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="99e90-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="99e90-128">U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="99e90-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99e90-129">Lokaal ontwikkelen met Hallo emulator</span><span class="sxs-lookup"><span data-stu-id="99e90-129">Develop locally with hello emulator</span></span>](local-emulator.md)
