---
title: aaaSearch Traffic Analytics voor Azure Search | Microsoft Docs
description: Schakel Search traffic analytics voor Azure Search, een zoekservice in de cloud gehoste in Microsoft Azure toounlock inzicht in uw gebruikers en uw gegevens.
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="365eb-103">Wat is search traffic analytics</span><span class="sxs-lookup"><span data-stu-id="365eb-103">What is search traffic analytics</span></span>
<span data-ttu-id="365eb-104">Search traffic analytics is een patroon voor het implementeren van een Feedbacklus voor uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="365eb-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="365eb-105">Dit patroon beschrijft Hallo gegevens die nodig zijn en hoe toocollect met behulp van Application Insights, een industrie-opvulteken voor het bewaken van services op meerdere platforms.</span><span class="sxs-lookup"><span data-stu-id="365eb-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="365eb-106">Search traffic analytics kunt u meer inzicht verkrijgen in uw zoekservice en inzicht in uw gebruikers en hun gedrag te ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="365eb-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="365eb-107">Doordat de gegevens over wat uw gebruikers kiest, is het mogelijk toomake beslissingen die u uw zoekervaring en tooback uitschakelen wanneer Hallo resultaten worden verwacht niet verder te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="365eb-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="365eb-108">Azure Search biedt een oplossing voor telemetrie die wordt geïntegreerd met Azure Application Insights en Power BI tooprovide uitgebreide bewaking en bijhouden.</span><span class="sxs-lookup"><span data-stu-id="365eb-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="365eb-109">Omdat interactie met Azure Search alleen via API's is, moet Hallo telemetrie door Hallo ontwikkelaars zoekactie, Hallo-instructies in deze pagina worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="365eb-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="365eb-110">Hallo relevante zoekquery gegevens identificeren</span><span class="sxs-lookup"><span data-stu-id="365eb-110">Identify hello relevant search data</span></span>

<span data-ttu-id="365eb-111">toohave nuttige zoekopdracht metrische gegevens en het benodigde toolog sommige signalen van gebruikers van zoektoepassing Hallo Hallo is.</span><span class="sxs-lookup"><span data-stu-id="365eb-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="365eb-112">Deze signalen geven inhoud die gebruikers zijn geïnteresseerd zijn in en waarmee ze rekening houden met het relevante tootheir moet.</span><span class="sxs-lookup"><span data-stu-id="365eb-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="365eb-113">Er zijn twee signalen die Search Traffic Analytics moet:</span><span class="sxs-lookup"><span data-stu-id="365eb-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="365eb-114">Gebruiker gegenereerde zoekopdracht gebeurtenissen: alleen zoekquery's die zijn geïnitieerd door een gebruiker interessante zijn.</span><span class="sxs-lookup"><span data-stu-id="365eb-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="365eb-115">Zoeken aanvragen gebruikt toopopulate facetten, aanvullende inhoud en ook geen interne informatie zijn niet belangrijk en leiden tot onjuiste en bijstelling van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="365eb-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="365eb-116">Gebruiker gegenereerde klikt u op gebeurtenissen: door te klikken in dit document, verwijzen we tooa gebruiker selecteren van een bepaald zoekresultaat geretourneerd van een zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="365eb-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="365eb-117">Een Klik in het algemeen betekent dat een document geen relevante resultaat voor een specifieke zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="365eb-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="365eb-118">Door te zoeken en klikt u op gebeurtenissen met een correlatie-id koppelen, is het mogelijk tooanalyze Hallo gedrag van gebruikers in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="365eb-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="365eb-119">Deze zoekopdracht inzichten zijn onmogelijk tooobtain met alleen verkeer zoeklogboeken.</span><span class="sxs-lookup"><span data-stu-id="365eb-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="365eb-120">Hoe tooimplement traffic analytics zoeken</span><span class="sxs-lookup"><span data-stu-id="365eb-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="365eb-121">Hallo signalen worden vermeld in de voorgaande Hallo sectie moet worden verzameld van Hallo-zoektoepassing zoals hello wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="365eb-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="365eb-122">Application Insights is een uitbreidbaar bewakingsoplossing, beschikbaar voor meerdere platforms, flexibele instrumentation opties.</span><span class="sxs-lookup"><span data-stu-id="365eb-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="365eb-123">Informatie over het gebruik van Application Insights kunt u profiteren van rapporten Hallo Power BI zoeken door Azure Search toomake Hallo analyse van gegevens eenvoudiger gemaakt.</span><span class="sxs-lookup"><span data-stu-id="365eb-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="365eb-124">In Hallo [portal](https://portal.azure.com) pagina voor uw Azure Search-service, Hallo Search Traffic Analytics blade bevat een referentieoverzicht voor het volgen van dit patroon telemetrie.</span><span class="sxs-lookup"><span data-stu-id="365eb-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="365eb-125">U kunt ook selecteren of een Application Insights-resource maken. Zie Hallo benodigde gegevens op één plek.</span><span class="sxs-lookup"><span data-stu-id="365eb-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Search Traffic Analytics instructies][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="365eb-127">1. Selecteer een Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="365eb-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="365eb-128">U moet een Application Insights-resource toouse tooselect of een maken als u nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="365eb-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="365eb-129">U kunt een resource die al in gebruik toolog Hallo aangepaste gebeurtenissen vereist kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="365eb-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="365eb-130">Wanneer u een nieuwe Application Insights-resource maakt, zijn alle toepassingstypen geldig voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="365eb-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="365eb-131">Selecteer Hallo een die het beste past bij Hallo platform dat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="365eb-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="365eb-132">Hallo-instrumentatiesleutel moet u voor het maken van Hallo telemetrie-client voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="365eb-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="365eb-133">U kunt dit downloaden Hallo Application Insights-portal-dashboard of kunt u dit downloaden van Hallo Search Traffic Analytics pagina gewenste toouse Hallo-exemplaar selecteren.</span><span class="sxs-lookup"><span data-stu-id="365eb-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="365eb-134">2. Softwareontwikkelaars van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="365eb-134">2. Instrument your application</span></span>

<span data-ttu-id="365eb-135">In deze fase is waar de softwareontwikkelaars van uw eigen zoektoepassing met behulp van Application Insights-resource Hallo uw Hallo worden gemaakt in stap hierboven.</span><span class="sxs-lookup"><span data-stu-id="365eb-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="365eb-136">Er zijn vier stappen toothis proces:</span><span class="sxs-lookup"><span data-stu-id="365eb-136">There are four steps toothis process:</span></span>

<span data-ttu-id="365eb-137">**IK. Maken van een client telemetrie** dit Hallo-object dat wordt verzonden gebeurtenissen toohello Application Insights-Resource is.</span><span class="sxs-lookup"><span data-stu-id="365eb-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="365eb-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="365eb-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="365eb-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="365eb-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="365eb-140">Voor andere talen en platforms, raadpleegt u volledige Hallo [lijst](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="365eb-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="365eb-141">**II. Aanvraag een Search-ID voor correlatie** toocorrelate search-aanvragen met klikken, het benodigde toohave een correlatie-id die is gekoppeld van deze twee afzonderlijke gebeurtenissen is.</span><span class="sxs-lookup"><span data-stu-id="365eb-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="365eb-142">Azure Search biedt een Search-Id wanneer u deze met een header aanvragen:</span><span class="sxs-lookup"><span data-stu-id="365eb-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="365eb-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="365eb-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="365eb-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="365eb-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="365eb-145">**III. Logboekgebeurtenissen zoeken**</span><span class="sxs-lookup"><span data-stu-id="365eb-145">**III. Log Search events**</span></span>

<span data-ttu-id="365eb-146">Elke keer dat een zoekaanvraag is uitgegeven door een gebruiker, u moet zich aanmelden die als een gebeurtenis zoeken Hello schema van een aangepaste gebeurtenis Application Insights te volgen:</span><span class="sxs-lookup"><span data-stu-id="365eb-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="365eb-147">**ServiceName**: (tekenreeks) service zoeknaam **zoekcode**: de unieke id (guid) van Hallo-zoekopdracht (komt in het antwoord van de zoekopdracht Hallo) **NaamCommunity**:-zoekindex service (tekenreeks) toobe opgevraagd **QueryTerms**: (tekenreeks) zoektermen ingevoerd door de gebruiker Hallo **ResultCount**: het aantal documenten die zijn geretourneerd (int) (wordt geleverd in het antwoord van de zoekopdracht Hallo)  **ScoringProfile**: naam Hallo score berekenen profiel gebruikt, indien van toepassing (tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="365eb-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="365eb-148">Aantal aanvragen op de gebruiker gegenereerde query's door toe te voegen $count = true tooyour zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="365eb-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="365eb-149">Zie voor meer informatie [hier](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="365eb-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="365eb-150">Houd er rekening mee tooonly logboek zoekquery's die worden gegenereerd door gebruikers.</span><span class="sxs-lookup"><span data-stu-id="365eb-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="365eb-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="365eb-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="365eb-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="365eb-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="365eb-153">**IV. Meld u Klik gebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="365eb-153">**IV. Log Click events**</span></span>

<span data-ttu-id="365eb-154">Elke keer dat een gebruiker een document, dat een signaal dat moet worden geregistreerd voor analysedoeleinden zoekopdracht op.</span><span class="sxs-lookup"><span data-stu-id="365eb-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="365eb-155">U gebruikt deze gebeurtenissen in het Application Insights aangepaste gebeurtenissen toolog Hello schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="365eb-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="365eb-156">**ServiceName**: (tekenreeks) service zoeknaam **SearchId**: de unieke id (guid) van Hallo gerelateerde zoekquery **DocId**: document-id (tekenreeks) **positie** : (int) positie van document in de zoekopdracht Hallo Hallo resultaten pagina</span><span class="sxs-lookup"><span data-stu-id="365eb-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="365eb-157">Positie verwijst toohello kardinaalcurveverbindingslijn volgorde in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="365eb-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="365eb-158">U staat op het gratis tooset telefoonnummer, zolang het is altijd Hallo dezelfde tooallow voor vergelijking.</span><span class="sxs-lookup"><span data-stu-id="365eb-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="365eb-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="365eb-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="365eb-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="365eb-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="365eb-161">3. Analyseren met Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="365eb-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="365eb-162">Nadat u hebt uw app geïnstrumenteerd en uw toepassing correct verbonden tooApplication Insights is geverifieerd, kunt u een vooraf gedefinieerde sjabloon is gemaakt met Azure Search voor Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="365eb-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="365eb-163">Deze sjabloon bevat grafieken en tabellen die u helpen u beter geïnformeerde beslissingen tooimprove prestaties en relevantie.</span><span class="sxs-lookup"><span data-stu-id="365eb-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="365eb-164">tooinstantiate hello Power BI desktop sjabloon, moet u drie soorten informatie over Application Insights.</span><span class="sxs-lookup"><span data-stu-id="365eb-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="365eb-165">Deze gegevens vindt u in Hallo Search Traffic Analytics pagina wanneer u Hallo resource toouse selecteert</span><span class="sxs-lookup"><span data-stu-id="365eb-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Application Insights Data Hallo Search Traffic Analytics-blade][2]

<span data-ttu-id="365eb-167">Metrische gegevens in Power BI-bureaubladsjabloon Hallo opgenomen:</span><span class="sxs-lookup"><span data-stu-id="365eb-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="365eb-168">Klikt u op via snelheid (CTR): ratio van gebruikers die op een bepaald document toohello aantal totale zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="365eb-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="365eb-169">Zoeken zonder te klikken: voorwaarden voor top-query's die geen klikken registreren</span><span class="sxs-lookup"><span data-stu-id="365eb-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="365eb-170">Meest geklikt documenten: meest geklikt documenten door-ID in Hallo afgelopen 24 uur, 7 dagen en 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="365eb-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="365eb-171">Paren van populaire term-document: voorwaarden die resulteren in hetzelfde document hebt geklikt, Hallo geordend door te klikken.</span><span class="sxs-lookup"><span data-stu-id="365eb-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="365eb-172">Tijd tooclick: gerangschikte klikken door tijd sinds het Hallo-zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="365eb-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Power BI-sjabloon voor het lezen van Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="365eb-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="365eb-174">Next Steps</span></span>
<span data-ttu-id="365eb-175">Uw zoekopdracht tooget krachtige en begrijpelijke manier mee toepassingsgegevens over uw zoekservice softwareontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="365eb-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="365eb-176">U vindt meer informatie over Application Insights [hier](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="365eb-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="365eb-177">Ga naar Application Insights [pagina met prijzen](https://azure.microsoft.com/pricing/details/application-insights/) toolearn meer informatie over de verschillende Servicelagen.</span><span class="sxs-lookup"><span data-stu-id="365eb-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="365eb-178">Meer informatie over het maken van fantastische rapporten.</span><span class="sxs-lookup"><span data-stu-id="365eb-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="365eb-179">Zie [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="365eb-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
