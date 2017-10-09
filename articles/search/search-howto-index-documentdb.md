---
title: aaaIndexing een Cosmos-DB-gegevensbron voor Azure Search | Microsoft Docs
description: Dit artikel ziet u hoe toocreate een Azure Search-indexeerfunctie met Cosmos DB als gegevensbron.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Cosmos DB verbinding te maken met Azure Search met behulp van indexeerfuncties

Als u een goede zoekopdracht ervaren tooimplement via uw Cosmos-DB-gegevens wilt, kunt u een Azure Search indexeerfunctie toopull gegevens in een Azure Search-index. In dit artikel wordt uitgelegd hoe u dat toointegrate Azure Cosmos DB met Azure Search zonder toowrite elke code toomaintain indexing-infrastructuur.

tooset van een indexeerfunctie Cosmos DB, hebt u een [Azure Search-service](search-create-service-portal.md), en maak een index, datasource en ten slotte Hallo indexeerfunctie. U kunt deze objecten met behulp van Hallo maken [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), of [REST-API](/rest/api/searchservice/) voor alle niet-.NET-talen. 

Als u ervoor voor Hallo-portal kiezen, Hallo [wizard gegevens importeren](search-import-data-portal.md) leidt u door Hallo maken van al deze resources.

> [!NOTE]
> Cosmos DB is Hallo volgende generatie van DocumentDB. Hoewel Hallo productnaam is gewijzigd, wordt het syntaxis als voorheen dezelfde Hallo. U kunt doorgaan toospecify `documentdb` zoals beschreven in dit artikel indexeerfunctie. 

> [!TIP]
> U kunt starten Hallo **gegevens importeren** wizard van Hallo Cosmos DB dashboard toosimplify voor de gegevensbron te indexeren. In de navigatie aan de linkerkant, gaat u te**verzamelingen** > **toevoegen Azure Search** tooget gestart.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Azure Search-indexeerfunctie-concepten
Azure Search ondersteunt Hallo maken en beheren van gegevensbronnen (inclusief Cosmos DB) en indexeerfuncties die van toepassing is die gegevensbronnen.

Een **gegevensbron** Hallo gegevens tooindex, referenties en het beleid voor het identificeren van wijzigingen in Hallo-gegevens (zoals gewijzigde of verwijderde documenten binnen uw verzameling). Hallo-gegevensbron is gedefinieerd als een onafhankelijke resource zodat deze kan worden gebruikt door meerdere indexeerfuncties.

Een **indexeerfunctie** wordt beschreven hoe gegevens Hallo loopt uit uw gegevensbron in een doel search-index. Een indexeerfunctie kan worden gebruikt voor:

* Uitvoeren van een momentopname van Hallo gegevens toopopulate een index.
* Een index met wijzigingen in de gegevensbron Hallo volgens een schema worden gesynchroniseerd. Hallo planning maakt deel uit van Hallo indexeerfunctie definitie.
* Updates op aanvraag tooan index zo nodig worden aangeroepen.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Stap 1: Een gegevensbron maken
toocreate een gegevensbron, gaat u een POST:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

Hallo-hoofdtekst van Hallo-aanvraag bevat Hallo definitie van de gegevensbron, waaronder Hallo velden na moet:

* **naam**: Kies een naam toorepresent uw Cosmos-DB-database.
* **type**: moet `documentdb`.
* **referenties**:
  
  * **connectionString**: vereist. Hallo verbinding info tooyour Azure Cosmos DB database opgeven in Hallo volgende indeling:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **container**:
  
  * **naam**: vereist. Hallo-id van Hallo Cosmos DB verzameling toobe geïndexeerd opgeven.
  * **query**: optioneel. U kunt een query tooflatten een willekeurige JSON-document opgeven in een platte schema dat u kunt de Azure Search index.
* **dataChangeDetectionPolicy**: aanbevolen. Zie [gewijzigd documenten te indexeren](#DataChangeDetectionPolicy) sectie.
* **dataDeletionDetectionPolicy**: optioneel. Zie [verwijderd documenten te indexeren](#DataDeletionDetectionPolicy) sectie.

### <a name="using-queries-tooshape-indexed-data"></a>Met behulp van query's tooshape geïndexeerde gegevens
U kunt een Cosmos-DB query tooflatten genest eigenschappen of matrices, project JSON-eigenschappen en filteren Hallo gegevens toobe geïndexeerd opgeven. 

Voorbeelddocument:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Filterquery:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Plat query:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Projectie-query:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Matrix afvlakken query:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Stap 2: Een index maken
Een doel-Azure Search-index maken als u nog niet hebt. U kunt een index maken met Hallo [gebruikersinterface van Azure portal](search-create-index-portal.md), Hallo [Index REST-API maken](/rest/api/searchservice/create-index) of [Index klasse](/dotnet/api/microsoft.azure.search.models.index).

Hallo volgende voorbeeld maakt een index met een veld-id en -beschrijving:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Zorg ervoor dat Hallo schema van de doelindex is compatibel met Hallo-schema van Hallo bron JSON-documenten of Hallo-uitvoer van uw aangepaste query-projectie.

> [!NOTE]
> Voor gepartitioneerde verzamelingen is de standaardsleutel document Hallo Cosmos-database `_rid` eigenschap, die wordt gewijzigd te`rid` in Azure Search. Bovendien Cosmos DB van `_rid` waarden bevatten tekens die ongeldig in Azure Search-sleutels zijn. Om deze reden Hallo `_rid` waarden Base64-gecodeerd zijn.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Toewijzing tussen JSON-gegevenstypen en Azure Search-gegevenstypen
| JSON-GEGEVENSTYPE | COMPATIBEL DOEL INDEX VELDTYPEN |
| --- | --- |
| BOOL |Edm.Boolean, Edm.String |
| Cijfers die als gehele getallen eruitzien |Edm.Int32, Edm.Int64, Edm.String |
| Cijfers die zijn opgemaakt als drijvende-punten |Edm.Double, Edm.String |
| Tekenreeks |Edm.String |
| Matrices met primitieve typen, bijvoorbeeld ["a", "b", "c"] |Collection(EDM.String) |
| Tekenreeksen die lijken op datums |Edm.DateTimeOffset, Edm.String |
| GeoJSON-objecten, bijvoorbeeld {'type': 'Point', 'coordinates': [lang, lat]} |Edm.GeographyPoint |
| Andere JSON-objecten |N.v.t. |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Stap 3: Maak een indexeerfunctie

Zodra het Hallo-index en gegevensbron zijn gemaakt, bent u klaar toocreate Hallo indexeerfunctie:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Elke twee uur wordt uitgevoerd door deze indexeerfunctie (schema-interval is ingesteld, te 'PT2H'). een indexeerfunctie toorun elke 30 minuten ingesteld hello-interval te 'PT30M'. Hallo kortste voor het interval is 5 minuten. Hallo schema is optioneel - als u dit weglaat, een indexeerfunctie slechts één keer is uitgevoerd wanneer deze gemaakt. U kunt echter een indexeerfunctie op aanvraag uitvoeren op elk gewenst moment.   

Voor meer informatie over Hallo indexeerfunctie-API maken, Bekijk [indexeerfunctie maken](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Indexeerfunctie op aanvraag uitvoeren
In aanvulling toorunning periodiek volgens een schema, kan ook een indexeerfunctie worden aangeroepen op aanvraag:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Wanneer uitvoeren API is geretourneerd, Hallo indexeerfunctie aanroep is gepland, maar verloopt asynchroon Hallo verwerkt. 

Status van de indexeerfunctie Hallo in Hallo portal of met behulp van Hallo ophalen indexeerfunctie Status API, die vervolgens worden beschreven, kunt u bewaken. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Ophalen van de status van de indexeerfunctie
Hallo-status en uitvoering geschiedenis van een indexeerfunctie kunt u ophalen:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

Hallo antwoord bevat algehele status van de indexeerfunctie en Hallo laatste (of in uitvoering) indexeerfunctie aanroep Hallo geschiedenis van recente indexeerfunctie aanroepen.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Uitvoergeschiedenis bevat up toohello 50 meest recente voltooide uitvoering en in omgekeerde volgorde worden gesorteerd (dus de meest recente uitvoering Hallo eerst in het antwoord Hallo komt).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Gewijzigde documenten te indexeren
Hallo-doel van een data detectie wijzigingsbeleid is tooefficiently artikelen gewijzigde gegevens identificeren. Is momenteel alleen ondersteund Hallo beleid Hallo `High Water Mark` met behulp van Hallo `_ts` (tijdstempel)-eigenschap opgegeven Cosmos-DB die wordt opgegeven als volgt:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Met dit beleid wordt aangeraden tooensure indexeerfunctie goede prestaties. 

Als u een aangepaste query gebruikt, zorgt u ervoor dat Hallo `_ts` eigenschap wordt toegewezen door Hallo-query.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Voortgang van de incrementele en aangepaste query 's
Incrementele voortgang tijdens het indexeren zorgt ervoor dat als de uitvoering van de indexeerfunctie wordt onderbroken door tijdelijke fouten of uitvoeringstijd limiet, Hallo indexeerfunctie kan worden opgepikt waar deze gebleven zodra deze wordt uitgevoerd was, in plaats van toore index Hallo volledige verzameling vanaf het begin. Dit is vooral belangrijk wanneer u grote verzamelingen. 

tooenable incrementele voortgang bij gebruik van een aangepaste query ervoor te zorgen dat uw query Hallo resultaten door Hallo orders `_ts` kolom. Hierdoor kunnen periodieke controle wijst dat gebruikmaakt van Azure Search tooprovide incrementele voortgang in Hallo aanwezigheid van fouten.   

In sommige gevallen, zelfs als de query bevat een `ORDER BY [collection alias]._ts` component, Azure Search kan niet afleiden die Hallo-query is geordend op Hallo `_ts`. U Azure Search kunt zien dat de resultaten zijn gerangschikt met behulp van Hallo `assumeOrderByHighWaterMarkColumn` configuratie-eigenschap. toospecify deze hint maken of bijwerken van de indexeerfunctie als volgt: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Documenten te indexeren verwijderd
Wanneer rijen worden verwijderd uit verzameling hello, u normaal toodelete die rijen uit ook Hallo search-index. Hallo-doel van een gegevens-verwijderingsbeleid detectie is tooefficiently verwijderde gegevensitems identificeren. Is momenteel alleen ondersteund Hallo beleid Hallo `Soft Delete` beleid (verwijdering is gemarkeerd met een van de markering van sommige sorteren), die is opgegeven als volgt:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Als u een aangepaste query gebruikt, controleert u of die Hallo-eigenschap waarnaar wordt verwezen door `softDeleteColumnName` wordt geprojecteerd door Hallo-query.

Hallo volgende voorbeeld maakt een gegevensbron met een beleid voor voorlopig verwijderen:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Volgende stappen
Gefeliciteerd. U hebt geleerd hoe toointegrate Azure Cosmos DB met Azure Search met behulp van de indexeerfunctie Hallo voor Cosmos-DB.

* toolearn hoe meer informatie over het Azure Cosmos DB Zie Hallo [Cosmos-DB-servicepagina](https://azure.microsoft.com/services/documentdb/).
* toolearn hoe meer informatie over het Azure Search Zie Hallo [service zoekpagina](https://azure.microsoft.com/services/search/).
