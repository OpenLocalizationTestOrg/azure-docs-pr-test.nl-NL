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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: Hoe tooquery met SQL?

Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) ondersteunt het uitvoeren van query's documenten met behulp van SQL. Dit artikel bevat een voorbeelddocument en twee voorbeeld SQL-query's en resultaten.

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Opvragen van gegevens met behulp van SQL

## <a name="sample-document"></a>Voorbeelddocument

Hallo SQL-query's in dit artikel gebruiken Hallo voorbeelddocument te volgen.

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
## <a name="where-can-i-run-sql-queries"></a>Waar kan ik SQL-query's uitvoeren?

U kunt query's met behulp van Hallo Data Explorer in hello Azure-portal via Hallo uitvoeren [REST-API en SDK's](documentdb-sdk-dotnet.md), en zelfs Hallo [queryspeelplaats](https://www.documentdb.com/sql/demo), die query's wordt uitgevoerd op een bestaande set met voorbeeldgegevens.

Zie voor meer informatie over SQL-query's:
* [SQL-query en SQL-syntaxis](documentdb-sql-query.md)

## <a name="prerequisites"></a>Vereisten

Deze zelfstudie wordt ervan uitgegaan dat u hebt een Azure DB die Cosmos-account en een verzameling. Geen van deze? Volledige Hallo [5 minuten Quick Start](create-mongodb-nodejs.md) of Hallo [developer-zelfstudie](tutorial-develop-mongodb.md) toocreate een account en een verzameling.

## <a name="example-query-1"></a>Voorbeeldquery 1

Hallo voorbeeld familie document bovenstaande gegeven, volgende SQL-query retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met `WakefieldFamily`. Omdat het een `SELECT *` Hallo-uitvoer van Hallo query-instructie is Hallo voltooid JSON-document:

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Resultaten**

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

## <a name="example-query-2"></a>Voorbeeldquery 2

de volgende query Hallo retourneert alle Hallo opgegeven namen van kinderen in Hallo familie-id die overeenkomt met `WakefieldFamily` hun hoogwaardige geordend.

**Query**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Resultaten**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Geleerd hoe tooquery met behulp van SQL  

U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.

> [!div class="nextstepaction"]
> [Uw gegevens globaal distribueren](tutorial-global-distribution-documentdb.md)

