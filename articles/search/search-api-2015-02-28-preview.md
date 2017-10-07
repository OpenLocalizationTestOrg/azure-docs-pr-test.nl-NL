---
title: aaaAzure Search Service REST API-versie Preview 2015-02-28-| Microsoft Docs
description: Azure Search Service REST API-versie 2015-02-28-Preview bevat experimentele functies zoals natuurlijke Taalanalyse en moreLikeThis zoekopdrachten.
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>Azure Search Service REST-API: Versie 2015-02-28-Preview
Dit artikel is Hallo-naslagdocumentatie voor `api-version=2015-02-28-Preview`. Deze preview Hallo huidige algemeen beschikbaar versie, breidt [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), doordat Hallo volgende experimentele kenmerken:

* `moreLikeThis`queryparameter in Hallo [documenten zoeken](#SearchDocs) API. Andere documenten die specifiek document relevante tooanother zijn gevonden.

Een paar extra onderdelen van Hallo `2015-02-28-Preview` REST-API afzonderlijk worden beschreven. Deze omvatten:

* [Score berekenen voor profielen](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexeerfuncties](search-api-indexers-2015-02-28-preview.md)

Azure Search-service is beschikbaar in meerdere versies. Raadpleeg het te[Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie.

## <a name="apis-in-this-document"></a>API's in dit document
Azure-API van zoekservice ondersteunt twee URL-syntaxis voor de API-bewerkingen: eenvoudige en OData (Zie [ondersteuning voor OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) voor meer informatie). Hallo bevat volgende lijst eenvoudige Hallo-syntaxis.

[Index maken](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Index bijwerken](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Index ophalen](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Aanbieding-indexen](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Indexstatistieken opvragen](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Test Analyzer](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Een Index verwijderen](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Toevoegen, verwijderen, en gegevens in een Index bijwerken](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Documenten zoeken](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Lookup-Document](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Aantal documenten](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Suggesties](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Indexbewerkingen
U kunt maken en beheren van de indexen in Azure Search-service via een eenvoudige HTTP-aanvragen (POST, GET, PUT, DELETE) op basis van een resource voor de gegeven index. toocreate een index u boeken eerst een JSON-document met een beschrijving van Hallo Indexeer schema. Hallo schema gedefinieerd Hallo velden van het Hallo-index, de gegevenstypen en hoe ze kunnen worden gebruikt (bijvoorbeeld in zoekopdrachten in volledige tekst, filters, sorteren of facetten). Het definieert ook scoreprofiel profielen, suggestiefunctie en andere kenmerken tooconfigure Hallo gedrag van Hallo index.

Hallo bevat volgende voorbeeld een afbeelding van een schema dat wordt gebruikt voor zoekopdrachten op gegevens van hotel met Hallo beschrijvingsveld gedefinieerd in twee talen. U ziet hoe kenmerken bepalen hoe Hallo veld wordt gebruikt. Bijvoorbeeld Hallo `hotelId` wordt gebruikt als de documentsleutel hello (`"key": true`) en wordt uitgesloten van zoekopdrachten in volledige tekst (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Nadat Hallo index is gemaakt, kunt u documenten die Hallo index vullen gaat uploaden. Zie [toevoegen of Update documenten](#AddOrUpdateDocuments) voor deze stap.

Zie voor een video-inleiding tooindexing in Azure Search, Hallo [aflevering Channel 9 Cloud hebben betrekking op Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Index maken
Een index is Hallo primaire methode voor het ordenen en documenten zoeken in Azure Search, vergelijkbare toohow een tabel ordent records in een database. Elke index heeft een verzameling van documenten dat alle toohello indexschema (veldnamen, gegevenstypen en eigenschappen) voldoen, maar indexen ook aanvullende constructies (suggestiefunctie, score-profielen en opties voor CORS) waarmee andere zoekgedrag opgeven.

U kunt een nieuwe index maken in Azure Search-service met behulp van een HTTP POST of PUT-aanvraag. Hallo-hoofdtekst van Hallo-aanvraag is een JSON-schema dat Hallo index en configuratie-informatie bevat.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

U kunt ook gebruik van PUT en Hallo indexnaam op Hallo URI opgeven. Als het Hallo-index niet bestaat, kunt u deze wordt gemaakt.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Maken van een index bepaalt Hallo-structuur van Hallo documenten opgeslagen en gebruikt in zoekopdrachten. Invullen Hallo index is een afzonderlijke bewerking. Voor deze stap kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/azure/mt183328.aspx) (beschikbaar voor ondersteunde gegevensbronnen) of een [toevoegen, bijwerken of verwijderen van documenten](https://msdn.microsoft.com/library/azure/dn798930.aspx) bewerking. Hallo omgekeerde index wordt gegenereerd wanneer het Hallo-documenten zijn geplaatst.

**Opmerking**: Hallo kunt u het maximum aantal indexen toegestaan hangt af van de prijscategorie. Hallo gratis service kunt u too3 indexen. Standard-service kan 50-indexen per zoekservice. Zie [limieten en beperkingen](http://msdn.microsoft.com/library/azure/dn798934.aspx) voor meer informatie.

**Aanvraag**

HTTPS is vereist voor alle aanvragen van de service. Hallo **Create Index** aanvraag kan worden geconstrueerd met een methode POST of PUT. Wanneer u POST, moet u de naam van een index in de aanvraagtekst Hallo samen met de indexdefinitie schema Hallo opgeven. Met opslag is de indexnaam Hallo deel van Hallo-URL. Als het Hallo-index niet bestaat, wordt deze gemaakt. Als deze al bestaat, is het bijgewerkte toohello nieuwe definitie.

Hallo indexnaam moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten. Hallo rest van de naam van de Hallo kan na het starten van de indexnaam Hallo met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang Hallo streepjes niet opeenvolgende zijn.

Hallo `api-version` is vereist. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor een lijst met beschikbare versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `Content-Type`: Vereist. Stel deze optie te`application/json`
* `api-key`: Vereist. Hallo `api-key` wordt gebruikt voor
* Hallo aanvraag tooyour Search-service worden geverifieerd. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **Create Index** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U kunt beide servicenaam Hallo ophalen en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

<a name="RequestData"></a>
**Syntaxis van de aanvraag hoofdtekst**

Hallo-hoofdtekst van Hallo-aanvraag bevat een schemadefinitie, waaronder Hallo lijst met gegevensvelden binnen de documenten die zal worden opgenomen in deze index, gegevenstypen, kenmerken, evenals een optionele lijst met profielen voor score berekenen gebruikte tooscore die overeenkomt met de documenten op Querytijd.

Houd er rekening mee voor een POST-aanvraag moet u de indexnaam Hallo opgeven in de aanvraagtekst Hallo.

Er kan alleen worden één sleutelveld in Hallo index. Toobe heeft een string-veld. Dit veld wordt de unieke id voor elk document dat is opgeslagen in de index Hallo Hallo.

belangrijkste onderdelen van een index Hallo zijn Hallo volgende:

* `name`
* `fields`die zal worden opgenomen in deze index, zoals naam, gegevenstype en eigenschappen die de toegestane acties op dat veld definiëren.
* `suggesters`gebruikt voor automatisch aanvullen of automatisch aangevulde query's.
* `scoringProfiles`gebruikt voor aangepaste zoekactie score positie. Zie [scoreprofiel profielen toevoegen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` toodefine hoe uw documenten/query's worden onderverdeeld in worden geïndexeerd/doorzoekbare tokens gebruikt. Zie [analyse in Azure Search](https://aka.ms//azsanalysis) voor meer informatie.
* `defaultScoringProfile`toooverwrite hello standaard score berekenen gedrag gebruikt.
* `corsOptions`tooallow cross-origin-query's op uw index.

Hallo-syntaxis voor het Hallo-aanvraaglading structureren is als volgt. Een voorbeeld van een aanvraag wordt aangeboden op verder in dit onderwerp.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Indexkenmerken**

Hallo kunnen volgende kenmerken worden ingesteld bij het maken van een index. Zie voor meer informatie over score berekenen en score berekenen voor profielen [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Stelt Hallo naam van Hallo-veld.

`type`-Stelt Hallo gegevenstype voor Hallo-veld.

`searchable`-Markeert Hallo veld als volledige tekst kunnen zoeken. Dit betekent dat deze ietwat analysis zoals woordafbreking tijdens het indexeren. Als u een `searchable` tooa veldwaarde zoals 'mooi day' intern worden gesplitst in afzonderlijke tokens Hallo 'mooi' en 'dag'. Hierdoor kan de volledige tekst zoekt naar deze voorwaarden. Velden van het type `Edm.String` of `Collection(Edm.String)` zijn `searchable` standaard. Mag geen velden van andere typen `searchable`.

* **Opmerking**: `searchable` velden gebruiken extra ruimte in de index omdat Azure Search, een extra tokens versie van de veldwaarde Hallo voor zoekopdrachten in volledige tekst wordt opgeslagen. Als u wilt dat toosave ruimte uw index en u hoeft niet een veld toobe opgenomen in zoekopdrachten, stelt u `searchable` te`false`.

`filterable`-Hiermee kunt Hallo veld toobe waarnaar wordt verwezen in `$filter` query's. `filterable`verschilt van `searchable` in de verwerking van tekenreeksen. Velden van het type `Edm.String` of `Collection(Edm.String)` die zijn `filterable` niet worden bewerkt woordafbreking, zodat vergelijkingen zijn voor exact overeenkomt met alleen. Bijvoorbeeld, als u dergelijke veld instellen `f` te 'mooi day' `$filter=f eq 'sunny'` wordt geen overeenkomsten gevonden maar `$filter=f eq 'sunny day'` wordt. Alle velden zijn `filterable` standaard.

`sortable`-Standaard Hallo system sorteert resultaten op score, maar in veel ervaringen gebruikers wilt toosort door velden in het Hallo-documenten. Velden van het type `Collection(Edm.String)` kan niet worden `sortable`. Alle andere velden zijn `sortable` standaard.

`facetable`-Doorgaans gebruikt in een weergave van zoekresultaten met treffers per categorie (bijvoorbeeld zoeken naar digitale camera's en Zie treffers op merk, door megapixels, door de prijs, enz.). Deze optie kan niet worden gebruikt met velden van het type `Edm.GeographyPoint`. Alle andere velden zijn `facetable` standaard.

* **Opmerking**: velden van het type `Edm.String` die zijn `filterable`, `sortable`, of `facetable` kan niet groter zijn dan 32 KB lang. Dit is omdat deze velden worden behandeld als een enkel zoekterm en Hallo maximale lengte van een term in Azure Search 32KB is. Als u toostore meer tekst dan deze in een veld één tekenreeks moet, moet u tooexplicitly ingesteld `filterable`, `sortable`, en `facetable` te`false` in de indexdefinitie van de.
* **Opmerking**: als een veld geen van bovenstaande Hallo heeft kenmerken te ingesteld`true` (`searchable`, `filterable`, `sortable`, of`facetable`) Hallo veld effectief is uitgesloten van Hallo omgekeerde index. Deze optie is nuttig voor velden die niet worden gebruikt in query's, maar die nodig zijn in de zoekresultaten. Met uitzondering van dergelijke velden van de index Hallo verbetert de prestaties.

`key`-Markeringen Hallo veld unieke id's voor documenten in Hallo index bevat. Moet precies één veld worden gekozen als Hallo `key` veld en moet zijn van het type `Edm.String`. Sleutelvelden kunnen worden gebruikt toolook documenten rechtstreeks via Hallo [Lookup API](#LookupAPI).

`retrievable`-Instellen of Hallo veld in een zoekresultaat kan worden geretourneerd.  Dit is handig wanneer u toouse een veld (bijvoorbeeld marge) als een filter wilt sorteren of score berekenen mechanisme, maar niet dat Hallo veld toobe zichtbaar toohello gebruiker wilt. Dit kenmerk moet `true` voor `key` velden.

`analyzer`-Naam van Hallo analyzer toouse voor veld Hallo Hallo stelt op zoektijd en indexering tijd. Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx). Deze optie kan alleen worden gebruikt met `searchable` velden en deze kunnen niet worden ingesteld met een `searchAnalyzer` of `indexAnalyzer`.  Zodra Hallo analyzer is gekozen, kan deze niet meer wijzigen voor het Hallo-veld.

`searchAnalyzer`-Stelt Hallo naam van Hallo analyzer gebruikt op het moment van de zoekactie voor Hallo-veld. Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx). Deze optie kan alleen worden gebruikt met `searchable` velden. Deze moet worden ingesteld samen met `indexAnalyzer` en deze kan niet worden ingesteld met Hallo `analyzer` optie. Deze analyzer kan worden bijgewerkt op een bestaand veld.

`indexAnalyzer`-Stelt Hallo naam van Hallo analyzer gebruikt bij indexering voor Hallo-veld. Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx). Deze optie kan alleen worden gebruikt met `searchable` velden. Deze moet worden ingesteld samen met `searchAnalyzer` en deze kan niet worden ingesteld met Hallo `analyzer` optie. Zodra Hallo analyzer is gekozen, kan deze niet meer wijzigen voor het Hallo-veld.

`suggesters`-Stelt Hallo zoekmodus en velden Hallo bron van Hallo-inhoud voor suggesties zijn. Zie [Suggestiefunctie](#Suggesters) voor meer informatie.

`scoringProfiles`-Definieert aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten hoger in de zoekresultaten weergegeven. Scoreprofiel profielen zijn opgebouwd veldgewichten en functies. Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie over Hallo kenmerken in een scoreprofiel gebruikt.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Taalondersteuning**

De doorzoekbare velden ondergaan analyse die het beste omvat vaak woordafbreking, tekst normalisatie en voorwaarden worden uitgefilterd. Standaard doorzoekbare velden in Azure Search worden geanalyseerd met Hallo [Apache Lucene standaard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) die tekst opgesplitst in elementen na de['Segmentering Unicode-tekst'](http://unicode.org/reports/tr29/) regels. Bovendien converteert Hallo standaard analyzer alle tekens tootheir kleine letters formulier. Zowel geïndexeerde documenten en zoektermen doorlopen die Hallo analysis tijdens het indexeren en de verwerking van query's.

Azure Search biedt ondersteuning voor verschillende talen. Elke taal is vereist voor een niet-standaard tekst analyzer die accounts voor kenmerken van een bepaalde taal. Azure Search biedt twee typen analyzers:

* 35 analyzers Lucene back-up.
* 50 analyzers bedrijfseigen Microsoft natuurlijke taal verwerken van de technologie die wordt gebruikt in Office en Bing back-up.

Sommige ontwikkelaars liever Hallo meer vertrouwde eenvoudige, open source-oplossing van Lucene. Lucene analyzers sneller zijn, maar Hallo Microsoft analyzers hebben geavanceerde mogelijkheden, zoals Lemmata, word decompounding (in talen zoals Duits, Deens, Nederlands, Zweeds, Noors, Ests, voltooien, Hongaars, Slowaaks) en entiteit herkenning (URL 's e-mailberichten, datums, getallen). Indien mogelijk moet u vergelijkingen van beide Hallo Microsoft en Lucene analyzers toodecide-welke is beter geschikt uitvoeren.

***Hoe ze zich verhouden***

Hallo Lucene analyzer voor Engels wordt standaard analyzer Hallo uitgebreid. Deze bezittelijke voornaamwoorden (afsluitende van) met woorden verwijdert, is van toepassing als gevolg conform [Porter afleiding algoritme](http://tartarus.org/~martin/PorterStemmer/), en verwijdert u Engels [stopwoorden](http://en.wikipedia.org/wiki/Stop_words).

Ter vergelijking voert Hallo Microsoft analyzer Lemmata in plaats van de gegevens als gevolg. Dit betekent dat deze kan omgaan met verbogen en onregelmatige word formulieren veel beter wat resulteert in meer relevante zoekresultaten (controle module 7 van [Azure Search MVA presentatie](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) voor meer informatie).

Indexering met Microsoft analyzers is gemiddeld twee toothree keer langzamer dan de Lucene-equivalenten, afhankelijk van het Hallo-taal. Prestaties van de zoekopdracht moet niet aanzienlijk beïnvloed voor de gemiddelde grootte query's.

***Configuratie***

Voor elk veld in de indexdefinitie hello, kunt u Hallo instellen `analyzer` tooan analyzer eigenschapsnaam die welke taal en de leverancier aangeeft. Hallo dezelfde analyzer worden toegepast wanneer het indexeren en het zoeken voor dat veld.
U kunt bijvoorbeeld afzonderlijke velden voor Engels, Frans en Spaans hotel beschrijvingen die bestaan naast elkaar in Hallo hebben dezelfde index. Gebruik Hallo ['searchFields' queryparameter](#SearchQueryParameters) toospecify welke toosearch taalspecifieke veld tegen in uw query's. U kunt query voorbeelden waarin Hallo bekijken `analyzer` eigenschap in [documenten zoeken](#SearchDocs). 

***Lijst met Analyzer***

Hieronder vindt u een lijst van ondersteunde talen samen met de namen van Lucene en Microsoft analyzer Hallo.

<table style="font-size:12">
    <tr>
        <th>Taal</th>
        <th>De naam van de Microsoft-analyzer</th>
        <th>Lucene analyzer naam</th>
    </tr>
    <tr>
        <td>Arabisch</td>
        <td>ar.Microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armeens</td>
        <td></td>
        <td>Hy.lucene</td>
      </tr>
    <tr>
        <td>Bengaals</td>
        <td>bn.Microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Baskisch</td>
        <td></td>
        <td>EU.lucene</td>
    </tr>
      <tr>
         <td>Bulgaars</td>
        <td>BG.Microsoft</td>
        <td>BG.lucene</td>
      </tr>
      <tr>
        <td>Catalaans</td>
        <td>CA.Microsoft</td>
        <td>CA.lucene</td>          
      </tr>
    <tr>
        <td>Vereenvoudigd Chinees</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Traditioneel Chinees</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Kroatisch</td>
        <td>HR.Microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Tsjechisch</td>
        <td>CS.Microsoft</td>
        <td>CS.lucene</td>        
    </tr>    
    <tr>
        <td>Deens</td>
        <td>da.Microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Nederlands</td>
        <td>nl.Microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>Nederlands</td>        
        <td>en.Microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estisch</td>
        <td>et.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Fins</td>
        <td>Fi.Microsoft</td>
        <td>Fi.lucene</td>        
    </tr>    
    <tr>
        <td>Frans</td>
        <td>FR.Microsoft</td>
        <td>FR.lucene</td>        
    </tr>
    <tr>
        <td>Galicisch</td>
        <td></td>
        <td>GL.lucene</td>        
      </tr>
    <tr>
        <td>Duits</td>
        <td>de.Microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Grieks</td>
        <td>El.Microsoft</td>
        <td>El.lucene</td>        
    </tr>
    <tr>
        <td>Gujarati</td>
        <td>Gu.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hebreeuws</td>
        <td>He.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>Hi.Microsoft</td>
        <td>Hi.lucene</td>        
    </tr>
    <tr>
        <td>Hongaars</td>        
        <td>Hu.Microsoft</td>
        <td>Hu.lucene</td>
    </tr>
    <tr>
        <td>IJslands</td>
        <td>is.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonesisch (Bahasa)</td>
        <td>ID.Microsoft</td>
        <td>ID.lucene</td>        
    </tr>
    <tr>
        <td>Iers</td>
        <td></td>
          <td>Ga.lucene</td>
    </tr>
    <tr>
        <td>Italiaans</td>
        <td>IT.Microsoft</td>
        <td>IT.lucene</td>        
    </tr>
    <tr>
        <td>Japans</td>
        <td>Ja.Microsoft</td>
        <td>Ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>Ka.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Koreaans</td>
        <td>Ko.Microsoft</td>
        <td>Ko.lucene</td>
    </tr>
    <tr>
        <td>Lets</td>        
        <td>LV.Microsoft</td>
        <td>LV.lucene</td>    
    </tr>
    <tr>
        <td>Litouws</td>
        <td>lt.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malajalam</td>
        <td>ml.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Maleis (Latijns)</td>
        <td>MS.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>Mr.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Noors</td>
        <td>NB.Microsoft</td>
        <td>No.lucene</td>        
    </tr>
      <tr>
        <td>Perzisch</td>
        <td></td>
        <td>FA.lucene</td>        
      </tr>
    <tr>
        <td>Pools</td>
        <td>PL.Microsoft</td>
        <td>PL.lucene</td>        
    </tr>
    <tr>
        <td>Portugees (Brazilië)</td>
        <td>pt Br.microsoft</td>
        <td>pt Br.lucene</td>        
    </tr>
    <tr>
        <td>Portugees (Portugal)</td>
        <td>pt Pt.microsoft</td>        
        <td>pt Pt.lucene</td>
    </tr>
    <tr>
        <td>Punjabi</td>
        <td>Pa.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Roemeens</td>
        <td>ro.Microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Russisch</td>
        <td>RU.Microsoft</td>
        <td>RU.lucene</td>    
    </tr>
    <tr>
        <td>Servisch (Cyrillisch)</td>
        <td>SR-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Servisch (Latijns)</td>
        <td>SR-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slowaaks</td>
        <td>SK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Sloveens</td>
        <td>SL.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Spaans</td>
        <td>ES.Microsoft</td>
        <td>ES.lucene</td>
    </tr>
    <tr>
        <td>Zweeds</td>
        <td>SV.Microsoft</td>
        <td>SV.lucene</td>
    </tr>

    <tr>
        <td>Tamil</td>
        <td>TA.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu</td>
        <td>te.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Thais</td>
        <td>TH.Microsoft</td>
        <td>TH.lucene</td>
    </tr>
    <tr>
        <td>Turks</td>
        <td>TR.Microsoft</td>
        <td>TR.lucene</td>        
    </tr>
    <tr>
        <td>Oekraïens</td>
        <td>UK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>Your.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamees</td>
        <td>VI.Microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Bovendien biedt Azure Search taal networkdirect analyzer configuraties</td>
    <tr>
        <td>Standaard ASCII Folding</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Unicode-tekst segmentering (standaard Tokenizer)</li>
            <li>Opvouwbaar filter ASCII - converteert Unicode-tekens die geen deel uitmaken toohello set eerst 127 ASCII-tekens in de ASCII-equivalenten. Dit is handig voor het verwijderen van diakritische tekens.</li>
        </ul>
        </td>
    </tr>
</table>

Alle analyzers met namen van aantekeningen voorzien met <i>lucene</i> worden van stroom voorzien door [van Apache Lucene taalanalyse](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Meer informatie over Hallo ASCII vouwen filter vindt [hier](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Suggesties**

Een `suggester` wordt gedefinieerd welke velden in een index zijn gebruikte toosupport automatisch aanvullen in zoekopdrachten. Doorgaans gedeeltelijke zoekreeksen toohello worden verzonden [suggesties API](#Suggestions) terwijl Hallo gebruiker een zoekquery typen is en het Hallo-API een set met voorgestelde zinnen retourneert. Een suggestie die u in Hallo index definieert bepaalt welke velden gebruikte toobuild Hallo automatisch aangevulde zoektermen. Zie [Suggestiefunctie](#Suggesters) voor configuratie-informatie.

**Scoreprofielen**

Een `scoringProfile` aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten in zoekresultaten Hallo hoger weergegeven definieert. Scoreprofiel profielen zijn opgebouwd veldgewichten en functies. toouse ze, geeft u een profiel met de naam in de queryreeks Hallo.

Een standaard score berekenen profiel werkt achter de schermen-toocompute Hallo een score zoeken voor elk item in een resultatenset. U kunt Hallo interne, naamloze scoreprofiel gebruiken. U kunt ook instellen `defaultScoringProfile` toouse een aangepast profiel als Hallo standaard, wanneer u een aangepast profiel niet is opgegeven in de queryreeks Hallo aangeroepen.

Zie [tooa search-index (Azure Search Service REST-API) toevoegen score berekenen profielen](search-api-scoring-profiles-2015-02-28-preview.md) voor meer informatie.

**CORS-opties**

Client-side Javascript kan API's standaard niet aanroepen omdat Hallo browser voorkomt u alle cross-origin-aanvragen dat. Inschakelen van CORS (Cross-Origin Resource Sharing) met instelling Hallo `corsOptions` kenmerk tooallow cross-origin-query's tooyour index. Houd er rekening mee dat alleen query API-ondersteuning CORS uit veiligheidsoverwegingen. Hallo volgend opties kan worden ingesteld voor CORS:

* `allowedOrigins`(vereist): dit is een lijst met oorsprongen op waarvoor toegang tooyour index wordt verleend. Dit betekent dat een Javascript-code opgehaald uit deze oorsprongen zijn toegestaan tooquery uw index (ervan uitgaande dat het juiste Hallo-API-sleutel biedt). Elke oorsprong heeft meestal Hallo vorm `protocol://fully-qualified-domain-name:port` Hoewel Hallo poort vaak wordt weggelaten. Zie [in dit artikel](http://go.microsoft.com/fwlink/?LinkId=330822) voor meer informatie.
  * Als u tooallow toegang tooall oorsprongen wilt, omvatten `*` als één item in Hallo `allowedOrigins` matrix. Houd er rekening mee dat **dit wordt niet aanbevolen beveiligingsprocedure voor productie search-services.** Dit kan echter nuttig zijn voor ontwikkeling of foutopsporing zijn.
* `maxAgeInSeconds`(optioneel): Browsers gebruiken deze waarde toodetermine Hallo duur (in seconden) toocache CORS voorbereidende antwoorden. Dit moet een niet-negatief geheel getal zijn. Hallo groter deze waarde is, Hallo betere prestaties, maar Hallo langer die het duurt voor CORS-beleid wijzigingen tootake effect. Als deze niet is ingesteld, wordt een standaardduur van 5 minuten gebruikt.

<a name="CreateUpdateIndexExample"></a>
**Voorbeeld van de aanvraag hoofdtekst**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Antwoord**

Aanvraag is gelukt: '201 gemaakt'.

Standaard bevat antwoordtekst Hallo Hallo JSON voor Hallo indexdefinitie die is gemaakt. Als hello `Prefer` aanvraagheader is te ingesteld`return=minimal`, Hallo antwoordtekst leeg en Hallo geslaagd status code ' 204 geen inhoud ' in plaats van '201 gemaakt'. Dit geldt ongeacht of gebruikte toocreate Hallo index plaatsen of POST was.

**Opmerkingen**

Op dit moment is er beperkte ondersteuning voor index schema-updates. Alle schema-updates die opnieuw worden geïndexeerd moeten zoals het wijzigen van veldtypen worden momenteel niet ondersteund. Hoewel u bestaande velden kunnen niet worden gewijzigd of verwijderd, kan nieuwe velden kunnen tooan bestaande index op elk gewenst moment worden toegevoegd. Wanneer u een nieuw veld toevoegt, hebben alle documenten in index Hallo automatisch een null-waarde voor dat veld. Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten toohello index zijn toegevoegd.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Suggesties
Hallo suggesties functie in Azure Search is een type-ahead of automatisch aanvullen query-functie, met een lijst van mogelijke zoektermen in het antwoord toopartial tekenreeks invoer in een zoekvak ingevoerd. U vast opgevallen Querysuggesties bij gebruik van zoekmachines commerciële web: '.NET' te typen Bing genereert een overzicht van voorwaarden voor '.NET 4.5 uitvoeren ', '.NET Framework 3.5", enzovoort. Wanneer u Hallo Search service REST-API, vereist suggesties implementeren in een aangepaste Azure Search-toepassing hello volgende:

* Suggesties inschakelen door het toevoegen van een **suggestie** bouw in uw index, geeft de naam hello, zoekmodus en een lijst met velden waarvoor automatisch aangevulde wordt aangeroepen. Bijvoorbeeld, als u 'stad' als een bronveld, te typen gedeeltelijke zoektekenreeks 'Sea' leidt ertoe dat "Seattle" opgeeft, 'Strand' en 'Seatac' (alle drie zijn de namen van de werkelijke stad) aangeboden tot als query suggesties toohello gebruiker.
* Suggesties aanroepen door de aanroepende Hallo [suggesties API](#Suggestions) in uw toepassingscode. Gedeeltelijke zoekreeksen worden doorgaans toohello service verzonden tijdens het Hallo-gebruiker is een zoekopdracht typen en deze API retourneert een set met voorgestelde zinnen.

Dit artikel wordt uitgelegd hoe tooconfigure een **suggestie**. Bekijk ook Hallo [suggesties API](#Suggestions) voor meer informatie over hoe een suggestie wordt gebruikt.

**Gebruik**

`Suggesters`in Hallo index worden gemaakt en werken het beste als gebruikt toosuggest specifieke documenten in plaats van losse voorwaarden of zinnen. Hallo best candidate velden zijn titels, namen en andere relatief korte zinnen die een item kunnen identificeren. Minder effectief zijn herhalende velden, zoals de categorieën en tags, of zeer lange velden zoals beschrijvingen of opmerkingen velden.

Als onderdeel van de indexdefinitie hello, kunt u een één suggestie toohello toevoegen `suggesters` verzameling. Eigenschappen die, een suggestie bepalen zijn Hallo volgende:

* `name`: Hallo-naam van Hallo suggestie. U Hallo-naam van Hallo suggestie gebruiken bij het aanroepen van Hallo `suggest` API.
* `searchMode`: Hallo toosearch gebruikte strategie voor candidate zinnen. Hallo modus worden alleen ondersteund op dit moment is `analyzingInfixMatching`, flexibele overeenkomende woordgroepen aan Hallo begin of in het midden van zinnen Hallo uitvoert.
* `sourceFields`: Een lijst met een of meer velden Hallo bron van Hallo-inhoud voor suggesties zijn. Alleen velden van het type `Edm.String` en `Collection(Edm.String)` mogelijk bronnen voor suggesties. Alleen de velden die een aangepaste taalanalyse ingesteld niet kunnen worden gebruikt.

**Suggestie voorbeeld**

Een suggestie maakt deel uit van Hallo index. Er kan slechts één suggestie bestaan in Hallo `suggesters` verzameling in de huidige versie Hallo naast Hallo verzameling velden en `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Als u Hallo openbare preview-versie van Azure Search gebruikt `suggesters` wordt vervangen door een oudere Boole-eigenschap (`"suggestions": false`) die alleen voorvoegsel suggesties voor korte tekenreeksen (3-25 tekens) wordt ondersteund. De vervanging ervan `suggesters`, ondersteunt infix overeenkomende waarmee wordt gezocht naar overeenkomende voorwaarden aan Hallo begin of in het midden van de Hallo van veldinhoud, met betere tolerantie voor fouten in zoekreeksen. Vanaf Hallo algemeen beschikbaar release, is dit nu Hallo alleen implementatie van Hallo suggesties API. Hallo oudere `suggestions` eigenschap die is geïntroduceerd in `api-version=2014-07-31-Preview` toowork blijft in deze versie, maar is niet operationeel in Hallo `2015-02-28` of latere versies van Azure Search.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Index bijwerken
U kunt een bestaande index in Azure Search met behulp van een HTTP PUT-aanvraag bijwerken. Updates kunnen het toevoegen van nieuwe velden toohello bestaand schema, CORS-opties wijzigen en wijzigen, scoreprofiel profielen bevatten. Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie. U opgeven Hallo naam van Hallo index tooupdate op Hallo aanvraag-URI:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Belangrijk:** ondersteuning voor index schema-updates beperkt toooperations die Hallo search-index opnieuw opbouwen niet nodig is. Alle schema-updates die opnieuw worden geïndexeerd moeten, zoals het wijzigen van veldtypen, worden momenteel niet ondersteund. Nieuwe velden kunnen op elk gewenst moment worden toegevoegd, hoewel bestaande velden kunnen niet worden gewijzigd of verwijderd. Hallo geldt te`suggesters`. Nieuwe velden kunnen worden toegevoegd tooa suggestie op Hallo Hallo tijdvelden worden toegevoegd, maar velden kunnen niet worden verwijderd uit `suggesters` en bestaande velden kunnen niet te worden toegevoegd`suggesters`.

Wanneer u een nieuw veld tooan index toevoegt, hebben alle documenten in index Hallo automatisch een null-waarde voor dat veld. Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten toohello index zijn toegevoegd.

**Aanvraag**

HTTPS is vereist voor alle aanvragen van de service. Hallo **Index bijwerken** aanvraag is opgesteld met HTTP PUT. Met opslag is de indexnaam Hallo deel van Hallo-URL. Als het Hallo-index niet bestaat, wordt deze gemaakt. Als al Hallo index bestaat, is het bijgewerkte toohello nieuwe definitie.

Hallo indexnaam moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten. Hallo rest van de naam van de Hallo kan na het starten van de indexnaam Hallo met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang Hallo streepjes niet opeenvolgende zijn.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `Content-Type`: Vereist. Stel deze optie te`application/json`
* `api-key`: Vereist. Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **Index bijwerken** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Syntaxis van de aanvraag hoofdtekst**

Bij het bijwerken van een bestaande index Hallo hoofdtekst vergezeld gaan van de oorspronkelijke schemadefinitie Hallo plus Hallo nieuwe velden die u wilt toevoegen, evenals Hallo gewijzigd scoreprofiel profielen, suggestiefunctie en CORS-opties, indien van toepassing. Als u scoreprofiel Hallo-profielen en CORS-opties niet wijzigt, moet u opnemen Hallo originele wanneer Hallo index is gemaakt. Hallo best patroon toouse voor updates is over het algemeen tooretrieve Hallo indexdefinitie met een GET, wijzigen en vervolgens bijwerken met PUT.

Hallo schemasyntaxis gebruikt een index is hier gereproduceerd toocreate voor uw gemak. Zie [Create Index](#CreateIndex) voor meer informatie.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Antwoord**

Aanvraag is gelukt: ' 204 geen inhoud '.

Standaard wordt Hallo antwoordtekst niet leeg zijn. Echter, als hello `Prefer` aanvraagheader is te ingesteld`return=representation`, Hallo antwoordtekst bevat Hallo JSON voor Hallo indexdefinitie die is bijgewerkt. In dit geval statuscode van Hallo geslaagd zijn ' 200 OK '.

**Definitie van de index met aangepaste analyzers bijwerken**

Als er een analyzer, een tokenizer, een token filter of een char-filter is gedefinieerd, kan niet worden gewijzigd. Nieuwe te kunnen alleen worden toegevoegd tooan bestaande index als hello `allowIndexDowntime` tootrue-vlag is ingesteld in Hallo index updateaanvraag: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Opmerking dat deze bewerking uw index offline wordt geplaatst voor ten minste een paar seconden, waardoor uw indexeren en query-toofail aanvragen. Beschikbaarheid en wegschrijven van Hallo-index kan worden gehinderd minuten nadat het Hallo-index wordt bijgewerkt of langer voor zeer grote indexen.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Lijst met indexen
Hallo **lijst indexen** bewerking retourneert een lijst met Hallo indexen momenteel in uw Azure Search-service.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Aanvraag**

HTTPS is vereist voor alle aanvragen van de service. Hallo **lijst indexen** aanvraag kan worden opgesteld met Hallo GET-methode.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Vereist. Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **lijst indexen** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hier volgt een voorbeeld-antwoordtekst:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Houd er rekening mee dat u kunt filteren, antwoord Hallo omlaag toojust Hallo eigenschappen die u geïnteresseerd bent in. Bijvoorbeeld: als u alleen een lijst met indexnamen wilt, Hallo OData gebruiken `$select` query-optie:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

In dit geval zou Hallo reactie van Hallo bovenstaande voorbeeld als volgt uitzien:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Dit is een nuttig toosave bandbreedte als er een groot aantal indexen in uw zoekservice.

<a name="GetIndex"></a>

## <a name="get-index"></a>Index ophalen
Hallo **Index ophalen** bewerking Hallo indexdefinitie opgehaald uit Azure Search.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **Index ophalen** aanvraag kan worden opgesteld met Hallo GET-methode.

Hallo [naam van de index] in Hallo aanvraag-URI geeft aan welke tooreturn index uit Hallo indexverzameling.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **Index ophalen** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Zie Hallo voorbeeld JSON in [maken en bijwerken van een Index](#CreateUpdateIndexExample) voor een voorbeeld van Hallo antwoord nettolading.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Index verwijderen
Hallo **Index verwijderen** bewerking verwijdert u een index en de bijbehorende documentatie van uw Azure Search-service. U krijgt de indexnaam Hallo van Hallo servicedashboard in hello Azure-portal of van Hallo API. Zie [lijst indexen](#ListIndexes) voor meer informatie.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **Index verwijderen** aanvraag kan worden opgesteld met Hallo DELETE-methode.

Hallo [naam van de index] in Hallo aanvraag-URI geeft aan welke toodelete index uit Hallo indexverzameling.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Vereist. Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, unieke tooyour service-URL. Hallo **Index verwijderen** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 204 geen inhoud wordt geretourneerd voor een geslaagde reactie.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Indexstatistieken opvragen
Hallo **statistieken voor Index ophalen** bewerking retourneert van Azure Search een aantal documenten voor de huidige index Hallo plus opslaggebruik.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Statistieken over document aantal en de opslaggrootte worden elke paar minuten, niet in realtime verzameld. Hallo-statistieken die zijn geretourneerd door deze API kan daarom niet overeen met wijzigingen die zijn veroorzaakt door een recente indexbewerkingen.
> 
> 

**Aanvraag**

HTTPS is vereist voor alle services aanvragen. Hallo **statistieken voor Index ophalen** aanvraag kan worden opgesteld met Hallo GET-methode.

Hallo [naam van de index] in Hallo aanvraag-URI vertelt Hallo service tooreturn indexstatistieken voor de opgegeven index Hallo.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **ophalen indexstatistieken** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hallo-antwoordtekst heeft Hallo volgende indeling:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Test Analyzer
Hallo **analyseren API** ziet u hoe een analyzer tekst opgesplitst in tokens.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Aanvraag**

HTTPS is vereist voor alle services aanvragen. Hallo **analyseren API** aanvraag kan worden opgesteld met Hallo POST-methode.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **analyseren API** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).

U moet ook de indexnaam Hallo en Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

of

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Hallo `analyzer_name`, `tokenizer_name`, `token_filter_name` en `char_filter_name` toobe geldige namen van de vooraf gedefinieerde of aangepaste analyzers, tokenizers, token filters en char filters voor Hallo index nodig. Zie informatie over het proces van lexicale analyse Hallo toolearn [analyse in Azure Search](https://aka.ms/azsanalysis).

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hallo-antwoordtekst heeft Hallo volgende indeling:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**API-voorbeeld analyseren**

**Aanvraag**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Antwoord**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Document bewerkingen
In Azure Search is een index wordt opgeslagen in de cloud Hallo en ingevuld met JSON-documenten toohello service te uploaden. Alle Hallo-documenten die u uploadt omvatten Hallo corpus van uw zoekgegevens. Documenten bevatten velden, zijn sommige van deze in de zoektermen tokenized als ze worden geüpload. Hallo `/docs` URL-segment in hello Azure Search API vertegenwoordigt Hallo-verzameling van documenten in een index. Alle bewerkingen die worden uitgevoerd op de verzameling Hallo zoals uploaden, samenvoegen, verwijderen of documenten opvragen plaatsvinden in Hallo context van een enkele index geval Hallo-URL's voor deze bewerkingen wordt altijd gestart met `/indexes/[index name]/docs` voor een naam voor de gegeven index.

Uw toepassingscode moet ofwel genereren voor JSON-documenten tooupload tooAzure zoeken of kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/dn946891.aspx) tooload documenten als gegevensbron hello Azure SQL Database of Azure Cosmos DB. Indexen worden gewoonlijk ingevuld uit een enkele gegevensset die u opgeeft.

U moet plannen op beschikt over een document voor elk item dat u wilt dat toosearch. Een toepassing van de verhuur film wellicht een document per film, een toepassing via wellicht een document per SKU, een toepassing online cursusprogramma wellicht een document per loop, een bedrijf wellicht een document voor elk academic papier in hun opslagplaats, enzovoort.

Documenten bestaan uit een of meer velden. Velden kunnen bevatten tekst die wordt door Azure Search in zoektermen tokenized, evenals niet getokeniseerd of niet-tekstwaarden plaatsen die kunnen worden gebruikt in filters of scoreprofiel profielen. Hallo worden namen, gegevenstypen en zoekfuncties ondersteund voor elk veld bepaald door Hallo Indexeer schema. Een van de velden Hallo in elke indexschema dat moet worden aangemerkt als een ID en elk document moet een waarde voor Hallo-ID-veld dat een unieke identificatie van dat document in Hallo index hebben. Alle andere documentvelden zijn optioneel en tooa null-waarde wordt teruggezet of niet opgegeven. Houd er rekening mee dat null-waarden geen ruimte vrijmaken in Hallo search-index hebben.

Als u documenten uploaden, moet hebt u al Hallo index gemaakt op Hallo-service. Zie [Create Index](#CreateIndex) voor meer informatie over deze eerste stap.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Toevoegen, bijwerken of verwijderen van documenten
U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST. Batchverwerking van documenten (too1000 documenten per batch) of 16 MB per batch wordt aanbevolen voor grote aantallen van updates.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Aanvraag**

HTTPS is vereist voor alle aanvragen van de service. U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST.

Hallo-aanvraag URI bevat [naam van de index] opgeven welke index toopost documenten. U kunt alleen documenten tooone index boeken tegelijk.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `Content-Type`: Vereist. Stel deze optie te`application/json`
* `api-key`: Vereist. Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **documenten toevoegen** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Hallo-hoofdtekst van Hallo-aanvraag bevat een of meer documenten toobe geïndexeerd. Documenten worden aangeduid met een unieke sleutel. Elk document dat is gekoppeld aan een actie: uploaden, samenvoegen, mergeOrUpload of verwijderen. Het uploaden van aanvragen mag Hallo documentgegevens bevatten als een set van sleutel-waardeparen.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Document sleutels mogen alleen letters, cijfers, streepjes ('-'), onderstrepingstekens ('_') en gelijk tekens ('='). Zie voor meer informatie [naamgevingsregels](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Documentacties**

* `upload`: Er is een upload-actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat. Houd er rekening mee dat alle velden in geval van Hallo-update worden vervangen.
* `merge`: Samenvoegen updates een bestaand document met het Hallo opgegeven velden. Als Hallo document niet bestaat, mislukt de Hallo samenvoegen. Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document. ook velden van het type `Collection(Edm.String)`. Bijvoorbeeld, als hello document bevat een veld 'labels' met de waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor 'tags' hello uiteindelijke waarde van veld Hallo 'tags' worden `["economy", "pool"]`. Het **niet** worden `["budget", "economy", "pool"]`.
* `mergeOrUpload`: gedraagt zich als `merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat. Als Hallo document niet bestaat nog, gedraagt zich als `upload` met een nieuw document.
* `delete`: Het opgegeven document Hallo verwijdert verwijderen uit Hallo index. Houd er rekening mee dat alle velden u opgeeft in een `delete` bewerking dan Hallo sleutelveld worden genegeerd. Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `merge` in plaats daarvan en stelt Hallo veld expliciet in te`null`.

**Antwoord**

Statuscode 200 wordt (OK) geretourneerd voor een geslaagd antwoord, wat betekent dat alle items zijn geïndexeerd. Dit wordt aangegeven door Hallo `status` eigenschap wordt ingesteld tootrue voor alle items, evenals Hallo `statusCode` eigenschap wordt ingesteld tooeither 201 (voor recent geüploade documenten) of 200 (voor samengevoegde of verwijderde documenten):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Statuscode 207 (meerdere Status) wordt geretourneerd wanneer ten minste één item is niet geïndexeerd. Items die niet zijn geïndexeerd hebben Hallo `status` veld toofalse ingesteld. Hallo `errorMessage` en `statusCode` eigenschappen Hallo reden voor fout indexeren hello wordt aangeven:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Hallo volgende tabel wordt uitgelegd Hallo verschillende per document statuscodes die kunnen worden geretourneerd in antwoord Hallo. Houd er rekening mee dat sommige duiden op problemen met het Hallo-aanvraag zelf, terwijl anderen tijdelijke fouten geven. Hallo laatstgenoemde die probeert u het opnieuw na een vertraging.

<table style="font-size:12">
    <tr>
        <th>Statuscode</th>
        <th>Betekenis</th>
        <th>Herstelbare</th>
        <th>Opmerkingen</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Document is gewijzigd of verwijderd.</td>
        <td>N.v.t.</td>
        <td>Verwijderbewerkingen zijn <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>. Dat wil zeggen, zelfs als de documentsleutel van een niet in de index hello bestaat, leidt probeert een delete-bewerking met die sleutel tot een 200-statuscode.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Document is gemaakt.</td>
        <td>N.v.t.</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Er is een fout opgetreden in Hallo-document dat waardoor deze niet kan worden geïndexeerd.</td>
        <td>Nee</td>
        <td>Hallo foutbericht weergegeven in het antwoord Hallo wordt aangegeven wat is er iets mis met Hallo-document.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>Hallo-document kan niet worden samengevoegd omdat Hallo opgegeven sleutel niet in het Hallo-index bestaat.</td>
        <td>Nee</td>
        <td>Deze fout treedt niet op bij uploads omdat ze nieuwe documenten maken en dit niet voor verwijderingen gebeurt omdat ze <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Een versieconflict gevonden tijdens een poging de tooindex een document.</td>
        <td>Ja</td>
        <td>Dit kan gebeuren wanneer u probeert tooindex Hallo dezelfde meer dan één keer gelijktijdig-document.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>Hallo index is tijdelijk niet beschikbaar omdat deze is bijgewerkt met de Hallo 'allowIndexDowntime' vlag set too'true'.</td>
        <td>Ja</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Uw search-service is tijdelijk niet beschikbaar is, mogelijk vanwege tooheavy laden.</td>
        <td>Ja</td>
        <td>Uw code moet worden gewacht voordat opnieuw uit te voeren in dit geval of u het risico verlenging van de Hallo-service niet beschikbaar zijn.</td>
    </tr>
</table> 

**Opmerking**: als uw clientcode wordt vaak een 207 antwoord tegenkomt, een mogelijke reden is dat Hallo system belast wordt. U kunt dit controleren door te controleren Hallo `statusCode` eigenschap voor 503. Als dit Hallo geval is, wordt aangeraden ***beperking indexering aanvragen***. Anders als indexering verkeer niet subside, Hallo system kan worden gestart voor het weigeren van alle aanvragen met 503-fouten.

Statuscode 429 geeft aan dat u het quotum van Hallo aantal documenten per index hebt overschreden. Een nieuwe index maken of een upgrade uit voor hogere Capaciteitslimieten.

**Voorbeeld:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Documenten zoeken
Een **Search** bewerking als een GET of POST-aanvraag wordt uitgegeven en parameters waarmee Hallo criteria voor het selecteren van de overeenkomende documenten bevat.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Wanneer toouse BOEKT in plaats van ophalen**

Bij het gebruik van HTTP GET toocall hello **Search** API, moet u toobe Houd er rekening mee dat Hallo Hallo aanvraag-URL kan niet langer zijn dan 8 KB. Dit is meestal genoeg voor de meeste toepassingen. Sommige toepassingen produceren echter zeer grote query's of OData-filterexpressies. Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters en query's dan GET. Met POST, Hallo aantal termen of componenten in een query is Hallo factor, niet Hallo grootte van Hallo onbewerkte query omdat Hallo aanvraag groottelimiet voor POST ongeveer 16 MB is beperken.

> [!NOTE]
> Hoewel de maximale grootte Hallo POST-aanvraag is te lang., zoekquery's en filterexpressies mogen niet willekeurig complexe. Zie [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) en [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over zoekopdracht query en filter complexiteit beperkingen.
> 
> 

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **Search** aanvraag kan worden opgesteld met Hallo GET of POST-methoden.

Hallo aanvraag-URI geeft aan welke tooquery index, voor alle documenten die overeenkomen met Hallo-parameters. Parameters zijn opgegeven in de queryreeks Hallo in geval van GET-aanvragen hello en in Hallo aanvraag hoofdtekst in geval van Hallo van POST-aanvragen.

Als een best practice bij het maken van GET-aanvragen te onthouden[URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke parameters bij het aanroepen van REST-API rechtstreeks Hallo-query. Voor **Search** bewerkingen, dit omvat:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

URL-codering wordt alleen aanbevolen voor Hallo hierboven queryparameters. Als u per ongeluk URL coderen hello volledige queryreeks (alles na Hallo?), worden aanvragen wordt verbroken.

Zo is de URL-codering ook alleen nodig bij het aanroepen van Hallo direct met REST-API aan. Er is geen URL-codering is nodig bij het aanroepen van **zoeken** POST, met of bij het gebruik van Hallo [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die het URL-codering voor u verwerkt.

<a name="SearchQueryParameters"></a>
**Query-Parameters**

**Search** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert. U opgeven dat deze parameters in Hallo URL querytekenreeks bij het aanroepen van **Search** via GET en als JSON-eigenschappen in de aanvraagtekst Hallo bij het aanroepen van **Search** via POST. Hallo-syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST. Deze verschillen worden vermeld als die van toepassing zijn hieronder:

`search=[string]`(optioneel) - Hallo toosearch voor tekst. Alle `searchable` velden worden doorzocht door standaard tenzij `searchFields` is opgegeven. Bij het zoeken naar `searchable` velden, Hallo zoektekst zelf tokenized, zodat meerdere voorwaarden kunnen worden gescheiden door spaties bevatten (bijvoorbeeld: `search=hello world`). toomatch gebruik van elke termijn `*` (dit kan handig zijn voor Booleaanse filterquery's). Als deze parameter wordt weggelaten heeft hetzelfde effect als de instelling voor het te Hallo`*`. Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) voor foutopsporingsgegevens op Hallo zoeksyntaxis.

* **Opmerking**: Hallo resultaten kunnen soms verrassend zijn bij het opvragen via `searchable` velden. Hallo tokenizer bevat logica toohandle gevallen algemene tooEnglish tekst zoals apostrof, komma's in cijfers, enzovoort. Bijvoorbeeld: `search=123,456` komt overeen met een enkele term 123,456 in plaats van afzonderlijke termen Hallo 123 en 456, omdat komma's worden gebruikt als duizend scheidingstekens voor grote aantallen in het Engels. Daarom wordt u aangeraden witruimte in plaats van leestekens tooseparate voorwaarden in Hallo `search` parameter.

`searchMode=any|all`(optioneel, standaard te`any`) - of één of alle Hallo zoektermen in volgorde toocount Hallo document als een overeenkomst moeten overeenkomen.

`searchFields=[string]`(optioneel) - Hallo lijst met door komma's gescheiden veld namen toosearch voor Hallo opgegeven tekst. Doelvelden moeten worden gemarkeerd als `searchable`.

`queryType=simple|full`(optioneel, standaard te`simple`): wanneer set te 'eenvoudige' zoektekst wordt geïnterpreteerd met behulp van een eenvoudige querytaal waarmee symbolen zoals +, * en ' '. Query's worden geëvalueerd in de doorzoekbare velden (of velden die zijn aangegeven in `searchFields`) in elk document standaard. Wanneer het querytype hello te is ingesteld`full` zoektekst met behulp van Hallo Lucene-querytaal waarmee veld-specifieke en gewogen zoekopdrachten wordt geïnterpreteerd. Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) en [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) voor foutopsporingsgegevens op Hallo zoeken syntaxis. 

> [!NOTE]
> Zoeken in Hallo Lucene querytaal wordt niet ondersteund voor $filter dat vergelijkbare functionaliteit biedt liggen.
> 
> 

`moreLikeThis=[key]`(optioneel) **Belangrijk:** deze functie is alleen beschikbaar in `2015-02-28-Preview`. Deze optie kan niet worden gebruikt in een query met Hallo tekst zoekparameter `search=[string]`. Hallo `moreLikeThis` parameter vindt documenten die vergelijkbaar toohello document dat is opgegeven door Hallo documentsleutel zijn. Wanneer een search-aanvraag wordt gedaan met `moreLikeThis`, een lijst met zoektermen is gegenereerd op basis van het Hallo-frequentie en zeldzaamheid van termen in Hallo brondocument. Deze voorwaarden worden vervolgens gebruikt toomake Hallo aanvraag. Hallo standaard de inhoud van alle `searchable` velden worden beschouwd als tenzij `searchFields` is gebruikte toorestrict welke velden worden doorzocht.  

`$skip=#`(optioneel) - aantal search Hallo resulteert tooskip; Kan niet meer dan 100.000. Als u documenten in volgorde tooscan maar kan niet worden gebruikt `$skip` vanwege toothis beperking, kunt u overwegen `$orderby` voor een compleet besteld sleutel en `$filter` query in plaats daarvan met een bereik.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `skip` in plaats van `$skip`.
> 
> 

`$top=#`(optioneel) - aantal search Hallo tooretrieve resulteert. Dit kan worden gebruikt in combinatie met `$skip` zoekresultaten tooimplement clientzijde oproepen.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.
> 
> 

`$count=true|false`(optioneel, standaard te`false`)-geeft aan of toofetch Hallo totaal aantal resultaten. Dit is het aantal alle documenten die overeenkomen met de Hallo Hallo `search` en `$filter` parameters worden genegeerd `$top` en `$skip`. Als u deze waarde te`true` mogelijk invloed op de prestaties. Houd er rekening mee dat Hallo aantal geretourneerd een benadering is.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `count` in plaats van `$count`.
> 
> 

`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies toosort Hallo resultaten door. Elke expressie kan bestaan uit naam van een veld of een aanroep van toohello `geo.distance()` functie. Elke expressie kan worden gevolgd door `asc` tooindicated oplopende, en `desc` tooindicate aflopende. Hallo standaard is oplopende volgorde. Ties wordt Hallo overeen scores van documenten worden opgesplitst. Als er geen `$orderby` is opgegeven, Hallo standaardsorteervolgorde is Aflopend op document overeen score. Er is een limiet van 32 componenten voor `$orderby`.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.
> 
> 

`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve. Als u niets opgeeft, moet alle velden die zijn gemarkeerd als worden opgehaald in het Hallo-schema zijn opgenomen. U kunt ook expliciet alle velden aanvragen door deze parameter te`*`.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.
> 
> 

`facet=[string]`(nul of meer) - een veld toofacet door. Hallo-tekenreeks kan eventueel parameters toocustomize Hallo facetten uitgedrukt als een door komma's gescheiden `name:value` paren. Geldige parameters zijn:

* `count`(max. aantal facet voorwaarden; standaardwaarde is 10). Er is geen maximum maar hogere waarden worden een bijbehorende op de prestaties, vooral als Hallo meervoudige veld een groot aantal unieke voorwaarden bevat.
  * Bijvoorbeeld: `facet=category,count:5` opgehaald Hallo bovenste vijf categorieën in facet resultaten.  
  * **Opmerking**: als hello `count` parameter kleiner is dan het aantal unieke voorwaarden hello, Hallo resultaten mogelijk niet nauwkeurig. Dit is vanwege toohello manier facetten query's zijn verdeeld over shards. Verhogen `count` doorgaans toeneemt Hallo nauwkeurigheid van Hallo term aantallen, maar in een prestatievermindering optreden.
* `sort`(een van de `count` toosort *aflopende* op aantal `-count` toosort *oplopende* op aantal `value` toosort *oplopende* op waarde, of `-value` toosort *aflopende* door waarde)
  * Bijvoorbeeld: `facet=category,count:3,sort:count` opgehaald Hallo bovenste drie categorieën in facet resultaten in aflopende volgorde voor het aantal documenten met de stadsnaam van elke Hallo. Bijvoorbeeld, als bovenste drie categorieën Hallo Budget, Motel en luxe zijn, Budget gevonden in de 5 is, Motel 6 en heeft, luxe 4 is, vervolgens hello buckets niet in volgorde van Hallo Motel, Budget, luxe.
  * Bijvoorbeeld: `facet=rating,sort:-value` buckets voor alle mogelijke beoordelingen in aflopende volgorde voor waarde produceert. Als Hallo classificaties uit 1 too5, wordt Hallo buckets besteld 5, 4, 3, 2, 1, ongeacht het aantal documenten overeenkomen met elke beoordeling.
* `values`(pipe gescheiden numerieke of `Edm.DateTimeOffset` waarden opgeven van een dynamische set facet vermelding waarden)
  * Bijvoorbeeld: `facet=baseRate,values:10|20` produceert drie buckets: één voor base snelheid 0 up toobut niet met inbegrip van 10, één voor 10 up toobut niet inclusief 20 en één voor 20 of hoger.
  * Bijvoorbeeld: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produceert twee buckets: één voor hotels renovated vóór februari 2010 en één voor hotels renovated februari 1e, 2010 of hoger.
* `interval`(geheel getal interval dat groter is dan 0 voor getallen, of `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` datumwaarden tijd)
  * Bijvoorbeeld: `facet=baseRate,interval:100` produceert op basis van base snelheid bereiken met een grootte van 100 buckets. Bijvoorbeeld, als base tarieven alle tussen $60 en $600, zullen er buckets voor 0-100, 100-200, 200 en 300, 400 500, 300 400 en 500-600.
  * Bijvoorbeeld: `facet=lastRenovationDate,interval:year` één bucket voor elk jaar wanneer hotels zijn renovated produceert.
* `timeoffset`([+-] hh: mm, [+-] UUMM, of [+-] hh) `timeoffset` is optioneel. Kan alleen worden gecombineerd met Hallo `interval` optie en alleen wanneer toegepaste tooa veld van het type `Edm.DateTimeOffset`. Hallo waarde geeft Hallo UTC tijd verschoven tooaccount voor bij het instellen van tijd grenzen.
  * Bijvoorbeeld: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` gebruikt Hallo dag grens die bij 01:00:00 UTC (middernacht in Hallo doeltijdzone begint)
* **Opmerking**: `count` en `sort` worden gecombineerd tot Hallo dezelfde facet specificatie, maar ze kunnen niet worden gecombineerd met `interval` of `values`, en `interval` en `values` kan niet worden gecombineerd.
* **Opmerking**: Interval facetten op datum / tijd worden berekend op basis van UTC-tijd als `timeoffset` is niet opgegeven. Bijvoorbeeld: voor `facet=lastRenovationDate,interval:day`, Hallo dag grens begint bij 00:00:00 UTC. 

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `facets` in plaats van `facet`. Bovendien geeft u het als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke facet-expressie is.
> 
> 

`$filter=[string]`(optioneel): een zoekexpressie gestructureerde in de standaard OData-syntaxis.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.
> 
> 

`highlight=[string]`(optioneel): een reeks door komma's gescheiden veldnamen gebruikt voor treffer worden gemarkeerd. Alleen `searchable` velden kunnen worden gebruikt voor treffers markeren.

`highlightPreTag=[string]`(optioneel, standaard te`<em>`): een string-code die voegt toohit licht toe. Moet worden ingesteld met `highlightPostTag`.

> [!NOTE]
> Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).
> 
> 

`highlightPostTag=[string]`(optioneel, standaard te`</em>`)-tekenreeks label toohit highlights worden toegevoegd. Moet worden ingesteld met `highlightPreTag`.

> [!NOTE]
> Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).
> 
> 

`scoringProfile=[string]`(optioneel) - Hallo-naam van een score profiel tooevaluate overeen scores voor overeenkomende documenten in volgorde toosort Hallo resultaten.

`scoringParameter=[string]`Geeft aan Hallo waarden voor elke parameter die is gedefinieerd in een score functie (nul of meer) - (bijvoorbeeld `referencePointParameter`) met de indeling Hallo `name-value1,value2,...`.

* Bijvoorbeeld, als Hallo score berekenen profiel een functie met definieert een parameter met de naam van de optie 'mylocation' hello query-tekenreeks zou zijn `&scoringParameter=mylocation--122.2,44.8`. Hallo eerste dash scheidt Hallo naam uit de lijst met waarden Hallo, terwijl de tweede streepje Hallo deel uit van Hallo eerste waarde (lengtegraad in dit voorbeeld maakt).
* Scoreprofiel parameters kunt u een dergelijke waarden in Hallo lijst met enkele aanhalingstekens escape zoals voor de code die versterking kunt bevatten komma's. Als Hallo waarden zelf tussen enkele aanhalingstekens bevatten, kunt u dit omheen door te verdubbelen.
  * Bijvoorbeeld, als u een parameter met de naam 'mytag' versterking tag hebt en u tooboost op Hallo code wilt waarden 'Hallo, O'Brien' en 'Smith' hello query verbindingsreeksoptie zou worden `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Aanhalingstekens zijn alleen vereist voor waarden die door komma's bevatten.

> [!NOTE]
> Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `scoringParameters` in plaats van `scoringParameter`. U ook als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke is `name-values` paar.
> 
> 

`minimumCoverage`(optioneel, standaard too100) - een getal tussen 0 en 100, waarmee wordt aangegeven percentage Hallo Hallo-index die moet worden gedekt door een zoekopdracht om Hallo query toobe gerapporteerd als een is voltooid. Standaard Hallo gehele index moet beschikbaar zijn of `Search` HTTP-statuscode 503 wordt geretourneerd. Als u instelt `minimumCoverage` en `Search` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord Hallo Hallo percentage Hallo-index die is opgenomen in het Hallo-query waarmee wordt aangegeven.

> [!NOTE]
> Als u deze parameter tooa-waarde lager dan 100 nuttig zijn kan voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica. Niet alle overeenkomende documenten zijn echter toobe aanwezig zijn in de zoekresultaten Hallo gegarandeerd. Als zoeken intrekken belangrijker tooyour toepassing dan beschikbaarheid is, wordt het aanbevolen tooleave is `minimumCoverage` op de standaardwaarde van 100.
> 
> 

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter in Hallo-URL, ongeacht of u aanroepen **Search** met GET of POST.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, unieke tooyour service-URL. Hallo **Search** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Voor GET: geen.

Voor POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Voortzetting van antwoorden voor Deelzoekopdrachten**

Soms kan niet Azure Search alle aangevraagde resultaten in een enkel antwoord met zoeken Hallo retourneren. Dit kan gebeuren om verschillende redenen, zoals wanneer Hallo query te veel documenten aanvragen door op te geven niet `$top` of een waarde opgeeft voor `$top` die te groot is. In dergelijke gevallen horen Azure Search Hallo `@odata.nextLink` aantekening in antwoordtekst hello, en ook `@search.nextPageParameters` als deze een POST-aanvraag. Kunt u Hallo waarden van deze aantekeningen tooformulate zoeken aanvraag tooget Hallo volgende ergens anders in Hallo zoeken antwoord. Dit wordt genoemd, een ***voortzetting*** van de oorspronkelijke zoekaanvraag Hallo en Hallo aantekeningen in het algemeen worden genoemd ***voortzetting tokens***. Zie [Hallo onderstaand voorbeeld](#SearchResponse) voor meer informatie over Hallo syntaxis van deze aantekeningen en waar ze worden weergegeven in de antwoordtekst Hallo. 

Hallo redenen waarom Azure Search voortzetting tokens retourneert zijn implementatie en onderwerp toochange. Robuuste clients moeten altijd gereed toohandle gevallen waarbij minder documenten dan verwacht worden geretourneerd en een vervolgtoken is opgenomen toocontinue bij het ophalen van documenten. Ook opmerking die u moet gebruiken dezelfde HTTP-methode als de oorspronkelijke aanvraag Hallo in volgorde toocontinue Hallo. Bijvoorbeeld, als u een GET-aanvraag verzonden, voortzetting verzoeken u verzendt moeten ook gebruiken GET (en ook voor POST).

<a name="SearchResponse"></a>
**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Voorbeelden:**

U vindt aanvullende voorbeelden gegeven op Hallo [OData-expressiesyntaxis voor Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) pagina.

1)    Hallo Search Index gesorteerd in aflopende volgorde datum.

    GET-/indexes/hotels/docs? zoeken = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'orderby': "lastRenovationDate desc"}

2)    In een meervoudige zoekopdracht zoekt Hallo-index en facetten voor categorieën, classificatie, labels, evenals artikelen met baseRate in specifieke bereiken ophalen:

    GET /indexes/hotels/docs? zoeken = test & facet = categorie & facet = classificatie & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['categorie', 'classificatie', 'tags', ' baseRate, waarden: 80 | 150 | 220"]}

3)    Met een filter Hallo vorige meervoudige queryresultaten beperken nadat de gebruiker op Hallo classificatie 3 en categorie 'Motel':

    GET /indexes/hotels/docs? zoeken = test & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & $filter = classificatie eq 3 en categorie-eq "Motel" & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['tags', ' baseRate, waarden: 80 | 150 | 220"], 'filter': 'classificatie eq 3 en categorie-eq 'Motel' '}

4) In een meervoudige zoekopdracht, moet u een bovenlimiet instellen op unieke voorwaarden in een query zijn geretourneerd. Hallo standaardwaarde is 10, maar u kunt vergroten of verkleinen van deze waarde Hallo `count` parameter op Hallo `facet` kenmerk:

    GET-/indexes/hotels/docs? zoeken = test & facet = city, aantal: 5 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'zoeken': 'test', 'facetten': ["city, aantal: 5"]}

5)    Hallo Index binnen specifieke velden; zoeken Bijvoorbeeld, een specifieke taal zijn gebonden veld:

    GET-/indexes/hotels/docs? zoeken = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "hôtel', 'searchFields':"description_fr"}

6) Hallo Index over meerdere velden zoeken. Bijvoorbeeld, u kunt opslaan en query doorzoekbare velden in meerdere talen, alle binnen dezelfde index Hallo.  Als de Engelse en Franse beschrijvingen naast elkaar bestaan in Hallo dezelfde document, kunt u terugkeren of alle in Hallo queryresultaten:

    GET-/indexes/hotels/docs? zoeken = hotel & searchFields = beschrijving, description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "Hotels", "searchFields": "beschrijving, description_fr"}

Houd er rekening mee dat u kunt alleen een query één index op een tijdstip. Maak meerdere indexen voor elke taal geen tenzij u tooquery een tegelijk.

7)    Wisselbestand - Get Hallo 1e pagina met items (paginaformaat is 10):

    GET-/indexes/hotels/docs? zoeken = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "* ', 'overslaan': 0, 'top': 10}

8)    Wisselbestand - Get Hallo 2e pagina met items (paginaformaat is 10):

    GET-/indexes/hotels/docs? zoeken = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'search': ' * ', 'overslaan': 10, 'top': 10}

9)    Ophalen van een specifieke set velden:

    GET-/indexes/hotels/docs? zoeken = * & $select = hotelName, beschrijving en api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'select': "hotelName Beschrijving"}

10)  Ophalen van documenten die overeenkomt met een specifieke filterexpressie:

    GET-/indexes/hotels/docs? $filter = (baseRate ge 60 en baseRate lt 300) of hotelName eq fraai blijven & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'filter': ' (baseRate ge 60 en baseRate lt 300) of hotelName eq 'Fraai verblijf' "}

11) Hallo-index te zoeken en fragmenten met treffers licht retourneren

    GET-/indexes/hotels/docs? zoeken = iets & Markeer = beschrijving & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets", "highlight": 'beschrijving'}

12) Hallo-index te zoeken en documenten van dichter toofarther weg van een referentielocatie gesorteerd retourneren

    GET-/indexes/hotels/docs? zoeken = iets & $orderby=geo.distance (locatie, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'orderby': ' geo.distance (locatie, geography'POINT(-122.12315 47.88121)')"}

13) Zoeken Hallo index ervan uitgaande dat er een 'geografisch' aangeroepen scoreprofiel met twee afstandsscorefuncties, wordt één definiëren van een parameter genaamd 'currentLocation' en één voor het definiëren van een parameter met de naam 'lastLocation'

    GET /indexes/hotels/docs? zoeken = iets & scoringProfile = geo & scoringParameter = currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'scoringProfile': 'geo', 'scoringParameters': [' currentLocation--122.123,44.77233 ', ' lastLocation--121.499,44.2113 ']}

14) Documenten zoeken in het Hallo-index met behulp [vereenvoudigde querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx). Deze query retourneert hotels waar doorzoekbare velden Hallo voorwaarden 'comfort' en 'locatie', maar niet 'motel bevatten':

    GET-/indexes/hotels/docs? zoeken = comfort + locatie-motel & searchMode = all & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "comfort + locatie-motel ', 'searchMode': 'alle'}

Houd er rekening mee Hallo gebruik van `searchMode=all` hierboven. Deze parameter inclusief overschrijft Hallo standaard van `searchMode=any`, zorgt dat `-motel` 'En niet' in plaats van "Of niet" betekent. Zonder `searchMode=all`, krijgt u "Of niet" dat wordt uitgebreid in plaats van de zoekresultaten wordt beperkt, en dit kan erg intuïtief toosome gebruikers zijn.

15) Documenten zoeken in het Hallo-index met behulp [lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx). Deze query retourneert hotels waarbij categorieveld Hallo Hallo term 'budget' en alle doorzoekbare velden die Hallo de zin "onlangs renovated" bevat. Documenten met Hallo zinsnede 'onlangs renovated' krijgen een hogere rang als gevolg van Hallo term versterking waarde (3)

    GET-/indexes/hotels/docs? zoeken = categorie: budget en \"onlangs renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & querytype = full

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "categorie: budget en \"onlangs renovated\"^ 3", 'queryType': 'volledige', 'searchMode': 'alle'}

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Lookup-Document
Hallo **Lookup Document** bewerking een document opgehaald uit Azure Search. Dit is handig wanneer een gebruiker op een specifieke zoekresultaat klikt en toolook om specifieke details over dat document gewenste.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **Lookup Document** verzoek als volgt kan worden samengesteld.

    GET /indexes/[index name]/docs/key?[query parameters]

U kunt ook Hallo traditionele OData-syntaxis voor het opzoeken van een sleutel gebruiken:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Hallo-aanvraag URI bevat [index name] en [sleutel], die aangeeft welke tooretrieve document uit welke index. U kunt slechts één document tegelijk ophalen. Gebruik **Search** tooget meerdere documenten in één aanvraag.

**Query-Parameters**

`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve. Als dat niet-opgegeven of te ingesteld`*`, alle velden die zijn gemarkeerd als worden opgehaald in het Hallo-schema zijn opgenomen in het Hallo-projectie.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, unieke tooyour service-URL. Hallo **Lookup Document** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Voorbeeld**

Lookup Hallo document die sleutel '2' heeft

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Lookup Hallo-document met sleutel 3 met OData-syntaxis:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Aantal documenten
Hallo **aantal documenten** bewerking wordt een telling van het aantal documenten in een zoekindex Hallo opgehaald. Hallo `$count` syntaxis maakt deel uit van Hallo OData-protocol.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **aantal documenten** aanvraag kan worden opgesteld met Hallo GET-methode.

Hallo [naam van de index] in Hallo aanvraag-URI vertelt Hallo service tooreturn een telling van alle items in Hallo docs verzameling van Hallo opgegeven index.

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.

* `Accept`: Met deze waarde te moet worden ingesteld`text/plain`.
* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, unieke tooyour service-URL. Hallo **aantal documenten** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Geen.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hallo-antwoordtekst bevat Hallo count-waarde als een geheel getal als tekst zonder opmaak geformatteerd.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Suggesties
Hallo **suggesties** bewerking suggesties op basis van deelzoekopdrachten invoer worden opgehaald. Dit wordt doorgaans gebruikt in de vakken tooprovide automatisch aangevulde zoeksuggesties als gebruikers zoektermen invoert.

Suggestie aanvragen die zijn gericht op het opmaken van de doeldocumenten, zodat Hallo voorgestelde tekst kan worden herhaald als meerdere candidate documenten Hallo overeenkomen met dezelfde invoer zoeken. U kunt `$select` tooretrieve andere document velden (inclusief Hallo documentsleutel) zodat u kunt zien welke document Hallo bron voor elke suggestie.

Een **suggesties** bewerking als een GET of POST-aanvraag is uitgegeven.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Wanneer toouse BOEKT in plaats van ophalen**

Bij het gebruik van HTTP GET toocall hello **suggesties** API, moet u toobe Houd er rekening mee dat Hallo Hallo aanvraag-URL kan niet langer zijn dan 8 KB. Dit is meestal genoeg voor de meeste toepassingen. Sommige toepassingen produceren echter zeer grote query's specifiek OData-filterexpressies. Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters dan GET. Met POST, Hallo aantal componenten in een filter is een beperkende factor hello, grootte van de onbewerkte filtertekenreeks Hallo niet Hallo omdat Hallo aanvraag groottelimiet voor POST is ongeveer 16 MB.

> [!NOTE]
> Hoewel de maximale grootte Hallo POST-aanvraag erg groot is, kunnen niet filterexpressies willekeurig complex zijn. Zie [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over filter complexiteit beperkingen.
> 
> 

**Aanvraag**

HTTPS is vereist voor serviceaanvragen. Hallo **suggesties** aanvraag kan worden opgesteld met Hallo GET of POST-methoden.

Hallo aanvraag-URI bevat Hallo-naam van Hallo index tooquery. Parameters, zoals Hallo gedeeltelijk invoer zoekterm, zijn opgegeven in de queryreeks Hallo in geval van Hallo van GET-aanvragen en in Hallo aanvraag hoofdtekst in geval van Hallo van POST-aanvragen.

Als een best practice bij het maken van GET-aanvragen te onthouden[URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke parameters bij het aanroepen van REST-API rechtstreeks Hallo-query. Voor **suggesties** bewerkingen, dit omvat:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

URL-codering wordt alleen aanbevolen voor Hallo hierboven queryparameters. Als u per ongeluk URL coderen hello volledige queryreeks (alles na Hallo?), worden aanvragen wordt verbroken.

Zo is de URL-codering ook alleen nodig bij het aanroepen van Hallo direct met REST-API aan. Er is geen URL-codering is nodig bij het aanroepen van **suggesties** met behulp van POST, of bij het gebruik van Hallo [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die het URL-codering voor u verwerkt.

**Query-Parameters**

**Suggesties** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert. U opgeven dat deze parameters in Hallo URL querytekenreeks bij het aanroepen van **suggesties** via GET en als JSON-eigenschappen in de aanvraagtekst Hallo bij het aanroepen van **suggesties** via POST. Hallo-syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST. Deze verschillen worden vermeld als die van toepassing zijn hieronder:

`search=[string]`-Hallo tekst toouse toosuggest zoekopdrachten. Moet minimaal 1 teken en niet meer dan 100 tekens.

`highlightPreTag=[string]`(optioneel): een tekenreeks-code die voegt toosearch treffers toe. Moet worden ingesteld met `highlightPostTag`.

> [!NOTE]
> Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).
> 
> 

`highlightPostTag=[string]`(optioneel): een tekenreeks-code die wordt toegevoegd toosearch treffers. Moet worden ingesteld met `highlightPreTag`.

> [!NOTE]
> Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).
> 
> 

`suggesterName=[string]`-Hallo-naam van Hallo suggestie als opgegeven in de Hallo `suggesters` verzameling die deel uitmaakt van de indexdefinitie Hallo. Een `suggester` bepaalt welke velden voor voorgestelde querytermen worden gescand. Zie [Suggestiefunctie](#Suggesters) voor meer informatie.

`fuzzy=[boolean]`(optioneel, standaard = false)-tootrue wanneer Stel deze API suggesties wordt gevonden, zelfs als er een teken vervangen of ontbreekt in de zoektekst Hallo is. Het wordt geleverd op de prestaties, zoals fuzzy suggestie zoekopdrachten trager en meer bronnen gebruiken terwijl dit een betere ervaring in sommige scenario's biedt.

`searchFields=[string]`(optioneel) - Hallo-lijst met door komma's gescheiden veld namen toosearch voor Hallo zoektekst opgegeven. Doelvelden moeten zijn ingeschakeld voor suggesties.

`$top=#`(optioneel, standaard = 5)-aantal suggesties tooretrieve Hallo. Moet een getal tussen 1 en 100 liggen.

> [!NOTE]
> Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.
> 
> 

`$filter=[string]`(optioneel): een expressie die documenten Hallo-filters in aanmerking voor suggesties.

> [!NOTE]
> Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.
> 
> 

`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies toosort Hallo resultaten door. Elke expressie kan bestaan uit naam van een veld of een aanroep van toohello `geo.distance()` functie. Elke expressie kan worden gevolgd door `asc` tooindicated oplopende, en `desc` tooindicate aflopende. Hallo standaard is oplopende volgorde. Er is een limiet van 32 componenten voor `$orderby`.

> [!NOTE]
> Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.
> 
> 

`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve. Als u niets opgeeft, wordt alleen Hallo documentsleutel en suggestie tekst wordt geretourneerd. U kunt alle velden expliciet aanvragen door deze parameter te`*`.

> [!NOTE]
> Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.
> 
> 

`minimumCoverage`(optioneel, standaard too80) - een getal tussen 0 en 100, waarmee wordt aangegeven percentage Hallo Hallo-index die moet worden gedekt door een query suggesties om Hallo query toobe gerapporteerd als een is voltooid. Standaard moet ten minste 80% van de index Hallo beschikbaar zijn of `Suggest` HTTP-statuscode 503 wordt geretourneerd. Als u instelt `minimumCoverage` en `Suggest` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord Hallo Hallo percentage Hallo-index die is opgenomen in het Hallo-query waarmee wordt aangegeven.

> [!NOTE]
> Als u deze parameter tooa-waarde lager dan 100 nuttig zijn kan voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica. Niet alle overeenkomende suggesties zijn echter toobe aanwezig is in de resultaten Hallo gegarandeerd. Als intrekken belangrijker tooyour toepassing dan beschikbaarheid en vervolgens de best niet toolower `minimumCoverage` lager dan de standaardwaarde 80.
> 
> 

`api-version=[string]`(vereist). Hallo preview-versie is `api-version=2015-02-28-Preview`. Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.

Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter in Hallo-URL, ongeacht of u aanroepen **suggesties** met GET of POST.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders

* `api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, unieke tooyour service-URL. Hallo **suggesties** aanvraag een beheersleutel of een querysleutel kunt opgeven als Hallo `api-key`.

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

**Aanvraagtekst**

Voor GET: geen.

Voor POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Als Hallo projectie optie gebruikte tooretrieve velden die zijn opgenomen in elk element van Hallo matrix:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Voorbeeld**

5 suggesties waarbij Hallo deelzoekopdrachten invoer is 'lux' ophalen

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
