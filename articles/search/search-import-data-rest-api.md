---
title: aaa "uploaden van gegevens (REST-API - Azure Search) | Microsoft Docs'
description: Meer informatie over hoe tooupload gegevens tooan index in Azure Search met behulp van Hallo REST-API.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Het uploaden van gegevens tooAzure zoeken met Hallo REST-API
> [!div class="op_single_selector"]
>
> * [Overzicht](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

In dit artikel wordt uitgelegd hoe u toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport gegevens in een Azure Search-index.

Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md).

In de volgorde toopush documenten in uw index met behulp van Hallo REST-API, doet u een HTTP POST-aanvraag tooyour index URL-eindpunt. Hallo-hoofdtekst van Hallo HTTP-aanvraag hoofdtekst is een JSON-object met Hallo documenten toobe toegevoegd, gewijzigd of verwijderd.

## <a name="identify-your-azure-search-services-admin-api-key"></a>De admin api-sleutel voor de Azure Search-service vaststellen
Bij de uitgifte van HTTP-aanvragen op basis van uw service met behulp van Hallo REST API, *elke* API-aanvraag vergezeld gaan van Hallo api-sleutel die is gegenereerd voor Hallo Search-service die u hebt ingericht. Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.

1. toofind van uw service api-sleutels, kunt u aanmelden toohello [Azure-portal](https://portal.azure.com/)
2. Blade Ga tooyour Azure Search service
3. Klik op Hallo 'Sleutels'-pictogram

Uw service heeft zowel *administratorsleutels* als *querysleutels*.

* De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen. Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.
* Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.

Voor de toepassing hello gegevens te importeren in een index, kunt u ofwel de primaire of secundaire administratorsleutel.

## <a name="decide-which-indexing-action-toouse"></a>Bepaal welke indexering actie toouse
Wanneer u Hallo REST-API gebruikt, doet u HTTP POST-aanvragen met JSON-aanvraag instanties tooyour Azure Search-index van de eindpunt-URL. Hallo JSON-object in de hoofdtekst van uw HTTP-aanvraag bevat een JSON-matrix met de naam 'waarde' bevat JSON-objecten die u wilt dat tooadd tooyour index documenten vertegenwoordigt, bijwerken of verwijderen.

Elk JSON-object in de matrix '' waarde '' Hallo vertegenwoordigt een document toobe geïndexeerd. Elk van deze objecten van het document Hallo sleutel bevat en geeft indexeerbewerking Hallo gewenst (uploaden, samenvoegen, verwijderen, enzovoort). Afhankelijk van welke van Hallo onderstaande bewerkingen die u kiest, moet alleen bepaalde velden voor elk document opnemen:

| @search.action | Beschrijving | Vereiste velden voor elk document | Opmerkingen |
| --- | --- | --- | --- |
| `upload` |Een `upload` actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat. |sleutel, plus andere velden die u wenst dat toodefine |Wanneer het bijwerken/vervangen van een bestaand document wordt elk veld dat niet is opgegeven in de aanvraag Hallo hebt ingesteld te`null`. Dit gebeurt zelfs als Hallo veld eerder tooa null-waarde is ingesteld. |
| `merge` |Een bestaand document met het Hallo updates opgegeven velden. Als Hallo document niet in de index hello bestaat, mislukt de Hallo samenvoegen. |sleutel, plus andere velden die u wenst dat toodefine |Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document. ook velden van het type `Collection(Edm.String)`. Bijvoorbeeld, als hello document bevat een veld `tags` met waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor `tags`, uiteindelijke waarde van Hallo Hallo `tags` veld `["economy", "pool"]`. Het wordt dus niet `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Deze bewerking gedraagt zich als `merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat. Als het Hallo-document niet bestaat, gedraagt zich als `upload` met een nieuw document. |sleutel, plus andere velden die u wenst dat toodefine |- |
| `delete` |Verwijdert het opgegeven document Hallo van Hallo index. |alleen sleutel |Alle velden die u opgeeft dan Hallo sleutelveld worden genegeerd. Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `merge` en stelt u Hallo veld expliciet toonull. |

## <a name="construct-your-http-request-and-request-body"></a>De HTTP-aanvraag en de hoofdtekst opstellen
Nu dat u de benodigde veldwaarden Hallo hebt verzameld voor uw indexbewerkingen, u bent klaar tooconstruct Hallo werkelijke HTTP-aanvraag en JSON-aanvraag hoofdtekst tooimport uw gegevens.

#### <a name="request-and-request-headers"></a>Aanvragen en aanvraagheaders
Hallo-URL, moet u tooprovide de servicenaam, de indexnaam ("hotels" in dit geval), evenals Hallo juiste API-versie (Hallo huidige API-versie is `2016-09-01` op Hallo moment van publicatie van dit document). U moet toodefine hello `Content-Type` en `api-key` aanvraagheaders. Voor deze laatste Hallo, een van de administratorsleutels van uw service te gebruiken.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Aanvraagtekst
```JSON
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
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

In dit geval gebruiken we `upload`, `mergeOrUpload` en `delete` als onze zoekacties.

We gaan ervan uit dat deze voorbeeldindex "hotels" al is gevuld met een aantal documenten. Hoe we hoefden niet toospecify alle mogelijke documentvelden Hallo bij gebruik van `mergeOrUpload` en hoe we alleen opgegeven Hallo documentsleutel (`hotelId`) bij gebruik van `delete`.

Bovendien opmerking die u alleen hoger too1000 documenten (of 16 MB) in een enkele indexeringsaanvraag opnemen kunt.

## <a name="understand-your-http-response-code"></a>De HTTP-antwoordcode begrijpen
#### <a name="200"></a>200
Na een geslaagde indexeringsaanvraag ontvangt u een HTTP-antwoord met de statuscode `200 OK`. Hallo JSON-hoofdtekst van Hallo HTTP-antwoord is als volgt:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Statuscode `207` wordt geretourneerd wanneer ten minste één item is niet geïndexeerd. Hallo JSON-hoofdtekst van Hallo HTTP-antwoord bevat informatie over mislukte Hallo-documenten.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Dit betekent vaak dat load Hallo op uw zoekopdracht service een waarbij tooreturn indexeringsaanvragen punt bereikt `503` reacties. In dit geval is het aanbevolen om de clientcode uit te stellen en te wachten voordat u het opnieuw probeert. Hierdoor krijgt Hallo system sommige toorecover tijd, Hallo kans dat toekomstige aanvragen waarschijnlijk wel mogelijk verhogen. Uw verzoeken om snel opnieuw uit te voeren, wordt alleen Hallo situatie verlengen.
>
>

#### <a name="429"></a>429
Statuscode `429` wordt geretourneerd wanneer u het quotum van Hallo aantal documenten per index hebt overschreden.

#### <a name="503"></a>503
Statuscode `503` wordt geretourneerd als geen van de items in aanvraag Hallo Hallo zijn geïndexeerd. Deze fout betekent dat Hallo-systeem zwaar belast wordt en uw aanvraag op dit moment niet worden verwerkt.

> [!NOTE]
> In dit geval is het aanbevolen om de clientcode uit te stellen en te wachten voordat u het opnieuw probeert. Hierdoor krijgt Hallo system sommige toorecover tijd, Hallo kans dat toekomstige aanvragen waarschijnlijk wel mogelijk verhogen. Uw verzoeken om snel opnieuw uit te voeren, wordt alleen Hallo situatie verlengen.
>
>

Zie [Documenten toevoegen, bijwerken of verwijderen](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) voor meer informatie over bewerkingen en antwoorden voor een geslaagde of mislukte bewerking. Zie [HTTP-statuscodes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) voor meer informatie over andere HTTP-statuscodes die kunnen worden geretourneerd in geval van storing.

## <a name="next-steps"></a>Volgende stappen
Na het vullen van uw Azure Search-index, zult u gereed toostart uitgeven van query's toosearch voor documenten. Zie [Een query uitvoeren in uw Azure-zoekindex](search-query-overview.md) voor meer informatie.
