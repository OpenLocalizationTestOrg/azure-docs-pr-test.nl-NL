---
title: aaaWorking met Hallo wijziging feed ondersteuning in Azure Cosmos DB | Microsoft Docs
description: Gebruik Azure Cosmos DB feed ondersteuning tootrack wijzigingen in documenten wijzigen en uitvoeren op basis van gebeurtenissen verwerken zoals triggers en caches en analyses systemen up-to-date te houden.
keywords: Feed wijzigen
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="65054-104">Werken met Hallo wijziging feed ondersteuning in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="65054-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="65054-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is een snelle en flexibele globaal gerepliceerd database-service die wordt gebruikt voor het opslaan van grote hoeveelheden transactionele en operationele gegevens met voorspelbare één cijfer milliseconde latentie voor leesbewerkingen en schrijft.</span><span class="sxs-lookup"><span data-stu-id="65054-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="65054-106">Hierdoor is het geschikt voor IoT, games, retail, en operationele logboekregistratie toepassingen.</span><span class="sxs-lookup"><span data-stu-id="65054-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="65054-107">Een algemene ontwerppatroon in deze toepassingen is tootrack wijzigingen aangebracht tooAzure Cosmos DB gegevens, en gerealiseerde weergaven bijwerken, voert u realtime-analyses, archiveren toocold gegevensopslag en trigger-meldingen op bepaalde gebeurtenissen op basis van deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="65054-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="65054-108">Hallo **wijziging feed ondersteuning** in Azure Cosmos DB kunt u toobuild efficiënte en schaalbare oplossingen voor elk van deze patronen.</span><span class="sxs-lookup"><span data-stu-id="65054-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="65054-109">Wijziging van de feed ondersteuning biedt Azure Cosmos DB een gesorteerde lijst van documenten binnen een verzameling Azure Cosmos DB in Hallo volgorde waarin ze zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="65054-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="65054-110">Dit kanaal kan worden gebruikt toolisten voor wijzigingen toodata binnen Hallo verzameling en uitvoeren van acties zoals:</span><span class="sxs-lookup"><span data-stu-id="65054-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="65054-111">Een aanroep tooan API geactiveerd wanneer een document wordt ingevoegd of gewijzigd</span><span class="sxs-lookup"><span data-stu-id="65054-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="65054-112">Verwerking van realtime (stream) uitvoeren op updates</span><span class="sxs-lookup"><span data-stu-id="65054-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="65054-113">Synchroniseer gegevens met een cache, de zoekmachine of het datawarehouse</span><span class="sxs-lookup"><span data-stu-id="65054-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="65054-114">Wijzigingen in Azure Cosmos DB kunnen worden doorgevoerd en worden asynchroon verwerkt en verdeeld over een of meer consumenten voor parallelle verwerking.</span><span class="sxs-lookup"><span data-stu-id="65054-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="65054-115">Bekijk Hallo API's voor de feed wijzigen en hoe u ze kunt gebruiken toobuild schaalbare realtime-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="65054-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="65054-116">Dit artikel laat zien hoe toowork met Azure Cosmos DB feed en Hallo DocumentDB API wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65054-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Met behulp van Azure DB die Cosmos wijziging feed toopower realtime analyses en gebeurtenisafhankelijke scenario's met computers](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="65054-118">Wijziging feed ondersteuning is alleen beschikbaar voor Hallo DocumentDB API op dit moment; Hallo Graph API en de tabel-API worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="65054-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="65054-119">Gebruiksvoorbeelden en scenario 's</span><span class="sxs-lookup"><span data-stu-id="65054-119">Use cases and scenarios</span></span>
<span data-ttu-id="65054-120">Feed wijzigen kunt u efficiënte verwerking van grote gegevenssets met een groot aantal schrijfbewerkingen en biedt een alternatieve tooquerying gehele gegevenssets tooidentify wat is er gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="65054-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="65054-121">U kunt bijvoorbeeld Hallo taken efficiënt volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="65054-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="65054-122">Een cache, search-index of een datawarehouse bijwerken met gegevens die zijn opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="65054-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="65054-123">Implementeren op toepassingsniveau gegevens lagen en archivering, dat wil zeggen, gegevensopslag ' hot ' in Azure Cosmos DB en leeftijd te 'koude gegevens'[Azure Blob Storage](../storage/common/storage-introduction.md) of [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65054-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="65054-124">Batch analytics implementeren op de gegevens met [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="65054-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="65054-125">Implementeer [lambda pijplijnen op Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="65054-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="65054-126">Azure Cosmos DB biedt een schaalbare database-oplossing die kan opname en query verwerken en implementeren van lambda-architecturen met lage totale Eigendomskosten.</span><span class="sxs-lookup"><span data-stu-id="65054-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="65054-127">Nul uitvaltijd migraties tooanother Azure DB die Cosmos-account met een andere partitieschema niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="65054-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="65054-128">**Lambda pijplijnen met Azure Cosmos DB voor opname en -query:**</span><span class="sxs-lookup"><span data-stu-id="65054-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Lambda-pijplijn voor opname en query op basis van Azure Cosmos-DB](./media/change-feed/lambda.png)

<span data-ttu-id="65054-130">Gebruik Azure Cosmos DB tooreceive en gebeurtenisgegevens van apparaten, sensoren, infrastructuur en toepassingen opslaan en verwerken van deze gebeurtenissen in realtime met [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), of [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65054-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="65054-131">Binnen uw [zonder server](http://azure.com/serverless) web- en mobiele apps, u kunt de gebeurtenissen bijhouden zoals wijzigingen tooyour klant profiel, voorkeuren of locatie tootrigger bepaalde acties zoals het verzenden van pushmeldingen meldingen tootheir apparaten met behulp van [Azure Functions](../azure-functions/functions-bindings-documentdb.md) of [App Services](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="65054-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="65054-132">Als u Azure Cosmos DB toobuild een spel, kunt u bijvoorbeeld wijziging feed tooimplement realtime scoreborden op basis van scores van voltooide games gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65054-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="65054-133">De werking van de feed wijzigen in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="65054-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="65054-134">Azure Cosmos DB biedt Hallo mogelijkheid tooincrementally lezen wijzigingen tooan Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="65054-135">Deze wijziging feed heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="65054-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="65054-136">Wijzigingen zijn in Azure Cosmos DB permanent en asynchroon kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="65054-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="65054-137">Toodocuments binnen een verzameling wijzigingen zijn onmiddellijk in Hallo wijziging feed beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="65054-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="65054-138">Elke wijziging tooa document wordt slechts één keer weergegeven in Hallo wijziging feed en clients beheren hun logica plaatsen van controlepunten.</span><span class="sxs-lookup"><span data-stu-id="65054-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="65054-139">Hallo wijziging feed processor-bibliotheek biedt plaatsen van controlepunten en 'ten minste eenmaal' semantiek.</span><span class="sxs-lookup"><span data-stu-id="65054-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="65054-140">Alleen Hallo recentste wijziging voor een bepaald document is opgenomen in het wijzigingenlogboek Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="65054-141">Tussentijdse wijzigingen zijn mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="65054-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="65054-142">Hallo wijziging feed is door wijzigingen in elke waarde voor de partitiesleutel gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="65054-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="65054-143">Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="65054-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="65054-144">Wijzigingen kunnen worden gesynchroniseerd vanuit elk punt in tijd, er is geen vaste Gegevensretentieperiode waarvoor wijzigingen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="65054-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="65054-145">Wijzigingen zijn beschikbaar in segmenten van de partitie sleutelbereiken.</span><span class="sxs-lookup"><span data-stu-id="65054-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="65054-146">Op deze manier kunt wijzigingen in grote verzamelingen toobe parallel worden verwerkt door meerdere gebruikers /-servers.</span><span class="sxs-lookup"><span data-stu-id="65054-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="65054-147">Toepassingen kunnen aanvragen voor meerdere wijziging-feeds gelijktijdig op Hallo dezelfde verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="65054-148">Azure Cosmos-DB wijzigen feed is standaard ingeschakeld voor alle accounts.</span><span class="sxs-lookup"><span data-stu-id="65054-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="65054-149">Kunt u uw [ingerichte doorvoer](request-units.md) in uw regio schrijven of een willekeurige [lezen regio](distribute-data-globally.md) tooread van Hallo feed, net als elke andere bewerking vanuit Azure Cosmos DB wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65054-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="65054-150">Hallo wijziging feed bevat INSERT en updatebewerkingen toodocuments binnen Hallo verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65054-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="65054-151">U kunt vastleggen verwijderingen door een 'soft-delete' vlag binnen uw documenten in plaats van verwijderingen.</span><span class="sxs-lookup"><span data-stu-id="65054-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="65054-152">U kunt ook een eindige vervalperiode voor uw documenten via Hallo instellen [TTL mogelijkheid](time-to-live.md)voor bijvoorbeeld 24 uur en gebruik Hallo waarde van die eigenschap toocapture worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="65054-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="65054-153">Met deze oplossing hebt u tooprocess wijzigingen binnen een kortere periode dan Hallo TTL verloopperiode.</span><span class="sxs-lookup"><span data-stu-id="65054-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="65054-154">Hallo wijziging feed is beschikbaar voor elke partitiesleutelbereik binnen Hallo documentverzameling en dus kan worden verdeeld over een of meer consumenten voor parallelle verwerking.</span><span class="sxs-lookup"><span data-stu-id="65054-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Feed voor gedistribueerde verwerking van Azure Cosmos DB wijzigen](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="65054-156">U hebt een aantal opties in de manier waarop u een wijziging in de feed in uw clientcode implementeert.</span><span class="sxs-lookup"><span data-stu-id="65054-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="65054-157">Hallo secties die onmiddellijk volgen beschrijven hoe tooimplement Hallo wijziging feed met hello Azure Cosmos DB REST-API en Hallo DocumentDB SDK's.</span><span class="sxs-lookup"><span data-stu-id="65054-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="65054-158">Echter, voor .NET-toepassingen, wordt u aangeraden Hallo nieuwe [wijziging feed processor bibliotheek](#change-feed-processor) voor verwerking van gebeurtenissen van Hallo wijzigen van de feed lezen wijzigingen vereenvoudigt meerdere partities en kunt meerdere threads in werkt Parallel.</span><span class="sxs-lookup"><span data-stu-id="65054-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="65054-159"><a id="rest-apis"></a>Werken met Hallo REST-API en DocumentDB SDK 's</span><span class="sxs-lookup"><span data-stu-id="65054-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="65054-160">Azure Cosmos DB biedt elastische containers voor opslag en doorvoer aangeroepen **verzamelingen**.</span><span class="sxs-lookup"><span data-stu-id="65054-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="65054-161">Gegevens in verzamelingen is logisch zijn gegroepeerd met [partitie sleutels](partition-data.md) voor schaalbaarheid en prestaties.</span><span class="sxs-lookup"><span data-stu-id="65054-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="65054-162">Azure Cosmos DB biedt verschillende API's voor toegang tot deze gegevens, met inbegrip van lookup-ID (lezen/Get), query en lees-feeds (scans).</span><span class="sxs-lookup"><span data-stu-id="65054-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="65054-163">Hallo wijziging feed kan worden verkregen met twee nieuwe aanvraag-headers toohello DocumentDB in te vullen `ReadDocumentFeed` API, en over het bereiken van partitiesleutels parallel kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="65054-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="65054-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="65054-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="65054-165">U gaat nu een korte kijken hoe ReadDocumentFeed werkt.</span><span class="sxs-lookup"><span data-stu-id="65054-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="65054-166">Azure Cosmos DB ondersteunt het lezen van een feed van documenten binnen een verzameling via Hallo `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="65054-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="65054-167">Hallo volgende aanvraag resulteert bijvoorbeeld een pagina van de documenten binnen Hallo `serverlogs` verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="65054-168">Resultaten kunnen worden beperkt met behulp van Hallo `x-ms-max-item-count` header en gelezen kunnen worden hervat door opnieuw indienen Hallo-aanvraag met een `x-ms-continuation` header in Hallo vorige antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="65054-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="65054-169">Wanneer dit wordt uitgevoerd op één enkele client `ReadDocumentFeed` doorlopen resultaten meerdere partities opeenvolgend.</span><span class="sxs-lookup"><span data-stu-id="65054-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="65054-170">**Seriële lezen feed document**</span><span class="sxs-lookup"><span data-stu-id="65054-170">**Serial read document feed**</span></span>

<span data-ttu-id="65054-171">U kunt ook ophalen Hallo-feed van documenten met behulp van een ondersteund Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="65054-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="65054-172">Bijvoorbeeld, Hallo volgende codefragment bevat hoe toouse hello [ReadDocumentFeedAsync methode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span><span class="sxs-lookup"><span data-stu-id="65054-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="65054-173">Gedistribueerde uitvoering van ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="65054-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="65054-174">Voor verzamelingen die een groot aantal updates opnemen of terabytes aan gegevens of meer bevatten, seriële uitvoering van lees-feed van een enkelvoudige clientcomputer mogelijk geen praktische.</span><span class="sxs-lookup"><span data-stu-id="65054-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="65054-175">In de volgorde toosupport biedt deze big data-scenario's, Azure Cosmos DB API's toodistribute `ReadDocumentFeed` aanroepen transparant tussen meerdere client lezers/gebruikers.</span><span class="sxs-lookup"><span data-stu-id="65054-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="65054-176">**Gedistribueerde lezen Document Feed**</span><span class="sxs-lookup"><span data-stu-id="65054-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="65054-177">tooprovide schaalbare verwerking van incrementele wijzigingen, Azure Cosmos DB ondersteunt een scale-out-model voor Hallo wijzigen op basis van de bereiken van partitiesleutels API feed.</span><span class="sxs-lookup"><span data-stu-id="65054-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="65054-178">U kunt een lijst van de partitie ophalen sleutelbereiken voor het uitvoeren van een verzameling een `ReadPartitionKeyRanges` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="65054-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="65054-179">U kunt uitvoeren voor elke partitiesleutelbereik een `ReadDocumentFeed` tooread documenten met partitiesleutels binnen dat bereik valt.</span><span class="sxs-lookup"><span data-stu-id="65054-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="65054-180">Bij het ophalen van partitie sleutelbereiken voor een verzameling</span><span class="sxs-lookup"><span data-stu-id="65054-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="65054-181">U kunt aanvragende Hallo Hallo partitie sleutelbereiken ophalen `pkranges` bron binnen een verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="65054-182">Bijvoorbeeld hello volgende aanvraag opgehaald Hallo lijst met partitie-sleutelbereiken voor Hallo `serverlogs` verzameling:</span><span class="sxs-lookup"><span data-stu-id="65054-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="65054-183">Deze aanvraag retourneert Hallo antwoord met metagegevens over Hallo partitie sleutelbereiken te volgen:</span><span class="sxs-lookup"><span data-stu-id="65054-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="65054-184">**Partitie-eigenschappen van de belangrijkste bereik**: elke partitiesleutelbereik Hallo metagegevenseigenschappen in de volgende tabel Hallo omvat:</span><span class="sxs-lookup"><span data-stu-id="65054-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="65054-185">Header-naam</span><span class="sxs-lookup"><span data-stu-id="65054-185">Header name</span></span></th>
        <th><span data-ttu-id="65054-186">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65054-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-187">id</span><span class="sxs-lookup"><span data-stu-id="65054-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="65054-188">Hallo-ID voor Hallo partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="65054-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="65054-189">Dit is een stabiele en de unieke ID binnen elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="65054-190">Moet worden gebruikt in de volgende aanroep tooread wijzigingen Hallo door partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="65054-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="65054-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="65054-192">Hallo maximale partitie sleutel hash-waarde voor Hallo partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="65054-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="65054-193">Voor intern gebruik.</span><span class="sxs-lookup"><span data-stu-id="65054-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="65054-194">minInclusive</span></span></td>
        <td><span data-ttu-id="65054-195">Hallo partitie moet minimaal de waarde van het sleutelhash voor Hallo partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="65054-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="65054-196">Voor intern gebruik.</span><span class="sxs-lookup"><span data-stu-id="65054-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="65054-197">U kunt dit doen met behulp van een ondersteund Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="65054-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="65054-198">Bijvoorbeeld: hello volgende fragment toont hoe de partitiesleutel tooretrieve bereiken in .NET Hallo met [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) methode.</span><span class="sxs-lookup"><span data-stu-id="65054-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="65054-199">Azure Cosmos DB ondersteunt voor het ophalen van documenten per partitiesleutelbereik door Hallo instelling optioneel `x-ms-documentdb-partitionkeyrangeid` header.</span><span class="sxs-lookup"><span data-stu-id="65054-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="65054-200">Uitvoeren van een incrementele ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="65054-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="65054-201">ReadDocumentFeed ondersteunt Hallo volgen scenario's / taken voor incrementele verwerking van wijzigingen in Azure Cosmos DB verzamelingen:</span><span class="sxs-lookup"><span data-stu-id="65054-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="65054-202">Lees alle wijzigingen toodocuments vanaf het begin van de hello, dat wil zeggen, van een verzameling maken.</span><span class="sxs-lookup"><span data-stu-id="65054-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="65054-203">Lees alle verandert toofuture updates toodocuments van huidige tijd en eventuele wijzigingen sinds een opgegeven gebruiker.</span><span class="sxs-lookup"><span data-stu-id="65054-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="65054-204">Alle wijzigingen toodocuments lezen van een logische versie van het Hallo-verzameling (ETag).</span><span class="sxs-lookup"><span data-stu-id="65054-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="65054-205">U kunt uw consumenten op basis van Hallo ETag geretourneerd van incrementele lezen-feed aanvragen controlepunt.</span><span class="sxs-lookup"><span data-stu-id="65054-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="65054-206">Hallo wijzigingen omvatten toodocuments inserts en updates.</span><span class="sxs-lookup"><span data-stu-id="65054-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="65054-207">toocapture worden verwijderd, u moet een eigenschap 'soft delete' gebruiken in uw documenten of Hallo [ingebouwde TTL eigenschap](time-to-live.md) toosignal een in behandeling zijnde verwijdering in Hallo feed wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65054-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="65054-208">na de tabel lijsten Hallo Hallo [aanvraag](/rest/api/documentdb/common-documentdb-rest-request-headers.md) en [antwoordheaders](/rest/api/documentdb/common-documentdb-rest-response-headers.md) voor ReadDocumentFeed bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="65054-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="65054-209">**Aanvraagheaders voor incrementele ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="65054-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="65054-210">Header-naam</span><span class="sxs-lookup"><span data-stu-id="65054-210">Header name</span></span></th>
        <th><span data-ttu-id="65054-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65054-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-212">EEN IM</span><span class="sxs-lookup"><span data-stu-id="65054-212">A-IM</span></span></td>
        <td><span data-ttu-id="65054-213">Moet worden ingesteld te 'Incrementele feed', of anders weggelaten</span><span class="sxs-lookup"><span data-stu-id="65054-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="65054-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="65054-215">Er is geen header: retourneert alle wijzigingen van Hallo vanaf (verzameling maken)</span><span class="sxs-lookup"><span data-stu-id="65054-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="65054-216">' * ': alle nieuwe wijzigingen toodata binnen Hallo verzameling geretourneerd</span><span class="sxs-lookup"><span data-stu-id="65054-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="65054-217">&lt;ETag&gt;: als tooa verzameling ETag instellen, retourneert alle wijzigingen die sinds logische tijdstempel</span><span class="sxs-lookup"><span data-stu-id="65054-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="65054-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="65054-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="65054-219">RFC 1123 tijdnotatie; genegeerd als If-None-Match is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="65054-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="65054-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="65054-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="65054-221">Hallo partitie sleutel bereik-ID voor het lezen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="65054-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="65054-222">**Antwoordheaders voor incrementele ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="65054-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="65054-223">Header-naam</span><span class="sxs-lookup"><span data-stu-id="65054-223">Header name</span></span></th>
        <th><span data-ttu-id="65054-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65054-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-225">ETag</span><span class="sxs-lookup"><span data-stu-id="65054-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="65054-226">Hallo logische LSN (sequence number) van de laatste document geretourneerd als antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="65054-227">Incrementele ReadDocumentFeed kan worden hervat door deze waarde in de If-None-Match opnieuw.</span><span class="sxs-lookup"><span data-stu-id="65054-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="65054-228">Hier volgt een voorbeeld aanvraag tooreturn alle incrementele wijzigingen in de verzameling van Hallo logische versie/ETag `28535` en partitioneren van de belangrijkste bereik = `16`:</span><span class="sxs-lookup"><span data-stu-id="65054-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="65054-229">Wijzigingen zijn geordend op tijd binnen elke waarde voor de partitiesleutel binnen Hallo partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="65054-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="65054-230">Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="65054-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="65054-231">Als er meer resultaten dan in één pagina passen, u de volgende pagina Hallo van resultaten kunt lezen door Hallo aanvraag Hello wordt opnieuw `If-None-Match` header met waarde gelijk toohello `etag` uit het vorige antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="65054-232">Als meerdere documenten zijn ingevoegd of Transactioneel binnen een opgeslagen procedure of trigger bijgewerkt, ze alle geretourneerd binnen Hallo dezelfde antwoordpagina.</span><span class="sxs-lookup"><span data-stu-id="65054-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="65054-233">Met de feed wijziging, krijgt u mogelijk meer items geretourneerd in een pagina, dan is opgegeven in `x-ms-max-item-count` in geval van meerdere documenten ingevoegd of geüpdatet binnen een opgeslagen procedures Hallo of triggers.</span><span class="sxs-lookup"><span data-stu-id="65054-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="65054-234">Wanneer u Hallo .NET SDK (1.17.0), stelt u Hallo veld `StartTime` in `ChangeFeedOptions` documenten toodirectly return gewijzigd sinds `StartTime` bij het aanroepen van `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="65054-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="65054-235">Door op te geven `If-Modified-Since` Hallo REST-API gebruikt, uw aanvraag wordt geretourneerd niet Hallo documenten zelf, maar in plaats daarvan Hallo vervolgtoken of `etag` in Hallo-antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="65054-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="65054-236">tooreturn hello documenten gewijzigde Hallo tijd, Hallo vervolgtoken opgegeven `etag` moet vervolgens worden gebruikt in de volgende aanvraag Hallo met `If-None-Match` tooreturn Hallo werkelijke documenten.</span><span class="sxs-lookup"><span data-stu-id="65054-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="65054-237">Hallo .NET SDK biedt Hallo [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) en [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper tooaccess wijzigingen in de verzameling tooa klassen.</span><span class="sxs-lookup"><span data-stu-id="65054-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="65054-238">Hallo volgende fragment toont hoe alle tooretrieve verandert vanaf Hallo met .NET SDK Hallo van één client.</span><span class="sxs-lookup"><span data-stu-id="65054-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="65054-239">En hello volgende fragment toont hoe tooprocess verandert in realtime met Azure Cosmos DB met behulp van Hallo wijziging feed ondersteuning en Hallo voorafgaand aan de functie.</span><span class="sxs-lookup"><span data-stu-id="65054-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="65054-240">de eerste aanroep Hallo retourneert alle Hallo documenten in Hallo verzameling en Hallo tweede alleen retourneert Hallo twee documenten die zijn gemaakt en die zijn gemaakt sinds het laatste controlepunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="65054-241">U kunt ook Hallo wijziging feed met behulp van de client side logica tooselectively procesgebeurtenissen filteren.</span><span class="sxs-lookup"><span data-stu-id="65054-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="65054-242">Dit is bijvoorbeeld een codefragment die gebruikmaakt van de client side LINQ tooprocess alleen temperatuur gebeurtenissen van apparaat sensoren wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65054-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="65054-243"><a id="change-feed-processor"></a>Bibliotheek van de Feed Processor wijzigingsbeheer</span><span class="sxs-lookup"><span data-stu-id="65054-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="65054-244">Een andere optie is toouse hello [Azure Cosmos DB wijzigen Feed Processor bibliotheek](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), kunt u eenvoudig distribueren voor gebeurtenisverwerking van een wijziging in de feed in meerdere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="65054-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="65054-245">Hallo-bibliotheek is ideaal voor het bouwen van wijziging lezers feed op Hallo .NET-platform.</span><span class="sxs-lookup"><span data-stu-id="65054-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="65054-246">Sommige werkstromen die zouden worden vereenvoudigd door middel van Hallo wijziging Feed Processor bibliotheek via Hallo-methoden die zijn opgenomen in Hallo andere Cosmos DB SDK's zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="65054-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="65054-247">Opvragen van de updates van wijziging feed wanneer gegevens worden opgeslagen op verschillende partities</span><span class="sxs-lookup"><span data-stu-id="65054-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="65054-248">Verplaatsen of gegevens van één verzameling tooanother repliceren</span><span class="sxs-lookup"><span data-stu-id="65054-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="65054-249">Parallelle uitvoering van de acties die worden geactiveerd door updates toodata en wijzig feed</span><span class="sxs-lookup"><span data-stu-id="65054-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="65054-250">Terwijl met behulp van Hallo API's in Hallo Cosmos-SDK's nauwkeurige toegang toochange kanaal updates in elke partitie bevat, vereenvoudigt met behulp van Hallo wijziging Feed Processor bibliotheek lezen wijzigingen in partities en meerdere threads die parallel werken.</span><span class="sxs-lookup"><span data-stu-id="65054-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="65054-251">In plaats van handmatig lezen wijzigingen van elke container en een vervolgtoken voor elke partitie opslaan, beheert Hallo wijziging Feed Processor lezen wijzigingen automatisch meerdere partities met een lease-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="65054-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="65054-252">Hallo-bibliotheek is beschikbaar als een NuGet-pakket: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) en van broncode als een Github [voorbeeld](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="65054-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="65054-253">Understanding wijziging Feed Processor-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="65054-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="65054-254">Er zijn vier onderdelen van de implementatie van Hallo wijziging Feed Processor: Hallo bewaakt verzameling, Hallo lease verzameling Hallo processor host en Hallo consumenten.</span><span class="sxs-lookup"><span data-stu-id="65054-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="65054-255">**Bewaakte verzameling:** Hallo bewaakt verzameling is Hallo gegevens op basis van welke Hallo wijziging feed wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="65054-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="65054-256">Een verzameling van de toohello bewaakt toevoegingen en wijzigingen worden doorgevoerd in Hallo wijziging feed van Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="65054-257">**Verzameling van de lease:** Hallo lease verzameling coördinaten Hallo wijziging feed over meerdere werknemers verwerken.</span><span class="sxs-lookup"><span data-stu-id="65054-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="65054-258">Een afzonderlijke verzameling is gebruikte toostore Hallo leases met een lease per partitie.</span><span class="sxs-lookup"><span data-stu-id="65054-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="65054-259">Het is nuttig toostore deze verzameling lease op een ander account Hello schrijven regio dichter toowhere Hallo wijziging Feed Processor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65054-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="65054-260">Een lease-object bevat Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="65054-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="65054-261">Eigenaar: Hiermee geeft u het Hallo-host die eigenaar is van de lease Hallo</span><span class="sxs-lookup"><span data-stu-id="65054-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="65054-262">Voortzetting: Hiermee geeft u Hallo positie (vervolgtoken) in Hallo wijziging feed voor een bepaalde partitie</span><span class="sxs-lookup"><span data-stu-id="65054-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="65054-263">Tijdstempel: Tijd van laatste lease is bijgewerkt. Hallo tijdstempel gebruikte toocheck kan zijn of Hallo lease is verlopen</span><span class="sxs-lookup"><span data-stu-id="65054-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="65054-264">**Processor Host:** elke host bepaalt hoeveel partities tooprocess op basis van hoeveel andere exemplaren van hosts actieve leases hebben.</span><span class="sxs-lookup"><span data-stu-id="65054-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="65054-265">Wanneer u een host start, verkrijgt deze leases toobalance Hallo werkbelasting op alle hosts.</span><span class="sxs-lookup"><span data-stu-id="65054-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="65054-266">Een host vernieuwt periodiek leases, dus leases actief blijven.</span><span class="sxs-lookup"><span data-stu-id="65054-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="65054-267">Een host controlepunten Hallo laatste voortzetting token tooits lease voor elk lezen.</span><span class="sxs-lookup"><span data-stu-id="65054-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="65054-268">tooensure gelijktijdigheid veiligheid, een host controleert Hallo ETag voor elke update lease.</span><span class="sxs-lookup"><span data-stu-id="65054-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="65054-269">Andere strategieën controlepunt worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="65054-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="65054-270">Bij het afsluiten, een host releases alle leases maar houdt Hallo voortzetting informatie, zodat het lezen van de opgeslagen controlepunt hello later kan worden hervat.</span><span class="sxs-lookup"><span data-stu-id="65054-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="65054-271">Het aantal hosts Hallo mag niet groter dan het aantal partities (leases) Hallo op dit moment.</span><span class="sxs-lookup"><span data-stu-id="65054-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="65054-272">**Consumenten:** consumenten of werknemers, threads die Hallo wijziging feed verwerking gestart door elke host uitvoeren zijn.</span><span class="sxs-lookup"><span data-stu-id="65054-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="65054-273">Elke host processor kan meerdere gebruikers hebben.</span><span class="sxs-lookup"><span data-stu-id="65054-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="65054-274">Elke consumer Hallo wijziging feed leest vanaf Hallo partitie wordt toegewezen tooand ontvangt een melding van de host van wijzigingen en verlopen van leases.</span><span class="sxs-lookup"><span data-stu-id="65054-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="65054-275">toofurther informatie over hoe deze vier elementen van wijziging Feed Processor samenwerken, bekijk een voorbeeld in het volgende diagram Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="65054-276">Hallo verzameling winkels documenten bewaakt en Hallo 'stad' gebruikt als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="65054-277">Zien we dat Hallo blauw partitie enzovoort documenten met het veld 'plaats' Hallo uit "A E" bevat.</span><span class="sxs-lookup"><span data-stu-id="65054-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="65054-278">Er zijn twee hosts, elk met twee consumenten lezen van Hallo vier partities parallel.</span><span class="sxs-lookup"><span data-stu-id="65054-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="65054-279">Hallo pijlen wijzen Hallo consumenten lezen van een specifieke positie in Hallo feed wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65054-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="65054-280">In de eerste partitie hello betekent Hallo donkere blauw ongelezen wijzigingen en lichte blauw Hallo Hallo al gelezen wijzigingen op Hallo wijziging feed.</span><span class="sxs-lookup"><span data-stu-id="65054-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="65054-281">Hallo hosts gebruiken Hallo lease verzameling toostore 'voortzetting' waarde tookeep bijgehouden Hallo huidige positie voor elke consumer lezen.</span><span class="sxs-lookup"><span data-stu-id="65054-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Met behulp van hello Azure Cosmos DB wijzigen feed processor host](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="65054-283">Met behulp van de wijziging Feed Processor-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="65054-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="65054-284">Hallo volgende sectie wordt uitgelegd hoe toouse wijziging Feed Processor-bibliotheek in de context voor het repliceren van wijzigingen uit een verzameling bron verzameling tooa bestemming Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="65054-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="65054-285">Hallo bronverzameling is hier Hallo bewaakt verzameling in de Feed wijziging-Processor.</span><span class="sxs-lookup"><span data-stu-id="65054-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="65054-286">**Installeren en omvatten Hallo wijziging Feed Processor NuGet-pakket**</span><span class="sxs-lookup"><span data-stu-id="65054-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="65054-287">Voordat u wijziging Feed Processor NuGet-pakket installeert, eerst installeren:</span><span class="sxs-lookup"><span data-stu-id="65054-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="65054-288">Microsoft.Azure.DocumentDB, versie 1.13.1 of hoger</span><span class="sxs-lookup"><span data-stu-id="65054-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="65054-289">Newtonsoft.Json, versie 9.0.1 of hoger installeren `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` en deze opnemen als een verwijzing.</span><span class="sxs-lookup"><span data-stu-id="65054-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="65054-290">**Een gecontroleerde, lease- en verzameling maken**</span><span class="sxs-lookup"><span data-stu-id="65054-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="65054-291">In de volgorde toouse Hallo wijziging Feed Processor bibliotheek moet Hallo lease verzameling toobe gemaakt voordat Hallo processor host (s) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65054-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="65054-292">Opnieuw, is het raadzaam een lease-verzameling opslaan op een ander account met een schrijven regio dichter toowhere Hallo dat wijziging Feed Processor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65054-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="65054-293">In dit voorbeeld verplaatsing van gegevens moet toocreate Hallo doelverzameling voordat Hallo wijziging Feed Processor host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65054-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="65054-294">In de voorbeeldcode Hallo noemen we een helper methode toocreate Hallo bewaakt, geleasete, en de bestemming verzamelingen als deze niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="65054-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="65054-295">Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor Hallo toepassing toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="65054-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="65054-296">Voor meer informatie gaat u naar Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="65054-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="65054-297">*Maken van een host processor*</span><span class="sxs-lookup"><span data-stu-id="65054-297">*Creating a processor host*</span></span>

<span data-ttu-id="65054-298">Hallo `ChangeFeedProcessorHost` klasse biedt een thread-veilige, met meerdere processen en veilige runtime-omgeving voor gebeurtenisprocessors die ook het plaatsen van controlepunten en partitie lease biedt.</span><span class="sxs-lookup"><span data-stu-id="65054-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="65054-299">Hallo toouse `ChangeFeedProcessorHost` klasse, die u kunt implementeren `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="65054-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="65054-300">Deze interface bevat drie methoden:</span><span class="sxs-lookup"><span data-stu-id="65054-300">This interface contains three methods:</span></span>

* <span data-ttu-id="65054-301">`OpenAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijzigen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="65054-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="65054-302">Gewijzigde tooperform een specifieke actie kan zijn wanneer consumenten/zien wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="65054-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="65054-303">`CloseAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijziging wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="65054-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="65054-304">Gewijzigde tooperform een specifieke actie kan zijn als consument/zien is gesloten.</span><span class="sxs-lookup"><span data-stu-id="65054-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="65054-305">`ProcessChangesAsync`: Deze functie wordt aangeroepen wanneer nieuwe wijzigingen in het document beschikbaar op de feed wijzigen zijn.</span><span class="sxs-lookup"><span data-stu-id="65054-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="65054-306">Het kan een specifieke actie na elke wijziging feed-update voor gewijzigde tooperform zijn.</span><span class="sxs-lookup"><span data-stu-id="65054-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="65054-307">In ons voorbeeld we Hallo-interface implementeren `IChangeFeedObserver` via Hallo `DocumentFeedObserver` klasse.</span><span class="sxs-lookup"><span data-stu-id="65054-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="65054-308">Hier Hallo `ProcessChangesAsync` upserts (updates) een document van de wijziging in de doelverzameling Hallo feed werken.</span><span class="sxs-lookup"><span data-stu-id="65054-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="65054-309">In dit voorbeeld is nuttig voor het verplaatsen van gegevens van één verzameling tooanother in volgorde toochange Hallo partitiesleutel van een gegevensset.</span><span class="sxs-lookup"><span data-stu-id="65054-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="65054-310">*Hallo Processor Host wordt uitgevoerd*</span><span class="sxs-lookup"><span data-stu-id="65054-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="65054-311">Beide opties voor feed wijzigen voordat u begint met de verwerking van gebeurtenissen, en opties van de feed host wijzigen kunnen worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="65054-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="65054-312">Hallo specifieke velden die kunnen worden aangepast worden samengevat in Hallo tabellen te volgen.</span><span class="sxs-lookup"><span data-stu-id="65054-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="65054-313">**Opties voor Feed wijzigen**:</span><span class="sxs-lookup"><span data-stu-id="65054-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="65054-314">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="65054-314">Property Name</span></span></th>
        <th><span data-ttu-id="65054-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65054-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="65054-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="65054-317">Opgehaald of ingesteld Hallo kunt u het maximum aantal items toobe geretourneerd in de inventarisatiebewerking Hallo in hello Azure Cosmos DB database-service.</span><span class="sxs-lookup"><span data-stu-id="65054-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="65054-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="65054-319">Opgehaald of ingesteld van Hallo partitie sleutel bereik-id voor de huidige aanvraag Hallo in hello Azure Cosmos DB database-service.</span><span class="sxs-lookup"><span data-stu-id="65054-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="65054-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="65054-321">Opgehaald of ingesteld van Hallo aanvraag vervolgtoken in hello Azure Cosmos DB database-service.</span><span class="sxs-lookup"><span data-stu-id="65054-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="65054-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="65054-322">SessionToken</span></span></td>
        <td><span data-ttu-id="65054-323">Opgehaald of ingesteld van sessietoken Hallo voor gebruik met de sessieconsistentie in hello Azure Cosmos DB database-service.</span><span class="sxs-lookup"><span data-stu-id="65054-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="65054-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="65054-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="65054-325">Opgehaald of ingesteld of wijziging feeds in hello Azure Cosmos DB database-service moet worden gestart van Hallo vanaf (true) of van de huidige (false).</span><span class="sxs-lookup"><span data-stu-id="65054-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="65054-326">Standaard wordt gestart vanuit de huidige (false).</span><span class="sxs-lookup"><span data-stu-id="65054-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="65054-327">**Opties voor de Feed Host wijzigen**:</span><span class="sxs-lookup"><span data-stu-id="65054-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="65054-328">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="65054-328">Property Name</span></span></th>
        <th><span data-ttu-id="65054-329">Type</span><span class="sxs-lookup"><span data-stu-id="65054-329">Type</span></span></th>
        <th><span data-ttu-id="65054-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65054-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="65054-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="65054-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="65054-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="65054-333">Hello-interval voor alle leases voor partities die momenteel worden vastgehouden door Hallo ChangeFeedEventHost exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65054-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="65054-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="65054-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="65054-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="65054-336">Hallo interval tookick uit een taak toocompute of partities gelijkmatig zijn verdeeld over bekende host exemplaren.</span><span class="sxs-lookup"><span data-stu-id="65054-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="65054-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="65054-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="65054-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="65054-339">Hallo-interval voor welke Hallo lease wordt uitgevoerd op een lease voor een partitie.</span><span class="sxs-lookup"><span data-stu-id="65054-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="65054-340">Als de lease Hallo niet wordt verlengd binnen dit interval, het is verlopen en eigendom van Hallo partitie verplaatst tooanother ChangeFeedEventHost exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65054-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="65054-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="65054-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="65054-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="65054-343">Hallo vertraging tussen een partitie voor de nieuwe wijzigingen op Hallo polling feed nadat alle huidige wijzigingen zijn geleegd.</span><span class="sxs-lookup"><span data-stu-id="65054-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="65054-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="65054-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="65054-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="65054-346">Hallo frequentie toocheckpoint leases.</span><span class="sxs-lookup"><span data-stu-id="65054-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="65054-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="65054-348">int</span><span class="sxs-lookup"><span data-stu-id="65054-348">Int</span></span></td>
        <td><span data-ttu-id="65054-349">Hallo partitie moet minimaal aantal voor Hallo host.</span><span class="sxs-lookup"><span data-stu-id="65054-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="65054-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="65054-351">int</span><span class="sxs-lookup"><span data-stu-id="65054-351">Int</span></span></td>
        <td><span data-ttu-id="65054-352">Hallo kunt u het maximum aantal partities Hallo host kan fungeren.</span><span class="sxs-lookup"><span data-stu-id="65054-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="65054-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="65054-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="65054-354">BOOL</span><span class="sxs-lookup"><span data-stu-id="65054-354">Bool</span></span></td>
        <td><span data-ttu-id="65054-355">Of op Hallo van de host Hallo alle bestaande leases starten moeten worden verwijderd en Hallo host moet worden gestart vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="65054-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="65054-356">het instantiëren van toostart gebeurtenisverwerking, `ChangeFeedProcessorHost`, bieden de juiste parameters Hallo voor uw Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="65054-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="65054-357">Roep vervolgens `RegisterObserverAsync` tooregister uw `IChangeFeedObserver` (DocumentFeedObserver in dit voorbeeld)-implementatie met Hallo-runtime.</span><span class="sxs-lookup"><span data-stu-id="65054-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="65054-358">Op dit moment probeert Hallo host tooacquire een lease op elke partitiesleutelbereik in hello Azure Cosmos DB verzameling op basis van een greedy-algoritme.</span><span class="sxs-lookup"><span data-stu-id="65054-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="65054-359">Deze leases gedurende een bepaald tijdsbestek geldig en moeten daarna worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="65054-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="65054-360">Zodra nieuwe knooppunten worker-exemplaren in dit geval online komen, ze reserveringen voor leases en gedurende een bepaalde periode Hallo load verschuift tussen knooppunten elke host probeert tooacquire meer leases.</span><span class="sxs-lookup"><span data-stu-id="65054-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="65054-361">In voorbeeldcode hello, gebruiken we een klasse (DocumentFeedObserverFactory.cs) factory toocreate een zien en Hallo `RegistObserverFactoryAsync` tooregister Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="65054-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="65054-362">In de loop van de tijd komt er een evenwicht tot stand.</span><span class="sxs-lookup"><span data-stu-id="65054-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="65054-363">Deze dynamische mogelijkheid kan tooconsumers naar automatische schaling toobe toegepast voor schaal omhoog en omlaag schalen op basis van CPU.</span><span class="sxs-lookup"><span data-stu-id="65054-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="65054-364">Als er wijzigingen zijn beschikbaar in Azure Cosmos DB sneller dan consumers kunnen verwerken, kan Hallo CPU toename op consumenten gebruikte toocause een automatisch geschaald aantal werkrolexemplaren zijn.</span><span class="sxs-lookup"><span data-stu-id="65054-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65054-365">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65054-365">Next steps</span></span>
* <span data-ttu-id="65054-366">Probeer Hallo [Azure Cosmos DB Wijzig feed codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="65054-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="65054-367">Aan de slag met Hallo coderen [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="65054-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
