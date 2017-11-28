---
title: aaaAzure Search Service REST API-versie Preview 2015-02-28-| Microsoft Docs
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
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="943ec-103">Azure Search Service REST-API: Versie 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="943ec-104">Dit artikel is Hallo-naslagdocumentatie voor `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-105">Deze preview Hallo huidige algemeen beschikbaar versie, breidt [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), doordat Hallo volgende experimentele kenmerken:</span><span class="sxs-lookup"><span data-stu-id="943ec-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="943ec-106">`moreLikeThis`queryparameter in Hallo [documenten zoeken](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="943ec-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="943ec-107">Andere documenten die specifiek document relevante tooanother zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="943ec-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="943ec-108">Een paar extra onderdelen van Hallo `2015-02-28-Preview` REST-API afzonderlijk worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="943ec-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="943ec-109">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="943ec-109">These include:</span></span>

* [<span data-ttu-id="943ec-110">Score berekenen voor profielen</span><span class="sxs-lookup"><span data-stu-id="943ec-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="943ec-111">Indexeerfuncties</span><span class="sxs-lookup"><span data-stu-id="943ec-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="943ec-112">Azure Search-service is beschikbaar in meerdere versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="943ec-113">Raadpleeg het te[Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="943ec-114">API's in dit document</span><span class="sxs-lookup"><span data-stu-id="943ec-114">APIs in this document</span></span>
<span data-ttu-id="943ec-115">Azure-API van zoekservice ondersteunt twee URL-syntaxis voor de API-bewerkingen: eenvoudige en OData (Zie [ondersteuning voor OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="943ec-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="943ec-116">Hallo bevat volgende lijst eenvoudige Hallo-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="943ec-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="943ec-117">Index maken</span><span class="sxs-lookup"><span data-stu-id="943ec-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-118">Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="943ec-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-119">Index ophalen</span><span class="sxs-lookup"><span data-stu-id="943ec-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-120">Aanbieding-indexen</span><span class="sxs-lookup"><span data-stu-id="943ec-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-121">Indexstatistieken opvragen</span><span class="sxs-lookup"><span data-stu-id="943ec-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-122">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="943ec-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-123">Een Index verwijderen</span><span class="sxs-lookup"><span data-stu-id="943ec-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-124">Toevoegen, verwijderen, en gegevens in een Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="943ec-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-125">Documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="943ec-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-126">Lookup-Document</span><span class="sxs-lookup"><span data-stu-id="943ec-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="943ec-127">Aantal documenten</span><span class="sxs-lookup"><span data-stu-id="943ec-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="943ec-128">Suggesties</span><span class="sxs-lookup"><span data-stu-id="943ec-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="943ec-129">Indexbewerkingen</span><span class="sxs-lookup"><span data-stu-id="943ec-129">Index Operations</span></span>
<span data-ttu-id="943ec-130">U kunt maken en beheren van de indexen in Azure Search-service via een eenvoudige HTTP-aanvragen (POST, GET, PUT, DELETE) op basis van een resource voor de gegeven index.</span><span class="sxs-lookup"><span data-stu-id="943ec-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="943ec-131">toocreate een index u boeken eerst een JSON-document met een beschrijving van Hallo Indexeer schema.</span><span class="sxs-lookup"><span data-stu-id="943ec-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="943ec-132">Hallo schema gedefinieerd Hallo velden van het Hallo-index, de gegevenstypen en hoe ze kunnen worden gebruikt (bijvoorbeeld in zoekopdrachten in volledige tekst, filters, sorteren of facetten).</span><span class="sxs-lookup"><span data-stu-id="943ec-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="943ec-133">Het definieert ook scoreprofiel profielen, suggestiefunctie en andere kenmerken tooconfigure Hallo gedrag van Hallo index.</span><span class="sxs-lookup"><span data-stu-id="943ec-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="943ec-134">Hallo bevat volgende voorbeeld een afbeelding van een schema dat wordt gebruikt voor zoekopdrachten op gegevens van hotel met Hallo beschrijvingsveld gedefinieerd in twee talen.</span><span class="sxs-lookup"><span data-stu-id="943ec-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="943ec-135">U ziet hoe kenmerken bepalen hoe Hallo veld wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="943ec-136">Bijvoorbeeld Hallo `hotelId` wordt gebruikt als de documentsleutel hello (`"key": true`) en wordt uitgesloten van zoekopdrachten in volledige tekst (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="943ec-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="943ec-137">Nadat Hallo index is gemaakt, kunt u documenten die Hallo index vullen gaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="943ec-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="943ec-138">Zie [toevoegen of Update documenten](#AddOrUpdateDocuments) voor deze stap.</span><span class="sxs-lookup"><span data-stu-id="943ec-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="943ec-139">Zie voor een video-inleiding tooindexing in Azure Search, Hallo [aflevering Channel 9 Cloud hebben betrekking op Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="943ec-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="943ec-140">Index maken</span><span class="sxs-lookup"><span data-stu-id="943ec-140">Create Index</span></span>
<span data-ttu-id="943ec-141">Een index is Hallo primaire methode voor het ordenen en documenten zoeken in Azure Search, vergelijkbare toohow een tabel ordent records in een database.</span><span class="sxs-lookup"><span data-stu-id="943ec-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="943ec-142">Elke index heeft een verzameling van documenten dat alle toohello indexschema (veldnamen, gegevenstypen en eigenschappen) voldoen, maar indexen ook aanvullende constructies (suggestiefunctie, score-profielen en opties voor CORS) waarmee andere zoekgedrag opgeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="943ec-143">U kunt een nieuwe index maken in Azure Search-service met behulp van een HTTP POST of PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="943ec-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="943ec-144">Hallo-hoofdtekst van Hallo-aanvraag is een JSON-schema dat Hallo index en configuratie-informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="943ec-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="943ec-145">U kunt ook gebruik van PUT en Hallo indexnaam op Hallo URI opgeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="943ec-146">Als het Hallo-index niet bestaat, kunt u deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="943ec-147">Maken van een index bepaalt Hallo-structuur van Hallo documenten opgeslagen en gebruikt in zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="943ec-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="943ec-148">Invullen Hallo index is een afzonderlijke bewerking.</span><span class="sxs-lookup"><span data-stu-id="943ec-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="943ec-149">Voor deze stap kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/azure/mt183328.aspx) (beschikbaar voor ondersteunde gegevensbronnen) of een [toevoegen, bijwerken of verwijderen van documenten](https://msdn.microsoft.com/library/azure/dn798930.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="943ec-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="943ec-150">Hallo omgekeerde index wordt gegenereerd wanneer het Hallo-documenten zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="943ec-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="943ec-151">**Opmerking**: Hallo kunt u het maximum aantal indexen toegestaan hangt af van de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="943ec-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="943ec-152">Hallo gratis service kunt u too3 indexen.</span><span class="sxs-lookup"><span data-stu-id="943ec-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="943ec-153">Standard-service kan 50-indexen per zoekservice.</span><span class="sxs-lookup"><span data-stu-id="943ec-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="943ec-154">Zie [limieten en beperkingen](http://msdn.microsoft.com/library/azure/dn798934.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="943ec-155">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-155">**Request**</span></span>

<span data-ttu-id="943ec-156">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="943ec-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="943ec-157">Hallo **Create Index** aanvraag kan worden geconstrueerd met een methode POST of PUT.</span><span class="sxs-lookup"><span data-stu-id="943ec-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="943ec-158">Wanneer u POST, moet u de naam van een index in de aanvraagtekst Hallo samen met de indexdefinitie schema Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="943ec-159">Met opslag is de indexnaam Hallo deel van Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="943ec-160">Als het Hallo-index niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="943ec-161">Als deze al bestaat, is het bijgewerkte toohello nieuwe definitie.</span><span class="sxs-lookup"><span data-stu-id="943ec-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="943ec-162">Hallo indexnaam moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="943ec-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="943ec-163">Hallo rest van de naam van de Hallo kan na het starten van de indexnaam Hallo met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang Hallo streepjes niet opeenvolgende zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="943ec-164">Hallo `api-version` is vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-164">hello `api-version` is required.</span></span> <span data-ttu-id="943ec-165">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor een lijst met beschikbare versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="943ec-166">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-166">**Request Headers**</span></span>

<span data-ttu-id="943ec-167">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-168">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-168">`Content-Type`: Required.</span></span> <span data-ttu-id="943ec-169">Stel deze optie te`application/json`</span><span class="sxs-lookup"><span data-stu-id="943ec-169">Set this too`application/json`</span></span>
* <span data-ttu-id="943ec-170">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-170">`api-key`: Required.</span></span> <span data-ttu-id="943ec-171">Hallo `api-key` wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="943ec-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="943ec-172">Hallo aanvraag tooyour Search-service worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-173">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-174">Hallo **Create Index** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-175">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-176">U kunt beide servicenaam Hallo ophalen en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-177">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-178"><a name="RequestData"></a>
**Syntaxis van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="943ec-179">Hallo-hoofdtekst van Hallo-aanvraag bevat een schemadefinitie, waaronder Hallo lijst met gegevensvelden binnen de documenten die zal worden opgenomen in deze index, gegevenstypen, kenmerken, evenals een optionele lijst met profielen voor score berekenen gebruikte tooscore die overeenkomt met de documenten op Querytijd.</span><span class="sxs-lookup"><span data-stu-id="943ec-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="943ec-180">Houd er rekening mee voor een POST-aanvraag moet u de indexnaam Hallo opgeven in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="943ec-181">Er kan alleen worden één sleutelveld in Hallo index.</span><span class="sxs-lookup"><span data-stu-id="943ec-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="943ec-182">Toobe heeft een string-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-182">It has toobe a string field.</span></span> <span data-ttu-id="943ec-183">Dit veld wordt de unieke id voor elk document dat is opgeslagen in de index Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="943ec-184">belangrijkste onderdelen van een index Hallo zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="943ec-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="943ec-185">`fields`die zal worden opgenomen in deze index, zoals naam, gegevenstype en eigenschappen die de toegestane acties op dat veld definiëren.</span><span class="sxs-lookup"><span data-stu-id="943ec-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="943ec-186">`suggesters`gebruikt voor automatisch aanvullen of automatisch aangevulde query's.</span><span class="sxs-lookup"><span data-stu-id="943ec-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="943ec-187">`scoringProfiles`gebruikt voor aangepaste zoekactie score positie.</span><span class="sxs-lookup"><span data-stu-id="943ec-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="943ec-188">Zie [scoreprofiel profielen toevoegen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="943ec-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` toodefine hoe uw documenten/query's worden onderverdeeld in worden geïndexeerd/doorzoekbare tokens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="943ec-190">Zie [analyse in Azure Search](https://aka.ms//azsanalysis) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="943ec-191">`defaultScoringProfile`toooverwrite hello standaard score berekenen gedrag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="943ec-192">`corsOptions`tooallow cross-origin-query's op uw index.</span><span class="sxs-lookup"><span data-stu-id="943ec-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="943ec-193">Hallo-syntaxis voor het Hallo-aanvraaglading structureren is als volgt.</span><span class="sxs-lookup"><span data-stu-id="943ec-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="943ec-194">Een voorbeeld van een aanvraag wordt aangeboden op verder in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="943ec-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="943ec-195">**Indexkenmerken**</span><span class="sxs-lookup"><span data-stu-id="943ec-195">**Index Attributes**</span></span>

<span data-ttu-id="943ec-196">Hallo kunnen volgende kenmerken worden ingesteld bij het maken van een index.</span><span class="sxs-lookup"><span data-stu-id="943ec-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="943ec-197">Zie voor meer informatie over score berekenen en score berekenen voor profielen [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="943ec-198">`name`-Stelt Hallo naam van Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="943ec-199">`type`-Stelt Hallo gegevenstype voor Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="943ec-200">`searchable`-Markeert Hallo veld als volledige tekst kunnen zoeken.</span><span class="sxs-lookup"><span data-stu-id="943ec-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="943ec-201">Dit betekent dat deze ietwat analysis zoals woordafbreking tijdens het indexeren.</span><span class="sxs-lookup"><span data-stu-id="943ec-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="943ec-202">Als u een `searchable` tooa veldwaarde zoals 'mooi day' intern worden gesplitst in afzonderlijke tokens Hallo 'mooi' en 'dag'.</span><span class="sxs-lookup"><span data-stu-id="943ec-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="943ec-203">Hierdoor kan de volledige tekst zoekt naar deze voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="943ec-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="943ec-204">Velden van het type `Edm.String` of `Collection(Edm.String)` zijn `searchable` standaard.</span><span class="sxs-lookup"><span data-stu-id="943ec-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="943ec-205">Mag geen velden van andere typen `searchable`.</span><span class="sxs-lookup"><span data-stu-id="943ec-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="943ec-206">**Opmerking**: `searchable` velden gebruiken extra ruimte in de index omdat Azure Search, een extra tokens versie van de veldwaarde Hallo voor zoekopdrachten in volledige tekst wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="943ec-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="943ec-207">Als u wilt dat toosave ruimte uw index en u hoeft niet een veld toobe opgenomen in zoekopdrachten, stelt u `searchable` te`false`.</span><span class="sxs-lookup"><span data-stu-id="943ec-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="943ec-208">`filterable`-Hiermee kunt Hallo veld toobe waarnaar wordt verwezen in `$filter` query's.</span><span class="sxs-lookup"><span data-stu-id="943ec-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="943ec-209">`filterable`verschilt van `searchable` in de verwerking van tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="943ec-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="943ec-210">Velden van het type `Edm.String` of `Collection(Edm.String)` die zijn `filterable` niet worden bewerkt woordafbreking, zodat vergelijkingen zijn voor exact overeenkomt met alleen.</span><span class="sxs-lookup"><span data-stu-id="943ec-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="943ec-211">Bijvoorbeeld, als u dergelijke veld instellen `f` te 'mooi day' `$filter=f eq 'sunny'` wordt geen overeenkomsten gevonden maar `$filter=f eq 'sunny day'` wordt.</span><span class="sxs-lookup"><span data-stu-id="943ec-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="943ec-212">Alle velden zijn `filterable` standaard.</span><span class="sxs-lookup"><span data-stu-id="943ec-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="943ec-213">`sortable`-Standaard Hallo system sorteert resultaten op score, maar in veel ervaringen gebruikers wilt toosort door velden in het Hallo-documenten.</span><span class="sxs-lookup"><span data-stu-id="943ec-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="943ec-214">Velden van het type `Collection(Edm.String)` kan niet worden `sortable`.</span><span class="sxs-lookup"><span data-stu-id="943ec-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="943ec-215">Alle andere velden zijn `sortable` standaard.</span><span class="sxs-lookup"><span data-stu-id="943ec-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="943ec-216">`facetable`-Doorgaans gebruikt in een weergave van zoekresultaten met treffers per categorie (bijvoorbeeld zoeken naar digitale camera's en Zie treffers op merk, door megapixels, door de prijs, enz.).</span><span class="sxs-lookup"><span data-stu-id="943ec-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="943ec-217">Deze optie kan niet worden gebruikt met velden van het type `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="943ec-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="943ec-218">Alle andere velden zijn `facetable` standaard.</span><span class="sxs-lookup"><span data-stu-id="943ec-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="943ec-219">**Opmerking**: velden van het type `Edm.String` die zijn `filterable`, `sortable`, of `facetable` kan niet groter zijn dan 32 KB lang.</span><span class="sxs-lookup"><span data-stu-id="943ec-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="943ec-220">Dit is omdat deze velden worden behandeld als een enkel zoekterm en Hallo maximale lengte van een term in Azure Search 32KB is.</span><span class="sxs-lookup"><span data-stu-id="943ec-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="943ec-221">Als u toostore meer tekst dan deze in een veld één tekenreeks moet, moet u tooexplicitly ingesteld `filterable`, `sortable`, en `facetable` te`false` in de indexdefinitie van de.</span><span class="sxs-lookup"><span data-stu-id="943ec-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="943ec-222">**Opmerking**: als een veld geen van bovenstaande Hallo heeft kenmerken te ingesteld`true` (`searchable`, `filterable`, `sortable`, of`facetable`) Hallo veld effectief is uitgesloten van Hallo omgekeerde index.</span><span class="sxs-lookup"><span data-stu-id="943ec-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="943ec-223">Deze optie is nuttig voor velden die niet worden gebruikt in query's, maar die nodig zijn in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="943ec-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="943ec-224">Met uitzondering van dergelijke velden van de index Hallo verbetert de prestaties.</span><span class="sxs-lookup"><span data-stu-id="943ec-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="943ec-225">`key`-Markeringen Hallo veld unieke id's voor documenten in Hallo index bevat.</span><span class="sxs-lookup"><span data-stu-id="943ec-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="943ec-226">Moet precies één veld worden gekozen als Hallo `key` veld en moet zijn van het type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="943ec-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="943ec-227">Sleutelvelden kunnen worden gebruikt toolook documenten rechtstreeks via Hallo [Lookup API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="943ec-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="943ec-228">`retrievable`-Instellen of Hallo veld in een zoekresultaat kan worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="943ec-229">Dit is handig wanneer u toouse een veld (bijvoorbeeld marge) als een filter wilt sorteren of score berekenen mechanisme, maar niet dat Hallo veld toobe zichtbaar toohello gebruiker wilt.</span><span class="sxs-lookup"><span data-stu-id="943ec-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="943ec-230">Dit kenmerk moet `true` voor `key` velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="943ec-231">`analyzer`-Naam van Hallo analyzer toouse voor veld Hallo Hallo stelt op zoektijd en indexering tijd.</span><span class="sxs-lookup"><span data-stu-id="943ec-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="943ec-232">Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="943ec-233">Deze optie kan alleen worden gebruikt met `searchable` velden en deze kunnen niet worden ingesteld met een `searchAnalyzer` of `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="943ec-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="943ec-234">Zodra Hallo analyzer is gekozen, kan deze niet meer wijzigen voor het Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="943ec-235">`searchAnalyzer`-Stelt Hallo naam van Hallo analyzer gebruikt op het moment van de zoekactie voor Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="943ec-236">Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="943ec-237">Deze optie kan alleen worden gebruikt met `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="943ec-238">Deze moet worden ingesteld samen met `indexAnalyzer` en deze kan niet worden ingesteld met Hallo `analyzer` optie.</span><span class="sxs-lookup"><span data-stu-id="943ec-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="943ec-239">Deze analyzer kan worden bijgewerkt op een bestaand veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="943ec-240">`indexAnalyzer`-Stelt Hallo naam van Hallo analyzer gebruikt bij indexering voor Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="943ec-241">Zie voor een set waarden toegestaan Hallo [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="943ec-242">Deze optie kan alleen worden gebruikt met `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="943ec-243">Deze moet worden ingesteld samen met `searchAnalyzer` en deze kan niet worden ingesteld met Hallo `analyzer` optie.</span><span class="sxs-lookup"><span data-stu-id="943ec-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="943ec-244">Zodra Hallo analyzer is gekozen, kan deze niet meer wijzigen voor het Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="943ec-245">`suggesters`-Stelt Hallo zoekmodus en velden Hallo bron van Hallo-inhoud voor suggesties zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="943ec-246">Zie [Suggestiefunctie](#Suggesters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="943ec-247">`scoringProfiles`-Definieert aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten hoger in de zoekresultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="943ec-248">Scoreprofiel profielen zijn opgebouwd veldgewichten en functies.</span><span class="sxs-lookup"><span data-stu-id="943ec-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="943ec-249">Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie over Hallo kenmerken in een scoreprofiel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="943ec-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Taalondersteuning**</span><span class="sxs-lookup"><span data-stu-id="943ec-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="943ec-251">De doorzoekbare velden ondergaan analyse die het beste omvat vaak woordafbreking, tekst normalisatie en voorwaarden worden uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="943ec-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="943ec-252">Standaard doorzoekbare velden in Azure Search worden geanalyseerd met Hallo [Apache Lucene standaard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) die tekst opgesplitst in elementen na de['Segmentering Unicode-tekst'](http://unicode.org/reports/tr29/) regels.</span><span class="sxs-lookup"><span data-stu-id="943ec-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="943ec-253">Bovendien converteert Hallo standaard analyzer alle tekens tootheir kleine letters formulier.</span><span class="sxs-lookup"><span data-stu-id="943ec-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="943ec-254">Zowel geïndexeerde documenten en zoektermen doorlopen die Hallo analysis tijdens het indexeren en de verwerking van query's.</span><span class="sxs-lookup"><span data-stu-id="943ec-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="943ec-255">Azure Search biedt ondersteuning voor verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="943ec-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="943ec-256">Elke taal is vereist voor een niet-standaard tekst analyzer die accounts voor kenmerken van een bepaalde taal.</span><span class="sxs-lookup"><span data-stu-id="943ec-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="943ec-257">Azure Search biedt twee typen analyzers:</span><span class="sxs-lookup"><span data-stu-id="943ec-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="943ec-258">35 analyzers Lucene back-up.</span><span class="sxs-lookup"><span data-stu-id="943ec-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="943ec-259">50 analyzers bedrijfseigen Microsoft natuurlijke taal verwerken van de technologie die wordt gebruikt in Office en Bing back-up.</span><span class="sxs-lookup"><span data-stu-id="943ec-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="943ec-260">Sommige ontwikkelaars liever Hallo meer vertrouwde eenvoudige, open source-oplossing van Lucene.</span><span class="sxs-lookup"><span data-stu-id="943ec-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="943ec-261">Lucene analyzers sneller zijn, maar Hallo Microsoft analyzers hebben geavanceerde mogelijkheden, zoals Lemmata, word decompounding (in talen zoals Duits, Deens, Nederlands, Zweeds, Noors, Ests, voltooien, Hongaars, Slowaaks) en entiteit herkenning (URL 's e-mailberichten, datums, getallen).</span><span class="sxs-lookup"><span data-stu-id="943ec-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="943ec-262">Indien mogelijk moet u vergelijkingen van beide Hallo Microsoft en Lucene analyzers toodecide-welke is beter geschikt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="943ec-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="943ec-263">***Hoe ze zich verhouden***</span><span class="sxs-lookup"><span data-stu-id="943ec-263">***How they compare***</span></span>

<span data-ttu-id="943ec-264">Hallo Lucene analyzer voor Engels wordt standaard analyzer Hallo uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="943ec-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="943ec-265">Deze bezittelijke voornaamwoorden (afsluitende van) met woorden verwijdert, is van toepassing als gevolg conform [Porter afleiding algoritme](http://tartarus.org/~martin/PorterStemmer/), en verwijdert u Engels [stopwoorden](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="943ec-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="943ec-266">Ter vergelijking voert Hallo Microsoft analyzer Lemmata in plaats van de gegevens als gevolg.</span><span class="sxs-lookup"><span data-stu-id="943ec-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="943ec-267">Dit betekent dat deze kan omgaan met verbogen en onregelmatige word formulieren veel beter wat resulteert in meer relevante zoekresultaten (controle module 7 van [Azure Search MVA presentatie](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="943ec-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="943ec-268">Indexering met Microsoft analyzers is gemiddeld twee toothree keer langzamer dan de Lucene-equivalenten, afhankelijk van het Hallo-taal.</span><span class="sxs-lookup"><span data-stu-id="943ec-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="943ec-269">Prestaties van de zoekopdracht moet niet aanzienlijk beïnvloed voor de gemiddelde grootte query's.</span><span class="sxs-lookup"><span data-stu-id="943ec-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="943ec-270">***Configuratie***</span><span class="sxs-lookup"><span data-stu-id="943ec-270">***Configuration***</span></span>

<span data-ttu-id="943ec-271">Voor elk veld in de indexdefinitie hello, kunt u Hallo instellen `analyzer` tooan analyzer eigenschapsnaam die welke taal en de leverancier aangeeft.</span><span class="sxs-lookup"><span data-stu-id="943ec-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="943ec-272">Hallo dezelfde analyzer worden toegepast wanneer het indexeren en het zoeken voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="943ec-273">U kunt bijvoorbeeld afzonderlijke velden voor Engels, Frans en Spaans hotel beschrijvingen die bestaan naast elkaar in Hallo hebben dezelfde index.</span><span class="sxs-lookup"><span data-stu-id="943ec-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="943ec-274">Gebruik Hallo ['searchFields' queryparameter](#SearchQueryParameters) toospecify welke toosearch taalspecifieke veld tegen in uw query's.</span><span class="sxs-lookup"><span data-stu-id="943ec-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="943ec-275">U kunt query voorbeelden waarin Hallo bekijken `analyzer` eigenschap in [documenten zoeken](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="943ec-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="943ec-276">***Lijst met Analyzer***</span><span class="sxs-lookup"><span data-stu-id="943ec-276">***Analyzer list***</span></span>

<span data-ttu-id="943ec-277">Hieronder vindt u een lijst van ondersteunde talen samen met de namen van Lucene en Microsoft analyzer Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="943ec-278">Taal</span><span class="sxs-lookup"><span data-stu-id="943ec-278">Language</span></span></th>
        <th><span data-ttu-id="943ec-279">De naam van de Microsoft-analyzer</span><span class="sxs-lookup"><span data-stu-id="943ec-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="943ec-280">Lucene analyzer naam</span><span class="sxs-lookup"><span data-stu-id="943ec-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-281">Arabisch</span><span class="sxs-lookup"><span data-stu-id="943ec-281">Arabic</span></span></td>
        <td><span data-ttu-id="943ec-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-284">Armeens</span><span class="sxs-lookup"><span data-stu-id="943ec-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="943ec-285">Hy.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="943ec-286">Bengaals</span><span class="sxs-lookup"><span data-stu-id="943ec-286">Bangla</span></span></td>
        <td><span data-ttu-id="943ec-287">bn.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="943ec-288">Baskisch</span><span class="sxs-lookup"><span data-stu-id="943ec-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="943ec-289">EU.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="943ec-290">Bulgaars</span><span class="sxs-lookup"><span data-stu-id="943ec-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="943ec-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="943ec-293">Catalaans</span><span class="sxs-lookup"><span data-stu-id="943ec-293">Catalan</span></span></td>
        <td><span data-ttu-id="943ec-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="943ec-296">Vereenvoudigd Chinees</span><span class="sxs-lookup"><span data-stu-id="943ec-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="943ec-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-299">Traditioneel Chinees</span><span class="sxs-lookup"><span data-stu-id="943ec-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="943ec-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="943ec-302">Kroatisch</span><span class="sxs-lookup"><span data-stu-id="943ec-302">Croatian</span></span></td>
        <td><span data-ttu-id="943ec-303">HR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-304">Tsjechisch</span><span class="sxs-lookup"><span data-stu-id="943ec-304">Czech</span></span></td>
        <td><span data-ttu-id="943ec-305">CS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-306">CS.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="943ec-307">Deens</span><span class="sxs-lookup"><span data-stu-id="943ec-307">Danish</span></span></td>
        <td><span data-ttu-id="943ec-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="943ec-310">Nederlands</span><span class="sxs-lookup"><span data-stu-id="943ec-310">Dutch</span></span></td>
        <td><span data-ttu-id="943ec-311">nl.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="943ec-313">Nederlands</span><span class="sxs-lookup"><span data-stu-id="943ec-313">English</span></span></td>        
        <td><span data-ttu-id="943ec-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-316">Estisch</span><span class="sxs-lookup"><span data-stu-id="943ec-316">Estonian</span></span></td>
        <td><span data-ttu-id="943ec-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-318">Fins</span><span class="sxs-lookup"><span data-stu-id="943ec-318">Finnish</span></span></td>
        <td><span data-ttu-id="943ec-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="943ec-321">Frans</span><span class="sxs-lookup"><span data-stu-id="943ec-321">French</span></span></td>
        <td><span data-ttu-id="943ec-322">FR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-323">FR.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-324">Galicisch</span><span class="sxs-lookup"><span data-stu-id="943ec-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="943ec-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="943ec-326">Duits</span><span class="sxs-lookup"><span data-stu-id="943ec-326">German</span></span></td>
        <td><span data-ttu-id="943ec-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-329">Grieks</span><span class="sxs-lookup"><span data-stu-id="943ec-329">Greek</span></span></td>
        <td><span data-ttu-id="943ec-330">El.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-331">El.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="943ec-332">Gujarati</span></span></td>
        <td><span data-ttu-id="943ec-333">Gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-334">Hebreeuws</span><span class="sxs-lookup"><span data-stu-id="943ec-334">Hebrew</span></span></td>
        <td><span data-ttu-id="943ec-335">He.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="943ec-336">Hindi</span></span></td>
        <td><span data-ttu-id="943ec-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-339">Hongaars</span><span class="sxs-lookup"><span data-stu-id="943ec-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="943ec-340">Hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-341">Hu.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-342">IJslands</span><span class="sxs-lookup"><span data-stu-id="943ec-342">Icelandic</span></span></td>
        <td><span data-ttu-id="943ec-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-344">Indonesisch (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="943ec-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="943ec-345">ID.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-346">ID.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-347">Iers</span><span class="sxs-lookup"><span data-stu-id="943ec-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="943ec-348">Ga.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-349">Italiaans</span><span class="sxs-lookup"><span data-stu-id="943ec-349">Italian</span></span></td>
        <td><span data-ttu-id="943ec-350">IT.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-351">IT.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-352">Japans</span><span class="sxs-lookup"><span data-stu-id="943ec-352">Japanese</span></span></td>
        <td><span data-ttu-id="943ec-353">Ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-354">Ja.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="943ec-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="943ec-355">Kannada</span></span></td>
        <td><span data-ttu-id="943ec-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-357">Koreaans</span><span class="sxs-lookup"><span data-stu-id="943ec-357">Korean</span></span></td>
        <td><span data-ttu-id="943ec-358">Ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-359">Ko.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-360">Lets</span><span class="sxs-lookup"><span data-stu-id="943ec-360">Latvian</span></span></td>        
        <td><span data-ttu-id="943ec-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-363">Litouws</span><span class="sxs-lookup"><span data-stu-id="943ec-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="943ec-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-365">Malajalam</span><span class="sxs-lookup"><span data-stu-id="943ec-365">Malayalam</span></span></td>
        <td><span data-ttu-id="943ec-366">ml.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-367">Maleis (Latijns)</span><span class="sxs-lookup"><span data-stu-id="943ec-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="943ec-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="943ec-369">Marathi</span></span></td>
        <td><span data-ttu-id="943ec-370">Mr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-371">Noors</span><span class="sxs-lookup"><span data-stu-id="943ec-371">Norwegian</span></span></td>
        <td><span data-ttu-id="943ec-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-373">No.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="943ec-374">Perzisch</span><span class="sxs-lookup"><span data-stu-id="943ec-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="943ec-375">FA.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="943ec-376">Pools</span><span class="sxs-lookup"><span data-stu-id="943ec-376">Polish</span></span></td>
        <td><span data-ttu-id="943ec-377">PL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-378">PL.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-379">Portugees (Brazilië)</span><span class="sxs-lookup"><span data-stu-id="943ec-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="943ec-380">pt Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-381">pt Br.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-382">Portugees (Portugal)</span><span class="sxs-lookup"><span data-stu-id="943ec-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="943ec-383">pt Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="943ec-384">pt Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="943ec-385">Punjabi</span></span></td>
        <td><span data-ttu-id="943ec-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-387">Roemeens</span><span class="sxs-lookup"><span data-stu-id="943ec-387">Romanian</span></span></td>
        <td><span data-ttu-id="943ec-388">ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-390">Russisch</span><span class="sxs-lookup"><span data-stu-id="943ec-390">Russian</span></span></td>
        <td><span data-ttu-id="943ec-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-393">Servisch (Cyrillisch)</span><span class="sxs-lookup"><span data-stu-id="943ec-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="943ec-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-395">Servisch (Latijns)</span><span class="sxs-lookup"><span data-stu-id="943ec-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="943ec-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-397">Slowaaks</span><span class="sxs-lookup"><span data-stu-id="943ec-397">Slovak</span></span></td>
        <td><span data-ttu-id="943ec-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-399">Sloveens</span><span class="sxs-lookup"><span data-stu-id="943ec-399">Slovenian</span></span></td>
        <td><span data-ttu-id="943ec-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-401">Spaans</span><span class="sxs-lookup"><span data-stu-id="943ec-401">Spanish</span></span></td>
        <td><span data-ttu-id="943ec-402">ES.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-403">ES.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-404">Zweeds</span><span class="sxs-lookup"><span data-stu-id="943ec-404">Swedish</span></span></td>
        <td><span data-ttu-id="943ec-405">SV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-406">SV.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="943ec-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="943ec-407">Tamil</span></span></td>
        <td><span data-ttu-id="943ec-408">TA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="943ec-409">Telugu</span></span></td>
        <td><span data-ttu-id="943ec-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-411">Thais</span><span class="sxs-lookup"><span data-stu-id="943ec-411">Thai</span></span></td>
        <td><span data-ttu-id="943ec-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-414">Turks</span><span class="sxs-lookup"><span data-stu-id="943ec-414">Turkish</span></span></td>
        <td><span data-ttu-id="943ec-415">TR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="943ec-416">TR.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-417">Oekraïens</span><span class="sxs-lookup"><span data-stu-id="943ec-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="943ec-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="943ec-419">Urdu</span></span></td>
        <td><span data-ttu-id="943ec-420">Your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-421">Vietnamees</span><span class="sxs-lookup"><span data-stu-id="943ec-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="943ec-422">VI.Microsoft</span><span class="sxs-lookup"><span data-stu-id="943ec-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="943ec-423">Bovendien biedt Azure Search taal networkdirect analyzer configuraties</span><span class="sxs-lookup"><span data-stu-id="943ec-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="943ec-424">Standaard ASCII Folding</span><span class="sxs-lookup"><span data-stu-id="943ec-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="943ec-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="943ec-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="943ec-426">Unicode-tekst segmentering (standaard Tokenizer)</span><span class="sxs-lookup"><span data-stu-id="943ec-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="943ec-427">Opvouwbaar filter ASCII - converteert Unicode-tekens die geen deel uitmaken toohello set eerst 127 ASCII-tekens in de ASCII-equivalenten.</span><span class="sxs-lookup"><span data-stu-id="943ec-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="943ec-428">Dit is handig voor het verwijderen van diakritische tekens.</span><span class="sxs-lookup"><span data-stu-id="943ec-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="943ec-429">Alle analyzers met namen van aantekeningen voorzien met <i>lucene</i> worden van stroom voorzien door [van Apache Lucene taalanalyse](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="943ec-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="943ec-430">Meer informatie over Hallo ASCII vouwen filter vindt [hier](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="943ec-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="943ec-431">**Suggesties**</span><span class="sxs-lookup"><span data-stu-id="943ec-431">**Suggesters**</span></span>

<span data-ttu-id="943ec-432">Een `suggester` wordt gedefinieerd welke velden in een index zijn gebruikte toosupport automatisch aanvullen in zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="943ec-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="943ec-433">Doorgaans gedeeltelijke zoekreeksen toohello worden verzonden [suggesties API](#Suggestions) terwijl Hallo gebruiker een zoekquery typen is en het Hallo-API een set met voorgestelde zinnen retourneert.</span><span class="sxs-lookup"><span data-stu-id="943ec-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="943ec-434">Een suggestie die u in Hallo index definieert bepaalt welke velden gebruikte toobuild Hallo automatisch aangevulde zoektermen.</span><span class="sxs-lookup"><span data-stu-id="943ec-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="943ec-435">Zie [Suggestiefunctie](#Suggesters) voor configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="943ec-436">**Scoreprofielen**</span><span class="sxs-lookup"><span data-stu-id="943ec-436">**Scoring profiles**</span></span>

<span data-ttu-id="943ec-437">Een `scoringProfile` aangepast scoreprofiel gedrag waarmee u het van invloed zijn op welke objecten in zoekresultaten Hallo hoger weergegeven definieert.</span><span class="sxs-lookup"><span data-stu-id="943ec-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="943ec-438">Scoreprofiel profielen zijn opgebouwd veldgewichten en functies.</span><span class="sxs-lookup"><span data-stu-id="943ec-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="943ec-439">toouse ze, geeft u een profiel met de naam in de queryreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="943ec-440">Een standaard score berekenen profiel werkt achter de schermen-toocompute Hallo een score zoeken voor elk item in een resultatenset.</span><span class="sxs-lookup"><span data-stu-id="943ec-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="943ec-441">U kunt Hallo interne, naamloze scoreprofiel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="943ec-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="943ec-442">U kunt ook instellen `defaultScoringProfile` toouse een aangepast profiel als Hallo standaard, wanneer u een aangepast profiel niet is opgegeven in de queryreeks Hallo aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="943ec-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="943ec-443">Zie [tooa search-index (Azure Search Service REST-API) toevoegen score berekenen profielen](search-api-scoring-profiles-2015-02-28-preview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="943ec-444">**CORS-opties**</span><span class="sxs-lookup"><span data-stu-id="943ec-444">**CORS Options**</span></span>

<span data-ttu-id="943ec-445">Client-side Javascript kan API's standaard niet aanroepen omdat Hallo browser voorkomt u alle cross-origin-aanvragen dat.</span><span class="sxs-lookup"><span data-stu-id="943ec-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="943ec-446">Inschakelen van CORS (Cross-Origin Resource Sharing) met instelling Hallo `corsOptions` kenmerk tooallow cross-origin-query's tooyour index.</span><span class="sxs-lookup"><span data-stu-id="943ec-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="943ec-447">Houd er rekening mee dat alleen query API-ondersteuning CORS uit veiligheidsoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="943ec-448">Hallo volgend opties kan worden ingesteld voor CORS:</span><span class="sxs-lookup"><span data-stu-id="943ec-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="943ec-449">`allowedOrigins`(vereist): dit is een lijst met oorsprongen op waarvoor toegang tooyour index wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="943ec-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="943ec-450">Dit betekent dat een Javascript-code opgehaald uit deze oorsprongen zijn toegestaan tooquery uw index (ervan uitgaande dat het juiste Hallo-API-sleutel biedt).</span><span class="sxs-lookup"><span data-stu-id="943ec-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="943ec-451">Elke oorsprong heeft meestal Hallo vorm `protocol://fully-qualified-domain-name:port` Hoewel Hallo poort vaak wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="943ec-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="943ec-452">Zie [in dit artikel](http://go.microsoft.com/fwlink/?LinkId=330822) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="943ec-453">Als u tooallow toegang tooall oorsprongen wilt, omvatten `*` als één item in Hallo `allowedOrigins` matrix.</span><span class="sxs-lookup"><span data-stu-id="943ec-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="943ec-454">Houd er rekening mee dat **dit wordt niet aanbevolen beveiligingsprocedure voor productie search-services.**</span><span class="sxs-lookup"><span data-stu-id="943ec-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="943ec-455">Dit kan echter nuttig zijn voor ontwikkeling of foutopsporing zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="943ec-456">`maxAgeInSeconds`(optioneel): Browsers gebruiken deze waarde toodetermine Hallo duur (in seconden) toocache CORS voorbereidende antwoorden.</span><span class="sxs-lookup"><span data-stu-id="943ec-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="943ec-457">Dit moet een niet-negatief geheel getal zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-457">This must be a non-negative integer.</span></span> <span data-ttu-id="943ec-458">Hallo groter deze waarde is, Hallo betere prestaties, maar Hallo langer die het duurt voor CORS-beleid wijzigingen tootake effect.</span><span class="sxs-lookup"><span data-stu-id="943ec-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="943ec-459">Als deze niet is ingesteld, wordt een standaardduur van 5 minuten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="943ec-460"><a name="CreateUpdateIndexExample"></a>
**Voorbeeld van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="943ec-461">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-461">**Response**</span></span>

<span data-ttu-id="943ec-462">Aanvraag is gelukt: '201 gemaakt'.</span><span class="sxs-lookup"><span data-stu-id="943ec-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="943ec-463">Standaard bevat antwoordtekst Hallo Hallo JSON voor Hallo indexdefinitie die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="943ec-464">Als hello `Prefer` aanvraagheader is te ingesteld`return=minimal`, Hallo antwoordtekst leeg en Hallo geslaagd status code ' 204 geen inhoud ' in plaats van '201 gemaakt'.</span><span class="sxs-lookup"><span data-stu-id="943ec-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="943ec-465">Dit geldt ongeacht of gebruikte toocreate Hallo index plaatsen of POST was.</span><span class="sxs-lookup"><span data-stu-id="943ec-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="943ec-466">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="943ec-466">**Remarks**</span></span>

<span data-ttu-id="943ec-467">Op dit moment is er beperkte ondersteuning voor index schema-updates.</span><span class="sxs-lookup"><span data-stu-id="943ec-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="943ec-468">Alle schema-updates die opnieuw worden geïndexeerd moeten zoals het wijzigen van veldtypen worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="943ec-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="943ec-469">Hoewel u bestaande velden kunnen niet worden gewijzigd of verwijderd, kan nieuwe velden kunnen tooan bestaande index op elk gewenst moment worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="943ec-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="943ec-470">Wanneer u een nieuw veld toevoegt, hebben alle documenten in index Hallo automatisch een null-waarde voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="943ec-471">Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten toohello index zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="943ec-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="943ec-472">Suggesties</span><span class="sxs-lookup"><span data-stu-id="943ec-472">Suggesters</span></span>
<span data-ttu-id="943ec-473">Hallo suggesties functie in Azure Search is een type-ahead of automatisch aanvullen query-functie, met een lijst van mogelijke zoektermen in het antwoord toopartial tekenreeks invoer in een zoekvak ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="943ec-474">U vast opgevallen Querysuggesties bij gebruik van zoekmachines commerciële web: '.NET' te typen Bing genereert een overzicht van voorwaarden voor '.NET 4.5 uitvoeren ', '.NET Framework 3.5", enzovoort.</span><span class="sxs-lookup"><span data-stu-id="943ec-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="943ec-475">Wanneer u Hallo Search service REST-API, vereist suggesties implementeren in een aangepaste Azure Search-toepassing hello volgende:</span><span class="sxs-lookup"><span data-stu-id="943ec-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="943ec-476">Suggesties inschakelen door het toevoegen van een **suggestie** bouw in uw index, geeft de naam hello, zoekmodus en een lijst met velden waarvoor automatisch aangevulde wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="943ec-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="943ec-477">Bijvoorbeeld, als u 'stad' als een bronveld, te typen gedeeltelijke zoektekenreeks 'Sea' leidt ertoe dat "Seattle" opgeeft, 'Strand' en 'Seatac' (alle drie zijn de namen van de werkelijke stad) aangeboden tot als query suggesties toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="943ec-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="943ec-478">Suggesties aanroepen door de aanroepende Hallo [suggesties API](#Suggestions) in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="943ec-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="943ec-479">Gedeeltelijke zoekreeksen worden doorgaans toohello service verzonden tijdens het Hallo-gebruiker is een zoekopdracht typen en deze API retourneert een set met voorgestelde zinnen.</span><span class="sxs-lookup"><span data-stu-id="943ec-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="943ec-480">Dit artikel wordt uitgelegd hoe tooconfigure een **suggestie**.</span><span class="sxs-lookup"><span data-stu-id="943ec-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="943ec-481">Bekijk ook Hallo [suggesties API](#Suggestions) voor meer informatie over hoe een suggestie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="943ec-482">**Gebruik**</span><span class="sxs-lookup"><span data-stu-id="943ec-482">**Usage**</span></span>

<span data-ttu-id="943ec-483">`Suggesters`in Hallo index worden gemaakt en werken het beste als gebruikt toosuggest specifieke documenten in plaats van losse voorwaarden of zinnen.</span><span class="sxs-lookup"><span data-stu-id="943ec-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="943ec-484">Hallo best candidate velden zijn titels, namen en andere relatief korte zinnen die een item kunnen identificeren.</span><span class="sxs-lookup"><span data-stu-id="943ec-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="943ec-485">Minder effectief zijn herhalende velden, zoals de categorieën en tags, of zeer lange velden zoals beschrijvingen of opmerkingen velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="943ec-486">Als onderdeel van de indexdefinitie hello, kunt u een één suggestie toohello toevoegen `suggesters` verzameling.</span><span class="sxs-lookup"><span data-stu-id="943ec-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="943ec-487">Eigenschappen die, een suggestie bepalen zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="943ec-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="943ec-488">`name`: Hallo-naam van Hallo suggestie.</span><span class="sxs-lookup"><span data-stu-id="943ec-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="943ec-489">U Hallo-naam van Hallo suggestie gebruiken bij het aanroepen van Hallo `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="943ec-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="943ec-490">`searchMode`: Hallo toosearch gebruikte strategie voor candidate zinnen.</span><span class="sxs-lookup"><span data-stu-id="943ec-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="943ec-491">Hallo modus worden alleen ondersteund op dit moment is `analyzingInfixMatching`, flexibele overeenkomende woordgroepen aan Hallo begin of in het midden van zinnen Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="943ec-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="943ec-492">`sourceFields`: Een lijst met een of meer velden Hallo bron van Hallo-inhoud voor suggesties zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="943ec-493">Alleen velden van het type `Edm.String` en `Collection(Edm.String)` mogelijk bronnen voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="943ec-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="943ec-494">Alleen de velden die een aangepaste taalanalyse ingesteld niet kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="943ec-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="943ec-495">**Suggestie voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="943ec-495">**Suggester Example**</span></span>

<span data-ttu-id="943ec-496">Een suggestie maakt deel uit van Hallo index.</span><span class="sxs-lookup"><span data-stu-id="943ec-496">A suggester is part of hello index.</span></span> <span data-ttu-id="943ec-497">Er kan slechts één suggestie bestaan in Hallo `suggesters` verzameling in de huidige versie Hallo naast Hallo verzameling velden en `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="943ec-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="943ec-498">Als u Hallo openbare preview-versie van Azure Search gebruikt `suggesters` wordt vervangen door een oudere Boole-eigenschap (`"suggestions": false`) die alleen voorvoegsel suggesties voor korte tekenreeksen (3-25 tekens) wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="943ec-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="943ec-499">De vervanging ervan `suggesters`, ondersteunt infix overeenkomende waarmee wordt gezocht naar overeenkomende voorwaarden aan Hallo begin of in het midden van de Hallo van veldinhoud, met betere tolerantie voor fouten in zoekreeksen.</span><span class="sxs-lookup"><span data-stu-id="943ec-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="943ec-500">Vanaf Hallo algemeen beschikbaar release, is dit nu Hallo alleen implementatie van Hallo suggesties API.</span><span class="sxs-lookup"><span data-stu-id="943ec-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="943ec-501">Hallo oudere `suggestions` eigenschap die is geïntroduceerd in `api-version=2014-07-31-Preview` toowork blijft in deze versie, maar is niet operationeel in Hallo `2015-02-28` of latere versies van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="943ec-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="943ec-502">Index bijwerken</span><span class="sxs-lookup"><span data-stu-id="943ec-502">Update Index</span></span>
<span data-ttu-id="943ec-503">U kunt een bestaande index in Azure Search met behulp van een HTTP PUT-aanvraag bijwerken.</span><span class="sxs-lookup"><span data-stu-id="943ec-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="943ec-504">Updates kunnen het toevoegen van nieuwe velden toohello bestaand schema, CORS-opties wijzigen en wijzigen, scoreprofiel profielen bevatten.</span><span class="sxs-lookup"><span data-stu-id="943ec-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="943ec-505">Zie [toevoegen score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="943ec-506">U opgeven Hallo naam van Hallo index tooupdate op Hallo aanvraag-URI:</span><span class="sxs-lookup"><span data-stu-id="943ec-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="943ec-507">**Belangrijk:** ondersteuning voor index schema-updates beperkt toooperations die Hallo search-index opnieuw opbouwen niet nodig is.</span><span class="sxs-lookup"><span data-stu-id="943ec-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="943ec-508">Alle schema-updates die opnieuw worden geïndexeerd moeten, zoals het wijzigen van veldtypen, worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="943ec-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="943ec-509">Nieuwe velden kunnen op elk gewenst moment worden toegevoegd, hoewel bestaande velden kunnen niet worden gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="943ec-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="943ec-510">Hallo geldt te`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="943ec-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="943ec-511">Nieuwe velden kunnen worden toegevoegd tooa suggestie op Hallo Hallo tijdvelden worden toegevoegd, maar velden kunnen niet worden verwijderd uit `suggesters` en bestaande velden kunnen niet te worden toegevoegd`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="943ec-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="943ec-512">Wanneer u een nieuw veld tooan index toevoegt, hebben alle documenten in index Hallo automatisch een null-waarde voor dat veld.</span><span class="sxs-lookup"><span data-stu-id="943ec-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="943ec-513">Er zijn geen extra opslagruimte worden gebruikt totdat nieuwe documenten toohello index zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="943ec-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="943ec-514">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-514">**Request**</span></span>

<span data-ttu-id="943ec-515">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="943ec-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="943ec-516">Hallo **Index bijwerken** aanvraag is opgesteld met HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="943ec-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="943ec-517">Met opslag is de indexnaam Hallo deel van Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="943ec-518">Als het Hallo-index niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="943ec-519">Als al Hallo index bestaat, is het bijgewerkte toohello nieuwe definitie.</span><span class="sxs-lookup"><span data-stu-id="943ec-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="943ec-520">Hallo indexnaam moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="943ec-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="943ec-521">Hallo rest van de naam van de Hallo kan na het starten van de indexnaam Hallo met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang Hallo streepjes niet opeenvolgende zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="943ec-522">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-523">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-524">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-525">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-525">**Request Headers**</span></span>

<span data-ttu-id="943ec-526">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-527">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-527">`Content-Type`: Required.</span></span> <span data-ttu-id="943ec-528">Stel deze optie te`application/json`</span><span class="sxs-lookup"><span data-stu-id="943ec-528">Set this too`application/json`</span></span>
* <span data-ttu-id="943ec-529">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-529">`api-key`: Required.</span></span> <span data-ttu-id="943ec-530">Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-531">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-532">Hallo **Index bijwerken** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-533">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-534">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-535">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-536">**Syntaxis van de aanvraag hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-536">**Request Body Syntax**</span></span>

<span data-ttu-id="943ec-537">Bij het bijwerken van een bestaande index Hallo hoofdtekst vergezeld gaan van de oorspronkelijke schemadefinitie Hallo plus Hallo nieuwe velden die u wilt toevoegen, evenals Hallo gewijzigd scoreprofiel profielen, suggestiefunctie en CORS-opties, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="943ec-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="943ec-538">Als u scoreprofiel Hallo-profielen en CORS-opties niet wijzigt, moet u opnemen Hallo originele wanneer Hallo index is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="943ec-539">Hallo best patroon toouse voor updates is over het algemeen tooretrieve Hallo indexdefinitie met een GET, wijzigen en vervolgens bijwerken met PUT.</span><span class="sxs-lookup"><span data-stu-id="943ec-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="943ec-540">Hallo schemasyntaxis gebruikt een index is hier gereproduceerd toocreate voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="943ec-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="943ec-541">Zie [Create Index](#CreateIndex) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="943ec-542">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-542">**Response**</span></span>

<span data-ttu-id="943ec-543">Aanvraag is gelukt: ' 204 geen inhoud '.</span><span class="sxs-lookup"><span data-stu-id="943ec-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="943ec-544">Standaard wordt Hallo antwoordtekst niet leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-544">By default hello response body will be empty.</span></span> <span data-ttu-id="943ec-545">Echter, als hello `Prefer` aanvraagheader is te ingesteld`return=representation`, Hallo antwoordtekst bevat Hallo JSON voor Hallo indexdefinitie die is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="943ec-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="943ec-546">In dit geval statuscode van Hallo geslaagd zijn ' 200 OK '.</span><span class="sxs-lookup"><span data-stu-id="943ec-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="943ec-547">**Definitie van de index met aangepaste analyzers bijwerken**</span><span class="sxs-lookup"><span data-stu-id="943ec-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="943ec-548">Als er een analyzer, een tokenizer, een token filter of een char-filter is gedefinieerd, kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="943ec-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="943ec-549">Nieuwe te kunnen alleen worden toegevoegd tooan bestaande index als hello `allowIndexDowntime` tootrue-vlag is ingesteld in Hallo index updateaanvraag:</span><span class="sxs-lookup"><span data-stu-id="943ec-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="943ec-550">Opmerking dat deze bewerking uw index offline wordt geplaatst voor ten minste een paar seconden, waardoor uw indexeren en query-toofail aanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="943ec-551">Beschikbaarheid en wegschrijven van Hallo-index kan worden gehinderd minuten nadat het Hallo-index wordt bijgewerkt of langer voor zeer grote indexen.</span><span class="sxs-lookup"><span data-stu-id="943ec-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="943ec-552">Lijst met indexen</span><span class="sxs-lookup"><span data-stu-id="943ec-552">List Indexes</span></span>
<span data-ttu-id="943ec-553">Hallo **lijst indexen** bewerking retourneert een lijst met Hallo indexen momenteel in uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="943ec-554">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-554">**Request**</span></span>

<span data-ttu-id="943ec-555">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="943ec-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="943ec-556">Hallo **lijst indexen** aanvraag kan worden opgesteld met Hallo GET-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="943ec-557">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-558">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-559">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-560">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-560">**Request Headers**</span></span>

<span data-ttu-id="943ec-561">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-562">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-562">`api-key`: Required.</span></span> <span data-ttu-id="943ec-563">Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-564">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-565">Hallo **lijst indexen** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).</span><span class="sxs-lookup"><span data-stu-id="943ec-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-566">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-567">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-568">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-569">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-569">**Request Body**</span></span>

<span data-ttu-id="943ec-570">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-570">None.</span></span>

<span data-ttu-id="943ec-571">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-571">**Response**</span></span>

<span data-ttu-id="943ec-572">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="943ec-573">Hier volgt een voorbeeld-antwoordtekst:</span><span class="sxs-lookup"><span data-stu-id="943ec-573">Here is an example response body:</span></span>

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

<span data-ttu-id="943ec-574">Houd er rekening mee dat u kunt filteren, antwoord Hallo omlaag toojust Hallo eigenschappen die u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="943ec-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="943ec-575">Bijvoorbeeld: als u alleen een lijst met indexnamen wilt, Hallo OData gebruiken `$select` query-optie:</span><span class="sxs-lookup"><span data-stu-id="943ec-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="943ec-576">In dit geval zou Hallo reactie van Hallo bovenstaande voorbeeld als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="943ec-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="943ec-577">Dit is een nuttig toosave bandbreedte als er een groot aantal indexen in uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="943ec-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="943ec-578">Index ophalen</span><span class="sxs-lookup"><span data-stu-id="943ec-578">Get Index</span></span>
<span data-ttu-id="943ec-579">Hallo **Index ophalen** bewerking Hallo indexdefinitie opgehaald uit Azure Search.</span><span class="sxs-lookup"><span data-stu-id="943ec-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="943ec-580">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-580">**Request**</span></span>

<span data-ttu-id="943ec-581">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-582">Hallo **Index ophalen** aanvraag kan worden opgesteld met Hallo GET-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="943ec-583">Hallo [naam van de index] in Hallo aanvraag-URI geeft aan welke tooreturn index uit Hallo indexverzameling.</span><span class="sxs-lookup"><span data-stu-id="943ec-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="943ec-584">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-585">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-586">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-587">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-587">**Request Headers**</span></span>

<span data-ttu-id="943ec-588">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-589">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-590">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-591">Hallo **Index ophalen** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).</span><span class="sxs-lookup"><span data-stu-id="943ec-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-592">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-593">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-594">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-595">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-595">**Request Body**</span></span>

<span data-ttu-id="943ec-596">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-596">None.</span></span>

<span data-ttu-id="943ec-597">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-597">**Response**</span></span>

<span data-ttu-id="943ec-598">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="943ec-599">Zie Hallo voorbeeld JSON in [maken en bijwerken van een Index](#CreateUpdateIndexExample) voor een voorbeeld van Hallo antwoord nettolading.</span><span class="sxs-lookup"><span data-stu-id="943ec-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="943ec-600">Index verwijderen</span><span class="sxs-lookup"><span data-stu-id="943ec-600">Delete Index</span></span>
<span data-ttu-id="943ec-601">Hallo **Index verwijderen** bewerking verwijdert u een index en de bijbehorende documentatie van uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="943ec-602">U krijgt de indexnaam Hallo van Hallo servicedashboard in hello Azure-portal of van Hallo API.</span><span class="sxs-lookup"><span data-stu-id="943ec-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="943ec-603">Zie [lijst indexen](#ListIndexes) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="943ec-604">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-604">**Request**</span></span>

<span data-ttu-id="943ec-605">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-606">Hallo **Index verwijderen** aanvraag kan worden opgesteld met Hallo DELETE-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="943ec-607">Hallo [naam van de index] in Hallo aanvraag-URI geeft aan welke toodelete index uit Hallo indexverzameling.</span><span class="sxs-lookup"><span data-stu-id="943ec-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="943ec-608">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-609">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-610">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-611">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-611">**Request Headers**</span></span>

<span data-ttu-id="943ec-612">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-613">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-613">`api-key`: Required.</span></span> <span data-ttu-id="943ec-614">Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-615">Het is een tekenreekswaarde, unieke tooyour service-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="943ec-616">Hallo **Index verwijderen** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-617">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-618">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-619">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-620">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-620">**Request Body**</span></span>

<span data-ttu-id="943ec-621">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-621">None.</span></span>

<span data-ttu-id="943ec-622">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-622">**Response**</span></span>

<span data-ttu-id="943ec-623">Statuscode: 204 geen inhoud wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="943ec-624">Indexstatistieken opvragen</span><span class="sxs-lookup"><span data-stu-id="943ec-624">Get Index Statistics</span></span>
<span data-ttu-id="943ec-625">Hallo **statistieken voor Index ophalen** bewerking retourneert van Azure Search een aantal documenten voor de huidige index Hallo plus opslaggebruik.</span><span class="sxs-lookup"><span data-stu-id="943ec-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="943ec-626">Statistieken over document aantal en de opslaggrootte worden elke paar minuten, niet in realtime verzameld.</span><span class="sxs-lookup"><span data-stu-id="943ec-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="943ec-627">Hallo-statistieken die zijn geretourneerd door deze API kan daarom niet overeen met wijzigingen die zijn veroorzaakt door een recente indexbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="943ec-628">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-628">**Request**</span></span>

<span data-ttu-id="943ec-629">HTTPS is vereist voor alle services aanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="943ec-630">Hallo **statistieken voor Index ophalen** aanvraag kan worden opgesteld met Hallo GET-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="943ec-631">Hallo [naam van de index] in Hallo aanvraag-URI vertelt Hallo service tooreturn indexstatistieken voor de opgegeven index Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="943ec-632">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-633">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-634">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-635">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-635">**Request Headers**</span></span>

<span data-ttu-id="943ec-636">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-637">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-638">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-639">Hallo **ophalen indexstatistieken** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).</span><span class="sxs-lookup"><span data-stu-id="943ec-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-640">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-641">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-642">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-643">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-643">**Request Body**</span></span>

<span data-ttu-id="943ec-644">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-644">None.</span></span>

<span data-ttu-id="943ec-645">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-645">**Response**</span></span>

<span data-ttu-id="943ec-646">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="943ec-647">Hallo-antwoordtekst heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="943ec-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="943ec-648">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="943ec-648">Test Analyzer</span></span>
<span data-ttu-id="943ec-649">Hallo **analyseren API** ziet u hoe een analyzer tekst opgesplitst in tokens.</span><span class="sxs-lookup"><span data-stu-id="943ec-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="943ec-650">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-650">**Request**</span></span>

<span data-ttu-id="943ec-651">HTTPS is vereist voor alle services aanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="943ec-652">Hallo **analyseren API** aanvraag kan worden opgesteld met Hallo POST-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="943ec-653">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-654">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-655">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-656">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-656">**Request Headers**</span></span>

<span data-ttu-id="943ec-657">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-658">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-659">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-660">Hallo **analyseren API** aanvraag moet bevatten een `api-key` set tooan beheersleutel (als tegengestelde tooa query-sleutel).</span><span class="sxs-lookup"><span data-stu-id="943ec-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-661">U moet ook de indexnaam Hallo en Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-662">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-663">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-664">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="943ec-665">of</span><span class="sxs-lookup"><span data-stu-id="943ec-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="943ec-666">Hallo `analyzer_name`, `tokenizer_name`, `token_filter_name` en `char_filter_name` toobe geldige namen van de vooraf gedefinieerde of aangepaste analyzers, tokenizers, token filters en char filters voor Hallo index nodig.</span><span class="sxs-lookup"><span data-stu-id="943ec-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="943ec-667">Zie informatie over het proces van lexicale analyse Hallo toolearn [analyse in Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="943ec-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="943ec-668">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-668">**Response**</span></span>

<span data-ttu-id="943ec-669">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="943ec-670">Hallo-antwoordtekst heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="943ec-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="943ec-671">**API-voorbeeld analyseren**</span><span class="sxs-lookup"><span data-stu-id="943ec-671">**Analyze API example**</span></span>

<span data-ttu-id="943ec-672">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="943ec-673">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="943ec-674">Document bewerkingen</span><span class="sxs-lookup"><span data-stu-id="943ec-674">Document Operations</span></span>
<span data-ttu-id="943ec-675">In Azure Search is een index wordt opgeslagen in de cloud Hallo en ingevuld met JSON-documenten toohello service te uploaden.</span><span class="sxs-lookup"><span data-stu-id="943ec-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="943ec-676">Alle Hallo-documenten die u uploadt omvatten Hallo corpus van uw zoekgegevens.</span><span class="sxs-lookup"><span data-stu-id="943ec-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="943ec-677">Documenten bevatten velden, zijn sommige van deze in de zoektermen tokenized als ze worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="943ec-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="943ec-678">Hallo `/docs` URL-segment in hello Azure Search API vertegenwoordigt Hallo-verzameling van documenten in een index.</span><span class="sxs-lookup"><span data-stu-id="943ec-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="943ec-679">Alle bewerkingen die worden uitgevoerd op de verzameling Hallo zoals uploaden, samenvoegen, verwijderen of documenten opvragen plaatsvinden in Hallo context van een enkele index geval Hallo-URL's voor deze bewerkingen wordt altijd gestart met `/indexes/[index name]/docs` voor een naam voor de gegeven index.</span><span class="sxs-lookup"><span data-stu-id="943ec-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="943ec-680">Uw toepassingscode moet ofwel genereren voor JSON-documenten tooupload tooAzure zoeken of kunt u een [indexeerfunctie](https://msdn.microsoft.com/library/dn946891.aspx) tooload documenten als gegevensbron hello Azure SQL Database of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="943ec-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="943ec-681">Indexen worden gewoonlijk ingevuld uit een enkele gegevensset die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="943ec-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="943ec-682">U moet plannen op beschikt over een document voor elk item dat u wilt dat toosearch.</span><span class="sxs-lookup"><span data-stu-id="943ec-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="943ec-683">Een toepassing van de verhuur film wellicht een document per film, een toepassing via wellicht een document per SKU, een toepassing online cursusprogramma wellicht een document per loop, een bedrijf wellicht een document voor elk academic papier in hun opslagplaats, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="943ec-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="943ec-684">Documenten bestaan uit een of meer velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="943ec-685">Velden kunnen bevatten tekst die wordt door Azure Search in zoektermen tokenized, evenals niet getokeniseerd of niet-tekstwaarden plaatsen die kunnen worden gebruikt in filters of scoreprofiel profielen.</span><span class="sxs-lookup"><span data-stu-id="943ec-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="943ec-686">Hallo worden namen, gegevenstypen en zoekfuncties ondersteund voor elk veld bepaald door Hallo Indexeer schema.</span><span class="sxs-lookup"><span data-stu-id="943ec-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="943ec-687">Een van de velden Hallo in elke indexschema dat moet worden aangemerkt als een ID en elk document moet een waarde voor Hallo-ID-veld dat een unieke identificatie van dat document in Hallo index hebben.</span><span class="sxs-lookup"><span data-stu-id="943ec-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="943ec-688">Alle andere documentvelden zijn optioneel en tooa null-waarde wordt teruggezet of niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="943ec-689">Houd er rekening mee dat null-waarden geen ruimte vrijmaken in Hallo search-index hebben.</span><span class="sxs-lookup"><span data-stu-id="943ec-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="943ec-690">Als u documenten uploaden, moet hebt u al Hallo index gemaakt op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="943ec-691">Zie [Create Index](#CreateIndex) voor meer informatie over deze eerste stap.</span><span class="sxs-lookup"><span data-stu-id="943ec-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="943ec-692">Toevoegen, bijwerken of verwijderen van documenten</span><span class="sxs-lookup"><span data-stu-id="943ec-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="943ec-693">U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="943ec-694">Batchverwerking van documenten (too1000 documenten per batch) of 16 MB per batch wordt aanbevolen voor grote aantallen van updates.</span><span class="sxs-lookup"><span data-stu-id="943ec-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="943ec-695">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-695">**Request**</span></span>

<span data-ttu-id="943ec-696">HTTPS is vereist voor alle aanvragen van de service.</span><span class="sxs-lookup"><span data-stu-id="943ec-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="943ec-697">U kunt uploaden, samenvoegen, merge of uploaden of delete documenten vanuit een opgegeven index met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="943ec-698">Hallo-aanvraag URI bevat [naam van de index] opgeven welke index toopost documenten.</span><span class="sxs-lookup"><span data-stu-id="943ec-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="943ec-699">U kunt alleen documenten tooone index boeken tegelijk.</span><span class="sxs-lookup"><span data-stu-id="943ec-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="943ec-700">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-701">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-702">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-703">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-703">**Request Headers**</span></span>

<span data-ttu-id="943ec-704">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-705">`Content-Type`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-705">`Content-Type`: Required.</span></span> <span data-ttu-id="943ec-706">Stel deze optie te`application/json`</span><span class="sxs-lookup"><span data-stu-id="943ec-706">Set this too`application/json`</span></span>
* <span data-ttu-id="943ec-707">`api-key`: Vereist.</span><span class="sxs-lookup"><span data-stu-id="943ec-707">`api-key`: Required.</span></span> <span data-ttu-id="943ec-708">Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-709">Het is een tekenreekswaarde, een unieke tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="943ec-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="943ec-710">Hallo **documenten toevoegen** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="943ec-711">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-712">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-713">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-714">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-714">**Request Body**</span></span>

<span data-ttu-id="943ec-715">Hallo-hoofdtekst van Hallo-aanvraag bevat een of meer documenten toobe geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="943ec-716">Documenten worden aangeduid met een unieke sleutel.</span><span class="sxs-lookup"><span data-stu-id="943ec-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="943ec-717">Elk document dat is gekoppeld aan een actie: uploaden, samenvoegen, mergeOrUpload of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="943ec-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="943ec-718">Het uploaden van aanvragen mag Hallo documentgegevens bevatten als een set van sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="943ec-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="943ec-719">Document sleutels mogen alleen letters, cijfers, streepjes ('-'), onderstrepingstekens ('_') en gelijk tekens ('=').</span><span class="sxs-lookup"><span data-stu-id="943ec-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="943ec-720">Zie voor meer informatie [naamgevingsregels](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="943ec-721">**Documentacties**</span><span class="sxs-lookup"><span data-stu-id="943ec-721">**Document Actions**</span></span>

* <span data-ttu-id="943ec-722">`upload`: Er is een upload-actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="943ec-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="943ec-723">Houd er rekening mee dat alle velden in geval van Hallo-update worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="943ec-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="943ec-724">`merge`: Samenvoegen updates een bestaand document met het Hallo opgegeven velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="943ec-725">Als Hallo document niet bestaat, mislukt de Hallo samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="943ec-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="943ec-726">Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="943ec-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="943ec-727">ook velden van het type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="943ec-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="943ec-728">Bijvoorbeeld, als hello document bevat een veld 'labels' met de waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor 'tags' hello uiteindelijke waarde van veld Hallo 'tags' worden `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="943ec-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="943ec-729">Het **niet** worden `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="943ec-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="943ec-730">`mergeOrUpload`: gedraagt zich als `merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat.</span><span class="sxs-lookup"><span data-stu-id="943ec-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="943ec-731">Als Hallo document niet bestaat nog, gedraagt zich als `upload` met een nieuw document.</span><span class="sxs-lookup"><span data-stu-id="943ec-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="943ec-732">`delete`: Het opgegeven document Hallo verwijdert verwijderen uit Hallo index.</span><span class="sxs-lookup"><span data-stu-id="943ec-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="943ec-733">Houd er rekening mee dat alle velden u opgeeft in een `delete` bewerking dan Hallo sleutelveld worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="943ec-734">Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `merge` in plaats daarvan en stelt Hallo veld expliciet in te`null`.</span><span class="sxs-lookup"><span data-stu-id="943ec-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="943ec-735">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-735">**Response**</span></span>

<span data-ttu-id="943ec-736">Statuscode 200 wordt (OK) geretourneerd voor een geslaagd antwoord, wat betekent dat alle items zijn geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="943ec-737">Dit wordt aangegeven door Hallo `status` eigenschap wordt ingesteld tootrue voor alle items, evenals Hallo `statusCode` eigenschap wordt ingesteld tooeither 201 (voor recent geüploade documenten) of 200 (voor samengevoegde of verwijderde documenten):</span><span class="sxs-lookup"><span data-stu-id="943ec-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="943ec-738">Statuscode 207 (meerdere Status) wordt geretourneerd wanneer ten minste één item is niet geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="943ec-739">Items die niet zijn geïndexeerd hebben Hallo `status` veld toofalse ingesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="943ec-740">Hallo `errorMessage` en `statusCode` eigenschappen Hallo reden voor fout indexeren hello wordt aangeven:</span><span class="sxs-lookup"><span data-stu-id="943ec-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="943ec-741">Hallo volgende tabel wordt uitgelegd Hallo verschillende per document statuscodes die kunnen worden geretourneerd in antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="943ec-742">Houd er rekening mee dat sommige duiden op problemen met het Hallo-aanvraag zelf, terwijl anderen tijdelijke fouten geven.</span><span class="sxs-lookup"><span data-stu-id="943ec-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="943ec-743">Hallo laatstgenoemde die probeert u het opnieuw na een vertraging.</span><span class="sxs-lookup"><span data-stu-id="943ec-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="943ec-744">Statuscode</span><span class="sxs-lookup"><span data-stu-id="943ec-744">Status code</span></span></th>
        <th><span data-ttu-id="943ec-745">Betekenis</span><span class="sxs-lookup"><span data-stu-id="943ec-745">Meaning</span></span></th>
        <th><span data-ttu-id="943ec-746">Herstelbare</span><span class="sxs-lookup"><span data-stu-id="943ec-746">Retryable</span></span></th>
        <th><span data-ttu-id="943ec-747">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="943ec-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-748">200</span><span class="sxs-lookup"><span data-stu-id="943ec-748">200</span></span></td>
        <td><span data-ttu-id="943ec-749">Document is gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="943ec-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="943ec-750">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="943ec-750">n/a</span></span></td>
        <td><span data-ttu-id="943ec-751">Verwijderbewerkingen zijn <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="943ec-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="943ec-752">Dat wil zeggen, zelfs als de documentsleutel van een niet in de index hello bestaat, leidt probeert een delete-bewerking met die sleutel tot een 200-statuscode.</span><span class="sxs-lookup"><span data-stu-id="943ec-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-753">201</span><span class="sxs-lookup"><span data-stu-id="943ec-753">201</span></span></td>
        <td><span data-ttu-id="943ec-754">Document is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="943ec-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="943ec-755">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="943ec-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-756">400</span><span class="sxs-lookup"><span data-stu-id="943ec-756">400</span></span></td>
        <td><span data-ttu-id="943ec-757">Er is een fout opgetreden in Hallo-document dat waardoor deze niet kan worden geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="943ec-758">Nee</span><span class="sxs-lookup"><span data-stu-id="943ec-758">No</span></span></td>
        <td><span data-ttu-id="943ec-759">Hallo foutbericht weergegeven in het antwoord Hallo wordt aangegeven wat is er iets mis met Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="943ec-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-760">404</span><span class="sxs-lookup"><span data-stu-id="943ec-760">404</span></span></td>
        <td><span data-ttu-id="943ec-761">Hallo-document kan niet worden samengevoegd omdat Hallo opgegeven sleutel niet in het Hallo-index bestaat.</span><span class="sxs-lookup"><span data-stu-id="943ec-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="943ec-762">Nee</span><span class="sxs-lookup"><span data-stu-id="943ec-762">No</span></span></td>
        <td><span data-ttu-id="943ec-763">Deze fout treedt niet op bij uploads omdat ze nieuwe documenten maken en dit niet voor verwijderingen gebeurt omdat ze <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="943ec-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-764">409</span><span class="sxs-lookup"><span data-stu-id="943ec-764">409</span></span></td>
        <td><span data-ttu-id="943ec-765">Een versieconflict gevonden tijdens een poging de tooindex een document.</span><span class="sxs-lookup"><span data-stu-id="943ec-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="943ec-766">Ja</span><span class="sxs-lookup"><span data-stu-id="943ec-766">Yes</span></span></td>
        <td><span data-ttu-id="943ec-767">Dit kan gebeuren wanneer u probeert tooindex Hallo dezelfde meer dan één keer gelijktijdig-document.</span><span class="sxs-lookup"><span data-stu-id="943ec-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-768">422</span><span class="sxs-lookup"><span data-stu-id="943ec-768">422</span></span></td>
        <td><span data-ttu-id="943ec-769">Hallo index is tijdelijk niet beschikbaar omdat deze is bijgewerkt met de Hallo 'allowIndexDowntime' vlag set too'true'.</span><span class="sxs-lookup"><span data-stu-id="943ec-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="943ec-770">Ja</span><span class="sxs-lookup"><span data-stu-id="943ec-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="943ec-771">503</span><span class="sxs-lookup"><span data-stu-id="943ec-771">503</span></span></td>
        <td><span data-ttu-id="943ec-772">Uw search-service is tijdelijk niet beschikbaar is, mogelijk vanwege tooheavy laden.</span><span class="sxs-lookup"><span data-stu-id="943ec-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="943ec-773">Ja</span><span class="sxs-lookup"><span data-stu-id="943ec-773">Yes</span></span></td>
        <td><span data-ttu-id="943ec-774">Uw code moet worden gewacht voordat opnieuw uit te voeren in dit geval of u het risico verlenging van de Hallo-service niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="943ec-775">**Opmerking**: als uw clientcode wordt vaak een 207 antwoord tegenkomt, een mogelijke reden is dat Hallo system belast wordt.</span><span class="sxs-lookup"><span data-stu-id="943ec-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="943ec-776">U kunt dit controleren door te controleren Hallo `statusCode` eigenschap voor 503.</span><span class="sxs-lookup"><span data-stu-id="943ec-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="943ec-777">Als dit Hallo geval is, wordt aangeraden ***beperking indexering aanvragen***.</span><span class="sxs-lookup"><span data-stu-id="943ec-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="943ec-778">Anders als indexering verkeer niet subside, Hallo system kan worden gestart voor het weigeren van alle aanvragen met 503-fouten.</span><span class="sxs-lookup"><span data-stu-id="943ec-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="943ec-779">Statuscode 429 geeft aan dat u het quotum van Hallo aantal documenten per index hebt overschreden.</span><span class="sxs-lookup"><span data-stu-id="943ec-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="943ec-780">Een nieuwe index maken of een upgrade uit voor hogere Capaciteitslimieten.</span><span class="sxs-lookup"><span data-stu-id="943ec-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="943ec-781">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="943ec-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="943ec-782">Documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="943ec-782">Search Documents</span></span>
<span data-ttu-id="943ec-783">Een **Search** bewerking als een GET of POST-aanvraag wordt uitgegeven en parameters waarmee Hallo criteria voor het selecteren van de overeenkomende documenten bevat.</span><span class="sxs-lookup"><span data-stu-id="943ec-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="943ec-784">**Wanneer toouse BOEKT in plaats van ophalen**</span><span class="sxs-lookup"><span data-stu-id="943ec-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="943ec-785">Bij het gebruik van HTTP GET toocall hello **Search** API, moet u toobe Houd er rekening mee dat Hallo Hallo aanvraag-URL kan niet langer zijn dan 8 KB.</span><span class="sxs-lookup"><span data-stu-id="943ec-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="943ec-786">Dit is meestal genoeg voor de meeste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-786">This is usually enough for most applications.</span></span> <span data-ttu-id="943ec-787">Sommige toepassingen produceren echter zeer grote query's of OData-filterexpressies.</span><span class="sxs-lookup"><span data-stu-id="943ec-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="943ec-788">Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters en query's dan GET.</span><span class="sxs-lookup"><span data-stu-id="943ec-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="943ec-789">Met POST, Hallo aantal termen of componenten in een query is Hallo factor, niet Hallo grootte van Hallo onbewerkte query omdat Hallo aanvraag groottelimiet voor POST ongeveer 16 MB is beperken.</span><span class="sxs-lookup"><span data-stu-id="943ec-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-790">Hoewel de maximale grootte Hallo POST-aanvraag is te lang., zoekquery's en filterexpressies mogen niet willekeurig complexe.</span><span class="sxs-lookup"><span data-stu-id="943ec-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="943ec-791">Zie [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) en [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over zoekopdracht query en filter complexiteit beperkingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="943ec-792">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-792">**Request**</span></span>

<span data-ttu-id="943ec-793">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-794">Hallo **Search** aanvraag kan worden opgesteld met Hallo GET of POST-methoden.</span><span class="sxs-lookup"><span data-stu-id="943ec-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="943ec-795">Hallo aanvraag-URI geeft aan welke tooquery index, voor alle documenten die overeenkomen met Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="943ec-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="943ec-796">Parameters zijn opgegeven in de queryreeks Hallo in geval van GET-aanvragen hello en in Hallo aanvraag hoofdtekst in geval van Hallo van POST-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="943ec-797">Als een best practice bij het maken van GET-aanvragen te onthouden[URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke parameters bij het aanroepen van REST-API rechtstreeks Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="943ec-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="943ec-798">Voor **Search** bewerkingen, dit omvat:</span><span class="sxs-lookup"><span data-stu-id="943ec-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="943ec-799">URL-codering wordt alleen aanbevolen voor Hallo hierboven queryparameters.</span><span class="sxs-lookup"><span data-stu-id="943ec-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="943ec-800">Als u per ongeluk URL coderen hello volledige queryreeks (alles na Hallo?), worden aanvragen wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="943ec-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="943ec-801">Zo is de URL-codering ook alleen nodig bij het aanroepen van Hallo direct met REST-API aan.</span><span class="sxs-lookup"><span data-stu-id="943ec-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="943ec-802">Er is geen URL-codering is nodig bij het aanroepen van **zoeken** POST, met of bij het gebruik van Hallo [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die het URL-codering voor u verwerkt.</span><span class="sxs-lookup"><span data-stu-id="943ec-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="943ec-803"><a name="SearchQueryParameters"></a>
**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="943ec-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="943ec-804">**Search** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert.</span><span class="sxs-lookup"><span data-stu-id="943ec-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="943ec-805">U opgeven dat deze parameters in Hallo URL querytekenreeks bij het aanroepen van **Search** via GET en als JSON-eigenschappen in de aanvraagtekst Hallo bij het aanroepen van **Search** via POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="943ec-806">Hallo-syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="943ec-807">Deze verschillen worden vermeld als die van toepassing zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="943ec-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="943ec-808">`search=[string]`(optioneel) - Hallo toosearch voor tekst.</span><span class="sxs-lookup"><span data-stu-id="943ec-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="943ec-809">Alle `searchable` velden worden doorzocht door standaard tenzij `searchFields` is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="943ec-810">Bij het zoeken naar `searchable` velden, Hallo zoektekst zelf tokenized, zodat meerdere voorwaarden kunnen worden gescheiden door spaties bevatten (bijvoorbeeld: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="943ec-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="943ec-811">toomatch gebruik van elke termijn `*` (dit kan handig zijn voor Booleaanse filterquery's).</span><span class="sxs-lookup"><span data-stu-id="943ec-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="943ec-812">Als deze parameter wordt weggelaten heeft hetzelfde effect als de instelling voor het te Hallo`*`.</span><span class="sxs-lookup"><span data-stu-id="943ec-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="943ec-813">Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) voor foutopsporingsgegevens op Hallo zoeksyntaxis.</span><span class="sxs-lookup"><span data-stu-id="943ec-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="943ec-814">**Opmerking**: Hallo resultaten kunnen soms verrassend zijn bij het opvragen via `searchable` velden.</span><span class="sxs-lookup"><span data-stu-id="943ec-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="943ec-815">Hallo tokenizer bevat logica toohandle gevallen algemene tooEnglish tekst zoals apostrof, komma's in cijfers, enzovoort. Bijvoorbeeld: `search=123,456` komt overeen met een enkele term 123,456 in plaats van afzonderlijke termen Hallo 123 en 456, omdat komma's worden gebruikt als duizend scheidingstekens voor grote aantallen in het Engels.</span><span class="sxs-lookup"><span data-stu-id="943ec-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="943ec-816">Daarom wordt u aangeraden witruimte in plaats van leestekens tooseparate voorwaarden in Hallo `search` parameter.</span><span class="sxs-lookup"><span data-stu-id="943ec-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="943ec-817">`searchMode=any|all`(optioneel, standaard te`any`) - of één of alle Hallo zoektermen in volgorde toocount Hallo document als een overeenkomst moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="943ec-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="943ec-818">`searchFields=[string]`(optioneel) - Hallo lijst met door komma's gescheiden veld namen toosearch voor Hallo opgegeven tekst.</span><span class="sxs-lookup"><span data-stu-id="943ec-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="943ec-819">Doelvelden moeten worden gemarkeerd als `searchable`.</span><span class="sxs-lookup"><span data-stu-id="943ec-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="943ec-820">`queryType=simple|full`(optioneel, standaard te`simple`): wanneer set te 'eenvoudige' zoektekst wordt geïnterpreteerd met behulp van een eenvoudige querytaal waarmee symbolen zoals +, * en ' '.</span><span class="sxs-lookup"><span data-stu-id="943ec-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="943ec-821">Query's worden geëvalueerd in de doorzoekbare velden (of velden die zijn aangegeven in `searchFields`) in elk document standaard.</span><span class="sxs-lookup"><span data-stu-id="943ec-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="943ec-822">Wanneer het querytype hello te is ingesteld`full` zoektekst met behulp van Hallo Lucene-querytaal waarmee veld-specifieke en gewogen zoekopdrachten wordt geïnterpreteerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="943ec-823">Zie [eenvoudige querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx) en [Lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx) voor foutopsporingsgegevens op Hallo zoeken syntaxis.</span><span class="sxs-lookup"><span data-stu-id="943ec-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="943ec-824">Zoeken in Hallo Lucene querytaal wordt niet ondersteund voor $filter dat vergelijkbare functionaliteit biedt liggen.</span><span class="sxs-lookup"><span data-stu-id="943ec-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="943ec-825">`moreLikeThis=[key]`(optioneel) **Belangrijk:** deze functie is alleen beschikbaar in `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-826">Deze optie kan niet worden gebruikt in een query met Hallo tekst zoekparameter `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="943ec-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="943ec-827">Hallo `moreLikeThis` parameter vindt documenten die vergelijkbaar toohello document dat is opgegeven door Hallo documentsleutel zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="943ec-828">Wanneer een search-aanvraag wordt gedaan met `moreLikeThis`, een lijst met zoektermen is gegenereerd op basis van het Hallo-frequentie en zeldzaamheid van termen in Hallo brondocument.</span><span class="sxs-lookup"><span data-stu-id="943ec-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="943ec-829">Deze voorwaarden worden vervolgens gebruikt toomake Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="943ec-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="943ec-830">Hallo standaard de inhoud van alle `searchable` velden worden beschouwd als tenzij `searchFields` is gebruikte toorestrict welke velden worden doorzocht.</span><span class="sxs-lookup"><span data-stu-id="943ec-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="943ec-831">`$skip=#`(optioneel) - aantal search Hallo resulteert tooskip; Kan niet meer dan 100.000.</span><span class="sxs-lookup"><span data-stu-id="943ec-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="943ec-832">Als u documenten in volgorde tooscan maar kan niet worden gebruikt `$skip` vanwege toothis beperking, kunt u overwegen `$orderby` voor een compleet besteld sleutel en `$filter` query in plaats daarvan met een bereik.</span><span class="sxs-lookup"><span data-stu-id="943ec-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-833">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `skip` in plaats van `$skip`.</span><span class="sxs-lookup"><span data-stu-id="943ec-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="943ec-834">`$top=#`(optioneel) - aantal search Hallo tooretrieve resulteert.</span><span class="sxs-lookup"><span data-stu-id="943ec-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="943ec-835">Dit kan worden gebruikt in combinatie met `$skip` zoekresultaten tooimplement clientzijde oproepen.</span><span class="sxs-lookup"><span data-stu-id="943ec-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-836">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.</span><span class="sxs-lookup"><span data-stu-id="943ec-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="943ec-837">`$count=true|false`(optioneel, standaard te`false`)-geeft aan of toofetch Hallo totaal aantal resultaten.</span><span class="sxs-lookup"><span data-stu-id="943ec-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="943ec-838">Dit is het aantal alle documenten die overeenkomen met de Hallo Hallo `search` en `$filter` parameters worden genegeerd `$top` en `$skip`.</span><span class="sxs-lookup"><span data-stu-id="943ec-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="943ec-839">Als u deze waarde te`true` mogelijk invloed op de prestaties.</span><span class="sxs-lookup"><span data-stu-id="943ec-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="943ec-840">Houd er rekening mee dat Hallo aantal geretourneerd een benadering is.</span><span class="sxs-lookup"><span data-stu-id="943ec-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-841">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `count` in plaats van `$count`.</span><span class="sxs-lookup"><span data-stu-id="943ec-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="943ec-842">`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies toosort Hallo resultaten door.</span><span class="sxs-lookup"><span data-stu-id="943ec-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="943ec-843">Elke expressie kan bestaan uit naam van een veld of een aanroep van toohello `geo.distance()` functie.</span><span class="sxs-lookup"><span data-stu-id="943ec-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="943ec-844">Elke expressie kan worden gevolgd door `asc` tooindicated oplopende, en `desc` tooindicate aflopende.</span><span class="sxs-lookup"><span data-stu-id="943ec-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="943ec-845">Hallo standaard is oplopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="943ec-845">hello default is ascending order.</span></span> <span data-ttu-id="943ec-846">Ties wordt Hallo overeen scores van documenten worden opgesplitst.</span><span class="sxs-lookup"><span data-stu-id="943ec-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="943ec-847">Als er geen `$orderby` is opgegeven, Hallo standaardsorteervolgorde is Aflopend op document overeen score.</span><span class="sxs-lookup"><span data-stu-id="943ec-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="943ec-848">Er is een limiet van 32 componenten voor `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="943ec-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-849">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="943ec-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="943ec-850">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="943ec-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="943ec-851">Als u niets opgeeft, moet alle velden die zijn gemarkeerd als worden opgehaald in het Hallo-schema zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="943ec-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="943ec-852">U kunt ook expliciet alle velden aanvragen door deze parameter te`*`.</span><span class="sxs-lookup"><span data-stu-id="943ec-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-853">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.</span><span class="sxs-lookup"><span data-stu-id="943ec-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="943ec-854">`facet=[string]`(nul of meer) - een veld toofacet door.</span><span class="sxs-lookup"><span data-stu-id="943ec-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="943ec-855">Hallo-tekenreeks kan eventueel parameters toocustomize Hallo facetten uitgedrukt als een door komma's gescheiden `name:value` paren.</span><span class="sxs-lookup"><span data-stu-id="943ec-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="943ec-856">Geldige parameters zijn:</span><span class="sxs-lookup"><span data-stu-id="943ec-856">Valid parameters are:</span></span>

* <span data-ttu-id="943ec-857">`count`(max. aantal facet voorwaarden; standaardwaarde is 10).</span><span class="sxs-lookup"><span data-stu-id="943ec-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="943ec-858">Er is geen maximum maar hogere waarden worden een bijbehorende op de prestaties, vooral als Hallo meervoudige veld een groot aantal unieke voorwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="943ec-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="943ec-859">Bijvoorbeeld: `facet=category,count:5` opgehaald Hallo bovenste vijf categorieën in facet resultaten.</span><span class="sxs-lookup"><span data-stu-id="943ec-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="943ec-860">**Opmerking**: als hello `count` parameter kleiner is dan het aantal unieke voorwaarden hello, Hallo resultaten mogelijk niet nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="943ec-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="943ec-861">Dit is vanwege toohello manier facetten query's zijn verdeeld over shards.</span><span class="sxs-lookup"><span data-stu-id="943ec-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="943ec-862">Verhogen `count` doorgaans toeneemt Hallo nauwkeurigheid van Hallo term aantallen, maar in een prestatievermindering optreden.</span><span class="sxs-lookup"><span data-stu-id="943ec-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="943ec-863">`sort`(een van de `count` toosort *aflopende* op aantal `-count` toosort *oplopende* op aantal `value` toosort *oplopende* op waarde, of `-value` toosort *aflopende* door waarde)</span><span class="sxs-lookup"><span data-stu-id="943ec-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="943ec-864">Bijvoorbeeld: `facet=category,count:3,sort:count` opgehaald Hallo bovenste drie categorieën in facet resultaten in aflopende volgorde voor het aantal documenten met de stadsnaam van elke Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="943ec-865">Bijvoorbeeld, als bovenste drie categorieën Hallo Budget, Motel en luxe zijn, Budget gevonden in de 5 is, Motel 6 en heeft, luxe 4 is, vervolgens hello buckets niet in volgorde van Hallo Motel, Budget, luxe.</span><span class="sxs-lookup"><span data-stu-id="943ec-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="943ec-866">Bijvoorbeeld: `facet=rating,sort:-value` buckets voor alle mogelijke beoordelingen in aflopende volgorde voor waarde produceert.</span><span class="sxs-lookup"><span data-stu-id="943ec-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="943ec-867">Als Hallo classificaties uit 1 too5, wordt Hallo buckets besteld 5, 4, 3, 2, 1, ongeacht het aantal documenten overeenkomen met elke beoordeling.</span><span class="sxs-lookup"><span data-stu-id="943ec-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="943ec-868">`values`(pipe gescheiden numerieke of `Edm.DateTimeOffset` waarden opgeven van een dynamische set facet vermelding waarden)</span><span class="sxs-lookup"><span data-stu-id="943ec-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="943ec-869">Bijvoorbeeld: `facet=baseRate,values:10|20` produceert drie buckets: één voor base snelheid 0 up toobut niet met inbegrip van 10, één voor 10 up toobut niet inclusief 20 en één voor 20 of hoger.</span><span class="sxs-lookup"><span data-stu-id="943ec-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="943ec-870">Bijvoorbeeld: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produceert twee buckets: één voor hotels renovated vóór februari 2010 en één voor hotels renovated februari 1e, 2010 of hoger.</span><span class="sxs-lookup"><span data-stu-id="943ec-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="943ec-871">`interval`(geheel getal interval dat groter is dan 0 voor getallen, of `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` datumwaarden tijd)</span><span class="sxs-lookup"><span data-stu-id="943ec-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="943ec-872">Bijvoorbeeld: `facet=baseRate,interval:100` produceert op basis van base snelheid bereiken met een grootte van 100 buckets.</span><span class="sxs-lookup"><span data-stu-id="943ec-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="943ec-873">Bijvoorbeeld, als base tarieven alle tussen $60 en $600, zullen er buckets voor 0-100, 100-200, 200 en 300, 400 500, 300 400 en 500-600.</span><span class="sxs-lookup"><span data-stu-id="943ec-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="943ec-874">Bijvoorbeeld: `facet=lastRenovationDate,interval:year` één bucket voor elk jaar wanneer hotels zijn renovated produceert.</span><span class="sxs-lookup"><span data-stu-id="943ec-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="943ec-875">`timeoffset`([+-] hh: mm, [+-] UUMM, of [+-] hh) `timeoffset` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="943ec-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="943ec-876">Kan alleen worden gecombineerd met Hallo `interval` optie en alleen wanneer toegepaste tooa veld van het type `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="943ec-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="943ec-877">Hallo waarde geeft Hallo UTC tijd verschoven tooaccount voor bij het instellen van tijd grenzen.</span><span class="sxs-lookup"><span data-stu-id="943ec-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="943ec-878">Bijvoorbeeld: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` gebruikt Hallo dag grens die bij 01:00:00 UTC (middernacht in Hallo doeltijdzone begint)</span><span class="sxs-lookup"><span data-stu-id="943ec-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="943ec-879">**Opmerking**: `count` en `sort` worden gecombineerd tot Hallo dezelfde facet specificatie, maar ze kunnen niet worden gecombineerd met `interval` of `values`, en `interval` en `values` kan niet worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="943ec-880">**Opmerking**: Interval facetten op datum / tijd worden berekend op basis van UTC-tijd als `timeoffset` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="943ec-881">Bijvoorbeeld: voor `facet=lastRenovationDate,interval:day`, Hallo dag grens begint bij 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="943ec-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="943ec-882">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `facets` in plaats van `facet`.</span><span class="sxs-lookup"><span data-stu-id="943ec-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="943ec-883">Bovendien geeft u het als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke facet-expressie is.</span><span class="sxs-lookup"><span data-stu-id="943ec-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="943ec-884">`$filter=[string]`(optioneel): een zoekexpressie gestructureerde in de standaard OData-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="943ec-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-885">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.</span><span class="sxs-lookup"><span data-stu-id="943ec-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="943ec-886">`highlight=[string]`(optioneel): een reeks door komma's gescheiden veldnamen gebruikt voor treffer worden gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="943ec-887">Alleen `searchable` velden kunnen worden gebruikt voor treffers markeren.</span><span class="sxs-lookup"><span data-stu-id="943ec-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="943ec-888">`highlightPreTag=[string]`(optioneel, standaard te`<em>`): een string-code die voegt toohit licht toe.</span><span class="sxs-lookup"><span data-stu-id="943ec-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="943ec-889">Moet worden ingesteld met `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="943ec-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-890">Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="943ec-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="943ec-891">`highlightPostTag=[string]`(optioneel, standaard te`</em>`)-tekenreeks label toohit highlights worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="943ec-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="943ec-892">Moet worden ingesteld met `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="943ec-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-893">Bij het aanroepen van **Search** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="943ec-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="943ec-894">`scoringProfile=[string]`(optioneel) - Hallo-naam van een score profiel tooevaluate overeen scores voor overeenkomende documenten in volgorde toosort Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="943ec-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="943ec-895">`scoringParameter=[string]`Geeft aan Hallo waarden voor elke parameter die is gedefinieerd in een score functie (nul of meer) - (bijvoorbeeld `referencePointParameter`) met de indeling Hallo `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="943ec-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="943ec-896">Bijvoorbeeld, als Hallo score berekenen profiel een functie met definieert een parameter met de naam van de optie 'mylocation' hello query-tekenreeks zou zijn `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="943ec-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="943ec-897">Hallo eerste dash scheidt Hallo naam uit de lijst met waarden Hallo, terwijl de tweede streepje Hallo deel uit van Hallo eerste waarde (lengtegraad in dit voorbeeld maakt).</span><span class="sxs-lookup"><span data-stu-id="943ec-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="943ec-898">Scoreprofiel parameters kunt u een dergelijke waarden in Hallo lijst met enkele aanhalingstekens escape zoals voor de code die versterking kunt bevatten komma's.</span><span class="sxs-lookup"><span data-stu-id="943ec-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="943ec-899">Als Hallo waarden zelf tussen enkele aanhalingstekens bevatten, kunt u dit omheen door te verdubbelen.</span><span class="sxs-lookup"><span data-stu-id="943ec-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="943ec-900">Bijvoorbeeld, als u een parameter met de naam 'mytag' versterking tag hebt en u tooboost op Hallo code wilt waarden 'Hallo, O'Brien' en 'Smith' hello query verbindingsreeksoptie zou worden `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="943ec-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="943ec-901">Aanhalingstekens zijn alleen vereist voor waarden die door komma's bevatten.</span><span class="sxs-lookup"><span data-stu-id="943ec-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-902">Bij het aanroepen van **Search** POST gebruikt, deze parameter is met de naam `scoringParameters` in plaats van `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="943ec-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="943ec-903">U ook als een JSON-matrix van tekenreeksen waar elke tekenreeks een afzonderlijke is `name-values` paar.</span><span class="sxs-lookup"><span data-stu-id="943ec-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="943ec-904">`minimumCoverage`(optioneel, standaard too100) - een getal tussen 0 en 100, waarmee wordt aangegeven percentage Hallo Hallo-index die moet worden gedekt door een zoekopdracht om Hallo query toobe gerapporteerd als een is voltooid.</span><span class="sxs-lookup"><span data-stu-id="943ec-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="943ec-905">Standaard Hallo gehele index moet beschikbaar zijn of `Search` HTTP-statuscode 503 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="943ec-906">Als u instelt `minimumCoverage` en `Search` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord Hallo Hallo percentage Hallo-index die is opgenomen in het Hallo-query waarmee wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-907">Als u deze parameter tooa-waarde lager dan 100 nuttig zijn kan voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica.</span><span class="sxs-lookup"><span data-stu-id="943ec-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="943ec-908">Niet alle overeenkomende documenten zijn echter toobe aanwezig zijn in de zoekresultaten Hallo gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="943ec-909">Als zoeken intrekken belangrijker tooyour toepassing dan beschikbaarheid is, wordt het aanbevolen tooleave is `minimumCoverage` op de standaardwaarde van 100.</span><span class="sxs-lookup"><span data-stu-id="943ec-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="943ec-910">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-911">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-912">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-913">Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter in Hallo-URL, ongeacht of u aanroepen **Search** met GET of POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="943ec-914">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-914">**Request Headers**</span></span>

<span data-ttu-id="943ec-915">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-916">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-917">Het is een tekenreekswaarde, unieke tooyour service-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="943ec-918">Hallo **Search** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="943ec-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="943ec-919">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-920">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-921">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-922">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-922">**Request Body**</span></span>

<span data-ttu-id="943ec-923">Voor GET: geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-923">For GET: None.</span></span>

<span data-ttu-id="943ec-924">Voor POST:</span><span class="sxs-lookup"><span data-stu-id="943ec-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
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

<span data-ttu-id="943ec-925">**Voortzetting van antwoorden voor Deelzoekopdrachten**</span><span class="sxs-lookup"><span data-stu-id="943ec-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="943ec-926">Soms kan niet Azure Search alle aangevraagde resultaten in een enkel antwoord met zoeken Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="943ec-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="943ec-927">Dit kan gebeuren om verschillende redenen, zoals wanneer Hallo query te veel documenten aanvragen door op te geven niet `$top` of een waarde opgeeft voor `$top` die te groot is.</span><span class="sxs-lookup"><span data-stu-id="943ec-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="943ec-928">In dergelijke gevallen horen Azure Search Hallo `@odata.nextLink` aantekening in antwoordtekst hello, en ook `@search.nextPageParameters` als deze een POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="943ec-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="943ec-929">Kunt u Hallo waarden van deze aantekeningen tooformulate zoeken aanvraag tooget Hallo volgende ergens anders in Hallo zoeken antwoord.</span><span class="sxs-lookup"><span data-stu-id="943ec-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="943ec-930">Dit wordt genoemd, een ***voortzetting*** van de oorspronkelijke zoekaanvraag Hallo en Hallo aantekeningen in het algemeen worden genoemd ***voortzetting tokens***.</span><span class="sxs-lookup"><span data-stu-id="943ec-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="943ec-931">Zie [Hallo onderstaand voorbeeld](#SearchResponse) voor meer informatie over Hallo syntaxis van deze aantekeningen en waar ze worden weergegeven in de antwoordtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="943ec-932">Hallo redenen waarom Azure Search voortzetting tokens retourneert zijn implementatie en onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="943ec-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="943ec-933">Robuuste clients moeten altijd gereed toohandle gevallen waarbij minder documenten dan verwacht worden geretourneerd en een vervolgtoken is opgenomen toocontinue bij het ophalen van documenten.</span><span class="sxs-lookup"><span data-stu-id="943ec-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="943ec-934">Ook opmerking die u moet gebruiken dezelfde HTTP-methode als de oorspronkelijke aanvraag Hallo in volgorde toocontinue Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="943ec-935">Bijvoorbeeld, als u een GET-aanvraag verzonden, voortzetting verzoeken u verzendt moeten ook gebruiken GET (en ook voor POST).</span><span class="sxs-lookup"><span data-stu-id="943ec-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="943ec-936"><a name="SearchResponse"></a>
**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="943ec-937">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
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
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="943ec-938">**Voorbeelden:**</span><span class="sxs-lookup"><span data-stu-id="943ec-938">**Examples:**</span></span>

<span data-ttu-id="943ec-939">U vindt aanvullende voorbeelden gegeven op Hallo [OData-expressiesyntaxis voor Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="943ec-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="943ec-940">Hallo Search Index gesorteerd in aflopende volgorde datum.</span><span class="sxs-lookup"><span data-stu-id="943ec-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="943ec-941">GET-/indexes/hotels/docs? zoeken = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'orderby': "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="943ec-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="943ec-943">In een meervoudige zoekopdracht zoekt Hallo-index en facetten voor categorieën, classificatie, labels, evenals artikelen met baseRate in specifieke bereiken ophalen:</span><span class="sxs-lookup"><span data-stu-id="943ec-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="943ec-944">GET /indexes/hotels/docs? zoeken = test & facet = categorie & facet = classificatie & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['categorie', 'classificatie', 'tags', ' baseRate, waarden: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="943ec-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="943ec-946">Met een filter Hallo vorige meervoudige queryresultaten beperken nadat de gebruiker op Hallo classificatie 3 en categorie 'Motel':</span><span class="sxs-lookup"><span data-stu-id="943ec-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="943ec-947">GET /indexes/hotels/docs? zoeken = test & facet = labels & facet baseRate, waarden: 80 = | 150 | 220 & $filter = classificatie eq 3 en categorie-eq "Motel" & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": 'test', 'facetten': ['tags', ' baseRate, waarden: 80 | 150 | 220"], 'filter': 'classificatie eq 3 en categorie-eq 'Motel' '}</span><span class="sxs-lookup"><span data-stu-id="943ec-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="943ec-949">In een meervoudige zoekopdracht, moet u een bovenlimiet instellen op unieke voorwaarden in een query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="943ec-950">Hallo standaardwaarde is 10, maar u kunt vergroten of verkleinen van deze waarde Hallo `count` parameter op Hallo `facet` kenmerk:</span><span class="sxs-lookup"><span data-stu-id="943ec-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="943ec-951">GET-/indexes/hotels/docs? zoeken = test & facet = city, aantal: 5 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'zoeken': 'test', 'facetten': ["city, aantal: 5"]}</span><span class="sxs-lookup"><span data-stu-id="943ec-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="943ec-953">Hallo Index binnen specifieke velden; zoeken Bijvoorbeeld, een specifieke taal zijn gebonden veld:</span><span class="sxs-lookup"><span data-stu-id="943ec-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="943ec-954">GET-/indexes/hotels/docs? zoeken = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "hôtel', 'searchFields':"description_fr"}</span><span class="sxs-lookup"><span data-stu-id="943ec-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="943ec-956">Hallo Index over meerdere velden zoeken.</span><span class="sxs-lookup"><span data-stu-id="943ec-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="943ec-957">Bijvoorbeeld, u kunt opslaan en query doorzoekbare velden in meerdere talen, alle binnen dezelfde index Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="943ec-958">Als de Engelse en Franse beschrijvingen naast elkaar bestaan in Hallo dezelfde document, kunt u terugkeren of alle in Hallo queryresultaten:</span><span class="sxs-lookup"><span data-stu-id="943ec-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="943ec-959">GET-/indexes/hotels/docs? zoeken = hotel & searchFields = beschrijving, description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "Hotels", "searchFields": "beschrijving, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="943ec-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="943ec-961">Houd er rekening mee dat u kunt alleen een query één index op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="943ec-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="943ec-962">Maak meerdere indexen voor elke taal geen tenzij u tooquery een tegelijk.</span><span class="sxs-lookup"><span data-stu-id="943ec-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="943ec-963">Wisselbestand - Get Hallo 1e pagina met items (paginaformaat is 10):</span><span class="sxs-lookup"><span data-stu-id="943ec-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="943ec-964">GET-/indexes/hotels/docs? zoeken = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "* ', 'overslaan': 0, 'top': 10}</span><span class="sxs-lookup"><span data-stu-id="943ec-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="943ec-966">Wisselbestand - Get Hallo 2e pagina met items (paginaformaat is 10):</span><span class="sxs-lookup"><span data-stu-id="943ec-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="943ec-967">GET-/indexes/hotels/docs? zoeken = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'search': ' * ', 'overslaan': 10, 'top': 10}</span><span class="sxs-lookup"><span data-stu-id="943ec-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="943ec-969">Ophalen van een specifieke set velden:</span><span class="sxs-lookup"><span data-stu-id="943ec-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="943ec-970">GET-/indexes/hotels/docs? zoeken = * & $select = hotelName, beschrijving en api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": ' * ', 'select': "hotelName Beschrijving"}</span><span class="sxs-lookup"><span data-stu-id="943ec-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="943ec-972">Ophalen van documenten die overeenkomt met een specifieke filterexpressie:</span><span class="sxs-lookup"><span data-stu-id="943ec-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="943ec-973">GET-/indexes/hotels/docs? $filter = (baseRate ge 60 en baseRate lt 300) of hotelName eq fraai blijven & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {'filter': ' (baseRate ge 60 en baseRate lt 300) of hotelName eq 'Fraai verblijf' "}</span><span class="sxs-lookup"><span data-stu-id="943ec-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="943ec-975">Hallo-index te zoeken en fragmenten met treffers licht retourneren</span><span class="sxs-lookup"><span data-stu-id="943ec-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="943ec-976">GET-/indexes/hotels/docs? zoeken = iets & Markeer = beschrijving & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets", "highlight": 'beschrijving'}</span><span class="sxs-lookup"><span data-stu-id="943ec-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="943ec-978">Hallo-index te zoeken en documenten van dichter toofarther weg van een referentielocatie gesorteerd retourneren</span><span class="sxs-lookup"><span data-stu-id="943ec-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="943ec-979">GET-/indexes/hotels/docs? zoeken = iets & $orderby=geo.distance (locatie, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'orderby': ' geo.distance (locatie, geography'POINT(-122.12315 47.88121)')"}</span><span class="sxs-lookup"><span data-stu-id="943ec-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="943ec-981">Zoeken Hallo index ervan uitgaande dat er een 'geografisch' aangeroepen scoreprofiel met twee afstandsscorefuncties, wordt één definiëren van een parameter genaamd 'currentLocation' en één voor het definiëren van een parameter met de naam 'lastLocation'</span><span class="sxs-lookup"><span data-stu-id="943ec-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="943ec-982">GET /indexes/hotels/docs? zoeken = iets & scoringProfile = geo & scoringParameter = currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "iets', 'scoringProfile': 'geo', 'scoringParameters': [' currentLocation--122.123,44.77233 ', ' lastLocation--121.499,44.2113 ']}</span><span class="sxs-lookup"><span data-stu-id="943ec-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="943ec-984">Documenten zoeken in het Hallo-index met behulp [vereenvoudigde querysyntaxis](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="943ec-985">Deze query retourneert hotels waar doorzoekbare velden Hallo voorwaarden 'comfort' en 'locatie', maar niet 'motel bevatten':</span><span class="sxs-lookup"><span data-stu-id="943ec-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="943ec-986">GET-/indexes/hotels/docs? zoeken = comfort + locatie-motel & searchMode = all & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="943ec-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="943ec-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "comfort + locatie-motel ', 'searchMode': 'alle'}</span><span class="sxs-lookup"><span data-stu-id="943ec-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="943ec-988">Houd er rekening mee Hallo gebruik van `searchMode=all` hierboven.</span><span class="sxs-lookup"><span data-stu-id="943ec-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="943ec-989">Deze parameter inclusief overschrijft Hallo standaard van `searchMode=any`, zorgt dat `-motel` 'En niet' in plaats van "Of niet" betekent.</span><span class="sxs-lookup"><span data-stu-id="943ec-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="943ec-990">Zonder `searchMode=all`, krijgt u "Of niet" dat wordt uitgebreid in plaats van de zoekresultaten wordt beperkt, en dit kan erg intuïtief toosome gebruikers zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="943ec-991">Documenten zoeken in het Hallo-index met behulp [lucene-querysyntaxis](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="943ec-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="943ec-992">Deze query retourneert hotels waarbij categorieveld Hallo Hallo term 'budget' en alle doorzoekbare velden die Hallo de zin "onlangs renovated" bevat.</span><span class="sxs-lookup"><span data-stu-id="943ec-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="943ec-993">Documenten met Hallo zinsnede 'onlangs renovated' krijgen een hogere rang als gevolg van Hallo term versterking waarde (3)</span><span class="sxs-lookup"><span data-stu-id="943ec-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="943ec-994">GET-/indexes/hotels/docs? zoeken = categorie: budget en \"onlangs renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & querytype = full</span><span class="sxs-lookup"><span data-stu-id="943ec-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="943ec-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"zoeken": "categorie: budget en \"onlangs renovated\"^ 3", 'queryType': 'volledige', 'searchMode': 'alle'}</span><span class="sxs-lookup"><span data-stu-id="943ec-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="943ec-996">Lookup-Document</span><span class="sxs-lookup"><span data-stu-id="943ec-996">Lookup Document</span></span>
<span data-ttu-id="943ec-997">Hallo **Lookup Document** bewerking een document opgehaald uit Azure Search.</span><span class="sxs-lookup"><span data-stu-id="943ec-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="943ec-998">Dit is handig wanneer een gebruiker op een specifieke zoekresultaat klikt en toolook om specifieke details over dat document gewenste.</span><span class="sxs-lookup"><span data-stu-id="943ec-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="943ec-999">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-999">**Request**</span></span>

<span data-ttu-id="943ec-1000">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-1001">Hallo **Lookup Document** verzoek als volgt kan worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="943ec-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="943ec-1002">U kunt ook Hallo traditionele OData-syntaxis voor het opzoeken van een sleutel gebruiken:</span><span class="sxs-lookup"><span data-stu-id="943ec-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="943ec-1003">Hallo-aanvraag URI bevat [index name] en [sleutel], die aangeeft welke tooretrieve document uit welke index.</span><span class="sxs-lookup"><span data-stu-id="943ec-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="943ec-1004">U kunt slechts één document tegelijk ophalen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1004">You can only get one document at a time.</span></span> <span data-ttu-id="943ec-1005">Gebruik **Search** tooget meerdere documenten in één aanvraag.</span><span class="sxs-lookup"><span data-stu-id="943ec-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="943ec-1006">**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="943ec-1006">**Query Parameters**</span></span>

<span data-ttu-id="943ec-1007">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="943ec-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="943ec-1008">Als dat niet-opgegeven of te ingesteld`*`, alle velden die zijn gemarkeerd als worden opgehaald in het Hallo-schema zijn opgenomen in het Hallo-projectie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="943ec-1009">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-1010">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-1011">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-1012">Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter.</span><span class="sxs-lookup"><span data-stu-id="943ec-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="943ec-1013">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-1013">**Request Headers**</span></span>

<span data-ttu-id="943ec-1014">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-1015">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-1016">Het is een tekenreekswaarde, unieke tooyour service-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="943ec-1017">Hallo **Lookup Document** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="943ec-1018">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-1019">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-1020">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-1021">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-1021">**Request Body**</span></span>

<span data-ttu-id="943ec-1022">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1022">None.</span></span>

<span data-ttu-id="943ec-1023">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-1023">**Response**</span></span>

<span data-ttu-id="943ec-1024">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="943ec-1025">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="943ec-1025">**Example**</span></span>

<span data-ttu-id="943ec-1026">Lookup Hallo document die sleutel '2' heeft</span><span class="sxs-lookup"><span data-stu-id="943ec-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="943ec-1027">Lookup Hallo-document met sleutel 3 met OData-syntaxis:</span><span class="sxs-lookup"><span data-stu-id="943ec-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="943ec-1028">Aantal documenten</span><span class="sxs-lookup"><span data-stu-id="943ec-1028">Count Documents</span></span>
<span data-ttu-id="943ec-1029">Hallo **aantal documenten** bewerking wordt een telling van het aantal documenten in een zoekindex Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="943ec-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="943ec-1030">Hallo `$count` syntaxis maakt deel uit van Hallo OData-protocol.</span><span class="sxs-lookup"><span data-stu-id="943ec-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="943ec-1031">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-1031">**Request**</span></span>

<span data-ttu-id="943ec-1032">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-1033">Hallo **aantal documenten** aanvraag kan worden opgesteld met Hallo GET-methode.</span><span class="sxs-lookup"><span data-stu-id="943ec-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="943ec-1034">Hallo [naam van de index] in Hallo aanvraag-URI vertelt Hallo service tooreturn een telling van alle items in Hallo docs verzameling van Hallo opgegeven index.</span><span class="sxs-lookup"><span data-stu-id="943ec-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="943ec-1035">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-1036">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-1037">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-1038">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-1038">**Request Headers**</span></span>

<span data-ttu-id="943ec-1039">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="943ec-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="943ec-1040">`Accept`: Met deze waarde te moet worden ingesteld`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="943ec-1041">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-1042">Het is een tekenreekswaarde, unieke tooyour service-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="943ec-1043">Hallo **aantal documenten** aanvraag kunt opgeven, een beheersleutel of een querysleutel voor `api-key`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="943ec-1044">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-1045">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-1046">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-1047">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-1047">**Request Body**</span></span>

<span data-ttu-id="943ec-1048">Geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1048">None.</span></span>

<span data-ttu-id="943ec-1049">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-1049">**Response**</span></span>

<span data-ttu-id="943ec-1050">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="943ec-1051">Hallo-antwoordtekst bevat Hallo count-waarde als een geheel getal als tekst zonder opmaak geformatteerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="943ec-1052">Suggesties</span><span class="sxs-lookup"><span data-stu-id="943ec-1052">Suggestions</span></span>
<span data-ttu-id="943ec-1053">Hallo **suggesties** bewerking suggesties op basis van deelzoekopdrachten invoer worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="943ec-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="943ec-1054">Dit wordt doorgaans gebruikt in de vakken tooprovide automatisch aangevulde zoeksuggesties als gebruikers zoektermen invoert.</span><span class="sxs-lookup"><span data-stu-id="943ec-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="943ec-1055">Suggestie aanvragen die zijn gericht op het opmaken van de doeldocumenten, zodat Hallo voorgestelde tekst kan worden herhaald als meerdere candidate documenten Hallo overeenkomen met dezelfde invoer zoeken.</span><span class="sxs-lookup"><span data-stu-id="943ec-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="943ec-1056">U kunt `$select` tooretrieve andere document velden (inclusief Hallo documentsleutel) zodat u kunt zien welke document Hallo bron voor elke suggestie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="943ec-1057">Een **suggesties** bewerking als een GET of POST-aanvraag is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="943ec-1058">**Wanneer toouse BOEKT in plaats van ophalen**</span><span class="sxs-lookup"><span data-stu-id="943ec-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="943ec-1059">Bij het gebruik van HTTP GET toocall hello **suggesties** API, moet u toobe Houd er rekening mee dat Hallo Hallo aanvraag-URL kan niet langer zijn dan 8 KB.</span><span class="sxs-lookup"><span data-stu-id="943ec-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="943ec-1060">Dit is meestal genoeg voor de meeste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="943ec-1061">Sommige toepassingen produceren echter zeer grote query's specifiek OData-filterexpressies.</span><span class="sxs-lookup"><span data-stu-id="943ec-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="943ec-1062">Voor deze toepassingen namelijk met behulp van HTTP POST een betere keuze kunt u grotere filters dan GET.</span><span class="sxs-lookup"><span data-stu-id="943ec-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="943ec-1063">Met POST, Hallo aantal componenten in een filter is een beperkende factor hello, grootte van de onbewerkte filtertekenreeks Hallo niet Hallo omdat Hallo aanvraag groottelimiet voor POST is ongeveer 16 MB.</span><span class="sxs-lookup"><span data-stu-id="943ec-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1064">Hoewel de maximale grootte Hallo POST-aanvraag erg groot is, kunnen niet filterexpressies willekeurig complex zijn.</span><span class="sxs-lookup"><span data-stu-id="943ec-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="943ec-1065">Zie [OData-expressiesyntaxis](https://msdn.microsoft.com/library/dn798921.aspx) voor meer informatie over filter complexiteit beperkingen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="943ec-1066">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="943ec-1066">**Request**</span></span>

<span data-ttu-id="943ec-1067">HTTPS is vereist voor serviceaanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="943ec-1068">Hallo **suggesties** aanvraag kan worden opgesteld met Hallo GET of POST-methoden.</span><span class="sxs-lookup"><span data-stu-id="943ec-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="943ec-1069">Hallo aanvraag-URI bevat Hallo-naam van Hallo index tooquery.</span><span class="sxs-lookup"><span data-stu-id="943ec-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="943ec-1070">Parameters, zoals Hallo gedeeltelijk invoer zoekterm, zijn opgegeven in de queryreeks Hallo in geval van Hallo van GET-aanvragen en in Hallo aanvraag hoofdtekst in geval van Hallo van POST-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="943ec-1071">Als een best practice bij het maken van GET-aanvragen te onthouden[URL coderen](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specifieke parameters bij het aanroepen van REST-API rechtstreeks Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="943ec-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="943ec-1072">Voor **suggesties** bewerkingen, dit omvat:</span><span class="sxs-lookup"><span data-stu-id="943ec-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="943ec-1073">URL-codering wordt alleen aanbevolen voor Hallo hierboven queryparameters.</span><span class="sxs-lookup"><span data-stu-id="943ec-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="943ec-1074">Als u per ongeluk URL coderen hello volledige queryreeks (alles na Hallo?), worden aanvragen wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="943ec-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="943ec-1075">Zo is de URL-codering ook alleen nodig bij het aanroepen van Hallo direct met REST-API aan.</span><span class="sxs-lookup"><span data-stu-id="943ec-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="943ec-1076">Er is geen URL-codering is nodig bij het aanroepen van **suggesties** met behulp van POST, of bij het gebruik van Hallo [.NET-clientbibliotheek](https://msdn.microsoft.com/library/dn951165.aspx), die het URL-codering voor u verwerkt.</span><span class="sxs-lookup"><span data-stu-id="943ec-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="943ec-1077">**Query-Parameters**</span><span class="sxs-lookup"><span data-stu-id="943ec-1077">**Query Parameters**</span></span>

<span data-ttu-id="943ec-1078">**Suggesties** verschillende querycriteria kunnen geven en ook opgeven zoekgedrag parameters accepteert.</span><span class="sxs-lookup"><span data-stu-id="943ec-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="943ec-1079">U opgeven dat deze parameters in Hallo URL querytekenreeks bij het aanroepen van **suggesties** via GET en als JSON-eigenschappen in de aanvraagtekst Hallo bij het aanroepen van **suggesties** via POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="943ec-1080">Hallo-syntaxis voor een aantal parameters is enigszins verschillen tussen GET en POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="943ec-1081">Deze verschillen worden vermeld als die van toepassing zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="943ec-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="943ec-1082">`search=[string]`-Hallo tekst toouse toosuggest zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="943ec-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="943ec-1083">Moet minimaal 1 teken en niet meer dan 100 tekens.</span><span class="sxs-lookup"><span data-stu-id="943ec-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="943ec-1084">`highlightPreTag=[string]`(optioneel): een tekenreeks-code die voegt toosearch treffers toe.</span><span class="sxs-lookup"><span data-stu-id="943ec-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="943ec-1085">Moet worden ingesteld met `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1086">Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="943ec-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="943ec-1087">`highlightPostTag=[string]`(optioneel): een tekenreeks-code die wordt toegevoegd toosearch treffers.</span><span class="sxs-lookup"><span data-stu-id="943ec-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="943ec-1088">Moet worden ingesteld met `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1089">Bij het aanroepen van **suggesties** gebruik van GET, gereserveerde tekens in Hallo URL procent-gecodeerd moeten zijn (bijvoorbeeld, in plaats van #, % 23).</span><span class="sxs-lookup"><span data-stu-id="943ec-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="943ec-1090">`suggesterName=[string]`-Hallo-naam van Hallo suggestie als opgegeven in de Hallo `suggesters` verzameling die deel uitmaakt van de indexdefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="943ec-1091">Een `suggester` bepaalt welke velden voor voorgestelde querytermen worden gescand.</span><span class="sxs-lookup"><span data-stu-id="943ec-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="943ec-1092">Zie [Suggestiefunctie](#Suggesters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="943ec-1093">`fuzzy=[boolean]`(optioneel, standaard = false)-tootrue wanneer Stel deze API suggesties wordt gevonden, zelfs als er een teken vervangen of ontbreekt in de zoektekst Hallo is.</span><span class="sxs-lookup"><span data-stu-id="943ec-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="943ec-1094">Het wordt geleverd op de prestaties, zoals fuzzy suggestie zoekopdrachten trager en meer bronnen gebruiken terwijl dit een betere ervaring in sommige scenario's biedt.</span><span class="sxs-lookup"><span data-stu-id="943ec-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="943ec-1095">`searchFields=[string]`(optioneel) - Hallo-lijst met door komma's gescheiden veld namen toosearch voor Hallo zoektekst opgegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="943ec-1096">Doelvelden moeten zijn ingeschakeld voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="943ec-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="943ec-1097">`$top=#`(optioneel, standaard = 5)-aantal suggesties tooretrieve Hallo.</span><span class="sxs-lookup"><span data-stu-id="943ec-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="943ec-1098">Moet een getal tussen 1 en 100 liggen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1099">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `top` in plaats van `$top`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="943ec-1100">`$filter=[string]`(optioneel): een expressie die documenten Hallo-filters in aanmerking voor suggesties.</span><span class="sxs-lookup"><span data-stu-id="943ec-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1101">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `filter` in plaats van `$filter`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="943ec-1102">`$orderby=[string]`(optioneel): een lijst met door komma's gescheiden expressies toosort Hallo resultaten door.</span><span class="sxs-lookup"><span data-stu-id="943ec-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="943ec-1103">Elke expressie kan bestaan uit naam van een veld of een aanroep van toohello `geo.distance()` functie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="943ec-1104">Elke expressie kan worden gevolgd door `asc` tooindicated oplopende, en `desc` tooindicate aflopende.</span><span class="sxs-lookup"><span data-stu-id="943ec-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="943ec-1105">Hallo standaard is oplopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="943ec-1105">hello default is ascending order.</span></span> <span data-ttu-id="943ec-1106">Er is een limiet van 32 componenten voor `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1107">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `orderby` in plaats van `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="943ec-1108">`$select=[string]`(optioneel): een lijst met door komma's gescheiden velden tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="943ec-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="943ec-1109">Als u niets opgeeft, wordt alleen Hallo documentsleutel en suggestie tekst wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="943ec-1110">U kunt alle velden expliciet aanvragen door deze parameter te`*`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1111">Bij het aanroepen van **suggesties** POST gebruikt, deze parameter is met de naam `select` in plaats van `$select`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="943ec-1112">`minimumCoverage`(optioneel, standaard too80) - een getal tussen 0 en 100, waarmee wordt aangegeven percentage Hallo Hallo-index die moet worden gedekt door een query suggesties om Hallo query toobe gerapporteerd als een is voltooid.</span><span class="sxs-lookup"><span data-stu-id="943ec-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="943ec-1113">Standaard moet ten minste 80% van de index Hallo beschikbaar zijn of `Suggest` HTTP-statuscode 503 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="943ec-1114">Als u instelt `minimumCoverage` en `Suggest` is geslaagd, wordt HTTP 200 retourneren en bevatten een `@search.coverage` waarde in het antwoord Hallo Hallo percentage Hallo-index die is opgenomen in het Hallo-query waarmee wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="943ec-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="943ec-1115">Als u deze parameter tooa-waarde lager dan 100 nuttig zijn kan voor beschikbaarheid van de zoekopdracht zelfs voor services met slechts één replica.</span><span class="sxs-lookup"><span data-stu-id="943ec-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="943ec-1116">Niet alle overeenkomende suggesties zijn echter toobe aanwezig is in de resultaten Hallo gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="943ec-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="943ec-1117">Als intrekken belangrijker tooyour toepassing dan beschikbaarheid en vervolgens de best niet toolower `minimumCoverage` lager dan de standaardwaarde 80.</span><span class="sxs-lookup"><span data-stu-id="943ec-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="943ec-1118">`api-version=[string]`(vereist).</span><span class="sxs-lookup"><span data-stu-id="943ec-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="943ec-1119">Hallo preview-versie is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="943ec-1120">Zie [Search Serviceversiebeheer](http://msdn.microsoft.com/library/azure/dn864560.aspx) voor meer informatie en alternatieve versies.</span><span class="sxs-lookup"><span data-stu-id="943ec-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="943ec-1121">Opmerking: Voor deze bewerking Hallo `api-version` is opgegeven als een queryparameter in Hallo-URL, ongeacht of u aanroepen **suggesties** met GET of POST.</span><span class="sxs-lookup"><span data-stu-id="943ec-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="943ec-1122">**Aanvraagheaders**</span><span class="sxs-lookup"><span data-stu-id="943ec-1122">**Request Headers**</span></span>

<span data-ttu-id="943ec-1123">Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="943ec-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="943ec-1124">`api-key`: Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is.</span><span class="sxs-lookup"><span data-stu-id="943ec-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="943ec-1125">Het is een tekenreekswaarde, unieke tooyour service-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="943ec-1126">Hallo **suggesties** aanvraag een beheersleutel of een querysleutel kunt opgeven als Hallo `api-key`.</span><span class="sxs-lookup"><span data-stu-id="943ec-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="943ec-1127">U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="943ec-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="943ec-1128">U krijgt de naam van de service Hallo en `api-key` van uw servicedashboard in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="943ec-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="943ec-1129">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.</span><span class="sxs-lookup"><span data-stu-id="943ec-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="943ec-1130">**Aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="943ec-1130">**Request Body**</span></span>

<span data-ttu-id="943ec-1131">Voor GET: geen.</span><span class="sxs-lookup"><span data-stu-id="943ec-1131">For GET: None.</span></span>

<span data-ttu-id="943ec-1132">Voor POST:</span><span class="sxs-lookup"><span data-stu-id="943ec-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="943ec-1133">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="943ec-1133">**Response**</span></span>

<span data-ttu-id="943ec-1134">Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="943ec-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="943ec-1135">Als Hallo projectie optie gebruikte tooretrieve velden die zijn opgenomen in elk element van Hallo matrix:</span><span class="sxs-lookup"><span data-stu-id="943ec-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="943ec-1136">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="943ec-1136">**Example**</span></span>

<span data-ttu-id="943ec-1137">5 suggesties waarbij Hallo deelzoekopdrachten invoer is 'lux' ophalen</span><span class="sxs-lookup"><span data-stu-id="943ec-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
