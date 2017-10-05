---
title: Hoe query SQL in Azure Cosmos DB? | Microsoft Docs
description: Informatie over query's uitvoeren met gegevens van de DocumentDB SQL in Azure Cosmos-DB
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="ebfb9-104">Azure Cosmos DB: Hoe kan ik query uitvoert met behulp van SQL?</span><span class="sxs-lookup"><span data-stu-id="ebfb9-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="ebfb9-105">De Azure DB die Cosmos [DocumentDB API](documentdb-introduction.md) ondersteunt het uitvoeren van query's documenten met behulp van SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="ebfb9-106">Dit artikel bevat een voorbeelddocument en twee voorbeeld SQL-query's en resultaten.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="ebfb9-107">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="ebfb9-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ebfb9-108">Opvragen van gegevens met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="ebfb9-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="ebfb9-109">Voorbeelddocument</span><span class="sxs-lookup"><span data-stu-id="ebfb9-109">Sample document</span></span>

<span data-ttu-id="ebfb9-110">De SQL-query's in dit artikel gebruikt het volgende voorbeelddocument.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="ebfb9-111">Waar kan ik SQL-query's uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="ebfb9-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="ebfb9-112">U kunt query's met de gegevensverkenner in de Azure portal via uitvoeren de [REST-API en SDK's](documentdb-sdk-dotnet.md), en zelfs de [queryspeelplaats](https://www.documentdb.com/sql/demo), die query's wordt uitgevoerd op een bestaande set met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="ebfb9-113">Zie voor meer informatie over SQL-query's:</span><span class="sxs-lookup"><span data-stu-id="ebfb9-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="ebfb9-114">SQL-query en SQL-syntaxis</span><span class="sxs-lookup"><span data-stu-id="ebfb9-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="ebfb9-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ebfb9-115">Prerequisites</span></span>

<span data-ttu-id="ebfb9-116">Deze zelfstudie wordt ervan uitgegaan dat u hebt een Azure DB die Cosmos-account en een verzameling.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="ebfb9-117">Geen van deze?</span><span class="sxs-lookup"><span data-stu-id="ebfb9-117">Don't have any of those?</span></span> <span data-ttu-id="ebfb9-118">Voltooi de [5 minuten Quick Start](create-mongodb-nodejs.md) of de [developer-zelfstudie](tutorial-develop-mongodb.md) voor het maken van een account en een verzameling.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="ebfb9-119">Voorbeeldquery 1</span><span class="sxs-lookup"><span data-stu-id="ebfb9-119">Example query 1</span></span>

<span data-ttu-id="ebfb9-120">Het voorbeeld familie document bovenstaande gegeven, volgende SQL-query retourneert de documenten waarbij het veld id overeenkomt met `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="ebfb9-121">Omdat het een `SELECT *` de uitvoer van de query-instructie is de volledige JSON-document:</span><span class="sxs-lookup"><span data-stu-id="ebfb9-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="ebfb9-122">**Query**</span><span class="sxs-lookup"><span data-stu-id="ebfb9-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="ebfb9-123">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ebfb9-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="ebfb9-124">Voorbeeldquery 2</span><span class="sxs-lookup"><span data-stu-id="ebfb9-124">Example query 2</span></span>

<span data-ttu-id="ebfb9-125">De volgende query retourneert de opgegeven namen van onderliggende items in de familie-id die overeenkomt met `WakefieldFamily` hun hoogwaardige geordend.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="ebfb9-126">**Query**</span><span class="sxs-lookup"><span data-stu-id="ebfb9-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="ebfb9-127">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ebfb9-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="ebfb9-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebfb9-128">Next steps</span></span>

<span data-ttu-id="ebfb9-129">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="ebfb9-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebfb9-130">Hebt geleerd hoe u een query uitvoert met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="ebfb9-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="ebfb9-131">U kunt nu doorgaan met de volgende zelfstudie voor informatie over het distribueren van uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="ebfb9-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebfb9-132">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="ebfb9-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

