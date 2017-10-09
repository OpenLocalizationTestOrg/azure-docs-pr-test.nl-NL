---
title: aaaQuery uw Azure Search-Index | Microsoft Docs
description: Een zoekopdracht in Azure search samenstellen en gebruiken van parameters toofilter en sorteren search zoekresultaten.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Een query uitvoeren in uw Azure Search-index
> [!div class="op_single_selector"]
> * [Overzicht](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Bij het indienen van search-aanvragen tooAzure zoeken, zijn er een aantal parameters dat kan worden opgegeven naast Hallo werkelijke woorden die in het zoekvak Hallo van uw toepassing worden getypt. Deze queryparameters bieden u tooachieve een betere controle over Hallo [zoeken in volledige tekst ervaring](search-lucene-query-architecture.md).

Hieronder volgt een lijst met een korte beschrijving van veelvoorkomende toepassingen van Hallo queryparameters in Azure Search. Raadpleeg voor een uitgebreid overzicht van queryparameters en hun gedrag Hallo gedetailleerde pagina's voor Hallo [REST-API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) en [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Typen query's
Azure Search biedt veel opties toocreate de krachtige query's. Hallo twee belangrijkste querytypen die u zult gebruiken zijn `search` en `filter`. Een `search` query zoekt naar een of meer voorwaarden in alle *doorzoekbare* velden in uw index en werkt op Hallo manier zou u een zoekmachine als Google of Bing toowork verwacht. Een `filter`-query evalueert een Booleaanse expressie op alle *filterbare* velden in een index. In tegenstelling tot `search` query's `filter` query's overeenkomen met de exacte inhoud van een veld, wat betekent dat ze hoofdlettergevoelig zijn voor tekenreeksvelden Hallo.

U kunt zoekopdrachten en filters samen of afzonderlijk gebruiken. Als u ze samen gebruiken, is het Hallo-filter eerste toohello gehele index toegepast en vervolgens Hallo-zoekopdracht uitgevoerd op Hallo resultaten van Hallo filter. Filters daarom is een nuttig tooimprove query-prestaties omdat het Hallo-verzameling van documenten die Hallo zoeken query behoeften tooprocess verminderd.

Hallo-syntaxis voor filterexpressies is een subset van Hallo [OData-filtertaal](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Voor zoekquery's kunt u beide Hallo [vereenvoudigde syntaxis](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) of Hallo [Lucene-querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) deze worden hieronder behandeld.

### <a name="simple-query-syntax"></a>Vereenvoudigde querysyntaxis
Hallo [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) Hallo query standaardtaal die wordt gebruikt in Azure Search is. Hallo vereenvoudigde querysyntaxis ondersteunt een aantal algemene Zoekoperators, zoals Hallo AND, OR, niet, woordgroep, achtervoegsel en prioriteit operators.

### <a name="lucene-query-syntax"></a>Lucene-querysyntaxis
Hallo [Lucene-querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) kunt u toouse Hallo algemeen vastgesteld en expressieve querytaal ontwikkeld als onderdeel van [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Met deze querysyntaxis kunt u tooeasily bereiken Hallo volgende mogelijkheden: [veldgerelateerde query's](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [fuzzy zoeken](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [zoeken bij benadering](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ versterking](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [zoeken op reguliere expressies](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [zoeken met jokertekens](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [syntaxisgrondbeginselen](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), en [query's met Booleaanse operators](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Resultaten ordenen
U kunt aanvragen dat Azure Search Hallo resultaten waarden in een bepaald veld geordend fungeert tijdens het ontvangen van resultaten van een zoekopdracht. Standaard ordent Azure Search zoekresultaten Hallo op basis van de positie Hallo van elk document zoeken score, die is afgeleid van [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Als u wilt dat Azure Search tooreturn uw resultaten geordend op een andere waarde dan Hallo zoeken score, kunt u Hallo `orderby` zoekparameter. U kunt de waarde Hallo Hallo opgeven `orderby` parameter tooinclude veld namen en roept toohello [ `geo.distance()` functie](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) voor georuimtelijke waarden. Elke expressie kan worden gevolgd door `asc` tooindicate dat de resultaten zijn aangevraagd in oplopende volgorde, en `desc` tooindicate dat resultaten in aflopende volgorde worden aangevraagd. Hallo standaard oplopende volgorde.

## <a name="paging"></a>Zoekresultaten oproepen
Azure Search kunt u eenvoudig tooimplement paging zoekresultaten. Met behulp van Hallo `top` en `skip` parameters, u kunt eenvoudig zoekaanvragen uitgeven waarmee u tooreceive Hallo totale aantal zoekresultaten in een beheersbare, geordende subset kunt weergeven om goede zoekopdracht uit te voeren. Tijdens het ontvangen van deze kleinere subsets van resultaten kunt u ook Hallo aantal documenten in totaal aantal zoekresultaten Hallo ontvangen.

U kunt meer informatie over het oproepen van zoekresultaten in Hallo artikel [hoe toopage zoekresultaten in Azure Search](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Markeren
In Azure Search benadrukken exacte aantal zoekresultaten weergeven die overeenkomen met de zoekopdracht Hallo Hallo wordt gemaakt eenvoudig met Hallo `highlight`, `highlightPreTag`, en `highlightPostTag` parameters. U kunt opgeven welk *doorzoekbare* velden benadrukt. ook kunt geven Hallo exacte tekenreeks labels tooappend toohello begin en einde van Hallo overeenkomende tekst die Azure Search retourneert tekst moeten hebben.

## <a name="try-out-query-syntax"></a>Querysyntaxis uitproberen

Hallo aanbevolen manier toounderstand syntaxisverschillen is door het indienen van query's en het bekijken van resultaten.

+ Gebruik [Search Explorer](search-explorer.md) in hello Azure-portal. Door het implementeren van [Hallo voorbeeld index](search-get-started-portal.md), u kunt een index Hallo query in minuten met behulp van hulpprogramma's in Hallo-portal.

+ Gebruik [Fiddler](search-fiddler.md) of Chrome Postman toosubmit query's tooan index dat u de zoekservice tooyour hebt geüpload. Beide hulpprogramma's voor ondersteuning voor REST-aanroepen tooan HTTP-eindpunt. 
