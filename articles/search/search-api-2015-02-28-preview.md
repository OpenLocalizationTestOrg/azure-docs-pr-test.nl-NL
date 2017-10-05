---
title: Azure Search Service REST API-versie Preview 2015-02-28-| Microsoft Docs
description: Azure Search Service REST API-versie 2015-02-28-Preview bevat experimentele functies zoals natuurlijke Taalanalyse en moreLikeThis zoekopdrachten.
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="cf52c-103">Azure Search Service REST-API: Versie 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="cf52c-104">Dit artikel is de documentatie bij `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-105">Deze preview breidt de huidige versie van de algemeen beschikbaar [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), door de volgende experimentele functies:</span><span class="sxs-lookup"><span data-stu-id="cf52c-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="cf52c-106">`moreLikeThis`queryparameter in de [documenten zoeken](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="cf52c-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="cf52c-107">Het zoeken naar andere documenten die relevant voor een ander specifieke document zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="cf52c-108">Een paar extra onderdelen van de `2015-02-28-Preview` REST-API afzonderlijk worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="cf52c-109">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="cf52c-109">These include:</span></span>

* [<span data-ttu-id="cf52c-110">Score berekenen voor profielen</span><span class="sxs-lookup"><span data-stu-id="cf52c-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="cf52c-111">Indexeerfuncties</span><span class="sxs-lookup"><span data-stu-id="cf52c-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="cf52c-112">Azure Search-service is beschikbaar in meerdere versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="cf52c-113">Raadpleeg [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="cf52c-114">API's in dit document</span><span class="sxs-lookup"><span data-stu-id="cf52c-114">APIs in this document</span></span>
<span data-ttu-id="cf52c-115">Azure-API van zoekservice ondersteunt twee URL-syntaxis voor de API-bewerkingen: eenvoudige en OData (Zie [ondersteuning voor OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="cf52c-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="cf52c-116">De volgende lijst ziet u de eenvoudige syntaxis.</span><span class="sxs-lookup"><span data-stu-id="cf52c-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="cf52c-117">Index maken</span><span class="sxs-lookup"><span data-stu-id="cf52c-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-118">Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="cf52c-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-119">Index ophalen</span><span class="sxs-lookup"><span data-stu-id="cf52c-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-120">Aanbieding-indexen</span><span class="sxs-lookup"><span data-stu-id="cf52c-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-121">Indexstatistieken opvragen</span><span class="sxs-lookup"><span data-stu-id="cf52c-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-122">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="cf52c-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-123">Een Index verwijderen</span><span class="sxs-lookup"><span data-stu-id="cf52c-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-124">Toevoegen, verwijderen, en gegevens in een Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="cf52c-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-125">Documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="cf52c-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-126">Lookup-Document</span><span class="sxs-lookup"><span data-stu-id="cf52c-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="cf52c-127">Aantal documenten</span><span class="sxs-lookup"><span data-stu-id="cf52c-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="cf52c-128">Suggesties</span><span class="sxs-lookup"><span data-stu-id="cf52c-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="cf52c-129">Indexbewerkingen</span><span class="sxs-lookup"><span data-stu-id="cf52c-129">Index Operations</span></span>
<span data-ttu-id="cf52c-130">U kunt maken en beheren van de indexen in Azure Search-service via een eenvoudige HTTP-aanvragen (POST, GET, PUT, DELETE) op basis van een resource voor de gegeven index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="cf52c-131">Als u wilt een index maken, moet u eerst een JSON-document met een beschrijving van het indexschema boeken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="cf52c-132">De velden van de index, de gegevenstypen en hoe ze kunnen worden gebruikt (bijvoorbeeld in zoekopdrachten in volledige tekst, filters, sorteren of facetten) worden gedefinieerd in het schema.</span><span class="sxs-lookup"><span data-stu-id="cf52c-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="cf52c-133">Het definieert ook scoreprofiel profielen, suggestiefunctie en andere kenmerken voor het configureren van het gedrag van de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="cf52c-134">Het volgende voorbeeld bevat een afbeelding van een schema dat wordt gebruikt voor zoekopdrachten op gegevens van hotel met het beschrijvingsveld gedefinieerd in twee talen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="cf52c-135">U ziet hoe kenmerken bepalen hoe het veld wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="cf52c-136">Bijvoorbeeld de `hotelId` wordt gebruikt als de documentsleutel (`"key": true`) en wordt uitgesloten van zoekopdrachten in volledige tekst (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="cf52c-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="cf52c-137">Nadat de index is gemaakt, kunt u documenten die de index te vullen gaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="cf52c-138">Zie [toevoegen of Update documenten](#AddOrUpdateDocuments) voor deze stap.</span><span class="sxs-lookup"><span data-stu-id="cf52c-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="cf52c-139">Zie voor een video-Inleiding tot in Azure Search indexeren, de [aflevering Channel 9 Cloud hebben betrekking op Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="cf52c-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="cf52c-140">Index maken</span><span class="sxs-lookup"><span data-stu-id="cf52c-140">Create Index</span></span>
<span data-ttu-id="cf52c-141">Een index is de primaire methode voor het ordenen en documenten zoeken in Azure Search, vergelijkbaar met hoe records in een database in een tabel worden geordend.</span><span class="sxs-lookup"><span data-stu-id="cf52c-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="cf52c-142">Elke index heeft een verzameling van documenten dat alle conform het indexschema (veldnamen, gegevenstypen en eigenschappen), maar indexen ook aanvullende constructies (suggestiefunctie, score-profielen en opties voor CORS) waarmee andere zoekgedrag opgeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="cf52c-143">U kunt een nieuwe index maken in Azure Search-service met behulp van een HTTP POST of PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cf52c-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="cf52c-144">De hoofdtekst van de aanvraag is een JSON-schema dat de index en configuratie-informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="cf52c-145">U kunt ook gebruik van opslag en geef de indexnaam op de URI.</span><span class="sxs-lookup"><span data-stu-id="cf52c-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="cf52c-146">Als de index niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="cf52c-147">Maken van een index bepaalt de structuur van de documenten opgeslagen en gebruikt in zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="cf52c-148">Vullen van de index is een afzonderlijke bewerking.</span><span class="sxs-lookup"><span data-stu-id="cf52c-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="cf52c-149">Voor deze stap kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/azure/mt183328.aspx) (beschikbaar voor ondersteunde gegevensbronnen) of een [toevoegen, bijwerken of verwijderen van documenten](https://msdn.microsoft.com/library/azure/dn798930.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="cf52c-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="cf52c-150">De omgekeerde index wordt gegenereerd wanneer de documenten worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="cf52c-151">**Opmerking**: het maximum aantal indexen toegestaan hangt af van de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="cf52c-152">De gratis service kunnen maximaal 3 indexen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="cf52c-153">Standard-service kan 50-indexen per zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="cf52c-154">Zie [limieten en beperkingen](http://msdn.microsoft.com/library/azure/dn798934.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="cf52c-155">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-155">**Request**</span></span>

<span data-ttu-id="cf52c-156">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="cf52c-157">De **Create Index** aanvraag kan worden geconstrueerd met een methode POST of PUT.</span><span class="sxs-lookup"><span data-stu-id="cf52c-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="cf52c-158">Wanneer u POST, moet u de naam van een index in de aanvraagtekst samen met de indexdefinitie schema opgeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="cf52c-159">Met opslag is de naam van de index onderdeel van de URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="cf52c-160">Als de index niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="cf52c-161">Als deze al bestaat, wordt deze bijgewerkt naar de nieuwe definitie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="cf52c-162">De naam van de index moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="cf52c-163">De rest van de naam kan na het starten van de naam van de index met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang de streepjes niet opeenvolgende zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="cf52c-164">De `api-version` is vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-164">The `api-version` is required.</span></span> <span data-ttu-id="cf52c-165">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor een lijst met beschikbare versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="cf52c-166">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-166">**Request Headers**</span></span>

<span data-ttu-id="cf52c-167">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-168">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-168">`Content-Type`: Required.</span></span> <span data-ttu-id="cf52c-169">Stel dit in op`application/json`</span><span class="sxs-lookup"><span data-stu-id="cf52c-169">Set this to `application/json`</span></span>
* <span data-ttu-id="cf52c-170">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-170">`api-key`: Required.</span></span> <span data-ttu-id="cf52c-171">De `api-key` wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="cf52c-171">The `api-key` is used to</span></span>
* <span data-ttu-id="cf52c-172">de aanvraag om uw Search-service te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-173">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-174">De **Create Index** aanvraag moet bevatten een `api-key` header ingesteld op de administratorsleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-175">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-176">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-177">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-178"><a name="RequestData"></a>
**Syntaxis van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="cf52c-179">De hoofdtekst van de aanvraag bevat een schemadefinitie waarin de lijst met gegevensvelden binnen de documenten die zal worden opgenomen in deze index, gegevenstypen, kenmerken, evenals een optionele lijst met profielen die worden gebruikt voor het beoordelen van overeenkomende documenten op het moment dat de query score berekenen .</span><span class="sxs-lookup"><span data-stu-id="cf52c-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="cf52c-180">Houd er rekening mee dat een POST-aanvraag, moet u de naam van de index in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="cf52c-181">Er kan alleen worden één sleutelveld in de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-181">There can only be one key field in the index.</span></span> <span data-ttu-id="cf52c-182">Er moet een tekenreeksveld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-182">It has to be a string field.</span></span> <span data-ttu-id="cf52c-183">Dit veld wordt de unieke identificatie aangegeven voor elk document dat is opgeslagen in de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="cf52c-184">De belangrijkste onderdelen van een index omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="cf52c-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="cf52c-185">`fields`die zal worden opgenomen in deze index, zoals naam, gegevenstype en eigenschappen die de toegestane acties op dat veld definiëren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="cf52c-186">`suggesters`gebruikt voor automatisch aanvullen of automatisch aangevulde query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="cf52c-187">`scoringProfiles`gebruikt voor aangepaste zoekactie score positie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="cf52c-188">Zie [scoreprofiel profielen toevoegen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="cf52c-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` gebruikt om te definiëren hoe uw documenten/query's worden onderverdeeld in worden geïndexeerd/doorzoekbare-tokens.</span><span class="sxs-lookup"><span data-stu-id="cf52c-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="cf52c-190">Zie [analyse in Azure Search](https://aka.ms//azsanalysis) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="cf52c-191">`defaultScoringProfile`gebruikt voor het overschrijven van de standaard score berekenen gedrag.</span><span class="sxs-lookup"><span data-stu-id="cf52c-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="cf52c-192">`corsOptions`cross-origin-query's op uw index toestaat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="cf52c-193">De syntaxis voor het structureren nettolading van de aanvraag is als volgt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="cf52c-194">Een voorbeeld van een aanvraag wordt aangeboden op verder in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="cf52c-195">**Indexkenmerken**</span><span class="sxs-lookup"><span data-stu-id="cf52c-195">**Index Attributes**</span></span>

<span data-ttu-id="cf52c-196">De volgende kenmerken kunnen worden ingesteld bij het maken van een index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="cf52c-197">Zie voor meer informatie over score berekenen en score berekenen voor profielen [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="cf52c-198">`name`-De naam van het veld ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="cf52c-199">`type`-Hiermee stelt u het gegevenstype voor het veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="cf52c-200">`searchable`-Markeert het veld als volledige tekst kunnen zoeken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="cf52c-201">Dit betekent dat deze ietwat analysis zoals woordafbreking tijdens het indexeren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="cf52c-202">Als u een `searchable` veld een waarde zoals 'mooi day', intern dit verdeeld in de afzonderlijke tokens 'mooi' en 'dag'.</span><span class="sxs-lookup"><span data-stu-id="cf52c-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="cf52c-203">Hierdoor kan de volledige tekst zoekt naar deze voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="cf52c-204">Velden van het type `Edm.String` of `Collection(Edm.String)` zijn `searchable` standaard.</span><span class="sxs-lookup"><span data-stu-id="cf52c-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="cf52c-205">Mag geen velden van andere typen `searchable`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="cf52c-206">**Opmerking**: `searchable` velden gebruiken extra ruimte in de index omdat Azure Search, een extra tokens versie van de waarde van het veld voor zoekopdrachten in volledige tekst wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="cf52c-207">Als u wilt opslaan ruimte in de index en hoeft u niet een veld in zoekopdrachten wilt opnemen, stelt `searchable` naar `false`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="cf52c-208">`filterable`-Kan het veld verwezen in `$filter` query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="cf52c-209">`filterable`verschilt van `searchable` in de verwerking van tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="cf52c-210">Velden van het type `Edm.String` of `Collection(Edm.String)` die zijn `filterable` niet worden bewerkt woordafbreking, zodat vergelijkingen zijn voor exact overeenkomt met alleen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="cf52c-211">Bijvoorbeeld, als u dergelijke veld instellen `f` om 'mooi day' `$filter=f eq 'sunny'` wordt geen overeenkomsten gevonden maar `$filter=f eq 'sunny day'` wordt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="cf52c-212">Alle velden zijn `filterable` standaard.</span><span class="sxs-lookup"><span data-stu-id="cf52c-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="cf52c-213">`sortable`-Het systeem worden standaard resultaten gesorteerd op score, maar veel ervaringen gebruikers wilt sorteren op velden in de documenten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="cf52c-214">Velden van het type `Collection(Edm.String)` kan niet worden `sortable`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="cf52c-215">Alle andere velden zijn `sortable` standaard.</span><span class="sxs-lookup"><span data-stu-id="cf52c-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="cf52c-216">`facetable`-Doorgaans gebruikt in een weergave van zoekresultaten met treffers per categorie (bijvoorbeeld zoeken naar digitale camera's en Zie treffers op merk, door megapixels, door de prijs, enz.).</span><span class="sxs-lookup"><span data-stu-id="cf52c-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="cf52c-217">Deze optie kan niet worden gebruikt met velden van het type `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="cf52c-218">Alle andere velden zijn `facetable` standaard.</span><span class="sxs-lookup"><span data-stu-id="cf52c-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="cf52c-219">**Opmerking**: velden van het type `Edm.String` die zijn `filterable`, `sortable`, of `facetable` kan niet groter zijn dan 32 KB lang.</span><span class="sxs-lookup"><span data-stu-id="cf52c-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="cf52c-220">Dit is omdat deze velden worden behandeld als een enkel zoekterm en de maximale lengte van een term in Azure Search 32KB is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="cf52c-221">Als u meer tekst dan deze opgeslagen in een enkel tekenreeksveld wilt, moet u expliciet instellen `filterable`, `sortable`, en `facetable` naar `false` in de indexdefinitie van de.</span><span class="sxs-lookup"><span data-stu-id="cf52c-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="cf52c-222">**Opmerking**: als een veld geen van de bovenstaande kenmerken die zijn ingesteld heeft op `true` (`searchable`, `filterable`, `sortable`, of`facetable`) het veld effectief is uitgesloten van de omgekeerde index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="cf52c-223">Deze optie is nuttig voor velden die niet worden gebruikt in query's, maar die nodig zijn in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="cf52c-224">Met uitzondering van dergelijke velden uit de index verbetert de prestaties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="cf52c-225">`key`-Markeert het veld bevat de unieke id's voor documenten in de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="cf52c-226">Moet precies één veld worden gekozen als de `key` veld en moet zijn van het type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="cf52c-227">Sleutelvelden kunnen worden gebruikt voor het opzoeken van documenten rechtstreeks via de [Lookup API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="cf52c-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="cf52c-228">`retrievable`-Instellen of het veld in een zoekresultaat kan worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="cf52c-229">Dit is handig als u een veld (bijvoorbeeld marge) gebruiken als een filter, wilt sorteren of score berekenen mechanisme maar niet dat het veld wilt zichtbaar is voor de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="cf52c-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="cf52c-230">Dit kenmerk moet `true` voor `key` velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="cf52c-231">`analyzer`-De naam van de analyzer te gebruiken voor het veld op zoektijd en indexering tijd instellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="cf52c-232">Zie voor de toegestane set waarden [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="cf52c-233">Deze optie kan alleen worden gebruikt met `searchable` velden en deze kunnen niet worden ingesteld met een `searchAnalyzer` of `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="cf52c-234">Zodra de analyzer is gekozen, kan deze niet meer wijzigen voor het veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="cf52c-235">`searchAnalyzer`-De naam van de analyzer gebruikt op het moment van de zoekactie voor het veld instellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="cf52c-236">Zie voor de toegestane set waarden [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="cf52c-237">Deze optie kan alleen worden gebruikt met `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="cf52c-238">Deze moet worden ingesteld samen met `indexAnalyzer` en deze kan niet worden ingesteld samen met de `analyzer` optie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="cf52c-239">Deze analyzer kan worden bijgewerkt op een bestaand veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="cf52c-240">`indexAnalyzer`-Hiermee stelt u de naam van de analysefunctie voor indexering tijd voor het veld wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="cf52c-241">Zie voor de toegestane set waarden [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="cf52c-242">Deze optie kan alleen worden gebruikt met `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="cf52c-243">Deze moet worden ingesteld samen met `searchAnalyzer` en deze kan niet worden ingesteld samen met de `analyzer` optie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="cf52c-244">Zodra de analyzer is gekozen, kan deze niet meer wijzigen voor het veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="cf52c-245">`suggesters`-De modus en de velden die de bron van de inhoud voor suggesties zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="cf52c-246">Zie [Suggestiefunctie](#Suggesters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="cf52c-247">`scoringProfiles`-Definieert aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten hoger in de zoekresultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="cf52c-248">Scoreprofiel profielen zijn opgebouwd veldgewichten en functies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="cf52c-249">Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie over de kenmerken in een scoreprofiel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="cf52c-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Taalondersteuning**</span><span class="sxs-lookup"><span data-stu-id="cf52c-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="cf52c-251">De doorzoekbare velden ondergaan analyse die het beste omvat vaak woordafbreking, tekst normalisatie en voorwaarden worden uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="cf52c-252">Standaard doorzoekbare velden in Azure Search worden geanalyseerd met de [Apache Lucene standaard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) die tekst opgesplitst in elementen na de['Segmentering Unicode-tekst'](http://unicode.org/reports/tr29/) regels.</span><span class="sxs-lookup"><span data-stu-id="cf52c-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="cf52c-253">De standaard analyzer converteert bovendien alle tekens naar hun formulier kleine letters.</span><span class="sxs-lookup"><span data-stu-id="cf52c-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="cf52c-254">Zowel geïndexeerde documenten en zoektermen doorlopen die de analyse tijdens het indexeren en de verwerking van query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="cf52c-255">Azure Search biedt ondersteuning voor verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="cf52c-256">Elke taal is vereist voor een niet-standaard tekst analyzer die accounts voor kenmerken van een bepaalde taal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="cf52c-257">Azure Search biedt twee typen analyzers:</span><span class="sxs-lookup"><span data-stu-id="cf52c-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="cf52c-258">35 analyzers Lucene back-up.</span><span class="sxs-lookup"><span data-stu-id="cf52c-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="cf52c-259">50 analyzers bedrijfseigen Microsoft natuurlijke taal verwerken van de technologie die wordt gebruikt in Office en Bing back-up.</span><span class="sxs-lookup"><span data-stu-id="cf52c-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="cf52c-260">Sommige ontwikkelaars liever de meer vertrouwde, eenvoudig en open-source Lucene-oplossing.</span><span class="sxs-lookup"><span data-stu-id="cf52c-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="cf52c-261">Lucene analyzers sneller zijn, maar de analyzers Microsoft hebben geavanceerde mogelijkheden, zoals Lemmata, word decompounding (in talen zoals Duits, Deens, Nederlands, Zweeds, Noors, Ests, voltooien, Hongaars, Slowaaks) en entiteit erkenning (URL 's e-mailberichten, datums, getallen).</span><span class="sxs-lookup"><span data-stu-id="cf52c-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="cf52c-262">Indien mogelijk moet u vergelijkingen van de Microsoft- en Lucene analyzers om te bepalen welke beter geschikt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="cf52c-263">***Hoe ze zich verhouden***</span><span class="sxs-lookup"><span data-stu-id="cf52c-263">***How they compare***</span></span>

<span data-ttu-id="cf52c-264">De analyzer Lucene voor Engels breidt de standaard analyzer.</span><span class="sxs-lookup"><span data-stu-id="cf52c-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="cf52c-265">Deze bezittelijke voornaamwoorden (afsluitende van) met woorden verwijdert, is van toepassing als gevolg conform [Porter afleiding algoritme](http://tartarus.org/~martin/PorterStemmer/), en verwijdert u Engels [stopwoorden](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="cf52c-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="cf52c-266">Ter vergelijking voert Microsoft analyzer Lemmata in plaats van de gegevens als gevolg.</span><span class="sxs-lookup"><span data-stu-id="cf52c-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="cf52c-267">Dit betekent dat deze kan omgaan met verbogen en onregelmatige word formulieren veel beter wat resulteert in meer relevante zoekresultaten (controle module 7 van [Azure Search MVA presentatie](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="cf52c-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="cf52c-268">Indexering met Microsoft analyzers is gemiddeld twee tot drie keer langzamer dan de Lucene-equivalenten, afhankelijk van de taal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="cf52c-269">Prestaties van de zoekopdracht moet niet aanzienlijk beïnvloed voor de gemiddelde grootte query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="cf52c-270">***Configuratie***</span><span class="sxs-lookup"><span data-stu-id="cf52c-270">***Configuration***</span></span>

<span data-ttu-id="cf52c-271">U kunt voor elk veld in de indexdefinitie instellen de `analyzer` eigenschap in op de naam van een analyzer die welke taal en de leverancier aangeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="cf52c-272">De dezelfde analyzer worden toegepast wanneer het indexeren en het zoeken voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="cf52c-273">U kunt bijvoorbeeld afzonderlijke velden voor Engels, Frans en Spaans hotel beschrijvingen die bestaan naast elkaar op dezelfde positie hebben.</span><span class="sxs-lookup"><span data-stu-id="cf52c-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="cf52c-274">Gebruik de ['searchFields' queryparameter](#SearchQueryParameters) om op te geven welk veld specifieke taal zijn gebonden om te zoeken op basis van uw query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="cf52c-275">U kunt bekijken query voorbeelden die zijn de `analyzer` eigenschap in [documenten zoeken](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="cf52c-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="cf52c-276">***Lijst met Analyzer***</span><span class="sxs-lookup"><span data-stu-id="cf52c-276">***Analyzer list***</span></span>

<span data-ttu-id="cf52c-277">Hieronder volgt de lijst van ondersteunde talen samen met de namen van Lucene en Microsoft analyzer.</span><span class="sxs-lookup"><span data-stu-id="cf52c-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="cf52c-278">Taal</span><span class="sxs-lookup"><span data-stu-id="cf52c-278">Language</span></span></th>
        <th><span data-ttu-id="cf52c-279">De naam van de Microsoft-analyzer</span><span class="sxs-lookup"><span data-stu-id="cf52c-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="cf52c-280">Lucene analyzer naam</span><span class="sxs-lookup"><span data-stu-id="cf52c-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-281">Arabisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-281">Arabic</span></span></td>
        <td><span data-ttu-id="cf52c-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-284">Armeens</span><span class="sxs-lookup"><span data-stu-id="cf52c-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="cf52c-285">Hy.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="cf52c-286">Bengaals</span><span class="sxs-lookup"><span data-stu-id="cf52c-286">Bangla</span></span></td>
        <td><span data-ttu-id="cf52c-287">bn.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="cf52c-288">Baskisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="cf52c-289">EU.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="cf52c-290">Bulgaars</span><span class="sxs-lookup"><span data-stu-id="cf52c-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="cf52c-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="cf52c-293">Catalaans</span><span class="sxs-lookup"><span data-stu-id="cf52c-293">Catalan</span></span></td>
        <td><span data-ttu-id="cf52c-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="cf52c-296">Vereenvoudigd Chinees</span><span class="sxs-lookup"><span data-stu-id="cf52c-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="cf52c-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-299">Traditioneel Chinees</span><span class="sxs-lookup"><span data-stu-id="cf52c-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="cf52c-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="cf52c-302">Kroatisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-302">Croatian</span></span></td>
        <td><span data-ttu-id="cf52c-303">HR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-304">Tsjechisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-304">Czech</span></span></td>
        <td><span data-ttu-id="cf52c-305">CS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-306">CS.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="cf52c-307">Deens</span><span class="sxs-lookup"><span data-stu-id="cf52c-307">Danish</span></span></td>
        <td><span data-ttu-id="cf52c-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="cf52c-310">Nederlands</span><span class="sxs-lookup"><span data-stu-id="cf52c-310">Dutch</span></span></td>
        <td><span data-ttu-id="cf52c-311">nl.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="cf52c-313">Nederlands</span><span class="sxs-lookup"><span data-stu-id="cf52c-313">English</span></span></td>        
        <td><span data-ttu-id="cf52c-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-316">Estisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-316">Estonian</span></span></td>
        <td><span data-ttu-id="cf52c-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-318">Fins</span><span class="sxs-lookup"><span data-stu-id="cf52c-318">Finnish</span></span></td>
        <td><span data-ttu-id="cf52c-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="cf52c-321">Frans</span><span class="sxs-lookup"><span data-stu-id="cf52c-321">French</span></span></td>
        <td><span data-ttu-id="cf52c-322">FR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-323">FR.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-324">Galicisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="cf52c-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="cf52c-326">Duits</span><span class="sxs-lookup"><span data-stu-id="cf52c-326">German</span></span></td>
        <td><span data-ttu-id="cf52c-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-329">Grieks</span><span class="sxs-lookup"><span data-stu-id="cf52c-329">Greek</span></span></td>
        <td><span data-ttu-id="cf52c-330">El.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-331">El.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="cf52c-332">Gujarati</span></span></td>
        <td><span data-ttu-id="cf52c-333">Gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-334">Hebreeuws</span><span class="sxs-lookup"><span data-stu-id="cf52c-334">Hebrew</span></span></td>
        <td><span data-ttu-id="cf52c-335">He.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="cf52c-336">Hindi</span></span></td>
        <td><span data-ttu-id="cf52c-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-339">Hongaars</span><span class="sxs-lookup"><span data-stu-id="cf52c-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="cf52c-340">Hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-341">Hu.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-342">IJslands</span><span class="sxs-lookup"><span data-stu-id="cf52c-342">Icelandic</span></span></td>
        <td><span data-ttu-id="cf52c-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-344">Indonesisch (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="cf52c-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="cf52c-345">ID.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-346">ID.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-347">Iers</span><span class="sxs-lookup"><span data-stu-id="cf52c-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="cf52c-348">Ga.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-349">Italiaans</span><span class="sxs-lookup"><span data-stu-id="cf52c-349">Italian</span></span></td>
        <td><span data-ttu-id="cf52c-350">IT.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-351">IT.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-352">Japans</span><span class="sxs-lookup"><span data-stu-id="cf52c-352">Japanese</span></span></td>
        <td><span data-ttu-id="cf52c-353">Ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-354">Ja.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="cf52c-355">Kannada</span></span></td>
        <td><span data-ttu-id="cf52c-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-357">Koreaans</span><span class="sxs-lookup"><span data-stu-id="cf52c-357">Korean</span></span></td>
        <td><span data-ttu-id="cf52c-358">Ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-359">Ko.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-360">Lets</span><span class="sxs-lookup"><span data-stu-id="cf52c-360">Latvian</span></span></td>        
        <td><span data-ttu-id="cf52c-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-363">Litouws</span><span class="sxs-lookup"><span data-stu-id="cf52c-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="cf52c-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-365">Malajalam</span><span class="sxs-lookup"><span data-stu-id="cf52c-365">Malayalam</span></span></td>
        <td><span data-ttu-id="cf52c-366">ml.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-367">Maleis (Latijns)</span><span class="sxs-lookup"><span data-stu-id="cf52c-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="cf52c-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="cf52c-369">Marathi</span></span></td>
        <td><span data-ttu-id="cf52c-370">Mr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-371">Noors</span><span class="sxs-lookup"><span data-stu-id="cf52c-371">Norwegian</span></span></td>
        <td><span data-ttu-id="cf52c-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-373">No.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="cf52c-374">Perzisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="cf52c-375">FA.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="cf52c-376">Pools</span><span class="sxs-lookup"><span data-stu-id="cf52c-376">Polish</span></span></td>
        <td><span data-ttu-id="cf52c-377">PL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-378">PL.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-379">Portugees (Brazilië)</span><span class="sxs-lookup"><span data-stu-id="cf52c-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="cf52c-380">pt Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-381">pt Br.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-382">Portugees (Portugal)</span><span class="sxs-lookup"><span data-stu-id="cf52c-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="cf52c-383">pt Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="cf52c-384">pt Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="cf52c-385">Punjabi</span></span></td>
        <td><span data-ttu-id="cf52c-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-387">Roemeens</span><span class="sxs-lookup"><span data-stu-id="cf52c-387">Romanian</span></span></td>
        <td><span data-ttu-id="cf52c-388">ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-390">Russisch</span><span class="sxs-lookup"><span data-stu-id="cf52c-390">Russian</span></span></td>
        <td><span data-ttu-id="cf52c-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-393">Servisch (Cyrillisch)</span><span class="sxs-lookup"><span data-stu-id="cf52c-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="cf52c-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-395">Servisch (Latijns)</span><span class="sxs-lookup"><span data-stu-id="cf52c-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="cf52c-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-397">Slowaaks</span><span class="sxs-lookup"><span data-stu-id="cf52c-397">Slovak</span></span></td>
        <td><span data-ttu-id="cf52c-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-399">Sloveens</span><span class="sxs-lookup"><span data-stu-id="cf52c-399">Slovenian</span></span></td>
        <td><span data-ttu-id="cf52c-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-401">Spaans</span><span class="sxs-lookup"><span data-stu-id="cf52c-401">Spanish</span></span></td>
        <td><span data-ttu-id="cf52c-402">ES.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-403">ES.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-404">Zweeds</span><span class="sxs-lookup"><span data-stu-id="cf52c-404">Swedish</span></span></td>
        <td><span data-ttu-id="cf52c-405">SV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-406">SV.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="cf52c-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="cf52c-407">Tamil</span></span></td>
        <td><span data-ttu-id="cf52c-408">TA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="cf52c-409">Telugu</span></span></td>
        <td><span data-ttu-id="cf52c-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-411">Thais</span><span class="sxs-lookup"><span data-stu-id="cf52c-411">Thai</span></span></td>
        <td><span data-ttu-id="cf52c-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-414">Turks</span><span class="sxs-lookup"><span data-stu-id="cf52c-414">Turkish</span></span></td>
        <td><span data-ttu-id="cf52c-415">TR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="cf52c-416">TR.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-417">Oekraïens</span><span class="sxs-lookup"><span data-stu-id="cf52c-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="cf52c-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="cf52c-419">Urdu</span></span></td>
        <td><span data-ttu-id="cf52c-420">Your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-421">Vietnamees</span><span class="sxs-lookup"><span data-stu-id="cf52c-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="cf52c-422">VI.Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf52c-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="cf52c-423">Bovendien biedt Azure Search taal networkdirect analyzer configuraties</span><span class="sxs-lookup"><span data-stu-id="cf52c-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="cf52c-424">Standaard ASCII Folding</span><span class="sxs-lookup"><span data-stu-id="cf52c-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="cf52c-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="cf52c-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="cf52c-426">Unicode-tekst segmentering (standaard Tokenizer)</span><span class="sxs-lookup"><span data-stu-id="cf52c-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="cf52c-427">Opvouwbaar filter ASCII - converteert Unicode-tekens die geen deel uitmaken van de set eerst 127 ASCII-tekens naar hun ASCII-equivalenten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="cf52c-428">Dit is handig voor het verwijderen van diakritische tekens.</span><span class="sxs-lookup"><span data-stu-id="cf52c-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="cf52c-429">Alle analyzers met namen van aantekeningen voorzien met <i>lucene</i> worden van stroom voorzien door [van Apache Lucene taalanalyse](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="cf52c-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="cf52c-430">Meer informatie over de ASCII vouwen filter vindt [hier](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="cf52c-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="cf52c-431">**Suggesties**</span><span class="sxs-lookup"><span data-stu-id="cf52c-431">**Suggesters**</span></span>

<span data-ttu-id="cf52c-432">Een `suggester` wordt gedefinieerd welke velden in een index worden gebruikt voor de ondersteuning voor automatisch aanvullen in zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="cf52c-433">Doorgaans gedeeltelijke zoekreeksen worden verzonden naar de [suggesties API](#Suggestions) terwijl de gebruiker een zoekopdracht typen is en de API een set met voorgestelde zinnen retourneert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="cf52c-434">Een suggestie die u in de index definieert bepaalt welke velden worden gebruikt om de type-ahead zoektermen samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="cf52c-435">Zie [Suggestiefunctie](#Suggesters) voor configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="cf52c-436">**Scoreprofielen**</span><span class="sxs-lookup"><span data-stu-id="cf52c-436">**Scoring profiles**</span></span>

<span data-ttu-id="cf52c-437">Een `scoringProfile` definieert aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten hoger in de zoekresultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="cf52c-438">Scoreprofiel profielen zijn opgebouwd veldgewichten en functies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="cf52c-439">Als u wilt gebruiken, geeft u een profiel met de naam van de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="cf52c-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="cf52c-440">Een standaard score berekenen profiel werkt achter de schermen om de score van een zoekopdracht voor elk item in een resultatenset te berekenen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="cf52c-441">U kunt de interne naamloze scoreprofiel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="cf52c-442">U kunt ook instellen `defaultScoringProfile` aangeroepen een aangepast profiel gebruiken als de standaard, wanneer u een aangepast profiel niet is opgegeven in de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="cf52c-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="cf52c-443">Zie [scoreprofiel profielen toevoegen aan een zoekindex (Azure Search Service REST-API)](search-api-scoring-profiles-2015-02-28-preview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="cf52c-444">**CORS-opties**</span><span class="sxs-lookup"><span data-stu-id="cf52c-444">**CORS Options**</span></span>

<span data-ttu-id="cf52c-445">Client-side Javascript kan API's standaard niet aanroepen omdat de browser voorkomen alle cross-origin-aanvragen dat wordt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="cf52c-446">Inschakelen van CORS (Cross-Origin Resource Sharing) door in te stellen de `corsOptions` kenmerk waarmee cross-origin-query's naar uw index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="cf52c-447">Houd er rekening mee dat alleen query API-ondersteuning CORS uit veiligheidsoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="cf52c-448">De volgende opties kunnen worden ingesteld voor CORS:</span><span class="sxs-lookup"><span data-stu-id="cf52c-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="cf52c-449">`allowedOrigins`(vereist): dit is een lijst met oorsprongen op waarvoor toegang tot uw index wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="cf52c-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="cf52c-450">Dit betekent dat eventuele Javascript-code opgehaald uit deze oorsprongen mag worden query uitvoeren in uw index (ervan uitgaande dat de juiste API-sleutel biedt).</span><span class="sxs-lookup"><span data-stu-id="cf52c-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="cf52c-451">Elke oorsprong heeft meestal de vorm `protocol://fully-qualified-domain-name:port` Hoewel de poort vaak wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="cf52c-452">Zie [in dit artikel](http://go.microsoft.com/fwlink/?LinkId=330822) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="cf52c-453">Als u toestaan toegang tot alle oorsprongen wilt, opnemen `*` als één item in de `allowedOrigins` matrix.</span><span class="sxs-lookup"><span data-stu-id="cf52c-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="cf52c-454">Houd er rekening mee dat **dit wordt niet aanbevolen beveiligingsprocedure voor productie search-services.**</span><span class="sxs-lookup"><span data-stu-id="cf52c-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="cf52c-455">Dit kan echter nuttig zijn voor ontwikkeling of foutopsporing zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="cf52c-456">`maxAgeInSeconds`(optioneel): Browsers gebruiken deze waarde voor de duur (in seconden) te voorbereidende CORS-antwoorden cache.</span><span class="sxs-lookup"><span data-stu-id="cf52c-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="cf52c-457">Dit moet een niet-negatief geheel getal zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-457">This must be a non-negative integer.</span></span> <span data-ttu-id="cf52c-458">Hoe hoger deze waarde is, de prestaties beter, maar hoe langer het duurt CORS wijzigingen voor beleid van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="cf52c-459">Als deze niet is ingesteld, wordt een standaardduur van 5 minuten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="cf52c-460"><a name="CreateUpdateIndexExample"></a>
**Voorbeeld van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="cf52c-461">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-461">**Response**</span></span>

<span data-ttu-id="cf52c-462">Aanvraag is gelukt: '201 gemaakt'.</span><span class="sxs-lookup"><span data-stu-id="cf52c-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="cf52c-463">De antwoordtekst bevatten standaard de JSON voor de definitie van de index die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="cf52c-464">Als de `Prefer` aanvraagheader is ingesteld op `return=minimal`, de antwoordtekst leeg en worden de statuscode geslaagd zijn ' 204 geen inhoud ' in plaats van '201 gemaakt'.</span><span class="sxs-lookup"><span data-stu-id="cf52c-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="cf52c-465">Dit geldt ook als plaatsen of POST is gebruikt om de index te maken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="cf52c-466">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="cf52c-466">**Remarks**</span></span>

<span data-ttu-id="cf52c-467">Op dit moment is er beperkte ondersteuning voor index schema-updates.</span><span class="sxs-lookup"><span data-stu-id="cf52c-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="cf52c-468">Alle schema-updates die opnieuw worden geïndexeerd moeten zoals het wijzigen van veldtypen worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf52c-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="cf52c-469">Hoewel u bestaande velden kunnen niet worden gewijzigd of verwijderd, worden nieuwe velden kunnen worden toegevoegd aan een bestaande index op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="cf52c-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="cf52c-470">Wanneer u een nieuw veld toevoegt, hebben alle documenten in de index automatisch een null-waarde voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="cf52c-471">Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten die zijn toegevoegd aan de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="cf52c-472">Suggesties</span><span class="sxs-lookup"><span data-stu-id="cf52c-472">Suggesters</span></span>
<span data-ttu-id="cf52c-473">De functie suggesties in Azure Search is een type-ahead of automatisch aanvullen query-functie, met een lijst van mogelijke zoektermen in reactie op invoer van gedeeltelijke tekenreeks ingevoerd in een zoekvak.</span><span class="sxs-lookup"><span data-stu-id="cf52c-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="cf52c-474">U vast opgevallen Querysuggesties bij gebruik van zoekmachines commerciële web: '.NET' te typen Bing genereert een overzicht van voorwaarden voor '.NET 4.5 uitvoeren ', '.NET Framework 3.5", enzovoort.</span><span class="sxs-lookup"><span data-stu-id="cf52c-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="cf52c-475">Wanneer u de zoekservice REST-API, suggesties implementeren in een aangepaste Azure Search-toepassing is het volgende vereist:</span><span class="sxs-lookup"><span data-stu-id="cf52c-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="cf52c-476">Suggesties inschakelen door het toevoegen van een **suggestie** bouw in uw index, geeft de naam, zoekmodus en een lijst met velden waarvoor automatisch aangevulde wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="cf52c-477">Bijvoorbeeld, als u 'stad' opgeeft als een bronveld gedeeltelijke zoektekenreeks 'Sea' te typen, leidt tot "Seattle", 'Strand' en 'Seatac' (alle drie zijn de namen van de werkelijke stad) aangeboden als suggesties voor de query voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cf52c-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="cf52c-478">Suggesties worden aangeroepen door het aanroepen van de [suggesties API](#Suggestions) in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="cf52c-479">Gedeeltelijke zoekreeksen worden meestal verzonden naar de service terwijl de gebruiker een zoekopdracht typen is en deze API een set met voorgestelde zinnen retourneert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="cf52c-480">Dit artikel wordt uitgelegd hoe u configureert een **suggestie**.</span><span class="sxs-lookup"><span data-stu-id="cf52c-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="cf52c-481">Controleer ook de [suggesties API](#Suggestions) voor meer informatie over hoe een suggestie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="cf52c-482">**Gebruik**</span><span class="sxs-lookup"><span data-stu-id="cf52c-482">**Usage**</span></span>

<span data-ttu-id="cf52c-483">`Suggesters`worden gemaakt in de index en werk aanbevolen als gebruikt voor bepaalde documenten in plaats van losse termen of woordgroepen voorstellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="cf52c-484">De beste kandidaat velden zijn titels, namen en andere relatief korte zinnen die een item kunnen identificeren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="cf52c-485">Minder effectief zijn herhalende velden, zoals de categorieën en tags, of zeer lange velden zoals beschrijvingen of opmerkingen velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="cf52c-486">Als onderdeel van de indexdefinitie, kunt u een suggestie één aan toevoegen de `suggesters` verzameling.</span><span class="sxs-lookup"><span data-stu-id="cf52c-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="cf52c-487">Eigenschappen die, een suggestie bepalen omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="cf52c-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="cf52c-488">`name`: De naam van de suggestie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="cf52c-489">U de naam van de suggestie gebruiken bij het aanroepen van de `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="cf52c-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="cf52c-490">`searchMode`: De gebruikte strategie voor het zoeken naar candidate zinnen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="cf52c-491">Alleen de modus die momenteel worden ondersteund is `analyzingInfixMatching`, uitvoert, wordt er flexibele overeenkomende woordgroepen aan het begin of in het midden van zinnen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="cf52c-492">`sourceFields`: Een lijst met een of meer velden die de bron van de inhoud voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="cf52c-493">Alleen velden van het type `Edm.String` en `Collection(Edm.String)` mogelijk bronnen voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="cf52c-494">Alleen de velden die een aangepaste taalanalyse ingesteld niet kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="cf52c-495">**Suggestie voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="cf52c-495">**Suggester Example**</span></span>

<span data-ttu-id="cf52c-496">Een suggestie maakt deel uit van de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-496">A suggester is part of the index.</span></span> <span data-ttu-id="cf52c-497">Er kan slechts één suggestie bestaan in de `suggesters` verzameling in de huidige versie, naast de verzameling van velden en `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="cf52c-498">Als u de openbare preview-versie van Azure Search gebruikt `suggesters` wordt vervangen door een oudere Boole-eigenschap (`"suggestions": false`) die alleen voorvoegsel suggesties voor korte tekenreeksen (3-25 tekens) wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf52c-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="cf52c-499">De vervanging ervan `suggesters`, ondersteunt infix overeenkomende waarmee wordt gezocht naar overeenkomende voorwaarden aan het begin of in het midden van veldinhoud, met betere tolerantie voor fouten in zoekreeksen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="cf52c-500">Vanaf versie van de algemeen beschikbaar, is dit nu de enige implementatie van de suggesties API.</span><span class="sxs-lookup"><span data-stu-id="cf52c-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="cf52c-501">De oudere `suggestions` eigenschap die is geïntroduceerd in `api-version=2014-07-31-Preview` blijft werken in deze versie, maar is niet operationeel is in de `2015-02-28` of latere versies van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="cf52c-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="cf52c-502">Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="cf52c-502">Update Index</span></span>
<span data-ttu-id="cf52c-503">U kunt een bestaande index in Azure Search met behulp van een HTTP PUT-aanvraag bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="cf52c-504">Updates kunnen nieuwe velden toevoegen aan het bestaande schema, CORS-opties wijzigen en wijzigen, scoreprofiel profielen bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="cf52c-505">Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="cf52c-506">U opgeven de naam van de index om bij te werken op de aanvraag-URI:</span><span class="sxs-lookup"><span data-stu-id="cf52c-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="cf52c-507">**Belangrijk:** ondersteuning voor index schema-updates is beperkt tot bewerkingen waarvoor de search-index opnieuw opbouwen niet nodig.</span><span class="sxs-lookup"><span data-stu-id="cf52c-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="cf52c-508">Alle schema-updates die opnieuw worden geïndexeerd moeten, zoals het wijzigen van veldtypen, worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf52c-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="cf52c-509">Nieuwe velden kunnen op elk gewenst moment worden toegevoegd, hoewel bestaande velden kunnen niet worden gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="cf52c-510">Hetzelfde geldt voor `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="cf52c-511">Nieuwe velden kunnen worden toegevoegd aan een suggestie op het moment dat de velden worden toegevoegd, maar velden kunnen niet worden verwijderd uit `suggesters` en bestaande velden kunnen niet worden toegevoegd aan `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="cf52c-512">Wanneer u een nieuw veld toevoegt aan een index, hebben alle documenten in de index automatisch een null-waarde voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="cf52c-513">Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten die zijn toegevoegd aan de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="cf52c-514">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-514">**Request**</span></span>

<span data-ttu-id="cf52c-515">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="cf52c-516">De **Index bijwerken** aanvraag is opgesteld met HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="cf52c-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="cf52c-517">Met opslag is de naam van de index onderdeel van de URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="cf52c-518">Als de index niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="cf52c-519">Als de index al bestaat, wordt deze bijgewerkt naar de nieuwe definitie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="cf52c-520">De naam van de index moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="cf52c-521">De rest van de naam kan na het starten van de naam van de index met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang de streepjes niet opeenvolgende zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="cf52c-522">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-523">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-524">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-525">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-525">**Request Headers**</span></span>

<span data-ttu-id="cf52c-526">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-527">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-527">`Content-Type`: Required.</span></span> <span data-ttu-id="cf52c-528">Stel dit in op`application/json`</span><span class="sxs-lookup"><span data-stu-id="cf52c-528">Set this to `application/json`</span></span>
* <span data-ttu-id="cf52c-529">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-529">`api-key`: Required.</span></span> <span data-ttu-id="cf52c-530">De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-531">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-532">De **Index bijwerken** aanvraag moet bevatten een `api-key` header ingesteld op de administratorsleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-533">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-534">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-535">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-536">**Syntaxis van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-536">**Request Body Syntax**</span></span>

<span data-ttu-id="cf52c-537">Bij het bijwerken van een bestaande index vergezeld de hoofdtekst gaan van de oorspronkelijke schemadefinitie, plus de nieuwe velden die u wilt toevoegen, evenals de gewijzigde scoreprofiel profielen, suggestiefunctie en CORS-opties, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf52c-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="cf52c-538">Als u de CORS-opties en profielen scoreprofiel niet wijzigt, moet u de oorspronkelijke wanneer de index is gemaakt opnemen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="cf52c-539">In het algemeen het beste patroon voor updates te gebruiken is het ophalen van de indexdefinitie met een GET, wijzigt u deze vervolgens bijwerken met PUT.</span><span class="sxs-lookup"><span data-stu-id="cf52c-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="cf52c-540">De schemasyntaxis van het gebruikt voor het maken van een index is hier gereproduceerd voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="cf52c-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="cf52c-541">Zie [Create Index](#CreateIndex) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="cf52c-542">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-542">**Response**</span></span>

<span data-ttu-id="cf52c-543">Aanvraag is gelukt: ' 204 geen inhoud '.</span><span class="sxs-lookup"><span data-stu-id="cf52c-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="cf52c-544">Standaard wordt de antwoordtekst leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-544">By default the response body will be empty.</span></span> <span data-ttu-id="cf52c-545">Echter, als de `Prefer` aanvraagheader is ingesteld op `return=representation`, de hoofdtekst van het antwoord bevat de JSON voor de definitie van de index die is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="cf52c-546">In dit geval wordt de statuscode geslaagd zijn ' 200 OK '.</span><span class="sxs-lookup"><span data-stu-id="cf52c-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="cf52c-547">**Definitie van de index met aangepaste analyzers bijwerken**</span><span class="sxs-lookup"><span data-stu-id="cf52c-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="cf52c-548">Als er een analyzer, een tokenizer, een token filter of een char-filter is gedefinieerd, kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="cf52c-549">Nieuwe te kunnen alleen worden toegevoegd aan een bestaande index als de `allowIndexDowntime` vlag is ingesteld op true in de index update-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="cf52c-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="cf52c-550">Houd er rekening mee dat deze bewerking uw index offline voor ten minste een paar seconden, waardoor uw indexeren en queryaanvragen mislukken wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="cf52c-551">Beschikbaarheid van de prestaties en schrijven van de index kan worden gehinderd minuten nadat de index is bijgewerkt of langer voor zeer grote indexen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="cf52c-552">Lijst met indexen</span><span class="sxs-lookup"><span data-stu-id="cf52c-552">List Indexes</span></span>
<span data-ttu-id="cf52c-553">De **lijst indexen** bewerking retourneert een lijst van de indexen momenteel in uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="cf52c-554">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-554">**Request**</span></span>

<span data-ttu-id="cf52c-555">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="cf52c-556">De **lijst indexen** aanvraag kan worden opgesteld met de GET-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="cf52c-557">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-558">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-559">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-560">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-560">**Request Headers**</span></span>

<span data-ttu-id="cf52c-561">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-562">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-562">`api-key`: Required.</span></span> <span data-ttu-id="cf52c-563">De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-564">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-565">De **lijst indexen** aanvraag moet bevatten een `api-key` ingesteld op een beheersleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-566">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-567">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-568">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-569">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-569">**Request Body**</span></span>

<span data-ttu-id="cf52c-570">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-570">None.</span></span>

<span data-ttu-id="cf52c-571">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-571">**Response**</span></span>

<span data-ttu-id="cf52c-572">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="cf52c-573">Hier volgt een voorbeeld-antwoordtekst:</span><span class="sxs-lookup"><span data-stu-id="cf52c-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="cf52c-574">Houd er rekening mee dat u het antwoord naar beneden eigenschappen die u geïnteresseerd bent in kunt filteren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="cf52c-575">Bijvoorbeeld: als u alleen een lijst met indexnamen wilt, gebruiken de OData `$select` query-optie:</span><span class="sxs-lookup"><span data-stu-id="cf52c-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="cf52c-576">In dit geval wordt zou het antwoord van het bovenstaande voorbeeld als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="cf52c-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="cf52c-577">Dit is een nuttig techniek bandbreedte opslaan als er een groot aantal indexen in uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="cf52c-578">Index ophalen</span><span class="sxs-lookup"><span data-stu-id="cf52c-578">Get Index</span></span>
<span data-ttu-id="cf52c-579">De **Index ophalen** bewerking krijgt de definitie van de index van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="cf52c-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="cf52c-580">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-580">**Request**</span></span>

<span data-ttu-id="cf52c-581">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-582">De **Index ophalen** aanvraag kan worden opgesteld met de GET-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="cf52c-583">De [indexnaam] in de aanvraag-URI geeft aan welke index om te retourneren van de indexverzameling.</span><span class="sxs-lookup"><span data-stu-id="cf52c-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="cf52c-584">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-585">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-586">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-587">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-587">**Request Headers**</span></span>

<span data-ttu-id="cf52c-588">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-589">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-590">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-591">De **Index ophalen** aanvraag moet bevatten een `api-key` ingesteld op een beheersleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-592">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-593">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-594">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-595">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-595">**Request Body**</span></span>

<span data-ttu-id="cf52c-596">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-596">None.</span></span>

<span data-ttu-id="cf52c-597">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-597">**Response**</span></span>

<span data-ttu-id="cf52c-598">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="cf52c-599">Zie het voorbeeld JSON in [maken en bijwerken van een Index](#CreateUpdateIndexExample) voor een voorbeeld van de nettolading van de reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="cf52c-600">Index verwijderen</span><span class="sxs-lookup"><span data-stu-id="cf52c-600">Delete Index</span></span>
<span data-ttu-id="cf52c-601">De **Index verwijderen** bewerking verwijdert u een index en de bijbehorende documentatie van uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="cf52c-602">U krijgt de naam van de index van het servicedashboard in de Azure portal of van de API.</span><span class="sxs-lookup"><span data-stu-id="cf52c-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="cf52c-603">Zie [lijst indexen](#ListIndexes) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="cf52c-604">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-604">**Request**</span></span>

<span data-ttu-id="cf52c-605">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-606">De **Index verwijderen** aanvraag kan worden opgesteld met de DELETE-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="cf52c-607">De [indexnaam] in de aanvraag-URI geeft aan welke index te verwijderen uit de indexverzameling.</span><span class="sxs-lookup"><span data-stu-id="cf52c-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="cf52c-608">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-609">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-610">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-611">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-611">**Request Headers**</span></span>

<span data-ttu-id="cf52c-612">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-613">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-613">`api-key`: Required.</span></span> <span data-ttu-id="cf52c-614">De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-615">Het is een tekenreekswaarde die uniek is voor uw service-URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="cf52c-616">De **Index verwijderen** aanvraag moet bevatten een `api-key` header ingesteld op de administratorsleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-617">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-618">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-619">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-620">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-620">**Request Body**</span></span>

<span data-ttu-id="cf52c-621">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-621">None.</span></span>

<span data-ttu-id="cf52c-622">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-622">**Response**</span></span>

<span data-ttu-id="cf52c-623">Statuscode: 204 geen inhoud wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="cf52c-624">Indexstatistieken opvragen</span><span class="sxs-lookup"><span data-stu-id="cf52c-624">Get Index Statistics</span></span>
<span data-ttu-id="cf52c-625">De **statistieken voor Index ophalen** bewerking retourneert van Azure Search een aantal documenten voor de huidige index plus opslaggebruik.</span><span class="sxs-lookup"><span data-stu-id="cf52c-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="cf52c-626">Statistieken over document aantal en de opslaggrootte worden elke paar minuten, niet in realtime verzameld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="cf52c-627">De statistieken die is geretourneerd door deze API kan daarom niet overeen met wijzigingen die zijn veroorzaakt door een recente indexbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="cf52c-628">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-628">**Request**</span></span>

<span data-ttu-id="cf52c-629">HTTPS is vereist voor alle services aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="cf52c-630">De **statistieken voor Index ophalen** aanvraag kan worden opgesteld met de GET-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="cf52c-631">De [indexnaam] in de aanvraag-URI Hiermee geeft u de service om terug te keren indexstatistieken voor de opgegeven index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="cf52c-632">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-633">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-634">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-635">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-635">**Request Headers**</span></span>

<span data-ttu-id="cf52c-636">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-637">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-638">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-639">De **ophalen indexstatistieken** aanvraag moet bevatten een `api-key` ingesteld op een beheersleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-640">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-641">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-642">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-643">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-643">**Request Body**</span></span>

<span data-ttu-id="cf52c-644">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-644">None.</span></span>

<span data-ttu-id="cf52c-645">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-645">**Response**</span></span>

<span data-ttu-id="cf52c-646">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="cf52c-647">De antwoordtekst is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cf52c-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="cf52c-648">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="cf52c-648">Test Analyzer</span></span>
<span data-ttu-id="cf52c-649">De **analyseren API** ziet u hoe een analyzer tekst opgesplitst in tokens.</span><span class="sxs-lookup"><span data-stu-id="cf52c-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="cf52c-650">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-650">**Request**</span></span>

<span data-ttu-id="cf52c-651">HTTPS is vereist voor alle services aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="cf52c-652">De **analyseren API** aanvraag kan worden opgesteld met de POST-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="cf52c-653">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-654">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-655">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-656">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-656">**Request Headers**</span></span>

<span data-ttu-id="cf52c-657">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-658">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-659">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-660">De **analyseren API** aanvraag moet bevatten een `api-key` ingesteld op een beheersleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-661">U moet ook de naam van de index en de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-662">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-663">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-664">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="cf52c-665">of</span><span class="sxs-lookup"><span data-stu-id="cf52c-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="cf52c-666">De `analyzer_name`, `tokenizer_name`, `token_filter_name` en `char_filter_name` moet een geldige naam van de vooraf gedefinieerde of aangepaste analyzers, tokenizers, token filters en char filters voor de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="cf52c-667">Voor meer informatie over het proces van lexicale analyse Zie [analyse in Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="cf52c-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="cf52c-668">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-668">**Response**</span></span>

<span data-ttu-id="cf52c-669">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="cf52c-670">De antwoordtekst is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cf52c-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="cf52c-671">**API-voorbeeld analyseren**</span><span class="sxs-lookup"><span data-stu-id="cf52c-671">**Analyze API example**</span></span>

<span data-ttu-id="cf52c-672">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="cf52c-673">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="cf52c-674">Document bewerkingen</span><span class="sxs-lookup"><span data-stu-id="cf52c-674">Document Operations</span></span>
<span data-ttu-id="cf52c-675">In Azure Search is een index wordt opgeslagen in de cloud, en ingevuld met JSON-documenten die u naar de service uploadt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="cf52c-676">Alle documenten die u uploadt, omvatten de corpus van uw zoekgegevens.</span><span class="sxs-lookup"><span data-stu-id="cf52c-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="cf52c-677">Documenten bevatten velden, zijn sommige van deze in de zoektermen tokenized als ze worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="cf52c-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="cf52c-678">De `/docs` URL-segment in de Azure Search API vertegenwoordigt de verzameling van documenten in een index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="cf52c-679">Alle bewerkingen die worden uitgevoerd op de verzameling zoals uploaden, samenvoegen, verwijderen of documenten nemen opvragen plaatsen in de context van een enkele index, dus de URL's voor deze bewerkingen wordt altijd gestart met `/indexes/[index name]/docs` voor een naam voor de gegeven index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="cf52c-680">Uw toepassingscode moet ofwel JSON-documenten te uploaden naar Azure Search genereren of kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/dn946891.aspx) documenten laden als de gegevensbron Azure SQL Database of Azure Cosmos DB is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="cf52c-681">Indexen worden gewoonlijk ingevuld uit een enkele gegevensset die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="cf52c-682">U moet plannen, moeten een document voor elk item dat u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="cf52c-683">Een toepassing van de verhuur film wellicht een document per film, een toepassing via wellicht een document per SKU, een toepassing online cursusprogramma wellicht een document per loop, een bedrijf wellicht een document voor elk academic papier in hun opslagplaats, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="cf52c-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="cf52c-684">Documenten bestaan uit een of meer velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="cf52c-685">Velden kunnen bevatten tekst die wordt door Azure Search in zoektermen tokenized, evenals niet getokeniseerd of niet-tekstwaarden plaatsen die kunnen worden gebruikt in filters of scoreprofiel profielen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="cf52c-686">De namen, gegevenstypen en zoekfuncties ondersteund voor elk veld worden bepaald door het schema van de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="cf52c-687">Een van de velden in elke indexschema dat moet worden aangemerkt als een ID en elk document moet een waarde hebben voor het veld ID die een unieke identificatie van dat document in de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="cf52c-688">Alle andere documentvelden zijn optioneel en wordt teruggezet op een null-waarde als niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="cf52c-689">Houd er rekening mee dat null-waarden geen ruimte vrijmaken in de search-index hebben.</span><span class="sxs-lookup"><span data-stu-id="cf52c-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="cf52c-690">Als u documenten uploaden, moet u al hebt gemaakt de index van de service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="cf52c-691">Zie [Create Index](#CreateIndex) voor meer informatie over deze eerste stap.</span><span class="sxs-lookup"><span data-stu-id="cf52c-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="cf52c-692">Toevoegen, bijwerken of verwijderen van documenten</span><span class="sxs-lookup"><span data-stu-id="cf52c-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="cf52c-693">U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="cf52c-694">Batchverwerking van documenten maximaal (1000 documenten per batch) of 16 MB per batch wordt aanbevolen voor grote aantallen van updates.</span><span class="sxs-lookup"><span data-stu-id="cf52c-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="cf52c-695">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-695">**Request**</span></span>

<span data-ttu-id="cf52c-696">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="cf52c-697">U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="cf52c-698">De aanvraag-URI bevat [naam van de index] opgeven welke index om documenten te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="cf52c-699">U kunt alleen documenten naar een index boeken tegelijk.</span><span class="sxs-lookup"><span data-stu-id="cf52c-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="cf52c-700">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-701">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-702">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-703">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-703">**Request Headers**</span></span>

<span data-ttu-id="cf52c-704">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-705">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-705">`Content-Type`: Required.</span></span> <span data-ttu-id="cf52c-706">Stel dit in op`application/json`</span><span class="sxs-lookup"><span data-stu-id="cf52c-706">Set this to `application/json`</span></span>
* <span data-ttu-id="cf52c-707">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="cf52c-707">`api-key`: Required.</span></span> <span data-ttu-id="cf52c-708">De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-709">Het is een tekenreekswaarde die uniek is voor uw service.</span><span class="sxs-lookup"><span data-stu-id="cf52c-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="cf52c-710">De **documenten toevoegen** aanvraag moet bevatten een `api-key` header ingesteld op de administratorsleutel (in plaats van een querysleutel).</span><span class="sxs-lookup"><span data-stu-id="cf52c-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="cf52c-711">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-712">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-713">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-714">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-714">**Request Body**</span></span>

<span data-ttu-id="cf52c-715">De hoofdtekst van de aanvraag bevat een of meer documenten te indexeren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="cf52c-716">Documenten worden aangeduid met een unieke sleutel.</span><span class="sxs-lookup"><span data-stu-id="cf52c-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="cf52c-717">Elk document dat is gekoppeld aan een actie: uploaden, samenvoegen, mergeOrUpload of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="cf52c-718">Het uploaden van aanvragen moeten de gegevens van het document bevatten als een set van sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="cf52c-719">Document sleutels mogen alleen letters, cijfers, streepjes ('-'), onderstrepingstekens ('_') en gelijk tekens ('=').</span><span class="sxs-lookup"><span data-stu-id="cf52c-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="cf52c-720">Zie voor meer informatie [naamgevingsregels](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="cf52c-721">**Documentacties**</span><span class="sxs-lookup"><span data-stu-id="cf52c-721">**Document Actions**</span></span>

* <span data-ttu-id="cf52c-722">`upload`: Er is een upload-actie is vergelijkbaar met een "upsert", waarbij het document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="cf52c-723">Houd er rekening mee dat alle velden in het geval van de update worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="cf52c-724">`merge`: Een bestaand document merge bijgewerkt met de opgegeven velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="cf52c-725">Als het document niet bestaat, mislukt de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="cf52c-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="cf52c-726">Alle velden die u in een samenvoeging opgeeft, vervangen de bestaande velden in het document,</span><span class="sxs-lookup"><span data-stu-id="cf52c-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="cf52c-727">ook velden van het type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="cf52c-728">Bijvoorbeeld, als het document bevat een veld 'labels' met de waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor 'tags', worden de uiteindelijke waarde van het veld 'tags' `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="cf52c-729">Het **niet** worden `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="cf52c-730">`mergeOrUpload`: gedraagt zich als `merge` wanneer een document met de opgegeven sleutel al in de index bestaat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="cf52c-731">Als het document niet bestaat nog, gedraagt zich als `upload` met een nieuw document.</span><span class="sxs-lookup"><span data-stu-id="cf52c-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="cf52c-732">`delete`: Het opgegeven document verwijdert verwijderen uit de index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="cf52c-733">Houd er rekening mee dat alle velden u opgeeft in een `delete` bewerking dan het sleutelveld worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="cf52c-734">Als u verwijderen van een afzonderlijk veld uit een document wilt, gebruikt u `merge` en stelt u het veld expliciet naar `null`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="cf52c-735">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-735">**Response**</span></span>

<span data-ttu-id="cf52c-736">Statuscode 200 wordt (OK) geretourneerd voor een geslaagd antwoord, wat betekent dat alle items zijn geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="cf52c-737">Dit wordt aangegeven door de `status` eigenschap wordt ingesteld op true voor alle artikelen, ook als de `statusCode` eigenschap wordt ingesteld op 201 (voor recent geüploade documenten) of 200 (voor samengevoegde of verwijderde documenten):</span><span class="sxs-lookup"><span data-stu-id="cf52c-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="cf52c-738">Statuscode 207 (meerdere Status) wordt geretourneerd wanneer ten minste één item is niet geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="cf52c-739">Items die niet zijn geïndexeerd hebben de `status` veld ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="cf52c-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="cf52c-740">De `errorMessage` en `statusCode` eigenschappen wordt de reden voor de indexering fout aangeven:</span><span class="sxs-lookup"><span data-stu-id="cf52c-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="cf52c-741">De volgende tabel beschrijft de verschillende per document statuscodes die kunnen worden geretourneerd in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="cf52c-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="cf52c-742">Houd er rekening mee dat sommige duiden op problemen met de aanvraag zelf, terwijl anderen tijdelijke fouten geven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="cf52c-743">De laatste die probeert u het opnieuw na een vertraging.</span><span class="sxs-lookup"><span data-stu-id="cf52c-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="cf52c-744">Statuscode</span><span class="sxs-lookup"><span data-stu-id="cf52c-744">Status code</span></span></th>
        <th><span data-ttu-id="cf52c-745">Betekenis</span><span class="sxs-lookup"><span data-stu-id="cf52c-745">Meaning</span></span></th>
        <th><span data-ttu-id="cf52c-746">Herstelbare</span><span class="sxs-lookup"><span data-stu-id="cf52c-746">Retryable</span></span></th>
        <th><span data-ttu-id="cf52c-747">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cf52c-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-748">200</span><span class="sxs-lookup"><span data-stu-id="cf52c-748">200</span></span></td>
        <td><span data-ttu-id="cf52c-749">Document is gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="cf52c-750">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="cf52c-750">n/a</span></span></td>
        <td><span data-ttu-id="cf52c-751">Verwijderbewerkingen zijn <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="cf52c-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="cf52c-752">Dat wil zeggen, zelfs als de documentsleutel van een niet in de index bestaat, leidt probeert een delete-bewerking met die sleutel tot een 200-statuscode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-753">201</span><span class="sxs-lookup"><span data-stu-id="cf52c-753">201</span></span></td>
        <td><span data-ttu-id="cf52c-754">Document is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="cf52c-755">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="cf52c-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-756">400</span><span class="sxs-lookup"><span data-stu-id="cf52c-756">400</span></span></td>
        <td><span data-ttu-id="cf52c-757">Er is een fout opgetreden in het document dat waardoor deze niet kan worden geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="cf52c-758">Nee</span><span class="sxs-lookup"><span data-stu-id="cf52c-758">No</span></span></td>
        <td><span data-ttu-id="cf52c-759">Het foutbericht in het antwoord geeft aan wat is het probleem met het document.</span><span class="sxs-lookup"><span data-stu-id="cf52c-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-760">404</span><span class="sxs-lookup"><span data-stu-id="cf52c-760">404</span></span></td>
        <td><span data-ttu-id="cf52c-761">Het document kan niet worden samengevoegd omdat de opgegeven sleutel niet in de index bestaat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="cf52c-762">Nee</span><span class="sxs-lookup"><span data-stu-id="cf52c-762">No</span></span></td>
        <td><span data-ttu-id="cf52c-763">Deze fout treedt niet op bij uploads omdat ze nieuwe documenten maken en dit niet voor verwijderingen gebeurt omdat ze <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="cf52c-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-764">409</span><span class="sxs-lookup"><span data-stu-id="cf52c-764">409</span></span></td>
        <td><span data-ttu-id="cf52c-765">Er is een versieconflict gedetecteerd bij een poging tot het indexeren van een document.</span><span class="sxs-lookup"><span data-stu-id="cf52c-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="cf52c-766">Ja</span><span class="sxs-lookup"><span data-stu-id="cf52c-766">Yes</span></span></td>
        <td><span data-ttu-id="cf52c-767">Dit kan gebeuren wanneer u probeert meer dan één keer gelijktijdig index van hetzelfde document.</span><span class="sxs-lookup"><span data-stu-id="cf52c-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-768">422</span><span class="sxs-lookup"><span data-stu-id="cf52c-768">422</span></span></td>
        <td><span data-ttu-id="cf52c-769">De index is tijdelijk niet beschikbaar omdat deze is bijgewerkt met de vlag 'allowIndexDowntime' is ingesteld op 'true'.</span><span class="sxs-lookup"><span data-stu-id="cf52c-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="cf52c-770">Ja</span><span class="sxs-lookup"><span data-stu-id="cf52c-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="cf52c-771">503</span><span class="sxs-lookup"><span data-stu-id="cf52c-771">503</span></span></td>
        <td><span data-ttu-id="cf52c-772">Uw search-service is tijdelijk niet beschikbaar is, mogelijk vanwege een zware belasting.</span><span class="sxs-lookup"><span data-stu-id="cf52c-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="cf52c-773">Ja</span><span class="sxs-lookup"><span data-stu-id="cf52c-773">Yes</span></span></td>
        <td><span data-ttu-id="cf52c-774">Uw code moet worden gewacht voordat opnieuw uit te voeren in dit geval of u het risico verlenging van de service niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="cf52c-775">**Opmerking**: als uw clientcode wordt vaak een 207 antwoord tegenkomt, een mogelijke reden is dat het systeem belast wordt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="cf52c-776">U kunt dit bevestigen door het controleren van de `statusCode` eigenschap voor 503.</span><span class="sxs-lookup"><span data-stu-id="cf52c-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="cf52c-777">Als dit het geval is, wordt aangeraden ***beperking indexering aanvragen***.</span><span class="sxs-lookup"><span data-stu-id="cf52c-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="cf52c-778">Anders als indexeren verkeer niet subside, kan start het systeem het verwijderen van alle aanvragen met 503-fouten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="cf52c-779">Statuscode 429 geeft aan dat u het quotum van het aantal documenten per index hebt overschreden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="cf52c-780">Een nieuwe index maken of een upgrade uit voor hogere Capaciteitslimieten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="cf52c-781">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="cf52c-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="cf52c-782">Documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="cf52c-782">Search Documents</span></span>
<span data-ttu-id="cf52c-783">Een **Search** bewerking als een GET of POST-aanvraag wordt uitgegeven en parameters waarmee de criteria voor het selecteren van de overeenkomende documenten bevat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="cf52c-784">**Wanneer POST gebruiken in plaats van GET**</span><span class="sxs-lookup"><span data-stu-id="cf52c-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="cf52c-785">Wanneer u HTTP GET aan te roepen de **Search** API, moet u er rekening mee dat de lengte van de aanvraag-URL kan niet hoger is dan 8 KB.</span><span class="sxs-lookup"><span data-stu-id="cf52c-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="cf52c-786">Dit is meestal genoeg voor de meeste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-786">This is usually enough for most applications.</span></span> <span data-ttu-id="cf52c-787">Sommige toepassingen produceren echter zeer grote query's of OData-filterexpressies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="cf52c-788">Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters en query's dan GET.</span><span class="sxs-lookup"><span data-stu-id="cf52c-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="cf52c-789">Met POST is het aantal voorwaarden of componenten in een query de beperkende factor, niet de grootte van de onbewerkte query omdat de limiet voor de aanvraag voor POST ongeveer 16 MB is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-790">Hoewel de maximale grootte van POST-aanvraag te lang. is, zoekquery's en filterexpressies mogen niet willekeurig complexe.</span><span class="sxs-lookup"><span data-stu-id="cf52c-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="cf52c-791">Zie [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) en [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over zoekopdracht query en filter complexiteit beperkingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="cf52c-792">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-792">**Request**</span></span>

<span data-ttu-id="cf52c-793">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-794">De **Search** aanvraag kan worden opgesteld met de methoden GET of POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="cf52c-795">De aanvraag-URI geeft aan welke index van de query voor alle documenten die overeenkomen met de parameters.</span><span class="sxs-lookup"><span data-stu-id="cf52c-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="cf52c-796">Parameters zijn opgegeven voor de queryreeks weergegeven in het geval van GET-aanvragen en in de aanvraag hoofdtekst in het geval van POST-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="cf52c-797">Als een best practice bij het maken van GET-aanvragen, moet u [URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke queryparameters bij het aanroepen van de REST-API rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="cf52c-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="cf52c-798">Voor **Search** bewerkingen, dit omvat:</span><span class="sxs-lookup"><span data-stu-id="cf52c-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="cf52c-799">URL-codering wordt alleen aanbevolen voor de bovenstaande queryparameters.</span><span class="sxs-lookup"><span data-stu-id="cf52c-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="cf52c-800">Als u per ongeluk URL coderen de volledige query-tekenreeks (alles na de?), aanvragen worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="cf52c-801">Zo is de URL-codering ook alleen nodig bij het aanroepen van de REST-API die rechtstreeks met de GET.</span><span class="sxs-lookup"><span data-stu-id="cf52c-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="cf52c-802">Er is geen URL-codering is nodig bij het aanroepen van **zoeken** met behulp van POST, of bij het gebruik de [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die het URL-codering voor u verwerkt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="cf52c-803"><a name="SearchQueryParameters"></a>
**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="cf52c-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="cf52c-804">**Search** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="cf52c-805">U opgeven dat deze parameters in de URL van de querytekenreeks bij het aanroepen van **Search** via GET en als JSON-eigenschappen in de aanvraagtekst bij het aanroepen van **Search** via POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="cf52c-806">De syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="cf52c-807">Deze verschillen worden vermeld als die van toepassing zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="cf52c-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="cf52c-808">`search=[string]`(optioneel) - de tekst om naar te zoeken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="cf52c-809">Alle `searchable` velden worden doorzocht door standaard tenzij `searchFields` is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="cf52c-810">Bij het zoeken naar `searchable` velden, de zoektekst zelf tokenized, zodat meerdere voorwaarden kunnen worden gescheiden door spaties bevatten (bijvoorbeeld: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="cf52c-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="cf52c-811">Gebruik voor elke term `*` (dit kan handig zijn voor Booleaanse filterquery's).</span><span class="sxs-lookup"><span data-stu-id="cf52c-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="cf52c-812">Als deze parameter wordt weggelaten heeft hetzelfde effect als instellen op `*`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="cf52c-813">Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) voor specifieke informatie over de syntaxis van de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="cf52c-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="cf52c-814">**Opmerking**: de resultaten kunnen soms verrassend worden tijdens het opvragen via `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="cf52c-815">Het tokenizer bevat de logica voor de afhandeling van aanvragen die gemeenschappelijk zijn voor de Engelse tekst zoals apostrof, komma's in cijfers, enzovoort. Bijvoorbeeld: `search=123,456` komt overeen met een enkele term 123,456 in plaats van de afzonderlijke termen 123 en 456, omdat komma's worden gebruikt als duizend scheidingstekens voor grote aantallen in het Engels.</span><span class="sxs-lookup"><span data-stu-id="cf52c-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="cf52c-816">Daarom wordt u aangeraden witruimte in plaats van leestekens te scheiden van de voorwaarden in de `search` parameter.</span><span class="sxs-lookup"><span data-stu-id="cf52c-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="cf52c-817">`searchMode=any|all`(optioneel, wordt standaard ingesteld op `any`) - of een of meer van de zoektermen om op te tellen van het document als een overeenkomst moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="cf52c-818">`searchFields=[string]`(optioneel): de lijst met door komma's gescheiden veldnamen om te zoeken naar de opgegeven tekst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="cf52c-819">Doelvelden moeten worden gemarkeerd als `searchable`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="cf52c-820">`queryType=simple|full`(optioneel, wordt standaard ingesteld op `simple`): wanneer is ingesteld op 'eenvoudige' zoektekst wordt geïnterpreteerd met behulp van een eenvoudige querytaal waarmee symbolen zoals +, * en ' '.</span><span class="sxs-lookup"><span data-stu-id="cf52c-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="cf52c-821">Query's worden geëvalueerd in de doorzoekbare velden (of velden die zijn aangegeven in `searchFields`) in elk document standaard.</span><span class="sxs-lookup"><span data-stu-id="cf52c-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="cf52c-822">Als het querytype is ingesteld op `full` zoektekst met behulp van de Lucene-querytaal waarmee veld-specifieke en gewogen zoekopdrachten wordt geïnterpreteerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="cf52c-823">Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) en [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) voor specifieke informatie over de syntaxis van de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="cf52c-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf52c-824">Zoeken in de querytaal wordt niet ondersteund voor $filter dat vergelijkbare functionaliteit biedt Lucene liggen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="cf52c-825">`moreLikeThis=[key]`(optioneel) **Belangrijk:** deze functie is alleen beschikbaar in `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-826">Deze optie kan niet worden gebruikt in een query met de parameter text search `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="cf52c-827">De `moreLikeThis` parameter vindt documenten die vergelijkbaar met het document dat is opgegeven door de documentsleutel zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="cf52c-828">Wanneer een search-aanvraag wordt gedaan met `moreLikeThis`, een lijst met zoektermen is gegenereerd op basis van de frequentie en zeldzaamheid van termen in de brondocument.</span><span class="sxs-lookup"><span data-stu-id="cf52c-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="cf52c-829">Deze voorwaarden worden vervolgens gebruikt om de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cf52c-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="cf52c-830">Standaard wordt de inhoud van alle `searchable` velden worden beschouwd als tenzij `searchFields` wordt gebruikt om te beperken welke velden worden doorzocht.</span><span class="sxs-lookup"><span data-stu-id="cf52c-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="cf52c-831">`$skip=#`(optioneel): het aantal zoekresultaten om over te slaan; Kan niet meer dan 100.000.</span><span class="sxs-lookup"><span data-stu-id="cf52c-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="cf52c-832">Als u wilt scannen van documenten in volgorde, maar kan niet worden gebruikt `$skip` vanwege deze beperking, kunt u overwegen `$orderby` voor een compleet besteld sleutel en `$filter` query in plaats daarvan met een bereik.</span><span class="sxs-lookup"><span data-stu-id="cf52c-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-833">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `skip` in plaats van `$skip`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="cf52c-834">`$top=#`(optioneel): het aantal zoekresultaten om op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="cf52c-835">Dit kan worden gebruikt in combinatie met `$skip` clientzijde oproepen van zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-836">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="cf52c-837">`$count=true|false`(optioneel, wordt standaard ingesteld op `false`)-geeft aan of voor het ophalen van het totale aantal resultaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="cf52c-838">Dit is de telling van alle documenten die overeenkomen met de `search` en `$filter` parameters worden genegeerd `$top` en `$skip`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="cf52c-839">De waarde instelt op `true` mogelijk invloed op de prestaties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="cf52c-840">Houd er rekening mee dat het aantal dat wordt geretourneerd een benadering is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-841">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `count` in plaats van `$count`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="cf52c-842">`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies sorteer de resultaten op.</span><span class="sxs-lookup"><span data-stu-id="cf52c-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="cf52c-843">Elke expressie kan bestaan uit naam van een veld of een aanroep van de `geo.distance()` functie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="cf52c-844">Elke expressie kan worden gevolgd door `asc` aangegeven oplopende, en `desc` om aan te geven aflopende.</span><span class="sxs-lookup"><span data-stu-id="cf52c-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="cf52c-845">De standaardwaarde is oplopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="cf52c-845">The default is ascending order.</span></span> <span data-ttu-id="cf52c-846">Ties wordt de overeenkomst scores van documenten worden opgesplitst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="cf52c-847">Als er geen `$orderby` is opgegeven, wordt de standaardsorteervolgorde is Aflopend op document overeen score.</span><span class="sxs-lookup"><span data-stu-id="cf52c-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="cf52c-848">Er is een limiet van 32 componenten voor `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-849">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="cf52c-850">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden om op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="cf52c-851">Als u niets opgeeft, moet alle velden die zijn gemarkeerd als worden opgehaald in het schema zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="cf52c-852">U kunt ook expliciet alle velden aanvragen door deze parameter in te stellen op `*`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-853">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="cf52c-854">`facet=[string]`(nul of meer) - facet door een veld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="cf52c-855">De tekenreeks kan eventueel parameters voor het aanpassen van de facetten die zijn uitgedrukt als een door komma's gescheiden `name:value` paren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="cf52c-856">Geldige parameters zijn:</span><span class="sxs-lookup"><span data-stu-id="cf52c-856">Valid parameters are:</span></span>

* <span data-ttu-id="cf52c-857">`count`(max. aantal facet voorwaarden; standaardwaarde is 10).</span><span class="sxs-lookup"><span data-stu-id="cf52c-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="cf52c-858">Er is geen maximum maar hogere waarden worden een bijbehorende op de prestaties, vooral als het meervoudige veld een groot aantal unieke voorwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="cf52c-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="cf52c-859">Bijvoorbeeld: `facet=category,count:5` de top vijf categorieën in facet resultaten opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cf52c-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="cf52c-860">**Opmerking**: als de `count` parameter kleiner is dan het aantal unieke termen, de resultaten mogelijk niet nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="cf52c-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="cf52c-861">Dit is vanwege de manier waarop facetten query's zijn verdeeld over shards.</span><span class="sxs-lookup"><span data-stu-id="cf52c-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="cf52c-862">Verhogen `count` doorgaans verhoogt de nauwkeurigheid van de termijn tellingen, maar in een prestatievermindering optreden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="cf52c-863">`sort`(een van de `count` te sorteren *aflopende* op aantal `-count` te sorteren *oplopende* op aantal `value` te sorteren *oplopende* door de waarde of `-value` te sorteren *aflopende* door waarde)</span><span class="sxs-lookup"><span data-stu-id="cf52c-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="cf52c-864">Bijvoorbeeld: `facet=category,count:3,sort:count` opgehaald van de belangrijkste drie categorieën in facet resultaten in aflopende volgorde voor het aantal documenten met de stadsnaam van elke.</span><span class="sxs-lookup"><span data-stu-id="cf52c-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="cf52c-865">Bijvoorbeeld, als de eerste drie categorieën Budget, Motel en luxe zijn, Budget gevonden in de 5 is, Motel 6 en heeft, luxe 4 is, klikt u vervolgens de buckets niet in de volgorde Motel, Budget, luxe.</span><span class="sxs-lookup"><span data-stu-id="cf52c-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="cf52c-866">Bijvoorbeeld: `facet=rating,sort:-value` buckets voor alle mogelijke beoordelingen in aflopende volgorde voor waarde produceert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="cf52c-867">Als de classificaties uit 1 tot en met 5, wordt de buckets besteld 5, 4, 3, 2, 1, ongeacht het aantal documenten overeenkomen met elke beoordeling.</span><span class="sxs-lookup"><span data-stu-id="cf52c-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="cf52c-868">`values`(pipe gescheiden numerieke of `Edm.DateTimeOffset` waarden opgeven van een dynamische set facet vermelding waarden)</span><span class="sxs-lookup"><span data-stu-id="cf52c-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="cf52c-869">Bijvoorbeeld: `facet=baseRate,values:10|20` produceert drie buckets: één voor base snelheid 0 tot en met, maar niet 10, één voor 10 tot inclusief maar niet inclusief 20 en één voor 20 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cf52c-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="cf52c-870">Bijvoorbeeld: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produceert twee buckets: één voor hotels renovated vóór februari 2010 en één voor hotels renovated februari 1e, 2010 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cf52c-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="cf52c-871">`interval`(geheel getal interval dat groter is dan 0 voor getallen, of `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` datumwaarden tijd)</span><span class="sxs-lookup"><span data-stu-id="cf52c-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="cf52c-872">Bijvoorbeeld: `facet=baseRate,interval:100` produceert op basis van base snelheid bereiken met een grootte van 100 buckets.</span><span class="sxs-lookup"><span data-stu-id="cf52c-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="cf52c-873">Bijvoorbeeld, als base tarieven alle tussen $60 en $600, zullen er buckets voor 0-100, 100-200, 200 en 300, 400 500, 300 400 en 500-600.</span><span class="sxs-lookup"><span data-stu-id="cf52c-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="cf52c-874">Bijvoorbeeld: `facet=lastRenovationDate,interval:year` één bucket voor elk jaar wanneer hotels zijn renovated produceert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="cf52c-875">`timeoffset`([+-] hh: mm, [+-] UUMM, of [+-] hh) `timeoffset` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="cf52c-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="cf52c-876">Kan alleen worden gecombineerd met de `interval` optie, en alleen wanneer toegepast op een veld van type `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="cf52c-877">De waarde geeft de UTC-tijd offset voor serviceaccount bij het instellen van tijd grenzen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="cf52c-878">Bijvoorbeeld: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` maakt gebruik van de dag-grens die begint bij 01:00:00 UTC (middernacht in de doel-tijdzone)</span><span class="sxs-lookup"><span data-stu-id="cf52c-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="cf52c-879">**Opmerking**: `count` en `sort` kunnen worden gecombineerd in dezelfde facet-specificatie, maar kan niet worden gecombineerd met `interval` of `values`, en `interval` en `values` kan niet worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="cf52c-880">**Opmerking**: Interval facetten op datum / tijd worden berekend op basis van UTC-tijd als `timeoffset` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="cf52c-881">Bijvoorbeeld: voor `facet=lastRenovationDate,interval:day`, de dag grens bij 00:00:00 UTC begint.</span><span class="sxs-lookup"><span data-stu-id="cf52c-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf52c-882">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `facets` in plaats van `facet`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="cf52c-883">Bovendien geeft u het als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke facet-expressie is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="cf52c-884">`$filter=[string]`(optioneel): een zoekexpressie gestructureerde in de standaard OData-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="cf52c-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-885">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="cf52c-886">`highlight=[string]`(optioneel): een reeks door komma's gescheiden veldnamen gebruikt voor treffer worden gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="cf52c-887">Alleen `searchable` velden kunnen worden gebruikt voor treffers markeren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="cf52c-888">`highlightPreTag=[string]`(optioneel, wordt standaard ingesteld op `<em>`): een string-code die voegt toe om licht bereikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="cf52c-889">Moet worden ingesteld met `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-890">Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in de URL moet procent gecodeerd (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="cf52c-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="cf52c-891">`highlightPostTag=[string]`(optioneel, wordt standaard ingesteld op `</em>`)-een string-code die wordt toegevoegd voor licht bereikt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="cf52c-892">Moet worden ingesteld met `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-893">Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in de URL moet procent gecodeerd (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="cf52c-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="cf52c-894">`scoringProfile=[string]`(optioneel): de naam van een scoreprofiel evalueren overeen scores voor documenten-koppeling om de resultaten te sorteren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="cf52c-895">`scoringParameter=[string]`Geeft aan de waarden voor elke parameter die is gedefinieerd in een score-functie (nul of meer) - (bijvoorbeeld `referencePointParameter`) met de indeling `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="cf52c-896">Bijvoorbeeld, als de scoreprofiel een functie met een parameter met de naam 'mylocation definieert' de queryoptie-tekenreeks zou zijn `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="cf52c-897">Het eerste streepje scheidt u de naam van de lijst met waarden terwijl de tweede streepje deel uit van de eerste waarde (lengtegraad in dit voorbeeld maakt).</span><span class="sxs-lookup"><span data-stu-id="cf52c-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="cf52c-898">Scoreprofiel parameters kunt u een dergelijke waarden in de lijst met enkele aanhalingstekens escape zoals voor de code die versterking kunt bevatten komma's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="cf52c-899">Als de waarden zelf tussen enkele aanhalingstekens bevatten, kunt u dit omheen door te verdubbelen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="cf52c-900">Bijvoorbeeld, als u een parameter met de naam 'mytag' versterking label hebben en u wilt verhogen in het label waarden 'Hallo, O'Brien' en 'Smith' de query verbindingsreeksoptie zou worden `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="cf52c-901">Aanhalingstekens zijn alleen vereist voor waarden die door komma's bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-902">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `scoringParameters` in plaats van `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="cf52c-903">U ook als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke is `name-values` paar.</span><span class="sxs-lookup"><span data-stu-id="cf52c-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="cf52c-904">`minimumCoverage`(optioneel, de standaardwaarde is 100)-een getal tussen 0 en 100 die het percentage van de index die moet worden gedekt door een zoekopdracht om de query moet worden gerapporteerd als een succes aangeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="cf52c-905">Standaard de gehele index moet beschikbaar zijn of `Search` HTTP-statuscode 503 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="cf52c-906">Als u instelt `minimumCoverage` en `Search` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord die het percentage van de index die is opgenomen in de query aangeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-907">Als deze parameter op een waarde lager dan 100 is handig voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica.</span><span class="sxs-lookup"><span data-stu-id="cf52c-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="cf52c-908">Niet alle overeenkomende documenten zijn echter gegarandeerd aanwezig zijn in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="cf52c-909">Als zoeken intrekken belangrijker voor uw toepassing dan beschikbaarheid, wordt het is raadzaam om te laten `minimumCoverage` op de standaardwaarde van 100.</span><span class="sxs-lookup"><span data-stu-id="cf52c-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="cf52c-910">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-911">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-912">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-913">Opmerking: voor deze bewerking, de `api-version` is opgegeven als een queryparameter in de URL ongeacht of u aanroepen **Search** met GET of POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="cf52c-914">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-914">**Request Headers**</span></span>

<span data-ttu-id="cf52c-915">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-916">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-917">Het is een tekenreekswaarde die uniek is voor uw service-URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="cf52c-918">De **Search** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="cf52c-919">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-920">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-921">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-922">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-922">**Request Body**</span></span>

<span data-ttu-id="cf52c-923">Voor GET: geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-923">For GET: None.</span></span>

<span data-ttu-id="cf52c-924">Voor POST:</span><span class="sxs-lookup"><span data-stu-id="cf52c-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="cf52c-925">**Voortzetting van antwoorden voor Deelzoekopdrachten**</span><span class="sxs-lookup"><span data-stu-id="cf52c-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="cf52c-926">Soms kan geen Azure Search alle aangevraagde resultaten retourneren in een enkel antwoord met zoeken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="cf52c-927">Dit kan gebeuren om verschillende redenen, zoals wanneer de query te veel documenten aanvragen door op te geven niet `$top` of een waarde opgeeft voor `$top` die te groot is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="cf52c-928">In dergelijke gevallen kunt u Azure Search bevat de `@odata.nextLink` aantekening in de hoofdtekst van antwoord en ook `@search.nextPageParameters` als deze een POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cf52c-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="cf52c-929">De waarden van deze aantekeningen kunt u een andere Search-aanvraag voor het ophalen van het volgende gedeelte van het antwoord van de zoekactie te formuleren.</span><span class="sxs-lookup"><span data-stu-id="cf52c-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="cf52c-930">Dit wordt genoemd, een ***voortzetting*** van de oorspronkelijke zoekopdracht aanvraag en de aantekeningen in het algemeen worden genoemd ***voortzetting tokens***.</span><span class="sxs-lookup"><span data-stu-id="cf52c-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="cf52c-931">Zie [het onderstaande voorbeeld](#SearchResponse) voor meer informatie over de syntaxis van deze aantekeningen en waar ze worden weergegeven in de hoofdtekst van het antwoord.</span><span class="sxs-lookup"><span data-stu-id="cf52c-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="cf52c-932">De redenen waarom Azure Search voortzetting tokens retourneert zijn implementatie en kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="cf52c-933">Robuuste clients moet altijd gereed is voor het afhandelen van gevallen waarbij minder documenten dan verwacht worden geretourneerd en een vervolgtoken is opgenomen om door te gaan met het ophalen van documenten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="cf52c-934">Houd er ook rekening mee dat u dezelfde HTTP-methode als de oorspronkelijke aanvraag gebruiken moet om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="cf52c-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="cf52c-935">Bijvoorbeeld, als u een GET-aanvraag verzonden, voortzetting verzoeken u verzendt moeten ook gebruiken GET (en ook voor POST).</span><span class="sxs-lookup"><span data-stu-id="cf52c-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="cf52c-936"><a name="SearchResponse"></a>
**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="cf52c-937">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="cf52c-938">**Voorbeelden:**</span><span class="sxs-lookup"><span data-stu-id="cf52c-938">**Examples:**</span></span>

<span data-ttu-id="cf52c-939">U vindt aanvullende voorbeelden gegeven op de [OData-expressiesyntaxis voor Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="cf52c-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="cf52c-940">Zoeken in de Index gesorteerd Aflopend op datum.</span><span class="sxs-lookup"><span data-stu-id="cf52c-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="cf52c-941">GET-/indexes/hotels/docs? zoeken = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'orderby': "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="cf52c-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="cf52c-943">Zoeken in de index in een meervoudige zoekopdracht, en facetten voor categorieën, classificatie, labels, evenals artikelen met baseRate in specifieke bereiken ophalen:</span><span class="sxs-lookup"><span data-stu-id="cf52c-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="cf52c-944">GET /indexes/hotels/docs? zoeken = test & facet = categorie & facet = classificatie & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['categorie', 'classificatie', 'tags', ' baseRate, waarden: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="cf52c-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="cf52c-946">De queryresultaten van de vorige meervoudige met een filter beperken nadat de gebruiker klikt op classificatie 3 en categorie 'Motel':</span><span class="sxs-lookup"><span data-stu-id="cf52c-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="cf52c-947">GET /indexes/hotels/docs? zoeken = test & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & $filter = classificatie eq 3 en categorie-eq "Motel" & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['tags', ' baseRate, waarden: 80 | 150 | 220"], 'filter': 'classificatie eq 3 en categorie-eq 'Motel' '}</span><span class="sxs-lookup"><span data-stu-id="cf52c-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="cf52c-949">In een meervoudige zoekopdracht, moet u een bovenlimiet instellen op unieke voorwaarden in een query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="cf52c-950">De standaardwaarde is 10, maar u kunt vergroten of verkleinen van deze waarde met behulp van de `count` parameter bij de `facet` kenmerk:</span><span class="sxs-lookup"><span data-stu-id="cf52c-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="cf52c-951">GET-/indexes/hotels/docs? zoeken = test & facet = city, aantal: 5 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'zoeken': 'test', 'facetten': ["city, aantal: 5"]}</span><span class="sxs-lookup"><span data-stu-id="cf52c-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="cf52c-953">Zoeken in de Index binnen specifieke velden; Bijvoorbeeld, een specifieke taal zijn gebonden veld:</span><span class="sxs-lookup"><span data-stu-id="cf52c-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="cf52c-954">GET-/indexes/hotels/docs? zoeken = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "hôtel', 'searchFields':"description_fr"}</span><span class="sxs-lookup"><span data-stu-id="cf52c-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="cf52c-956">De Index zoeken in meerdere velden.</span><span class="sxs-lookup"><span data-stu-id="cf52c-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="cf52c-957">U kunt bijvoorbeeld, opslaan en opvragen doorzoekbare velden in meerdere talen, allemaal binnen dezelfde index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="cf52c-958">Als de Engelse en Franse beschrijvingen in hetzelfde document naast elkaar bestaan, kunt u een of meer in de queryresultaten retourneren:</span><span class="sxs-lookup"><span data-stu-id="cf52c-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="cf52c-959">GET-/indexes/hotels/docs? zoeken = hotel & searchFields = beschrijving, description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "Hotels", "searchFields": "beschrijving, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="cf52c-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="cf52c-961">Houd er rekening mee dat u kunt alleen een query één index op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="cf52c-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="cf52c-962">Maak meerdere indexen voor elke taal geen tenzij u van plan bent een voor een query.</span><span class="sxs-lookup"><span data-stu-id="cf52c-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="cf52c-963">Wisselbestand - Get de 1e pagina van de items (paginaformaat is 10):</span><span class="sxs-lookup"><span data-stu-id="cf52c-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="cf52c-964">GET-/indexes/hotels/docs? zoeken = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "* ', 'overslaan': 0, 'top': 10}</span><span class="sxs-lookup"><span data-stu-id="cf52c-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="cf52c-966">Wisselbestand - Get van de 2e pagina van de items (paginaformaat is 10):</span><span class="sxs-lookup"><span data-stu-id="cf52c-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="cf52c-967">GET-/indexes/hotels/docs? zoeken = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'search': ' * ', 'overslaan': 10, 'top': 10}</span><span class="sxs-lookup"><span data-stu-id="cf52c-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="cf52c-969">Ophalen van een specifieke set velden:</span><span class="sxs-lookup"><span data-stu-id="cf52c-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="cf52c-970">GET-/indexes/hotels/docs? zoeken = * & $select = hotelName, beschrijving en api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'select': "hotelName Beschrijving"}</span><span class="sxs-lookup"><span data-stu-id="cf52c-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="cf52c-972">Ophalen van documenten die overeenkomt met een specifieke filterexpressie:</span><span class="sxs-lookup"><span data-stu-id="cf52c-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="cf52c-973">GET-/indexes/hotels/docs? $filter = (baseRate ge 60 en baseRate lt 300) of hotelName eq fraai blijven & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'filter': ' (baseRate ge 60 en baseRate lt 300) of hotelName eq 'Fraai verblijf' "}</span><span class="sxs-lookup"><span data-stu-id="cf52c-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="cf52c-975">De index en keer terug fragmenten met treffers licht zoeken</span><span class="sxs-lookup"><span data-stu-id="cf52c-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="cf52c-976">GET-/indexes/hotels/docs? zoeken = iets & Markeer = beschrijving & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets", "highlight": 'beschrijving'}</span><span class="sxs-lookup"><span data-stu-id="cf52c-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="cf52c-978">Zoeken in de index en documenten van dichter bij verder weg van verwijzing naar een locatie gesorteerd retourneren</span><span class="sxs-lookup"><span data-stu-id="cf52c-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="cf52c-979">GET-/indexes/hotels/docs? zoeken = iets & $orderby=geo.distance (locatie, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'orderby': ' geo.distance (locatie, geography'POINT(-122.12315 47.88121)')"}</span><span class="sxs-lookup"><span data-stu-id="cf52c-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="cf52c-981">Zoeken in de index ervan uitgaande dat er is een 'geografisch' aangeroepen scoreprofiel met twee afstandsscorefuncties, één definiëren van een parameter genaamd 'currentLocation' en één voor het definiëren van een parameter met de naam 'lastLocation'</span><span class="sxs-lookup"><span data-stu-id="cf52c-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="cf52c-982">GET /indexes/hotels/docs? zoeken = iets & scoringProfile = geo & scoringParameter = currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'scoringProfile': 'geo', 'scoringParameters': [' currentLocation--122.123,44.77233 ', ' lastLocation--121.499,44.2113 ']}</span><span class="sxs-lookup"><span data-stu-id="cf52c-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="cf52c-984">Documenten zoeken in de index met behulp [vereenvoudigde querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="cf52c-985">Deze query retourneert hotels waar doorzoekbare velden de termen 'comfort' en 'locatie', maar niet 'motel bevatten':</span><span class="sxs-lookup"><span data-stu-id="cf52c-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="cf52c-986">GET-/indexes/hotels/docs? zoeken = comfort + locatie-motel & searchMode = all & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="cf52c-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="cf52c-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "comfort + locatie-motel ', 'searchMode': 'alle'}</span><span class="sxs-lookup"><span data-stu-id="cf52c-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="cf52c-988">Let op het gebruik van `searchMode=all` hierboven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="cf52c-989">De standaardwaarde van deze parameter inclusief overschrijft `searchMode=any`, zorgt dat `-motel` 'En niet' in plaats van "Of niet" betekent.</span><span class="sxs-lookup"><span data-stu-id="cf52c-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="cf52c-990">Zonder `searchMode=all`u "Of niet" dat wordt uitgebreid dan beperkt zoekresultaten ophalen en dit kan erg intuïtief om bepaalde gebruikers zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="cf52c-991">Documenten zoeken in de index met behulp [lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf52c-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="cf52c-992">Deze query retourneert hotels waar de categorieveld bevat de term 'budget' en de doorzoekbare velden die de zin 'onlangs renovated'.</span><span class="sxs-lookup"><span data-stu-id="cf52c-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="cf52c-993">Documenten met de zinsnede 'onlangs renovated' krijgen een hogere rang als gevolg van de termijn versterking waarde (3)</span><span class="sxs-lookup"><span data-stu-id="cf52c-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="cf52c-994">GET-/indexes/hotels/docs? zoeken = categorie: budget en \"onlangs renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & querytype = full</span><span class="sxs-lookup"><span data-stu-id="cf52c-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="cf52c-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "categorie: budget en \"onlangs renovated\"^ 3", 'queryType': 'volledige', 'searchMode': 'alle'}</span><span class="sxs-lookup"><span data-stu-id="cf52c-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="cf52c-996">Lookup-Document</span><span class="sxs-lookup"><span data-stu-id="cf52c-996">Lookup Document</span></span>
<span data-ttu-id="cf52c-997">De **Lookup Document** bewerking een document opgehaald uit Azure Search.</span><span class="sxs-lookup"><span data-stu-id="cf52c-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="cf52c-998">Dit is handig wanneer een gebruiker op een specifieke zoekresultaat klikt en u wilt zoeken om specifieke details over dat document.</span><span class="sxs-lookup"><span data-stu-id="cf52c-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="cf52c-999">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-999">**Request**</span></span>

<span data-ttu-id="cf52c-1000">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-1001">De **Lookup Document** verzoek als volgt kan worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="cf52c-1002">U kunt ook kunt u de traditionele OData-syntaxis voor het opzoeken van een sleutel:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="cf52c-1003">De aanvraag-URI bevat [index name] en [sleutel], die aangeeft welk document op te halen uit welke index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="cf52c-1004">U kunt slechts één document tegelijk ophalen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1004">You can only get one document at a time.</span></span> <span data-ttu-id="cf52c-1005">Gebruik **Search** meerdere documenten in één aanvraag ophalen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="cf52c-1006">**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1006">**Query Parameters**</span></span>

<span data-ttu-id="cf52c-1007">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden om op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="cf52c-1008">Als dat niet-opgegeven of ingesteld op `*`, alle velden die zijn gemarkeerd als worden opgehaald in het schema zijn opgenomen in de projectie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="cf52c-1009">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-1010">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-1011">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-1012">Opmerking: voor deze bewerking, de `api-version` is opgegeven als een queryparameter.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="cf52c-1013">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1013">**Request Headers**</span></span>

<span data-ttu-id="cf52c-1014">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-1015">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-1016">Het is een tekenreekswaarde die uniek is voor uw service-URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="cf52c-1017">De **Lookup Document** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="cf52c-1018">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-1019">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-1020">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-1021">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1021">**Request Body**</span></span>

<span data-ttu-id="cf52c-1022">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1022">None.</span></span>

<span data-ttu-id="cf52c-1023">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1023">**Response**</span></span>

<span data-ttu-id="cf52c-1024">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="cf52c-1025">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1025">**Example**</span></span>

<span data-ttu-id="cf52c-1026">Het document dat de sleutel '2' heeft lookup</span><span class="sxs-lookup"><span data-stu-id="cf52c-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="cf52c-1027">Het document dat uit de sleutel met OData-syntaxis 3 lookup:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="cf52c-1028">Aantal documenten</span><span class="sxs-lookup"><span data-stu-id="cf52c-1028">Count Documents</span></span>
<span data-ttu-id="cf52c-1029">De **aantal documenten** bewerking wordt een telling van het aantal documenten in een zoekindex opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="cf52c-1030">De `$count` syntaxis maakt deel uit van het OData-protocol.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="cf52c-1031">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1031">**Request**</span></span>

<span data-ttu-id="cf52c-1032">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-1033">De **aantal documenten** aanvraag kan worden opgesteld met de GET-methode.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="cf52c-1034">De [indexnaam] in de aanvraag-URI Hiermee geeft u de service te retourneren van een telling van alle items in de verzameling documenten van de opgegeven index.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="cf52c-1035">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-1036">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-1037">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-1038">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1038">**Request Headers**</span></span>

<span data-ttu-id="cf52c-1039">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="cf52c-1040">`Accept`: Met deze waarde moet worden ingesteld op `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="cf52c-1041">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-1042">Het is een tekenreekswaarde die uniek is voor uw service-URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="cf52c-1043">De **aantal documenten** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="cf52c-1044">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-1045">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-1046">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-1047">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1047">**Request Body**</span></span>

<span data-ttu-id="cf52c-1048">Geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1048">None.</span></span>

<span data-ttu-id="cf52c-1049">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1049">**Response**</span></span>

<span data-ttu-id="cf52c-1050">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="cf52c-1051">Hoofdtekst van de reactie bevat de count-waarde als een geheel getal als tekst zonder opmaak geformatteerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="cf52c-1052">Suggesties</span><span class="sxs-lookup"><span data-stu-id="cf52c-1052">Suggestions</span></span>
<span data-ttu-id="cf52c-1053">De **suggesties** bewerking suggesties op basis van deelzoekopdrachten invoer worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="cf52c-1054">Dit wordt doorgaans gebruikt in de zoekvakken opgeven type-ahead suggesties gebruikers zoektermen invoert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="cf52c-1055">Suggestie aanvragen gericht op de voorstellen doeldocumenten, zodat de voorgestelde tekst kan worden herhaald als meerdere candidate documenten invoer dezelfde zoekopdracht overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="cf52c-1056">U kunt `$select` om op te halen van andere documentvelden (inclusief de documentsleutel) zodat u kunt zien welke document is de bron voor elke suggestie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="cf52c-1057">Een **suggesties** bewerking als een GET of POST-aanvraag is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="cf52c-1058">**Wanneer POST gebruiken in plaats van GET**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="cf52c-1059">Wanneer u HTTP GET aan te roepen de **suggesties** API, moet u er rekening mee dat de lengte van de aanvraag-URL kan niet hoger is dan 8 KB.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="cf52c-1060">Dit is meestal genoeg voor de meeste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="cf52c-1061">Sommige toepassingen produceren echter zeer grote query's specifiek OData-filterexpressies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="cf52c-1062">Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters dan GET.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="cf52c-1063">Met POST is het aantal componenten in een filter de beperkende factor, niet de grootte van de onbewerkte filtertekenreeks omdat de limiet voor de aanvraag voor POST ongeveer 16 MB is.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1064">Hoewel de maximale grootte van POST-aanvraag erg groot is, kunnen niet filterexpressies willekeurig complex zijn.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="cf52c-1065">Zie [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over filter complexiteit beperkingen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="cf52c-1066">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1066">**Request**</span></span>

<span data-ttu-id="cf52c-1067">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="cf52c-1068">De **suggesties** aanvraag kan worden opgesteld met de methoden GET of POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="cf52c-1069">De aanvraag-URI bevat de naam van de index van de query.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="cf52c-1070">Parameters, zoals de gedeeltelijk invoer zoekterm zijn opgegeven voor de queryreeks weergegeven in het geval van GET-aanvragen en in de aanvraag hoofdtekst in het geval van POST-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="cf52c-1071">Als een best practice bij het maken van GET-aanvragen, moet u [URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke queryparameters bij het aanroepen van de REST-API rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="cf52c-1072">Voor **suggesties** bewerkingen, dit omvat:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="cf52c-1073">URL-codering wordt alleen aanbevolen voor de bovenstaande queryparameters.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="cf52c-1074">Als u per ongeluk URL coderen de volledige query-tekenreeks (alles na de?), aanvragen worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="cf52c-1075">Zo is de URL-codering ook alleen nodig bij het aanroepen van de REST-API die rechtstreeks met de GET.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="cf52c-1076">Er is geen URL-codering is nodig bij het aanroepen van **suggesties** POST, met of wanneer u de [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die URL-codering voor u verwerkt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="cf52c-1077">**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1077">**Query Parameters**</span></span>

<span data-ttu-id="cf52c-1078">**Suggesties** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="cf52c-1079">U opgeven dat deze parameters in de URL van de querytekenreeks bij het aanroepen van **suggesties** via GET en als JSON-eigenschappen in de aanvraagtekst bij het aanroepen van **suggesties** via POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="cf52c-1080">De syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="cf52c-1081">Deze verschillen worden vermeld als die van toepassing zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="cf52c-1082">`search=[string]`-de tekst moet worden gebruikt voor het voorstellen van query's.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="cf52c-1083">Moet minimaal 1 teken en niet meer dan 100 tekens.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="cf52c-1084">`highlightPreTag=[string]`(optioneel): een tekenreeks tag die voegt toe om te zoeken naar treffers.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="cf52c-1085">Moet worden ingesteld met `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1086">Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in de URL moet procent gecodeerd (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="cf52c-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="cf52c-1087">`highlightPostTag=[string]`(optioneel): een tekenreeks tag die worden toegevoegd om te zoeken naar treffers.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="cf52c-1088">Moet worden ingesteld met `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1089">Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in de URL moet procent gecodeerd (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="cf52c-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="cf52c-1090">`suggesterName=[string]`-de naam van de suggestie zoals opgegeven in de `suggesters` verzameling die deel uitmaakt van de indexdefinitie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="cf52c-1091">Een `suggester` bepaalt welke velden voor voorgestelde querytermen worden gescand.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="cf52c-1092">Zie [Suggestiefunctie](#Suggesters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="cf52c-1093">`fuzzy=[boolean]`(optioneel, standaard = false)-als ingesteld op waar deze API vindt u suggesties zelfs als er een teken vervangen of ontbreekt in de zoektekst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="cf52c-1094">Het wordt geleverd op de prestaties, zoals fuzzy suggestie zoekopdrachten trager en meer bronnen gebruiken terwijl dit een betere ervaring in sommige scenario's biedt.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="cf52c-1095">`searchFields=[string]`(optioneel): de lijst met door komma's gescheiden veldnamen om te zoeken naar de opgegeven zoektekst.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="cf52c-1096">Doelvelden moeten zijn ingeschakeld voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="cf52c-1097">`$top=#`(optioneel, standaard = 5)-het aantal suggesties om op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="cf52c-1098">Moet een getal tussen 1 en 100 liggen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1099">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="cf52c-1100">`$filter=[string]`(optioneel): een expressie die de documenten filters in aanmerking voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1101">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="cf52c-1102">`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies sorteer de resultaten op.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="cf52c-1103">Elke expressie kan bestaan uit naam van een veld of een aanroep van de `geo.distance()` functie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="cf52c-1104">Elke expressie kan worden gevolgd door `asc` aangegeven oplopende, en `desc` om aan te geven aflopende.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="cf52c-1105">De standaardwaarde is oplopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1105">The default is ascending order.</span></span> <span data-ttu-id="cf52c-1106">Er is een limiet van 32 componenten voor `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1107">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="cf52c-1108">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden om op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="cf52c-1109">Als u niets opgeeft, worden alleen de sleutel en suggestie tekst wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="cf52c-1110">U kunt alle velden expliciet aanvragen door deze parameter in te stellen op `*`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1111">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="cf52c-1112">`minimumCoverage`(optioneel, de standaardwaarde 80)-een getal tussen 0 en 100 die het percentage van de index die moet worden gedekt door een query suggesties om de query moet worden gerapporteerd als een succes aangeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="cf52c-1113">Standaard ten minste 80% van de index moet beschikbaar zijn of `Suggest` HTTP-statuscode 503 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="cf52c-1114">Als u instelt `minimumCoverage` en `Suggest` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord die het percentage van de index die is opgenomen in de query aangeeft.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="cf52c-1115">Als deze parameter op een waarde lager dan 100 is handig voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="cf52c-1116">Niet alle overeenkomende suggesties zijn echter gegarandeerd aanwezig zijn in de resultaten.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="cf52c-1117">Als intrekken belangrijker voor uw toepassing dan beschikbaarheid, wordt het is raadzaam niet te verlagen `minimumCoverage` lager dan de standaardwaarde 80.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="cf52c-1118">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="cf52c-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="cf52c-1119">De preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="cf52c-1120">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="cf52c-1121">Opmerking: voor deze bewerking, de `api-version` is opgegeven als een queryparameter in de URL ongeacht of u aanroepen **suggesties** met GET of POST.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="cf52c-1122">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1122">**Request Headers**</span></span>

<span data-ttu-id="cf52c-1123">De volgende lijst beschrijft de vereiste en optionele aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="cf52c-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="cf52c-1124">`api-key`: De `api-key` wordt gebruikt voor verificatie van de aanvraag voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="cf52c-1125">Het is een tekenreekswaarde die uniek is voor uw service-URL.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="cf52c-1126">De **suggesties** aanvraag kunt opgeven, een beheersleutel of een querysleutel als de `api-key`.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="cf52c-1127">U moet ook de naam van de service om de aanvraag-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="cf52c-1128">U krijgt de servicenaam en `api-key` van uw servicedashboard in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="cf52c-1129">Zie [maken van een Azure Search-service in de portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="cf52c-1130">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1130">**Request Body**</span></span>

<span data-ttu-id="cf52c-1131">Voor GET: geen.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1131">For GET: None.</span></span>

<span data-ttu-id="cf52c-1132">Voor POST:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="cf52c-1133">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1133">**Response**</span></span>

<span data-ttu-id="cf52c-1134">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="cf52c-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="cf52c-1135">Als de optie projectie wordt gebruikt voor het ophalen van velden die zijn opgenomen in elk element van de matrix:</span><span class="sxs-lookup"><span data-stu-id="cf52c-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="cf52c-1136">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="cf52c-1136">**Example**</span></span>

<span data-ttu-id="cf52c-1137">5 suggesties waar de deelzoekopdrachten-invoer is 'lux' ophalen</span><span class="sxs-lookup"><span data-stu-id="cf52c-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
