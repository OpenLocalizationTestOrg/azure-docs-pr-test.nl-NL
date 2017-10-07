---
title: aaaAzure Cosmos DB schaal en prestaties testen | Microsoft Docs
description: Meer informatie over hoe tooperform schaal en prestaties testen met Azure Cosmos-DB
keywords: Prestaties testen
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Prestaties en schaal testen met Azure Cosmos-DB
Prestaties en schaal testen is een belangrijke stap in de ontwikkeling van toepassingen. Voor veel toepassingen Hallo databaselaag heeft een aanzienlijke invloed op Hallo van de algehele prestaties en schaalbaarheid en is daarom een essentieel onderdeel van de prestaties van het testen. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is speciaal hiervoor gemaakte voor elastisch schalen en voorspelbare prestaties en daarom een geweldige geschikt voor toepassingen die een krachtige databaselaag moeten. 

In dit artikel is een verwijzing voor ontwikkelaars Cosmos DB evalueren voor hoge prestaties toepassingsscenario's of prestaties testen van suites voor hun Cosmos-DB-werkbelastingen te implementeren. Richt zich voornamelijk op de geïsoleerde prestatietests van Hallo-database, maar bevat ook aanbevolen procedures voor productietoepassingen.

Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:   

* Waar vind ik een voorbeeld .NET client-toepassing voor het testen van de prestaties van de Cosmos-DB 
* Hoe ik hoge doorvoersnelheid niveaus met Cosmos DB van mijn clienttoepassing bereikt?

tooget gestart met code, download Hallo-project uit [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Hallo-doel van deze toepassing is toodemonstrate aanbevolen procedures voor het uitpakken van betere prestaties buiten Cosmos DB met een beperkt aantal clientcomputers. Dit is niet gemaakt toodemonstrate Hallo piek-capaciteit van Hallo-service, die kan worden geschaald onbeperkt.
> 
> 

Als u configuratie clientzijde opties tooimprove Cosmos DB prestaties zoekt, Zie [tips voor betere prestaties van Azure DB die Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Hallo-prestaties testen van de toepassing uitvoeren
Hallo snelste manier tooget gestart is toocompile en Voer Hallo .NET voorbeeldcode hieronder, zoals beschreven in de onderstaande stappen voor Hallo. Ook kunt u de broncode Hallo bekijken en implementeren van vergelijkbare configuraties tooyour eigen clienttoepassingen.

**Stap 1:** Hallo-project downloaden uit [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), of fork Hallo GitHub-opslagplaats.

**Stap 2:** Hallo instellingen wijzigen voor EndpointUrl, AuthorizationKey, CollectionThroughput en DocumentTemplate App.config (optioneel).

> [!NOTE]
> Raadpleeg voor het inrichten van verzamelingen met hoge doorvoer toohello [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate Hallo kosten per verzameling. Azure DB Cosmos facturen opslag en doorvoer onafhankelijk op uurbasis, zodat u kunt u kosten besparen door te verwijderen of te verlagen Hallo doorvoer van uw Azure Cosmos DB verzamelingen nadat u hebt getest.
> 
> 

**Stap 3:** compileren en Hallo console-app uitvoeren vanaf de opdrachtregel Hallo. Hier ziet u uitvoer zoals Hallo volgende:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Stap 4 (indien nodig):** Hallo doorvoer gerapporteerd (RU/s) uit Hallo hulpprogramma moet Hallo dezelfde of hoger is dan Hallo ingerichte doorvoer van Hallo-verzameling. Als dat niet het geval is, toenemende Hallo DegreeOfParallelism in kleine stappen helpen u mogelijk de Hallo limiet is bereikt. Als Hallo doorvoer van uw clientapp plateaus, meerdere exemplaren van Hallo app starten op Hallo van dezelfde of verschillende computers vindt u een limiet is bereikt Hallo ingericht via Hallo verschillende exemplaren. Als u hulp nodig hebt bij deze stap, schrijft u een e-mailbericht tooaskcosmosdb@microsoft.com of een ondersteuningsticket vanuit Hallo bestand [Azure Portal](https://portal.azure.com).

Zodra u Hallo-app die wordt uitgevoerd hebt, kunt u proberen andere [beleid indexeren](indexing-policies.md) en [consistentieniveaus](consistency-levels.md) toounderstand de impact op de doorvoer en latentie. Ook kunt u de broncode Hallo bekijken en vergelijkbare configuraties tooyour eigen testsuites of productietoepassingen implementeren.

## <a name="next-steps"></a>Volgende stappen
In dit artikel, die we kijken hoe u de prestaties en schaal testen met Cosmos-database met een .NET-console-app kunt uitvoeren. Raadpleeg toohello onderstaande koppelingen voor meer informatie over het werken met Azure Cosmos DB.

* [Azure DB Cosmos-prestaties testen voorbeeld](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Client configuration opties tooimprove Azure DB die Cosmos-prestaties](performance-tips.md)
* [Serverzijde partitioneren in Azure Cosmos-DB](partition-data.md)


