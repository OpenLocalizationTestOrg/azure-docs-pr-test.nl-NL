---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: Voorlopige documentatie voor Hallo synoniemen (preview)-functie, worden weergegeven in hello Azure Search REST-API.
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="7a2ce-102">Synoniemen in Azure Search (preview)</span><span class="sxs-lookup"><span data-stu-id="7a2ce-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="7a2ce-103">Synoniemen in zoekmachines koppelen gelijkwaardige termen die impliciet Vouw Hallo bereik van een query zonder Hallo gebruiker tooactually Hallo term bieden.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="7a2ce-104">Bijvoorbeeld vallen bepaalde Hallo term 'aquaduct' en synoniem koppelingen van 'hondachtige' en 'puppy', alle documenten met 'aquaduct', 'hondachtige' of 'puppy' binnen Hallo bereik van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="7a2ce-105">In Azure Search wordt synoniem uitbreiding uitgevoerd op moment dat de query.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="7a2ce-106">U kunt synoniem maps tooa service niets onderbreking van de tooexisting bewerkingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="7a2ce-107">U kunt toevoegen een **synonymMaps** tooa veld eigenschapdefinitie zonder toorebuild Hallo index.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="7a2ce-108">Zie voor meer informatie [Index bijwerken](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="7a2ce-109">Beschikbaarheid van functies</span><span class="sxs-lookup"><span data-stu-id="7a2ce-109">Feature availability</span></span>

<span data-ttu-id="7a2ce-110">Hallo-synoniemen functie is momenteel in preview en alleen ondersteund de meest recente preview-api-versie Hallo (api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="7a2ce-111">Azure Portal biedt er momenteel geen ondersteuning voor.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="7a2ce-112">Omdat Hallo API-versie op Hallo-aanvraag is opgegeven, is het mogelijk toocombine algemeen beschikbaar (GA) en de preview-API's in Hallo dezelfde app.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="7a2ce-113">Preview-API's niet onder de SERVICEOVEREENKOMST en de functies zijn kan echter wel wijzigen, zodat u kunt beter niet met deze in productietoepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="7a2ce-114">Hoe toouse synoniemen in Azure zoeken</span><span class="sxs-lookup"><span data-stu-id="7a2ce-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="7a2ce-115">In Azure Search is synoniem ondersteuning gebaseerd op synoniem maps dat u definieert en tooyour service uploaden.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="7a2ce-116">Deze toewijzingen deel uitmaken van een onafhankelijke resource (zoals indexen of gegevensbronnen) en kunnen worden gebruikt door een doorzoekbaar veld in een index in uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="7a2ce-117">Synoniem toegewezen en indexen onafhankelijk worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="7a2ce-118">Zodra u een kaart synoniem definiëren en upload het tooyour service, kunt u Hallo synoniem functie op een veld inschakelen door een nieuwe eigenschap toe te voegen **synonymMaps** in Hallo velddefinitie.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="7a2ce-119">Maken, bijwerken en verwijderen van die een synoniem-kaart altijd een hele document-bewerking is, wat betekent dat u geen maken, bijwerken of delen van Hallo synoniem kaart incrementeel te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="7a2ce-120">Zelfs een afzonderlijke vermelding bijwerken vereist een opnieuw laden.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="7a2ce-121">Synoniemen opnemen in uw toepassing search is een proces in twee stappen:</span><span class="sxs-lookup"><span data-stu-id="7a2ce-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="7a2ce-122">Toevoegen van een synoniem kaart tooyour search-service via Hallo onderstaande API's.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="7a2ce-123">Configureer een doorzoekbare toouse Hallo synoniem veldtoewijzing in Hallo indexdefinitie.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="7a2ce-124">SynonymMaps Resource API 's</span><span class="sxs-lookup"><span data-stu-id="7a2ce-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="7a2ce-125">Toevoegen of bijwerken van een kaart synoniem onder uw service en met behulp van posten of te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="7a2ce-126">Synoniem maps worden geüpload toohello service via POST of PUT.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="7a2ce-127">Elke regel moet worden gevolgd door een nieuwe regelteken hello (\n).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="7a2ce-128">U kunt definiëren van too5, 000 regels per synoniem kaart in een gratis service en 10.000 regels in andere SKU's.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="7a2ce-129">Elke regel kan van too20 uitbreidingen hebben.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="7a2ce-130">In dit voorbeeld moet synoniem maps Hallo Apache Solr indeling die hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="7a2ce-131">Als u een bestaande synoniem woordenlijst in een andere indeling en toouse wilt deze rechtstreeks laat ons weten op [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="7a2ce-132">U kunt een nieuwe synoniem-toewijzing met behulp van HTTP POST, zoals in het volgende voorbeeld Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="7a2ce-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="7a2ce-133">U kunt ook gebruik van PUT en Hallo synoniem toewijzingsnaam op Hallo URI opgeven.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="7a2ce-134">Als Hallo synoniem kaart niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="7a2ce-135">Apache Solr synoniem indeling</span><span class="sxs-lookup"><span data-stu-id="7a2ce-135">Apache Solr synonym format</span></span>

<span data-ttu-id="7a2ce-136">Hallo Solr indeling ondersteunt gelijkwaardige en expliciete synoniem toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="7a2ce-137">Regels voor apparaatgroeptoewijzing voldoen toohello open-source synoniem filterspecificatie van Apache Solr, in dit document beschreven: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="7a2ce-138">Hieronder volgt een voorbeeldregel voor de equivalente synoniemen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="7a2ce-139">Met de Hallo regel hierboven, zoeken query 'VS' te vergroten 'VS' of 'Verenigde Staten' of 'Verenigde Staten van Amerika'.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="7a2ce-140">Expliciete toewijzing wordt aangeduid met een pijl ' = > '.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="7a2ce-141">Als u opgeeft, een reeks termijn van een zoekopdracht die overeenkomt met de Hallo linkerzijde van ' = > ' wordt vervangen door Hallo alternatieven aan de rechterkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="7a2ce-142">Hallo regel onderstaande gezien, zoekquery's 'Washington', 'Staat Washington'</span><span class="sxs-lookup"><span data-stu-id="7a2ce-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="7a2ce-143">of "WA" alle herschreven te "WA".</span><span class="sxs-lookup"><span data-stu-id="7a2ce-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="7a2ce-144">Expliciete toewijzing alleen van toepassing is in de opgegeven Hallo richting en herschrijven Hallo query "WA" niet te 'Washington' in dit geval.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="7a2ce-145">Lijst synoniem maps onder uw service.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="7a2ce-146">Een kaart synoniem onder uw service ophalen.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="7a2ce-147">Verwijderen van een kaart synoniemen onder uw service.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="7a2ce-148">Configureer een doorzoekbare toouse Hallo synoniem veldtoewijzing in Hallo indexdefinitie.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="7a2ce-149">De eigenschap van een nieuw veld **synonymMaps** mag gebruikte toospecify een synoniem kaart toouse voor een doorzoekbaar veld.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="7a2ce-150">Synoniem maps service level bronnen en kunnen worden verwezen vanuit elk veld van een index onder Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="7a2ce-151">**synonymMaps** kan worden opgegeven voor de doorzoekbare velden van het Hallo-type 'Edm.String' of 'Verzameling (EDM.String)'.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="7a2ce-152">In dit voorbeeld, kunt u slechts één synoniem toewijzen per veld hebben.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="7a2ce-153">Als u meerdere synoniem maps toouse wilt, laat ons weten op [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="7a2ce-154">Gevolgen van synoniemen voor andere zoekfuncties</span><span class="sxs-lookup"><span data-stu-id="7a2ce-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="7a2ce-155">Hallo synoniemen functie herschrijft Hallo oorspronkelijke query met synoniemen Hello OR-operator.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="7a2ce-156">Om deze reden behandelen treffers syntaxismarkering en -profielen scoren de oorspronkelijke termijn Hallo en synoniemen als equivalent.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="7a2ce-157">Synoniem functie toosearch query's van toepassing is en is niet van toepassing toofilters of facetten.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="7a2ce-158">Op deze manier worden suggesties alleen gebaseerd op de oorspronkelijke termijn Hallo; synoniem overeenkomsten worden niet weergegeven in het Hallo-antwoord.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="7a2ce-159">Synoniem uitbreidingen zijn niet van toepassing toowildcard zoektermen; voorvoegsel, bij benadering, en de regex-voorwaarden worden niet aangevuld.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="7a2ce-160">Tips voor het bouwen van een synoniem-kaart</span><span class="sxs-lookup"><span data-stu-id="7a2ce-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="7a2ce-161">Een beknopte, goed ontworpen synoniem-kaart is efficiënter dan een volledige lijst van mogelijke overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="7a2ce-162">Uitzonderlijk groot of complex woordenlijsten langer tooparse nemen en van invloed zijn op Hallo Querylatentie als Hallo query toomany synoniemen wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="7a2ce-163">In plaats van de schatting waarmee voorwaarden kunnen worden gebruikt, kunt u de werkelijke voorwaarden Hallo via krijgen een [verkeer analyserapport zoeken](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="7a2ce-164">Als een inleiding en de validatie oefening inschakelen en vervolgens gebruik dit rapport tooprecisely bepalen welke voorwaarden profiteren van een overeenkomst synoniem en ga vervolgens verder met toouse als validatie van de kaart synoniem opstellen van een beter resultaat.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="7a2ce-165">Hallo vooraf gedefinieerd rapport, tegels Hallo 'meest algemene zoekquery's ' en 'nul resultaat zoekquery's ', krijgt u Hallo benodigde informatie.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="7a2ce-166">U kunt meerdere synoniem toewijzingen maken voor uw zoektoepassing (bijvoorbeeld per taal als de toepassing meerdere talen van de klant base ondersteunt).</span><span class="sxs-lookup"><span data-stu-id="7a2ce-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="7a2ce-167">Een veld kunt een van beide op dit moment alleen kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="7a2ce-168">U kunt de eigenschap synonymMaps van een veld op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a2ce-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a2ce-169">Next Steps</span></span>

- <span data-ttu-id="7a2ce-170">Als u een bestaande index in een ontwikkelomgeving (niet-productieve) hebt, experimenteren met een kleine woordenlijst toosee hoe Hallo toevoeging van synoniemen Hallo zoekervaring, met inbegrip van de gevolgen voor score berekenen voor profielen, treffers markeringen en suggesties verandert.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="7a2ce-171">[Inschakelen van search traffic analytics](search-traffic-analytics.md) en gebruik Hallo vooraf gedefinieerde Power BI-rapport toolearn welke termen worden gebruikt Hallo meeste en welke waarden retourneren nul documenten.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="7a2ce-172">. Met deze inzichten worden herzien Hallo woordenlijst tooinclude synoniemen voor niet-productieve query's die moeten worden het omzetten van toodocuments in uw index.</span><span class="sxs-lookup"><span data-stu-id="7a2ce-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
