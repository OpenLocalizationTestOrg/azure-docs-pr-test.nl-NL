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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="15464-103">Query uitvoeren op uw Azure Search-index met behulp van Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="15464-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="15464-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="15464-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="15464-105">Portal</span><span class="sxs-lookup"><span data-stu-id="15464-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="15464-106">.NET</span><span class="sxs-lookup"><span data-stu-id="15464-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="15464-107">REST</span><span class="sxs-lookup"><span data-stu-id="15464-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="15464-108">Dit artikel laat zien hoe uw index met behulp tooquery Hallo [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="15464-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="15464-109">Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md) en moet deze index [gevuld zijn met gegevens](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="15464-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="15464-110">Zie [How full text search works in Azure Search](search-lucene-query-architecture.md) (Hoe zoeken in volledige tekst werkt in Azure Search) voor achtergrondinformatie.</span><span class="sxs-lookup"><span data-stu-id="15464-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="15464-111">De query api-sleutel voor de Azure Search-service vaststellen</span><span class="sxs-lookup"><span data-stu-id="15464-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="15464-112">Een belangrijk onderdeel van elke zoekbewerking in hello Azure Search REST API is Hallo *api-sleutel* die is gegenereerd voor Hallo-service die u hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="15464-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="15464-113">Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.</span><span class="sxs-lookup"><span data-stu-id="15464-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="15464-114">toofind van uw service api-sleutels, kunt u aanmelden toohello [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="15464-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="15464-115">Blade Ga tooyour Azure Search service</span><span class="sxs-lookup"><span data-stu-id="15464-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="15464-116">Klik op het pictogram 'Sleutels' Hallo</span><span class="sxs-lookup"><span data-stu-id="15464-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="15464-117">Uw service heeft zowel *administratorsleutels* als *querysleutels*.</span><span class="sxs-lookup"><span data-stu-id="15464-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="15464-118">De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="15464-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="15464-119">Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.</span><span class="sxs-lookup"><span data-stu-id="15464-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="15464-120">Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.</span><span class="sxs-lookup"><span data-stu-id="15464-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="15464-121">Voor de toepassing hello van query's op een index, kunt u een van de query-sleutel.</span><span class="sxs-lookup"><span data-stu-id="15464-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="15464-122">De administratorsleutels kunnen ook worden gebruikt voor query's, maar moet u een querysleutel in uw toepassingscode als dit beter Hallo volgt [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="15464-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="15464-123">Uw query formuleren</span><span class="sxs-lookup"><span data-stu-id="15464-123">Formulate your query</span></span>
<span data-ttu-id="15464-124">Er zijn twee manieren ook[zoeken in uw index met behulp van Hallo REST-API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="15464-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="15464-125">Een manier is een HTTP POST-aanvraag tooissue waarbij uw queryparameters worden gedefinieerd in een JSON-object in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="15464-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="15464-126">Hallo andere manier is een HTTP GET-aanvraag tooissue waarbij uw queryparameters worden gedefinieerd binnen Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="15464-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="15464-127">POST heeft meer [versoepeld limieten](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) op Hallo grootte van de queryparameters dan GET.</span><span class="sxs-lookup"><span data-stu-id="15464-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="15464-128">Daarom wordt u aangeraden POST te gebruiken, tenzij er speciale omstandigheden zijn waarin het gebruik van GET beter zou zijn.</span><span class="sxs-lookup"><span data-stu-id="15464-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="15464-129">Voor zowel POST als GET moet u tooprovide uw *servicenaam*, *indexnaam*, en de juiste Hallo *API-versie* (Hallo huidige API-versie is `2016-09-01` Hallo gelijktijdig van de publicatie van dit document) in Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="15464-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="15464-130">Voor GET, Hallo *querytekenreeks* Hallo einde van Hallo-URL is waarin u Hallo queryparameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="15464-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="15464-131">Hieronder vindt u Hallo URL-indeling:</span><span class="sxs-lookup"><span data-stu-id="15464-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="15464-132">Hallo-indeling voor POST is hetzelfde hello, maar met alleen api-versie in de queryreeksparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="15464-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="15464-133">Voorbeelden van query 's</span><span class="sxs-lookup"><span data-stu-id="15464-133">Example Queries</span></span>
<span data-ttu-id="15464-134">Hier volgen een paar voorbeeldquery's op een index met de naam "hotels".</span><span class="sxs-lookup"><span data-stu-id="15464-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="15464-135">Deze query's worden weergegeven in zowel de GET als POST-indeling.</span><span class="sxs-lookup"><span data-stu-id="15464-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="15464-136">Hallo term 'budget' hello gehele index zoeken en alleen Hallo retourneren `hotelName` veld:</span><span class="sxs-lookup"><span data-stu-id="15464-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="15464-137">Een filter toohello index toofind hotels goedkoper dan €150 per nachten toepassen en retourneren Hallo `hotelId` en `description`:</span><span class="sxs-lookup"><span data-stu-id="15464-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="15464-138">Volledige zoekindex hello, volgorde op een bepaald veld (`lastRenovationDate`) Neem Hallo twee bovenste resultaten in aflopende volgorde, en alleen weergeven `hotelName` en `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="15464-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="15464-139">De HTTP-aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="15464-139">Submit your HTTP request</span></span>
<span data-ttu-id="15464-140">Nu u uw query hebt geformuleerd als onderdeel van uw HTTP-aanvraag-URL (voor GET) of hoofdtekst (voor POST), kunt u uw aanvraagheaders definiëren en uw query verzenden.</span><span class="sxs-lookup"><span data-stu-id="15464-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="15464-141">Aanvragen en aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="15464-141">Request and Request Headers</span></span>
<span data-ttu-id="15464-142">U moet twee aanvraagheaders definiëren voor GET en drie voor POST:</span><span class="sxs-lookup"><span data-stu-id="15464-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="15464-143">Hallo `api-key` header toohello querysleutel in stap I hierboven moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="15464-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="15464-144">U kunt ook een administratorsleutel gebruiken als Hallo `api-key` header, maar het wordt aanbevolen dat u een querysleutel gebruikt, aangezien deze exclusieve alleen alleen-lezentoegang tooindexes en -documenten.</span><span class="sxs-lookup"><span data-stu-id="15464-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="15464-145">Hallo `Accept` header moet worden ingesteld te`application/json`.</span><span class="sxs-lookup"><span data-stu-id="15464-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="15464-146">Alleen voor POST, Hallo `Content-Type` header ook te worden ingesteld`application/json`.</span><span class="sxs-lookup"><span data-stu-id="15464-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="15464-147">Hieronder vindt u een HTTP GET-aanvraag toosearch Hallo index "hotels met behulp van Azure Search REST API, met een eenvoudige query waarin wordt gezocht naar Hallo term 'motel' hello":</span><span class="sxs-lookup"><span data-stu-id="15464-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="15464-148">Hier volgt Hallo dezelfde voorbeeldquery, met behulp van HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="15464-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="15464-149">Een queryaanvraag is gelukt resulteert in een statuscode van `200 OK` en Hallo zoekresultaten worden geretourneerd als JSON in Hallo antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="15464-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="15464-150">Hier ziet u welke Hallo-resultaten voor Hallo hierboven query's eruit zien, ervan uitgaande dat index Hallo "hotels" is gevuld met de voorbeeldgegevens Hallo in [gegevens importeren in Azure Search met behulp van REST-API Hallo](search-import-data-rest-api.md) (Houd er rekening mee dat Hallo JSON is voor de duidelijkheid geformatteerd).</span><span class="sxs-lookup"><span data-stu-id="15464-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="15464-151">toolearn meer, gaat u naar Hallo "Antwoord" sectie van [documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="15464-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="15464-152">Zie [HTTP-statuscodes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) voor meer informatie over andere HTTP-statuscodes die kunnen worden geretourneerd in geval van storing.</span><span class="sxs-lookup"><span data-stu-id="15464-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
