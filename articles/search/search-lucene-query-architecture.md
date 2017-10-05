---
title: Volledige tekst zoeken (Lucene)-engine-architectuur in Azure Search | Microsoft Docs
description: Uitleg van de Lucene query verwerking en document ophalen concepten voor zoeken in volledige tekst, met betrekking tot de Azure Search.
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: 9b7adf78271407963ed1d4b34a7760d707b5fc3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="b3094-103">Hoe vol tekst zoeken werkt in Azure Search</span><span class="sxs-lookup"><span data-stu-id="b3094-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="b3094-104">Dit artikel is voor ontwikkelaars die u een beter begrip moeten van de werking van Lucene zoeken in volledige tekst in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b3094-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="b3094-105">Voor tekst-query's, Azure Search naadloos verwachte resultaten in de meeste gevallen levert, maar soms mogelijk krijgt u een resultaat enigszins lijkt "off".</span><span class="sxs-lookup"><span data-stu-id="b3094-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="b3094-106">In deze situaties als zich een achtergrond op de vier fasen van de queryuitvoering Lucene (query parseren, lexicale analyse, document-koppeling, score berekenen) kunt u specifieke wijzigingen in queryparameters of de indexconfiguratie van de die het gewenste resultaat levert te identificeren.</span><span class="sxs-lookup"><span data-stu-id="b3094-106">In these situations, having a background in the four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes to query parameters or index configuration that will deliver the desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="b3094-107">Azure Search Lucene gebruikt voor zoekopdrachten in volledige tekst, maar Lucene-integratie is niet volledig.</span><span class="sxs-lookup"><span data-stu-id="b3094-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="b3094-108">We selectief weergeven en Lucene uitbreiden zodat de naar Azure Search belangrijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="b3094-108">We selectively expose and extend Lucene functionality to enable the scenarios important to Azure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="b3094-109">Overzicht van de architectuur en diagram</span><span class="sxs-lookup"><span data-stu-id="b3094-109">Architecture overview and diagram</span></span>

<span data-ttu-id="b3094-110">Verwerking van een zoekopdracht voor volledige tekst begint met het parseren van de querytekst om uit te pakken zoektermen.</span><span class="sxs-lookup"><span data-stu-id="b3094-110">Processing a full text search query starts with parsing the query text to extract search terms.</span></span> <span data-ttu-id="b3094-111">De zoekmachine maakt gebruik van een index ophalen van documenten met overeenkomende voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="b3094-111">The search engine uses an index to retrieve documents with matching terms.</span></span> <span data-ttu-id="b3094-112">Afzonderlijke querytermen zijn soms uitgesplitst en in nieuwe formulieren voor het casten van een bredere net over wat kan worden beschouwd als een mogelijke overeenkomst geregenereerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-112">Individual query terms are sometimes broken down and reconstituted into new forms to cast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="b3094-113">Geen resultatenset is vervolgens gesorteerd op een toegewezen aan elk document dat overeenkomende afzonderlijke relevantie-score.</span><span class="sxs-lookup"><span data-stu-id="b3094-113">A result set is then sorted by a relevance score assigned to each individual matching document.</span></span> <span data-ttu-id="b3094-114">Die aan de bovenkant van de ranglijst worden teruggestuurd naar de aanroepende toepassing.</span><span class="sxs-lookup"><span data-stu-id="b3094-114">Those at the top of the ranked list are returned to the calling application.</span></span>

<span data-ttu-id="b3094-115">Aangepast, bestaat uitvoering van de query uit vier fasen:</span><span class="sxs-lookup"><span data-stu-id="b3094-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="b3094-116">Query bij het parseren van</span><span class="sxs-lookup"><span data-stu-id="b3094-116">Query parsing</span></span> 
2. <span data-ttu-id="b3094-117">Lexicale analyse</span><span class="sxs-lookup"><span data-stu-id="b3094-117">Lexical analysis</span></span> 
3. <span data-ttu-id="b3094-118">Document ophalen</span><span class="sxs-lookup"><span data-stu-id="b3094-118">Document retrieval</span></span> 
4. <span data-ttu-id="b3094-119">Score berekenen</span><span class="sxs-lookup"><span data-stu-id="b3094-119">Scoring</span></span> 

<span data-ttu-id="b3094-120">Het volgende diagram illustreert de onderdelen die wordt gebruikt voor het verwerken van een zoekaanvraag.</span><span class="sxs-lookup"><span data-stu-id="b3094-120">The diagram below illustrates the components used to process a search request.</span></span> 

 ![Architectuurdiagram van de Lucene-query in Azure Search][1]


| <span data-ttu-id="b3094-122">Belangrijkste onderdelen</span><span class="sxs-lookup"><span data-stu-id="b3094-122">Key components</span></span> | <span data-ttu-id="b3094-123">Functionele beschrijving</span><span class="sxs-lookup"><span data-stu-id="b3094-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="b3094-124">**Query parsers**</span><span class="sxs-lookup"><span data-stu-id="b3094-124">**Query parsers**</span></span> | <span data-ttu-id="b3094-125">Afzonderlijke querytermen van query's en de querystructuur (een querystructuur) worden verzonden naar de zoekmachine maken.</span><span class="sxs-lookup"><span data-stu-id="b3094-125">Separate query terms from query operators and create the query structure (a query tree) to be sent to the search engine.</span></span> |
|<span data-ttu-id="b3094-126">**Analyzers**</span><span class="sxs-lookup"><span data-stu-id="b3094-126">**Analyzers**</span></span> | <span data-ttu-id="b3094-127">Lexicale analyse uitvoeren op querytermen.</span><span class="sxs-lookup"><span data-stu-id="b3094-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="b3094-128">Dit proces kan betrekking hebben op transformeren, te verwijderen of uitbreiden van de voorwaarden van de query.</span><span class="sxs-lookup"><span data-stu-id="b3094-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="b3094-129">**Index**</span><span class="sxs-lookup"><span data-stu-id="b3094-129">**Index**</span></span> | <span data-ttu-id="b3094-130">Een efficiënte gegevensstructuur op te slaan en te organiseren doorzoekbare voorwaarden opgehaald uit de geïndexeerde documenten.</span><span class="sxs-lookup"><span data-stu-id="b3094-130">An efficient data structure used to store and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="b3094-131">**Zoekmachine**</span><span class="sxs-lookup"><span data-stu-id="b3094-131">**Search engine**</span></span> | <span data-ttu-id="b3094-132">Haalt en scores overeenkomende documenten op basis van de inhoud van de omgekeerde index.</span><span class="sxs-lookup"><span data-stu-id="b3094-132">Retrieves and scores matching documents based on the contents of the inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="b3094-133">Anatomie van een zoekaanvraag</span><span class="sxs-lookup"><span data-stu-id="b3094-133">Anatomy of a search request</span></span>

<span data-ttu-id="b3094-134">Een zoekaanvraag is een complete specificatie van wat moet worden geretourneerd in een resultatenset.</span><span class="sxs-lookup"><span data-stu-id="b3094-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="b3094-135">In de meest eenvoudige vorm is een lege query zonder criteria alle soorten.</span><span class="sxs-lookup"><span data-stu-id="b3094-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="b3094-136">Een voorbeeld van een meer realistische bevat parameters, verschillende querytermen, mogelijk binnen het bereik van bepaalde velden, met mogelijk een filterexpressie en ordening van regels.</span><span class="sxs-lookup"><span data-stu-id="b3094-136">A more realistic example includes parameters, several query terms, perhaps scoped to certain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="b3094-137">Het volgende voorbeeld wordt een zoekaanvraag u verzenden naar Azure Search met behulp van mogelijk de [REST-API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="b3094-137">The following example is a search request you might send to Azure Search using the [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

<span data-ttu-id="b3094-138">Voor deze aanvraag zijn de zoekmachine doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="b3094-138">For this request, the search engine does the following:</span></span>

1. <span data-ttu-id="b3094-139">Documenten gefilterd waar de prijs is ten minste $60 en minder dan 300 $.</span><span class="sxs-lookup"><span data-stu-id="b3094-139">Filters out documents where the price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="b3094-140">De query worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-140">Executes the query.</span></span> <span data-ttu-id="b3094-141">In dit voorbeeld wordt de zoekopdracht bestaat uit zinnen en voorwaarden: `"Spacious, air-condition* +\"Ocean view\""` (gebruikers doorgaans niet leestekens in te voeren, maar dit op te nemen in het voorbeeld, kunnen wij waarin wordt uitgelegd hoe analyzers verwerkt; het).</span><span class="sxs-lookup"><span data-stu-id="b3094-141">In this example, the search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in the example allows us to explain how analyzers handle it).</span></span> <span data-ttu-id="b3094-142">Voor deze query scant het zoekprogramma de beschrijving en titelvelden opgegeven in `searchFields` voor documenten die 'Oceaan weergave' bevatten en ook op de term 'groot', of op voorwaarden die met het voorvoegsel beginnen 'air-condition'.</span><span class="sxs-lookup"><span data-stu-id="b3094-142">For this query, the search engine scans the description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on the term "spacious", or on terms that start with the prefix "air-condition".</span></span> <span data-ttu-id="b3094-143">De `searchMode` parameter wordt gebruikt op een term (standaard) of al deze gevallen waarbij een term niet expliciet hoeft (`+`).</span><span class="sxs-lookup"><span data-stu-id="b3094-143">The `searchMode` parameter is used to match on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="b3094-144">Hiermee worden de resulterende set hotels door nabijheid tot een opgegeven geografische locatie en vervolgens wordt geretourneerd naar de aanroepende toepassing gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="b3094-144">Orders the resulting set of hotels by proximity to a given geography location, and then returned to the calling application.</span></span> 

<span data-ttu-id="b3094-145">Het merendeel van dit artikel gaat over de verwerking van de *zoekquery*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="b3094-145">The majority of this article is about processing of the *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="b3094-146">Filteren en ordening vallen buiten het bereik.</span><span class="sxs-lookup"><span data-stu-id="b3094-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="b3094-147">Zie voor meer informatie de [zoeken-API-naslagdocumentatie](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="b3094-147">For more information, see the [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="b3094-148">Stap 1: Een Query bij het parseren van</span><span class="sxs-lookup"><span data-stu-id="b3094-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="b3094-149">Zoals vermeld, is de queryreeks in de eerste regel van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="b3094-149">As noted, the query string is the first line of the request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="b3094-150">De queryparser scheidt operators (zoals `*` en `+` in het voorbeeld) in een zoekvak voorwaarden en de query in deconstructs *subquery's* met een ondersteund type:</span><span class="sxs-lookup"><span data-stu-id="b3094-150">The query parser separates operators (such as `*` and `+` in the example) from search terms, and deconstructs the search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="b3094-151">*term query* voor zelfstandige voorwaarden (zoals groot)</span><span class="sxs-lookup"><span data-stu-id="b3094-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="b3094-152">*woordgroep query* voor tussen aanhalingstekens voorwaarden (zoals Oceaan weergave)</span><span class="sxs-lookup"><span data-stu-id="b3094-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="b3094-153">*voorvoegsel query* voor voorwaarden gevolgd door een operator voorvoegsel `*` (zoals air-condition)</span><span class="sxs-lookup"><span data-stu-id="b3094-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="b3094-154">Zie voor een volledige lijst met ondersteunde querytypen [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="b3094-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="b3094-155">Operators die zijn gekoppeld aan een subquery bepalen of de query 'moet' of 'moet' voldaan voordat een document om te worden beschouwd als een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="b3094-155">Operators associated with a subquery determine whether the query "must be" or "should be" satisfied in order for a document to be considered a match.</span></span> <span data-ttu-id="b3094-156">Bijvoorbeeld: `+"Ocean view"` 'moet' is vanwege de `+` operator.</span><span class="sxs-lookup"><span data-stu-id="b3094-156">For example, `+"Ocean view"` is "must" due to the `+` operator.</span></span> 

<span data-ttu-id="b3094-157">De queryparser worden opnieuw gestructureerd de subquery's in een *querystructuur* (een interne structuur voor de query) dit wordt doorgegeven op naar de zoekmachine.</span><span class="sxs-lookup"><span data-stu-id="b3094-157">The query parser restructures the subqueries into a *query tree* (an internal structure representing the query) it passes on to the search engine.</span></span> <span data-ttu-id="b3094-158">In de eerste fase van het parseren van de query uitziet de querystructuur van de.</span><span class="sxs-lookup"><span data-stu-id="b3094-158">In the first stage of query parsing, the query tree looks like this.</span></span>  

 ![Booleaanse waarde searchmode ieder query][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="b3094-160">Ondersteund parsers: eenvoudig en volledige Lucene</span><span class="sxs-lookup"><span data-stu-id="b3094-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="b3094-161">Azure Search beschrijft de twee andere querytalen `simple` (standaard) en `full`.</span><span class="sxs-lookup"><span data-stu-id="b3094-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="b3094-162">Door in te stellen de `queryType` parameter bij uw zoekaanvraag, geeft u aan de queryparser welke querytaal gewenst zodat deze het interpreteren van de operators en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="b3094-162">By setting the `queryType` parameter with your search request, you tell the query parser which query language you choose so that it knows how to interpret the operators and syntax.</span></span> <span data-ttu-id="b3094-163">De [eenvoudige query taal](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuïtieve en robuuste, vaak geschikte gebruikersinvoer als interpreteren-is zonder dat de verwerking van de clientzijde.</span><span class="sxs-lookup"><span data-stu-id="b3094-163">The [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable to interpret user input as-is without client-side processing.</span></span> <span data-ttu-id="b3094-164">Biedt ondersteuning voor query's van webzoekmachines bekend.</span><span class="sxs-lookup"><span data-stu-id="b3094-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="b3094-165">De [volledige Lucene-querytaal](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), die wordt geleverd door in te stellen `queryType=full`, wordt de standaardtaal voor eenvoudige query uitgebreid met ondersteuning voor meer operators en querytypen zoals jokerteken, bij benadering, regex en veldgerelateerde query's.</span><span class="sxs-lookup"><span data-stu-id="b3094-165">The [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends the default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="b3094-166">Bijvoorbeeld, wordt een reguliere expressie in vereenvoudigde querysyntaxis verzonden geïnterpreteerd als een queryreeks bevat en niet een expressie.</span><span class="sxs-lookup"><span data-stu-id="b3094-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="b3094-167">De voorbeeldaanvraag in dit artikel maakt gebruik van de volledige Lucene-querytaal.</span><span class="sxs-lookup"><span data-stu-id="b3094-167">The example request in this article uses the Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-the-parser"></a><span data-ttu-id="b3094-168">Gevolgen van het searchMode in de parser</span><span class="sxs-lookup"><span data-stu-id="b3094-168">Impact of searchMode on the parser</span></span> 

<span data-ttu-id="b3094-169">Een andere aanvraag zoekparameter die gevolgen heeft voor het parseren is de `searchMode` parameter.</span><span class="sxs-lookup"><span data-stu-id="b3094-169">Another search request parameter that affects parsing is the `searchMode` parameter.</span></span> <span data-ttu-id="b3094-170">Hiermee kunt u de standaardoperator voor Boole-query's: een (standaard) of alle.</span><span class="sxs-lookup"><span data-stu-id="b3094-170">It controls the default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="b3094-171">Wanneer `searchMode=any`, die is de standaardinstelling en de spatie als scheidingsteken tussen groot en air-condition is of (`||`), zodat de tekst van de query voorbeeld gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="b3094-171">When `searchMode=any`, which is the default, the space delimiter between spacious and air-condition is OR (`||`), making the sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="b3094-172">Expliciete operators, zoals `+` in `+"Ocean view"`, zijn niet-ambigue Booleaanse query constructie (de term *moet* overeen).</span><span class="sxs-lookup"><span data-stu-id="b3094-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (the term *must* match).</span></span> <span data-ttu-id="b3094-173">Minder duidelijk is het interpreteren van de overige voorwaarden: groot en air-condition.</span><span class="sxs-lookup"><span data-stu-id="b3094-173">Less obvious is how to interpret the remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="b3094-174">Moet de zoekmachine overeenkomsten vinden voor de weergave Oceaan *en* groot *en* air-condition?</span><span class="sxs-lookup"><span data-stu-id="b3094-174">Should the search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="b3094-175">Of moet Oceaan weergave vinden plus *een* van de overige voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="b3094-175">Or should it find ocean view plus *either one* of the remaining terms?</span></span> 

<span data-ttu-id="b3094-176">Standaard (`searchMode=any`), de zoekmachine wordt ervan uitgegaan dat de breder interpretatie.</span><span class="sxs-lookup"><span data-stu-id="b3094-176">By default (`searchMode=any`), the search engine assumes the broader interpretation.</span></span> <span data-ttu-id="b3094-177">Een veld *moet* overeenkomen, opgetreden bij het weergeven 'of' semantiek.</span><span class="sxs-lookup"><span data-stu-id="b3094-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="b3094-178">De structuur van de eerste query eerder geïllustreerd, met de twee 'moet' bewerkingen, ziet u de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="b3094-178">The initial query tree illustrated previously, with the two "should" operations, shows the default.</span></span>  

<span data-ttu-id="b3094-179">Stel dat we nu `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="b3094-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="b3094-180">In dit geval wordt wordt de ruimte geïnterpreteerd als een 'en'-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b3094-180">In this case, the space is interpreted as an "and" operation.</span></span> <span data-ttu-id="b3094-181">Elk van de overige voorwaarden zijn beide aanwezig in het document in aanmerking wilt komen als een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="b3094-181">Each of the remaining terms must both be present in the document to qualify as a match.</span></span> <span data-ttu-id="b3094-182">De resulterende voorbeeldquery wordt geïnterpreteerd als volgt:</span><span class="sxs-lookup"><span data-stu-id="b3094-182">The resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="b3094-183">Een boomstructuur gewijzigde query voor deze query zou zijn als volgt, waarbij een overeenkomende document is het snijpunt van alle drie subquery's:</span><span class="sxs-lookup"><span data-stu-id="b3094-183">A modified query tree for this query would be as follows, where a matching document is the intersection of all three subqueries:</span></span> 

 ![Booleaanse query searchmode alle][3]

> [!Note] 
> <span data-ttu-id="b3094-185">Kiezen `searchMode=any` via `searchMode=all` is een beste beslissing ontvangen op door het uitvoeren van representatieve query's.</span><span class="sxs-lookup"><span data-stu-id="b3094-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="b3094-186">Gebruikers die waarschijnlijk ook operators (algemeen zijn wanneer zoeken document opslaat) wellicht resultaten intuïtievere als `searchMode=all` informeert Booleaanse query constructies.</span><span class="sxs-lookup"><span data-stu-id="b3094-186">Users who are likely to include operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="b3094-187">Voor meer informatie over de wisselwerking tussen `searchMode` en operators, Zie [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="b3094-187">For more about the interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="b3094-188">Stap 2: Lexicale analyse</span><span class="sxs-lookup"><span data-stu-id="b3094-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="b3094-189">Lexicale analyzers proces *benaming query's* en *woorden van query's* nadat de structuur van de querystructuur van de.</span><span class="sxs-lookup"><span data-stu-id="b3094-189">Lexical analyzers process *term queries* and *phrase queries* after the query tree is structured.</span></span> <span data-ttu-id="b3094-190">Een analyzer tekst invoerwaarden krijgen tot het door de parser accepteert, verwerkt de tekst en klikt u vervolgens verzendt terug tokenized voorwaarden om te worden opgenomen in de querystructuur van de.</span><span class="sxs-lookup"><span data-stu-id="b3094-190">An analyzer accepts the text inputs given to it by the parser, processes the text, and then sends back tokenized terms to be incorporated into the query tree.</span></span> 

<span data-ttu-id="b3094-191">De meest voorkomende vorm van lexicale analyse is *taalkundige analysis* welke transformaties query voorwaarden op basis van regels die specifiek zijn voor een bepaalde taal:</span><span class="sxs-lookup"><span data-stu-id="b3094-191">The most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific to a given language:</span></span> 

* <span data-ttu-id="b3094-192">Een zoekterm voor het root-formulier van een woord te beperken</span><span class="sxs-lookup"><span data-stu-id="b3094-192">Reducing a query term to the root form of a word</span></span> 
* <span data-ttu-id="b3094-193">Verwijderen van niet-essentiële woorden (stopwoorden, zoals 'het' of 'en' in het Engels)</span><span class="sxs-lookup"><span data-stu-id="b3094-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="b3094-194">Een samengestelde woord in onderdelen op te splitsen</span><span class="sxs-lookup"><span data-stu-id="b3094-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="b3094-195">Kleine hoofdlettergebruik van een woord hoofdletters</span><span class="sxs-lookup"><span data-stu-id="b3094-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="b3094-196">Al deze bewerkingen vaak verschillen tussen de ingevoerde tekst door de gebruiker en de voorwaarden die zijn opgeslagen in de index wilt wissen.</span><span class="sxs-lookup"><span data-stu-id="b3094-196">All of these operations tend to erase differences between the text input provided by the user and the terms stored in the index.</span></span> <span data-ttu-id="b3094-197">Dergelijke bewerkingen voorbij de verwerking van tekst en vereisen diepgaande kennis van de taal zelf.</span><span class="sxs-lookup"><span data-stu-id="b3094-197">Such operations go beyond text processing and require in-depth knowledge of the language itself.</span></span> <span data-ttu-id="b3094-198">Als u wilt toevoegen in deze laag van de taalkundige awareness, Azure Search biedt ondersteuning voor een lange lijst met [taalanalyse](https://docs.microsoft.com/rest/api/searchservice/language-support) van Lucene en van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b3094-198">To add this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="b3094-199">Vereisten voor de analyse kunnen variëren van minimale tot uitgebreide afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="b3094-199">Analysis requirements can range from minimal to elaborate depending on your scenario.</span></span> <span data-ttu-id="b3094-200">U kunt de complexiteit van lexicale analyse beheren door het selecteren van de vooraf gedefinieerde analyzers of door het maken van uw eigen [aangepaste analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="b3094-200">You can control complexity of lexical analysis by the selecting one of the predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="b3094-201">Analyzers zijn gericht op de doorzoekbare velden en zijn opgegeven als onderdeel van de velddefinitie van een.</span><span class="sxs-lookup"><span data-stu-id="b3094-201">Analyzers are scoped to searchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="b3094-202">Hiermee kunt u lexicale analyse op basis van veld per variëren.</span><span class="sxs-lookup"><span data-stu-id="b3094-202">This allows you to vary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="b3094-203">Niet is opgegeven, de *standaard* Lucene analyzer wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3094-203">Unspecified, the *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="b3094-204">In ons voorbeeld vóór analyse, heeft de structuur van de eerste query de term 'Spacious' met een hoofdletter "S" en een komma, die de queryparser wordt geïnterpreteerd als een deel van de zoekterm (een door komma's wordt niet beschouwd als een query language-operator).</span><span class="sxs-lookup"><span data-stu-id="b3094-204">In our example, prior to analysis, the initial query tree has the term "Spacious," with an uppercase "S" and a comma that the query parser interprets as a part of the query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="b3094-205">Wanneer de standaard analyzer de term verwerkt, wordt deze kleine letters 'Oceaan weergeven' en 'groot' en verwijder het teken met door komma's.</span><span class="sxs-lookup"><span data-stu-id="b3094-205">When the default analyzer processes the term, it will lowercase "ocean view" and "spacious", and remove the comma character.</span></span> <span data-ttu-id="b3094-206">De gewijzigde query-structuur ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b3094-206">The modified query tree will look as follows:</span></span> 

 ![Booleaanse query geanalyseerde voorwaarden][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="b3094-208">Analyzer gedrag testen</span><span class="sxs-lookup"><span data-stu-id="b3094-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="b3094-209">Het gedrag van een analyzer kan worden getest met de [analyseren API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="b3094-209">The behavior of an analyzer can be tested using the [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="b3094-210">Geef de tekst die u wilt analyseren om te zien wat vermeldingen analyzer wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-210">Provide the text you want to analyze to see what terms given analyzer will generate.</span></span> <span data-ttu-id="b3094-211">Als u wilt zien hoe de standaard analyzer zou de tekst 'air-condition' verwerken, kunt u bijvoorbeeld de volgende aanvraag uitgeven:</span><span class="sxs-lookup"><span data-stu-id="b3094-211">For example, to see how the standard analyzer would process the text "air-condition", you can issue the following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="b3094-212">De standaard analyzer verdeelt de ingevoerde tekst in de volgende twee tokens aantekeningen te maken met kenmerken zoals begin en einde offsets (gebruikt voor het markeren van treffers), evenals hun positie (gebruikt voor de zinsnede overeenkomende):</span><span class="sxs-lookup"><span data-stu-id="b3094-212">The standard analyzer breaks the input text into the following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-to-lexical-analysis"></a><span data-ttu-id="b3094-213">Uitzonderingen op lexicale analyse</span><span class="sxs-lookup"><span data-stu-id="b3094-213">Exceptions to lexical analysis</span></span> 

<span data-ttu-id="b3094-214">Lexicale analysis geldt alleen voor querytypen waarvoor volledige voorwaarden – een term query of een woordgroep-query.</span><span class="sxs-lookup"><span data-stu-id="b3094-214">Lexical analysis applies only to query types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="b3094-215">Het is niet van toepassing op querytypen met onvolledige voorwaarden – voorvoegsel query, jokertekens query, regex query – of op een fuzzy query.</span><span class="sxs-lookup"><span data-stu-id="b3094-215">It doesn’t apply to query types with incomplete terms – prefix query, wildcard query, regex query – or to a fuzzy query.</span></span> <span data-ttu-id="b3094-216">De querytypen, met inbegrip van de query voorvoegsel met de term *air-condition\**  in ons voorbeeld rechtstreeks aan de querystructuur, het omzeilen van de analyse-fase worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b3094-216">Those query types, including the prefix query with term *air-condition\** in our example, are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="b3094-217">De enige transformatie die wordt uitgevoerd op de voorwaarden van deze typen query is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="b3094-217">The only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="b3094-218">Stap 3: Document ophalen</span><span class="sxs-lookup"><span data-stu-id="b3094-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="b3094-219">Ophalen van het document verwijst naar het zoeken van documenten met die overeenkomt met de voorwaarden in de index.</span><span class="sxs-lookup"><span data-stu-id="b3094-219">Document retrieval refers to finding documents with matching terms in the index.</span></span> <span data-ttu-id="b3094-220">Deze fase is beste begrepen door een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b3094-220">This stage is understood best through an example.</span></span> <span data-ttu-id="b3094-221">Laten we beginnen met een index hotels met de volgende eenvoudige schema:</span><span class="sxs-lookup"><span data-stu-id="b3094-221">Let's start with a hotels index having the following simple schema:</span></span> 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

<span data-ttu-id="b3094-222">Verder wordt ervan uitgegaan dat deze index de volgende vier documenten bevat:</span><span class="sxs-lookup"><span data-stu-id="b3094-222">Further assume that this index contains the following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance to the beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on the north shore of the island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

<span data-ttu-id="b3094-223">**Hoe voorwaarden worden geïndexeerd**</span><span class="sxs-lookup"><span data-stu-id="b3094-223">**How terms are indexed**</span></span>

<span data-ttu-id="b3094-224">Het helpt om te begrijpen ophalen, te weten van enkele basisbeginselen van het indexeren.</span><span class="sxs-lookup"><span data-stu-id="b3094-224">To understand retrieval, it helps to know a few basics about indexing.</span></span> <span data-ttu-id="b3094-225">De eenheid voor opslag is een omgekeerde index, één voor elk doorzoekbaar veld.</span><span class="sxs-lookup"><span data-stu-id="b3094-225">The unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="b3094-226">Is een gesorteerde lijst van alle voorwaarden van alle documenten in een omgekeerde index.</span><span class="sxs-lookup"><span data-stu-id="b3094-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="b3094-227">Elke term wordt toegewezen aan de lijst met documenten waarin zich, duidelijk naar voren, in het onderstaande voorbeeld voordoet.</span><span class="sxs-lookup"><span data-stu-id="b3094-227">Each term maps to the list of documents in which it occurs, as evident in the example below.</span></span>

<span data-ttu-id="b3094-228">De voorwaarden in een omgekeerde index produceren, voert de zoekmachine lexicale analyse over de inhoud van documenten, vergelijkbaar met wat er tijdens de verwerking van query's gebeurt.</span><span class="sxs-lookup"><span data-stu-id="b3094-228">To produce the terms in an inverted index, the search engine performs lexical analysis over the content of documents, similar to what happens during query processing.</span></span> <span data-ttu-id="b3094-229">Tekst invoer worden doorgegeven aan een analyzer, geïntegreerd in een kleine, enz., afhankelijk van de configuratie analyzer en leestekens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b3094-229">Text inputs are passed to an analyzer, lower-cased, stripped of punctuation, and so forth, depending on the analyzer configuration.</span></span> <span data-ttu-id="b3094-230">Het is algemene, maar niet vereist, met de dezelfde analyzers voor zoeken en indexeren operations zodat querytermen meer gelijke termen in de index uitzien.</span><span class="sxs-lookup"><span data-stu-id="b3094-230">It's common, but not required, to use the same analyzers for search and indexing operations so that query terms look more like terms inside the index.</span></span>

> [!Note]
> <span data-ttu-id="b3094-231">Azure Search kunt u verschillende analyzers voor indexeren opgeven en zoek via aanvullende `indexAnalyzer` en `searchAnalyzer` veld parameters.</span><span class="sxs-lookup"><span data-stu-id="b3094-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="b3094-232">Als u niets opgeeft, wordt de analyzer ingesteld met de `analyzer` eigenschap wordt gebruikt voor het indexeren en het zoeken.</span><span class="sxs-lookup"><span data-stu-id="b3094-232">If unspecified, the analyzer set with the `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="b3094-233">**Omgekeerde index voor voorbeelddocumenten**</span><span class="sxs-lookup"><span data-stu-id="b3094-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="b3094-234">Terugkeren naar het voorbeeld voor het **titel** veld omgekeerde index ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b3094-234">Returning to our example, for the **title** field, the inverted index looks like this:</span></span>

| <span data-ttu-id="b3094-235">Termijn</span><span class="sxs-lookup"><span data-stu-id="b3094-235">Term</span></span> | <span data-ttu-id="b3094-236">Lijst met standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="b3094-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="b3094-237">atman</span><span class="sxs-lookup"><span data-stu-id="b3094-237">atman</span></span> | <span data-ttu-id="b3094-238">1</span><span class="sxs-lookup"><span data-stu-id="b3094-238">1</span></span> |
| <span data-ttu-id="b3094-239">strand</span><span class="sxs-lookup"><span data-stu-id="b3094-239">beach</span></span> | <span data-ttu-id="b3094-240">2</span><span class="sxs-lookup"><span data-stu-id="b3094-240">2</span></span> |
| <span data-ttu-id="b3094-241">hotel</span><span class="sxs-lookup"><span data-stu-id="b3094-241">hotel</span></span> | <span data-ttu-id="b3094-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="b3094-242">1, 3</span></span> |
| <span data-ttu-id="b3094-243">Oceaan</span><span class="sxs-lookup"><span data-stu-id="b3094-243">ocean</span></span> | <span data-ttu-id="b3094-244">4</span><span class="sxs-lookup"><span data-stu-id="b3094-244">4</span></span>  |
| <span data-ttu-id="b3094-245">playa</span><span class="sxs-lookup"><span data-stu-id="b3094-245">playa</span></span> | <span data-ttu-id="b3094-246">3</span><span class="sxs-lookup"><span data-stu-id="b3094-246">3</span></span> |
| <span data-ttu-id="b3094-247">toevlucht</span><span class="sxs-lookup"><span data-stu-id="b3094-247">resort</span></span> | <span data-ttu-id="b3094-248">3</span><span class="sxs-lookup"><span data-stu-id="b3094-248">3</span></span> |
| <span data-ttu-id="b3094-249">Terugtrekken</span><span class="sxs-lookup"><span data-stu-id="b3094-249">retreat</span></span> | <span data-ttu-id="b3094-250">4</span><span class="sxs-lookup"><span data-stu-id="b3094-250">4</span></span> |

<span data-ttu-id="b3094-251">In het titelveld alleen *hotel* wordt weergegeven in twee documenten: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="b3094-251">In the title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="b3094-252">Voor de **beschrijving** veld de index is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b3094-252">For the **description** field, the index is as follows:</span></span>

| <span data-ttu-id="b3094-253">Termijn</span><span class="sxs-lookup"><span data-stu-id="b3094-253">Term</span></span> | <span data-ttu-id="b3094-254">Lijst met standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="b3094-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="b3094-255">lucht</span><span class="sxs-lookup"><span data-stu-id="b3094-255">air</span></span> | <span data-ttu-id="b3094-256">3</span><span class="sxs-lookup"><span data-stu-id="b3094-256">3</span></span>
| <span data-ttu-id="b3094-257">en</span><span class="sxs-lookup"><span data-stu-id="b3094-257">and</span></span> | <span data-ttu-id="b3094-258">4</span><span class="sxs-lookup"><span data-stu-id="b3094-258">4</span></span>
| <span data-ttu-id="b3094-259">strand</span><span class="sxs-lookup"><span data-stu-id="b3094-259">beach</span></span> | <span data-ttu-id="b3094-260">1</span><span class="sxs-lookup"><span data-stu-id="b3094-260">1</span></span>
| <span data-ttu-id="b3094-261">voorwaarde</span><span class="sxs-lookup"><span data-stu-id="b3094-261">conditioned</span></span> | <span data-ttu-id="b3094-262">3</span><span class="sxs-lookup"><span data-stu-id="b3094-262">3</span></span>
| <span data-ttu-id="b3094-263">vertrouwd</span><span class="sxs-lookup"><span data-stu-id="b3094-263">comfortable</span></span> | <span data-ttu-id="b3094-264">3</span><span class="sxs-lookup"><span data-stu-id="b3094-264">3</span></span>
| <span data-ttu-id="b3094-265">afstand</span><span class="sxs-lookup"><span data-stu-id="b3094-265">distance</span></span> | <span data-ttu-id="b3094-266">1</span><span class="sxs-lookup"><span data-stu-id="b3094-266">1</span></span>
| <span data-ttu-id="b3094-267">eiland</span><span class="sxs-lookup"><span data-stu-id="b3094-267">island</span></span> | <span data-ttu-id="b3094-268">2</span><span class="sxs-lookup"><span data-stu-id="b3094-268">2</span></span>
| <span data-ttu-id="b3094-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="b3094-269">kauaʻi</span></span> | <span data-ttu-id="b3094-270">2</span><span class="sxs-lookup"><span data-stu-id="b3094-270">2</span></span>
| <span data-ttu-id="b3094-271">zich bevindt</span><span class="sxs-lookup"><span data-stu-id="b3094-271">located</span></span> | <span data-ttu-id="b3094-272">2</span><span class="sxs-lookup"><span data-stu-id="b3094-272">2</span></span>
| <span data-ttu-id="b3094-273">Noord</span><span class="sxs-lookup"><span data-stu-id="b3094-273">north</span></span> | <span data-ttu-id="b3094-274">2</span><span class="sxs-lookup"><span data-stu-id="b3094-274">2</span></span>
| <span data-ttu-id="b3094-275">Oceaan</span><span class="sxs-lookup"><span data-stu-id="b3094-275">ocean</span></span> | <span data-ttu-id="b3094-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="b3094-276">1, 2, 3</span></span>
| <span data-ttu-id="b3094-277">van</span><span class="sxs-lookup"><span data-stu-id="b3094-277">of</span></span> | <span data-ttu-id="b3094-278">2</span><span class="sxs-lookup"><span data-stu-id="b3094-278">2</span></span>
| <span data-ttu-id="b3094-279">op</span><span class="sxs-lookup"><span data-stu-id="b3094-279">on</span></span> |<span data-ttu-id="b3094-280">2</span><span class="sxs-lookup"><span data-stu-id="b3094-280">2</span></span>
| <span data-ttu-id="b3094-281">Stille</span><span class="sxs-lookup"><span data-stu-id="b3094-281">quiet</span></span> | <span data-ttu-id="b3094-282">4</span><span class="sxs-lookup"><span data-stu-id="b3094-282">4</span></span>
| <span data-ttu-id="b3094-283">ruimten</span><span class="sxs-lookup"><span data-stu-id="b3094-283">rooms</span></span>  | <span data-ttu-id="b3094-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="b3094-284">1, 3</span></span>
| <span data-ttu-id="b3094-285">secluded</span><span class="sxs-lookup"><span data-stu-id="b3094-285">secluded</span></span> | <span data-ttu-id="b3094-286">4</span><span class="sxs-lookup"><span data-stu-id="b3094-286">4</span></span>
| <span data-ttu-id="b3094-287">wal</span><span class="sxs-lookup"><span data-stu-id="b3094-287">shore</span></span> | <span data-ttu-id="b3094-288">2</span><span class="sxs-lookup"><span data-stu-id="b3094-288">2</span></span>
| <span data-ttu-id="b3094-289">groot</span><span class="sxs-lookup"><span data-stu-id="b3094-289">spacious</span></span> | <span data-ttu-id="b3094-290">1</span><span class="sxs-lookup"><span data-stu-id="b3094-290">1</span></span>
| <span data-ttu-id="b3094-291">de</span><span class="sxs-lookup"><span data-stu-id="b3094-291">the</span></span> | <span data-ttu-id="b3094-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="b3094-292">1, 2</span></span>
| <span data-ttu-id="b3094-293">tot</span><span class="sxs-lookup"><span data-stu-id="b3094-293">to</span></span> | <span data-ttu-id="b3094-294">1</span><span class="sxs-lookup"><span data-stu-id="b3094-294">1</span></span>
| <span data-ttu-id="b3094-295">weergeven</span><span class="sxs-lookup"><span data-stu-id="b3094-295">view</span></span> | <span data-ttu-id="b3094-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="b3094-296">1, 2, 3</span></span>
| <span data-ttu-id="b3094-297">roulatie van</span><span class="sxs-lookup"><span data-stu-id="b3094-297">walking</span></span> | <span data-ttu-id="b3094-298">1</span><span class="sxs-lookup"><span data-stu-id="b3094-298">1</span></span>
| <span data-ttu-id="b3094-299">met</span><span class="sxs-lookup"><span data-stu-id="b3094-299">with</span></span> | <span data-ttu-id="b3094-300">3</span><span class="sxs-lookup"><span data-stu-id="b3094-300">3</span></span>


<span data-ttu-id="b3094-301">**Overeenkomende querytermen tegen geïndexeerde voorwaarden**</span><span class="sxs-lookup"><span data-stu-id="b3094-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="b3094-302">Gezien de bovenstaande omgekeerde indexen, gaan we u terug naar de voorbeeldquery en Zie hoe overeenkomende documenten zijn gevonden voor de voorbeeldquery.</span><span class="sxs-lookup"><span data-stu-id="b3094-302">Given the inverted indices above, let’s return to the sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="b3094-303">Let erop dat de laatste querystructuur ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b3094-303">Recall that the final query tree looks like this:</span></span> 

 ![Booleaanse query geanalyseerde voorwaarden][4]

<span data-ttu-id="b3094-305">Tijdens het uitvoeren van query worden afzonderlijke query's uitgevoerd met de doorzoekbare velden onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="b3094-305">During query execution, individual queries are executed against the searchable fields independently.</span></span> 

+ <span data-ttu-id="b3094-306">Het komt overeen met 'groot' TermQuery, documenteer 1 (Hotel Atman).</span><span class="sxs-lookup"><span data-stu-id="b3094-306">The TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="b3094-307">De PrefixQuery ' air-condition * ', komt niet overeen met alle documenten.</span><span class="sxs-lookup"><span data-stu-id="b3094-307">The PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="b3094-308">Dit is een probleem dat soms confuses ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b3094-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="b3094-309">Hoewel de term air-conditioned in het document bestaat, is deze opgesplitst in twee termen door de standaard analyzer.</span><span class="sxs-lookup"><span data-stu-id="b3094-309">Although the term air-conditioned exists in the document, it is split into two terms by the default analyzer.</span></span> <span data-ttu-id="b3094-310">Intrekken voorvoegsel query's die voor gedeeltelijke termen bevatten, worden niet geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="b3094-311">Daarom worden voorwaarden met het voorvoegsel 'air-condition' opgezocht in de omgekeerde index en niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="b3094-311">Therefore terms with prefix "air-condition" are looked up in the inverted index and not found.</span></span>

+ <span data-ttu-id="b3094-312">De PhraseQuery, 'Oceaan weergave', zoekt de termen 'Oceaan' en 'weergeven' en de buurt van de voorwaarden in het originele document wordt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-312">The PhraseQuery, "ocean view", looks up the terms "ocean" and "view" and checks the proximity of terms in the original document.</span></span> <span data-ttu-id="b3094-313">Documenten 1, 2 en 3 overeen met deze query in het omschrijvingsveld.</span><span class="sxs-lookup"><span data-stu-id="b3094-313">Documents 1, 2 and 3 match this query in the description field.</span></span> <span data-ttu-id="b3094-314">U ziet document 4 heeft de term Oceaan in de titel, maar wordt niet beschouwd als een overeenkomst als er op zoek bent naar de zinsnede 'Oceaan weergave' in plaats van afzonderlijke woorden.</span><span class="sxs-lookup"><span data-stu-id="b3094-314">Notice document 4 has the term ocean in the title but isn’t considered a match, as we're looking for the "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="b3094-315">Een zoekquery tenzij u de velden in te stellen beperken onafhankelijk tegen de doorzoekbare velden in de Azure Search-index wordt uitgevoerd de `searchFields` parameter, zoals geïllustreerd in de zoekaanvraag voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b3094-315">A search query is executed independently against all searchable fields in the Azure Search index unless you limit the fields set with the `searchFields` parameter, as illustrated in the example search request.</span></span> <span data-ttu-id="b3094-316">Documenten die overeenkomen met een van de geselecteerde velden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b3094-316">Documents that match in any of the selected fields are returned.</span></span> 

<span data-ttu-id="b3094-317">Op de gehele voor de desbetreffende query worden de documenten die overeenkomen met 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="b3094-317">On the whole, for the query in question, the documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="b3094-318">Stap 4: score berekenen</span><span class="sxs-lookup"><span data-stu-id="b3094-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="b3094-319">Elk document dat in een resultatenset search is een score relevantie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b3094-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="b3094-320">De functie van de score relevantie is positie hoger documenten die het beste een gebruiker-vraag te beantwoorden zoals deze wordt weergegeven door de query.</span><span class="sxs-lookup"><span data-stu-id="b3094-320">The function of the relevance score is to rank higher those documents that best answer a user question as expressed by the search query.</span></span> <span data-ttu-id="b3094-321">De score wordt berekend op basis van statistische eigenschappen van de voorwaarden die overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="b3094-321">The score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="b3094-322">Is de kern van de formule van de score [TF/IDF (frequentie term frequentie inverse document)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="b3094-322">At the core of the scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="b3094-323">In de query's met zeldzame en algemene voorwaarden, bevordert TF/IDF resultaten met de zeldzame term.</span><span class="sxs-lookup"><span data-stu-id="b3094-323">In queries containing rare and common terms, TF/IDF promotes results containing the rare term.</span></span> <span data-ttu-id="b3094-324">Bijvoorbeeld in een hypothetische index met alle Wikipedia artikelen van documenten die overeenkomen met de query *de directeur*, documenten die overeenkomen met op *directeur* worden beschouwd als meer dan documenten overeen op de relevante *de*.</span><span class="sxs-lookup"><span data-stu-id="b3094-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched the query *the president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="b3094-325">Score berekenen voor voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b3094-325">Scoring example</span></span>

<span data-ttu-id="b3094-326">Intrekken van de drie documenten die overeenkomen met de voorbeeldquery:</span><span class="sxs-lookup"><span data-stu-id="b3094-326">Recall the three documents that matched our example query:</span></span>
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance to the beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on the north shore of the island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="b3094-327">Document 1 komt overeen met de query beste omdat zowel de term *groot* en de vereiste woordgroep *Oceaan weergave* optreden in het omschrijvingsveld.</span><span class="sxs-lookup"><span data-stu-id="b3094-327">Document 1 matched the query best because both the term *spacious* and the required phrase *ocean view* occur in the description field.</span></span> <span data-ttu-id="b3094-328">De volgende twee documenten die overeenkomen met alleen de woordgroep *Oceaan weergave*.</span><span class="sxs-lookup"><span data-stu-id="b3094-328">The next two documents match only the phrase *ocean view*.</span></span> <span data-ttu-id="b3094-329">Mogelijk verrassend dat de score relevantie voor document 2 en 3 anders is, ondanks dat ze overeenkomen met de query op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="b3094-329">It might be surprising that the relevance score for document 2 and 3 is different even though they matched the query in the same way.</span></span> <span data-ttu-id="b3094-330">Omdat de formule van de score meer onderdelen dan alleen TF/IDF bevat wordt.</span><span class="sxs-lookup"><span data-stu-id="b3094-330">It's because the scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="b3094-331">In dit geval document 3 die een enigszins hogere score is toegewezen, omdat de beschrijving korter is.</span><span class="sxs-lookup"><span data-stu-id="b3094-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="b3094-332">Meer informatie over [Lucene van praktische score berekenen voor de formule](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) om te begrijpen hoe het veldlengte en andere factoren van invloed is op de score relevantie.</span><span class="sxs-lookup"><span data-stu-id="b3094-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) to understand how field length and other factors can influence the relevance score.</span></span>

<span data-ttu-id="b3094-333">Sommige querytypen (jokerteken, voorvoegsel, regex) bijdragen altijd een constante score voor de algehele document score.</span><span class="sxs-lookup"><span data-stu-id="b3094-333">Some query types (wildcard, prefix, regex) always contribute a constant score to the overall document score.</span></span> <span data-ttu-id="b3094-334">Hierdoor komt overeen met gevonden via de uitbreiding van de query moet worden opgenomen in de resultaten, maar zonder de volgorde.</span><span class="sxs-lookup"><span data-stu-id="b3094-334">This allows matches found through query expansion to be included in the results, but without affecting the ranking.</span></span> 

<span data-ttu-id="b3094-335">Een voorbeeld illustreert waarom dit is van belang.</span><span class="sxs-lookup"><span data-stu-id="b3094-335">An example illustrates why this matters.</span></span> <span data-ttu-id="b3094-336">Zoekopdrachten met jokertekens, met inbegrip van zoekopdrachten voor voorvoegsel, zijn niet-eenduidige per definitie omdat de invoer is gedeeltelijke tekenreeks met mogelijke overeenkomsten op een zeer groot aantal verschillende voorwaarden (overweeg invoer van het "rondleiding *" met overeenkomsten gevonden op 'rondleidingen', 'tourettes' en 'tourmaline').</span><span class="sxs-lookup"><span data-stu-id="b3094-336">Wildcard searches, including prefix searches, are ambiguous by definition because the input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="b3094-337">Gezien de aard van deze resultaten, kan er niet worden redelijkerwijs afleiden welke voorwaarden vindt u meer dan andere waardevolle.</span><span class="sxs-lookup"><span data-stu-id="b3094-337">Given the nature of these results, there is no way to reasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="b3094-338">Om deze reden negeren we term frequenties wanneer resultaten scoren van typen jokerteken, voorvoegsel en regex-query's.</span><span class="sxs-lookup"><span data-stu-id="b3094-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="b3094-339">In een meerdelig zoekaanvraag die gedeeltelijke en volledige voorwaarden bevat, worden de resultaten van de gedeeltelijk invoer opgenomen met een constante score om te voorkomen dat de afwijking naar mogelijk onverwacht komt overeen met.</span><span class="sxs-lookup"><span data-stu-id="b3094-339">In a multi-part search request that includes partial and complete terms, results from the partial input are incorporated with a constant score to avoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="b3094-340">Score afstemmen</span><span class="sxs-lookup"><span data-stu-id="b3094-340">Score tuning</span></span>

<span data-ttu-id="b3094-341">Er zijn twee manieren om af te stemmen relevantie scores in Azure Search:</span><span class="sxs-lookup"><span data-stu-id="b3094-341">There are two ways to tune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="b3094-342">**Score berekenen voor profielen** promoveren van documenten in de gerangschikte lijst met resultaten op basis van een set regels.</span><span class="sxs-lookup"><span data-stu-id="b3094-342">**Scoring profiles** promote documents in the ranked list of results based on a set of rules.</span></span> <span data-ttu-id="b3094-343">In ons voorbeeld kan we kunt u documenten die overeenkomen met in het titelveld meer relevante dan documenten die overeenkomen met in het omschrijvingsveld.</span><span class="sxs-lookup"><span data-stu-id="b3094-343">In our example, we could consider documents that matched in the title field more relevant than documents that matched in the description field.</span></span> <span data-ttu-id="b3094-344">Bovendien kan er als onze index had een prijsveld voor elke hotel, documenten met lagere prijs promoveren.</span><span class="sxs-lookup"><span data-stu-id="b3094-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="b3094-345">Meer informatie over het meer [score berekenen voor profielen toevoegen aan een search-index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="b3094-345">Learn more how to [add Scoring Profiles to a search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="b3094-346">**Versterking** (alleen beschikbaar in de volledige Lucene-querysyntaxis) biedt een prestatieverbetering operator `^` die kunnen worden toegepast op een deel van de querystructuur van de.</span><span class="sxs-lookup"><span data-stu-id="b3094-346">**Term boosting** (available only in the Full Lucene query syntax) provides a boosting operator `^` that can be applied to any part of the query tree.</span></span> <span data-ttu-id="b3094-347">In ons voorbeeld, in plaats van het zoeken op het voorvoegsel *air-condition*\*, een kan zoekterm voor de exacte *air-condition* of het voorvoegsel, maar de documenten die overeenkomen met de exacte term hoger door toe te passen versterking aan de query term zijn gerangschikt: *lucht voorwaarde ^ 2 || AIR-condition**.</span><span class="sxs-lookup"><span data-stu-id="b3094-347">In our example, instead of searching on the prefix *air-condition*\*, one could search for either the exact term *air-condition* or the prefix, but documents that match on the exact term are ranked higher by applying boost to the term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="b3094-348">Meer informatie over [versterking](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="b3094-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="b3094-349">Score berekenen voor in een gedistribueerde index</span><span class="sxs-lookup"><span data-stu-id="b3094-349">Scoring in a distributed index</span></span>

<span data-ttu-id="b3094-350">Alle indexen in Azure Search automatisch opgesplitst in meerdere shards ons toestemming te distribueren snel de index tussen meerdere knooppunten tijdens service schaal omhoog of omlaag schalen.</span><span class="sxs-lookup"><span data-stu-id="b3094-350">All indexes in Azure Search are automatically split into multiple shards, allowing us to quickly distribute the index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="b3094-351">Wanneer een zoekaanvraag is uitgegeven, wordt deze onafhankelijk tegen elke shard verstrekt.</span><span class="sxs-lookup"><span data-stu-id="b3094-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="b3094-352">De resultaten van elke shard worden vervolgens samengevoegd en geordend op score (als er geen andere volgorde gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="b3094-352">The results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="b3094-353">Het is belangrijk te weten dat de scoreprofiel functie gewichten term frequentie tegen de inverse document frequentie in alle documenten in de shard query niet over de breedte van alle shards.</span><span class="sxs-lookup"><span data-stu-id="b3094-353">It is important to know that the scoring function weights query term frequency against its inverse document frequency in all documents within the shard, not across all shards!</span></span>

<span data-ttu-id="b3094-354">Dit betekent dat een score relevantie *kan* zijn verschillend voor identieke documenten als ze zich op andere shards bevinden.</span><span class="sxs-lookup"><span data-stu-id="b3094-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="b3094-355">Deze verschillen vaak gelukkig verdwijnen wanneer het aantal documenten in de index vanwege meer zelfs term distributie groeit.</span><span class="sxs-lookup"><span data-stu-id="b3094-355">Fortunately, such differences tend to disappear as the number of documents in the index grows due to more even term distribution.</span></span> <span data-ttu-id="b3094-356">Het is niet mogelijk om aan te nemen op welke shard een document wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b3094-356">It’s not possible to assume on which shard any given document will be placed.</span></span> <span data-ttu-id="b3094-357">Echter, ervan uitgaande dat de documentsleutel van een niet wijzigen, deze wordt altijd worden toegewezen aan de dezelfde shard.</span><span class="sxs-lookup"><span data-stu-id="b3094-357">However, assuming a document key doesn't change, it will always be assigned to the same shard.</span></span>

<span data-ttu-id="b3094-358">In het algemeen is document score niet het aanbevolen kenmerk voor het ordenen van documenten als stabiliteit van de volgorde belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="b3094-358">In general, document score is not the best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="b3094-359">Bijvoorbeeld, is gezien twee document met een identieke score, er geen garantie waarvoor een eerste wordt weergegeven in latere uitvoeringen van dezelfde query.</span><span class="sxs-lookup"><span data-stu-id="b3094-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of the same query.</span></span> <span data-ttu-id="b3094-360">Document score geeft alleen een algemeen beeld van het document relevantie ten opzichte van andere documenten in de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="b3094-360">Document score should only give a general sense of document relevance relative to other documents in the results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b3094-361">Conclusie</span><span class="sxs-lookup"><span data-stu-id="b3094-361">Conclusion</span></span>

<span data-ttu-id="b3094-362">Het succes van zoekmachines internet heeft verwachtingen voor zoeken in volledige tekst gegenereerd via persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="b3094-362">The success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="b3094-363">Voor vrijwel elke soort zoekervaring verwachten we nu de engine om te begrijpen onze bedoeling, zelfs wanneer de voorwaarden zijn onjuist gespeld of zijn onvolledig.</span><span class="sxs-lookup"><span data-stu-id="b3094-363">For almost any kind of search experience, we now expect the engine to understand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="b3094-364">We verwachten mogelijk zelfs op basis van in de buurt vergelijkbare termen of synoniemen die we hebben nooit echt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b3094-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="b3094-365">Zoekopdracht in volledige tekst is van een technisch oogpunt zeer complex is of waarvoor geavanceerde analyses van de taalkundige en een systematische aanpak op de verwerking van de manieren waarop distill, vouw en transformeren querytermen leveren een relevante resultaat.</span><span class="sxs-lookup"><span data-stu-id="b3094-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach to processing in ways that distill, expand, and transform query terms to deliver a relevant result.</span></span> <span data-ttu-id="b3094-366">Gezien de intrinsieke complexiteit, zijn er veel factoren die van invloed kunnen zijn op het resultaat van een query.</span><span class="sxs-lookup"><span data-stu-id="b3094-366">Given the inherent complexities, there are a lot of factors that can affect the outcome of a query.</span></span> <span data-ttu-id="b3094-367">Om deze reden biedt voldoende tijd om te begrijpen van het mechanisme van zoeken in volledige tekst concrete voordelen bij een poging om te werken via onverwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="b3094-367">For this reason, investing the time to understand the mechanics of full text search offers tangible benefits when trying to work through unexpected results.</span></span>  

<span data-ttu-id="b3094-368">In dit artikel verkend zoeken in volledige tekst in de context van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b3094-368">This article explored full text search in the context of Azure Search.</span></span> <span data-ttu-id="b3094-369">We hopen dat dit biedt u voldoende achtergrond voor het herkennen van mogelijke oorzaken en oplossingen voor het adresseren van veelvoorkomende problemen van de query.</span><span class="sxs-lookup"><span data-stu-id="b3094-369">We hope it gives you sufficient background to recognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b3094-370">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3094-370">Next steps</span></span>

+ <span data-ttu-id="b3094-371">De voorbeeld-index bouwen, uitproberen verschillende query's en resultaten bekijken.</span><span class="sxs-lookup"><span data-stu-id="b3094-371">Build the sample index, try out different queries and review results.</span></span> <span data-ttu-id="b3094-372">Zie voor instructies [bouwen en query uitvoeren op een index in de portal](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="b3094-372">For instructions, see [Build and query an index in the portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="b3094-373">Probeer extra querysyntaxis van de [documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) voorbeeld in deze sectie of van [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in de portal.</span><span class="sxs-lookup"><span data-stu-id="b3094-373">Try additional query syntax from the [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in the portal.</span></span>

+ <span data-ttu-id="b3094-374">Bekijk [score berekenen voor profielen](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) als u wilt afstemmen ranking in uw zoektoepassing.</span><span class="sxs-lookup"><span data-stu-id="b3094-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want to tune ranking in your search application.</span></span>

+ <span data-ttu-id="b3094-375">Meer informatie over het toepassen van [taalspecifieke lexicale analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="b3094-375">Learn how to apply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="b3094-376">[Configureren van aangepaste analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) voor minimale verwerking of speciale verwerking voor specifieke velden.</span><span class="sxs-lookup"><span data-stu-id="b3094-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="b3094-377">[Standard- en Engelse analyzers vergelijken](http://alice.unearth.ai/)) naast elkaar op deze demo-website.</span><span class="sxs-lookup"><span data-stu-id="b3094-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="b3094-378">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b3094-378">See also</span></span>

[<span data-ttu-id="b3094-379">REST-API documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="b3094-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="b3094-380">Vereenvoudigde querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="b3094-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="b3094-381">Volledige Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="b3094-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="b3094-382">Zoekresultaten verwerken</span><span class="sxs-lookup"><span data-stu-id="b3094-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
