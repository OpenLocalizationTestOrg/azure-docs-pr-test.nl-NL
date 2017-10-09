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
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="b6cd9-103">Het uploaden van gegevens tooAzure zoeken met Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="b6cd9-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="b6cd9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b6cd9-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="b6cd9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b6cd9-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="b6cd9-106">REST</span><span class="sxs-lookup"><span data-stu-id="b6cd9-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="b6cd9-107">In dit artikel wordt uitgelegd hoe u toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport gegevens in een Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="b6cd9-108">Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="b6cd9-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="b6cd9-109">In de volgorde toopush documenten in uw index met behulp van Hallo REST-API, doet u een HTTP POST-aanvraag tooyour index URL-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="b6cd9-110">Hallo-hoofdtekst van Hallo HTTP-aanvraag hoofdtekst is een JSON-object met Hallo documenten toobe toegevoegd, gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="b6cd9-111">De admin api-sleutel voor de Azure Search-service vaststellen</span><span class="sxs-lookup"><span data-stu-id="b6cd9-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="b6cd9-112">Bij de uitgifte van HTTP-aanvragen op basis van uw service met behulp van Hallo REST API, *elke* API-aanvraag vergezeld gaan van Hallo api-sleutel die is gegenereerd voor Hallo Search-service die u hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="b6cd9-113">Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="b6cd9-114">toofind van uw service api-sleutels, kunt u aanmelden toohello [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b6cd9-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="b6cd9-115">Blade Ga tooyour Azure Search service</span><span class="sxs-lookup"><span data-stu-id="b6cd9-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="b6cd9-116">Klik op Hallo 'Sleutels'-pictogram</span><span class="sxs-lookup"><span data-stu-id="b6cd9-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="b6cd9-117">Uw service heeft zowel *administratorsleutels* als *querysleutels*.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="b6cd9-118">De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="b6cd9-119">Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="b6cd9-120">Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="b6cd9-121">Voor de toepassing hello gegevens te importeren in een index, kunt u ofwel de primaire of secundaire administratorsleutel.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="b6cd9-122">Bepaal welke indexering actie toouse</span><span class="sxs-lookup"><span data-stu-id="b6cd9-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="b6cd9-123">Wanneer u Hallo REST-API gebruikt, doet u HTTP POST-aanvragen met JSON-aanvraag instanties tooyour Azure Search-index van de eindpunt-URL.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="b6cd9-124">Hallo JSON-object in de hoofdtekst van uw HTTP-aanvraag bevat een JSON-matrix met de naam 'waarde' bevat JSON-objecten die u wilt dat tooadd tooyour index documenten vertegenwoordigt, bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="b6cd9-125">Elk JSON-object in de matrix '' waarde '' Hallo vertegenwoordigt een document toobe geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="b6cd9-126">Elk van deze objecten van het document Hallo sleutel bevat en geeft indexeerbewerking Hallo gewenst (uploaden, samenvoegen, verwijderen, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="b6cd9-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="b6cd9-127">Afhankelijk van welke van Hallo onderstaande bewerkingen die u kiest, moet alleen bepaalde velden voor elk document opnemen:</span><span class="sxs-lookup"><span data-stu-id="b6cd9-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="b6cd9-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b6cd9-128">Description</span></span> | <span data-ttu-id="b6cd9-129">Vereiste velden voor elk document</span><span class="sxs-lookup"><span data-stu-id="b6cd9-129">Necessary fields for each document</span></span> | <span data-ttu-id="b6cd9-130">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b6cd9-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="b6cd9-131">Een `upload` actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="b6cd9-132">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="b6cd9-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="b6cd9-133">Wanneer het bijwerken/vervangen van een bestaand document wordt elk veld dat niet is opgegeven in de aanvraag Hallo hebt ingesteld te`null`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="b6cd9-134">Dit gebeurt zelfs als Hallo veld eerder tooa null-waarde is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="b6cd9-135">Een bestaand document met het Hallo updates opgegeven velden.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="b6cd9-136">Als Hallo document niet in de index hello bestaat, mislukt de Hallo samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="b6cd9-137">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="b6cd9-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="b6cd9-138">Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="b6cd9-139">ook velden van het type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="b6cd9-140">Bijvoorbeeld, als hello document bevat een veld `tags` met waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor `tags`, uiteindelijke waarde van Hallo Hallo `tags` veld `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="b6cd9-141">Het wordt dus niet `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="b6cd9-142">Deze bewerking gedraagt zich als `merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="b6cd9-143">Als het Hallo-document niet bestaat, gedraagt zich als `upload` met een nieuw document.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="b6cd9-144">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="b6cd9-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="b6cd9-145">Verwijdert het opgegeven document Hallo van Hallo index.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="b6cd9-146">alleen sleutel</span><span class="sxs-lookup"><span data-stu-id="b6cd9-146">key only</span></span> |<span data-ttu-id="b6cd9-147">Alle velden die u opgeeft dan Hallo sleutelveld worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="b6cd9-148">Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `merge` en stelt u Hallo veld expliciet toonull.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="b6cd9-149">De HTTP-aanvraag en de hoofdtekst opstellen</span><span class="sxs-lookup"><span data-stu-id="b6cd9-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="b6cd9-150">Nu dat u de benodigde veldwaarden Hallo hebt verzameld voor uw indexbewerkingen, u bent klaar tooconstruct Hallo werkelijke HTTP-aanvraag en JSON-aanvraag hoofdtekst tooimport uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="b6cd9-151">Aanvragen en aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="b6cd9-151">Request and Request Headers</span></span>
<span data-ttu-id="b6cd9-152">Hallo-URL, moet u tooprovide de servicenaam, de indexnaam ("hotels" in dit geval), evenals Hallo juiste API-versie (Hallo huidige API-versie is `2016-09-01` op Hallo moment van publicatie van dit document).</span><span class="sxs-lookup"><span data-stu-id="b6cd9-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="b6cd9-153">U moet toodefine hello `Content-Type` en `api-key` aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="b6cd9-154">Voor deze laatste Hallo, een van de administratorsleutels van uw service te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="b6cd9-155">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="b6cd9-155">Request Body</span></span>
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

<span data-ttu-id="b6cd9-156">In dit geval gebruiken we `upload`, `mergeOrUpload` en `delete` als onze zoekacties.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="b6cd9-157">We gaan ervan uit dat deze voorbeeldindex "hotels" al is gevuld met een aantal documenten.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="b6cd9-158">Hoe we hoefden niet toospecify alle mogelijke documentvelden Hallo bij gebruik van `mergeOrUpload` en hoe we alleen opgegeven Hallo documentsleutel (`hotelId`) bij gebruik van `delete`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="b6cd9-159">Bovendien opmerking die u alleen hoger too1000 documenten (of 16 MB) in een enkele indexeringsaanvraag opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="b6cd9-160">De HTTP-antwoordcode begrijpen</span><span class="sxs-lookup"><span data-stu-id="b6cd9-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="b6cd9-161">200</span><span class="sxs-lookup"><span data-stu-id="b6cd9-161">200</span></span>
<span data-ttu-id="b6cd9-162">Na een geslaagde indexeringsaanvraag ontvangt u een HTTP-antwoord met de statuscode `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="b6cd9-163">Hallo JSON-hoofdtekst van Hallo HTTP-antwoord is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b6cd9-163">hello JSON body of hello HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="b6cd9-164">207</span><span class="sxs-lookup"><span data-stu-id="b6cd9-164">207</span></span>
<span data-ttu-id="b6cd9-165">Statuscode `207` wordt geretourneerd wanneer ten minste één item is niet geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="b6cd9-166">Hallo JSON-hoofdtekst van Hallo HTTP-antwoord bevat informatie over mislukte Hallo-documenten.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

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
> <span data-ttu-id="b6cd9-167">Dit betekent vaak dat load Hallo op uw zoekopdracht service een waarbij tooreturn indexeringsaanvragen punt bereikt `503` reacties.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="b6cd9-168">In dit geval is het aanbevolen om de clientcode uit te stellen en te wachten voordat u het opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="b6cd9-169">Hierdoor krijgt Hallo system sommige toorecover tijd, Hallo kans dat toekomstige aanvragen waarschijnlijk wel mogelijk verhogen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="b6cd9-170">Uw verzoeken om snel opnieuw uit te voeren, wordt alleen Hallo situatie verlengen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="b6cd9-171">429</span><span class="sxs-lookup"><span data-stu-id="b6cd9-171">429</span></span>
<span data-ttu-id="b6cd9-172">Statuscode `429` wordt geretourneerd wanneer u het quotum van Hallo aantal documenten per index hebt overschreden.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="b6cd9-173">503</span><span class="sxs-lookup"><span data-stu-id="b6cd9-173">503</span></span>
<span data-ttu-id="b6cd9-174">Statuscode `503` wordt geretourneerd als geen van de items in aanvraag Hallo Hallo zijn geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="b6cd9-175">Deze fout betekent dat Hallo-systeem zwaar belast wordt en uw aanvraag op dit moment niet worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="b6cd9-176">In dit geval is het aanbevolen om de clientcode uit te stellen en te wachten voordat u het opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="b6cd9-177">Hierdoor krijgt Hallo system sommige toorecover tijd, Hallo kans dat toekomstige aanvragen waarschijnlijk wel mogelijk verhogen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="b6cd9-178">Uw verzoeken om snel opnieuw uit te voeren, wordt alleen Hallo situatie verlengen.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="b6cd9-179">Zie [Documenten toevoegen, bijwerken of verwijderen](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) voor meer informatie over bewerkingen en antwoorden voor een geslaagde of mislukte bewerking.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="b6cd9-180">Zie [HTTP-statuscodes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) voor meer informatie over andere HTTP-statuscodes die kunnen worden geretourneerd in geval van storing.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6cd9-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6cd9-181">Next steps</span></span>
<span data-ttu-id="b6cd9-182">Na het vullen van uw Azure Search-index, zult u gereed toostart uitgeven van query's toosearch voor documenten.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="b6cd9-183">Zie [Een query uitvoeren in uw Azure-zoekindex](search-query-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b6cd9-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
