---
title: 'Azure Cosmos DB: Hoe kan ik query uitvoert met behulp van de API DocumentDB? | Microsoft Docs'
description: Meer informatie over query met de DocumentDB-API voor Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="bed3a-104">Azure Cosmos DB: Hoe kan ik query met de API voor MongoDB?</span><span class="sxs-lookup"><span data-stu-id="bed3a-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="bed3a-105">De Azure DB die Cosmos [API voor MongoDB](mongodb-introduction.md) ondersteunt [MongoDB shell-query's](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="bed3a-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="bed3a-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="bed3a-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bed3a-107">Een query met MongoDB</span><span class="sxs-lookup"><span data-stu-id="bed3a-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="bed3a-108">Voorbeelddocument</span><span class="sxs-lookup"><span data-stu-id="bed3a-108">Sample document</span></span>

<span data-ttu-id="bed3a-109">De query's in dit artikel gebruikt het volgende voorbeelddocument.</span><span class="sxs-lookup"><span data-stu-id="bed3a-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="bed3a-110"><a id="examplequery1"></a>Voorbeeldquery 1</span><span class="sxs-lookup"><span data-stu-id="bed3a-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="bed3a-111">Het voorbeeld familie document bovenstaande gegeven, de volgende query retourneert de documenten waarbij het veld id overeenkomt met `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="bed3a-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="bed3a-112">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="bed3a-113">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="bed3a-114"><a id="examplequery2"></a>Voorbeeldquery 2</span><span class="sxs-lookup"><span data-stu-id="bed3a-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="bed3a-115">De volgende query retourneert alle onderliggende objecten in de familie.</span><span class="sxs-lookup"><span data-stu-id="bed3a-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="bed3a-116">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="bed3a-117">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="bed3a-118"><a id="examplequery3"></a>Voorbeeldquery 3</span><span class="sxs-lookup"><span data-stu-id="bed3a-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="bed3a-119">De volgende query retourneert alle families die zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="bed3a-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="bed3a-120">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="bed3a-121">**Resultaten** geen document wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bed3a-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="bed3a-122"><a id="examplequery4"></a>Voorbeeldquery 4</span><span class="sxs-lookup"><span data-stu-id="bed3a-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="bed3a-123">De volgende query retourneert alle families die niet zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="bed3a-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="bed3a-124">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="bed3a-125">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="bed3a-126">}</span><span class="sxs-lookup"><span data-stu-id="bed3a-126">}</span></span>

## <span data-ttu-id="bed3a-127"><a id="examplequery5"></a>Voorbeeldquery 5</span><span class="sxs-lookup"><span data-stu-id="bed3a-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="bed3a-128">De volgende query retourneert de families die niet zijn geregistreerd en status NY.</span><span class="sxs-lookup"><span data-stu-id="bed3a-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="bed3a-129">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="bed3a-130">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="bed3a-131">}</span><span class="sxs-lookup"><span data-stu-id="bed3a-131">}</span></span>


## <span data-ttu-id="bed3a-132"><a id="examplequery6"></a>Voorbeeldquery 6</span><span class="sxs-lookup"><span data-stu-id="bed3a-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="bed3a-133">De volgende query retourneert alle families waar kinderen cijfers 8 zijn.</span><span class="sxs-lookup"><span data-stu-id="bed3a-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="bed3a-134">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="bed3a-135">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="bed3a-136">}</span><span class="sxs-lookup"><span data-stu-id="bed3a-136">}</span></span>

## <span data-ttu-id="bed3a-137"><a id="examplequery7"></a>Voorbeeldquery 7</span><span class="sxs-lookup"><span data-stu-id="bed3a-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="bed3a-138">De volgende query retourneert alle families waarbij de grootte van onderliggende matrix 3 is.</span><span class="sxs-lookup"><span data-stu-id="bed3a-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="bed3a-139">**Query**</span><span class="sxs-lookup"><span data-stu-id="bed3a-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="bed3a-140">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="bed3a-140">**Results**</span></span>

<span data-ttu-id="bed3a-141">Er zijn geen resultaten geretourneerd als er geen meer dan 2 onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="bed3a-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="bed3a-142">Alleen gebruikt als parameter 2 wordt deze query mislukt en wordt het volledige document retourneren.</span><span class="sxs-lookup"><span data-stu-id="bed3a-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bed3a-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bed3a-143">Next steps</span></span>

<span data-ttu-id="bed3a-144">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="bed3a-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bed3a-145">Hebt geleerd hoe u een query uitvoert met behulp van MongoDB</span><span class="sxs-lookup"><span data-stu-id="bed3a-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="bed3a-146">U kunt nu doorgaan met de volgende zelfstudie voor informatie over het distribueren van uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="bed3a-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bed3a-147">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="bed3a-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

