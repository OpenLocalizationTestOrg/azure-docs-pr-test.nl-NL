---
title: aaaHow toopage zoekresultaten in Azure Search | Microsoft Docs
description: Paginering in Azure Search, een gehoste cloud search-service op Microsoft Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Hoe toopage zoekresultaten in Azure Search
In dit artikel biedt richtlijnen voor hoe toouse hello Azure Search Service REST API tooimplement standaardelementen van een zoekopdracht resultaten pagina, zoals het totale aantal, document ophalen, sorteervolgorde en navigatie.

In elk geval hieronder vermelde opties voor pagina's gerelateerde gegevens of informatie tooyour zoekresultatenpagina bijdragen worden opgegeven via Hallo [zoekdocument](http://msdn.microsoft.com/library/azure/dn798927.aspx) aanvragen verzonden tooyour Azure Search-Service. Aanvragen bevatten een GET-opdracht, pad, en queryparameters die informeren Hallo service wat wordt aangevraagd en hoe tooformulate Hallo antwoord.

> [!NOTE]
> Een geldige aanvraag bevat een aantal elementen, zoals een service-URL en het pad, HTTP-term `api-version`, enzovoort. We bijgesneden Hallo voorbeelden toohighlight alleen Hallo syntaxis relevante toopagination voor beknopt alternatief bevat. Zie Hallo [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentatie voor meer informatie over de syntaxis van de aanvraag.
> 
> 

## <a name="total-hits-and-page-counts"></a>Totaal aantal treffers en het aantal paginaweergaven
Hallo totaal aantal resultaten geretourneerd door een query en vervolgens te retourneren die resulteert in kleinere reeksen wordt weergegeven, is de fundamentele toovirtually alle zoekpagina's.

![][1]

In Azure Search, gebruikt u Hallo `$count`, `$top`, en `$skip` parameters tooreturn deze waarden. Hallo volgende voorbeeld ziet u een voorbeeld van een aanvraag voor het totaal aantal treffers geretourneerd als `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Documenten in groepen van 15 ophalen en totaal aantal treffers hello, beginnend bij de eerste pagina Hallo worden ook weergegeven:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Resultaten pagineren vereist zowel `$top` en `$skip`, waarbij `$top` Hiermee geeft u op hoeveel items tooreturn in een batch en `$skip` Hiermee geeft u op hoeveel items tooskip. In Hallo bijvoorbeeld na elke pagina Hallo naast 15 worden artikelen weergegeven, aangegeven door Hallo incrementele jumps in Hallo `$skip` parameter.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Lay-out
Op een pagina met zoekresultaten, kunt u tooshow een miniatuur, een subset van velden en een koppeling tooa product met volledig pagina.

 ![][2]

U wilt gebruiken in Azure Search `$select` en een lookup-opdracht tooimplement deze ervaring.

tooreturn een subset van velden voor een naast elkaar indeling:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Afbeeldingen en media-bestanden zijn niet rechtstreeks kan worden doorzocht en moeten worden opgeslagen in een ander platform van de opslag, zoals Azure Blob storage, tooreduce kosten. Definieer een veld waarin de URL-adres van de externe inhoud Hallo Hallo in Hallo-index en documenten. U kunt vervolgens Hallo veld gebruiken als een verwijzing naar afbeelding. Hallo URL toohello installatiekopie moet Hallo-document.

tooretrieve een productbeschrijving pagina voor een **onClick** gebeurtenis, gebruik [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in Hallo Hallo document tooretrieve sleutel. Hallo-gegevenstype van het Hallo-sleutel is `Edm.String`. In dit voorbeeld is het *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Sorteren op relevantie, classificatie of prijs
Sorteervolgorde vaak toorelevance standaard, maar het algemene toomake alternatieve sorteervolgorde direct beschikbaar is, zodat klanten snel bestaande resultaten naar een andere volgorde van de waarden van positie verplaatsen kunnen.

 ![][3]

In Azure Search sorteren is gebaseerd op Hallo `$orderby` expressie, voor alle velden die zijn geïndexeerd als`"Sortable": true.`

Relevantie is ten zeerste aan score berekenen voor profielen gekoppeld. U kunt gebruiken Hallo standaard score berekenen, die afhankelijk is van tekst analyse en statistieken toorank bestellen alle resultaten met hogere scores gebeurt toodocuments met meer of sterker komt overeen met een zoekterm.

Alternatieve sorteervolgorde zijn meestal gekoppeld aan **onClick** Hallo sorteervolgorde gebeurtenissen die terugbellen tooa methode die is gebaseerd. Bijvoorbeeld, krijgt deze pagina-element:

 ![][4]

Maakt u een methode die de sorteeroptie Hallo geselecteerd als invoer accepteert en retourneert een geordende lijst voor Hallo criteria die zijn gekoppeld aan die optie.

 ![][5]

> [!NOTE]
> Hallo standaard score berekenen is voldoende voor veel scenario's, wordt u aangeraden relevantie in plaats daarvan op een aangepaste scoreprofiel baseert. Een aangepaste scoreprofiel biedt een manier tooboost items meer nuttige tooyour bedrijven. Zie [een scoreprofiel toevoegen](http://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie. 
> 
> 

## <a name="faceted-navigation"></a>Facetnavigatie
Zoeken navigatie is gebruikelijk dat op een pagina met zoekresultaten, vaak zich bevindt op Hallo zijde of begin van een pagina. In Azure Search biedt facetnavigatie zelf gerichte zoeken op basis van vooraf gedefinieerde filters. Zie [facetnavigatie in Azure Search](search-faceted-navigation.md) voor meer informatie.

## <a name="filters-at-hello-page-level"></a>Filters op Hallo paginaniveau
Als uw ontwerp van de oplossing opgenomen toegewezen zoekpagina's voor specifieke typen inhoud (bijvoorbeeld, een online retail toepassing met afdelingen bovenaan Hallo Hallo pagina vermeld), kunt u een filterexpressie naast een **onClick** gebeurtenis tooopen een pagina in een vooraf gefilterde staat. 

U kunt een filter met of zonder een zoekexpressie verzenden. Bijvoorbeeld worden hello volgende aanvraag gefilterd op de naam van het merk, alleen documenten die overeenkomen met het retourneren.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Zie [documenten zoeken (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) voor meer informatie over `$filter` expressies.

## <a name="see-also"></a>Zie ook
* [Azure Search Service REST-API](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Indexbewerkingen](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Document bewerkingen](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Video's en zelfstudies over het Azure Search](search-video-demo-tutorial-list.md)
* [Meervoudige navigatie in Azure Search](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
