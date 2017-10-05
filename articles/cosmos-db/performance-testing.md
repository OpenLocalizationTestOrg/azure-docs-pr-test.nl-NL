---
title: Azure DB Cosmos schaal en prestaties testen | Microsoft Docs
description: Meer informatie over het uitvoeren van de schaal en prestaties testen met Azure Cosmos-DB
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="697d9-104">Prestaties en schaal testen met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="697d9-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="697d9-105">Prestaties en schaal testen is een belangrijke stap in de ontwikkeling van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="697d9-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="697d9-106">De databaselaag heeft een aanzienlijke invloed op de algehele prestaties en schaalbaarheid en kan daarom een essentieel onderdeel van de prestatietests voor veel toepassingen.</span><span class="sxs-lookup"><span data-stu-id="697d9-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="697d9-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is speciaal hiervoor gemaakte voor elastisch schalen en voorspelbare prestaties en daarom een geweldige geschikt voor toepassingen die een krachtige databaselaag moeten.</span><span class="sxs-lookup"><span data-stu-id="697d9-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="697d9-108">In dit artikel is een verwijzing voor ontwikkelaars Cosmos DB evalueren voor hoge prestaties toepassingsscenario's of prestaties testen van suites voor hun Cosmos-DB-werkbelastingen te implementeren.</span><span class="sxs-lookup"><span data-stu-id="697d9-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="697d9-109">Richt zich voornamelijk op de geïsoleerde prestaties testen van de database, maar bevat ook aanbevolen procedures voor productietoepassingen.</span><span class="sxs-lookup"><span data-stu-id="697d9-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="697d9-110">Na het lezen van dit artikel kunt u zich de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="697d9-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="697d9-111">Waar vind ik een voorbeeld .NET client-toepassing voor het testen van de prestaties van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="697d9-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="697d9-112">Hoe ik hoge doorvoersnelheid niveaus met Cosmos DB van mijn clienttoepassing bereikt?</span><span class="sxs-lookup"><span data-stu-id="697d9-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="697d9-113">Download het project uit om te beginnen met code [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="697d9-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="697d9-114">Het doel van deze toepassing is voor het demonstreren van aanbevolen procedures voor het uitpakken van betere prestaties buiten Cosmos DB met een beperkt aantal clientcomputers.</span><span class="sxs-lookup"><span data-stu-id="697d9-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="697d9-115">Dit is niet gemaakt voor het demonstreren van de piek-capaciteit van de service, die kan worden geschaald onbeperkt.</span><span class="sxs-lookup"><span data-stu-id="697d9-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="697d9-116">Als u op zoek bent voor clientzijde configuratieopties Cosmos DB prestaties te verbeteren, Zie [tips voor betere prestaties van Azure DB die Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="697d9-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="697d9-117">De toepassing testen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="697d9-117">Run the performance testing application</span></span>
<span data-ttu-id="697d9-118">De snelste manier om te beginnen is compileren en het .NET-voorbeeld hieronder, zoals beschreven in de onderstaande stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="697d9-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="697d9-119">U kunt ook de broncode controleren en gelijkaardige configuraties implementeren voor uw eigen clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="697d9-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="697d9-120">**Stap 1:** downloaden van het project uit [Azure Cosmos DB prestaties testen Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), of de GitHub-opslagplaats vertakken.</span><span class="sxs-lookup"><span data-stu-id="697d9-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="697d9-121">**Stap 2:** Wijzig de instellingen voor EndpointUrl, AuthorizationKey, CollectionThroughput en DocumentTemplate App.config (optioneel).</span><span class="sxs-lookup"><span data-stu-id="697d9-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="697d9-122">Voordat u verzamelingen met hoge doorvoer inricht, raadpleegt u de [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) als indicatie van de kosten per verzameling.</span><span class="sxs-lookup"><span data-stu-id="697d9-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="697d9-123">Azure DB Cosmos facturen opslag en doorvoer onafhankelijk op uurbasis, zodat u kunt u kosten besparen door te verwijderen of te verlagen van de doorvoer van uw Azure Cosmos DB verzamelingen nadat u hebt getest.</span><span class="sxs-lookup"><span data-stu-id="697d9-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="697d9-124">**Stap 3:** compileren en de console-app uitvoeren vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="697d9-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="697d9-125">Hier ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="697d9-125">You should see output like the following:</span></span>

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


<span data-ttu-id="697d9-126">**Stap 4 (indien nodig):** de doorvoer gerapporteerd (RU/s) uit het hulpprogramma moet gelijk zijn of hoger is dan de ingerichte doorvoer van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="697d9-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="697d9-127">Als dat niet het geval is, de DegreeOfParallelism in kleine stappen verhogen, kunt u de limiet is bereikt.</span><span class="sxs-lookup"><span data-stu-id="697d9-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="697d9-128">Als de doorvoer van uw clientapp plateaus, kunt meerdere exemplaren van de app op de dezelfde of andere machines starten u de ingerichte limiet bereikt over de verschillende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="697d9-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="697d9-129">Als u hulp nodig hebt bij deze stap, schrijft u een e-mail naar askcosmosdb@microsoft.com of het bestand een ondersteuningsticket vanuit de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="697d9-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="697d9-130">Zodra u de app actief hebt, kunt u proberen andere [beleid indexeren](indexing-policies.md) en [consistentieniveaus](consistency-levels.md) om te begrijpen van de impact op de doorvoer en latentie.</span><span class="sxs-lookup"><span data-stu-id="697d9-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="697d9-131">Ook kunt u de broncode controleren en soortgelijke configuraties voor uw eigen tests suites of productietoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="697d9-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="697d9-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="697d9-132">Next steps</span></span>
<span data-ttu-id="697d9-133">In dit artikel, die we kijken hoe u de prestaties en schaal testen met Cosmos-database met een .NET-console-app kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="697d9-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="697d9-134">Raadpleeg de onderstaande koppelingen voor meer informatie over het werken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="697d9-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="697d9-135">Azure DB Cosmos-prestaties testen voorbeeld</span><span class="sxs-lookup"><span data-stu-id="697d9-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="697d9-136">Client-configuratieopties voor het verbeteren van Azure DB die Cosmos-prestaties</span><span class="sxs-lookup"><span data-stu-id="697d9-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="697d9-137">Serverzijde partitioneren in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="697d9-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


