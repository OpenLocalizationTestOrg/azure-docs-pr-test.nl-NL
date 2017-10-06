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
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Werken met Hallo wijziging feed ondersteuning in Azure Cosmos-DB
[Azure Cosmos DB](../cosmos-db/introduction.md) is een snelle en flexibele globaal gerepliceerd database-service die wordt gebruikt voor het opslaan van grote hoeveelheden transactionele en operationele gegevens met voorspelbare één cijfer milliseconde latentie voor leesbewerkingen en schrijft. Hierdoor is het geschikt voor IoT, games, retail, en operationele logboekregistratie toepassingen. Een algemene ontwerppatroon in deze toepassingen is tootrack wijzigingen aangebracht tooAzure Cosmos DB gegevens, en gerealiseerde weergaven bijwerken, voert u realtime-analyses, archiveren toocold gegevensopslag en trigger-meldingen op bepaalde gebeurtenissen op basis van deze wijzigingen. Hallo **wijziging feed ondersteuning** in Azure Cosmos DB kunt u toobuild efficiënte en schaalbare oplossingen voor elk van deze patronen.

Wijziging van de feed ondersteuning biedt Azure Cosmos DB een gesorteerde lijst van documenten binnen een verzameling Azure Cosmos DB in Hallo volgorde waarin ze zijn gewijzigd. Dit kanaal kan worden gebruikt toolisten voor wijzigingen toodata binnen Hallo verzameling en uitvoeren van acties zoals:

* Een aanroep tooan API geactiveerd wanneer een document wordt ingevoegd of gewijzigd
* Verwerking van realtime (stream) uitvoeren op updates
* Synchroniseer gegevens met een cache, de zoekmachine of het datawarehouse

Wijzigingen in Azure Cosmos DB kunnen worden doorgevoerd en worden asynchroon verwerkt en verdeeld over een of meer consumenten voor parallelle verwerking. Bekijk Hallo API's voor de feed wijzigen en hoe u ze kunt gebruiken toobuild schaalbare realtime-toepassingen. Dit artikel laat zien hoe toowork met Azure Cosmos DB feed en Hallo DocumentDB API wijzigen. 

![Met behulp van Azure DB die Cosmos wijziging feed toopower realtime analyses en gebeurtenisafhankelijke scenario's met computers](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Wijziging feed ondersteuning is alleen beschikbaar voor Hallo DocumentDB API op dit moment; Hallo Graph API en de tabel-API worden momenteel niet ondersteund.

## <a name="use-cases-and-scenarios"></a>Gebruiksvoorbeelden en scenario 's
Feed wijzigen kunt u efficiënte verwerking van grote gegevenssets met een groot aantal schrijfbewerkingen en biedt een alternatieve tooquerying gehele gegevenssets tooidentify wat is er gewijzigd. U kunt bijvoorbeeld Hallo taken efficiënt volgende uitvoeren:

* Een cache, search-index of een datawarehouse bijwerken met gegevens die zijn opgeslagen in Azure Cosmos DB.
* Implementeren op toepassingsniveau gegevens lagen en archivering, dat wil zeggen, gegevensopslag ' hot ' in Azure Cosmos DB en leeftijd te 'koude gegevens'[Azure Blob Storage](../storage/common/storage-introduction.md) of [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Batch analytics implementeren op de gegevens met [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementeer [lambda pijplijnen op Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) met Azure Cosmos DB. Azure Cosmos DB biedt een schaalbare database-oplossing die kan opname en query verwerken en implementeren van lambda-architecturen met lage totale Eigendomskosten. 
* Nul uitvaltijd migraties tooanother Azure DB die Cosmos-account met een andere partitieschema niet uitvoeren.

**Lambda pijplijnen met Azure Cosmos DB voor opname en -query:**

![Lambda-pijplijn voor opname en query op basis van Azure Cosmos-DB](./media/change-feed/lambda.png)

Gebruik Azure Cosmos DB tooreceive en gebeurtenisgegevens van apparaten, sensoren, infrastructuur en toepassingen opslaan en verwerken van deze gebeurtenissen in realtime met [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), of [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Binnen uw [zonder server](http://azure.com/serverless) web- en mobiele apps, u kunt de gebeurtenissen bijhouden zoals wijzigingen tooyour klant profiel, voorkeuren of locatie tootrigger bepaalde acties zoals het verzenden van pushmeldingen meldingen tootheir apparaten met behulp van [Azure Functions](../azure-functions/functions-bindings-documentdb.md) of [App Services](https://azure.microsoft.com/services/app-service/). Als u Azure Cosmos DB toobuild een spel, kunt u bijvoorbeeld wijziging feed tooimplement realtime scoreborden op basis van scores van voltooide games gebruiken.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>De werking van de feed wijzigen in Azure Cosmos DB
Azure Cosmos DB biedt Hallo mogelijkheid tooincrementally lezen wijzigingen tooan Azure DB die Cosmos-verzameling. Deze wijziging feed heeft Hallo volgende eigenschappen:

* Wijzigingen zijn in Azure Cosmos DB permanent en asynchroon kunnen worden verwerkt.
* Toodocuments binnen een verzameling wijzigingen zijn onmiddellijk in Hallo wijziging feed beschikbaar.
* Elke wijziging tooa document wordt slechts één keer weergegeven in Hallo wijziging feed en clients beheren hun logica plaatsen van controlepunten. Hallo wijziging feed processor-bibliotheek biedt plaatsen van controlepunten en 'ten minste eenmaal' semantiek.
* Alleen Hallo recentste wijziging voor een bepaald document is opgenomen in het wijzigingenlogboek Hallo. Tussentijdse wijzigingen zijn mogelijk niet beschikbaar.
* Hallo wijziging feed is door wijzigingen in elke waarde voor de partitiesleutel gesorteerd. Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden.
* Wijzigingen kunnen worden gesynchroniseerd vanuit elk punt in tijd, er is geen vaste Gegevensretentieperiode waarvoor wijzigingen beschikbaar zijn.
* Wijzigingen zijn beschikbaar in segmenten van de partitie sleutelbereiken. Op deze manier kunt wijzigingen in grote verzamelingen toobe parallel worden verwerkt door meerdere gebruikers /-servers.
* Toepassingen kunnen aanvragen voor meerdere wijziging-feeds gelijktijdig op Hallo dezelfde verzameling.

Azure Cosmos-DB wijzigen feed is standaard ingeschakeld voor alle accounts. Kunt u uw [ingerichte doorvoer](request-units.md) in uw regio schrijven of een willekeurige [lezen regio](distribute-data-globally.md) tooread van Hallo feed, net als elke andere bewerking vanuit Azure Cosmos DB wijzigen. Hallo wijziging feed bevat INSERT en updatebewerkingen toodocuments binnen Hallo verzameling gemaakt. U kunt vastleggen verwijderingen door een 'soft-delete' vlag binnen uw documenten in plaats van verwijderingen. U kunt ook een eindige vervalperiode voor uw documenten via Hallo instellen [TTL mogelijkheid](time-to-live.md)voor bijvoorbeeld 24 uur en gebruik Hallo waarde van die eigenschap toocapture worden verwijderd. Met deze oplossing hebt u tooprocess wijzigingen binnen een kortere periode dan Hallo TTL verloopperiode. Hallo wijziging feed is beschikbaar voor elke partitiesleutelbereik binnen Hallo documentverzameling en dus kan worden verdeeld over een of meer consumenten voor parallelle verwerking. 

![Feed voor gedistribueerde verwerking van Azure Cosmos DB wijzigen](./media/change-feed/changefeedvisual.png)

U hebt een aantal opties in de manier waarop u een wijziging in de feed in uw clientcode implementeert. Hallo secties die onmiddellijk volgen beschrijven hoe tooimplement Hallo wijziging feed met hello Azure Cosmos DB REST-API en Hallo DocumentDB SDK's. Echter, voor .NET-toepassingen, wordt u aangeraden Hallo nieuwe [wijziging feed processor bibliotheek](#change-feed-processor) voor verwerking van gebeurtenissen van Hallo wijzigen van de feed lezen wijzigingen vereenvoudigt meerdere partities en kunt meerdere threads in werkt Parallel. 

## <a id="rest-apis"></a>Werken met Hallo REST-API en DocumentDB SDK 's
Azure Cosmos DB biedt elastische containers voor opslag en doorvoer aangeroepen **verzamelingen**. Gegevens in verzamelingen is logisch zijn gegroepeerd met [partitie sleutels](partition-data.md) voor schaalbaarheid en prestaties. Azure Cosmos DB biedt verschillende API's voor toegang tot deze gegevens, met inbegrip van lookup-ID (lezen/Get), query en lees-feeds (scans). Hallo wijziging feed kan worden verkregen met twee nieuwe aanvraag-headers toohello DocumentDB in te vullen `ReadDocumentFeed` API, en over het bereiken van partitiesleutels parallel kunnen worden verwerkt.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
U gaat nu een korte kijken hoe ReadDocumentFeed werkt. Azure Cosmos DB ondersteunt het lezen van een feed van documenten binnen een verzameling via Hallo `ReadDocumentFeed` API. Hallo volgende aanvraag resulteert bijvoorbeeld een pagina van de documenten binnen Hallo `serverlogs` verzameling. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Resultaten kunnen worden beperkt met behulp van Hallo `x-ms-max-item-count` header en gelezen kunnen worden hervat door opnieuw indienen Hallo-aanvraag met een `x-ms-continuation` header in Hallo vorige antwoord geretourneerd. Wanneer dit wordt uitgevoerd op één enkele client `ReadDocumentFeed` doorlopen resultaten meerdere partities opeenvolgend. 

**Seriële lezen feed document**

U kunt ook ophalen Hallo-feed van documenten met behulp van een ondersteund Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md). Bijvoorbeeld, Hallo volgende codefragment bevat hoe toouse hello [ReadDocumentFeedAsync methode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Gedistribueerde uitvoering van ReadDocumentFeed
Voor verzamelingen die een groot aantal updates opnemen of terabytes aan gegevens of meer bevatten, seriële uitvoering van lees-feed van een enkelvoudige clientcomputer mogelijk geen praktische. In de volgorde toosupport biedt deze big data-scenario's, Azure Cosmos DB API's toodistribute `ReadDocumentFeed` aanroepen transparant tussen meerdere client lezers/gebruikers. 

**Gedistribueerde lezen Document Feed**

tooprovide schaalbare verwerking van incrementele wijzigingen, Azure Cosmos DB ondersteunt een scale-out-model voor Hallo wijzigen op basis van de bereiken van partitiesleutels API feed.

* U kunt een lijst van de partitie ophalen sleutelbereiken voor het uitvoeren van een verzameling een `ReadPartitionKeyRanges` aanroepen. 
* U kunt uitvoeren voor elke partitiesleutelbereik een `ReadDocumentFeed` tooread documenten met partitiesleutels binnen dat bereik valt.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Bij het ophalen van partitie sleutelbereiken voor een verzameling
U kunt aanvragende Hallo Hallo partitie sleutelbereiken ophalen `pkranges` bron binnen een verzameling. Bijvoorbeeld hello volgende aanvraag opgehaald Hallo lijst met partitie-sleutelbereiken voor Hallo `serverlogs` verzameling:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Deze aanvraag retourneert Hallo antwoord met metagegevens over Hallo partitie sleutelbereiken te volgen:

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


**Partitie-eigenschappen van de belangrijkste bereik**: elke partitiesleutelbereik Hallo metagegevenseigenschappen in de volgende tabel Hallo omvat:

<table>
    <tr>
        <th>Header-naam</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Hallo-ID voor Hallo partitiesleutelbereik. Dit is een stabiele en de unieke ID binnen elke verzameling.</p>
            <p>Moet worden gebruikt in de volgende aanroep tooread wijzigingen Hallo door partitiesleutelbereik.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Hallo maximale partitie sleutel hash-waarde voor Hallo partitiesleutelbereik. Voor intern gebruik.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Hallo partitie moet minimaal de waarde van het sleutelhash voor Hallo partitiesleutelbereik. Voor intern gebruik.</td>
    </tr>       
</table>

U kunt dit doen met behulp van een ondersteund Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md). Bijvoorbeeld: hello volgende fragment toont hoe de partitiesleutel tooretrieve bereiken in .NET Hallo met [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) methode.

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

Azure Cosmos DB ondersteunt voor het ophalen van documenten per partitiesleutelbereik door Hallo instelling optioneel `x-ms-documentdb-partitionkeyrangeid` header. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Uitvoeren van een incrementele ReadDocumentFeed
ReadDocumentFeed ondersteunt Hallo volgen scenario's / taken voor incrementele verwerking van wijzigingen in Azure Cosmos DB verzamelingen:

* Lees alle wijzigingen toodocuments vanaf het begin van de hello, dat wil zeggen, van een verzameling maken.
* Lees alle verandert toofuture updates toodocuments van huidige tijd en eventuele wijzigingen sinds een opgegeven gebruiker.
* Alle wijzigingen toodocuments lezen van een logische versie van het Hallo-verzameling (ETag). U kunt uw consumenten op basis van Hallo ETag geretourneerd van incrementele lezen-feed aanvragen controlepunt.

Hallo wijzigingen omvatten toodocuments inserts en updates. toocapture worden verwijderd, u moet een eigenschap 'soft delete' gebruiken in uw documenten of Hallo [ingebouwde TTL eigenschap](time-to-live.md) toosignal een in behandeling zijnde verwijdering in Hallo feed wijzigen.

na de tabel lijsten Hallo Hallo [aanvraag](/rest/api/documentdb/common-documentdb-rest-request-headers.md) en [antwoordheaders](/rest/api/documentdb/common-documentdb-rest-response-headers.md) voor ReadDocumentFeed bewerkingen.

**Aanvraagheaders voor incrementele ReadDocumentFeed**:

<table>
    <tr>
        <th>Header-naam</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>EEN IM</td>
        <td>Moet worden ingesteld te 'Incrementele feed', of anders weggelaten</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Er is geen header: retourneert alle wijzigingen van Hallo vanaf (verzameling maken)</p>
            <p>' * ': alle nieuwe wijzigingen toodata binnen Hallo verzameling geretourneerd</p>         
            <p>&lt;ETag&gt;: als tooa verzameling ETag instellen, retourneert alle wijzigingen die sinds logische tijdstempel</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 tijdnotatie; genegeerd als If-None-Match is opgegeven.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Hallo partitie sleutel bereik-ID voor het lezen van gegevens.</td>
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
            <p>Hallo logische LSN (sequence number) van de laatste document geretourneerd als antwoord Hallo.</p>
            <p>Incrementele ReadDocumentFeed kan worden hervat door deze waarde in de If-None-Match opnieuw.</p>
        </td>
    </tr>
</table>

Hier volgt een voorbeeld aanvraag tooreturn alle incrementele wijzigingen in de verzameling van Hallo logische versie/ETag `28535` en partitioneren van de belangrijkste bereik = `16`:

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

Wijzigingen zijn geordend op tijd binnen elke waarde voor de partitiesleutel binnen Hallo partitiesleutelbereik. Er is geen gegarandeerde volgorde voor partitie-sleutelwaarden. Als er meer resultaten dan in één pagina passen, u de volgende pagina Hallo van resultaten kunt lezen door Hallo aanvraag Hello wordt opnieuw `If-None-Match` header met waarde gelijk toohello `etag` uit het vorige antwoord Hallo. Als meerdere documenten zijn ingevoegd of Transactioneel binnen een opgeslagen procedure of trigger bijgewerkt, ze alle geretourneerd binnen Hallo dezelfde antwoordpagina.

> [!NOTE]
> Met de feed wijziging, krijgt u mogelijk meer items geretourneerd in een pagina, dan is opgegeven in `x-ms-max-item-count` in geval van meerdere documenten ingevoegd of geüpdatet binnen een opgeslagen procedures Hallo of triggers. 

Wanneer u Hallo .NET SDK (1.17.0), stelt u Hallo veld `StartTime` in `ChangeFeedOptions` documenten toodirectly return gewijzigd sinds `StartTime` bij het aanroepen van `CreateDocumentChangeFeedQuery`. Door op te geven `If-Modified-Since` Hallo REST-API gebruikt, uw aanvraag wordt geretourneerd niet Hallo documenten zelf, maar in plaats daarvan Hallo vervolgtoken of `etag` in Hallo-antwoordheader. tooreturn hello documenten gewijzigde Hallo tijd, Hallo vervolgtoken opgegeven `etag` moet vervolgens worden gebruikt in de volgende aanvraag Hallo met `If-None-Match` tooreturn Hallo werkelijke documenten. 

Hallo .NET SDK biedt Hallo [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) en [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper tooaccess wijzigingen in de verzameling tooa klassen. Hallo volgende fragment toont hoe alle tooretrieve verandert vanaf Hallo met .NET SDK Hallo van één client.

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
En hello volgende fragment toont hoe tooprocess verandert in realtime met Azure Cosmos DB met behulp van Hallo wijziging feed ondersteuning en Hallo voorafgaand aan de functie. de eerste aanroep Hallo retourneert alle Hallo documenten in Hallo verzameling en Hallo tweede alleen retourneert Hallo twee documenten die zijn gemaakt en die zijn gemaakt sinds het laatste controlepunt Hallo.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

U kunt ook Hallo wijziging feed met behulp van de client side logica tooselectively procesgebeurtenissen filteren. Dit is bijvoorbeeld een codefragment die gebruikmaakt van de client side LINQ tooprocess alleen temperatuur gebeurtenissen van apparaat sensoren wijzigen.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Bibliotheek van de Feed Processor wijzigingsbeheer
Een andere optie is toouse hello [Azure Cosmos DB wijzigen Feed Processor bibliotheek](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), kunt u eenvoudig distribueren voor gebeurtenisverwerking van een wijziging in de feed in meerdere gebruikers. Hallo-bibliotheek is ideaal voor het bouwen van wijziging lezers feed op Hallo .NET-platform. Sommige werkstromen die zouden worden vereenvoudigd door middel van Hallo wijziging Feed Processor bibliotheek via Hallo-methoden die zijn opgenomen in Hallo andere Cosmos DB SDK's zijn onder andere: 

* Opvragen van de updates van wijziging feed wanneer gegevens worden opgeslagen op verschillende partities
* Verplaatsen of gegevens van één verzameling tooanother repliceren
* Parallelle uitvoering van de acties die worden geactiveerd door updates toodata en wijzig feed 

Terwijl met behulp van Hallo API's in Hallo Cosmos-SDK's nauwkeurige toegang toochange kanaal updates in elke partitie bevat, vereenvoudigt met behulp van Hallo wijziging Feed Processor bibliotheek lezen wijzigingen in partities en meerdere threads die parallel werken. In plaats van handmatig lezen wijzigingen van elke container en een vervolgtoken voor elke partitie opslaan, beheert Hallo wijziging Feed Processor lezen wijzigingen automatisch meerdere partities met een lease-mechanisme.

Hallo-bibliotheek is beschikbaar als een NuGet-pakket: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) en van broncode als een Github [voorbeeld](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Understanding wijziging Feed Processor-bibliotheek 

Er zijn vier onderdelen van de implementatie van Hallo wijziging Feed Processor: Hallo bewaakt verzameling, Hallo lease verzameling Hallo processor host en Hallo consumenten. 

**Bewaakte verzameling:** Hallo bewaakt verzameling is Hallo gegevens op basis van welke Hallo wijziging feed wordt gegenereerd. Een verzameling van de toohello bewaakt toevoegingen en wijzigingen worden doorgevoerd in Hallo wijziging feed van Hallo-verzameling. 

**Verzameling van de lease:** Hallo lease verzameling coördinaten Hallo wijziging feed over meerdere werknemers verwerken. Een afzonderlijke verzameling is gebruikte toostore Hallo leases met een lease per partitie. Het is nuttig toostore deze verzameling lease op een ander account Hello schrijven regio dichter toowhere Hallo wijziging Feed Processor wordt uitgevoerd. Een lease-object bevat Hallo volgende kenmerken: 
* Eigenaar: Hiermee geeft u het Hallo-host die eigenaar is van de lease Hallo
* Voortzetting: Hiermee geeft u Hallo positie (vervolgtoken) in Hallo wijziging feed voor een bepaalde partitie
* Tijdstempel: Tijd van laatste lease is bijgewerkt. Hallo tijdstempel gebruikte toocheck kan zijn of Hallo lease is verlopen 

**Processor Host:** elke host bepaalt hoeveel partities tooprocess op basis van hoeveel andere exemplaren van hosts actieve leases hebben. 
1.  Wanneer u een host start, verkrijgt deze leases toobalance Hallo werkbelasting op alle hosts. Een host vernieuwt periodiek leases, dus leases actief blijven. 
2.  Een host controlepunten Hallo laatste voortzetting token tooits lease voor elk lezen. tooensure gelijktijdigheid veiligheid, een host controleert Hallo ETag voor elke update lease. Andere strategieën controlepunt worden ook ondersteund.  
3.  Bij het afsluiten, een host releases alle leases maar houdt Hallo voortzetting informatie, zodat het lezen van de opgeslagen controlepunt hello later kan worden hervat. 

Het aantal hosts Hallo mag niet groter dan het aantal partities (leases) Hallo op dit moment.

**Consumenten:** consumenten of werknemers, threads die Hallo wijziging feed verwerking gestart door elke host uitvoeren zijn. Elke host processor kan meerdere gebruikers hebben. Elke consumer Hallo wijziging feed leest vanaf Hallo partitie wordt toegewezen tooand ontvangt een melding van de host van wijzigingen en verlopen van leases.

toofurther informatie over hoe deze vier elementen van wijziging Feed Processor samenwerken, bekijk een voorbeeld in het volgende diagram Hallo. Hallo verzameling winkels documenten bewaakt en Hallo 'stad' gebruikt als partitiesleutel Hallo. Zien we dat Hallo blauw partitie enzovoort documenten met het veld 'plaats' Hallo uit "A E" bevat. Er zijn twee hosts, elk met twee consumenten lezen van Hallo vier partities parallel. Hallo pijlen wijzen Hallo consumenten lezen van een specifieke positie in Hallo feed wijzigen. In de eerste partitie hello betekent Hallo donkere blauw ongelezen wijzigingen en lichte blauw Hallo Hallo al gelezen wijzigingen op Hallo wijziging feed. Hallo hosts gebruiken Hallo lease verzameling toostore 'voortzetting' waarde tookeep bijgehouden Hallo huidige positie voor elke consumer lezen. 

![Met behulp van hello Azure Cosmos DB wijzigen feed processor host](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Met behulp van de wijziging Feed Processor-bibliotheek 
Hallo volgende sectie wordt uitgelegd hoe toouse wijziging Feed Processor-bibliotheek in de context voor het repliceren van wijzigingen uit een verzameling bron verzameling tooa bestemming Hallo Hallo. Hallo bronverzameling is hier Hallo bewaakt verzameling in de Feed wijziging-Processor. 

**Installeren en omvatten Hallo wijziging Feed Processor NuGet-pakket** 

Voordat u wijziging Feed Processor NuGet-pakket installeert, eerst installeren: 
* Microsoft.Azure.DocumentDB, versie 1.13.1 of hoger 
* Newtonsoft.Json, versie 9.0.1 of hoger installeren `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` en deze opnemen als een verwijzing.

**Een gecontroleerde, lease- en verzameling maken** 

In de volgorde toouse Hallo wijziging Feed Processor bibliotheek moet Hallo lease verzameling toobe gemaakt voordat Hallo processor host (s) wordt uitgevoerd. Opnieuw, is het raadzaam een lease-verzameling opslaan op een ander account met een schrijven regio dichter toowhere Hallo dat wijziging Feed Processor wordt uitgevoerd. In dit voorbeeld verplaatsing van gegevens moet toocreate Hallo doelverzameling voordat Hallo wijziging Feed Processor host wordt uitgevoerd. In de voorbeeldcode Hallo noemen we een helper methode toocreate Hallo bewaakt, geleasete, en de bestemming verzamelingen als deze niet al bestaan. 

> [!WARNING]
> Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor Hallo toepassing toocommunicate met Azure Cosmos DB. Voor meer informatie gaat u naar Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Maken van een host processor*

Hallo `ChangeFeedProcessorHost` klasse biedt een thread-veilige, met meerdere processen en veilige runtime-omgeving voor gebeurtenisprocessors die ook het plaatsen van controlepunten en partitie lease biedt. Hallo toouse `ChangeFeedProcessorHost` klasse, die u kunt implementeren `IChangeFeedObserver`. Deze interface bevat drie methoden:

* `OpenAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijzigen wordt geopend. Gewijzigde tooperform een specifieke actie kan zijn wanneer consumenten/zien wordt geopend.  
* `CloseAsync`: Deze functie wordt aangeroepen wanneer de feed zien wijziging wordt beëindigd. Gewijzigde tooperform een specifieke actie kan zijn als consument/zien is gesloten.  
* `ProcessChangesAsync`: Deze functie wordt aangeroepen wanneer nieuwe wijzigingen in het document beschikbaar op de feed wijzigen zijn. Het kan een specifieke actie na elke wijziging feed-update voor gewijzigde tooperform zijn.  

In ons voorbeeld we Hallo-interface implementeren `IChangeFeedObserver` via Hallo `DocumentFeedObserver` klasse. Hier Hallo `ProcessChangesAsync` upserts (updates) een document van de wijziging in de doelverzameling Hallo feed werken. In dit voorbeeld is nuttig voor het verplaatsen van gegevens van één verzameling tooanother in volgorde toochange Hallo partitiesleutel van een gegevensset. 

*Hallo Processor Host wordt uitgevoerd*

Beide opties voor feed wijzigen voordat u begint met de verwerking van gebeurtenissen, en opties van de feed host wijzigen kunnen worden aangepast. 
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
Hallo specifieke velden die kunnen worden aangepast worden samengevat in Hallo tabellen te volgen. 

**Opties voor Feed wijzigen**:
<table>
    <tr>
        <th>De naam van eigenschap</th>
        <th>Beschrijving</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Opgehaald of ingesteld Hallo kunt u het maximum aantal items toobe geretourneerd in de inventarisatiebewerking Hallo in hello Azure Cosmos DB database-service.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Opgehaald of ingesteld van Hallo partitie sleutel bereik-id voor de huidige aanvraag Hallo in hello Azure Cosmos DB database-service.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Opgehaald of ingesteld van Hallo aanvraag vervolgtoken in hello Azure Cosmos DB database-service.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Opgehaald of ingesteld van sessietoken Hallo voor gebruik met de sessieconsistentie in hello Azure Cosmos DB database-service.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Opgehaald of ingesteld of wijziging feeds in hello Azure Cosmos DB database-service moet worden gestart van Hallo vanaf (true) of van de huidige (false). Standaard wordt gestart vanuit de huidige (false).</td>
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
        <td>Hello-interval voor alle leases voor partities die momenteel worden vastgehouden door Hallo ChangeFeedEventHost exemplaar.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Hallo interval tookick uit een taak toocompute of partities gelijkmatig zijn verdeeld over bekende host exemplaren.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Hallo-interval voor welke Hallo lease wordt uitgevoerd op een lease voor een partitie. Als de lease Hallo niet wordt verlengd binnen dit interval, het is verlopen en eigendom van Hallo partitie verplaatst tooanother ChangeFeedEventHost exemplaar.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>Hallo vertraging tussen een partitie voor de nieuwe wijzigingen op Hallo polling feed nadat alle huidige wijzigingen zijn geleegd.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Hallo frequentie toocheckpoint leases.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Hallo partitie moet minimaal aantal voor Hallo host.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>Hallo kunt u het maximum aantal partities Hallo host kan fungeren.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>BOOL</td>
        <td>Of op Hallo van de host Hallo alle bestaande leases starten moeten worden verwijderd en Hallo host moet worden gestart vanaf het begin.</td>
    </tr>
</table>


het instantiëren van toostart gebeurtenisverwerking, `ChangeFeedProcessorHost`, bieden de juiste parameters Hallo voor uw Azure DB die Cosmos-verzameling. Roep vervolgens `RegisterObserverAsync` tooregister uw `IChangeFeedObserver` (DocumentFeedObserver in dit voorbeeld)-implementatie met Hallo-runtime. Op dit moment probeert Hallo host tooacquire een lease op elke partitiesleutelbereik in hello Azure Cosmos DB verzameling op basis van een greedy-algoritme. Deze leases gedurende een bepaald tijdsbestek geldig en moeten daarna worden vernieuwd. Zodra nieuwe knooppunten worker-exemplaren in dit geval online komen, ze reserveringen voor leases en gedurende een bepaalde periode Hallo load verschuift tussen knooppunten elke host probeert tooacquire meer leases. 

In voorbeeldcode hello, gebruiken we een klasse (DocumentFeedObserverFactory.cs) factory toocreate een zien en Hallo `RegistObserverFactoryAsync` tooregister Hallo zien. 

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
In de loop van de tijd komt er een evenwicht tot stand. Deze dynamische mogelijkheid kan tooconsumers naar automatische schaling toobe toegepast voor schaal omhoog en omlaag schalen op basis van CPU. Als er wijzigingen zijn beschikbaar in Azure Cosmos DB sneller dan consumers kunnen verwerken, kan Hallo CPU toename op consumenten gebruikte toocause een automatisch geschaald aantal werkrolexemplaren zijn.

## <a name="next-steps"></a>Volgende stappen
* Probeer Hallo [Azure Cosmos DB Wijzig feed codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Aan de slag met Hallo coderen [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/).
