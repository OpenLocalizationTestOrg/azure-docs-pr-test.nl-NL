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
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a>Werken met de ondersteuning in Azure Cosmos DB feed wijziging
[Azure Cosmos DB](../cosmos-db/introduction.md) is een snelle en flexibele globaal gerepliceerd database-service die wordt gebruikt voor het opslaan van grote hoeveelheden transactionele en operationele gegevens met voorspelbare één cijfer milliseconde latentie voor leesbewerkingen en schrijft. Hierdoor is het geschikt voor IoT, games, retail, en operationele logboekregistratie toepassingen. Een algemene ontwerppatroon in deze toepassingen is het bijhouden van wijzigingen aangebracht in Azure DB die Cosmos-gegevens en gerealiseerde weergaven bijwerken, realtime analyses uitvoeren, archiveren van gegevens naar koude opslag en trigger-meldingen op bepaalde gebeurtenissen op basis van deze wijzigingen. De **wijziging feed ondersteuning** in Azure Cosmos DB kunt u efficiënter en schaalbare oplossingen bouwen voor elk van deze patronen.

Wijziging van de feed ondersteuning biedt Azure Cosmos DB een gesorteerde lijst van documenten binnen een verzameling Azure Cosmos DB in de volgorde waarin ze zijn gewijzigd. Deze feed kan worden gebruikt om te luisteren om de wijzigingen in gegevens binnen de verzameling en het uitvoeren van acties zoals:

* Een aanroep van een API geactiveerd wanneer een document wordt ingevoegd of gewijzigd
* Verwerking van realtime (stream) uitvoeren op updates
* Synchroniseer gegevens met een cache, de zoekmachine of het datawarehouse

Wijzigingen in Azure Cosmos DB kunnen worden doorgevoerd en worden asynchroon verwerkt en verdeeld over een of meer consumenten voor parallelle verwerking. Bekijk de API's voor de feed wijzigen en hoe u ze kunt gebruiken om schaalbare realtime toepassingen te bouwen. Dit artikel laat zien hoe u werkt met Azure Cosmos DB wijzigen feed en de DocumentDB-API. 

![Power realtime analyses en gebeurtenisafhankelijke scenario's met computers met behulp van Azure DB die Cosmos wijziging feed](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Wijziging feed ondersteuning is alleen beschikbaar voor de DocumentDB-API op dit moment; de Graph API en de API van de tabel zijn momenteel niet ondersteund.

## <a name="use-cases-and-scenarios"></a>Gebruiksvoorbeelden en scenario 's
Feed wijzigen kunt u efficiënte verwerking van grote gegevenssets met een groot aantal schrijfbewerkingen en biedt een alternatief voor het uitvoeren van query's gehele gegevenssets om te zien wat er is gewijzigd. U kunt bijvoorbeeld de volgende taken efficiënt uitvoeren:

* Een cache, search-index of een datawarehouse bijwerken met gegevens die zijn opgeslagen in Azure Cosmos DB.
* Implementeren op toepassingsniveau gegevens lagen en archivering, dat wil zeggen, gegevensopslag ' hot ' in Azure Cosmos DB en na verloop van tijd 'koude gegevens' naar [Azure Blob Storage](../storage/common/storage-introduction.md) of [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Batch analytics implementeren op de gegevens met [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementeer [lambda pijplijnen op Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) met Azure Cosmos DB. Azure Cosmos DB biedt een schaalbare database-oplossing die kan opname en query verwerken en implementeren van lambda-architecturen met lage totale Eigendomskosten. 
* Nul uitvaltijd migraties naar een andere Azure DB die Cosmos-account met een andere partitieschema niet uitvoeren.

**Lambda pijplijnen met Azure Cosmos DB voor opname en -query:**

![Lambda-pijplijn voor opname en query op basis van Azure Cosmos-DB](./media/change-feed/lambda.png)

U kunt Azure Cosmos-database gebruiken voor het ontvangen en opslaan van gebeurtenisgegevens van apparaten, sensoren, infrastructuur en toepassingen en verwerken van deze gebeurtenissen in realtime met [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), of [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Binnen uw [zonder server](http://azure.com/serverless) web- en mobiele apps, kunt u de gebeurtenissen bijhouden zoals wijzigingen in uw klant profiel, voorkeuren of locatie voor het activeren van bepaalde acties zoals pushmeldingen verzenden naar hun apparaten via [ Azure Functions](../azure-functions/functions-bindings-documentdb.md) of [App Services](https://azure.microsoft.com/services/app-service/). Als u gebruikmaakt van Azure DB die Cosmos om een spel samen te stellen, kunt u, bijvoorbeeld gebruik feed voor het implementeren van realtime scoreborden op basis van scores van voltooide games wijzigen.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>De werking van de feed wijzigen in Azure Cosmos DB
Azure Cosmos DB biedt de mogelijkheid updates die zijn aangebracht aan een verzameling Azure Cosmos DB stapsgewijs te lezen. Deze wijziging feed heeft de volgende eigenschappen:

* Wijzigingen zijn in Azure Cosmos DB permanent en asynchroon kunnen worden verwerkt.
* Wijzigingen in de documenten binnen een verzameling zijn beschikbaar in de feed wijziging onmiddellijk.
* Elke wijziging in een document wordt slechts één keer weergegeven in de feed wijziging en clients beheren hun logica plaatsen van controlepunten. De wijziging feed processor-bibliotheek biedt plaatsen van controlepunten en 'ten minste eenmaal' semantiek.
* Alleen de meest recente wijziging voor een bepaald document is opgenomen in het logboekbestand. Tussentijdse wijzigingen zijn mogelijk niet beschikbaar.
* De feed wijzigen is door wijzigingen in elke waarde voor de partitiesleutel gesorteerd. Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.
* Wijzigingen kunnen worden gesynchroniseerd vanuit elk punt in tijd, er is geen vaste Gegevensretentieperiode waarvoor wijzigingen beschikbaar zijn.
* Wijzigingen zijn beschikbaar in segmenten van de partitie sleutelbereiken. Op deze manier kunt wijzigingen in grote verzamelingen parallel worden verwerkt door meerdere gebruikers /-servers.
* Toepassingen kunnen aanvragen voor meerdere wijziging feeds gelijktijdig op dezelfde verzameling.

Azure Cosmos-DB wijzigen feed is standaard ingeschakeld voor alle accounts. U kunt uw [ingerichte doorvoer](request-units.md) in uw regio schrijven of een willekeurige [regio lezen](distribute-data-globally.md) om te lezen van de feed wijziging, net als elke andere bewerking van de Azure Cosmos-database. De feed wijziging omvat INSERT en update-bewerkingen die zijn aangebracht in de documenten binnen de verzameling. U kunt vastleggen verwijderingen door een 'soft-delete' vlag binnen uw documenten in plaats van verwijderingen. U kunt ook een eindige vervalperiode voor uw documenten via instellen de [TTL mogelijkheid](time-to-live.md), bijvoorbeeld 24 uur en gebruik de waarde van die eigenschap voor het vastleggen van verwijderingen. Met deze oplossing hebt u wijzigingen verwerken binnen een kortere periode dan de TTL verloopperiode. De feed wijziging is beschikbaar voor elke partitiesleutelbereik binnen de documentenverzameling en dus kan worden verdeeld over een of meer consumenten voor parallelle verwerking. 

![Feed voor gedistribueerde verwerking van Azure Cosmos DB wijzigen](./media/change-feed/changefeedvisual.png)

U hebt een aantal opties in de manier waarop u een wijziging in de feed in uw clientcode implementeert. De volgende secties onmiddellijk wordt beschreven hoe de wijziging feed met behulp van de REST-API van Azure Cosmos-database en de DocumentDB SDK's implementeren. Echter voor .NET-toepassingen, wordt u aangeraden de nieuwe [wijziging feed processor bibliotheek](#change-feed-processor) feed voor de verwerking van gebeurtenissen van de wijziging naar lezen wijzigingen meerdere partities vereenvoudigt en kunt meerdere threads in werkt Parallel. 

## <a id="rest-apis"></a>Werken met de REST-API en de DocumentDB SDK 's
Azure Cosmos DB biedt elastische containers voor opslag en doorvoer aangeroepen **verzamelingen**. Gegevens in verzamelingen is logisch zijn gegroepeerd met [partitie sleutels](partition-data.md) voor schaalbaarheid en prestaties. Azure Cosmos DB biedt verschillende API's voor toegang tot deze gegevens, met inbegrip van lookup-ID (lezen/Get), query en lees-feeds (scans). De feed wijziging kan worden verkregen met twee nieuwe aanvraagheaders tot de DocumentDB in te vullen `ReadDocumentFeed` API, en over het bereiken van partitiesleutels parallel kunnen worden verwerkt.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
U gaat nu een korte kijken hoe ReadDocumentFeed werkt. Azure Cosmos DB ondersteunt het lezen van een feed van documenten binnen een verzameling via de `ReadDocumentFeed` API. De volgende aanvraag resulteert bijvoorbeeld een pagina van de documenten binnen de `serverlogs` verzameling. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Resultaten kunnen worden beperkt met behulp van de `x-ms-max-item-count` header en gelezen kunnen worden hervat door opnieuw indienen van de aanvraag met een `x-ms-continuation` header in het vorige antwoord geretourneerd. Wanneer dit wordt uitgevoerd op één enkele client `ReadDocumentFeed` doorlopen resultaten meerdere partities opeenvolgend. 

**Seriële lezen feed document**

U kunt ook de feed van documenten met een van de ondersteunde ophalen [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md). Bijvoorbeeld, het volgende fragment toont hoe u de [ReadDocumentFeedAsync methode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Gedistribueerde uitvoering van ReadDocumentFeed
Voor verzamelingen die een groot aantal updates opnemen of terabytes aan gegevens of meer bevatten, seriële uitvoering van lees-feed van een enkelvoudige clientcomputer mogelijk geen praktische. Om deze big data-scenario's te ondersteunen, biedt Azure Cosmos DB API's te distribueren `ReadDocumentFeed` aanroepen transparant tussen meerdere client lezers/gebruikers. 

**Gedistribueerde lezen Document Feed**

Om te bieden schaalbare verwerking van incrementele wijzigingen Azure Cosmos DB ondersteunt een scale-out-model voor de feed API op basis van de bereiken van partitiesleutels wijziging.

* U kunt een lijst van de partitie ophalen sleutelbereiken voor het uitvoeren van een verzameling een `ReadPartitionKeyRanges` aanroepen. 
* U kunt uitvoeren voor elke partitiesleutelbereik een `ReadDocumentFeed` om documenten te lezen met partitiesleutels binnen dat bereik valt.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Bij het ophalen van partitie sleutelbereiken voor een verzameling
U kunt de sleutelbereiken partitie ophalen door het aanvragen van de `pkranges` bron binnen een verzameling. Bijvoorbeeld de volgende aanvraag opgehaald in de lijst met belangrijke bereiken van de partitie voor de `serverlogs` verzameling:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Deze aanvraag retourneert het volgende antwoord met metagegevens over de partitie sleutel bereiken:

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


**Partitie-eigenschappen van de belangrijkste bereik**: elke partitiesleutelbereik bevat de eigenschappen van metagegevens in de volgende tabel:

<table>
    <tr>
        <th>Header-naam</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>De ID voor de partitiesleutelbereik. Dit is een stabiele en de unieke ID binnen elke verzameling.</p>
            <p>Moet worden gebruikt in de aanroep van de volgende wijzigingen lezen door partitiesleutelbereik.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>De maximumgrootte van een partitie sleutelhash-waarde voor de partitiesleutelbereik. Voor intern gebruik.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>De minimale partitie sleutelhash-waarde voor de partitiesleutelbereik. Voor intern gebruik.</td>
    </tr>       
</table>

U kunt dit doen met behulp van een van de ondersteunde [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md). Bijvoorbeeld het volgende fragment toont hoe op te halen van de partitie sleutelbereiken aan .NET met de [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) methode.

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

Azure Cosmos DB ophalen van documenten per partitiesleutelbereik ondersteunt door de optionele `x-ms-documentdb-partitionkeyrangeid` header. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Uitvoeren van een incrementele ReadDocumentFeed
ReadDocumentFeed ondersteunt de volgende scenario's / taken voor incrementele verwerking van wijzigingen in Azure Cosmos DB verzamelingen:

* Alle wijzigingen naar documenten vanaf het begin dat wil zeggen lezen van een verzameling maken.
* Alle wijzigingen die in toekomstige updates voor documenten van huidige tijd of eventuele wijzigingen sinds een opgegeven gebruiker lezen.
* Alle wijzigingen naar documenten lezen van een logische versie van de verzameling (ETag). U kunt uw consumenten op basis van de geretourneerde ETag van incrementele lezen-feed van aanvragen controlepunt.

De wijzigingen die zijn ingevoegd en updates van documenten. Om vast te leggen verwijdert, moet u een eigenschap 'soft delete' gebruiken in uw documenten of gebruik de [ingebouwde TTL eigenschap](time-to-live.md) om aan te geven van een in behandeling zijnde verwijdering van de feed veranderen.

De volgende tabel bevat de [aanvraag](/rest/api/documentdb/common-documentdb-rest-request-headers.md) en [antwoordheaders](/rest/api/documentdb/common-documentdb-rest-response-headers.md) voor ReadDocumentFeed bewerkingen.

**Aanvraagheaders voor incrementele ReadDocumentFeed**:

<table>
    <tr>
        <th>Header-naam</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>EEN IM</td>
        <td>Moet worden ingesteld op 'Incrementele feed', of anders weggelaten</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Er is geen header: retourneert alle wijzigingen vanaf het begin (verzameling maken)</p>
            <p>' * ': retourneert alle nieuwe wijzigingen aan gegevens binnen de verzameling</p>           
            <p>&lt;ETag&gt;: als is ingesteld op een verzameling ETag, retourneert alle wijzigingen die sinds logische tijdstempel</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 tijdnotatie; genegeerd als If-None-Match is opgegeven.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>De belangrijkste bereik partitie-ID voor het lezen van gegevens.</td>
    </tr>
</table>

**Antwoordheaders voor incrementele ReadDocumentFeed**:

<table> <tr>
        <th>Header-naam</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>ETag</td>
        <td>
            <p>De logische LSN (sequence number) van de laatste document in het antwoord geretourneerd.</p>
            <p>Incrementele ReadDocumentFeed kan worden hervat door deze waarde in de If-None-Match opnieuw.</p>
        </td>
    </tr>
</table>

Hier volgt een voorbeeld van een aanvraag om te retourneren van alle incrementele wijzigingen in de verzameling van de logische versie/ETag `28535` en partitioneren van de belangrijkste bereik = `16`:

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

Wijzigingen zijn geordend op tijd binnen elke waarde voor de partitiesleutel binnen de partitiesleutelbereik. Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden. Als er meer resultaten dan in één pagina passen, kunt u de volgende pagina van de resultaten lezen door deze opnieuw indienen van de aanvraag met de `If-None-Match` header met waarde gelijk is aan de `etag` uit het vorige antwoord. Als meerdere documenten zijn ingevoegd of Transactioneel binnen een opgeslagen procedure of trigger bijgewerkt, ze alle geretourneerd binnen dezelfde antwoordpagina.

> [!NOTE]
> Met de feed wijziging, krijgt u mogelijk meer items geretourneerd in een pagina, dan is opgegeven in `x-ms-max-item-count` in het geval van meerdere documenten ingevoegd of geüpdatet binnen een opgeslagen procedures of triggers. 

Wanneer u de .NET SDK (1.17.0), stelt u het veld `StartTime` in `ChangeFeedOptions` rechtstreeks gewijzigde documenten sinds retourneren `StartTime` bij het aanroepen van `CreateDocumentChangeFeedQuery`. Door op te geven `If-Modified-Since` met de REST API, uw aanvraag wordt geretourneerd niet de documenten zelf, maar in plaats daarvan het vervolgtoken of `etag` in de antwoordheader. Om te retourneren van de documenten gewijzigd in de opgegeven tijd, het vervolgtoken `etag` moet vervolgens worden gebruikt in de volgende aanvraag met `If-None-Match` te retourneren van de werkelijke documenten. 

De .NET SDK biedt de [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) en [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helperklassen voor toegang tot de wijzigingen die zijn aangebracht aan een verzameling. Het volgende fragment toont hoe op te halen van alle wijzigingen vanaf het begin met de .NET SDK uit één client.

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
En het volgende fragment toont het verwerken van wijzigingen in realtime met Azure Cosmos DB met behulp van de wijziging-feed ondersteuning en de voorgaande functie. De eerste aanroep retourneert alle documenten in de verzameling en de tweede retourneert alleen de twee documenten die zijn gemaakt sinds het laatste controlepunt zijn gemaakt.

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

U kunt ook filteren op de wijziging feed met behulp van de logica voor de client selectief om gebeurtenissen te verwerken. Dit is bijvoorbeeld een codefragment die clientzijde LINQ gebruikt voor het verwerken van gebeurtenissen voor wijzigingen in alleen temperatuur van apparaat sensoren.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Bibliotheek van de Feed Processor wijzigingsbeheer
Een andere optie is met de [Azure Cosmos DB wijzigen Feed Processor bibliotheek](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), kunt u eenvoudig distribueren voor gebeurtenisverwerking van een wijziging in de feed in meerdere gebruikers. De bibliotheek is ideaal voor het bouwen van wijziging feed lezers van het .NET-platform. Sommige werkstromen die zouden worden vereenvoudigd door middel van de wijziging Feed Processor-bibliotheek via de methoden die zijn opgenomen in de andere Cosmos DB-SDK's zijn onder andere: 

* Opvragen van de updates van wijziging feed wanneer gegevens worden opgeslagen op verschillende partities
* Verplaatsen of het repliceren van gegevens uit een verzameling naar een andere
* Parallelle uitvoering van de acties die worden geactiveerd door software-updates tot gegevens en feed wijzigen 

Terwijl met de API's in de Cosmos-SDK's nauwkeurig toegang tot de feed-updates in elke partitie bevat, vereenvoudigt met behulp van de Feed Processor wijzigen bibliotheek lezen wijzigingen in partities en meerdere threads die parallel werken. In plaats van handmatig lezen wijzigingen van elke container en een vervolgtoken voor elke partitie opslaan, beheert de wijziging Feed Processor lezen wijzigingen automatisch meerdere partities met een lease-mechanisme.

De bibliotheek is beschikbaar als een NuGet-pakket: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) en van broncode als een Github [voorbeeld](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Understanding wijziging Feed Processor-bibliotheek 

Vier belangrijke onderdelen van de implementatie van de Feed Processor van wijziging: de bewaakte verzameling, de verzameling van de lease, de processor-host en de consumenten. 

**Bewaakte verzameling:** de bewaakte verzameling is de gegevens op basis waarvan de feed wijziging is gegenereerd. Eventuele toevoegingen en wijzigingen in de bewaakte verzameling worden doorgevoerd in de feed wijziging van de verzameling. 

**Verzameling van de lease:** de lease verzameling coördinaten verwerking van de feed in meerdere werknemers wijziging. Een verzameling afzonderlijke wordt gebruikt voor het opslaan van de leases met een lease per partitie. Het is nuttig voor het opslaan van deze verzameling lease op een ander account met de regio schrijven dichter aan waarop de wijziging Feed Processor wordt uitgevoerd. Een lease-object bevat de volgende kenmerken: 
* Eigenaar: Hiermee geeft u op de host die eigenaar is van de lease
* Voortzetting: Geeft de positie (vervolgtoken) in de feed voor een bepaalde partitie wijziging
* Tijdstempel: Tijd van laatste lease is bijgewerkt. de tijdstempel kan worden gebruikt om te controleren of de lease is verlopen 

**Processor Host:** elke host bepaalt hoeveel partities verwerken op basis van hoeveel andere exemplaren van hosts actieve leases hebben. 
1.  Wanneer u een host start, verkrijgt deze leases om de werkbelasting kan worden verdeeld over alle hosts. Een host vernieuwt periodiek leases, dus leases actief blijven. 
2.  Een host controlepunten lezen voor de laatste vervolgtoken aan de lease voor elk. Een host controleert gelijktijdigheid om veiligheid te garanderen, de ETag voor elke update lease. Andere strategieën controlepunt worden ook ondersteund.  
3.  Bij het afsluiten, is een host alle leases worden vrijgegeven, maar blijft de informatie over de voortzetting dus bij het lezen van het controlepunt van de opgeslagen later kan worden hervat. 

Het aantal hosts mag niet groter zijn dan het aantal partities (leases) op dit moment.

**Consumenten:** consumenten of werknemers, zijn de threads die de verwerking van de wijziging feed gestart door elke host uitvoeren. Elke host processor kan meerdere gebruikers hebben. Elke consumer leest de wijziging feed uit de partitie die is toegewezen aan en ontvangt een melding van de host van wijzigingen en verlopen van leases.

Om verder te begrijpen hoe deze vier elementen van wijziging Feed Processor samenwerken, bekijk een voorbeeld in het volgende diagram. De bewaakte verzameling documenten worden opgeslagen en gebruikt de 'plaats' als de partitiesleutel. We zien dat de blauwe partitie enzovoort documenten met het veld 'plaats' uit "A-E" bevat. Er zijn twee hosts, elk met twee consumenten lezen van de vier partities parallel. De pijlen geven het lezen van een specifieke positie in de feed wijziging consumenten. In de eerste partitie vertegenwoordigt de donkere blauw ongelezen wijzigingen terwijl de lichte blauw de al gelezen wijzigingen in de feed wijzigen vertegenwoordigt. De hosts de lease-verzameling gebruiken voor het opslaan van een waarde 'voortzetting' om de huidige positie lezen voor elke consumer bij te houden. 

![Met behulp van de wijziging Azure Cosmos DB feed processor host](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Met behulp van de wijziging Feed Processor-bibliotheek 
De volgende sectie wordt uitgelegd hoe u van de bibliotheek wijzigen Feed Processor in de context van het repliceren van wijzigingen uit een bronverzameling naar een doelverzameling. De bronverzameling is hier de bewaakte verzameling in de Feed wijziging-Processor. 

**Installeren en de wijziging Feed Processor NuGet-pakket opnemen** 

Voordat u wijziging Feed Processor NuGet-pakket installeert, eerst installeren: 
* Microsoft.Azure.DocumentDB, versie 1.13.1 of hoger 
* Newtonsoft.Json, versie 9.0.1 of hoger installeren `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` en deze opnemen als een verwijzing.

**Een gecontroleerde, lease- en verzameling maken** 

Om de wijziging Feed Processor bibliotheek gebruiken, moet de verzameling van de lease worden gemaakt voordat de processor host (s) wordt uitgevoerd. Opnieuw, is het raadzaam een lease-verzameling opslaan op een ander account met een regio schrijven dichter aan waarop de wijziging Feed Processor wordt uitgevoerd. In dit voorbeeld verplaatsing van gegevens moet maken van de doelverzameling zouden worden voordat de wijziging Feed Processor host wordt uitgevoerd. In de voorbeeldcode noemen we een Help-methode voor het maken van de bewaakte geleasete, en de bestemming verzamelingen als deze niet al bestaan. 

> [!WARNING]
> Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor de toepassing om te communiceren met Azure Cosmos DB. Voor meer informatie raadpleegt u de [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Maken van een host processor*

De `ChangeFeedProcessorHost` klasse biedt een thread-veilige, met meerdere processen en veilige runtime-omgeving voor gebeurtenisprocessors die ook het plaatsen van controlepunten en partitie lease biedt. Gebruik de `ChangeFeedProcessorHost` klasse, die u kunt implementeren `IChangeFeedObserver`. Deze interface bevat drie methoden:

* `OpenAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijzigen wordt geopend. Het kan worden aangepast voor een specifieke actie uitgevoerd wanneer consumenten/zien wordt geopend.  
* `CloseAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijziging wordt beëindigd. Het kan worden aangepast voor een specifieke actie uitgevoerd wanneer de consument/zien wordt gesloten.  
* `ProcessChangesAsync`: Deze functie wordt aangeroepen wanneer nieuwe wijzigingen in het document beschikbaar op de feed wijzigen zijn. Het kan worden aangepast voor een specifieke actie na elke wijziging feed update uitgevoerd.  

In ons voorbeeld wordt de interface implementeren `IChangeFeedObserver` via de `DocumentFeedObserver` klasse. Hier de `ProcessChangesAsync` upserts (updates) een document van de wijziging in de doelverzameling feed werken. In dit voorbeeld is nuttig voor het verplaatsen van gegevens uit een verzameling naar een andere om te wijzigen van de partitiesleutel van een gegevensset. 

*De Processor-Host wordt uitgevoerd*

Beide opties voor feed wijzigen voordat u begint met de verwerking van gebeurtenissen, en opties van de feed host wijzigen kunnen worden aangepast. 
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
De specifieke velden die kunnen worden aangepast worden samengevat in de volgende tabellen. 

**Opties voor Feed wijzigen**:
<table>
    <tr>
        <th>De naam van eigenschap</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Opgehaald of ingesteld van het maximum aantal items in de opsomming wordt in de database-service van Azure DB die Cosmos wordt geretourneerd.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Opgehaald of ingesteld van de partitie-id sleutel bereik voor de huidige aanvraag in de database-service van Azure Cosmos DB.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Opgehaald of ingesteld van de aanvraag vervolgtoken in de database-service van Azure Cosmos DB.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Opgehaald of ingesteld van het sessietoken voor gebruik met sessieconsistentie in de database-service van Azure Cosmos DB.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Opgehaald of ingesteld of wijziging in de database-service van Azure DB die Cosmos-kanaal moet worden gestart vanaf het begin (true) of van de huidige (false). Standaard wordt gestart vanuit de huidige (false).</td>
    </tr>
</table>

**Opties voor de Feed Host wijzigen**:
<table>
    <tr>
        <th>De naam van eigenschap</th>
        <th>Type</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>Het interval voor alle leases voor partities die momenteel worden vastgehouden door het ChangeFeedEventHost-exemplaar.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Het interval voor ere van een taak of partities gelijkmatig zijn verdeeld over exemplaren van de bekende host berekenen.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Het interval waarvoor de lease op een lease voor een partitie wordt gehouden. Als de lease is niet vernieuwd binnen dit interval, het is verlopen en eigendom van de partitie worden verplaatst naar een ander exemplaar van ChangeFeedEventHost.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>De vertraging tussen een partitie polling voor nieuwe wijzigingen op de feed, nadat alle huidige wijzigingen zijn geleegd.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>De frequentie controlepunt leases.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Het aantal minimale partitie voor de host.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>Het maximale aantal partities die de host kan fungeren.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>BOOL</td>
        <td>Hiermee wordt aangegeven of bij het starten van de host alle bestaande leases moeten worden verwijderd en de host moet worden gestart vanaf het begin.</td>
    </tr>
</table>


Voor het starten van de verwerking van gebeurtenissen instantiëren `ChangeFeedProcessorHost`, bied de juiste parameters voor uw Azure DB die Cosmos-verzameling. Roep vervolgens `RegisterObserverAsync` registreren uw `IChangeFeedObserver` (DocumentFeedObserver in dit voorbeeld)-implementatie met de runtime. Op dit moment probeert de host een lease op elke partitiesleutelbereik in de Azure DB die Cosmos-verzameling met behulp van een greedy-algoritme te verkrijgen. Deze leases gedurende een bepaald tijdsbestek geldig en moeten daarna worden vernieuwd. Zodra nieuwe knooppunten worker-exemplaren in dit geval online komen, ze reserveringen voor leases en gedurende een bepaalde periode de belasting verschuift tussen knooppunten elke host probeert te verkrijgen van meer leases. 

In de voorbeeldcode gebruiken we een factory klasse (DocumentFeedObserverFactory.cs) voor het maken van een zien en de `RegistObserverFactoryAsync` registreren van de zien. 

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
In de loop van de tijd komt er een evenwicht tot stand. Deze dynamische mogelijkheid kan automatisch schalen om te worden toegepast op gebruikers voor schaal omhoog en omlaag schalen op basis van CPU. Als er wijzigingen zijn beschikbaar in Azure Cosmos DB sneller dan consumers kunnen verwerken, kan de toename van de CPU op consumenten ervoor zorgen dat een automatisch geschaald op het aantal worker-instantie worden gebruikt.

## <a name="next-steps"></a>Volgende stappen
* Probeer de [Azure Cosmos DB Wijzig feed codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Aan de slag programmeren met de [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md) of de [REST-API](/rest/api/documentdb/).
