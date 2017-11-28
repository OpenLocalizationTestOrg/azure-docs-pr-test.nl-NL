---
title: aaaHow tooquery grafiekgegevens in Azure Cosmos DB? | Microsoft Docs
description: Meer informatie over tooquery grafiekgegevens in Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="2d264-104">Azure Cosmos DB: Hoe tooquery met Hallo Graph API (preview)?</span><span class="sxs-lookup"><span data-stu-id="2d264-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="2d264-105">Hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) ondersteunt [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) query's.</span><span class="sxs-lookup"><span data-stu-id="2d264-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="2d264-106">In dit artikel biedt voorbeelddocumenten en query's tooget die u gestart.</span><span class="sxs-lookup"><span data-stu-id="2d264-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="2d264-107">De verwijzing naar een gedetailleerde Gremlin wordt verstrekt in Hallo [Gremlin ondersteuning](gremlin-support.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2d264-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="2d264-108">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d264-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2d264-109">Een query met Gremlin</span><span class="sxs-lookup"><span data-stu-id="2d264-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d264-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2d264-110">Prerequisites</span></span>

<span data-ttu-id="2d264-111">Voor deze toowork query's moet u een Azure DB die Cosmos-account hebt en grafiekgegevens in Hallo container hebt.</span><span class="sxs-lookup"><span data-stu-id="2d264-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="2d264-112">Geen van deze?</span><span class="sxs-lookup"><span data-stu-id="2d264-112">Don't have any of those?</span></span> <span data-ttu-id="2d264-113">Volledige Hallo [5 minuten Quick Start](create-graph-dotnet.md) of Hallo [developer-zelfstudie](tutorial-query-graph.md) toocreate een account en vul uw database.</span><span class="sxs-lookup"><span data-stu-id="2d264-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="2d264-114">U kunt uitvoeren na query's op basis van Hallo Hallo [Azure Cosmos DB .NET graph-bibliotheek](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), of uw favoriete Gremlin-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="2d264-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="2d264-115">Aantal hoekpunten in Hallo-grafiek</span><span class="sxs-lookup"><span data-stu-id="2d264-115">Count vertices in hello graph</span></span>

<span data-ttu-id="2d264-116">Hallo volgende fragment toont hoe toocount aantal hoekpunten in de grafiek Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="2d264-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="2d264-117">Filters</span><span class="sxs-lookup"><span data-stu-id="2d264-117">Filters</span></span>

<span data-ttu-id="2d264-118">U kunt uitvoeren met behulp van Gremlin filters `has` en `hasLabel` stappen en deze te combineren met `and`, `or`, en `not` toobuild complexer filtert.</span><span class="sxs-lookup"><span data-stu-id="2d264-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="2d264-119">Azure Cosmos DB biedt schema networkdirect indexeren van alle eigenschappen in uw hoekpunten en graden voor snelle query's:</span><span class="sxs-lookup"><span data-stu-id="2d264-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="2d264-120">Projectie</span><span class="sxs-lookup"><span data-stu-id="2d264-120">Projection</span></span>

<span data-ttu-id="2d264-121">U kunt bepaalde eigenschappen in queryresultaten Hallo Hallo met projecteren `values` stap:</span><span class="sxs-lookup"><span data-stu-id="2d264-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="2d264-122">Verwante randen en hoekpunten zoeken</span><span class="sxs-lookup"><span data-stu-id="2d264-122">Find related edges and vertices</span></span>

<span data-ttu-id="2d264-123">Tot nu toe hebt we alleen query's die in elke database werken gezien.</span><span class="sxs-lookup"><span data-stu-id="2d264-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="2d264-124">Grafieken zijn snelle en efficiënte voor traversal bewerkingen wanneer u toonavigate toorelated randen en hoekpunten nodig.</span><span class="sxs-lookup"><span data-stu-id="2d264-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="2d264-125">We vinden alle vrienden of van Thomas.</span><span class="sxs-lookup"><span data-stu-id="2d264-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="2d264-126">We doen dit met behulp van Gremlin `outE` toofind alle Hallo uitgaande van Thomas randen stap en klik vervolgens in hoekpunten toohello doorlopen van de randen van Gremlin met `inV` stap:</span><span class="sxs-lookup"><span data-stu-id="2d264-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="2d264-127">de volgende query Hallo voert twee hops toofind alle Thomas 'vrienden of van vrienden ', door het aanroepen van `outE` en `inV` twee keer.</span><span class="sxs-lookup"><span data-stu-id="2d264-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="2d264-128">Kunt u complexere query's maken en implementeren van krachtige grafiek traversal logica met Gremlin, inclusief groeperen filter expressies uitvoeren met behulp van lussen Hallo `loop` stap en uitvoering voorwaardelijke navigatie met Hallo `choose` stap.</span><span class="sxs-lookup"><span data-stu-id="2d264-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="2d264-129">Meer informatie over wat u met doen kunt [Gremlin ondersteuning](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="2d264-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d264-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d264-130">Next steps</span></span>

<span data-ttu-id="2d264-131">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="2d264-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d264-132">Geleerd hoe tooquery met behulp van de grafiek</span><span class="sxs-lookup"><span data-stu-id="2d264-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="2d264-133">U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="2d264-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d264-134">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="2d264-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)