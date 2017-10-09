---
title: aaaSQL query metrische gegevens voor de API van Azure Cosmos DB DocumentDB | Microsoft Docs
description: Meer informatie over hoe tooinstrument en foutopsporing Hallo prestaties van de SQL-query's van Azure DB die Cosmos-aanvragen.
keywords: SQL-syntaxis, sql-query, sql-query's, json-querytaal, database-concepten en sql-query's, statistische functies
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Prestaties van query's met Azure Cosmos DB afstemmen
Azure Cosmos DB biedt een [SQL-API voor het opvragen van gegevens](documentdb-sql-query.md), zonder schema of secundaire indexen. Dit artikel wordt de volgende informatie voor ontwikkelaars Hallo:

* Details op hoog niveau over de werking van Azure Cosmos DB SQL-query-uitvoering
* Meer informatie over de aanvraag- en reactieheaders query en opties voor client-SDK
* Tips en aanbevolen procedures voor prestaties van query 's
* Voorbeelden van hoe tooutilize SQL uitvoering statistieken toodebug query uitvoeren op prestaties

## <a name="about-sql-query-execution"></a>Over het uitvoeren van de SQL-query

In Azure Cosmos DB, slaat u de gegevens in de containers die kunnen worden uitgebreid tooany [grootte of aanvraag opslagdoorvoer](partition-data.md). Azure Cosmos DB schaalt naadloos gegevens meerdere fysieke partities onder Hallo dekt toohandle Gegevensgroei of stijging van ingerichte doorvoer. U kunt SQL-query's tooany container Hallo REST-API of een van de Hallo ondersteund met de opdracht [DocumentDB SDK's](documentdb-sdk-dotnet.md).

Een kort overzicht van het partitioneren: definieert u een partitiesleutel zoals 'plaats', waarmee wordt bepaald hoe gegevens zijn verdeeld over fysieke partities. Gegevens die behoren tooa één partitiesleutel (bijvoorbeeld 'city' == "Seattle") zijn opgeslagen in een fysieke partitie maar één fysieke partitie heeft doorgaans meerdere partitiesleutels. Wanneer een partitie zijn opslaggrootte bereikt, Hallo service naadloos Hallo partitie worden gesplitst in twee nieuwe partities en Hallo partitiesleutel gelijkmatig wordt verdeeld over deze partities. Aangezien partities tijdelijke zijn, hello API's gebruiken een abstractie van een 'partitiesleutelbereik', waarmee de Hallo bereiken van de belangrijkste hashes partitie. 

Wanneer u een query tooAzure Cosmos DB verzendt, voert Hallo SDK deze logische stappen uit:

* Hallo SQL query toodetermine Hallo uitvoering queryplan parseren. 
* Als het Hallo-query bevat een filter voor de partitiesleutel hello, zoals `SELECT * FROM c WHERE c.city = "Seattle"`, gerouteerde tooa is één partitie. Als het Hallo-query heeft geen een filter voor de partitiesleutel en vervolgens deze wordt uitgevoerd in alle partities en de resultaten worden samengevoegd clientzijde.
* Hallo-query is uitgevoerd binnen elke partitie in de reeks of parallel, op basis van de clientconfiguratie. Binnen elke partitie Hallo query mogelijk maken een of meer retouren, afhankelijk van de complexiteit van de query hello, geconfigureerd paginaformaat en ingerichte doorvoer van Hallo-verzameling. Elke uitvoering retourneert Hallo aantal [aanvraageenheden](request-units.md) verbruikt door uitvoering van de query, en desgewenst Uitvoeringsstatistieken query. 
* Hallo SDK voert een samenvatting van de queryresultaten Hallo meerdere partities. Bijvoorbeeld, als Hallo query een ORDER BY meerdere partities omvat, zijn vervolgens resultaten uit afzonderlijke partities tooreturn samenvoegen gesorteerd resultaten globaal sorteren. Als het Hallo-query is een aggregatie zoals `COUNT`, Hallo tellingen van afzonderlijke partities worden de opgetelde tooproduce Hallo totale aantal.

Hallo-SDK's bieden verschillende opties voor het uitvoeren van de query. Bijvoorbeeld in .NET deze opties zijn beschikbaar in Hallo `FeedOptions` klasse. Hallo volgende tabel beschrijft deze opties en hoe ze invloed hebben op uitvoeringstijd van de query. 

| Optie | Beschrijving |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | U moet instellen tootrue voor elke query die toobe uitgevoerd op meer dan één partitie vereist. Dit is een expliciete vlag tooenable u toomake weloverwogen prestatie-en nadelen tijdens de ontwikkeling. |
| `EnableScanInQuery` | Moet worden tootrue ingesteld als u ervoor hebt gekozen buiten het indexeren, maar toch wilt dat toorun Hallo query via een scan. Alleen van toepassing als indexering voor Hallo aangevraagd filterpad is uitgeschakeld. | 
| `MaxItemCount` | Hallo maximum aantal items tooreturn per round trip toohello server. Door in te stellen te-1, kunt u Hallo server Hallo aantal items beheren. Of u kunt deze waarde tooretrieve slechts een klein aantal items per round trip verlagen. 
| `MaxBufferedItemCount` | Dit is een optie voor de clientzijde en toolimit Hallo geheugenverbruik gebruikt bij het uitvoeren van cross-partitie ORDER BY. Een hogere waarde vermindert Hallo latentie voor het sorteren van cross-partitie. |
| `MaxDegreeOfParallelism` | Opgehaald of ingesteld Hallo aantal gelijktijdige bewerkingen clientzijde tijdens parallelle queryuitvoering in hello Azure DocumentDB-database-service wordt uitgevoerd. Een positief eigenschapswaarde beperkt Hallo aantal gelijktijdige bewerkingen toohello ingestelde waarde. Als deze tooless dan 0 is ingesteld, besluit Hallo systeem automatisch het aantal gelijktijdige bewerkingen toorun Hallo. |
| `PopulateQueryMetrics` | Hiermee gedetailleerde logboekregistratie van statistieken voor de tijd die is doorgebracht in verschillende fasen van de uitvoering van de query zoals compileertijd en index Lustijd document laden tijd. Met de ondersteuning van Azure toodiagnose query prestatieproblemen kunt u de uitvoer van de query statistieken delen. |
| `RequestContinuation` | U kunt de queryuitvoering hervatten door door te geven in een ondoorzichtige vervolgtoken Hallo geretourneerd door een query. Hallo vervolgtoken ingekapseld alle staat is vereist voor uitvoering van de query. |
| `ResponseContinuationTokenLimitInKb` | U kunt Hallo maximale grootte van Hallo vervolgtoken geretourneerd door de server Hallo beperken. Mogelijk moet u tooset dit als uw toepassingshost limieten op antwoord header-grootte. Wanneer dit wordt mogelijk uitgebreid Hallo totale duur en RUs verbruikt voor het Hallo-query.  |

Bijvoorbeeld, u gaat nu een voorbeeldquery op partitiesleutel is aangevraagd op een verzameling met `/city` als Hallo partitie sleutel en ingericht met 100.000 RU/s doorvoer. U deze query met aanvragen `CreateDocumentQuery<T>` in .NET Hallo volgende:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Hallo SDK codefragment hierboven weergegeven, overeenkomt met toohello REST-API-aanvraag te volgen:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Elke pagina van de uitvoering van query overeenkomt met de REST-API tooa `POST` Hello `Accept: application/query+json` kop- en SQL-query in de hoofdtekst van het Hallo Hallo. Elke query kunnen een of meer reizen toohello server Hello afronden `x-ms-continuation` token teruggestuurd tussen het Hallo-client en server tooresume uitvoeren. Hallo configuratieopties in FeedOptions worden toohello server in de vorm Hallo van aanvraagheaders doorgegeven. Bijvoorbeeld: `MaxItemCount` komt overeen te`x-ms-max-item-count`. 

Hallo aanvraag retourneert Hallo volgende (afgekapt voor leesbaarheid) antwoord:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

Hallo sleutel antwoordheaders geretourneerde Hallo query zijn Hallo volgende:

| Optie | Beschrijving |
| ------ | ----------- |
| `x-ms-item-count` | Hallo aantal items in Hallo antwoord geretourneerd. Dit is afhankelijk van de opgegeven Hallo `x-ms-max-item-count`, Hallo aantal items dat binnen de maximale reactiegrootte nettolading Hallo Hallo ingerichte doorvoer en uitvoeringstijd van de query past. |  
| `x-ms-continuation:` | Hallo voortzetting token tooresume uitvoering van Hallo query, als er extra resultaten beschikbaar zijn. | 
| `x-ms-documentdb-query-metrics` | Hallo query statistieken voor Hallo uitvoering. Dit is een tekenreeks met scheidingstekens met statistieken van de tijd besteed aan Hallo verschillende fasen van de uitvoering van de query. Geretourneerde als `x-ms-documentdb-populatequerymetrics` te is ingesteld`True`. | 
| `x-ms-request-charge` | aantal Hallo [aanvraageenheden](request-units.md) verbruikt door Hallo-query. | 

Zie voor meer informatie over Hallo REST-API-aanvraagheaders en opties [opvragen van resources met behulp van Hallo DocumentDB REST-API](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Aanbevolen procedures voor prestaties van query 's
Hallo volgen Hallo meest voorkomende factoren die van invloed op prestaties van Azure DB die Cosmos-query's. We verdiepen in elk van deze onderwerpen in dit artikel.

| Factor | Tip | 
| ------ | -----| 
| Ingerichte doorvoer | Meet RU per query en zorg ervoor dat er Hallo vereist ingerichte doorvoer voor uw query's. | 
| Partitionering en partitiesleutels | Voorkeur voor query's met Hallo partitie sleutelwaarde in filtercomponent Hallo voor lage latentie. |
| SDK en query-opties | Volg de aanbevolen procedures van de SDK zoals directe verbinding en clientzijde uitvoering queryopties afstemmen. |
| Netwerklatentie | Account voor netwerk overhead in meting en gebruik multihoming API's tooread van Hallo dichtstbijzijnde regio. |
| Indexeringsbeleid | Zorg ervoor dat u Hallo vereist paden/indexeringsbeleid voor Hallo-query. |
| Query-uitvoering metrische gegevens | Analyseer Hallo query uitvoering metrische gegevens tooidentify potentiële regeneraties van query's en vormen.  |

### <a name="provisioned-throughput"></a>Ingerichte doorvoer
In de Cosmos-DB maakt u containers voor gegevens, elk met gereserveerde doorvoer, uitgedrukt in de aanvraag-eenheden (RU) per de seconde. Het lezen van een document van 1 KB is 1 RU en elke bewerking (met inbegrip van query's) is genormaliseerde tooa vast aantal RUs op basis van de complexiteit. Bijvoorbeeld, als er 1000 RU/s ingericht voor de container en u hebt een query zoals `SELECT * FROM c WHERE c.city = 'Seattle'` die 5 RUs verbruikt en vervolgens kunt u uitvoeren (1000 RU/s) / (5 RU/query) = 200 query/s dergelijke query's per seconde. 

Als u meer dan 200 query's per seconde indient, begint Hallo service binnenkomende aanvragen frequentiebeperkende hierboven 200/s. in dit geval Hallo SDK's automatisch verwerken door het uitvoeren van een backoff/nieuwe poging en daarom ziet u mogelijk een hogere latentie voor deze query's. Hallo ingerichte doorvoer toohello verhogen vereist waarde verbetert uw Querylatentie en de doorvoer. 

toolearn meer informatie over aanvraageenheden, Zie [Aanvraageenheden](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Partitionering en partitiesleutels
Met Azure Cosmos DB doorgaans uitvoeren query's in volgorde van de snelste/meest efficiënte tooslower/minder efficiënt Hallo. 

* Op een enkele partitie en item sleutel ophalen
* Query's uitvoeren met een filter-component op een enkele partitiesleutel
* Query uitvoeren zonder dat een gelijkheid of bereik filter-component op een eigenschap
* Een query uitvoeren zonder filters

Zoekt die tooconsult moeten alle partities nodig hogere latentie en hogere RUs kan gebruiken. Aangezien elke partitie automatisch indexeren tegen alle eigenschappen heeft, kan Hallo query worden geleverd efficiënt uit Hallo index in dit geval. U kunt query's die sneller partities met behulp van Hallo parallelle uitvoering opties omvatten.

toolearn meer informatie over partitioneren en partitiesleutels, Zie [partitioneren in Azure Cosmos DB](partition-data.md).

### <a name="sdk-and-query-options"></a>SDK en query-opties
Zie [Tips voor betere prestaties](performance-tips.md) en [prestatietests](performance-testing.md) voor hoe tooget Hallo beste clientzijde prestaties van de Azure Cosmos-database. Dit omvat het gebruik Hallo nieuwste SDK's, platform-specifieke netwerkconfiguraties als standaardaantal verbindingen, frequentie van garbagecollection, configureren en gebruiken van lightweight connectiviteitsopties zoals Direct/TCP. 


#### <a name="max-item-count"></a>Aantal items max
Hallo voor query's, waarde van `MaxItemCount` kan een aanzienlijke invloed hebben op het moment dat de end-to-end-query. Elke retournetwerklatentie toohello server retourneren niet meer dan het aantal items in Hallo `MaxItemCount` (standaard van 100 objecten). Als u deze tooa hogere waarde (-1 is maximum- en aanbevolen) worden uw totale duur van de query verbeteren door het aantal retouren tussen server en client, met name voor query's met grote resultatensets hello te beperken.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Maximale mate van parallelle uitvoering
Voor query's optimaliseren Hallo `MaxDegreeOfParallelism` tooidentify Hallo aanbevolen configuraties voor uw toepassing, met name als u bij het uitvoeren van query's de cross-partitie (zonder een filter op Hallo partitiesleutel waarde). `MaxDegreeOfParallelism`Hiermee bepaalt u Hallo maximum aantal parallelle taken, dat wil zeggen, Hallo maximumaantal partities toobe parallel bezocht. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Stel dat
* D = standaard maximale aantal parallelle taken (totaal aantal processor in client-computer Hallo =)
* P = gebruiker opgegeven maximale aantal parallelle taken
* N = aantal partities die u moet een toobe bezocht voor het beantwoorden van een query

Hieronder vindt u implicaties van hoe de zich Hallo parallelle query's voor verschillende waarden van P. gedragen zou
* (P == 0) = > seriële modus
* (P == 1) = > maximaal één taak
* (P > 1) = > parallelle taken Min (P, N) 
* (P < 1) = > parallelle taken Min (N, D)

Voor SDK-releaseopmerkingen en Zie voor meer informatie over geïmplementeerde klassen en methoden [DocumentDB SDK's](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Netwerklatentie
Zie [Azure Cosmos DB globale distributie](tutorial-global-distribution-documentdb.md) tooset-up maken van globale distributie en verbinding maken met de dichtstbijzijnde regio toohello. Netwerklatentie heeft een aanzienlijke invloed op prestaties van query's als u een grote resultatenset Hallo query ophalen of toomake meerdere retouren nodig. 

Hallo sectie op metrische gegevens query-uitvoering wordt uitgelegd hoe tooretrieve Hallo server uitvoeringstijd van query's ( `totalExecutionTimeInMs`), zodat u tijd besteed aan het uitvoeren van de query en -tijd besteed aan het netwerk onderweg kunt onderscheiden.

### <a name="indexing-policy"></a>Indexeringsbeleid
Zie [indexeringsbeleid configureren](indexing-policies.md) voor indexeren paden, soorten, en modi en invloed op uitvoering van de query. Hallo indexeren beleid gebruikt standaard hash-indexering voor tekenreeksen, die geldt voor gelijkheid query's, maar niet voor query's bereik/order by-query's. Als u een bereik query's nodig voor tekenreeksen, wordt u aangeraden Hallo bereik indextype voor alle tekenreeksen geven. 

## <a name="query-execution-metrics"></a>Query-uitvoering metrische gegevens
U kunt gedetailleerde metrische gegevens op de uitvoering van de query verkrijgen door door te geven in Hallo optionele `x-ms-documentdb-populatequerymetrics` header (`FeedOptions.PopulateQueryMetrics` in Hallo .NET SDK). waarde geretourneerd in Hallo `x-ms-documentdb-query-metrics` heeft Hallo sleutel / waarde-paren die zijn bedoeld voor geavanceerde probleemoplossing van de uitvoering van de query te volgen. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Gegevens | Eenheid | Beschrijving | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | milliseconden | Uitvoeringstijd van de query | 
| `queryCompileTimeInMs` | milliseconden | Query-compilatie  | 
| `queryLogicalPlanBuildTimeInMs` | milliseconden | Tijd toobuild logische queryplan | 
| `queryPhysicalPlanBuildTimeInMs` | milliseconden | Tijd toobuild fysieke queryplan | 
| `queryOptimizationTimeInMs` | milliseconden | Tijd besteed aan de query te optimaliseren | 
| `VMExecutionTimeInMs` | milliseconden | Tijd besteed aan de query-runtime | 
| `indexLookupTimeInMs` | milliseconden | Tijd besteed aan fysieke index laag | 
| `documentLoadTimeInMs` | milliseconden | Tijd besteed aan het laden van documenten  | 
| `systemFunctionExecuteTimeInMs` | milliseconden | Totale tijd besteed aan het uitvoerende system (ingebouwde) functies in milliseconden  | 
| `userFunctionExecuteTimeInMs` | milliseconden | Totale tijd besteed worden uitgevoerd door de gebruiker gedefinieerde functies in milliseconden | 
| `retrievedDocumentCount` | milliseconden | Totaal aantal opgehaalde documenten  | 
| `retrievedDocumentSize` | Bytes | Totale grootte van de opgehaalde documenten in bytes  | 
| `outputDocumentCount` | Aantal | Het aantal uitvoerdocumenten | 
| `writeOutputTimeInMs` | milliseconden | Uitvoeringstijd van de query in milliseconden | 
| `indexUtilizationRatio` | verhouding (< = 1) | Verhouding tussen aantal documenten dat overeenkomt met de Hallo filter toohello aantal documenten die worden geladen  | 

Hallo client SDK's kunnen intern query maken die meerdere query operations tooserve Hallo binnen elke partitie. Hallo client meer dan één aanroep per partitie als het totaal aantal resultaten Hallo overschrijdt maakt `x-ms-max-item-count`, als Hallo query Hallo ingerichte doorvoer voor Hallo-partitie overschrijdt, of als hello query nettolading Hallo maximale grootte per pagina bereikt of als hello query Hallo bereikt systeem toegewezen time-outlimiet. Elke gedeeltelijke queryuitvoering retourneert een `x-ms-documentdb-query-metrics` voor die pagina. 

Hier volgen enkele voorbeeldquery's en hoe toointerpret sommige Hallo metrische gegevens van de uitvoering van de query geretourneerd: 

| Query’s uitvoeren | Voorbeeld metrische gegevens | Beschrijving | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Hallo aantal documenten opgehaald is is 100 + 1 toomatch Hallo de TOP-component. Querytijd voornamelijk die is doorgebracht in `WriteOutputTime` en `DocumentLoadTime` omdat het een scan. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount is nu hogere (500 + 1 toomatch Hallo component TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Ongeveer 0,9 ms is besteed aan IndexLookupTime voor een sleutel-lookup, omdat deze het opzoeken van een index op `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Iets meer tijd (1,7 ms) die is doorgebracht in IndexLookupTime via een scan bereik omdat dit het opzoeken van een index op `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Dezelfde tijd besteed aan `DocumentLoadTime` als de voorgaande query's, maar lagere `WriteOutputTime` omdat we bij het projecteren van slechts één eigenschap. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Punt 213 ms is die is doorgebracht in `UserDefinedFunctionExecutionTime` uitvoeren UDF Hallo van elke waarde van `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Er is ongeveer 0,6 ms gespendeerd aan het `IndexLookupTime` op `/Name/?`. De meeste Hallo uitvoeringstijd (ms ~ 7)-query in `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | Query als een scan wordt uitgevoerd, omdat deze gebruikmaakt van `LOWER`, en 500 buiten 2491 opgehaalde documenten worden geretourneerd. |


## <a name="next-steps"></a>Volgende stappen
* toolearn over Hallo ondersteund SQL-query's en trefwoorden, Zie [SQL-query](documentdb-sql-query.md). 
* toolearn over aanvraageenheden, Zie [aanvraageenheden](request-units.md).
* toolearn over indexeringsbeleid, Zie [indexeren van beleid](indexing-policies.md) 


