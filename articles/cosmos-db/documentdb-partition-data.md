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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Partitioneren in Azure Cosmos DB met Hallo DocumentDB-API

[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is een globale gedistribueerde en modellen database service ontworpen toohelp u bereiken snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met uw toepassing wanneer het groeit. 

Dit artikel bevat een overzicht van hoe toowork met het partitioneren van de Cosmos-DB containers met DocumentDB API Hallo. Zie [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API. 

tooget gestart met code, Hallo-project downloaden [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:   

* Hoe werkt partitionering in Azure Cosmos DB?
* Hoe configureer partitioneren in Azure Cosmos DB
* Wat partitiesleutels zijn en hoe ik Hallo rechts partitiesleutel kiezen voor de toepassing?

tooget gestart met code, Hallo-project downloaden [Azure Cosmos DB prestaties testen stuurprogramma Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Partitiesleutels

Hallo DocumentDB API Geef Hallo partitie sleuteldefinitie Hallo vorm van een JSON-pad. Hallo ziet volgende tabel u voorbeelden van partitie basisdefinities en Hallo waarden tooeach overeenkomt. Hallo partitiesleutel is opgegeven als een pad, bijvoorbeeld `/department` vertegenwoordigt Hallo eigenschap afdeling. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Partitiesleutel</strong></p></td>
            <td valign="top"><p><strong>Beschrijving</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/Department</p></td>
            <td valign="top"><p>Komt overeen toohello waarde van doc.department waarbij doc Hallo item is.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Eigenschappen/naam</p></td>
            <td valign="top"><p>Komt overeen toohello waarde van doc.properties.name waarbij doc Hallo item (de geneste eigenschap) is.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ID</p></td>
            <td valign="top"><p>Komt overeen met de waarde van doc.id toohello (sleutel-id en partitie zijn Hallo dezelfde eigenschap).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ 'afdeling name'</p></td>
            <td valign="top"><p>Komt overeen toohello waarde van doc ["afdelingsnaam"], waarbij doc Hallo item is.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> Hallo-syntaxis voor de partitiesleutel is vergelijkbaar toohello padspecificatie voor indexering beleid paden met Hallo belangrijke verschil dat pad Hallo overeenkomt met de eigenschap toohello in plaats van Hallo waarde, dus er is geen jokerteken op Hallo end. Bijvoorbeeld, geeft u afdeling /? Hallo tooindex waarden onder afdeling, maar /department opgeven als sleuteldefinitie Hallo-partitie. Hallo partitiesleutel is impliciet geïndexeerd en kan niet worden uitgesloten van het indexeren met indexering beleid onderdrukkingen.
> 
> 

Bekijk hoe Hallo keuze van de partitiesleutel heeft impact op Hallo prestaties van uw toepassing.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Werken met hello Azure Cosmos DB SDK 's
Azure Cosmos DB is ondersteuning toegevoegd voor automatische partitionering met [REST API-versie 2015-12-16](/rest/api/documentdb/). In de volgorde toocreate gepartitioneerd containers, moet u de SDK-versies 1.6.0 downloaden of hoger in een van de Hallo ondersteund platforms SDK (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Containers maken
Hallo volgende voorbeeld ziet u een .NET-codefragment toocreate een container toostore apparaat telemetriegegevens van 20.000 aanvraageenheden per seconde van doorvoer. Hallo SDK stelt Hallo OfferThroughput waarde (die op zijn beurt Hallo ingesteld `x-ms-offer-throughput` aanvraagheader in Hallo REST-API). Hier stelt Hallo `/deviceId` als partitiesleutel Hallo. Hallo keuze van de partitiesleutel wordt opgeslagen samen met de rest van metagegevens zoals naam en het indexeringsbeleid Hallo Hallo.

Voor dit voorbeeld wordt gekozen `deviceId` Aangezien we dat weten (a) omdat er een groot aantal apparaten, schrijfbewerkingen kunnen meerdere partities gelijkmatig worden verdeeld en ons toestemming tooscale Hallo database tooingest enorme hoeveelheden gegevens en (b) veel Hallo aanvragen, zoals ophalen van de meest recente lezen Hallo zijn binnen het bereik tooa één apparaat-id voor een apparaat en kunnen worden opgehaald uit een enkele partitie.

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

Deze methode maakt een REST-API aanroepen tooCosmos DB en Hallo-service wordt een aantal partities op basis van de aangevraagde doorvoer Hallo inrichten. U kunt Hallo doorvoer van een container wijzigen wanneer de prestaties van uw behoeften ontwikkelen. 

### <a name="reading-and-writing-items"></a>Lezen en schrijven van items
Nu gaan we gegevens invoegen in Cosmos-DB. Hier volgt een voorbeeldklasse met een apparaat bij het lezen en een aanroep van tooCreateDocumentAsync tooinsert een nieuw apparaat lezen in een container. Dit is een voorbeeld gebruik Hallo DocumentDB-API:

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

We Hallo item door de partitiesleutel en id lezen, bijwerken en verwijder deze vervolgens als een laatste stap door de partitiesleutel en -id. Opmerking dat Hallo leesbewerkingen een waarde PartitionKey bevatten (overeenkomstige toohello `x-ms-documentdb-partitionkey` aanvraagheader in Hallo REST-API).

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

### <a name="querying-partitioned-containers"></a>Gepartitioneerde containers doorzoeken
Als u automatisch een query met gegevens in gepartitioneerde containers Cosmos DB Hallo routes query toohello partities overeenkomt toohello partitie sleutelwaarden die zijn opgegeven in het Hallo-filter (wanneer aanwezig). Deze query is bijvoorbeeld gerouteerde toojust Hallo partitie met Hallo partitiesleutel 'XMS-0001'.

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hallo volgende query heeft geen een filter op Hallo partitiesleutel (DeviceId) en is fanned van tooall-partities waar deze wordt uitgevoerd tegen index Hallo-partitie. Opmerking u toospecify hello EnableCrossPartitionQuery hebt (`x-ms-documentdb-query-enablecrosspartition` in Hallo REST-API) toohave Hallo SDK tooexecute een query meerdere partities.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Biedt ondersteuning voor cosmos DB [statistische functies](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` en `AVG` over gepartitioneerd containers met behulp van SQL wordt gestart met de SDK's 1.12.0 en hoger. Query's moeten een enkel samengestelde operator bevatten en moeten één waarde bevatten in Hallo projectie.

### <a name="parallel-query-execution"></a>Parallelle queryuitvoering
Hallo Cosmos DB SDK's 1.9.0 en hierboven ondersteuning parallelle uitvoering queryopties, waarmee u kunt de lage latentie tooperform opgevraagd tegen gepartitioneerde verzamelingen, zelfs wanneer ze nodig hebben tootouch een groot aantal partities. Hallo na query is bijvoorbeeld geconfigureerde toorun parallel meerdere partities.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
U kunt parallelle queryuitvoering beheren door afstemmen Hallo volgende parameters:

* Door in te stellen `MaxDegreeOfParallelism`, kunt u bepalen Hallo mate van parallelle uitvoering, dat wil zeggen, Hallo maximum aantal gelijktijdige netwerk verbindingen toohello van container partities. Als u deze te 1 instelt, worden Hallo mate van parallelle uitvoering wordt beheerd door Hallo SDK. Als hello `MaxDegreeOfParallelism` is niet opgegeven of stel too0, de standaardwaarde hello is, zal er een netwerk met één verbinding toohello container partities.
* Door in te stellen `MaxBufferedItemCount`, kunt u handelt uit query latentie en client-side geheugengebruik. Als u deze parameter of stel deze optie te-1, wordt het aantal items in de buffer opgeslagen tijdens parallelle queryuitvoering hello wordt beheerd door Hallo SDK.

Hallo gegeven dezelfde toestand van de verzameling Hallo een parallelle query retourneert resultaten in dezelfde als in seriële uitvoering volgorde Hallo. Bij het uitvoeren van een query voor cross-partitie met sorteren (ORDER BY en/of boven) Hallo hello Azure Cosmos DB SDK problemen query parallel in partities ingedeeld en samenvoegingen gedeeltelijk gesorteerde resulteert in het Hallo client side tooproduce globaal besteld resultaten.

### <a name="executing-stored-procedures"></a>Opgeslagen procedures uitvoeren
U kunt ook uitvoeren atomische transacties tegen documenten met Hallo dezelfde apparaat-ID, bijvoorbeeld als u statistische functies onderhoudt of Hallo meest recente toestand van een apparaat in één item. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
In de volgende sectie hello kijken we hoe u toopartitioned containers uit één partitie containers kunt verplaatsen.

## <a name="next-steps"></a>Volgende stappen
In dit artikel wordt een overzicht van hoe toowork met partitionering van Azure DB die Cosmos-containers met DocumentDB API Hallo opgegeven. Zie ook [partitionerings- en horizontaal schalen](../cosmos-db/partition-data.md) voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API. 

* Schaal en prestaties testen met Azure Cosmos DB uitvoeren. Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.
* Aan de slag met Hallo coderen [SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/)
* Meer informatie over [ingerichte doorvoer in Azure Cosmos-DB](request-units.md)

