---
title: 'Azure Cosmos DB: Hoe DocumentDB API met behulp van tooquery Hallo? | Microsoft Docs'
description: Meer informatie over tooquery Hello DocumentDB-API voor Azure Cosmos-DB
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
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="af474-104">Azure Cosmos DB: Hoe tooquery met API voor MongoDB?</span><span class="sxs-lookup"><span data-stu-id="af474-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="af474-105">Hello Azure Cosmos DB [API voor MongoDB](mongodb-introduction.md) ondersteunt [MongoDB shell-query's](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="af474-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="af474-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="af474-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="af474-107">Een query met MongoDB</span><span class="sxs-lookup"><span data-stu-id="af474-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="af474-108">Voorbeelddocument</span><span class="sxs-lookup"><span data-stu-id="af474-108">Sample document</span></span>

<span data-ttu-id="af474-109">Hallo-query's in dit artikel gebruiken Hallo voorbeelddocument te volgen.</span><span class="sxs-lookup"><span data-stu-id="af474-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="af474-110"><a id="examplequery1"></a>Voorbeeldquery 1</span><span class="sxs-lookup"><span data-stu-id="af474-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="af474-111">Hallo voorbeeld familie document bovenstaande gegeven, Hallo volgende retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met opvragen `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="af474-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="af474-112">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="af474-113">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-113">**Results**</span></span>

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

## <span data-ttu-id="af474-114"><a id="examplequery2"></a>Voorbeeldquery 2</span><span class="sxs-lookup"><span data-stu-id="af474-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="af474-115">de volgende query Hallo retourneert alle Hallo onderliggende in Hallo-familie.</span><span class="sxs-lookup"><span data-stu-id="af474-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="af474-116">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="af474-117">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-117">**Results**</span></span>

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


## <span data-ttu-id="af474-118"><a id="examplequery3"></a>Voorbeeldquery 3</span><span class="sxs-lookup"><span data-stu-id="af474-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="af474-119">de volgende query Hallo retourneert alle Hallo families die zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="af474-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="af474-120">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="af474-121">**Resultaten** geen document wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="af474-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="af474-122"><a id="examplequery4"></a>Voorbeeldquery 4</span><span class="sxs-lookup"><span data-stu-id="af474-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="af474-123">de volgende query Hallo retourneert alle Hallo families die niet zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="af474-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="af474-124">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="af474-125">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-125">**Results**</span></span>

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
<span data-ttu-id="af474-126">}</span><span class="sxs-lookup"><span data-stu-id="af474-126">}</span></span>

## <span data-ttu-id="af474-127"><a id="examplequery5"></a>Voorbeeldquery 5</span><span class="sxs-lookup"><span data-stu-id="af474-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="af474-128">de volgende query Hallo retourneert alle Hallo families die niet zijn geregistreerd en de status is NY.</span><span class="sxs-lookup"><span data-stu-id="af474-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="af474-129">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="af474-130">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-130">**Results**</span></span>

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
<span data-ttu-id="af474-131">}</span><span class="sxs-lookup"><span data-stu-id="af474-131">}</span></span>


## <span data-ttu-id="af474-132"><a id="examplequery6"></a>Voorbeeldquery 6</span><span class="sxs-lookup"><span data-stu-id="af474-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="af474-133">de volgende query Hallo retourneert alle Hallo families waar kinderen cijfers 8 zijn.</span><span class="sxs-lookup"><span data-stu-id="af474-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="af474-134">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="af474-135">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-135">**Results**</span></span>

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
<span data-ttu-id="af474-136">}</span><span class="sxs-lookup"><span data-stu-id="af474-136">}</span></span>

## <span data-ttu-id="af474-137"><a id="examplequery7"></a>Voorbeeldquery 7</span><span class="sxs-lookup"><span data-stu-id="af474-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="af474-138">de volgende query Hallo retourneert alle Hallo families waarbij de grootte van onderliggende matrix 3 is.</span><span class="sxs-lookup"><span data-stu-id="af474-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="af474-139">**Query**</span><span class="sxs-lookup"><span data-stu-id="af474-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="af474-140">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="af474-140">**Results**</span></span>

<span data-ttu-id="af474-141">Er zijn geen resultaten geretourneerd als er geen meer dan 2 onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="af474-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="af474-142">Alleen gebruikt als parameter 2 wordt deze query mislukt en wordt het volledige document Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="af474-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af474-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af474-143">Next steps</span></span>

<span data-ttu-id="af474-144">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="af474-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af474-145">Geleerd hoe tooquery met MongoDB</span><span class="sxs-lookup"><span data-stu-id="af474-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="af474-146">U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="af474-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af474-147">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="af474-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

