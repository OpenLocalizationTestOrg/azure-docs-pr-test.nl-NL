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
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="c64d4-104">Prestaties en schaal testen met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="c64d4-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="c64d4-105">Prestaties en schaal testen is een belangrijke stap in de ontwikkeling van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c64d4-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="c64d4-106">Voor veel toepassingen Hallo databaselaag heeft een aanzienlijke invloed op Hallo van de algehele prestaties en schaalbaarheid en is daarom een essentieel onderdeel van de prestaties van het testen.</span><span class="sxs-lookup"><span data-stu-id="c64d4-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="c64d4-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is speciaal hiervoor gemaakte voor elastisch schalen en voorspelbare prestaties en daarom een geweldige geschikt voor toepassingen die een krachtige databaselaag moeten.</span><span class="sxs-lookup"><span data-stu-id="c64d4-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="c64d4-108">In dit artikel is een verwijzing voor ontwikkelaars Cosmos DB evalueren voor hoge prestaties toepassingsscenario's of prestaties testen van suites voor hun Cosmos-DB-werkbelastingen te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c64d4-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="c64d4-109">Richt zich voornamelijk op de geïsoleerde prestatietests van Hallo-database, maar bevat ook aanbevolen procedures voor productietoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c64d4-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="c64d4-110">Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c64d4-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="c64d4-111">Waar vind ik een voorbeeld .NET client-toepassing voor het testen van de prestaties van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="c64d4-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="c64d4-112">Hoe ik hoge doorvoersnelheid niveaus met Cosmos DB van mijn clienttoepassing bereikt?</span><span class="sxs-lookup"><span data-stu-id="c64d4-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="c64d4-113">tooget gestart met code, download Hallo-project uit [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="c64d4-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="c64d4-114">Hallo-doel van deze toepassing is toodemonstrate aanbevolen procedures voor het uitpakken van betere prestaties buiten Cosmos DB met een beperkt aantal clientcomputers.</span><span class="sxs-lookup"><span data-stu-id="c64d4-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="c64d4-115">Dit is niet gemaakt toodemonstrate Hallo piek-capaciteit van Hallo-service, die kan worden geschaald onbeperkt.</span><span class="sxs-lookup"><span data-stu-id="c64d4-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="c64d4-116">Als u configuratie clientzijde opties tooimprove Cosmos DB prestaties zoekt, Zie [tips voor betere prestaties van Azure DB die Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="c64d4-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="c64d4-117">Hallo-prestaties testen van de toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c64d4-117">Run hello performance testing application</span></span>
<span data-ttu-id="c64d4-118">Hallo snelste manier tooget gestart is toocompile en Voer Hallo .NET voorbeeldcode hieronder, zoals beschreven in de onderstaande stappen voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="c64d4-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="c64d4-119">Ook kunt u de broncode Hallo bekijken en implementeren van vergelijkbare configuraties tooyour eigen clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c64d4-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="c64d4-120">**Stap 1:** Hallo-project downloaden uit [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), of fork Hallo GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c64d4-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="c64d4-121">**Stap 2:** Hallo instellingen wijzigen voor EndpointUrl, AuthorizationKey, CollectionThroughput en DocumentTemplate App.config (optioneel).</span><span class="sxs-lookup"><span data-stu-id="c64d4-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="c64d4-122">Raadpleeg voor het inrichten van verzamelingen met hoge doorvoer toohello [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate Hallo kosten per verzameling.</span><span class="sxs-lookup"><span data-stu-id="c64d4-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="c64d4-123">Azure DB Cosmos facturen opslag en doorvoer onafhankelijk op uurbasis, zodat u kunt u kosten besparen door te verwijderen of te verlagen Hallo doorvoer van uw Azure Cosmos DB verzamelingen nadat u hebt getest.</span><span class="sxs-lookup"><span data-stu-id="c64d4-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="c64d4-124">**Stap 3:** compileren en Hallo console-app uitvoeren vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="c64d4-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="c64d4-125">Hier ziet u uitvoer zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c64d4-125">You should see output like hello following:</span></span>

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


<span data-ttu-id="c64d4-126">**Stap 4 (indien nodig):** Hallo doorvoer gerapporteerd (RU/s) uit Hallo hulpprogramma moet Hallo dezelfde of hoger is dan Hallo ingerichte doorvoer van Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="c64d4-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="c64d4-127">Als dat niet het geval is, toenemende Hallo DegreeOfParallelism in kleine stappen helpen u mogelijk de Hallo limiet is bereikt.</span><span class="sxs-lookup"><span data-stu-id="c64d4-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="c64d4-128">Als Hallo doorvoer van uw clientapp plateaus, meerdere exemplaren van Hallo app starten op Hallo van dezelfde of verschillende computers vindt u een limiet is bereikt Hallo ingericht via Hallo verschillende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c64d4-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="c64d4-129">Als u hulp nodig hebt bij deze stap, schrijft u een e-mailbericht tooaskcosmosdb@microsoft.com of een ondersteuningsticket vanuit Hallo bestand [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c64d4-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c64d4-130">Zodra u Hallo-app die wordt uitgevoerd hebt, kunt u proberen andere [beleid indexeren](indexing-policies.md) en [consistentieniveaus](consistency-levels.md) toounderstand de impact op de doorvoer en latentie.</span><span class="sxs-lookup"><span data-stu-id="c64d4-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="c64d4-131">Ook kunt u de broncode Hallo bekijken en vergelijkbare configuraties tooyour eigen testsuites of productietoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="c64d4-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c64d4-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c64d4-132">Next steps</span></span>
<span data-ttu-id="c64d4-133">In dit artikel, die we kijken hoe u de prestaties en schaal testen met Cosmos-database met een .NET-console-app kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c64d4-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="c64d4-134">Raadpleeg toohello onderstaande koppelingen voor meer informatie over het werken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c64d4-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="c64d4-135">Azure DB Cosmos-prestaties testen voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c64d4-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="c64d4-136">Client configuration opties tooimprove Azure DB die Cosmos-prestaties</span><span class="sxs-lookup"><span data-stu-id="c64d4-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="c64d4-137">Serverzijde partitioneren in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="c64d4-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


