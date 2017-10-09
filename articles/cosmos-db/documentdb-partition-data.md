---
title: aaaPartitioning en schalen in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe partitionering werkt in Azure Cosmos DB hoe tooconfigure partitioneren en partitiesleutels en hoe toopick Hallo rechts partitie-sleutel voor uw toepassing.
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="4d309-103">Partitioneren in Azure Cosmos DB met Hallo DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="4d309-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="4d309-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is een globale gedistribueerde en modellen database service ontworpen toohelp u bereiken snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met uw toepassing wanneer het groeit.</span><span class="sxs-lookup"><span data-stu-id="4d309-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="4d309-105">Dit artikel bevat een overzicht van hoe toowork met het partitioneren van de Cosmos-DB containers met DocumentDB API Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d309-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4d309-106">Zie [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="4d309-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="4d309-107">tooget gestart met code, Hallo-project downloaden [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4d309-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="4d309-108">Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4d309-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="4d309-109">Hoe werkt partitionering in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4d309-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="4d309-110">Hoe configureer partitioneren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4d309-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="4d309-111">Wat partitiesleutels zijn en hoe ik Hallo rechts partitiesleutel kiezen voor de toepassing?</span><span class="sxs-lookup"><span data-stu-id="4d309-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="4d309-112">tooget gestart met code, Hallo-project downloaden [Azure Cosmos DB prestaties testen stuurprogramma Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4d309-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="4d309-113">Partitiesleutels</span><span class="sxs-lookup"><span data-stu-id="4d309-113">Partition keys</span></span>

<span data-ttu-id="4d309-114">Hallo DocumentDB API Geef Hallo partitie sleuteldefinitie Hallo vorm van een JSON-pad.</span><span class="sxs-lookup"><span data-stu-id="4d309-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="4d309-115">Hallo ziet volgende tabel u voorbeelden van partitie basisdefinities en Hallo waarden tooeach overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="4d309-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="4d309-116">Hallo partitiesleutel is opgegeven als een pad, bijvoorbeeld `/department` vertegenwoordigt Hallo eigenschap afdeling.</span><span class="sxs-lookup"><span data-stu-id="4d309-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="4d309-117"><strong>Partitiesleutel</strong></span><span class="sxs-lookup"><span data-stu-id="4d309-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4d309-118"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="4d309-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4d309-119">/Department</span><span class="sxs-lookup"><span data-stu-id="4d309-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4d309-120">Komt overeen toohello waarde van doc.department waarbij doc Hallo item is.</span><span class="sxs-lookup"><span data-stu-id="4d309-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4d309-121">Eigenschappen/naam</span><span class="sxs-lookup"><span data-stu-id="4d309-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4d309-122">Komt overeen toohello waarde van doc.properties.name waarbij doc Hallo item (de geneste eigenschap) is.</span><span class="sxs-lookup"><span data-stu-id="4d309-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4d309-123">/ID</span><span class="sxs-lookup"><span data-stu-id="4d309-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4d309-124">Komt overeen met de waarde van doc.id toohello (sleutel-id en partitie zijn Hallo dezelfde eigenschap).</span><span class="sxs-lookup"><span data-stu-id="4d309-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4d309-125">/ 'afdeling name'</span><span class="sxs-lookup"><span data-stu-id="4d309-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4d309-126">Komt overeen toohello waarde van doc ["afdelingsnaam"], waarbij doc Hallo item is.</span><span class="sxs-lookup"><span data-stu-id="4d309-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="4d309-127">Hallo-syntaxis voor de partitiesleutel is vergelijkbaar toohello padspecificatie voor indexering beleid paden met Hallo belangrijke verschil dat pad Hallo overeenkomt met de eigenschap toohello in plaats van Hallo waarde, dus er is geen jokerteken op Hallo end.</span><span class="sxs-lookup"><span data-stu-id="4d309-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="4d309-128">Bijvoorbeeld, geeft u afdeling /?</span><span class="sxs-lookup"><span data-stu-id="4d309-128">For example, you would specify /department/?</span></span> <span data-ttu-id="4d309-129">Hallo tooindex waarden onder afdeling, maar /department opgeven als sleuteldefinitie Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="4d309-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="4d309-130">Hallo partitiesleutel is impliciet geïndexeerd en kan niet worden uitgesloten van het indexeren met indexering beleid onderdrukkingen.</span><span class="sxs-lookup"><span data-stu-id="4d309-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="4d309-131">Bekijk hoe Hallo keuze van de partitiesleutel heeft impact op Hallo prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d309-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="4d309-132">Werken met hello Azure Cosmos DB SDK 's</span><span class="sxs-lookup"><span data-stu-id="4d309-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="4d309-133">Azure Cosmos DB is ondersteuning toegevoegd voor automatische partitionering met [REST API-versie 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4d309-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="4d309-134">In de volgorde toocreate gepartitioneerd containers, moet u de SDK-versies 1.6.0 downloaden of hoger in een van de Hallo ondersteund platforms SDK (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="4d309-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="4d309-135">Containers maken</span><span class="sxs-lookup"><span data-stu-id="4d309-135">Creating containers</span></span>
<span data-ttu-id="4d309-136">Hallo volgende voorbeeld ziet u een .NET-codefragment toocreate een container toostore apparaat telemetriegegevens van 20.000 aanvraageenheden per seconde van doorvoer.</span><span class="sxs-lookup"><span data-stu-id="4d309-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="4d309-137">Hallo SDK stelt Hallo OfferThroughput waarde (die op zijn beurt Hallo ingesteld `x-ms-offer-throughput` aanvraagheader in Hallo REST-API).</span><span class="sxs-lookup"><span data-stu-id="4d309-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="4d309-138">Hier stelt Hallo `/deviceId` als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d309-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="4d309-139">Hallo keuze van de partitiesleutel wordt opgeslagen samen met de rest van metagegevens zoals naam en het indexeringsbeleid Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d309-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="4d309-140">Voor dit voorbeeld wordt gekozen `deviceId` Aangezien we dat weten (a) omdat er een groot aantal apparaten, schrijfbewerkingen kunnen meerdere partities gelijkmatig worden verdeeld en ons toestemming tooscale Hallo database tooingest enorme hoeveelheden gegevens en (b) veel Hallo aanvragen, zoals ophalen van de meest recente lezen Hallo zijn binnen het bereik tooa één apparaat-id voor een apparaat en kunnen worden opgehaald uit een enkele partitie.</span><span class="sxs-lookup"><span data-stu-id="4d309-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="4d309-141">Deze methode maakt een REST-API aanroepen tooCosmos DB en Hallo-service wordt een aantal partities op basis van de aangevraagde doorvoer Hallo inrichten.</span><span class="sxs-lookup"><span data-stu-id="4d309-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4d309-142">U kunt Hallo doorvoer van een container wijzigen wanneer de prestaties van uw behoeften ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="4d309-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="4d309-143">Lezen en schrijven van items</span><span class="sxs-lookup"><span data-stu-id="4d309-143">Reading and writing items</span></span>
<span data-ttu-id="4d309-144">Nu gaan we gegevens invoegen in Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="4d309-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="4d309-145">Hier volgt een voorbeeldklasse met een apparaat bij het lezen en een aanroep van tooCreateDocumentAsync tooinsert een nieuw apparaat lezen in een container.</span><span class="sxs-lookup"><span data-stu-id="4d309-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="4d309-146">Dit is een voorbeeld gebruik Hallo DocumentDB-API:</span><span class="sxs-lookup"><span data-stu-id="4d309-146">This is an example leveraging hello DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="4d309-147">We Hallo item door de partitiesleutel en id lezen, bijwerken en verwijder deze vervolgens als een laatste stap door de partitiesleutel en -id. Opmerking dat Hallo leesbewerkingen een waarde PartitionKey bevatten (overeenkomstige toohello `x-ms-documentdb-partitionkey` aanvraagheader in Hallo REST-API).</span><span class="sxs-lookup"><span data-stu-id="4d309-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="4d309-148">Gepartitioneerde containers doorzoeken</span><span class="sxs-lookup"><span data-stu-id="4d309-148">Querying partitioned containers</span></span>
<span data-ttu-id="4d309-149">Als u automatisch een query met gegevens in gepartitioneerde containers Cosmos DB Hallo routes query toohello partities overeenkomt toohello partitie sleutelwaarden die zijn opgegeven in het Hallo-filter (wanneer aanwezig).</span><span class="sxs-lookup"><span data-stu-id="4d309-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4d309-150">Deze query is bijvoorbeeld gerouteerde toojust Hallo partitie met Hallo partitiesleutel 'XMS-0001'.</span><span class="sxs-lookup"><span data-stu-id="4d309-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4d309-151">Hallo volgende query heeft geen een filter op Hallo partitiesleutel (DeviceId) en is fanned van tooall-partities waar deze wordt uitgevoerd tegen index Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="4d309-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4d309-152">Opmerking u toospecify hello EnableCrossPartitionQuery hebt (`x-ms-documentdb-query-enablecrosspartition` in Hallo REST-API) toohave Hallo SDK tooexecute een query meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="4d309-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="4d309-153">Biedt ondersteuning voor cosmos DB [statistische functies](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` en `AVG` over gepartitioneerd containers met behulp van SQL wordt gestart met de SDK's 1.12.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="4d309-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="4d309-154">Query's moeten een enkel samengestelde operator bevatten en moeten één waarde bevatten in Hallo projectie.</span><span class="sxs-lookup"><span data-stu-id="4d309-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="4d309-155">Parallelle queryuitvoering</span><span class="sxs-lookup"><span data-stu-id="4d309-155">Parallel query execution</span></span>
<span data-ttu-id="4d309-156">Hallo Cosmos DB SDK's 1.9.0 en hierboven ondersteuning parallelle uitvoering queryopties, waarmee u kunt de lage latentie tooperform opgevraagd tegen gepartitioneerde verzamelingen, zelfs wanneer ze nodig hebben tootouch een groot aantal partities.</span><span class="sxs-lookup"><span data-stu-id="4d309-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4d309-157">Hallo na query is bijvoorbeeld geconfigureerde toorun parallel meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="4d309-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4d309-158">U kunt parallelle queryuitvoering beheren door afstemmen Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="4d309-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4d309-159">Door in te stellen `MaxDegreeOfParallelism`, kunt u bepalen Hallo mate van parallelle uitvoering, dat wil zeggen, Hallo maximum aantal gelijktijdige netwerk verbindingen toohello van container partities.</span><span class="sxs-lookup"><span data-stu-id="4d309-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="4d309-160">Als u deze te 1 instelt, worden Hallo mate van parallelle uitvoering wordt beheerd door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="4d309-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4d309-161">Als hello `MaxDegreeOfParallelism` is niet opgegeven of stel too0, de standaardwaarde hello is, zal er een netwerk met één verbinding toohello container partities.</span><span class="sxs-lookup"><span data-stu-id="4d309-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="4d309-162">Door in te stellen `MaxBufferedItemCount`, kunt u handelt uit query latentie en client-side geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="4d309-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4d309-163">Als u deze parameter of stel deze optie te-1, wordt het aantal items in de buffer opgeslagen tijdens parallelle queryuitvoering hello wordt beheerd door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="4d309-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4d309-164">Hallo gegeven dezelfde toestand van de verzameling Hallo een parallelle query retourneert resultaten in dezelfde als in seriële uitvoering volgorde Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d309-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4d309-165">Bij het uitvoeren van een query voor cross-partitie met sorteren (ORDER BY en/of boven) Hallo hello Azure Cosmos DB SDK problemen query parallel in partities ingedeeld en samenvoegingen gedeeltelijk gesorteerde resulteert in het Hallo client side tooproduce globaal besteld resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d309-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="4d309-166">Opgeslagen procedures uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4d309-166">Executing stored procedures</span></span>
<span data-ttu-id="4d309-167">U kunt ook uitvoeren atomische transacties tegen documenten met Hallo dezelfde apparaat-ID, bijvoorbeeld als u statistische functies onderhoudt of Hallo meest recente toestand van een apparaat in één item.</span><span class="sxs-lookup"><span data-stu-id="4d309-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="4d309-168">In de volgende sectie hello kijken we hoe u toopartitioned containers uit één partitie containers kunt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="4d309-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d309-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d309-169">Next steps</span></span>
<span data-ttu-id="4d309-170">In dit artikel wordt een overzicht van hoe toowork met partitionering van Azure DB die Cosmos-containers met DocumentDB API Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="4d309-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4d309-171">Zie ook [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="4d309-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="4d309-172">Schaal en prestaties testen met Azure Cosmos DB uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4d309-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="4d309-173">Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4d309-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="4d309-174">Aan de slag met Hallo coderen [SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="4d309-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="4d309-175">Meer informatie over [ingerichte doorvoer in Azure Cosmos-DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="4d309-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

