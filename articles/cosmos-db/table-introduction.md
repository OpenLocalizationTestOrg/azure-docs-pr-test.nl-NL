---
title: aaaIntroduction tooAzure Cosmos DB van tabel API | Microsoft Docs
description: Informatie over het gebruik van Azure DB die Cosmos toostore en grote hoeveelheden gegevens met behulp van de lage latentie sleutel / waarde-query Hallo populaire OSS MongoDB APIs.
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Inleiding tooAzure Cosmos DB: tabel-API

[Azure Cosmos DB](introduction.md) is de wereldwijd gedistribueerde databaseservice met meerdere modellen van Microsoft voor essentiële toepassingen. Biedt Azure Cosmos DB [directe globale distributie](distribute-data-globally.md), [elastisch schalen van doorvoer en opslag](partition-data.md) overal ter wereld, één cijfer milliseconde latenties op Hallo 99th percentiel, [vijf goed gedefinieerde consistentieniveaus](consistency-levels.md), hoge beschikbaarheid, alle back-ups door gegarandeerd [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexeert automatisch gegevens](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) zonder dat u toodeal met schema- en management. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens. 

![Azure-tabelopslag-API en Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Azure Cosmos DB biedt Hallo tabel-API (preview) voor toepassingen die een sleutel-waardearchief met flexibele schema, voorspelbare prestaties, wereldwijde distributie en hoge doorvoersnelheid nodig. Hallo tabel API biedt Hallo dezelfde functionaliteit als Azure Table storage, maar maakt gebruik van Hallo voordelen van hello Azure Cosmos DB-engine. 

Toouse Azure Table storage voor tabellen met hoge opslag en lagere doorvoer vereisten kan worden voortgezet. Ondersteuning voor tabellen geoptimaliseerd voor opslag in een toekomstige update leidt tot Azure Cosmos DB en bestaande en nieuwe Azure Table storage-accounts worden bijgewerkt tooAzure Cosmos DB.

## <a name="premium-and-standard-table-apis"></a>Premium- en Standard-table-API's
Als u Azure Table storage momenteel gebruikt, kunt u krijgen Hallo volgende voordelen tooAzure Cosmos DB 'tabel premium' preview worden verplaatst:

|  | Azure-tabelopslag | Azure Cosmos DB: tabelopslag (preview-versie) |
| --- | --- | --- |
| Latentie | Snel, maar geen bovengrens voor latentie | Latentie voor lees- en schrijfbewerkingen, één cijfer milliseconde back met < 10 ms latentie leest en < 15 ms latentie schrijft op Hallo 99th percentiel, op elke schaal, overal ter wereld Hallo |
| Doorvoer | Zeer schaalbaar, maar zonder model op basis van toegewezen doorvoer. Tabellen hebben een schaalbaarheidslimiet van 20.000 bewerkingen/sec | Zeer schaalbaar met [toegewezen gereserveerde doorvoer per tabel](request-units.md), op basis van serviceovereenkomsten. Accounts hebben geen bovengrens voor doorvoer en bieden ondersteuning voor > 10 miljoen bewerkingen/sec per tabel |
| Wereldwijde distributie | Eén regio met één optioneel leesbaar secundair leesgebied voor hoge beschikbaarheid. U kunt geen failover starten | [Directe globale distributie](distribute-data-globally.md) uit één too30 + regio's, ondersteuning voor [automatische en handmatige failover](regional-failover.md) op elk gewenst moment, overal ter wereld Hallo |
| Indexeren | Alleen primaire index op PartitionKey en RowKey. Geen secundaire indexen | Automatische en volledige indexering voor alle eigenschappen, geen indexbeheer |
| Query’s uitvoeren | Voor de queryuitvoering wordt een index gebruikt als primaire sleutel. In andere gevallen wordt er gescand. | Query's kunnen profiteren van de automatische indexering van eigenschappen voor een snelle uitvoertijden van query's. De database-engine van Azure Cosmos DB ondersteunt samenvoegingen, georuimtelijke bewerkingen en sorteren. |
| Consistentie | Sterk binnen primaire regio. Uiteindelijk met secundaire regio | [Vijf goed gedefinieerde consistentieniveaus](consistency-levels.md) tootrade uit beschikbaarheid, latentie, doorvoer en consistentie op basis van de behoeften van uw toepassing |
| Prijzen | Geoptimaliseerd voor opslag  | Geoptimaliseerd voor doorvoer |
| SLA's | 99,9 % beschikbaarheid | 99,99% beschikbaarheid binnen één regio en de mogelijkheid tooadd meer regio's voor hogere beschikbaarheid. [Toonaangevende uitgebreide serviceovereenkomsten ](https://azure.microsoft.com/support/legal/sla/cosmos-db/) op algemene beschikbaarheid |

## <a name="how-tooget-started"></a>Hoe tooget gestart

Een Azure DB die Cosmos-account maken in Hallo [Azure-portal](https://portal.azure.com), en aan de slag met onze [Quick Start voor tabel-API met .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Volgende stappen

Hier volgen enkele aanwijzers tooget u gestart:
* [Een .NET-toepassing hello tabel API met bouwen](create-table-dotnet.md)
* [Ontwikkelen met Hallo tabel API in .NET](tutorial-develop-table-dotnet.md)
* [Een query over tabelgegevens met behulp van Hallo tabel API](tutorial-query-table.md)
* [Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo tabel-API](tutorial-global-distribution-table.md)
* [Inleiding tot Azure Cosmos DB Table-API SDK voor .NET](table-sdk-dotnet.md)
