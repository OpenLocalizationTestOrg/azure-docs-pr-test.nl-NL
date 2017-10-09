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
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="7746b-103">Hoe toopage zoekresultaten in Azure Search</span><span class="sxs-lookup"><span data-stu-id="7746b-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="7746b-104">In dit artikel biedt richtlijnen voor hoe toouse hello Azure Search Service REST API tooimplement standaardelementen van een zoekopdracht resultaten pagina, zoals het totale aantal, document ophalen, sorteervolgorde en navigatie.</span><span class="sxs-lookup"><span data-stu-id="7746b-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="7746b-105">In elk geval hieronder vermelde opties voor pagina's gerelateerde gegevens of informatie tooyour zoekresultatenpagina bijdragen worden opgegeven via Hallo [zoekdocument](http://msdn.microsoft.com/library/azure/dn798927.aspx) aanvragen verzonden tooyour Azure Search-Service.</span><span class="sxs-lookup"><span data-stu-id="7746b-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="7746b-106">Aanvragen bevatten een GET-opdracht, pad, en queryparameters die informeren Hallo service wat wordt aangevraagd en hoe tooformulate Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="7746b-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="7746b-107">Een geldige aanvraag bevat een aantal elementen, zoals een service-URL en het pad, HTTP-term `api-version`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="7746b-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="7746b-108">We bijgesneden Hallo voorbeelden toohighlight alleen Hallo syntaxis relevante toopagination voor beknopt alternatief bevat.</span><span class="sxs-lookup"><span data-stu-id="7746b-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="7746b-109">Zie Hallo [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentatie voor meer informatie over de syntaxis van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="7746b-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="7746b-110">Totaal aantal treffers en het aantal paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="7746b-110">Total hits and Page Counts</span></span>
<span data-ttu-id="7746b-111">Hallo totaal aantal resultaten geretourneerd door een query en vervolgens te retourneren die resulteert in kleinere reeksen wordt weergegeven, is de fundamentele toovirtually alle zoekpagina's.</span><span class="sxs-lookup"><span data-stu-id="7746b-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="7746b-112">In Azure Search, gebruikt u Hallo `$count`, `$top`, en `$skip` parameters tooreturn deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7746b-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="7746b-113">Hallo volgende voorbeeld ziet u een voorbeeld van een aanvraag voor het totaal aantal treffers geretourneerd als `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="7746b-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="7746b-114">Documenten in groepen van 15 ophalen en totaal aantal treffers hello, beginnend bij de eerste pagina Hallo worden ook weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7746b-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="7746b-115">Resultaten pagineren vereist zowel `$top` en `$skip`, waarbij `$top` Hiermee geeft u op hoeveel items tooreturn in een batch en `$skip` Hiermee geeft u op hoeveel items tooskip.</span><span class="sxs-lookup"><span data-stu-id="7746b-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="7746b-116">In Hallo bijvoorbeeld na elke pagina Hallo naast 15 worden artikelen weergegeven, aangegeven door Hallo incrementele jumps in Hallo `$skip` parameter.</span><span class="sxs-lookup"><span data-stu-id="7746b-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="7746b-117">Lay-out</span><span class="sxs-lookup"><span data-stu-id="7746b-117">Layout</span></span>
<span data-ttu-id="7746b-118">Op een pagina met zoekresultaten, kunt u tooshow een miniatuur, een subset van velden en een koppeling tooa product met volledig pagina.</span><span class="sxs-lookup"><span data-stu-id="7746b-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="7746b-119">U wilt gebruiken in Azure Search `$select` en een lookup-opdracht tooimplement deze ervaring.</span><span class="sxs-lookup"><span data-stu-id="7746b-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="7746b-120">tooreturn een subset van velden voor een naast elkaar indeling:</span><span class="sxs-lookup"><span data-stu-id="7746b-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="7746b-121">Afbeeldingen en media-bestanden zijn niet rechtstreeks kan worden doorzocht en moeten worden opgeslagen in een ander platform van de opslag, zoals Azure Blob storage, tooreduce kosten.</span><span class="sxs-lookup"><span data-stu-id="7746b-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="7746b-122">Definieer een veld waarin de URL-adres van de externe inhoud Hallo Hallo in Hallo-index en documenten.</span><span class="sxs-lookup"><span data-stu-id="7746b-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="7746b-123">U kunt vervolgens Hallo veld gebruiken als een verwijzing naar afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7746b-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="7746b-124">Hallo URL toohello installatiekopie moet Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="7746b-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="7746b-125">tooretrieve een productbeschrijving pagina voor een **onClick** gebeurtenis, gebruik [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in Hallo Hallo document tooretrieve sleutel.</span><span class="sxs-lookup"><span data-stu-id="7746b-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="7746b-126">Hallo-gegevenstype van het Hallo-sleutel is `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="7746b-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="7746b-127">In dit voorbeeld is het *246810*.</span><span class="sxs-lookup"><span data-stu-id="7746b-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="7746b-128">Sorteren op relevantie, classificatie of prijs</span><span class="sxs-lookup"><span data-stu-id="7746b-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="7746b-129">Sorteervolgorde vaak toorelevance standaard, maar het algemene toomake alternatieve sorteervolgorde direct beschikbaar is, zodat klanten snel bestaande resultaten naar een andere volgorde van de waarden van positie verplaatsen kunnen.</span><span class="sxs-lookup"><span data-stu-id="7746b-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="7746b-130">In Azure Search sorteren is gebaseerd op Hallo `$orderby` expressie, voor alle velden die zijn geïndexeerd als`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="7746b-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="7746b-131">Relevantie is ten zeerste aan score berekenen voor profielen gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="7746b-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="7746b-132">U kunt gebruiken Hallo standaard score berekenen, die afhankelijk is van tekst analyse en statistieken toorank bestellen alle resultaten met hogere scores gebeurt toodocuments met meer of sterker komt overeen met een zoekterm.</span><span class="sxs-lookup"><span data-stu-id="7746b-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="7746b-133">Alternatieve sorteervolgorde zijn meestal gekoppeld aan **onClick** Hallo sorteervolgorde gebeurtenissen die terugbellen tooa methode die is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="7746b-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="7746b-134">Bijvoorbeeld, krijgt deze pagina-element:</span><span class="sxs-lookup"><span data-stu-id="7746b-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="7746b-135">Maakt u een methode die de sorteeroptie Hallo geselecteerd als invoer accepteert en retourneert een geordende lijst voor Hallo criteria die zijn gekoppeld aan die optie.</span><span class="sxs-lookup"><span data-stu-id="7746b-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="7746b-136">Hallo standaard score berekenen is voldoende voor veel scenario's, wordt u aangeraden relevantie in plaats daarvan op een aangepaste scoreprofiel baseert.</span><span class="sxs-lookup"><span data-stu-id="7746b-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="7746b-137">Een aangepaste scoreprofiel biedt een manier tooboost items meer nuttige tooyour bedrijven.</span><span class="sxs-lookup"><span data-stu-id="7746b-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="7746b-138">Zie [een scoreprofiel toevoegen](http://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7746b-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="7746b-139">Facetnavigatie</span><span class="sxs-lookup"><span data-stu-id="7746b-139">Faceted navigation</span></span>
<span data-ttu-id="7746b-140">Zoeken navigatie is gebruikelijk dat op een pagina met zoekresultaten, vaak zich bevindt op Hallo zijde of begin van een pagina.</span><span class="sxs-lookup"><span data-stu-id="7746b-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="7746b-141">In Azure Search biedt facetnavigatie zelf gerichte zoeken op basis van vooraf gedefinieerde filters.</span><span class="sxs-lookup"><span data-stu-id="7746b-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="7746b-142">Zie [facetnavigatie in Azure Search](search-faceted-navigation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7746b-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="7746b-143">Filters op Hallo paginaniveau</span><span class="sxs-lookup"><span data-stu-id="7746b-143">Filters at hello page level</span></span>
<span data-ttu-id="7746b-144">Als uw ontwerp van de oplossing opgenomen toegewezen zoekpagina's voor specifieke typen inhoud (bijvoorbeeld, een online retail toepassing met afdelingen bovenaan Hallo Hallo pagina vermeld), kunt u een filterexpressie naast een **onClick** gebeurtenis tooopen een pagina in een vooraf gefilterde staat.</span><span class="sxs-lookup"><span data-stu-id="7746b-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="7746b-145">U kunt een filter met of zonder een zoekexpressie verzenden.</span><span class="sxs-lookup"><span data-stu-id="7746b-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="7746b-146">Bijvoorbeeld worden hello volgende aanvraag gefilterd op de naam van het merk, alleen documenten die overeenkomen met het retourneren.</span><span class="sxs-lookup"><span data-stu-id="7746b-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="7746b-147">Zie [documenten zoeken (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) voor meer informatie over `$filter` expressies.</span><span class="sxs-lookup"><span data-stu-id="7746b-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="7746b-148">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7746b-148">See Also</span></span>
* [<span data-ttu-id="7746b-149">Azure Search Service REST-API</span><span class="sxs-lookup"><span data-stu-id="7746b-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="7746b-150">Indexbewerkingen</span><span class="sxs-lookup"><span data-stu-id="7746b-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="7746b-151">Document bewerkingen</span><span class="sxs-lookup"><span data-stu-id="7746b-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="7746b-152">Video's en zelfstudies over het Azure Search</span><span class="sxs-lookup"><span data-stu-id="7746b-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="7746b-153">Meervoudige navigatie in Azure Search</span><span class="sxs-lookup"><span data-stu-id="7746b-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
