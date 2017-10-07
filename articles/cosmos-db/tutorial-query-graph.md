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
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Hoe tooquery met Hallo Graph API (preview)?

Hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) ondersteunt [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) query's. In dit artikel biedt voorbeelddocumenten en query's tooget die u gestart. De verwijzing naar een gedetailleerde Gremlin wordt verstrekt in Hallo [Gremlin ondersteuning](gremlin-support.md) artikel.

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Een query met Gremlin

## <a name="prerequisites"></a>Vereisten

Voor deze toowork query's moet u een Azure DB die Cosmos-account hebt en grafiekgegevens in Hallo container hebt. Geen van deze? Volledige Hallo [5 minuten Quick Start](create-graph-dotnet.md) of Hallo [developer-zelfstudie](tutorial-query-graph.md) toocreate een account en vul uw database. U kunt uitvoeren na query's op basis van Hallo Hallo [Azure Cosmos DB .NET graph-bibliotheek](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), of uw favoriete Gremlin-stuurprogramma.

## <a name="count-vertices-in-hello-graph"></a>Aantal hoekpunten in Hallo-grafiek

Hallo volgende fragment toont hoe toocount aantal hoekpunten in de grafiek Hallo Hallo:

```
g.V().count()
```

## <a name="filters"></a>Filters

U kunt uitvoeren met behulp van Gremlin filters `has` en `hasLabel` stappen en deze te combineren met `and`, `or`, en `not` toobuild complexer filtert. Azure Cosmos DB biedt schema networkdirect indexeren van alle eigenschappen in uw hoekpunten en graden voor snelle query's:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projectie

U kunt bepaalde eigenschappen in queryresultaten Hallo Hallo met projecteren `values` stap:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Verwante randen en hoekpunten zoeken

Tot nu toe hebt we alleen query's die in elke database werken gezien. Grafieken zijn snelle en efficiënte voor traversal bewerkingen wanneer u toonavigate toorelated randen en hoekpunten nodig. We vinden alle vrienden of van Thomas. We doen dit met behulp van Gremlin `outE` toofind alle Hallo uitgaande van Thomas randen stap en klik vervolgens in hoekpunten toohello doorlopen van de randen van Gremlin met `inV` stap:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

de volgende query Hallo voert twee hops toofind alle Thomas 'vrienden of van vrienden ', door het aanroepen van `outE` en `inV` twee keer. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Kunt u complexere query's maken en implementeren van krachtige grafiek traversal logica met Gremlin, inclusief groeperen filter expressies uitvoeren met behulp van lussen Hallo `loop` stap en uitvoering voorwaardelijke navigatie met Hallo `choose` stap. Meer informatie over wat u met doen kunt [Gremlin ondersteuning](gremlin-support.md)!

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Geleerd hoe tooquery met behulp van de grafiek 

U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.

> [!div class="nextstepaction"]
> [Uw gegevens globaal distribueren](tutorial-global-distribution-documentdb.md)