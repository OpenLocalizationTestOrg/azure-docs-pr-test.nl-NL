---
title: aaa "query uitvoeren in een index (.NET API - Azure Search) | Microsoft Docs'
description: Een zoekopdracht in Azure search samenstellen en gebruiken van parameters toofilter en sorteren search zoekresultaten.
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="9c6f8-103">Query uitvoeren op uw Azure Search-index met behulp van Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9c6f8-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c6f8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9c6f8-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9c6f8-105">Portal</span><span class="sxs-lookup"><span data-stu-id="9c6f8-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9c6f8-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9c6f8-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9c6f8-107">REST</span><span class="sxs-lookup"><span data-stu-id="9c6f8-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="9c6f8-108">In dit artikel leert u hoe uw index met behulp tooquery Hallo [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="9c6f8-109">Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md) en moet deze index [gevuld zijn met gegevens](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c6f8-110">Alle voorbeeldcode in dit artikel is geschreven in C#.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="9c6f8-111">U vindt de volledige broncode Hallo [op GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="9c6f8-112">U kunt ook lezen over Hallo [Azure Search .NET SDK](search-howto-dotnet-sdk.md) voor een meer gedetailleerde doorloop van Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="9c6f8-113">De query api-sleutel voor de Azure Search-service vaststellen</span><span class="sxs-lookup"><span data-stu-id="9c6f8-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="9c6f8-114">Nu u een Azure Search-index hebt gemaakt, bent u bijna klaar tooissue query's op basis van Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="9c6f8-115">Eerst moet u tooobtain een Hallo query api-sleutels die is gegenereerd voor Hallo zoekservice die u hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="9c6f8-116">Hallo .NET SDK verzendt deze api-sleutel voor elke aanvraag tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="9c6f8-117">Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="9c6f8-118">toofind api-sleutels met uw service u zich in toohello aanmelden kunt [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9c6f8-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9c6f8-119">Blade Ga tooyour Azure Search service</span><span class="sxs-lookup"><span data-stu-id="9c6f8-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="9c6f8-120">Klik op Hallo 'Sleutels'-pictogram</span><span class="sxs-lookup"><span data-stu-id="9c6f8-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="9c6f8-121">Uw service heeft zowel *administratorsleutels* als *querysleutels*.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9c6f8-122">De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9c6f8-123">Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="9c6f8-124">Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="9c6f8-125">Voor de toepassing hello van query's op een index, kunt u een van de query-sleutel.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="9c6f8-126">De administratorsleutels kunnen ook worden gebruikt voor query's, maar moet u een querysleutel in uw toepassingscode als dit beter Hallo volgt [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="9c6f8-127">Maak een instantie van klasse SearchIndexClient Hallo</span><span class="sxs-lookup"><span data-stu-id="9c6f8-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="9c6f8-128">query's tooissue Hello Azure Search .NET SDK, moet u een exemplaar van Hallo toocreate `SearchIndexClient` klasse.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="9c6f8-129">Deze klasse heeft verschillende constructors.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-129">This class has several constructors.</span></span> <span data-ttu-id="9c6f8-130">Hallo gewenste neemt uw naam zoekservice, de naam van de index en een `SearchCredentials` object als parameters.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="9c6f8-131">`SearchCredentials` verpakt uw api-sleutel.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="9c6f8-132">Hallo-code hieronder maakt u een nieuwe `SearchIndexClient` voor de index "hotels" hello (gemaakt in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md)) met waarden voor Hallo zoeken servicenaam en api-sleutel die zijn opgeslagen in de configuratie van de toepassing hello bestand (`appsettings.json` in geval van Hallo Hallo [voorbeeldtoepassing](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="9c6f8-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="9c6f8-133">`SearchIndexClient` heeft een `Documents`-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="9c6f8-134">Deze eigenschap bevat dat alle methoden die u nodig hebt tooquery Azure Search-index Hallo.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="9c6f8-135">Een query uitvoeren in uw index</span><span class="sxs-lookup"><span data-stu-id="9c6f8-135">Query your index</span></span>
<span data-ttu-id="9c6f8-136">Zoeken met Hallo .NET SDK is net zo eenvoudig als aanroepen Hallo `Documents.Search` methode op uw `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="9c6f8-137">Deze methode heeft een aantal parameters, waaronder de zoektekst hello, samen met een `SearchParameters` -object dat gebruikt toofurther verfijnen Hallo query worden kan.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="9c6f8-138">Typen query 's</span><span class="sxs-lookup"><span data-stu-id="9c6f8-138">Types of Queries</span></span>
<span data-ttu-id="9c6f8-139">Hallo twee main [querytypen](search-query-overview.md#types-of-queries) gewenste zijn `search` en `filter`.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="9c6f8-140">Een `search`-query zoekt naar een of meer voorwaarden in alle *doorzoekbare* velden in de index.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="9c6f8-141">Een `filter`-query evalueert een Booleaanse expressie op alle *filterbare* velden in een index.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="9c6f8-142">Zowel zoekopdrachten en filters worden uitgevoerd met behulp van Hallo `Documents.Search` methode.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="9c6f8-143">Een zoekopdracht kan worden doorgegeven aan Hallo `searchText` parameter, terwijl een filterexpressie kan worden doorgegeven aan Hallo `Filter` eigenschap Hallo `SearchParameters` klasse.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="9c6f8-144">toofilter zonder te zoeken, geeft `"*"` voor Hallo `searchText` parameter.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="9c6f8-145">toosearch zonder te filteren, stelt u Hallo `Filter` eigenschap niet in of niet doorgegeven een `SearchParameters` instantie.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="9c6f8-146">Voorbeelden van query 's</span><span class="sxs-lookup"><span data-stu-id="9c6f8-146">Example Queries</span></span>
<span data-ttu-id="9c6f8-147">Hallo volgende voorbeeldcode ziet u een aantal verschillende manieren tooquery Hallo "hotels" index die is gedefinieerd in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="9c6f8-148">Hallo documenten die worden geretourneerd met Hallo zoekresultaten zijn instanties van Hallo `Hotel` klasse, die is gedefinieerd in [gegevens importeren in met behulp van Azure Search .NET SDK Hallo](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="9c6f8-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="9c6f8-149">Hallo voorbeeldcode maakt gebruik van een `WriteDocuments` methode toooutput Hallo zoeken resultaten toohello console.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="9c6f8-150">Deze methode wordt beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="9c6f8-151">Zoekresultaten verwerken</span><span class="sxs-lookup"><span data-stu-id="9c6f8-151">Handle search results</span></span>
<span data-ttu-id="9c6f8-152">Hallo `Documents.Search` methode retourneert een `DocumentSearchResult` -object dat Hallo resultaten van Hallo query bevat.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="9c6f8-153">Hallo-voorbeeld in de vorige sectie Hallo gebruikgemaakt van een methode aangeroepen `WriteDocuments` toooutput Hallo search-resultaten toohello console:</span><span class="sxs-lookup"><span data-stu-id="9c6f8-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="9c6f8-154">Hier ziet u wat Hallo resultaten eruitzien zoals voor Hallo query's in de vorige sectie hello, uitgaande Hallo "hotels" index is gevuld met de voorbeeldgegevens Hallo in [gegevens importeren in met behulp van Azure Search .NET SDK Hallo](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="9c6f8-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="9c6f8-155">bovenstaande Hallo voorbeeldcode maakt gebruik van Hallo console toooutput zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="9c6f8-156">U moet ook zoekresultaten toodisplay in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="9c6f8-157">Zie [dit voorbeeld op GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) voor een voorbeeld van hoe toorender in een ASP.NET MVC-gebaseerde webtoepassing zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="9c6f8-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

