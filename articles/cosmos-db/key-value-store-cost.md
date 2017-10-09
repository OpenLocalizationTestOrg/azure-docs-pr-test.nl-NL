---
title: "aaaAzure Cosmos-database als een winkel sleutelwaarde – kosten overzicht | Microsoft Docs"
description: Meer informatie over Hallo lage kosten van het gebruik van Azure DB die Cosmos als een winkel sleutelwaarde.
keywords: sleutel-waardearchief
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos-database als een winkel sleutelwaarde – kosten-overzicht

Azure Cosmos-database is een globaal gedistribueerd en modellen database-service voor het bouwen van maximaal beschikbare, grote schaal toepassingen eenvoudig. Standaard indexeert Azure Cosmos DB automatisch alle Hallo gegevens efficiënt opgenomen. Hierdoor kunnen snel en consistent [SQL](documentdb-sql-query.md) (en [JavaScript](programming.md)) query's op alle soorten gegevens. 

Dit artikel beschrijft Hallo kosten van Azure DB die Cosmos voor eenvoudige schrijven en leesbewerkingen wanneer deze wordt gebruikt als een sleutel/waarde-archief. Schrijven bewerkingen behoren invoeg-, vervangt, verwijderingen en upserts van documenten. Naast het 99,99% beschikbaarheid te garanderen, biedt Azure Cosmos DB gegarandeerd < 10 ms latentie voor leesbewerkingen en < 15 ms latentie voor Hallo (geïndexeerd) schrijft respectievelijk op Hallo 99th percentiel. 

## <a name="why-we-use-request-units-rus"></a>Waarom we Aanvraageenheden (RUs) gebruiken

Prestaties van Azure DB Cosmos is gebaseerd op Hallo hoeveelheid ingerichte [Aanvraageenheden](request-units.md) (RU) voor Hallo-partitie. Hallo-inrichting is een tweede samenvattingen en is gekocht in RUs per seconde en RUs/min ([niet toobe verward met Hallo per uur facturering](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs moeten worden beschouwd als een andere vereenvoudigt Hallo inrichting van vereiste doorvoer voor de toepassing hello valuta. Onze klanten geen toothink van de verschillen tussen lezen en schrijven capaciteitseenheden. Hallo één valuta model van RUs maakt efficiëntie tooshare Hallo ingerichte capaciteit tussen lees- en schrijfbewerkingen. Dit Capaciteitsmodel ingerichte stelt Hallo service tooprovide een voorspelbare en consistente doorvoer, lage latentie en hoge beschikbaarheid worden gegarandeerd. Ten slotte gebruiken we RU toomodel doorvoer, maar elke ingerichte RU heeft ook een gedefinieerde hoeveelheid resources (geheugen, Core). RU per seconde is niet alleen IOPS.

Als een systeem globaal gedistribueerde database is Cosmos DB Hallo alleen Azure-service die voorziet in een SLA op latentie, doorvoer en consistentie in toevoeging toohigh beschikbaarheid. Hallo-doorvoer die u inricht is toegepaste tooeach van Hallo regio's die zijn gekoppeld aan uw databaseaccount Cosmos DB. Cosmos DB biedt voor leesbewerkingen meerdere, goed gedefinieerde [consistentieniveaus](consistency-levels.md) voor toochoose uit. 

Hallo volgende tabel ziet u Hallo aantal RUs vereist tooperform lezen en schrijven op basis van de grootte van het document van 1KB en 100KBs transacties.

|De grootte van artikel|1 lezen|1 schrijven|
|-------------|------|-------|
|1 KB|1 RU|5 RUs|
|100 KB|10 RUs|50 RUs|

## <a name="cost-of-reads-and-writes"></a>Kosten van lees- en schrijfbewerkingen

Als u 1000 RU per seconde inricht, moet dit bedragen too3.6m RU per uur en kost $0.08 Hallo uur (in Hallo VS en Europa). Voor een document van de grootte van 1KB dit betekent dat u 3,6 m leesbewerkingen gebruiken kan of 0.72m schrijft (3.6mRU / 5) met behulp van de ingerichte doorvoer. Genormaliseerde toomillion leest en schrijft, Hallo kosten zou $0,022 /m leesbewerkingen ($0.08 / 3,6) en $0.111/ m schrijft ($0.08 / 0.72). Hallo kosten per miljoen minimale zoals weergegeven in onderstaande tabel voor hello wordt.

|De grootte van artikel|1m lezen|1m schrijven|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|


De meeste Hallo basic blob of object winkels services kosten $0,40 per miljoen lezen transactie en $5 per transactie miljoen schrijven. Als u optimaal gebruikt, mag Cosmos DB too98% goedkoper dan deze andere oplossingen (van 1KB transacties).

## <a name="next-steps"></a>Volgende stappen

Bezoek ons regelmatig voor nieuwe artikelen voor het optimaliseren van Azure DB die Cosmos resources worden ingericht. In die tijd Hallo van mening bent dat gratis toouse onze [RU Rekenmachine](https://www.documentdb.com/capacityplanner).

