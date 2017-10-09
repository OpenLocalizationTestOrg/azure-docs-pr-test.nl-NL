---
title: aaaIntroduction tooAzure Cosmos DB | Microsoft Docs
description: Lees hier alles over Azure Cosmos DB. Deze wereldwijd gedistribueerde database met meerdere modellen is gebouwd voor lage latentie, elastische schaalbaarheid en hoge beschikbaarheid.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Welkom tooAzure Cosmos-DB

Azure Cosmos DB is de wereldwijd gedistribueerde database van Microsoft met meerdere modellen. Met Hallo op een knop te klikken, Azure Cosmos DB Hiermee kunt u tooelastically en onafhankelijk van elkaar schalen doorvoer en opslag op een willekeurig aantal Azure regio. De oplossing biedt gegarandeerde doorvoer, latentie, beschikbaarheid en consistentie, vastgelegd in uitgebreide [serviceovereenkomsten](https://aka.ms/acdbsla) (SLA's), iets wat geen andere databaseservice kan bieden.

![Azure Cosmos DB is de service van Microsoft voor wereldwijd gedistribueerde databases met mogelijkheden voor elastisch uitschalen, een gegarandeerde lage latentie, vijf consistentiemodellen en uitgebreide, gegarandeerde SLA's](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Oplossingen die profiteren van Azure Cosmos DB

Alle [web, mobiel, games en IoT-toepassingen](use-cases.md) die toohandle enorme hoeveelheden lees- en schrijfbewerkingen op moet een [globale](distribute-data-globally.md) schalen met een lage responstijden voor een verscheidenheid aan gegevens van Azure Cosmos DB profiteren [gegarandeerd](https://azure.microsoft.com/support/legal/sla/cosmos-db/) beschikbaarheid, hoge doorvoer, lage latentie en instelbare consistentie.

## <a name="key-capabilities"></a>Belangrijkste mogelijkheden
Als een globaal gedistribueerde database-service biedt Azure Cosmos DB Hallo mogelijkheden toohelp u schaalbare, uiterst responsieve toepassingen bouwen te volgen:

* **Kant-en-klare wereldwijde distributie**
    * U kunt [distribueren van uw gegevens](distribute-data-globally.md) tooany aantal [Azure-regio's](https://azure.microsoft.com/regions/), Hello [klikt u op een knop](tutorial-global-distribution-documentdb.md). Hierdoor kunt u tooput uw gegevens waar uw gebruikers zijn, de laagst mogelijke latentie Hallo tooyour klanten zodat. 
    * Met behulp van Azure Cosmos DB weet multihoming API's, Hallo app altijd waarbij Hallo dichtstbijzijnde regio en stuurt aanvragen toohello dichtstbijzijnde datacentrum. Dit alles is mogelijk zonder wijzigingen config, instellen van uw regio schrijven en veel gebieden gelezen als u wilt en Hallo rest wordt afgehandeld.

* **Meerdere gegevensmodellen en populaire API's voor het raadplegen en opvragen van gegevens**
    * Hallo atom recordreeks van (ARS) gebaseerde gegevensmodel dat Azure Cosmos DB is gebaseerd op systeemeigen ondersteuning biedt voor meerdere gegevensmodellen, met inbegrip van maar niet beperkt toodocument, grafiek, sleutel / waarde-, table en kolomgegevens modellen.
    * API's voor Hallo gegevensmodellen te volgen worden met SDK's beschikbaar in meerdere talen ondersteund:
        * [DocumentDB-API](documentdb-introduction.md)
        * [MongoDB-API](mongodb-introduction.md)
        * [Tabel-API](table-introduction.md)
        * [Grafiek-API (Gremlin)](graph-introduction.md)
        * Aanvullende gegevensmodellen komen binnenkort beschikbaar 

* **Doorvoer en opslag op aanvraag elastisch schalen, waar ook ter wereld**
    * U kunt databasedoorvoer op eenvoudige wijze schalen met de granulatie [per seconde](request-units.md) en de instelling op elk gewenst moment wijzigen. 
    * Grootte van de opslagruimte schalen [transparant en automatisch](partition-data.md) toohandle uw vereisten grootte nu en permanent verloren.

* **Zeer responsieve en bedrijfskritische toepassingen bouwen**
    * Azure Cosmos DB wordt gegarandeerd dat de lage latentie end-to-end op Hallo 99th percentiel tooits klanten. 
    * Voor een typische 1 KB-artikel, Cosmos DB wordt gegarandeerd dat de latentie end-to-end van leesbewerkingen onder 10 ms en geïndexeerde schrijfbewerkingen onder 15 ms op Hallo 99th percentiel, Hallo binnen dezelfde Azure-regio. Hallo mediaan latenties zijn aanzienlijk minder (onder 5 ms).

* **Zorgen voor vrijwel volledige beschikbaarheid**
    * Beschikbaarheid van 99,99% binnen één regio.
    * Aantal tooany implementeren [Azure-regio's](https://azure.microsoft.com/regions) voor hogere beschikbaarheid.
    * U kunt zonder gegevensverlies [een storing simuleren](regional-failover.md) in een of meer regio's. 

* **Schrijven globaal gedistribueerde toepassingen hello manier rechts**
    * Vijf [consistentie modellen](consistency-levels.md) -modellen bieden een breed scala aan sterke SQL-achtige consistentie alle Hallo manier tooNoSQL-achtige uiteindelijke consistentie en elke ding ertussen. 
  
* **Niet-goed-geld-teruggarantie**
    * Uw gegevens komen razendsnel op de plaats van bestemming of u krijgt uw geld terug. 
    * [Serviceovereenkomsten](https://aka.ms/acdbsla) voor beschikbaarheid, latentie, doorvoer en consistentie. 

* **Geen databaseschema/indexbeheer**
    * U hoeft zich geen zorgen meer te maken of uw databaseschema en indexen nog synchroon zijn met uw toepassingsschema. We maken namelijk geen gebruik van schema's. 
    * Database-engine van Azure Cosmos-database is volledig schema networkdirect – indexeert automatisch alle Hallo gegevens het opgenomen zonder dat een schema of indexen en fungeert razendsnelle snelle query's. 

* **Lage eigendomskosten**
    * Vijfmaal tooten [rendabeler](https://aka.ms/cosmos-db-tco-paper) dan een niet-beheerde oplossing.
    * Drie keer goedkoper dan DynamoDB.

## <a name="capability-comparison"></a>Vergelijking van functionaliteit

Azure Cosmos DB biedt de beste mogelijkheden Hallo van relationele en niet-relationele databases.

| Functionaliteit | Relationele databases   | Niet-relationele databases (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Wereldwijde distributie | Nee | Nee | Ja, kant-en-klare distributie in meer dan 30 regio's met multihoming-API's|
| Horizontaal schalen | Nee | Ja | Ja, u kunt doorvoer en opslag onafhankelijk van elkaar schalen | 
| Gegarandeerde latentie | Nee | Ja | Ja, 99% van de leesbewerkingen in < 10 ms en van de schrijfbewerkingen in < 15 ms | 
| Hoge beschikbaarheid | Nee | Ja | Ja, Cosmos DB is altijd ingeschakeld, beschikt over PACELC-tradeoffs, en biedt opties voor automatische en handmatige failover|
| Gegevensmodel + API | Relationeel + SQL | Meerdere modellen + OSS-API | Meerdere modellen + SQL + OSS-API (binnenkort meer) |
| SLA's | Ja | Nee | Ja, uitgebreide SLA's voor latentie, doorvoer, consistentie en beschikbaarheid |


## <a name="next-steps"></a>Volgende stappen
Lees onze snelstartgidsen om snel aan de slag te gaan met Azure Cosmos DB:

* [Aan de slag met de DocumentDB-API van Azure Cosmos DB](create-documentdb-dotnet.md)
* [Aan de slag met de MongoDB-API van Azure Cosmos DB](create-mongodb-nodejs.md)
* [Aan de slag met de grafiek-API van Azure Cosmos DB](create-graph-dotnet.md)
* [Aan de slag met de tabel-API van Azure Cosmos DB](create-table-dotnet.md)
