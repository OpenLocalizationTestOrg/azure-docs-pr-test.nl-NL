---
title: Partitionering en schalen in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe partitionering werkt in Azure Cosmos DB, partitie-sleutels en configureren met het partitioneren en het kiezen van de juiste partitiesleutel voor uw toepassing.
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
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="88c58-103">Partitioneren in Azure Cosmos-database met de DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="88c58-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="88c58-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is een globale gedistribueerde, meerdere model-database-service waarmee u snel, voorspelbare prestaties en schaalbaarheid naadloos samen met uw toepassing bereiken wanneer deze groeit.</span><span class="sxs-lookup"><span data-stu-id="88c58-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="88c58-105">Dit artikel bevat een overzicht van het werken met het partitioneren van de Cosmos-DB containers met de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="88c58-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="88c58-106">Zie [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="88c58-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="88c58-107">Download het project uit om te beginnen met code [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="88c58-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="88c58-108">Na het lezen van dit artikel kunt u zich de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="88c58-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="88c58-109">Hoe werkt partitionering in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="88c58-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="88c58-110">Hoe configureer partitioneren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="88c58-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="88c58-111">Wat partitiesleutels zijn en hoe ik de juiste partitiesleutel kiezen voor de toepassing?</span><span class="sxs-lookup"><span data-stu-id="88c58-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="88c58-112">Download het project uit om te beginnen met code [Azure Cosmos DB prestaties testen stuurprogramma Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="88c58-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="88c58-113">Partitiesleutels</span><span class="sxs-lookup"><span data-stu-id="88c58-113">Partition keys</span></span>

<span data-ttu-id="88c58-114">In de DocumentDB-API geeft u de definitie van de partitie sleutel in de vorm van een JSON-pad.</span><span class="sxs-lookup"><span data-stu-id="88c58-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="88c58-115">De volgende tabel ziet u voorbeelden van partitie basisdefinities en de waarden die overeenkomen met elke.</span><span class="sxs-lookup"><span data-stu-id="88c58-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="88c58-116">De partitiesleutel is opgegeven als een pad, bijvoorbeeld `/department` vertegenwoordigt de eigenschap afdeling.</span><span class="sxs-lookup"><span data-stu-id="88c58-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="88c58-117"><strong>Partitiesleutel</strong></span><span class="sxs-lookup"><span data-stu-id="88c58-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="88c58-118"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="88c58-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="88c58-119">/Department</span><span class="sxs-lookup"><span data-stu-id="88c58-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="88c58-120">Komt overeen met de waarde van doc.department doc waar het item is.</span><span class="sxs-lookup"><span data-stu-id="88c58-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="88c58-121">Eigenschappen/naam</span><span class="sxs-lookup"><span data-stu-id="88c58-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="88c58-122">Komt overeen met de waarde van doc.properties.name waar doc is voor het item (de geneste eigenschap).</span><span class="sxs-lookup"><span data-stu-id="88c58-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="88c58-123">/ID</span><span class="sxs-lookup"><span data-stu-id="88c58-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="88c58-124">Komt overeen met de waarde van doc.id (sleutel-id en partitie zijn dezelfde eigenschap).</span><span class="sxs-lookup"><span data-stu-id="88c58-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="88c58-125">/ 'afdeling name'</span><span class="sxs-lookup"><span data-stu-id="88c58-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="88c58-126">Komt overeen met de waarde van doc ["Afdelingsnaam '] doc waar het item is.</span><span class="sxs-lookup"><span data-stu-id="88c58-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="88c58-127">De syntaxis voor de partitiesleutel is vergelijkbaar met het opgegeven pad voor indexeren beleid paden met het belangrijkste verschil is dat het pad overeenkomt met de eigenschap in plaats van de waarde, dat wil zeggen er zich geen jokerteken aan het einde.</span><span class="sxs-lookup"><span data-stu-id="88c58-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="88c58-128">Bijvoorbeeld, geeft u afdeling /?</span><span class="sxs-lookup"><span data-stu-id="88c58-128">For example, you would specify /department/?</span></span> <span data-ttu-id="88c58-129">de waarden onder afdeling indexeert, maar u /department opgeven als de definitie van de partitie.</span><span class="sxs-lookup"><span data-stu-id="88c58-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="88c58-130">De partitiesleutel is impliciet geïndexeerd en kan niet worden uitgesloten van het indexeren met indexering beleid onderdrukkingen.</span><span class="sxs-lookup"><span data-stu-id="88c58-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="88c58-131">Bekijk hoe de keuze van de partitiesleutel heeft impact op de prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="88c58-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="88c58-132">Werken met de SDK's van Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="88c58-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="88c58-133">Azure Cosmos DB is ondersteuning toegevoegd voor automatische partitionering met [REST API-versie 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="88c58-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="88c58-134">Om te kunnen gepartitioneerde containers te maken, moet u de SDK-versies 1.6.0 downloaden of hoger in een van de ondersteunde platforms SDK (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="88c58-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="88c58-135">Containers maken</span><span class="sxs-lookup"><span data-stu-id="88c58-135">Creating containers</span></span>
<span data-ttu-id="88c58-136">Het volgende voorbeeld ziet u een .NET-codefragment voor het maken van een container voor het opslaan van apparaat telemetriegegevens van 20.000 aanvraageenheden per seconde van doorvoer.</span><span class="sxs-lookup"><span data-stu-id="88c58-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="88c58-137">De SDK stelt u de waarde OfferThroughput (die op zijn beurt stelt de `x-ms-offer-throughput` aanvraag-header in de REST-API).</span><span class="sxs-lookup"><span data-stu-id="88c58-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="88c58-138">Hier stelt de `/deviceId` als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="88c58-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="88c58-139">De keuze van de partitiesleutel wordt opgeslagen samen met de rest van de container-metagegevens, zoals naam en het indexeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="88c58-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="88c58-140">Voor dit voorbeeld wordt gekozen `deviceId` Aangezien we dat weten (a) omdat er een groot aantal apparaten, schrijfbewerkingen kunnen meerdere partities gelijkmatig worden verdeeld en ons toestemming te schalen van de database voor het opnemen van grote hoeveelheden gegevens en (b) veel van de aanvragen, zoals het ophalen van de meest recente lezen voor een apparaat zijn gericht op één apparaat-id en kunnen worden opgehaald uit een enkele partitie.</span><span class="sxs-lookup"><span data-stu-id="88c58-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="88c58-141">Deze methode maakt een REST-API-aanroep om Cosmos-database en de service wordt een aantal partities op basis van de aangevraagde doorvoer inrichten.</span><span class="sxs-lookup"><span data-stu-id="88c58-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="88c58-142">U kunt de doorvoer van een container te wijzigen wanneer de prestaties van uw behoeften ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="88c58-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="88c58-143">Lezen en schrijven van items</span><span class="sxs-lookup"><span data-stu-id="88c58-143">Reading and writing items</span></span>
<span data-ttu-id="88c58-144">Nu gaan we gegevens invoegen in Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="88c58-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="88c58-145">Hier volgt een voorbeeldklasse met een apparaat lezen en een aanroep naar CreateDocumentAsync invoegen van een nieuw apparaat lezen in een container.</span><span class="sxs-lookup"><span data-stu-id="88c58-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="88c58-146">Dit is een voorbeeld gebruik van de DocumentDB-API:</span><span class="sxs-lookup"><span data-stu-id="88c58-146">This is an example leveraging the DocumentDB API:</span></span>

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

<span data-ttu-id="88c58-147">Laten we het item door de partitiesleutel en -id niet lezen, bijwerken en als laatste stap, verwijdert u deze door partitiesleutel en -id. Opmerking dat gelezen gegevens een PartitionKey-waarde bevatten (die overeenkomt met de `x-ms-documentdb-partitionkey` aanvraag-header in de REST-API).</span><span class="sxs-lookup"><span data-stu-id="88c58-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="88c58-148">Gepartitioneerde containers doorzoeken</span><span class="sxs-lookup"><span data-stu-id="88c58-148">Querying partitioned containers</span></span>
<span data-ttu-id="88c58-149">Als u query's gegevens in gepartitioneerde containers, routeert Cosmos DB automatisch de query naar de partities die overeenkomt met de partitie sleutelwaarden die zijn opgegeven in het filter (wanneer aanwezig).</span><span class="sxs-lookup"><span data-stu-id="88c58-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="88c58-150">Deze query wordt bijvoorbeeld doorgestuurd naar partitie met de partitiesleutel 'XMS-0001'.</span><span class="sxs-lookup"><span data-stu-id="88c58-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="88c58-151">De volgende query heeft geen een filter voor de partitiesleutel (DeviceId) en is fanned uit op alle partities waarop deze wordt uitgevoerd op basis van de index van de partitie.</span><span class="sxs-lookup"><span data-stu-id="88c58-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="88c58-152">Opmerking die u hebt voor het opgeven van de EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in de REST-API) om de SDK voor het uitvoeren van een query meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="88c58-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="88c58-153">Biedt ondersteuning voor cosmos DB [statistische functies](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` en `AVG` over gepartitioneerd containers met behulp van SQL wordt gestart met de SDK's 1.12.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="88c58-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="88c58-154">Query's moeten een enkel samengestelde operator bevatten en moeten één waarde bevatten in de projectie.</span><span class="sxs-lookup"><span data-stu-id="88c58-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="88c58-155">Parallelle queryuitvoering</span><span class="sxs-lookup"><span data-stu-id="88c58-155">Parallel query execution</span></span>
<span data-ttu-id="88c58-156">De Cosmos-DB SDK's 1.9.0 en hoger ondersteuning parallelle uitvoering queryopties, waarmee u kunt uitvoeren lage latentie query's voor gepartitioneerde verzamelingen, zelfs als ze nodig hebben om een groot aantal partities touch.</span><span class="sxs-lookup"><span data-stu-id="88c58-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="88c58-157">De volgende query is bijvoorbeeld geconfigureerd voor meerdere partities parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="88c58-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="88c58-158">U kunt parallelle queryuitvoering beheren door het afstemmen van de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="88c58-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="88c58-159">Door in te stellen `MaxDegreeOfParallelism`, u kunt de mate van parallelle uitvoering, dat wil zeggen, het maximum aantal gelijktijdige netwerkverbindingen op de container partities beheren.</span><span class="sxs-lookup"><span data-stu-id="88c58-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="88c58-160">Als u deze instelt op-1, de mate van parallelle uitvoering wordt beheerd door de SDK.</span><span class="sxs-lookup"><span data-stu-id="88c58-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="88c58-161">Als de `MaxDegreeOfParallelism` is niet opgegeven of is ingesteld op 0, wat de standaardwaarde is, zal er een netwerk met één verbinding met de partities van de container.</span><span class="sxs-lookup"><span data-stu-id="88c58-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="88c58-162">Door in te stellen `MaxBufferedItemCount`, kunt u handelt uit query latentie en client-side geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="88c58-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="88c58-163">Als u deze parameter of stel deze optie in op-1, het aantal items in de buffer opgeslagen tijdens parallelle queryuitvoering wordt beheerd door de SDK.</span><span class="sxs-lookup"><span data-stu-id="88c58-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="88c58-164">Gezien de dezelfde status van de verzameling, retourneert een parallelle query resultaten in dezelfde volgorde als in seriële uitvoering.</span><span class="sxs-lookup"><span data-stu-id="88c58-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="88c58-165">Bij het uitvoeren van een query voor cross-partitie met sorteren (ORDER BY en/of boven) geeft de query parallel meerdere partities uit Azure Cosmos DB SDK en gedeeltelijk gesorteerde resulteert in de clientzijde levert geen resultaten globaal geordende worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="88c58-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="88c58-166">Opgeslagen procedures uitvoeren</span><span class="sxs-lookup"><span data-stu-id="88c58-166">Executing stored procedures</span></span>
<span data-ttu-id="88c58-167">U kunt ook atomische transacties tegen documenten met dezelfde apparaat-ID, zoals uitvoeren als u statistische functies of de meest recente toestand van een apparaat in één item onderhoudt.</span><span class="sxs-lookup"><span data-stu-id="88c58-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="88c58-168">In het volgende gedeelte kijken we hoe u naar een gepartitioneerde containers uit één partitie containers verplaatsen kunt.</span><span class="sxs-lookup"><span data-stu-id="88c58-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88c58-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88c58-169">Next steps</span></span>
<span data-ttu-id="88c58-170">In dit artikel wordt een overzicht van het werken met partitionering van Azure DB die Cosmos-containers met de DocumentDB-API opgegeven.</span><span class="sxs-lookup"><span data-stu-id="88c58-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="88c58-171">Zie ook [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="88c58-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="88c58-172">Schaal en prestaties testen met Azure Cosmos DB uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="88c58-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="88c58-173">Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="88c58-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="88c58-174">Aan de slag programmeren met de [SDK's](documentdb-sdk-dotnet.md) of de [REST-API](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="88c58-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="88c58-175">Meer informatie over [ingerichte doorvoer in Azure Cosmos-DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="88c58-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

