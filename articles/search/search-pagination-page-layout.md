---
title: Hoe zoekresultaten in Azure Search | Microsoft Docs
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
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="c8a46-103">Pagina's met zoekresultaten maken in Azure Search</span><span class="sxs-lookup"><span data-stu-id="c8a46-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="c8a46-104">In dit artikel biedt richtlijnen voor het gebruik van de Azure Search Service REST API voor het implementeren van standaardelementen van een pagina met zoekresultaten, zoals het totale aantal, document ophalen, sorteervolgorde en navigatie.</span><span class="sxs-lookup"><span data-stu-id="c8a46-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="c8a46-105">In elk geval hieronder vermelde opties voor pagina's gerelateerde bijdragen of gegevens naar de pagina met zoekresultaten worden opgegeven via de [zoekdocument](http://msdn.microsoft.com/library/azure/dn798927.aspx) aanvragen die naar uw Azure Search-Service verzonden.</span><span class="sxs-lookup"><span data-stu-id="c8a46-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="c8a46-106">Aanvragen bevatten een GET-opdracht, pad, en queryparameters die informeren over de service wat wordt aangevraagd en hoe u het antwoord formuleren.</span><span class="sxs-lookup"><span data-stu-id="c8a46-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="c8a46-107">Een geldige aanvraag bevat een aantal elementen, zoals een service-URL en het pad, HTTP-term `api-version`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c8a46-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="c8a46-108">Als beknopt alternatief bevat, wordt de voorbeelden om uit te lichten alleen de syntaxis die relevant is voor paginering bijgesneden.</span><span class="sxs-lookup"><span data-stu-id="c8a46-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="c8a46-109">Zie de [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentatie voor meer informatie over de syntaxis van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c8a46-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="c8a46-110">Totaal aantal treffers en het aantal paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="c8a46-110">Total hits and Page Counts</span></span>
<span data-ttu-id="c8a46-111">Het totale aantal resultaten geretourneerd door een query wordt weergegeven en vervolgens de resultaten te retourneren in kleinere reeksen is van cruciaal belang op vrijwel alle pagina's voor zoeken.</span><span class="sxs-lookup"><span data-stu-id="c8a46-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="c8a46-112">In Azure Search, gebruikt u de `$count`, `$top`, en `$skip` parameters om deze waarden te retourneren.</span><span class="sxs-lookup"><span data-stu-id="c8a46-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="c8a46-113">Het volgende voorbeeld toont een voorbeeld van een aanvraag voor het totaal aantal treffers geretourneerd als `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="c8a46-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="c8a46-114">Documenten in groepen van 15 ophalen en het totaal aantal treffers, beginnend bij de eerste pagina worden ook weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c8a46-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="c8a46-115">Resultaten pagineren vereist zowel `$top` en `$skip`, waarbij `$top` Hiermee geeft u op hoeveel items om te retourneren in een batch en `$skip` Hiermee geeft u op hoeveel items om over te slaan.</span><span class="sxs-lookup"><span data-stu-id="c8a46-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="c8a46-116">In het volgende voorbeeld wordt elke pagina bevat de volgende 15 items aangegeven door de incrementele jumps in de `$skip` parameter.</span><span class="sxs-lookup"><span data-stu-id="c8a46-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="c8a46-117">Lay-out</span><span class="sxs-lookup"><span data-stu-id="c8a46-117">Layout</span></span>
<span data-ttu-id="c8a46-118">Op een pagina met zoekresultaten, is het raadzaam om een miniatuur, een subset van velden en een koppeling naar een product met volledig pagina weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c8a46-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="c8a46-119">U wilt gebruiken in Azure Search `$select` en een lookup-opdracht voor het implementeren van deze ervaring.</span><span class="sxs-lookup"><span data-stu-id="c8a46-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="c8a46-120">Een subset van velden voor een naast elkaar indeling geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="c8a46-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="c8a46-121">Installatiekopieën en media-bestanden zijn niet rechtstreeks kan worden doorzocht en moeten worden opgeslagen in een ander platform van de opslag, zoals Azure Blob-opslag om kosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="c8a46-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="c8a46-122">Definieer een veld waarin de URL-adres van de externe inhoud opgeslagen in de index en documenten.</span><span class="sxs-lookup"><span data-stu-id="c8a46-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="c8a46-123">Vervolgens kunt u het veld als een verwijzing naar afbeelding.</span><span class="sxs-lookup"><span data-stu-id="c8a46-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="c8a46-124">De URL van de afbeelding moet in het document.</span><span class="sxs-lookup"><span data-stu-id="c8a46-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="c8a46-125">Voor het ophalen van een product beschrijvingspagina voor een **onClick** gebeurtenis, gebruik [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) om door te geven in de sleutel van het document om op te halen.</span><span class="sxs-lookup"><span data-stu-id="c8a46-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="c8a46-126">Het gegevenstype van de sleutel is `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="c8a46-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="c8a46-127">In dit voorbeeld is het *246810*.</span><span class="sxs-lookup"><span data-stu-id="c8a46-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="c8a46-128">Sorteren op relevantie, classificatie of prijs</span><span class="sxs-lookup"><span data-stu-id="c8a46-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="c8a46-129">Sorteervolgorde vaak standaard op relevantie, maar het is gebruikelijk om alternatieve sorteren orders gemakkelijk beschikbaar maken zodat klanten snel bestaande resultaten naar een andere volgorde van de waarden van positie verplaatsen kunnen.</span><span class="sxs-lookup"><span data-stu-id="c8a46-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="c8a46-130">In Azure Search sorteren is gebaseerd op de `$orderby` expressie, voor alle velden die zijn geïndexeerd als`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="c8a46-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="c8a46-131">Relevantie is ten zeerste aan score berekenen voor profielen gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c8a46-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="c8a46-132">Kunt u het standaard scoren die afhankelijk is van de analyse van tekst en statistieken rangschikken volgorde alle resultaten met hogere scores gebeurt met documenten met meer of sterker komt overeen met een zoekterm.</span><span class="sxs-lookup"><span data-stu-id="c8a46-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="c8a46-133">Alternatieve sorteervolgorde zijn meestal gekoppeld aan **onClick** gebeurtenissen die terugbellen naar een methode die de sorteervolgorde is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="c8a46-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="c8a46-134">Bijvoorbeeld, krijgt deze pagina-element:</span><span class="sxs-lookup"><span data-stu-id="c8a46-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="c8a46-135">Maakt u een methode die de geselecteerde sorteeroptie als invoer accepteert en retourneert een geordende lijst voor de criteria gekoppeld aan die optie.</span><span class="sxs-lookup"><span data-stu-id="c8a46-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="c8a46-136">De standaard score berekenen is voldoende voor veel scenario's, wordt u aangeraden relevantie in plaats daarvan op een aangepaste scoreprofiel baseert.</span><span class="sxs-lookup"><span data-stu-id="c8a46-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="c8a46-137">Een aangepaste scoreprofiel biedt u een manier versterking items meer nuttig zijn voor uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="c8a46-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="c8a46-138">Zie [een scoreprofiel toevoegen](http://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c8a46-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="c8a46-139">Facetnavigatie</span><span class="sxs-lookup"><span data-stu-id="c8a46-139">Faceted navigation</span></span>
<span data-ttu-id="c8a46-140">Zoeken navigatie is gebruikelijk dat op een pagina met zoekresultaten, vaak zich bevindt op de bovenkant van de pagina of.</span><span class="sxs-lookup"><span data-stu-id="c8a46-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="c8a46-141">In Azure Search biedt facetnavigatie zelf gerichte zoeken op basis van vooraf gedefinieerde filters.</span><span class="sxs-lookup"><span data-stu-id="c8a46-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="c8a46-142">Zie [facetnavigatie in Azure Search](search-faceted-navigation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c8a46-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="c8a46-143">Filters op paginaniveau</span><span class="sxs-lookup"><span data-stu-id="c8a46-143">Filters at the page level</span></span>
<span data-ttu-id="c8a46-144">Als uw ontwerp van de oplossing opgenomen toegewezen zoekpagina's voor specifieke typen inhoud (bijvoorbeeld, een online retail toepassing met afdelingen weergegeven boven aan de pagina), kunt u een filterexpressie naast een **onClick**gebeurtenis om een pagina openen in een vooraf gefilterde staat.</span><span class="sxs-lookup"><span data-stu-id="c8a46-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="c8a46-145">U kunt een filter met of zonder een zoekexpressie verzenden.</span><span class="sxs-lookup"><span data-stu-id="c8a46-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="c8a46-146">De volgende aanvraag wordt bijvoorbeeld filteren op naam van het merk, alleen documenten die overeenkomen met het retourneren.</span><span class="sxs-lookup"><span data-stu-id="c8a46-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="c8a46-147">Zie [documenten zoeken (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) voor meer informatie over `$filter` expressies.</span><span class="sxs-lookup"><span data-stu-id="c8a46-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="c8a46-148">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c8a46-148">See Also</span></span>
* [<span data-ttu-id="c8a46-149">Azure Search Service REST-API</span><span class="sxs-lookup"><span data-stu-id="c8a46-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="c8a46-150">Indexbewerkingen</span><span class="sxs-lookup"><span data-stu-id="c8a46-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="c8a46-151">Document bewerkingen</span><span class="sxs-lookup"><span data-stu-id="c8a46-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="c8a46-152">Video's en zelfstudies over het Azure Search</span><span class="sxs-lookup"><span data-stu-id="c8a46-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="c8a46-153">Meervoudige navigatie in Azure Search</span><span class="sxs-lookup"><span data-stu-id="c8a46-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
