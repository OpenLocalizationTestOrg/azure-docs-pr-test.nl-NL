---
title: Werken met de wijziging feed ondersteuning in Azure Cosmos DB | Microsoft Docs
description: Azure Cosmos DB wijzigen feed ondersteuning gebruiken voor het bijhouden van wijzigingen in documenten en het uitvoeren van verwerking op basis van gebeurtenissen zoals triggers en caches en analyses systemen up-to-date te houden.
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
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="45787-104">Werken met de ondersteuning in Azure Cosmos DB feed wijziging</span><span class="sxs-lookup"><span data-stu-id="45787-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="45787-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is een snelle en flexibele globaal gerepliceerd database-service die wordt gebruikt voor het opslaan van grote hoeveelheden transactionele en operationele gegevens met voorspelbare één cijfer milliseconde latentie voor leesbewerkingen en schrijft.</span><span class="sxs-lookup"><span data-stu-id="45787-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="45787-106">Hierdoor is het geschikt voor IoT, games, retail, en operationele logboekregistratie toepassingen.</span><span class="sxs-lookup"><span data-stu-id="45787-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="45787-107">Een algemene ontwerppatroon in deze toepassingen is het bijhouden van wijzigingen aangebracht in Azure DB die Cosmos-gegevens en gerealiseerde weergaven bijwerken, realtime analyses uitvoeren, archiveren van gegevens naar koude opslag en trigger-meldingen op bepaalde gebeurtenissen op basis van deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="45787-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="45787-108">De **wijziging feed ondersteuning** in Azure Cosmos DB kunt u efficiënter en schaalbare oplossingen bouwen voor elk van deze patronen.</span><span class="sxs-lookup"><span data-stu-id="45787-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="45787-109">Wijziging van de feed ondersteuning biedt Azure Cosmos DB een gesorteerde lijst van documenten binnen een verzameling Azure Cosmos DB in de volgorde waarin ze zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="45787-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="45787-110">Deze feed kan worden gebruikt om te luisteren om de wijzigingen in gegevens binnen de verzameling en het uitvoeren van acties zoals:</span><span class="sxs-lookup"><span data-stu-id="45787-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="45787-111">Een aanroep van een API geactiveerd wanneer een document wordt ingevoegd of gewijzigd</span><span class="sxs-lookup"><span data-stu-id="45787-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="45787-112">Verwerking van realtime (stream) uitvoeren op updates</span><span class="sxs-lookup"><span data-stu-id="45787-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="45787-113">Synchroniseer gegevens met een cache, de zoekmachine of het datawarehouse</span><span class="sxs-lookup"><span data-stu-id="45787-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="45787-114">Wijzigingen in Azure Cosmos DB kunnen worden doorgevoerd en worden asynchroon verwerkt en verdeeld over een of meer consumenten voor parallelle verwerking.</span><span class="sxs-lookup"><span data-stu-id="45787-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="45787-115">Bekijk de API's voor de feed wijzigen en hoe u ze kunt gebruiken om schaalbare realtime toepassingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="45787-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="45787-116">Dit artikel laat zien hoe u werkt met Azure Cosmos DB wijzigen feed en de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="45787-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Power realtime analyses en gebeurtenisafhankelijke scenario's met computers met behulp van Azure DB die Cosmos wijziging feed](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="45787-118">Wijziging feed ondersteuning is alleen beschikbaar voor de DocumentDB-API op dit moment; de Graph API en de API van de tabel zijn momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="45787-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="45787-119">Gebruiksvoorbeelden en scenario 's</span><span class="sxs-lookup"><span data-stu-id="45787-119">Use cases and scenarios</span></span>
<span data-ttu-id="45787-120">Feed wijzigen kunt u efficiënte verwerking van grote gegevenssets met een groot aantal schrijfbewerkingen en biedt een alternatief voor het uitvoeren van query's gehele gegevenssets om te zien wat er is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="45787-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="45787-121">U kunt bijvoorbeeld de volgende taken efficiënt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="45787-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="45787-122">Een cache, search-index of een datawarehouse bijwerken met gegevens die zijn opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="45787-123">Implementeren op toepassingsniveau gegevens lagen en archivering, dat wil zeggen, gegevensopslag ' hot ' in Azure Cosmos DB en na verloop van tijd 'koude gegevens' naar [Azure Blob Storage](../storage/common/storage-introduction.md) of [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45787-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="45787-124">Batch analytics implementeren op de gegevens met [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="45787-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="45787-125">Implementeer [lambda pijplijnen op Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="45787-126">Azure Cosmos DB biedt een schaalbare database-oplossing die kan opname en query verwerken en implementeren van lambda-architecturen met lage totale Eigendomskosten.</span><span class="sxs-lookup"><span data-stu-id="45787-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="45787-127">Nul uitvaltijd migraties naar een andere Azure DB die Cosmos-account met een andere partitieschema niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="45787-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="45787-128">**Lambda pijplijnen met Azure Cosmos DB voor opname en -query:**</span><span class="sxs-lookup"><span data-stu-id="45787-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Lambda-pijplijn voor opname en query op basis van Azure Cosmos-DB](./media/change-feed/lambda.png)

<span data-ttu-id="45787-130">U kunt Azure Cosmos-database gebruiken voor het ontvangen en opslaan van gebeurtenisgegevens van apparaten, sensoren, infrastructuur en toepassingen en verwerken van deze gebeurtenissen in realtime met [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), of [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45787-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="45787-131">Binnen uw [zonder server](http://azure.com/serverless) web- en mobiele apps, kunt u de gebeurtenissen bijhouden zoals wijzigingen in uw klant profiel, voorkeuren of locatie voor het activeren van bepaalde acties zoals pushmeldingen verzenden naar hun apparaten via [ Azure Functions](../azure-functions/functions-bindings-documentdb.md) of [App Services](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="45787-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="45787-132">Als u gebruikmaakt van Azure DB die Cosmos om een spel samen te stellen, kunt u, bijvoorbeeld gebruik feed voor het implementeren van realtime scoreborden op basis van scores van voltooide games wijzigen.</span><span class="sxs-lookup"><span data-stu-id="45787-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="45787-133">De werking van de feed wijzigen in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="45787-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="45787-134">Azure Cosmos DB biedt de mogelijkheid updates die zijn aangebracht aan een verzameling Azure Cosmos DB stapsgewijs te lezen.</span><span class="sxs-lookup"><span data-stu-id="45787-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="45787-135">Deze wijziging feed heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="45787-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="45787-136">Wijzigingen zijn in Azure Cosmos DB permanent en asynchroon kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="45787-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="45787-137">Wijzigingen in de documenten binnen een verzameling zijn beschikbaar in de feed wijziging onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="45787-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="45787-138">Elke wijziging in een document wordt slechts één keer weergegeven in de feed wijziging en clients beheren hun logica plaatsen van controlepunten.</span><span class="sxs-lookup"><span data-stu-id="45787-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="45787-139">De wijziging feed processor-bibliotheek biedt plaatsen van controlepunten en 'ten minste eenmaal' semantiek.</span><span class="sxs-lookup"><span data-stu-id="45787-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="45787-140">Alleen de meest recente wijziging voor een bepaald document is opgenomen in het logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="45787-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="45787-141">Tussentijdse wijzigingen zijn mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="45787-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="45787-142">De feed wijzigen is door wijzigingen in elke waarde voor de partitiesleutel gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="45787-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="45787-143">Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="45787-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="45787-144">Wijzigingen kunnen worden gesynchroniseerd vanuit elk punt in tijd, er is geen vaste Gegevensretentieperiode waarvoor wijzigingen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="45787-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="45787-145">Wijzigingen zijn beschikbaar in segmenten van de partitie sleutelbereiken.</span><span class="sxs-lookup"><span data-stu-id="45787-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="45787-146">Op deze manier kunt wijzigingen in grote verzamelingen parallel worden verwerkt door meerdere gebruikers /-servers.</span><span class="sxs-lookup"><span data-stu-id="45787-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="45787-147">Toepassingen kunnen aanvragen voor meerdere wijziging feeds gelijktijdig op dezelfde verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="45787-148">Azure Cosmos-DB wijzigen feed is standaard ingeschakeld voor alle accounts.</span><span class="sxs-lookup"><span data-stu-id="45787-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="45787-149">U kunt uw [ingerichte doorvoer](request-units.md) in uw regio schrijven of een willekeurige [regio lezen](distribute-data-globally.md) om te lezen van de feed wijziging, net als elke andere bewerking van de Azure Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="45787-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="45787-150">De feed wijziging omvat INSERT en update-bewerkingen die zijn aangebracht in de documenten binnen de verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="45787-151">U kunt vastleggen verwijderingen door een 'soft-delete' vlag binnen uw documenten in plaats van verwijderingen.</span><span class="sxs-lookup"><span data-stu-id="45787-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="45787-152">U kunt ook een eindige vervalperiode voor uw documenten via instellen de [TTL mogelijkheid](time-to-live.md), bijvoorbeeld 24 uur en gebruik de waarde van die eigenschap voor het vastleggen van verwijderingen.</span><span class="sxs-lookup"><span data-stu-id="45787-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="45787-153">Met deze oplossing hebt u wijzigingen verwerken binnen een kortere periode dan de TTL verloopperiode.</span><span class="sxs-lookup"><span data-stu-id="45787-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="45787-154">De feed wijziging is beschikbaar voor elke partitiesleutelbereik binnen de documentenverzameling en dus kan worden verdeeld over een of meer consumenten voor parallelle verwerking.</span><span class="sxs-lookup"><span data-stu-id="45787-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Feed voor gedistribueerde verwerking van Azure Cosmos DB wijzigen](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="45787-156">U hebt een aantal opties in de manier waarop u een wijziging in de feed in uw clientcode implementeert.</span><span class="sxs-lookup"><span data-stu-id="45787-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="45787-157">De volgende secties onmiddellijk wordt beschreven hoe de wijziging feed met behulp van de REST-API van Azure Cosmos-database en de DocumentDB SDK's implementeren.</span><span class="sxs-lookup"><span data-stu-id="45787-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="45787-158">Echter voor .NET-toepassingen, wordt u aangeraden de nieuwe [wijziging feed processor bibliotheek](#change-feed-processor) feed voor de verwerking van gebeurtenissen van de wijziging naar lezen wijzigingen meerdere partities vereenvoudigt en kunt meerdere threads in werkt Parallel.</span><span class="sxs-lookup"><span data-stu-id="45787-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="45787-159"><a id="rest-apis"></a>Werken met de REST-API en de DocumentDB SDK 's</span><span class="sxs-lookup"><span data-stu-id="45787-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="45787-160">Azure Cosmos DB biedt elastische containers voor opslag en doorvoer aangeroepen **verzamelingen**.</span><span class="sxs-lookup"><span data-stu-id="45787-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="45787-161">Gegevens in verzamelingen is logisch zijn gegroepeerd met [partitie sleutels](partition-data.md) voor schaalbaarheid en prestaties.</span><span class="sxs-lookup"><span data-stu-id="45787-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="45787-162">Azure Cosmos DB biedt verschillende API's voor toegang tot deze gegevens, met inbegrip van lookup-ID (lezen/Get), query en lees-feeds (scans).</span><span class="sxs-lookup"><span data-stu-id="45787-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="45787-163">De feed wijziging kan worden verkregen met twee nieuwe aanvraagheaders tot de DocumentDB in te vullen `ReadDocumentFeed` API, en over het bereiken van partitiesleutels parallel kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="45787-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="45787-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="45787-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="45787-165">U gaat nu een korte kijken hoe ReadDocumentFeed werkt.</span><span class="sxs-lookup"><span data-stu-id="45787-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="45787-166">Azure Cosmos DB ondersteunt het lezen van een feed van documenten binnen een verzameling via de `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="45787-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="45787-167">De volgende aanvraag resulteert bijvoorbeeld een pagina van de documenten binnen de `serverlogs` verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="45787-168">Resultaten kunnen worden beperkt met behulp van de `x-ms-max-item-count` header en gelezen kunnen worden hervat door opnieuw indienen van de aanvraag met een `x-ms-continuation` header in het vorige antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="45787-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="45787-169">Wanneer dit wordt uitgevoerd op één enkele client `ReadDocumentFeed` doorlopen resultaten meerdere partities opeenvolgend.</span><span class="sxs-lookup"><span data-stu-id="45787-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="45787-170">**Seriële lezen feed document**</span><span class="sxs-lookup"><span data-stu-id="45787-170">**Serial read document feed**</span></span>

<span data-ttu-id="45787-171">U kunt ook de feed van documenten met een van de ondersteunde ophalen [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="45787-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="45787-172">Bijvoorbeeld, het volgende fragment toont hoe u de [ReadDocumentFeedAsync methode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span><span class="sxs-lookup"><span data-stu-id="45787-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="45787-173">Gedistribueerde uitvoering van ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="45787-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="45787-174">Voor verzamelingen die een groot aantal updates opnemen of terabytes aan gegevens of meer bevatten, seriële uitvoering van lees-feed van een enkelvoudige clientcomputer mogelijk geen praktische.</span><span class="sxs-lookup"><span data-stu-id="45787-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="45787-175">Om deze big data-scenario's te ondersteunen, biedt Azure Cosmos DB API's te distribueren `ReadDocumentFeed` aanroepen transparant tussen meerdere client lezers/gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45787-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="45787-176">**Gedistribueerde lezen Document Feed**</span><span class="sxs-lookup"><span data-stu-id="45787-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="45787-177">Om te bieden schaalbare verwerking van incrementele wijzigingen Azure Cosmos DB ondersteunt een scale-out-model voor de feed API op basis van de bereiken van partitiesleutels wijziging.</span><span class="sxs-lookup"><span data-stu-id="45787-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="45787-178">U kunt een lijst van de partitie ophalen sleutelbereiken voor het uitvoeren van een verzameling een `ReadPartitionKeyRanges` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="45787-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="45787-179">U kunt uitvoeren voor elke partitiesleutelbereik een `ReadDocumentFeed` om documenten te lezen met partitiesleutels binnen dat bereik valt.</span><span class="sxs-lookup"><span data-stu-id="45787-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="45787-180">Bij het ophalen van partitie sleutelbereiken voor een verzameling</span><span class="sxs-lookup"><span data-stu-id="45787-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="45787-181">U kunt de sleutelbereiken partitie ophalen door het aanvragen van de `pkranges` bron binnen een verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="45787-182">Bijvoorbeeld de volgende aanvraag opgehaald in de lijst met belangrijke bereiken van de partitie voor de `serverlogs` verzameling:</span><span class="sxs-lookup"><span data-stu-id="45787-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="45787-183">Deze aanvraag retourneert het volgende antwoord met metagegevens over de partitie sleutel bereiken:</span><span class="sxs-lookup"><span data-stu-id="45787-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

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


<span data-ttu-id="45787-184">**Partitie-eigenschappen van de belangrijkste bereik**: elke partitiesleutelbereik bevat de eigenschappen van metagegevens in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="45787-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="45787-185">Header-naam</span><span class="sxs-lookup"><span data-stu-id="45787-185">Header name</span></span></th>
        <th><span data-ttu-id="45787-186">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45787-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-187">id</span><span class="sxs-lookup"><span data-stu-id="45787-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="45787-188">De ID voor de partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="45787-188">The ID for the partition key range.</span></span> <span data-ttu-id="45787-189">Dit is een stabiele en de unieke ID binnen elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="45787-190">Moet worden gebruikt in de aanroep van de volgende wijzigingen lezen door partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="45787-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="45787-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="45787-192">De maximumgrootte van een partitie sleutelhash-waarde voor de partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="45787-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="45787-193">Voor intern gebruik.</span><span class="sxs-lookup"><span data-stu-id="45787-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="45787-194">minInclusive</span></span></td>
        <td><span data-ttu-id="45787-195">De minimale partitie sleutelhash-waarde voor de partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="45787-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="45787-196">Voor intern gebruik.</span><span class="sxs-lookup"><span data-stu-id="45787-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="45787-197">U kunt dit doen met behulp van een van de ondersteunde [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="45787-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="45787-198">Bijvoorbeeld het volgende fragment toont hoe op te halen van de partitie sleutelbereiken aan .NET met de [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) methode.</span><span class="sxs-lookup"><span data-stu-id="45787-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="45787-199">Azure Cosmos DB ophalen van documenten per partitiesleutelbereik ondersteunt door de optionele `x-ms-documentdb-partitionkeyrangeid` header.</span><span class="sxs-lookup"><span data-stu-id="45787-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="45787-200">Uitvoeren van een incrementele ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="45787-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="45787-201">ReadDocumentFeed ondersteunt de volgende scenario's / taken voor incrementele verwerking van wijzigingen in Azure Cosmos DB verzamelingen:</span><span class="sxs-lookup"><span data-stu-id="45787-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="45787-202">Alle wijzigingen naar documenten vanaf het begin dat wil zeggen lezen van een verzameling maken.</span><span class="sxs-lookup"><span data-stu-id="45787-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="45787-203">Alle wijzigingen die in toekomstige updates voor documenten van huidige tijd of eventuele wijzigingen sinds een opgegeven gebruiker lezen.</span><span class="sxs-lookup"><span data-stu-id="45787-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="45787-204">Alle wijzigingen naar documenten lezen van een logische versie van de verzameling (ETag).</span><span class="sxs-lookup"><span data-stu-id="45787-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="45787-205">U kunt uw consumenten op basis van de geretourneerde ETag van incrementele lezen-feed van aanvragen controlepunt.</span><span class="sxs-lookup"><span data-stu-id="45787-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="45787-206">De wijzigingen die zijn ingevoegd en updates van documenten.</span><span class="sxs-lookup"><span data-stu-id="45787-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="45787-207">Om vast te leggen verwijdert, moet u een eigenschap 'soft delete' gebruiken in uw documenten of gebruik de [ingebouwde TTL eigenschap](time-to-live.md) om aan te geven van een in behandeling zijnde verwijdering van de feed veranderen.</span><span class="sxs-lookup"><span data-stu-id="45787-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="45787-208">De volgende tabel bevat de [aanvraag](/rest/api/documentdb/common-documentdb-rest-request-headers.md) en [antwoordheaders](/rest/api/documentdb/common-documentdb-rest-response-headers.md) voor ReadDocumentFeed bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="45787-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="45787-209">**Aanvraagheaders voor incrementele ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="45787-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="45787-210">Header-naam</span><span class="sxs-lookup"><span data-stu-id="45787-210">Header name</span></span></th>
        <th><span data-ttu-id="45787-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45787-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-212">EEN IM</span><span class="sxs-lookup"><span data-stu-id="45787-212">A-IM</span></span></td>
        <td><span data-ttu-id="45787-213">Moet worden ingesteld op 'Incrementele feed', of anders weggelaten</span><span class="sxs-lookup"><span data-stu-id="45787-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="45787-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="45787-215">Er is geen header: retourneert alle wijzigingen vanaf het begin (verzameling maken)</span><span class="sxs-lookup"><span data-stu-id="45787-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="45787-216">' * ': retourneert alle nieuwe wijzigingen aan gegevens binnen de verzameling</span><span class="sxs-lookup"><span data-stu-id="45787-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="45787-217">&lt;ETag&gt;: als is ingesteld op een verzameling ETag, retourneert alle wijzigingen die sinds logische tijdstempel</span><span class="sxs-lookup"><span data-stu-id="45787-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="45787-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="45787-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="45787-219">RFC 1123 tijdnotatie; genegeerd als If-None-Match is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="45787-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="45787-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="45787-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="45787-221">De belangrijkste bereik partitie-ID voor het lezen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="45787-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="45787-222">**Antwoordheaders voor incrementele ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="45787-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="45787-223">Header-naam</span><span class="sxs-lookup"><span data-stu-id="45787-223">Header name</span></span></th>
        <th><span data-ttu-id="45787-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45787-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-225">ETag</span><span class="sxs-lookup"><span data-stu-id="45787-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="45787-226">De logische LSN (sequence number) van de laatste document in het antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="45787-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="45787-227">Incrementele ReadDocumentFeed kan worden hervat door deze waarde in de If-None-Match opnieuw.</span><span class="sxs-lookup"><span data-stu-id="45787-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="45787-228">Hier volgt een voorbeeld van een aanvraag om te retourneren van alle incrementele wijzigingen in de verzameling van de logische versie/ETag `28535` en partitioneren van de belangrijkste bereik = `16`:</span><span class="sxs-lookup"><span data-stu-id="45787-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="45787-229">Wijzigingen zijn geordend op tijd binnen elke waarde voor de partitiesleutel binnen de partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="45787-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="45787-230">Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="45787-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="45787-231">Als er meer resultaten dan in één pagina passen, kunt u de volgende pagina van de resultaten lezen door deze opnieuw indienen van de aanvraag met de `If-None-Match` header met waarde gelijk is aan de `etag` uit het vorige antwoord.</span><span class="sxs-lookup"><span data-stu-id="45787-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="45787-232">Als meerdere documenten zijn ingevoegd of Transactioneel binnen een opgeslagen procedure of trigger bijgewerkt, ze alle geretourneerd binnen dezelfde antwoordpagina.</span><span class="sxs-lookup"><span data-stu-id="45787-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="45787-233">Met de feed wijziging, krijgt u mogelijk meer items geretourneerd in een pagina, dan is opgegeven in `x-ms-max-item-count` in het geval van meerdere documenten ingevoegd of geüpdatet binnen een opgeslagen procedures of triggers.</span><span class="sxs-lookup"><span data-stu-id="45787-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="45787-234">Wanneer u de .NET SDK (1.17.0), stelt u het veld `StartTime` in `ChangeFeedOptions` rechtstreeks gewijzigde documenten sinds retourneren `StartTime` bij het aanroepen van `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="45787-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="45787-235">Door op te geven `If-Modified-Since` met de REST API, uw aanvraag wordt geretourneerd niet de documenten zelf, maar in plaats daarvan het vervolgtoken of `etag` in de antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="45787-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="45787-236">Om te retourneren van de documenten gewijzigd in de opgegeven tijd, het vervolgtoken `etag` moet vervolgens worden gebruikt in de volgende aanvraag met `If-None-Match` te retourneren van de werkelijke documenten.</span><span class="sxs-lookup"><span data-stu-id="45787-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="45787-237">De .NET SDK biedt de [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) en [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helperklassen voor toegang tot de wijzigingen die zijn aangebracht aan een verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="45787-238">Het volgende fragment toont hoe op te halen van alle wijzigingen vanaf het begin met de .NET SDK uit één client.</span><span class="sxs-lookup"><span data-stu-id="45787-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

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
<span data-ttu-id="45787-239">En het volgende fragment toont het verwerken van wijzigingen in realtime met Azure Cosmos DB met behulp van de wijziging-feed ondersteuning en de voorgaande functie.</span><span class="sxs-lookup"><span data-stu-id="45787-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="45787-240">De eerste aanroep retourneert alle documenten in de verzameling en de tweede retourneert alleen de twee documenten die zijn gemaakt sinds het laatste controlepunt zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45787-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="45787-241">U kunt ook filteren op de wijziging feed met behulp van de logica voor de client selectief om gebeurtenissen te verwerken.</span><span class="sxs-lookup"><span data-stu-id="45787-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="45787-242">Dit is bijvoorbeeld een codefragment die clientzijde LINQ gebruikt voor het verwerken van gebeurtenissen voor wijzigingen in alleen temperatuur van apparaat sensoren.</span><span class="sxs-lookup"><span data-stu-id="45787-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="45787-243"><a id="change-feed-processor"></a>Bibliotheek van de Feed Processor wijzigingsbeheer</span><span class="sxs-lookup"><span data-stu-id="45787-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="45787-244">Een andere optie is met de [Azure Cosmos DB wijzigen Feed Processor bibliotheek](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), kunt u eenvoudig distribueren voor gebeurtenisverwerking van een wijziging in de feed in meerdere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45787-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="45787-245">De bibliotheek is ideaal voor het bouwen van wijziging feed lezers van het .NET-platform.</span><span class="sxs-lookup"><span data-stu-id="45787-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="45787-246">Sommige werkstromen die zouden worden vereenvoudigd door middel van de wijziging Feed Processor-bibliotheek via de methoden die zijn opgenomen in de andere Cosmos DB-SDK's zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="45787-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="45787-247">Opvragen van de updates van wijziging feed wanneer gegevens worden opgeslagen op verschillende partities</span><span class="sxs-lookup"><span data-stu-id="45787-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="45787-248">Verplaatsen of het repliceren van gegevens uit een verzameling naar een andere</span><span class="sxs-lookup"><span data-stu-id="45787-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="45787-249">Parallelle uitvoering van de acties die worden geactiveerd door software-updates tot gegevens en feed wijzigen</span><span class="sxs-lookup"><span data-stu-id="45787-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="45787-250">Terwijl met de API's in de Cosmos-SDK's nauwkeurig toegang tot de feed-updates in elke partitie bevat, vereenvoudigt met behulp van de Feed Processor wijzigen bibliotheek lezen wijzigingen in partities en meerdere threads die parallel werken.</span><span class="sxs-lookup"><span data-stu-id="45787-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="45787-251">In plaats van handmatig lezen wijzigingen van elke container en een vervolgtoken voor elke partitie opslaan, beheert de wijziging Feed Processor lezen wijzigingen automatisch meerdere partities met een lease-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="45787-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="45787-252">De bibliotheek is beschikbaar als een NuGet-pakket: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) en van broncode als een Github [voorbeeld](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="45787-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="45787-253">Understanding wijziging Feed Processor-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="45787-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="45787-254">Vier belangrijke onderdelen van de implementatie van de Feed Processor van wijziging: de bewaakte verzameling, de verzameling van de lease, de processor-host en de consumenten.</span><span class="sxs-lookup"><span data-stu-id="45787-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="45787-255">**Bewaakte verzameling:** de bewaakte verzameling is de gegevens op basis waarvan de feed wijziging is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="45787-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="45787-256">Eventuele toevoegingen en wijzigingen in de bewaakte verzameling worden doorgevoerd in de feed wijziging van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="45787-257">**Verzameling van de lease:** de lease verzameling coördinaten verwerking van de feed in meerdere werknemers wijziging.</span><span class="sxs-lookup"><span data-stu-id="45787-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="45787-258">Een verzameling afzonderlijke wordt gebruikt voor het opslaan van de leases met een lease per partitie.</span><span class="sxs-lookup"><span data-stu-id="45787-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="45787-259">Het is nuttig voor het opslaan van deze verzameling lease op een ander account met de regio schrijven dichter aan waarop de wijziging Feed Processor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45787-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="45787-260">Een lease-object bevat de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="45787-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="45787-261">Eigenaar: Hiermee geeft u op de host die eigenaar is van de lease</span><span class="sxs-lookup"><span data-stu-id="45787-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="45787-262">Voortzetting: Geeft de positie (vervolgtoken) in de feed voor een bepaalde partitie wijziging</span><span class="sxs-lookup"><span data-stu-id="45787-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="45787-263">Tijdstempel: Tijd van laatste lease is bijgewerkt. de tijdstempel kan worden gebruikt om te controleren of de lease is verlopen</span><span class="sxs-lookup"><span data-stu-id="45787-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="45787-264">**Processor Host:** elke host bepaalt hoeveel partities verwerken op basis van hoeveel andere exemplaren van hosts actieve leases hebben.</span><span class="sxs-lookup"><span data-stu-id="45787-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="45787-265">Wanneer u een host start, verkrijgt deze leases om de werkbelasting kan worden verdeeld over alle hosts.</span><span class="sxs-lookup"><span data-stu-id="45787-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="45787-266">Een host vernieuwt periodiek leases, dus leases actief blijven.</span><span class="sxs-lookup"><span data-stu-id="45787-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="45787-267">Een host controlepunten lezen voor de laatste vervolgtoken aan de lease voor elk.</span><span class="sxs-lookup"><span data-stu-id="45787-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="45787-268">Een host controleert gelijktijdigheid om veiligheid te garanderen, de ETag voor elke update lease.</span><span class="sxs-lookup"><span data-stu-id="45787-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="45787-269">Andere strategieën controlepunt worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="45787-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="45787-270">Bij het afsluiten, is een host alle leases worden vrijgegeven, maar blijft de informatie over de voortzetting dus bij het lezen van het controlepunt van de opgeslagen later kan worden hervat.</span><span class="sxs-lookup"><span data-stu-id="45787-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="45787-271">Het aantal hosts mag niet groter zijn dan het aantal partities (leases) op dit moment.</span><span class="sxs-lookup"><span data-stu-id="45787-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="45787-272">**Consumenten:** consumenten of werknemers, zijn de threads die de verwerking van de wijziging feed gestart door elke host uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="45787-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="45787-273">Elke host processor kan meerdere gebruikers hebben.</span><span class="sxs-lookup"><span data-stu-id="45787-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="45787-274">Elke consumer leest de wijziging feed uit de partitie die is toegewezen aan en ontvangt een melding van de host van wijzigingen en verlopen van leases.</span><span class="sxs-lookup"><span data-stu-id="45787-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="45787-275">Om verder te begrijpen hoe deze vier elementen van wijziging Feed Processor samenwerken, bekijk een voorbeeld in het volgende diagram.</span><span class="sxs-lookup"><span data-stu-id="45787-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="45787-276">De bewaakte verzameling documenten worden opgeslagen en gebruikt de 'plaats' als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="45787-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="45787-277">We zien dat de blauwe partitie enzovoort documenten met het veld 'plaats' uit "A-E" bevat.</span><span class="sxs-lookup"><span data-stu-id="45787-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="45787-278">Er zijn twee hosts, elk met twee consumenten lezen van de vier partities parallel.</span><span class="sxs-lookup"><span data-stu-id="45787-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="45787-279">De pijlen geven het lezen van een specifieke positie in de feed wijziging consumenten.</span><span class="sxs-lookup"><span data-stu-id="45787-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="45787-280">In de eerste partitie vertegenwoordigt de donkere blauw ongelezen wijzigingen terwijl de lichte blauw de al gelezen wijzigingen in de feed wijzigen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="45787-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="45787-281">De hosts de lease-verzameling gebruiken voor het opslaan van een waarde 'voortzetting' om de huidige positie lezen voor elke consumer bij te houden.</span><span class="sxs-lookup"><span data-stu-id="45787-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Met behulp van de wijziging Azure Cosmos DB feed processor host](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="45787-283">Met behulp van de wijziging Feed Processor-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="45787-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="45787-284">De volgende sectie wordt uitgelegd hoe u van de bibliotheek wijzigen Feed Processor in de context van het repliceren van wijzigingen uit een bronverzameling naar een doelverzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="45787-285">De bronverzameling is hier de bewaakte verzameling in de Feed wijziging-Processor.</span><span class="sxs-lookup"><span data-stu-id="45787-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="45787-286">**Installeren en de wijziging Feed Processor NuGet-pakket opnemen**</span><span class="sxs-lookup"><span data-stu-id="45787-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="45787-287">Voordat u wijziging Feed Processor NuGet-pakket installeert, eerst installeren:</span><span class="sxs-lookup"><span data-stu-id="45787-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="45787-288">Microsoft.Azure.DocumentDB, versie 1.13.1 of hoger</span><span class="sxs-lookup"><span data-stu-id="45787-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="45787-289">Newtonsoft.Json, versie 9.0.1 of hoger installeren `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` en deze opnemen als een verwijzing.</span><span class="sxs-lookup"><span data-stu-id="45787-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="45787-290">**Een gecontroleerde, lease- en verzameling maken**</span><span class="sxs-lookup"><span data-stu-id="45787-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="45787-291">Om de wijziging Feed Processor bibliotheek gebruiken, moet de verzameling van de lease worden gemaakt voordat de processor host (s) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45787-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="45787-292">Opnieuw, is het raadzaam een lease-verzameling opslaan op een ander account met een regio schrijven dichter aan waarop de wijziging Feed Processor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45787-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="45787-293">In dit voorbeeld verplaatsing van gegevens moet maken van de doelverzameling zouden worden voordat de wijziging Feed Processor host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45787-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="45787-294">In de voorbeeldcode noemen we een Help-methode voor het maken van de bewaakte geleasete, en de bestemming verzamelingen als deze niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="45787-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="45787-295">Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor de toepassing om te communiceren met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="45787-296">Voor meer informatie raadpleegt u de [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="45787-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="45787-297">*Maken van een host processor*</span><span class="sxs-lookup"><span data-stu-id="45787-297">*Creating a processor host*</span></span>

<span data-ttu-id="45787-298">De `ChangeFeedProcessorHost` klasse biedt een thread-veilige, met meerdere processen en veilige runtime-omgeving voor gebeurtenisprocessors die ook het plaatsen van controlepunten en partitie lease biedt.</span><span class="sxs-lookup"><span data-stu-id="45787-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="45787-299">Gebruik de `ChangeFeedProcessorHost` klasse, die u kunt implementeren `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="45787-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="45787-300">Deze interface bevat drie methoden:</span><span class="sxs-lookup"><span data-stu-id="45787-300">This interface contains three methods:</span></span>

* <span data-ttu-id="45787-301">`OpenAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijzigen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="45787-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="45787-302">Het kan worden aangepast voor een specifieke actie uitgevoerd wanneer consumenten/zien wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="45787-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="45787-303">`CloseAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijziging wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="45787-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="45787-304">Het kan worden aangepast voor een specifieke actie uitgevoerd wanneer de consument/zien wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="45787-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="45787-305">`ProcessChangesAsync`: Deze functie wordt aangeroepen wanneer nieuwe wijzigingen in het document beschikbaar op de feed wijzigen zijn.</span><span class="sxs-lookup"><span data-stu-id="45787-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="45787-306">Het kan worden aangepast voor een specifieke actie na elke wijziging feed update uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45787-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="45787-307">In ons voorbeeld wordt de interface implementeren `IChangeFeedObserver` via de `DocumentFeedObserver` klasse.</span><span class="sxs-lookup"><span data-stu-id="45787-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="45787-308">Hier de `ProcessChangesAsync` upserts (updates) een document van de wijziging in de doelverzameling feed werken.</span><span class="sxs-lookup"><span data-stu-id="45787-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="45787-309">In dit voorbeeld is nuttig voor het verplaatsen van gegevens uit een verzameling naar een andere om te wijzigen van de partitiesleutel van een gegevensset.</span><span class="sxs-lookup"><span data-stu-id="45787-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="45787-310">*De Processor-Host wordt uitgevoerd*</span><span class="sxs-lookup"><span data-stu-id="45787-310">*Running the Processor Host*</span></span>

<span data-ttu-id="45787-311">Beide opties voor feed wijzigen voordat u begint met de verwerking van gebeurtenissen, en opties van de feed host wijzigen kunnen worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="45787-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="45787-312">De specifieke velden die kunnen worden aangepast worden samengevat in de volgende tabellen.</span><span class="sxs-lookup"><span data-stu-id="45787-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="45787-313">**Opties voor Feed wijzigen**:</span><span class="sxs-lookup"><span data-stu-id="45787-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="45787-314">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="45787-314">Property Name</span></span></th>
        <th><span data-ttu-id="45787-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45787-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="45787-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="45787-317">Opgehaald of ingesteld van het maximum aantal items in de opsomming wordt in de database-service van Azure DB die Cosmos wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="45787-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="45787-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="45787-319">Opgehaald of ingesteld van de partitie-id sleutel bereik voor de huidige aanvraag in de database-service van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="45787-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="45787-321">Opgehaald of ingesteld van de aanvraag vervolgtoken in de database-service van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="45787-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="45787-322">SessionToken</span></span></td>
        <td><span data-ttu-id="45787-323">Opgehaald of ingesteld van het sessietoken voor gebruik met sessieconsistentie in de database-service van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45787-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="45787-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="45787-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="45787-325">Opgehaald of ingesteld of wijziging in de database-service van Azure DB die Cosmos-kanaal moet worden gestart vanaf het begin (true) of van de huidige (false).</span><span class="sxs-lookup"><span data-stu-id="45787-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="45787-326">Standaard wordt gestart vanuit de huidige (false).</span><span class="sxs-lookup"><span data-stu-id="45787-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="45787-327">**Opties voor de Feed Host wijzigen**:</span><span class="sxs-lookup"><span data-stu-id="45787-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="45787-328">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="45787-328">Property Name</span></span></th>
        <th><span data-ttu-id="45787-329">Type</span><span class="sxs-lookup"><span data-stu-id="45787-329">Type</span></span></th>
        <th><span data-ttu-id="45787-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45787-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="45787-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="45787-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45787-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="45787-333">Het interval voor alle leases voor partities die momenteel worden vastgehouden door het ChangeFeedEventHost-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="45787-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="45787-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="45787-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45787-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="45787-336">Het interval voor ere van een taak of partities gelijkmatig zijn verdeeld over exemplaren van de bekende host berekenen.</span><span class="sxs-lookup"><span data-stu-id="45787-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="45787-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="45787-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45787-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="45787-339">Het interval waarvoor de lease op een lease voor een partitie wordt gehouden.</span><span class="sxs-lookup"><span data-stu-id="45787-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="45787-340">Als de lease is niet vernieuwd binnen dit interval, het is verlopen en eigendom van de partitie worden verplaatst naar een ander exemplaar van ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="45787-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="45787-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="45787-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45787-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="45787-343">De vertraging tussen een partitie polling voor nieuwe wijzigingen op de feed, nadat alle huidige wijzigingen zijn geleegd.</span><span class="sxs-lookup"><span data-stu-id="45787-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="45787-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="45787-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="45787-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="45787-346">De frequentie controlepunt leases.</span><span class="sxs-lookup"><span data-stu-id="45787-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="45787-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="45787-348">int</span><span class="sxs-lookup"><span data-stu-id="45787-348">Int</span></span></td>
        <td><span data-ttu-id="45787-349">Het aantal minimale partitie voor de host.</span><span class="sxs-lookup"><span data-stu-id="45787-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="45787-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="45787-351">int</span><span class="sxs-lookup"><span data-stu-id="45787-351">Int</span></span></td>
        <td><span data-ttu-id="45787-352">Het maximale aantal partities die de host kan fungeren.</span><span class="sxs-lookup"><span data-stu-id="45787-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="45787-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="45787-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="45787-354">BOOL</span><span class="sxs-lookup"><span data-stu-id="45787-354">Bool</span></span></td>
        <td><span data-ttu-id="45787-355">Hiermee wordt aangegeven of bij het starten van de host alle bestaande leases moeten worden verwijderd en de host moet worden gestart vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="45787-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="45787-356">Voor het starten van de verwerking van gebeurtenissen instantiëren `ChangeFeedProcessorHost`, bied de juiste parameters voor uw Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="45787-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="45787-357">Roep vervolgens `RegisterObserverAsync` registreren uw `IChangeFeedObserver` (DocumentFeedObserver in dit voorbeeld)-implementatie met de runtime.</span><span class="sxs-lookup"><span data-stu-id="45787-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="45787-358">Op dit moment probeert de host een lease op elke partitiesleutelbereik in de Azure DB die Cosmos-verzameling met behulp van een greedy-algoritme te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="45787-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="45787-359">Deze leases gedurende een bepaald tijdsbestek geldig en moeten daarna worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="45787-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="45787-360">Zodra nieuwe knooppunten worker-exemplaren in dit geval online komen, ze reserveringen voor leases en gedurende een bepaalde periode de belasting verschuift tussen knooppunten elke host probeert te verkrijgen van meer leases.</span><span class="sxs-lookup"><span data-stu-id="45787-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="45787-361">In de voorbeeldcode gebruiken we een factory klasse (DocumentFeedObserverFactory.cs) voor het maken van een zien en de `RegistObserverFactoryAsync` registreren van de zien.</span><span class="sxs-lookup"><span data-stu-id="45787-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="45787-362">In de loop van de tijd komt er een evenwicht tot stand.</span><span class="sxs-lookup"><span data-stu-id="45787-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="45787-363">Deze dynamische mogelijkheid kan automatisch schalen om te worden toegepast op gebruikers voor schaal omhoog en omlaag schalen op basis van CPU.</span><span class="sxs-lookup"><span data-stu-id="45787-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="45787-364">Als er wijzigingen zijn beschikbaar in Azure Cosmos DB sneller dan consumers kunnen verwerken, kan de toename van de CPU op consumenten ervoor zorgen dat een automatisch geschaald op het aantal worker-instantie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="45787-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45787-365">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45787-365">Next steps</span></span>
* <span data-ttu-id="45787-366">Probeer de [Azure Cosmos DB Wijzig feed codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="45787-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="45787-367">Aan de slag programmeren met de [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md) of de [REST-API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="45787-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
