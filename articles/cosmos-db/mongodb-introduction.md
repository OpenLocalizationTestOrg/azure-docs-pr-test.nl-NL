---
title: 'Inleiding tooAzure Cosmos DB: API voor MongoDB | Microsoft Docs'
description: Informatie over hoe u kunt Azure Cosmos DB toostore en grote hoeveelheden JSON-documenten met behulp van de lage latentie query Hallo populaire OSS MongoDB APIs.
keywords: Wat is MongoDB
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Inleiding tooAzure Cosmos DB: API voor MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) is de wereldwijd gedistribueerde databaseservice met meerdere modellen van Microsoft voor essentiële toepassingen. Biedt Azure Cosmos DB [directe globale distributie](distribute-data-globally.md), [elastisch schalen van doorvoer en opslag](partition-data.md) overal ter wereld, één cijfer milliseconde latenties op Hallo 99th percentiel, [vijf goed gedefinieerde consistentieniveaus](consistency-levels.md), hoge beschikbaarheid, alle back-ups door gegarandeerd [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexeert automatisch gegevens](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) zonder dat u toodeal met schema- en management. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens. 

![Azure Cosmos DB: MongoDB API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Cosmos DB databases kunnen worden gebruikt als gegevensarchief Hallo voor apps die zijn geschreven voor [MongoDB](https://docs.mongodb.com/manual/introduction/). Dit betekent dat met behulp van de bestaande [stuurprogramma's](https://docs.mongodb.org/ecosystem/drivers/), uw toepassing geschreven voor MongoDB kan nu met Cosmos DB communiceren en Cosmos DB databases in plaats van MongoDB-databases gebruiken. In veel gevallen kunt u overschakelen van het gebruik van MongoDB tooCosmos DB door eenvoudigweg een verbindingsreeks. Met deze functionaliteit kunt u gemakkelijk maken en in de MongoDB-databasetoepassingen uitvoeren in hello Azure cloud met Azure Cosmos DB globale verdeling en [uitgebreide toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db), maar blijft toouse bekend vaardigheden en hulpprogramma's voor MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Wat is Hallo voordeel van het gebruik van Azure DB die Cosmos voor MongoDB toepassingen?

**Elastische schaalbare doorvoer en opslag:** eenvoudig omhoog of omlaag uw database MongoDB toomeet uw toepassing moet. Uw gegevens worden opgeslagen op SSD-schijven (Solid State Disks) voor lage voorspelbare latenties. MongoDB-verzamelingen die kunnen worden geschaald toovirtually biedt ondersteuning voor cosmos DB onbeperkte opslaggrootte en ingerichte doorvoer. U kunt schalen Cosmos DB met voorspelbare prestaties naadloos wanneer uw toepassing groeit. 

**Meerdere landen/regio-replicatie:** Cosmos DB repliceert transparant je je hebt gekoppeld aan je account MongoDB, zodat u toodevelop-toepassingen waarvoor globale toegang toodata en tegelijkertijd de wisselwerking tussen tooall regio's consistentie, beschikbaarheid en prestaties, met bijbehorende garanties. Cosmos DB biedt transparante regionale failover multihoming API's, en Hallo mogelijkheid tooelastically scale doorvoer en opslag van verschillende Hallo wereld. Meer informatie [Distribueer gegevens globaal](distribute-data-globally.md).

**Compatibiliteit met MongoDB**: U kunt uw bestaande MongoDB-expertise toepassingscode en tooling. U kunt met behulp van MongoDB toepassingen te ontwikkelen en implementeren tooproduction Hallo volledig met beheerde-globaal gedistribueerde Cosmos-DB-service.

**Er is geen Serverbeheer**: U heb toomanage en schalen van uw MongoDB-databases. Cosmos DB is een volledig beheerde service, wat betekent dat u hebt geen toomanage geen infrastructuur of virtuele Machines zelf. Cosmos DB is beschikbaar in 30 + [Azure-gebieden](https://azure.microsoft.com/regions/services/).

**Instelbare consistentieniveaus:** selecteren uit vijf goed gedefinieerde consistentie niveaus tooachieve optimale balans tussen de consistentie en prestaties. Voor query's en leesbewerkingen biedt Cosmos DB vijf verschillende consistentieniveaus: sterk, gebonden-verouderd, sessie, consistente voorvoegsel en uiteindelijk. Deze gedetailleerde, goed gedefinieerde consistentieniveaus kunt u toomake geluid verschillen tussen de consistentie, beschikbaarheid en latentie. Meer informatie [met behulp van de consistentie niveaus toomaximize beschikbaarheid en prestaties](consistency-levels.md).

**Automatische indexering**: standaard Cosmos DB automatisch geïndexeerd alle Hallo eigenschappen in documenten in de MongoDB-database en niet verwacht of vereist een schema of het maken van secundaire indexen.

**Enterprise hoogwaardige** -Azure Cosmos DB ondersteunt meerdere lokale replica's toodeliver 99,99% beschikbaarheid en gegevensbescherming in Hallo face van lokale en regionale fouten. Azure Cosmos DB heeft enterprise hoogwaardige [naleving certificeringen](https://www.microsoft.com/trustcenter) en beveiligingsfuncties. 

Meer informatie in deze Azure video met Scott Hanselman en Azure Cosmos DB Principal Engineering Manager, Kirill Gavrylyuk vrijdag.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Hoe tooget gestart

Ga als volgt Hallo MongoDB snelstartgidsen toocreate een Cosmos-DB-account en migreren van uw bestaande Mongo DB toepassing toouse Cosmos DB of bouwen van een nieuwe:

* [Migreren van een bestaande Node.js MongoDB-web-app](create-mongodb-nodejs.md).
* [Een web-App voor MongoDB-API met .NET- en hello Azure-portal](create-mongodb-dotnet.md)
* [Maken van een console-app van de MongoDB-API met Java en hello Azure-portal](create-mongodb-java.md)

## <a name="next-steps"></a>Volgende stappen

Informatie over Azure Cosmos DB MongoDB-API is geïntegreerd in Hallo algemene Azure Cosmos DB-documentatie, maar hier zijn enkele aanwijzers tooget u gestart:

* Ga als volgt Hallo [tooa MongoDB-account koppelen](connect-mongodb-account.md) zelfstudie toolearn hoe tooget verbindingsreeksgegevens account.
* Ga als volgt Hallo [MongoChef voor gebruik met Azure Cosmos DB](mongodb-mongochef.md) zelfstudie toolearn hoe toocreate een verbinding tussen uw Azure DB die Cosmos-database en de MongoDB-app in MongoChef.
* Ga als volgt Hallo [migreren van gegevens tooAzure Cosmos DB met protocolondersteuning voor MongoDB](mongodb-migrate.md) zelfstudie tooimport uw gegevens tooan API voor MongoDB-database.
* Verbinding maken met de API voor het gebruik van MongoDB-account tooan [Robomongo](mongodb-robomongo.md).
* Meer informatie over hoeveel RUs van uw bewerkingen met Hallo gebruikmaakt [GetLastRequestStatistics opdracht en Azure portal metrische gegevens Hallo](request-units.md#GetLastRequestStatistics).
* Meer informatie over hoe te[lezen voorkeuren voor globaal gedistribueerde apps configureren](../cosmos-db/tutorial-global-distribution-mongodb.md).
