---
title: aaa "query uitvoeren in een index (REST-API - Azure Search) | Microsoft Docs'
description: Een zoekopdracht in Azure search samenstellen en gebruiken van parameters toofilter en sorteren search zoekresultaten.
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Query uitvoeren op uw Azure Search-index met behulp van Hallo REST-API
> [!div class="op_single_selector"]
>
> * [Overzicht](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Dit artikel laat zien hoe uw index met behulp tooquery Hallo [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).

Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md) en moet deze index [gevuld zijn met gegevens](search-what-is-data-import.md). Zie [How full text search works in Azure Search](search-lucene-query-architecture.md) (Hoe zoeken in volledige tekst werkt in Azure Search) voor achtergrondinformatie.

## <a name="identify-your-azure-search-services-query-api-key"></a>De query api-sleutel voor de Azure Search-service vaststellen
Een belangrijk onderdeel van elke zoekbewerking in hello Azure Search REST API is Hallo *api-sleutel* die is gegenereerd voor Hallo-service die u hebt ingericht. Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.

1. toofind van uw service api-sleutels, kunt u aanmelden toohello [Azure-portal](https://portal.azure.com/)
2. Blade Ga tooyour Azure Search service
3. Klik op het pictogram 'Sleutels' Hallo

Uw service heeft zowel *administratorsleutels* als *querysleutels*.

* De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen. Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.
* Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.

Voor de toepassing hello van query's op een index, kunt u een van de query-sleutel. De administratorsleutels kunnen ook worden gebruikt voor query's, maar moet u een querysleutel in uw toepassingscode als dit beter Hallo volgt [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Uw query formuleren
Er zijn twee manieren ook[zoeken in uw index met behulp van Hallo REST-API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Een manier is een HTTP POST-aanvraag tooissue waarbij uw queryparameters worden gedefinieerd in een JSON-object in de aanvraagtekst Hallo. Hallo andere manier is een HTTP GET-aanvraag tooissue waarbij uw queryparameters worden gedefinieerd binnen Hallo aanvraag-URL. POST heeft meer [versoepeld limieten](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) op Hallo grootte van de queryparameters dan GET. Daarom wordt u aangeraden POST te gebruiken, tenzij er speciale omstandigheden zijn waarin het gebruik van GET beter zou zijn.

Voor zowel POST als GET moet u tooprovide uw *servicenaam*, *indexnaam*, en de juiste Hallo *API-versie* (Hallo huidige API-versie is `2016-09-01` Hallo gelijktijdig van de publicatie van dit document) in Hallo aanvraag-URL. Voor GET, Hallo *querytekenreeks* Hallo einde van Hallo-URL is waarin u Hallo queryparameters opgeven. Hieronder vindt u Hallo URL-indeling:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Hallo-indeling voor POST is hetzelfde hello, maar met alleen api-versie in de queryreeksparameters Hallo.

#### <a name="example-queries"></a>Voorbeelden van query 's
Hier volgen een paar voorbeeldquery's op een index met de naam "hotels". Deze query's worden weergegeven in zowel de GET als POST-indeling.

Hallo term 'budget' hello gehele index zoeken en alleen Hallo retourneren `hotelName` veld:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Een filter toohello index toofind hotels goedkoper dan €150 per nachten toepassen en retourneren Hallo `hotelId` en `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Volledige zoekindex hello, volgorde op een bepaald veld (`lastRenovationDate`) Neem Hallo twee bovenste resultaten in aflopende volgorde, en alleen weergeven `hotelName` en `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>De HTTP-aanvraag verzenden
Nu u uw query hebt geformuleerd als onderdeel van uw HTTP-aanvraag-URL (voor GET) of hoofdtekst (voor POST), kunt u uw aanvraagheaders definiëren en uw query verzenden.

#### <a name="request-and-request-headers"></a>Aanvragen en aanvraagheaders
U moet twee aanvraagheaders definiëren voor GET en drie voor POST:

1. Hallo `api-key` header toohello querysleutel in stap I hierboven moet worden ingesteld. U kunt ook een administratorsleutel gebruiken als Hallo `api-key` header, maar het wordt aanbevolen dat u een querysleutel gebruikt, aangezien deze exclusieve alleen alleen-lezentoegang tooindexes en -documenten.
2. Hallo `Accept` header moet worden ingesteld te`application/json`.
3. Alleen voor POST, Hallo `Content-Type` header ook te worden ingesteld`application/json`.

Hieronder vindt u een HTTP GET-aanvraag toosearch Hallo index "hotels met behulp van Azure Search REST API, met een eenvoudige query waarin wordt gezocht naar Hallo term 'motel' hello":

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Hier volgt Hallo dezelfde voorbeeldquery, met behulp van HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Een queryaanvraag is gelukt resulteert in een statuscode van `200 OK` en Hallo zoekresultaten worden geretourneerd als JSON in Hallo antwoordtekst. Hier ziet u welke Hallo-resultaten voor Hallo hierboven query's eruit zien, ervan uitgaande dat index Hallo "hotels" is gevuld met de voorbeeldgegevens Hallo in [gegevens importeren in Azure Search met behulp van REST-API Hallo](search-import-data-rest-api.md) (Houd er rekening mee dat Hallo JSON is voor de duidelijkheid geformatteerd).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn meer, gaat u naar Hallo "Antwoord" sectie van [documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Zie [HTTP-statuscodes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) voor meer informatie over andere HTTP-statuscodes die kunnen worden geretourneerd in geval van storing.
