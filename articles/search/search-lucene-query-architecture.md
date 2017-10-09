---
title: architectuur van aaaFull tekst zoeken engine (Lucene) in Azure Search | Microsoft Docs
description: Uitleg van de Lucene query verwerking en document ophalen concepten voor zoeken in volledige tekst, als verwante tooAzure zoeken.
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
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="fde34-103">Hoe vol tekst zoeken werkt in Azure Search</span><span class="sxs-lookup"><span data-stu-id="fde34-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="fde34-104">Dit artikel is voor ontwikkelaars die u een beter begrip moeten van de werking van Lucene zoeken in volledige tekst in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fde34-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="fde34-105">Voor tekst-query's, Azure Search naadloos verwachte resultaten in de meeste gevallen levert, maar soms mogelijk krijgt u een resultaat enigszins lijkt "off".</span><span class="sxs-lookup"><span data-stu-id="fde34-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="fde34-106">In deze situaties met een achtergrond in vier fasen van de queryuitvoering Lucene Hallo (query parseren, lexicale analyse, document-koppeling, score berekenen) kunt u specifieke wijzigingen tooquery parameters te identificeren of index van de configuratie die Hallo levert het gewenste resultaat.</span><span class="sxs-lookup"><span data-stu-id="fde34-106">In these situations, having a background in hello four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes tooquery parameters or index configuration that will deliver hello desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="fde34-107">Azure Search Lucene gebruikt voor zoekopdrachten in volledige tekst, maar Lucene-integratie is niet volledig.</span><span class="sxs-lookup"><span data-stu-id="fde34-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="fde34-108">We selectief weergeven en Lucene functionaliteit tooenable Hallo scenario's belangrijke tooAzure zoekopdracht uit te breiden.</span><span class="sxs-lookup"><span data-stu-id="fde34-108">We selectively expose and extend Lucene functionality tooenable hello scenarios important tooAzure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="fde34-109">Overzicht van de architectuur en diagram</span><span class="sxs-lookup"><span data-stu-id="fde34-109">Architecture overview and diagram</span></span>

<span data-ttu-id="fde34-110">Verwerking van een zoekopdracht voor volledige tekst begint met het parseren van tooextract zoektermen op Hallo query tekst.</span><span class="sxs-lookup"><span data-stu-id="fde34-110">Processing a full text search query starts with parsing hello query text tooextract search terms.</span></span> <span data-ttu-id="fde34-111">Hallo zoekmachine maakt gebruik van een index tooretrieve documenten met overeenkomende voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="fde34-111">hello search engine uses an index tooretrieve documents with matching terms.</span></span> <span data-ttu-id="fde34-112">Afzonderlijke querytermen soms worden opgedeeld en geregenereerd in nieuwe formulieren toocast breder net over wat kan worden beschouwd als een mogelijke overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="fde34-112">Individual query terms are sometimes broken down and reconstituted into new forms toocast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="fde34-113">Geen resultatenset is vervolgens gesorteerd op een relevantie score toegewezen tooeach afzonderlijke overeenkomende document.</span><span class="sxs-lookup"><span data-stu-id="fde34-113">A result set is then sorted by a relevance score assigned tooeach individual matching document.</span></span> <span data-ttu-id="fde34-114">Die boven Hallo Hallo gerangschikte lijst worden de aanroepende toepassing toohello geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-114">Those at hello top of hello ranked list are returned toohello calling application.</span></span>

<span data-ttu-id="fde34-115">Aangepast, bestaat uitvoering van de query uit vier fasen:</span><span class="sxs-lookup"><span data-stu-id="fde34-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="fde34-116">Query bij het parseren van</span><span class="sxs-lookup"><span data-stu-id="fde34-116">Query parsing</span></span> 
2. <span data-ttu-id="fde34-117">Lexicale analyse</span><span class="sxs-lookup"><span data-stu-id="fde34-117">Lexical analysis</span></span> 
3. <span data-ttu-id="fde34-118">Document ophalen</span><span class="sxs-lookup"><span data-stu-id="fde34-118">Document retrieval</span></span> 
4. <span data-ttu-id="fde34-119">Score berekenen</span><span class="sxs-lookup"><span data-stu-id="fde34-119">Scoring</span></span> 

<span data-ttu-id="fde34-120">Hallo diagram hieronder ziet u Hallo onderdelen die worden gebruikt tooprocess een zoekaanvraag.</span><span class="sxs-lookup"><span data-stu-id="fde34-120">hello diagram below illustrates hello components used tooprocess a search request.</span></span> 

 ![Architectuurdiagram van de Lucene-query in Azure Search][1]


| <span data-ttu-id="fde34-122">Belangrijkste onderdelen</span><span class="sxs-lookup"><span data-stu-id="fde34-122">Key components</span></span> | <span data-ttu-id="fde34-123">Functionele beschrijving</span><span class="sxs-lookup"><span data-stu-id="fde34-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="fde34-124">**Query parsers**</span><span class="sxs-lookup"><span data-stu-id="fde34-124">**Query parsers**</span></span> | <span data-ttu-id="fde34-125">Afzonderlijke querytermen van query's en Hallo query structuur (een querystructuur) toobe verzonden toohello zoekmachine maken.</span><span class="sxs-lookup"><span data-stu-id="fde34-125">Separate query terms from query operators and create hello query structure (a query tree) toobe sent toohello search engine.</span></span> |
|<span data-ttu-id="fde34-126">**Analyzers**</span><span class="sxs-lookup"><span data-stu-id="fde34-126">**Analyzers**</span></span> | <span data-ttu-id="fde34-127">Lexicale analyse uitvoeren op querytermen.</span><span class="sxs-lookup"><span data-stu-id="fde34-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="fde34-128">Dit proces kan betrekking hebben op transformeren, te verwijderen of uitbreiden van de voorwaarden van de query.</span><span class="sxs-lookup"><span data-stu-id="fde34-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="fde34-129">**Index**</span><span class="sxs-lookup"><span data-stu-id="fde34-129">**Index**</span></span> | <span data-ttu-id="fde34-130">Een efficiënte gegevensstructuur toostore gebruikt en organiseren doorzoekbare voorwaarden opgehaald uit de geïndexeerde documenten.</span><span class="sxs-lookup"><span data-stu-id="fde34-130">An efficient data structure used toostore and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="fde34-131">**Zoekmachine**</span><span class="sxs-lookup"><span data-stu-id="fde34-131">**Search engine**</span></span> | <span data-ttu-id="fde34-132">Haalt en scores die overeenkomt met de documenten op basis van de inhoud Hallo Hallo omgekeerd index.</span><span class="sxs-lookup"><span data-stu-id="fde34-132">Retrieves and scores matching documents based on hello contents of hello inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="fde34-133">Anatomie van een zoekaanvraag</span><span class="sxs-lookup"><span data-stu-id="fde34-133">Anatomy of a search request</span></span>

<span data-ttu-id="fde34-134">Een zoekaanvraag is een complete specificatie van wat moet worden geretourneerd in een resultatenset.</span><span class="sxs-lookup"><span data-stu-id="fde34-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="fde34-135">In de meest eenvoudige vorm is een lege query zonder criteria alle soorten.</span><span class="sxs-lookup"><span data-stu-id="fde34-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="fde34-136">Een voorbeeld van een meer realistische parameters bevat, verschillende query termen, mogelijk bereik toocertain velden, met mogelijk een filterexpressie en ordening van regels.</span><span class="sxs-lookup"><span data-stu-id="fde34-136">A more realistic example includes parameters, several query terms, perhaps scoped toocertain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="fde34-137">Hallo volgende voorbeeld wordt een zoekaanvraag u mogelijk tooAzure Search verzendt met behulp van Hallo [REST-API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="fde34-137">hello following example is a search request you might send tooAzure Search using hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

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

<span data-ttu-id="fde34-138">Voor deze aanvraag zoekmachine Hallo Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="fde34-138">For this request, hello search engine does hello following:</span></span>

1. <span data-ttu-id="fde34-139">Documenten gefilterd waar Hallo prijs is ten minste $60 en minder dan 300 $.</span><span class="sxs-lookup"><span data-stu-id="fde34-139">Filters out documents where hello price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="fde34-140">Hallo query worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-140">Executes hello query.</span></span> <span data-ttu-id="fde34-141">In dit voorbeeld Hallo zoekquery bestaat uit zinnen en voorwaarden: `"Spacious, air-condition* +\"Ocean view\""` (gebruikers doorgaans niet leestekens in te voeren, maar op te nemen in Hallo voorbeeld, kunnen wij tooexplain hoe analyzers verwerkt; het).</span><span class="sxs-lookup"><span data-stu-id="fde34-141">In this example, hello search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in hello example allows us tooexplain how analyzers handle it).</span></span> <span data-ttu-id="fde34-142">Voor deze query zoekmachine Hallo Hallo beschrijving gescand en titelvelden opgegeven in `searchFields` voor documenten die 'Oceaan weergave' bevatten en ook op Hallo term 'groot' of op voorwaarden die met het voorvoegsel Hallo beginnen 'air-condition'.</span><span class="sxs-lookup"><span data-stu-id="fde34-142">For this query, hello search engine scans hello description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on hello term "spacious", or on terms that start with hello prefix "air-condition".</span></span> <span data-ttu-id="fde34-143">Hallo `searchMode` parameter gebruikte toomatch zich op een term (standaard) of al deze gevallen waarbij een term niet expliciet hoeft (`+`).</span><span class="sxs-lookup"><span data-stu-id="fde34-143">hello `searchMode` parameter is used toomatch on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="fde34-144">Resulterende reeks hotels Hallo orders door nabijheid tooa opgegeven geografische locatie en vervolgens de aanroepende toepassing toohello wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-144">Orders hello resulting set of hotels by proximity tooa given geography location, and then returned toohello calling application.</span></span> 

<span data-ttu-id="fde34-145">Hallo meerderheid van dit artikel is over het verwerken van Hallo *zoekquery*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="fde34-145">hello majority of this article is about processing of hello *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="fde34-146">Filteren en ordening vallen buiten het bereik.</span><span class="sxs-lookup"><span data-stu-id="fde34-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="fde34-147">Zie voor meer informatie, Hallo [zoeken-API-naslagdocumentatie](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="fde34-147">For more information, see hello [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="fde34-148">Stap 1: Een Query bij het parseren van</span><span class="sxs-lookup"><span data-stu-id="fde34-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="fde34-149">Zoals vermeld, is queryreeks Hallo Hallo eerste regel van Hallo-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="fde34-149">As noted, hello query string is hello first line of hello request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="fde34-150">Hallo query parser scheidt operators (zoals `*` en `+` in Hallo voorbeeld) in een zoekvak, en het Hallo-zoekopdracht in deconstructs *subquery's* met een ondersteund type:</span><span class="sxs-lookup"><span data-stu-id="fde34-150">hello query parser separates operators (such as `*` and `+` in hello example) from search terms, and deconstructs hello search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="fde34-151">*term query* voor zelfstandige voorwaarden (zoals groot)</span><span class="sxs-lookup"><span data-stu-id="fde34-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="fde34-152">*woordgroep query* voor tussen aanhalingstekens voorwaarden (zoals Oceaan weergave)</span><span class="sxs-lookup"><span data-stu-id="fde34-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="fde34-153">*voorvoegsel query* voor voorwaarden gevolgd door een operator voorvoegsel `*` (zoals air-condition)</span><span class="sxs-lookup"><span data-stu-id="fde34-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="fde34-154">Zie voor een volledige lijst met ondersteunde querytypen [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="fde34-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="fde34-155">Operators die zijn gekoppeld aan een subquery bepalen of Hallo query 'moet' of 'moet' om een document tevreden toobe beschouwd als een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="fde34-155">Operators associated with a subquery determine whether hello query "must be" or "should be" satisfied in order for a document toobe considered a match.</span></span> <span data-ttu-id="fde34-156">Bijvoorbeeld: `+"Ocean view"` 'moet' is vanwege toohello `+` operator.</span><span class="sxs-lookup"><span data-stu-id="fde34-156">For example, `+"Ocean view"` is "must" due toohello `+` operator.</span></span> 

<span data-ttu-id="fde34-157">Hallo queryparser worden opnieuw gestructureerd Hallo subquery's in een *querystructuur* (een interne structuur die Hallo query) dit wordt doorgegeven op toohello zoekmachine.</span><span class="sxs-lookup"><span data-stu-id="fde34-157">hello query parser restructures hello subqueries into a *query tree* (an internal structure representing hello query) it passes on toohello search engine.</span></span> <span data-ttu-id="fde34-158">In de eerste fase van de query bij het parseren van Hallo uitziet Hallo querystructuur.</span><span class="sxs-lookup"><span data-stu-id="fde34-158">In hello first stage of query parsing, hello query tree looks like this.</span></span>  

 ![Booleaanse waarde searchmode ieder query][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="fde34-160">Ondersteund parsers: eenvoudig en volledige Lucene</span><span class="sxs-lookup"><span data-stu-id="fde34-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="fde34-161">Azure Search beschrijft de twee andere querytalen `simple` (standaard) en `full`.</span><span class="sxs-lookup"><span data-stu-id="fde34-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="fde34-162">Door de instelling Hallo `queryType` parameter bij uw zoekaanvraag, geeft u aan Hallo queryparser welke querytaal gewenst zodat deze weet hoe toointerpret Hallo operators en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="fde34-162">By setting hello `queryType` parameter with your search request, you tell hello query parser which query language you choose so that it knows how toointerpret hello operators and syntax.</span></span> <span data-ttu-id="fde34-163">Hallo [eenvoudige query taal](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) intuïtief en robuuste, vaak geschikte toointerpret gebruikersinvoer als-is zonder dat de verwerking van de clientzijde.</span><span class="sxs-lookup"><span data-stu-id="fde34-163">hello [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable toointerpret user input as-is without client-side processing.</span></span> <span data-ttu-id="fde34-164">Biedt ondersteuning voor query's van webzoekmachines bekend.</span><span class="sxs-lookup"><span data-stu-id="fde34-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="fde34-165">Hallo [volledige Lucene-querytaal](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), die wordt geleverd door in te stellen `queryType=full`, wordt de standaardtaal eenvoudige query Hallo uitgebreid met ondersteuning voor meer operators en querytypen zoals jokerteken, bij benadering, regex en veldgerelateerde query's.</span><span class="sxs-lookup"><span data-stu-id="fde34-165">hello [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends hello default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="fde34-166">Bijvoorbeeld, wordt een reguliere expressie in vereenvoudigde querysyntaxis verzonden geïnterpreteerd als een queryreeks bevat en niet een expressie.</span><span class="sxs-lookup"><span data-stu-id="fde34-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="fde34-167">aanvraag voor het voorbeeld in dit artikel Hallo Hallo volledige Lucene querytaal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fde34-167">hello example request in this article uses hello Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-hello-parser"></a><span data-ttu-id="fde34-168">Gevolgen van het searchMode op Hallo parser</span><span class="sxs-lookup"><span data-stu-id="fde34-168">Impact of searchMode on hello parser</span></span> 

<span data-ttu-id="fde34-169">Een andere aanvraag zoekparameter die gevolgen heeft voor het parseren is Hallo `searchMode` parameter.</span><span class="sxs-lookup"><span data-stu-id="fde34-169">Another search request parameter that affects parsing is hello `searchMode` parameter.</span></span> <span data-ttu-id="fde34-170">Hiermee kunt u de standaardoperator Hallo voor Boole-query's: een (standaard) of alle.</span><span class="sxs-lookup"><span data-stu-id="fde34-170">It controls hello default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="fde34-171">Wanneer `searchMode=any`, dat standaard Hallo Hallo spatie als scheidingsteken tussen groot is en air-condition is of (`||`), waardoor Hallo query voorbeeldtekst gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="fde34-171">When `searchMode=any`, which is hello default, hello space delimiter between spacious and air-condition is OR (`||`), making hello sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="fde34-172">Expliciete operators zoals `+` in `+"Ocean view"`, zijn niet-ambigue Booleaanse query constructie (Hallo term *moet* overeen).</span><span class="sxs-lookup"><span data-stu-id="fde34-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (hello term *must* match).</span></span> <span data-ttu-id="fde34-173">Minder duidelijk is hoe toointerpret Hallo resterende termen: groot en air-condition.</span><span class="sxs-lookup"><span data-stu-id="fde34-173">Less obvious is how toointerpret hello remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="fde34-174">Moet Hallo zoekmachine overeenkomsten vinden voor de weergave Oceaan *en* groot *en* air-condition?</span><span class="sxs-lookup"><span data-stu-id="fde34-174">Should hello search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="fde34-175">Of moet Oceaan weergave vinden plus *een* Hallo resterende voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="fde34-175">Or should it find ocean view plus *either one* of hello remaining terms?</span></span> 

<span data-ttu-id="fde34-176">Standaard (`searchMode=any`), Hallo zoekmachine wordt ervan uitgegaan dat Hallo breder interpretatie.</span><span class="sxs-lookup"><span data-stu-id="fde34-176">By default (`searchMode=any`), hello search engine assumes hello broader interpretation.</span></span> <span data-ttu-id="fde34-177">Een veld *moet* overeenkomen, opgetreden bij het weergeven 'of' semantiek.</span><span class="sxs-lookup"><span data-stu-id="fde34-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="fde34-178">structuur van de eerste query Hallo geïllustreerd voorheen Hello twee 'moet' bewerkingen, toont Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="fde34-178">hello initial query tree illustrated previously, with hello two "should" operations, shows hello default.</span></span>  

<span data-ttu-id="fde34-179">Stel dat we nu `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="fde34-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="fde34-180">In dit geval wordt Hallo ruimte geïnterpreteerd als een 'en'-bewerking.</span><span class="sxs-lookup"><span data-stu-id="fde34-180">In this case, hello space is interpreted as an "and" operation.</span></span> <span data-ttu-id="fde34-181">Elk van de overige voorwaarden Hallo zijn beide aanwezig in Hallo document tooqualify als een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="fde34-181">Each of hello remaining terms must both be present in hello document tooqualify as a match.</span></span> <span data-ttu-id="fde34-182">de resulterende voorbeeldquery Hello wordt geïnterpreteerd als volgt:</span><span class="sxs-lookup"><span data-stu-id="fde34-182">hello resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="fde34-183">Een boomstructuur gewijzigde query voor deze query zou zijn als volgt, waarbij een overeenkomende document Hallo snijpunt van alle drie subquery's is:</span><span class="sxs-lookup"><span data-stu-id="fde34-183">A modified query tree for this query would be as follows, where a matching document is hello intersection of all three subqueries:</span></span> 

 ![Booleaanse query searchmode alle][3]

> [!Note] 
> <span data-ttu-id="fde34-185">Kiezen `searchMode=any` via `searchMode=all` is een beste beslissing ontvangen op door het uitvoeren van representatieve query's.</span><span class="sxs-lookup"><span data-stu-id="fde34-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="fde34-186">Gebruikers die waarschijnlijk tooinclude operators (algemeen zijn wanneer zoeken document opslaat) wellicht resultaten intuïtievere als `searchMode=all` informeert Booleaanse query constructies.</span><span class="sxs-lookup"><span data-stu-id="fde34-186">Users who are likely tooinclude operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="fde34-187">Voor meer informatie over de wisselwerking tussen Hallo `searchMode` en operators, Zie [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="fde34-187">For more about hello interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="fde34-188">Stap 2: Lexicale analyse</span><span class="sxs-lookup"><span data-stu-id="fde34-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="fde34-189">Lexicale analyzers proces *benaming query's* en *woorden van query's* nadat Hallo querystructuur is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="fde34-189">Lexical analyzers process *term queries* and *phrase queries* after hello query tree is structured.</span></span> <span data-ttu-id="fde34-190">Een analyzer accepteert tekst invoer opgegeven tooit Hallo door Hallo parser, processen tekst hello en vervolgens verzendt terug tokenized voorwaarden toobe opgenomen in de querystructuur van de Hallo.</span><span class="sxs-lookup"><span data-stu-id="fde34-190">An analyzer accepts hello text inputs given tooit by hello parser, processes hello text, and then sends back tokenized terms toobe incorporated into hello query tree.</span></span> 

<span data-ttu-id="fde34-191">meest voorkomende vorm van lexicale analyse Hallo is *taalkundige analysis* welke transformaties querytermen op basis van regels voor specifieke tooa opgegeven taal:</span><span class="sxs-lookup"><span data-stu-id="fde34-191">hello most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific tooa given language:</span></span> 

* <span data-ttu-id="fde34-192">Een query term toohello hoofdmap vorm van een woord verminderen</span><span class="sxs-lookup"><span data-stu-id="fde34-192">Reducing a query term toohello root form of a word</span></span> 
* <span data-ttu-id="fde34-193">Verwijderen van niet-essentiële woorden (stopwoorden, zoals 'het' of 'en' in het Engels)</span><span class="sxs-lookup"><span data-stu-id="fde34-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="fde34-194">Een samengestelde woord in onderdelen op te splitsen</span><span class="sxs-lookup"><span data-stu-id="fde34-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="fde34-195">Kleine hoofdlettergebruik van een woord hoofdletters</span><span class="sxs-lookup"><span data-stu-id="fde34-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="fde34-196">Al deze bewerkingen vaak tooerase verschillen tussen Hallo tekstinvoer geleverd door het Hallo-gebruiker en Hallo voorwaarden opgeslagen in het Hallo-index.</span><span class="sxs-lookup"><span data-stu-id="fde34-196">All of these operations tend tooerase differences between hello text input provided by hello user and hello terms stored in hello index.</span></span> <span data-ttu-id="fde34-197">Dergelijke bewerkingen voorbij de verwerking van tekst en vereisen diepgaande kennis van Hallo taal zelf.</span><span class="sxs-lookup"><span data-stu-id="fde34-197">Such operations go beyond text processing and require in-depth knowledge of hello language itself.</span></span> <span data-ttu-id="fde34-198">tooadd deze laag van de taalkundige awareness, Azure Search ondersteunt een lange lijst met [taalanalyse](https://docs.microsoft.com/rest/api/searchservice/language-support) van Lucene en van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fde34-198">tooadd this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="fde34-199">Vereisten voor analyse kunnen variëren van minimale tooelaborate afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="fde34-199">Analysis requirements can range from minimal tooelaborate depending on your scenario.</span></span> <span data-ttu-id="fde34-200">U kunt de complexiteit van lexicale analyse beheren door Hallo een vooraf gedefinieerde Hallo analyzers te selecteren of door het maken van uw eigen [aangepaste analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="fde34-200">You can control complexity of lexical analysis by hello selecting one of hello predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="fde34-201">Analyzers bereik toosearchable velden zijn en worden opgegeven als onderdeel van de velddefinitie van een.</span><span class="sxs-lookup"><span data-stu-id="fde34-201">Analyzers are scoped toosearchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="fde34-202">Hiermee kunt u toovary lexicale analyse op basis van de per-veld.</span><span class="sxs-lookup"><span data-stu-id="fde34-202">This allows you toovary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="fde34-203">Hallo niet is opgegeven, *standaard* Lucene analyzer wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fde34-203">Unspecified, hello *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="fde34-204">In ons voorbeeld voorafgaande tooanalysis Hallo eerste querystructuur heeft Hallo term 'Spacious' met een hoofdletter "S" en een komma die queryparser Hallo wordt geïnterpreteerd als een deel van de zoekterm hello (een door komma's wordt niet beschouwd als een query language-operator).</span><span class="sxs-lookup"><span data-stu-id="fde34-204">In our example, prior tooanalysis, hello initial query tree has hello term "Spacious," with an uppercase "S" and a comma that hello query parser interprets as a part of hello query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="fde34-205">Wanneer Hallo standaard analyzer Hallo term verwerkt, wordt deze kleine letters 'Oceaan weergeven' en 'groot' en Hallo kommateken verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fde34-205">When hello default analyzer processes hello term, it will lowercase "ocean view" and "spacious", and remove hello comma character.</span></span> <span data-ttu-id="fde34-206">Hallo gewijzigde querystructuur ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="fde34-206">hello modified query tree will look as follows:</span></span> 

 ![Booleaanse query geanalyseerde voorwaarden][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="fde34-208">Analyzer gedrag testen</span><span class="sxs-lookup"><span data-stu-id="fde34-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="fde34-209">Hallo-gedrag van een analyzer kan worden getest met Hallo [analyseren API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="fde34-209">hello behavior of an analyzer can be tested using hello [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="fde34-210">Geef Hallo tekst tooanalyze toosee welke vermeldingen analyzer wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-210">Provide hello text you want tooanalyze toosee what terms given analyzer will generate.</span></span> <span data-ttu-id="fde34-211">Bijvoorbeeld, hoe Hallo standaard analyzer zou verwerken toosee Hallo tekst 'air-condition', kunt u de volgende aanvraag Hallo uitgeven:</span><span class="sxs-lookup"><span data-stu-id="fde34-211">For example, toosee how hello standard analyzer would process hello text "air-condition", you can issue hello following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="fde34-212">de ingevoerde tekst hello Hallo standaard analyzer opgesplitst in Hallo na twee tokens, aantekeningen te maken met kenmerken zoals begin en einde offsets (gebruikt voor het markeren van treffers), evenals hun positie (gebruikt voor de zinsnede overeenkomende):</span><span class="sxs-lookup"><span data-stu-id="fde34-212">hello standard analyzer breaks hello input text into hello following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

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

### <a name="exceptions-toolexical-analysis"></a><span data-ttu-id="fde34-213">Uitzonderingen toolexical analyse</span><span class="sxs-lookup"><span data-stu-id="fde34-213">Exceptions toolexical analysis</span></span> 

<span data-ttu-id="fde34-214">Lexicale analysis geldt alleen tooquery typen waarvoor volledige voorwaarden – een term query of een woordgroep-query.</span><span class="sxs-lookup"><span data-stu-id="fde34-214">Lexical analysis applies only tooquery types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="fde34-215">Het tooquery typen met onvolledige voorwaarden – voorvoegsel query, jokertekens query, regex query – of tooa fuzzy query niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="fde34-215">It doesn’t apply tooquery types with incomplete terms – prefix query, wildcard query, regex query – or tooa fuzzy query.</span></span> <span data-ttu-id="fde34-216">De querytypen, inclusief Hallo voorvoegsel query met term *air-condition\**  in ons voorbeeld toegevoegd rechtstreeks toohello querystructuur Hallo analysis fase overslaan.</span><span class="sxs-lookup"><span data-stu-id="fde34-216">Those query types, including hello prefix query with term *air-condition\** in our example, are added directly toohello query tree, bypassing hello analysis stage.</span></span> <span data-ttu-id="fde34-217">Hallo is alleen transformatie uitgevoerd op de voorwaarden van deze typen query lowercasing.</span><span class="sxs-lookup"><span data-stu-id="fde34-217">hello only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="fde34-218">Stap 3: Document ophalen</span><span class="sxs-lookup"><span data-stu-id="fde34-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="fde34-219">Ophalen van het document verwijst toofinding documenten met overeenkomende voorwaarden in Hallo index.</span><span class="sxs-lookup"><span data-stu-id="fde34-219">Document retrieval refers toofinding documents with matching terms in hello index.</span></span> <span data-ttu-id="fde34-220">Deze fase is beste begrepen door een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fde34-220">This stage is understood best through an example.</span></span> <span data-ttu-id="fde34-221">Laten we beginnen met een index hotels met Hallo eenvoudige schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="fde34-221">Let's start with a hotels index having hello following simple schema:</span></span> 

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

<span data-ttu-id="fde34-222">Verder wordt ervan uitgegaan dat deze index bevat Hallo vier documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="fde34-222">Further assume that this index contains hello following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
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

<span data-ttu-id="fde34-223">**Hoe voorwaarden worden geïndexeerd**</span><span class="sxs-lookup"><span data-stu-id="fde34-223">**How terms are indexed**</span></span>

<span data-ttu-id="fde34-224">ophalen van toounderstand helpt tooknow enkele basisbeginselen van het indexeren.</span><span class="sxs-lookup"><span data-stu-id="fde34-224">toounderstand retrieval, it helps tooknow a few basics about indexing.</span></span> <span data-ttu-id="fde34-225">Hallo-eenheid voor opslag is een omgekeerde index, één voor elk doorzoekbaar veld.</span><span class="sxs-lookup"><span data-stu-id="fde34-225">hello unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="fde34-226">Is een gesorteerde lijst van alle voorwaarden van alle documenten in een omgekeerde index.</span><span class="sxs-lookup"><span data-stu-id="fde34-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="fde34-227">Elke term maps toohello lijst van documenten waarin zich, zo duidelijk in Hallo in het volgende voorbeeld voordoet.</span><span class="sxs-lookup"><span data-stu-id="fde34-227">Each term maps toohello list of documents in which it occurs, as evident in hello example below.</span></span>

<span data-ttu-id="fde34-228">tooproduce hello voorwaarden in een omgekeerde index Hallo zoekmachine voert lexicale analyse over de inhoud van documenten, Hallo vergelijkbare toowhat er gebeurt tijdens het verwerken van query's.</span><span class="sxs-lookup"><span data-stu-id="fde34-228">tooproduce hello terms in an inverted index, hello search engine performs lexical analysis over hello content of documents, similar toowhat happens during query processing.</span></span> <span data-ttu-id="fde34-229">Tekst invoer worden doorgegeven tooan analyzer, geïntegreerd in een kleine, enz., afhankelijk van Hallo analyzer configuratie en leestekens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fde34-229">Text inputs are passed tooan analyzer, lower-cased, stripped of punctuation, and so forth, depending on hello analyzer configuration.</span></span> <span data-ttu-id="fde34-230">Het algemene, maar niet vereist is, toouse Hallo dezelfde analyzers voor zoeken en indexeren operations zodat querytermen zoals voorwaarden binnen Hallo index meer uitzien.</span><span class="sxs-lookup"><span data-stu-id="fde34-230">It's common, but not required, toouse hello same analyzers for search and indexing operations so that query terms look more like terms inside hello index.</span></span>

> [!Note]
> <span data-ttu-id="fde34-231">Azure Search kunt u verschillende analyzers voor indexeren opgeven en zoek via aanvullende `indexAnalyzer` en `searchAnalyzer` veld parameters.</span><span class="sxs-lookup"><span data-stu-id="fde34-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="fde34-232">Als u niets opgeeft, Hallo analyzer ingesteld met Hallo `analyzer` eigenschap wordt gebruikt voor het indexeren en het zoeken.</span><span class="sxs-lookup"><span data-stu-id="fde34-232">If unspecified, hello analyzer set with hello `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="fde34-233">**Omgekeerde index voor voorbeelddocumenten**</span><span class="sxs-lookup"><span data-stu-id="fde34-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="fde34-234">Retourneren van tooour zo kan voor Hallo **titel** veld Hallo omgekeerde index ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="fde34-234">Returning tooour example, for hello **title** field, hello inverted index looks like this:</span></span>

| <span data-ttu-id="fde34-235">Termijn</span><span class="sxs-lookup"><span data-stu-id="fde34-235">Term</span></span> | <span data-ttu-id="fde34-236">Lijst met standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="fde34-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="fde34-237">atman</span><span class="sxs-lookup"><span data-stu-id="fde34-237">atman</span></span> | <span data-ttu-id="fde34-238">1</span><span class="sxs-lookup"><span data-stu-id="fde34-238">1</span></span> |
| <span data-ttu-id="fde34-239">strand</span><span class="sxs-lookup"><span data-stu-id="fde34-239">beach</span></span> | <span data-ttu-id="fde34-240">2</span><span class="sxs-lookup"><span data-stu-id="fde34-240">2</span></span> |
| <span data-ttu-id="fde34-241">hotel</span><span class="sxs-lookup"><span data-stu-id="fde34-241">hotel</span></span> | <span data-ttu-id="fde34-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="fde34-242">1, 3</span></span> |
| <span data-ttu-id="fde34-243">Oceaan</span><span class="sxs-lookup"><span data-stu-id="fde34-243">ocean</span></span> | <span data-ttu-id="fde34-244">4</span><span class="sxs-lookup"><span data-stu-id="fde34-244">4</span></span>  |
| <span data-ttu-id="fde34-245">playa</span><span class="sxs-lookup"><span data-stu-id="fde34-245">playa</span></span> | <span data-ttu-id="fde34-246">3</span><span class="sxs-lookup"><span data-stu-id="fde34-246">3</span></span> |
| <span data-ttu-id="fde34-247">toevlucht</span><span class="sxs-lookup"><span data-stu-id="fde34-247">resort</span></span> | <span data-ttu-id="fde34-248">3</span><span class="sxs-lookup"><span data-stu-id="fde34-248">3</span></span> |
| <span data-ttu-id="fde34-249">Terugtrekken</span><span class="sxs-lookup"><span data-stu-id="fde34-249">retreat</span></span> | <span data-ttu-id="fde34-250">4</span><span class="sxs-lookup"><span data-stu-id="fde34-250">4</span></span> |

<span data-ttu-id="fde34-251">In Hallo titelveld alleen *hotel* wordt weergegeven in twee documenten: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="fde34-251">In hello title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="fde34-252">Voor Hallo **beschrijving** veld Hallo index is als volgt:</span><span class="sxs-lookup"><span data-stu-id="fde34-252">For hello **description** field, hello index is as follows:</span></span>

| <span data-ttu-id="fde34-253">Termijn</span><span class="sxs-lookup"><span data-stu-id="fde34-253">Term</span></span> | <span data-ttu-id="fde34-254">Lijst met standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="fde34-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="fde34-255">lucht</span><span class="sxs-lookup"><span data-stu-id="fde34-255">air</span></span> | <span data-ttu-id="fde34-256">3</span><span class="sxs-lookup"><span data-stu-id="fde34-256">3</span></span>
| <span data-ttu-id="fde34-257">en</span><span class="sxs-lookup"><span data-stu-id="fde34-257">and</span></span> | <span data-ttu-id="fde34-258">4</span><span class="sxs-lookup"><span data-stu-id="fde34-258">4</span></span>
| <span data-ttu-id="fde34-259">strand</span><span class="sxs-lookup"><span data-stu-id="fde34-259">beach</span></span> | <span data-ttu-id="fde34-260">1</span><span class="sxs-lookup"><span data-stu-id="fde34-260">1</span></span>
| <span data-ttu-id="fde34-261">voorwaarde</span><span class="sxs-lookup"><span data-stu-id="fde34-261">conditioned</span></span> | <span data-ttu-id="fde34-262">3</span><span class="sxs-lookup"><span data-stu-id="fde34-262">3</span></span>
| <span data-ttu-id="fde34-263">vertrouwd</span><span class="sxs-lookup"><span data-stu-id="fde34-263">comfortable</span></span> | <span data-ttu-id="fde34-264">3</span><span class="sxs-lookup"><span data-stu-id="fde34-264">3</span></span>
| <span data-ttu-id="fde34-265">afstand</span><span class="sxs-lookup"><span data-stu-id="fde34-265">distance</span></span> | <span data-ttu-id="fde34-266">1</span><span class="sxs-lookup"><span data-stu-id="fde34-266">1</span></span>
| <span data-ttu-id="fde34-267">eiland</span><span class="sxs-lookup"><span data-stu-id="fde34-267">island</span></span> | <span data-ttu-id="fde34-268">2</span><span class="sxs-lookup"><span data-stu-id="fde34-268">2</span></span>
| <span data-ttu-id="fde34-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="fde34-269">kauaʻi</span></span> | <span data-ttu-id="fde34-270">2</span><span class="sxs-lookup"><span data-stu-id="fde34-270">2</span></span>
| <span data-ttu-id="fde34-271">zich bevindt</span><span class="sxs-lookup"><span data-stu-id="fde34-271">located</span></span> | <span data-ttu-id="fde34-272">2</span><span class="sxs-lookup"><span data-stu-id="fde34-272">2</span></span>
| <span data-ttu-id="fde34-273">Noord</span><span class="sxs-lookup"><span data-stu-id="fde34-273">north</span></span> | <span data-ttu-id="fde34-274">2</span><span class="sxs-lookup"><span data-stu-id="fde34-274">2</span></span>
| <span data-ttu-id="fde34-275">Oceaan</span><span class="sxs-lookup"><span data-stu-id="fde34-275">ocean</span></span> | <span data-ttu-id="fde34-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="fde34-276">1, 2, 3</span></span>
| <span data-ttu-id="fde34-277">van</span><span class="sxs-lookup"><span data-stu-id="fde34-277">of</span></span> | <span data-ttu-id="fde34-278">2</span><span class="sxs-lookup"><span data-stu-id="fde34-278">2</span></span>
| <span data-ttu-id="fde34-279">op</span><span class="sxs-lookup"><span data-stu-id="fde34-279">on</span></span> |<span data-ttu-id="fde34-280">2</span><span class="sxs-lookup"><span data-stu-id="fde34-280">2</span></span>
| <span data-ttu-id="fde34-281">Stille</span><span class="sxs-lookup"><span data-stu-id="fde34-281">quiet</span></span> | <span data-ttu-id="fde34-282">4</span><span class="sxs-lookup"><span data-stu-id="fde34-282">4</span></span>
| <span data-ttu-id="fde34-283">ruimten</span><span class="sxs-lookup"><span data-stu-id="fde34-283">rooms</span></span>  | <span data-ttu-id="fde34-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="fde34-284">1, 3</span></span>
| <span data-ttu-id="fde34-285">secluded</span><span class="sxs-lookup"><span data-stu-id="fde34-285">secluded</span></span> | <span data-ttu-id="fde34-286">4</span><span class="sxs-lookup"><span data-stu-id="fde34-286">4</span></span>
| <span data-ttu-id="fde34-287">wal</span><span class="sxs-lookup"><span data-stu-id="fde34-287">shore</span></span> | <span data-ttu-id="fde34-288">2</span><span class="sxs-lookup"><span data-stu-id="fde34-288">2</span></span>
| <span data-ttu-id="fde34-289">groot</span><span class="sxs-lookup"><span data-stu-id="fde34-289">spacious</span></span> | <span data-ttu-id="fde34-290">1</span><span class="sxs-lookup"><span data-stu-id="fde34-290">1</span></span>
| <span data-ttu-id="fde34-291">Hallo</span><span class="sxs-lookup"><span data-stu-id="fde34-291">hello</span></span> | <span data-ttu-id="fde34-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="fde34-292">1, 2</span></span>
| <span data-ttu-id="fde34-293">te</span><span class="sxs-lookup"><span data-stu-id="fde34-293">too</span></span>| <span data-ttu-id="fde34-294">1</span><span class="sxs-lookup"><span data-stu-id="fde34-294">1</span></span>
| <span data-ttu-id="fde34-295">weergeven</span><span class="sxs-lookup"><span data-stu-id="fde34-295">view</span></span> | <span data-ttu-id="fde34-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="fde34-296">1, 2, 3</span></span>
| <span data-ttu-id="fde34-297">roulatie van</span><span class="sxs-lookup"><span data-stu-id="fde34-297">walking</span></span> | <span data-ttu-id="fde34-298">1</span><span class="sxs-lookup"><span data-stu-id="fde34-298">1</span></span>
| <span data-ttu-id="fde34-299">met</span><span class="sxs-lookup"><span data-stu-id="fde34-299">with</span></span> | <span data-ttu-id="fde34-300">3</span><span class="sxs-lookup"><span data-stu-id="fde34-300">3</span></span>


<span data-ttu-id="fde34-301">**Overeenkomende querytermen tegen geïndexeerde voorwaarden**</span><span class="sxs-lookup"><span data-stu-id="fde34-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="fde34-302">Hallo omgekeerd indexen bovenstaande gegeven, gaan we terug toohello voorbeeldquery en Zie hoe overeenkomende documenten zijn gevonden voor de voorbeeldquery.</span><span class="sxs-lookup"><span data-stu-id="fde34-302">Given hello inverted indices above, let’s return toohello sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="fde34-303">Intrekken dat Hallo laatste querybewerking structuur ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="fde34-303">Recall that hello final query tree looks like this:</span></span> 

 ![Booleaanse query geanalyseerde voorwaarden][4]

<span data-ttu-id="fde34-305">Tijdens het uitvoeren van query worden afzonderlijke query's uitgevoerd met de doorzoekbare velden Hallo onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="fde34-305">During query execution, individual queries are executed against hello searchable fields independently.</span></span> 

+ <span data-ttu-id="fde34-306">Hallo TermQuery 'groot' komt overeen met document 1 (Hotel Atman).</span><span class="sxs-lookup"><span data-stu-id="fde34-306">hello TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="fde34-307">Hallo PrefixQuery, ' air-condition * ', komt niet overeen met alle documenten.</span><span class="sxs-lookup"><span data-stu-id="fde34-307">hello PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="fde34-308">Dit is een probleem dat soms confuses ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="fde34-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="fde34-309">Hoewel Hallo term air-conditioned Hallo document bevat, is deze opgesplitst in twee termen door Hallo standaard analyzer.</span><span class="sxs-lookup"><span data-stu-id="fde34-309">Although hello term air-conditioned exists in hello document, it is split into two terms by hello default analyzer.</span></span> <span data-ttu-id="fde34-310">Intrekken voorvoegsel query's die voor gedeeltelijke termen bevatten, worden niet geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="fde34-311">Daarom voorwaarden met het voorvoegsel 'air-condition' worden opgezocht in Hallo omgekeerde index en niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="fde34-311">Therefore terms with prefix "air-condition" are looked up in hello inverted index and not found.</span></span>

+ <span data-ttu-id="fde34-312">Hallo PhraseQuery 'Oceaan weergave' Hallo voorwaarden "Oceaan" en "view" worden opgezocht en Hallo nabijheid van termen in het originele document Hallo controleert.</span><span class="sxs-lookup"><span data-stu-id="fde34-312">hello PhraseQuery, "ocean view", looks up hello terms "ocean" and "view" and checks hello proximity of terms in hello original document.</span></span> <span data-ttu-id="fde34-313">Documenten 1, 2 en 3 overeen met deze query in Hallo beschrijvingsveld.</span><span class="sxs-lookup"><span data-stu-id="fde34-313">Documents 1, 2 and 3 match this query in hello description field.</span></span> <span data-ttu-id="fde34-314">Kennisgeving document 4 Hallo term Oceaan in Hallo titel heeft, maar wordt niet beschouwd als een overeenkomst als we op zoek bent naar Hallo "view Oceaan" woordgroep in plaats van afzonderlijke woorden.</span><span class="sxs-lookup"><span data-stu-id="fde34-314">Notice document 4 has hello term ocean in hello title but isn’t considered a match, as we're looking for hello "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="fde34-315">Een zoekopdracht wordt onafhankelijk uitgevoerd tegen de doorzoekbare velden in Azure Search-index tenzij u beperken Hallo velden ingesteld met Hallo Hallo `searchFields` parameter, zoals geïllustreerd in de zoekaanvraag Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fde34-315">A search query is executed independently against all searchable fields in hello Azure Search index unless you limit hello fields set with hello `searchFields` parameter, as illustrated in hello example search request.</span></span> <span data-ttu-id="fde34-316">Documenten die overeenkomen met een Hallo geselecteerd velden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fde34-316">Documents that match in any of hello selected fields are returned.</span></span> 

<span data-ttu-id="fde34-317">Hallo-documenten die overeenkomen met zijn op Hallo hele voor Hallo query betrokken, 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="fde34-317">On hello whole, for hello query in question, hello documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="fde34-318">Stap 4: score berekenen</span><span class="sxs-lookup"><span data-stu-id="fde34-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="fde34-319">Elk document dat in een resultatenset search is een score relevantie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="fde34-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="fde34-320">Hallo-functie van Hallo relevantie score is toorank hoger die documenten best een gebruiker te beantwoorden vraag Hallo zoekquery uitgedrukt.</span><span class="sxs-lookup"><span data-stu-id="fde34-320">hello function of hello relevance score is toorank higher those documents that best answer a user question as expressed by hello search query.</span></span> <span data-ttu-id="fde34-321">Hallo-score wordt berekend op basis van statistische eigenschappen van de voorwaarden die overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="fde34-321">hello score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="fde34-322">Hallo core Hallo score berekenen voor de formule is [TF/IDF (frequentie term frequentie inverse document)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="fde34-322">At hello core of hello scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="fde34-323">In de query's met zeldzame en algemene voorwaarden, bevordert TF/IDF Hallo zeldzame term met resultaten.</span><span class="sxs-lookup"><span data-stu-id="fde34-323">In queries containing rare and common terms, TF/IDF promotes results containing hello rare term.</span></span> <span data-ttu-id="fde34-324">Bijvoorbeeld in een hypothetische index met alle artikelen voor Wikipedia (Engelstalig) van de documenten die query overeenkomende hello *Hallo directeur*, documenten die overeenkomen met op *directeur* worden beschouwd als meer dan relevante documenten die overeenkomen met op *de*.</span><span class="sxs-lookup"><span data-stu-id="fde34-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched hello query *hello president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="fde34-325">Score berekenen voor voorbeeld</span><span class="sxs-lookup"><span data-stu-id="fde34-325">Scoring example</span></span>

<span data-ttu-id="fde34-326">Hallo drie documenten die overeenkomen met onze voorbeeldquery intrekken:</span><span class="sxs-lookup"><span data-stu-id="fde34-326">Recall hello three documents that matched our example query:</span></span>
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
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
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
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="fde34-327">1 overeenkomende Hallo query beste document omdat beide Hallo term *groot* Hallo vereist wachtwoordzin *Oceaan weergave* in Hallo beschrijvingsveld optreden.</span><span class="sxs-lookup"><span data-stu-id="fde34-327">Document 1 matched hello query best because both hello term *spacious* and hello required phrase *ocean view* occur in hello description field.</span></span> <span data-ttu-id="fde34-328">de volgende twee documenten Hallo overeen met alleen Hallo woordgroep *Oceaan weergave*.</span><span class="sxs-lookup"><span data-stu-id="fde34-328">hello next two documents match only hello phrase *ocean view*.</span></span> <span data-ttu-id="fde34-329">Het kan worden verrast die Hallo relevantie score voor document 2 en 3 verschilt ondanks dat ze overeenkomen met Hallo-query in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="fde34-329">It might be surprising that hello relevance score for document 2 and 3 is different even though they matched hello query in hello same way.</span></span> <span data-ttu-id="fde34-330">Het is omdat Hallo score berekenen voor de formule meer onderdelen dan alleen TF/IDF bevat.</span><span class="sxs-lookup"><span data-stu-id="fde34-330">It's because hello scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="fde34-331">In dit geval document 3 die een enigszins hogere score is toegewezen, omdat de beschrijving korter is.</span><span class="sxs-lookup"><span data-stu-id="fde34-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="fde34-332">Meer informatie over [Lucene van praktische score berekenen voor de formule](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand hoe veldlengte en andere factoren kunnen invloed hebben op Hallo relevantie score.</span><span class="sxs-lookup"><span data-stu-id="fde34-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand how field length and other factors can influence hello relevance score.</span></span>

<span data-ttu-id="fde34-333">Sommige querytypen (jokerteken, voorvoegsel, regex) bijdragen altijd een constante score toohello totale score-document.</span><span class="sxs-lookup"><span data-stu-id="fde34-333">Some query types (wildcard, prefix, regex) always contribute a constant score toohello overall document score.</span></span> <span data-ttu-id="fde34-334">Hierdoor komt overeen met via query uitbreiding toobe opgenomen in het Hallo-resultaten, maar zonder Hallo ranking gevonden.</span><span class="sxs-lookup"><span data-stu-id="fde34-334">This allows matches found through query expansion toobe included in hello results, but without affecting hello ranking.</span></span> 

<span data-ttu-id="fde34-335">Een voorbeeld illustreert waarom dit is van belang.</span><span class="sxs-lookup"><span data-stu-id="fde34-335">An example illustrates why this matters.</span></span> <span data-ttu-id="fde34-336">Zoekopdrachten met jokertekens, met inbegrip van zoekopdrachten voor voorvoegsel, zijn niet-eenduidige per definitie omdat Hallo-invoer gedeeltelijke tekenreeks met mogelijke overeenkomsten op een zeer groot aantal verschillende voorwaarden is (Houd rekening met een invoer van het "rondleiding *" met overeenkomsten gevonden op 'rondleidingen', 'tourettes', en " tourmaline').</span><span class="sxs-lookup"><span data-stu-id="fde34-336">Wildcard searches, including prefix searches, are ambiguous by definition because hello input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="fde34-337">Opgegeven Hallo aard van deze resultaten, is er geen enkele manier tooreasonably afleiden welke voorwaarden vindt u meer dan andere waardevolle.</span><span class="sxs-lookup"><span data-stu-id="fde34-337">Given hello nature of these results, there is no way tooreasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="fde34-338">Om deze reden negeren we term frequenties wanneer resultaten scoren van typen jokerteken, voorvoegsel en regex-query's.</span><span class="sxs-lookup"><span data-stu-id="fde34-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="fde34-339">In een meerdelig zoekaanvraag met gedeeltelijke en volledige voorwaarden, resultaten van Hallo gedeeltelijke invoer met een constante zijn ingebouwd score tooavoid afwijking naar mogelijk onverwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="fde34-339">In a multi-part search request that includes partial and complete terms, results from hello partial input are incorporated with a constant score tooavoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="fde34-340">Score afstemmen</span><span class="sxs-lookup"><span data-stu-id="fde34-340">Score tuning</span></span>

<span data-ttu-id="fde34-341">Er zijn twee manieren tootune relevantie scores in Azure Search:</span><span class="sxs-lookup"><span data-stu-id="fde34-341">There are two ways tootune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="fde34-342">**Score berekenen voor profielen** promoveren van documenten in Hallo gerangschikte lijst met resultaten op basis van een reeks regels.</span><span class="sxs-lookup"><span data-stu-id="fde34-342">**Scoring profiles** promote documents in hello ranked list of results based on a set of rules.</span></span> <span data-ttu-id="fde34-343">In ons voorbeeld, kunnen we documenten die overeenkomen met in Hallo titelveld relevanter dan documenten die overeenkomen met in beschrijvingsveld Hallo overwegen.</span><span class="sxs-lookup"><span data-stu-id="fde34-343">In our example, we could consider documents that matched in hello title field more relevant than documents that matched in hello description field.</span></span> <span data-ttu-id="fde34-344">Bovendien kan er als onze index had een prijsveld voor elke hotel, documenten met lagere prijs promoveren.</span><span class="sxs-lookup"><span data-stu-id="fde34-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="fde34-345">Meer informatie hoe te[score berekenen voor profielen tooa search-index toevoegen.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="fde34-345">Learn more how too[add Scoring Profiles tooa search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="fde34-346">**Versterking** (alleen beschikbaar in de volledige Lucene-querysyntaxis Hallo) biedt een prestatieverbetering operator `^` die kunnen worden toegepast tooany deel uit van Hallo querystructuur.</span><span class="sxs-lookup"><span data-stu-id="fde34-346">**Term boosting** (available only in hello Full Lucene query syntax) provides a boosting operator `^` that can be applied tooany part of hello query tree.</span></span> <span data-ttu-id="fde34-347">In ons voorbeeld, in plaats van het zoeken op voorvoegsel Hallo *air-condition*\*, een kan zoeken naar een van beide Hallo exacte termen *air-condition* Hallo voorvoegsel maar documenten die overeenkomen met op Hallo exacte term hoger door toe te passen versterking toohello term query zijn gerangschikt: *lucht voorwaarde ^ 2 || AIR-condition**.</span><span class="sxs-lookup"><span data-stu-id="fde34-347">In our example, instead of searching on hello prefix *air-condition*\*, one could search for either hello exact term *air-condition* or hello prefix, but documents that match on hello exact term are ranked higher by applying boost toohello term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="fde34-348">Meer informatie over [versterking](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="fde34-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="fde34-349">Score berekenen voor in een gedistribueerde index</span><span class="sxs-lookup"><span data-stu-id="fde34-349">Scoring in a distributed index</span></span>

<span data-ttu-id="fde34-350">Alle indexen in Azure Search worden automatisch splitsen in meerdere shards, zodat ons tooquickly distribueren Hallo index over meerdere knooppunten tijdens service schaal omhoog of omlaag schalen.</span><span class="sxs-lookup"><span data-stu-id="fde34-350">All indexes in Azure Search are automatically split into multiple shards, allowing us tooquickly distribute hello index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="fde34-351">Wanneer een zoekaanvraag is uitgegeven, wordt deze onafhankelijk tegen elke shard verstrekt.</span><span class="sxs-lookup"><span data-stu-id="fde34-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="fde34-352">Hallo worden resultaten van elke shard vervolgens samengevoegd en geordend op score (als er geen andere volgorde gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="fde34-352">hello results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="fde34-353">Het is belangrijk tooknow die Hallo scoreprofiel functie gewichten query term frequentie tegen de inverse document frequentie in alle documenten in de shard hello, niet over de breedte van alle shards.</span><span class="sxs-lookup"><span data-stu-id="fde34-353">It is important tooknow that hello scoring function weights query term frequency against its inverse document frequency in all documents within hello shard, not across all shards!</span></span>

<span data-ttu-id="fde34-354">Dit betekent dat een score relevantie *kan* zijn verschillend voor identieke documenten als ze zich op andere shards bevinden.</span><span class="sxs-lookup"><span data-stu-id="fde34-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="fde34-355">Deze verschillen vaak gelukkig toodisappear wanneer het aantal documenten in index Hallo Hallo vanwege toomore zelfs term distributie groeit.</span><span class="sxs-lookup"><span data-stu-id="fde34-355">Fortunately, such differences tend toodisappear as hello number of documents in hello index grows due toomore even term distribution.</span></span> <span data-ttu-id="fde34-356">Het is niet mogelijk tooassume op welke shard een document wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="fde34-356">It’s not possible tooassume on which shard any given document will be placed.</span></span> <span data-ttu-id="fde34-357">Echter, ervan uitgaande dat de documentsleutel van een niet wijzigen, deze wordt altijd toegewezen toohello dezelfde shard.</span><span class="sxs-lookup"><span data-stu-id="fde34-357">However, assuming a document key doesn't change, it will always be assigned toohello same shard.</span></span>

<span data-ttu-id="fde34-358">Document score is in het algemeen niet aanbevolen Hallo-kenmerk voor het ordenen van documenten als stabiliteit van de volgorde belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="fde34-358">In general, document score is not hello best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="fde34-359">Bijvoorbeeld, gezien twee document met een identieke score, er is geen garantie waarvoor een eerste wordt weergegeven in latere runs Hallo dezelfde query.</span><span class="sxs-lookup"><span data-stu-id="fde34-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of hello same query.</span></span> <span data-ttu-id="fde34-360">Document score alleen geeft een algemeen beeld van het document relevantie relatieve tooother documenten in de resultatenset Hallo.</span><span class="sxs-lookup"><span data-stu-id="fde34-360">Document score should only give a general sense of document relevance relative tooother documents in hello results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="fde34-361">Conclusie</span><span class="sxs-lookup"><span data-stu-id="fde34-361">Conclusion</span></span>

<span data-ttu-id="fde34-362">Hallo succes van zoekmachines internet heeft verwachtingen voor zoeken in volledige tekst gegenereerd via persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="fde34-362">hello success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="fde34-363">Voor vrijwel elke soort zoekervaring nu naar verwachting krijgt Hallo-engine toounderstand onze bedoeling, zelfs wanneer de voorwaarden zijn getypt of zijn onvolledig.</span><span class="sxs-lookup"><span data-stu-id="fde34-363">For almost any kind of search experience, we now expect hello engine toounderstand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="fde34-364">We verwachten mogelijk zelfs op basis van in de buurt vergelijkbare termen of synoniemen die we hebben nooit echt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fde34-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="fde34-365">Zoekopdracht in volledige tekst is van een technisch oogpunt zeer complex is of waarvoor geavanceerde analyses van de taalkundige en een tooprocessing systematisch op een manier die distill, vouw en transformeren query voorwaarden toodeliver een relevante resultaat.</span><span class="sxs-lookup"><span data-stu-id="fde34-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach tooprocessing in ways that distill, expand, and transform query terms toodeliver a relevant result.</span></span> <span data-ttu-id="fde34-366">Opgegeven Hallo inherente complexiteit, zijn er veel factoren die van invloed kunnen zijn op Hallo uitkomst van een query.</span><span class="sxs-lookup"><span data-stu-id="fde34-366">Given hello inherent complexities, there are a lot of factors that can affect hello outcome of a query.</span></span> <span data-ttu-id="fde34-367">Om deze reden biedt investeren Hallo tijd toounderstand Hallo mechanisme van zoeken in volledige tekst concrete voordelen bij het toowork via onverwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="fde34-367">For this reason, investing hello time toounderstand hello mechanics of full text search offers tangible benefits when trying toowork through unexpected results.</span></span>  

<span data-ttu-id="fde34-368">In dit artikel verkend zoeken in volledige tekst in de context Hallo van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fde34-368">This article explored full text search in hello context of Azure Search.</span></span> <span data-ttu-id="fde34-369">We hopen dat dit biedt u voldoende achtergrond toorecognize mogelijke oorzaken en oplossingen voor het adresseren van veelvoorkomende problemen van de query.</span><span class="sxs-lookup"><span data-stu-id="fde34-369">We hope it gives you sufficient background toorecognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fde34-370">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fde34-370">Next steps</span></span>

+ <span data-ttu-id="fde34-371">Hallo voorbeeld index bouwen, uitproberen verschillende query's en resultaten bekijken.</span><span class="sxs-lookup"><span data-stu-id="fde34-371">Build hello sample index, try out different queries and review results.</span></span> <span data-ttu-id="fde34-372">Zie voor instructies [bouwen en query uitvoeren op een index in de portal Hallo](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="fde34-372">For instructions, see [Build and query an index in hello portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="fde34-373">Probeer extra querysyntaxis van Hallo [documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) voorbeeld in deze sectie of van [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="fde34-373">Try additional query syntax from hello [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in hello portal.</span></span>

+ <span data-ttu-id="fde34-374">Bekijk [score berekenen voor profielen](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) als u wilt dat tootune classificeren in uw zoektoepassing.</span><span class="sxs-lookup"><span data-stu-id="fde34-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want tootune ranking in your search application.</span></span>

+ <span data-ttu-id="fde34-375">Meer informatie over hoe tooapply [taalspecifieke lexicale analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="fde34-375">Learn how tooapply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="fde34-376">[Configureren van aangepaste analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) voor minimale verwerking of speciale verwerking voor specifieke velden.</span><span class="sxs-lookup"><span data-stu-id="fde34-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="fde34-377">[Standard- en Engelse analyzers vergelijken](http://alice.unearth.ai/)) naast elkaar op deze demo-website.</span><span class="sxs-lookup"><span data-stu-id="fde34-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="fde34-378">Zie ook</span><span class="sxs-lookup"><span data-stu-id="fde34-378">See also</span></span>

[<span data-ttu-id="fde34-379">REST-API documenten zoeken</span><span class="sxs-lookup"><span data-stu-id="fde34-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="fde34-380">Vereenvoudigde querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="fde34-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="fde34-381">Volledige Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="fde34-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="fde34-382">Zoekresultaten verwerken</span><span class="sxs-lookup"><span data-stu-id="fde34-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
