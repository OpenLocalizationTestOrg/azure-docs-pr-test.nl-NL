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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB: Hoe tooquery met API voor MongoDB?

Hello Azure Cosmos DB [API voor MongoDB](mongodb-introduction.md) ondersteunt [MongoDB shell-query's](https://docs.mongodb.com/manual/tutorial/query-documents/). 

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Een query met MongoDB

## <a name="sample-document"></a>Voorbeelddocument

Hallo-query's in dit artikel gebruiken Hallo voorbeelddocument te volgen.

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
## <a id="examplequery1"></a>Voorbeeldquery 1 

Hallo voorbeeld familie document bovenstaande gegeven, Hallo volgende retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met opvragen `WakefieldFamily`.

**Query**
    
    db.families.find({ id: “WakefieldFamily”})

**Resultaten**

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

## <a id="examplequery2"></a>Voorbeeldquery 2 

de volgende query Hallo retourneert alle Hallo onderliggende in Hallo-familie. 

**Query**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Resultaten**

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


## <a id="examplequery3"></a>Voorbeeldquery 3 

de volgende query Hallo retourneert alle Hallo families die zijn geregistreerd. 

**Query**
    
    db.families.find( { "isRegistered" : true })
**Resultaten** geen document wordt geretourneerd. 

## <a id="examplequery4"></a>Voorbeeldquery 4

de volgende query Hallo retourneert alle Hallo families die niet zijn geregistreerd. 

**Query**
    
    db.families.find( { "isRegistered" : false })
**Resultaten**

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
}

## <a id="examplequery5"></a>Voorbeeldquery 5

de volgende query Hallo retourneert alle Hallo families die niet zijn geregistreerd en de status is NY. 

**Query**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Resultaten**

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
}


## <a id="examplequery6"></a>Voorbeeldquery 6

de volgende query Hallo retourneert alle Hallo families waar kinderen cijfers 8 zijn.

**Query**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Resultaten**

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
}

## <a id="examplequery7"></a>Voorbeeldquery 7

de volgende query Hallo retourneert alle Hallo families waarbij de grootte van onderliggende matrix 3 is.

**Query**
  
      db.Family.find( {children: { $size:3} } )

**Resultaten**

Er zijn geen resultaten geretourneerd als er geen meer dan 2 onderliggende elementen. Alleen gebruikt als parameter 2 wordt deze query mislukt en wordt het volledige document Hallo retourneren.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Geleerd hoe tooquery met MongoDB 

U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.

> [!div class="nextstepaction"]
> [Uw gegevens globaal distribueren](tutorial-global-distribution-documentdb.md)

