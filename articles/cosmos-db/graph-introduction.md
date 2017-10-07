---
title: Inleiding tooAzure Cosmos DB Graph API's | Microsoft Docs
description: Meer informatie over hoe u kunt Azure Cosmos DB toostore, query en bladeren enorme grafieken met een lage latentie Hallo Hallo Gremlin grafiek query language van Apache TinkerPop gebruiken.
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Inleiding tooAzure Cosmos DB: Graph API

[Azure Cosmos DB](introduction.md) is Hallo globaal gedistribueerd en modellen database-service van Microsoft voor essentiële toepassingen. Biedt Azure Cosmos DB [directe globale distributie](distribute-data-globally.md), [elastisch schalen van doorvoer en opslag](partition-data.md) overal ter wereld, één cijfer milliseconde latenties op Hallo 99th percentiel, [vijf goed gedefinieerde consistentieniveaus](consistency-levels.md), hoge beschikbaarheid, die worden ondersteund door gegarandeerd [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexeert automatisch gegevens](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) zonder dat u toodeal met schema- en management. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens.

![Gremlin grafiek en Azure Cosmos-DB](./media/graph-introduction/graph-gremlin.png)

Hello Azure Cosmos DB Graph API biedt:

- Modellering van de grafiek
- Verandering API 's
- Directe globale distributie
- Elastisch schalen van opslag en doorvoer met minder dan 10 ms lezen latenties en minder dan 15 ms op Hallo 99th percentiel
- Automatisch te indexeren met de beschikbaarheid van de directe query
- Instelbare consistentieniveaus
- Uitgebreide Sla's, met inbegrip van 99,99% beschikbaarheid

tooquery Azure Cosmos DB, kunt u Hallo [Apache TinkerPop](http://tinkerpop.apache.org) graph traversal taal, [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), of andere TinkerPop-compatibele grafiek systemen, zoals [Apache Spark GraphX](spark-connector-graph.md).

Dit artikel biedt een overzicht van hello Azure Cosmos DB Graph API en wordt uitgelegd hoe u kunt deze toostore enorme grafieken miljarden hoekpunten en randen. U kunt query Hallo grafieken met milliseconde latentie en eenvoudig ontwikkelen van Hallo grafiek structuur en -schema.

## <a name="graph-database"></a>Grafiek-database
Gegevens is zoals deze wordt weergegeven in de praktijk Hallo natuurlijk verbonden. Er is een traditionele gegevens modelleren gericht op entiteiten. Voor veel toepassingen er is ook een toomodel nodig of toomodel zowel entiteiten en relaties natuurlijk.

Een [grafiek](http://mathworld.wolfram.com/Graph.html) is een structuur die bestaat uit [hoekpunten](http://mathworld.wolfram.com/GraphVertex.html) en [randen](http://mathworld.wolfram.com/GraphEdge.html). Zowel hoekpunten en randen kunnen een willekeurig aantal eigenschappen hebben. Hoekpunten geven aan afzonderlijke objecten, zoals een persoon, een plaats of een gebeurtenis. Randen geven relaties tussen hoekpunten. Bijvoorbeeld, een persoon mogelijk weet iemand anders, worden betrokken bij een gebeurtenis en onlangs op een locatie. Eigenschappen van snelle informatie over Hallo hoekpunten en randen. Van de Voorbeeldeigenschappen omvatten een hoekpunt met een naam, leeftijd en rand met een tijdstempel en/of een gewicht. Meer formeel dit model wordt ook wel een [eigenschappengrafiek](http://tinkerpop.apache.org/docs/current/reference/#intro). Azure Cosmos DB ondersteunt Hallo eigenschap grafiek model.

Hallo volgende steekproef bijvoorbeeld grafiek toont relaties tussen gebruikers, mobiele apparaten, interesses en besturingssystemen.

![Voorbeelddatabase met personen, apparaten en interesses](./media/graph-introduction/sample-graph.png)

Grafieken zijn nuttig toounderstand een breed scala aan gegevenssets in de wetenschap, technologie en bedrijven. Grafiek-databases kunnen u model en opslaan van grafieken natuurlijk en efficiënt, waardoor ze handig voor veel scenario's. Grafiek-databases zijn meestal NoSQL-databases, omdat deze ook vaak nodig schemaflexibiliteit en snelle herhaling gevallen.

Grafieken bieden een nieuwe en krachtige gegevens techniek modelleren. Maar dit feit zelf is niet een voldoende reden toouse een graph-database. Voor veel gebruiksvoorbeelden en patronen die betrekking hebben op grafiek traversals grafieken leveren betere prestaties dan traditionele SQL en NoSQL-databases met orde van grootte. Dit verschil in prestaties is verder versterkt wanneer meer dan één relatie, zoals vriend van een vriend passeert.

U kunt snelle traversals Hallo die grafiek databases bieden combineren met grafiek algoritmen, zoals Diepte eerste zoeken, brede eerste zoeken, en van Dijkstra algoritme toosolve problemen in verschillende domeinen zoals sociale netwerken, inhoudsbeheer georuimtelijke, en aanbevelingen.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Wereld scale grafieken met Azure Cosmos-DB
Azure Cosmos-database is een volledig beheerde grafiek database biedt wereldwijde distributie elastisch schalen van opslag en doorvoer, automatisch te indexeren en query instelbare consistentieniveaus en ondersteuning voor Hallo TinkerPop standaard.  

![Architectuur van Azure DB Cosmos-grafiek](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure Cosmos-DB biedt de volgende Hallo differentiated mogelijkheden vergelijking tooother grafiek databases in de markt Hallo:

* Elastische schaalbare doorvoer en opslag

 Grafieken in de praktijk Hallo moeten tooscale buiten Hallo-capaciteit van één server. Met Azure Cosmos DB, kunt u uw grafieken probleemloos schalen op meerdere servers. U kunt ook Hallo doorvoer van uw grafiek onafhankelijk op basis van uw toegangspatronen schalen. Azure Cosmos DB ondersteunt graph-databases die kunnen worden geschaald toovirtually onbeperkte opslaggrootte en ingerichte doorvoer.

* Meerdere landen/regio-replicatie

 Azure Cosmos DB repliceert transparant uw grafiek tooall gegevensgebieden die je hebt gekoppeld aan uw account. Replicatie kunt u toodevelop toepassingen waarvoor toodata globale toegang. Er zijn voor-en nadelen in Hallo gebieden van de consistentie, beschikbaarheid, prestaties en en bijbehorende garanties. Azure Cosmos DB biedt transparante regionale failover met multihoming-API's. U kunt schalen doorvoer en opslag op Hallo wereld.

* Snelle query's en traversals met bekende Gremlin syntaxis

 Heterogene hoekpunten en randen opslaan en deze documenten via de syntaxis van een bekend Gremlin opvragen. Azure Cosmos-database maakt gebruik van een uiterst gelijktijdige, vergrendeling vrij, logboek gestructureerde indexering technologie tooautomatically index alle inhoud. Deze mogelijkheid kan uitgebreide realtime query's en traversals zonder Hallo moeten toospecify schemahints, secundaire indexen of weergaven. Meer informatie [Query grafieken met Gremlin](gremlin-support.md).

* Volledig beheerd

 Azure Cosmos DB elimineert Hallo nodig toomanage database- en machineresources. Als een volledig beheerde Microsoft Azure-service, u niet nodig toomanage virtuele machines te doen, implementeren en configureren van software, beheren schalen of bekommeren om complexe gegevenslaag upgrades. Elke grafiek wordt automatisch een back-up en beveiligd tegen regionale fouten. U kunt gemakkelijk een Cosmos-DB Azure-account toevoegen en capaciteit inrichten als u dit nodig zodat u zich kunt richten op uw toepassing in plaats van het besturingssysteem en het beheren van uw database.

* Automatische indexeren

 Standaard Azure Cosmos DB automatisch alle Hallo eigenschappen binnen de knooppunten en randen in de grafiek Hallo geïndexeerd en niet verwacht of vereist een schema of het maken van secundaire indexen.

* Compatibiliteit met Apache TinkerPop

 Azure Cosmos DB Hallo open source Apache TinkerPop standaard ondersteunt systeemeigen en kan worden geïntegreerd met andere systemen grafiek TinkerPop ingeschakeld. Ja, kunt u eenvoudig migreren vanaf een andere grafiek database, zoals Titan of Neo4j, of Azure Cosmos DB met grafiek analytics frameworks zoals [Apache Spark GraphX](spark-connector-graph.md).

* Instelbare consistentieniveaus

 Selecteer in de vijf goed gedefinieerde consistentie niveaus tooachieve optimale balans tussen de consistentie en prestaties. Voor query's en leesbewerkingen biedt Azure Cosmos DB vijf verschillende consistentieniveaus: sterk, gebonden-verouderd, sessie, consistent voorvoegsel en mogelijk. Deze gedetailleerde, goed gedefinieerde consistentieniveaus kunt u toomake geluid voor-en nadelen van de consistentie, beschikbaarheid en latentie. Meer informatie [met behulp van de consistentie niveaus toomaximize beschikbaarheid en prestaties in DocumentDB](consistency-levels.md).

Azure Cosmos DB kunt ook gebruiken om meerdere modellen, zoals documenten en de grafiek, binnen dezelfde containers/databases Hallo. U kunt een verzameling toostore grafiek documentgegevens naast documenten gebruiken. U kunt beide SQL-query's via JSON en Gremlin query's tooquery Hallo dezelfde gegevens als een grafiek.

## <a name="getting-started"></a>Aan de slag
U kunt gebruiken hello Azure-opdrachtregelinterface (CLI), Azure Powershell of Azure-portal met ondersteuning voor graph API toocreate Azure Cosmos DB accounts Hallo. Nadat u de accounts hebt gemaakt, hello Azure portal biedt een service-eindpunt, zoals `https://<youraccount>.graphs.azure.com`, biedt een WebSocket-front-end voor Gremlin. U kunt uw hulpmiddelen TinkerPop-compatibel, zoals Hallo [Gremin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), tooconnect toothis eindpunt en bouwen toepassingen in Java, Node.js of eventuele Gremlin clientstuurprogramma.

Hallo geeft volgende tabel populaire Gremlin stuurprogramma's die u met Azure Cosmos DB gebruiken kunt:

| Downloaden | Documentatie |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin-JavaScript op Github](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin console](https://tinkerpop.apache.org/downloads.html) |[TinkerPop docs](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Azure Cosmos DB biedt ook een .NET-bibliotheek met Gremlin uitbreidingsmethoden boven op Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md) via NuGet. Deze bibliotheek bevat een 'in-process' Gremlin-server waarmee u tooconnect kunt rechtstreeks tooDocumentDB gegevenspartities.

| Downloaden | Documentatie |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Met behulp van Hallo [Azure Cosmos DB Emulator](local-emulator.md), u kunt gebruiken Hallo Graph API toodevelop en lokaal testen zonder te maken van een Azure-abonnement of mogelijke kosten. Wanneer u tevreden bent over hoe uw toepassing in Hallo Emulator werkt, kunt u een Azure DB die Cosmos-account in Hallo cloud toousing overschakelen.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Scenario's voor ondersteuning van Azure DB die Cosmos grafiek
Hier volgen enkele scenario's waar de grafiek ondersteuning van Azure Cosmos-database kan worden gebruikt:

* Sociale netwerken

 Door het combineren van gegevens over uw klanten en hun interacties met andere mensen, kunt u gepersonaliseerde ervaring te ontwikkelen, klant gedrag te voorspellen of mensen communiceren met anderen interesses. Azure Cosmos DB worden gebruikte toomanage sociale netwerken en klantvoorkeuren en gegevens bijhouden.

* Aanbeveling engines

 Dit scenario wordt doorgaans gebruikt in de detailhandel Hallo. U kunt aangepaste aanbevelingen opbouwen door een combinatie van informatie over producten, gebruikers en interactie van gebruikers, zoals aanschaffen, bladeren of een item. lage latentie en elastisch schalen systeemeigen Hallo grafiek ondersteuning van Azure DB die Cosmos is ideaal voor het modelleren van deze bewerkingen.

* Georuimtelijk

 Veel toepassingen in telecommunicatie, logistiek en reizen plannen moeten een locatie van belang zijn binnen een gebied toofind of Hallo kortste/optimale route tussen twee locaties vinden. Azure Cosmos-database is een natuurlijke geschikt is voor deze problemen.

* Internet of Things

 Met Hallo netwerk- en verbindingen tussen gemodelleerd als een grafiek van IoT-apparaten, kunt u beter inzicht te krijgen van de status van uw apparaten en activa Hallo bouwen en meer informatie over hoe wijzigingen in één deel uitmaken van Hallo netwerk mogelijk invloed is op een ander deel.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over de ondersteuning van de grafiek in Azure Cosmos DB, Zie:

* Aan de slag met Hallo [Azure Cosmos DB grafiek zelfstudie](create-graph-dotnet.md).
* Meer informatie over het te[query grafieken in Azure Cosmos DB met Gremlin](gremlin-support.md).
