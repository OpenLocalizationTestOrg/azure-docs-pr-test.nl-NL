---
title: Zelfstudie voor Azure DB Cosmos globale distributie voor MongoDB-API | Microsoft Docs
description: Informatie over het instellen van Azure DB die Cosmos globale distributie op basis van de MongoDB-API.
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="498a3-104">Het instellen van Azure DB die Cosmos globale distributie op basis van de MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="498a3-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="498a3-105">In dit artikel, laten we zien hoe de Azure portal instellen van Azure DB die Cosmos globale distributie en vervolgens verbinding met de MongoDB-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="498a3-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="498a3-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="498a3-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="498a3-107">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="498a3-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="498a3-108">Configureren globale distributie met behulp van de [MongoDB-API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="498a3-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="498a3-109">Verifiëren van de regionale instellingen met de MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="498a3-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="498a3-110">De eenvoudigste manier van dubbele uw globale configuratie binnen API controleren voor MongoDB om uit te voeren, is de *isMaster()* opdracht van de Mongo-Shell.</span><span class="sxs-lookup"><span data-stu-id="498a3-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="498a3-111">Vanuit de Mongo-Shell:</span><span class="sxs-lookup"><span data-stu-id="498a3-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="498a3-112">Voorbeeld van resultaten:</span><span class="sxs-lookup"><span data-stu-id="498a3-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="498a3-113">Verbinding maken met een voorkeursregio met de MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="498a3-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="498a3-114">De MongoDB-API kunt u uw verzameling lezen voorkeur voor een globaal gedistribueerde database opgeven.</span><span class="sxs-lookup"><span data-stu-id="498a3-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="498a3-115">Voor beide lage latentie leest en globale hoge beschikbaarheid, wordt aangeraden uw verzameling lezen voorkeur instelt op *dichtstbijzijnde*.</span><span class="sxs-lookup"><span data-stu-id="498a3-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="498a3-116">Een voorkeur voor het lezen *dichtstbijzijnde* is geconfigureerd voor het lezen van de dichtstbijzijnde regio.</span><span class="sxs-lookup"><span data-stu-id="498a3-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="498a3-117">Voor toepassingen met een primaire lezen/schrijven regio en een secundaire regio voor noodherstel (DR) scenario's, wordt aangeraden dat uw verzameling lezen voorkeur instelt op *secundaire voorkeur*.</span><span class="sxs-lookup"><span data-stu-id="498a3-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="498a3-118">Een voorkeur voor het lezen *secundaire voorkeur* is geconfigureerd voor het lezen van de secundaire regio als de primaire regio niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="498a3-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="498a3-119">Als u handmatig wilt ten slotte uw lezen gebieden opgeven.</span><span class="sxs-lookup"><span data-stu-id="498a3-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="498a3-120">U kunt de regio Tag binnen uw voorkeur lezen instellen.</span><span class="sxs-lookup"><span data-stu-id="498a3-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="498a3-121">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="498a3-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="498a3-122">U kunt informatie over het beheren van de consistentie van uw account globaal gerepliceerde door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="498a3-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="498a3-123">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="498a3-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="498a3-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="498a3-124">Next steps</span></span>

<span data-ttu-id="498a3-125">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="498a3-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="498a3-126">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="498a3-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="498a3-127">Globale distributie op basis van de DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="498a3-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="498a3-128">U kunt nu doorgaan met de volgende zelfstudie voor meer informatie over het ontwikkelen van lokaal via de lokale Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="498a3-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="498a3-129">Lokaal ontwikkelen met de emulator</span><span class="sxs-lookup"><span data-stu-id="498a3-129">Develop locally with the emulator</span></span>](local-emulator.md)