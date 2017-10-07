---
title: aaa "maken van een index (REST-API - Azure Search) | Microsoft Docs'
description: Een index in code met hello Azure Search HTTP REST-API maken.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Een Azure Search index maken met Hallo REST-API
> [!div class="op_single_selector"]
>
> * [Overzicht](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

In dit artikel begeleidt u stapsgewijs door het Hallo-proces voor het maken van een Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) met behulp van hello Azure Search REST-API.

Voordat u de stappen in dit artikel uitvoert en een index maakt, moet u eerst [een Azure Search-service](search-create-service-portal.md) hebben gemaakt.

toocreate een Azure Search-index met behulp van Hallo REST-API, doet u een één HTTP POST-aanvraag tooyour Azure Search-service van URL-eindpunt. De indexdefinitie van de worden opgenomen in de aanvraagtekst Hallo als juist opgemaakte JSON-inhoud.

## <a name="identify-your-azure-search-services-admin-api-key"></a>De admin api-sleutel voor de Azure Search-service vaststellen
Nu dat u een Azure Search-service hebt ingericht, kunt u HTTP-aanvragen op basis van uw service Hallo REST-API met URL-eindpunt uitgeven. *Alle* API-aanvragen Hallo api-sleutel die is gegenereerd voor de zoekservice die u hebt ingericht Hallo moeten bevatten. Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.

1. toofind van uw service api-sleutels u zich bij Hallo aanmelden moet [Azure-portal](https://portal.azure.com/)
2. Blade Ga tooyour Azure Search service
3. Klik op Hallo 'Sleutels'-pictogram

Uw service heeft zowel *administratorsleutels* als *querysleutels*.

* De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen. Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.
* Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.

Voor Hallo-toepassing van een index te maken, kunt u ofwel de primaire of secundaire administratorsleutel.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Een index voor Azure Search definiëren met een goed-opgemaakte JSON
De index van een HTTP POST-aanvraag tooyour service wilt maken. Hallo-hoofdtekst van uw HTTP POST-aanvraag bevat een JSON-object dat uw Azure Search-index definieert.

1. Hallo eerste eigenschap van dit JSON-object is Hallo-naam van de index.
2. Hallo tweede eigenschap van dit JSON-object is een JSON-matrix met de naam `fields` die een afzonderlijk JSON-object voor elk veld in uw index bevat. Elk van deze JSON-objecten bevat meerdere naamwaardeparen voor elk Hallo veldkenmerken, zoals "name", "type", enzovoort.

Het is belangrijk dat u uw zoekopdracht gebruiker ervaring en zakelijke behoeften rekening houden bij het ontwerpen van uw index als elk veld Hallo moet worden toegewezen [juiste kenmerken](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Deze kenmerken bepalen welke zoekfuncties (filteren, facetten, zoekacties volledige tekst sorteren enzovoort) toepassing toowhich velden. Voor elk kenmerk dat u niet opgeeft, worden standaard Hallo tooenable Hallo bijbehorende zoekfunctie tenzij speciaal uitschakelt.

In ons voorbeeld hebben we onze index hotels genoemd en de velden als volgt ingesteld:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

We hebt zorgvuldig Hallo indexkenmerken voor elk veld op basis van onze verwachting dat ze worden gebruikt in een toepassing gekozen. Bijvoorbeeld: `hotelId` is een unieke sleutel die mensen zoeken naar hotels waarschijnlijk niet kennen, zodat we een zoekopdracht in volledige tekst voor dat veld door in te stellen uitschakelen `searchable` te`false`, die databaseruimte Hallo index.

Houd er rekening mee dat precies één veld in de index van het type `Edm.String` moet worden Hallo aangemerkt als Hallo 'key'-veld.

bovenstaande Hallo indexdefinitie maakt gebruik van een taalanalyse voor Hallo `description_fr` veld omdat het beoogde toostore Franse tekst. Zie [onderwerp Hallo Language support](https://docs.microsoft.com/rest/api/searchservice/Language-support) en de bijbehorende Hallo [blogbericht](https://azure.microsoft.com/blog/language-support-in-azure-search/) voor meer informatie over taalanalyse.

## <a name="issue-hello-http-request"></a>Probleem Hallo HTTP-aanvraag
1. Door de indexdefinitie van de als aanvraagtekst hello, uitgeven, een eindpunt-URL voor HTTP POST-aanvraag tooyour Azure Search-service. Hallo-URL worden toouse ervoor dat de naam van de service als Hallo-hostnaam en Hallo juiste plaatsen `api-version` als een queryreeksparameter opgeven (Hallo huidige API-versie is `2016-09-01` op Hallo moment van publicatie van dit document).
2. Geef in de aanvraagheaders Hallo Hallo `Content-Type` als `application/json`. U moet ook tooprovide Beheersleutel van uw service die u in stap I in Hallo vastgesteld `api-key` header.

U hebt tooprovide uw eigen naam en de api key tooissue Hallo serviceaanvraag hieronder:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Als een aanvraag is gelukt, ziet u de statuscode 201 (Gemaakt). Bezoek voor meer informatie over het maken van een index via REST-API Hallo Hallo [hier API-referentiemateriaal](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Zie [HTTP-statuscodes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) voor meer informatie over andere HTTP-statuscodes die kunnen worden geretourneerd in geval van storing.

Wanneer u met een toodelete index en wilt dit bent klaar, roept u de aanvraag HTTP DELETE. Dit is bijvoorbeeld hoe we de index "hotels" hello wilt verwijderen:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Volgende stappen
Nadat een Azure Search-index is gemaakt, kunt u zich gereed te[uw inhoud uploaden naar de index Hallo](search-what-is-data-import.md) zodat u kunt beginnen met het zoeken van gegevens.
