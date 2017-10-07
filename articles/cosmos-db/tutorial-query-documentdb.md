---
title: aaaHow tooquery SQL in Azure Cosmos DB? | Microsoft Docs
description: Meer informatie over tooquery met gegevens van de DocumentDB SQL in Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="b22a7-104">Azure Cosmos DB: Hoe tooquery met SQL?</span><span class="sxs-lookup"><span data-stu-id="b22a7-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="b22a7-105">Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) ondersteunt het uitvoeren van query's documenten met behulp van SQL.</span><span class="sxs-lookup"><span data-stu-id="b22a7-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="b22a7-106">Dit artikel bevat een voorbeelddocument en twee voorbeeld SQL-query's en resultaten.</span><span class="sxs-lookup"><span data-stu-id="b22a7-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="b22a7-107">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b22a7-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b22a7-108">Opvragen van gegevens met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="b22a7-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="b22a7-109">Voorbeelddocument</span><span class="sxs-lookup"><span data-stu-id="b22a7-109">Sample document</span></span>

<span data-ttu-id="b22a7-110">Hallo SQL-query's in dit artikel gebruiken Hallo voorbeelddocument te volgen.</span><span class="sxs-lookup"><span data-stu-id="b22a7-110">hello SQL queries in this article use hello following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="b22a7-111">Waar kan ik SQL-query's uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="b22a7-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="b22a7-112">U kunt query's met behulp van Hallo Data Explorer in hello Azure-portal via Hallo uitvoeren [REST-API en SDK's](documentdb-sdk-dotnet.md), en zelfs Hallo [queryspeelplaats](https://www.documentdb.com/sql/demo), die query's wordt uitgevoerd op een bestaande set met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="b22a7-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="b22a7-113">Zie voor meer informatie over SQL-query's:</span><span class="sxs-lookup"><span data-stu-id="b22a7-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="b22a7-114">SQL-query en SQL-syntaxis</span><span class="sxs-lookup"><span data-stu-id="b22a7-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="b22a7-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b22a7-115">Prerequisites</span></span>

<span data-ttu-id="b22a7-116">Deze zelfstudie wordt ervan uitgegaan dat u hebt een Azure DB die Cosmos-account en een verzameling.</span><span class="sxs-lookup"><span data-stu-id="b22a7-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="b22a7-117">Geen van deze?</span><span class="sxs-lookup"><span data-stu-id="b22a7-117">Don't have any of those?</span></span> <span data-ttu-id="b22a7-118">Volledige Hallo [5 minuten Quick Start](create-mongodb-nodejs.md) of Hallo [developer-zelfstudie](tutorial-develop-mongodb.md) toocreate een account en een verzameling.</span><span class="sxs-lookup"><span data-stu-id="b22a7-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="b22a7-119">Voorbeeldquery 1</span><span class="sxs-lookup"><span data-stu-id="b22a7-119">Example query 1</span></span>

<span data-ttu-id="b22a7-120">Hallo voorbeeld familie document bovenstaande gegeven, volgende SQL-query retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="b22a7-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="b22a7-121">Omdat het een `SELECT *` Hallo-uitvoer van Hallo query-instructie is Hallo voltooid JSON-document:</span><span class="sxs-lookup"><span data-stu-id="b22a7-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="b22a7-122">**Query**</span><span class="sxs-lookup"><span data-stu-id="b22a7-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="b22a7-123">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="b22a7-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="b22a7-124">Voorbeeldquery 2</span><span class="sxs-lookup"><span data-stu-id="b22a7-124">Example query 2</span></span>

<span data-ttu-id="b22a7-125">de volgende query Hallo retourneert alle Hallo opgegeven namen van kinderen in Hallo familie-id die overeenkomt met `WakefieldFamily` hun hoogwaardige geordend.</span><span class="sxs-lookup"><span data-stu-id="b22a7-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="b22a7-126">**Query**</span><span class="sxs-lookup"><span data-stu-id="b22a7-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="b22a7-127">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="b22a7-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="b22a7-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b22a7-128">Next steps</span></span>

<span data-ttu-id="b22a7-129">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="b22a7-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b22a7-130">Geleerd hoe tooquery met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="b22a7-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="b22a7-131">U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="b22a7-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b22a7-132">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="b22a7-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

