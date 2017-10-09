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
# <a name="what-is-search-traffic-analytics"></a>Wat is search traffic analytics
Search traffic analytics is een patroon voor het implementeren van een Feedbacklus voor uw zoekservice. Dit patroon beschrijft Hallo gegevens die nodig zijn en hoe toocollect met behulp van Application Insights, een industrie-opvulteken voor het bewaken van services op meerdere platforms.

Search traffic analytics kunt u meer inzicht verkrijgen in uw zoekservice en inzicht in uw gebruikers en hun gedrag te ontgrendelen. Doordat de gegevens over wat uw gebruikers kiest, is het mogelijk toomake beslissingen die u uw zoekervaring en tooback uitschakelen wanneer Hallo resultaten worden verwacht niet verder te verbeteren.

Azure Search biedt een oplossing voor telemetrie die wordt geïntegreerd met Azure Application Insights en Power BI tooprovide uitgebreide bewaking en bijhouden. Omdat interactie met Azure Search alleen via API's is, moet Hallo telemetrie door Hallo ontwikkelaars zoekactie, Hallo-instructies in deze pagina worden geïmplementeerd.

## <a name="identify-hello-relevant-search-data"></a>Hallo relevante zoekquery gegevens identificeren

toohave nuttige zoekopdracht metrische gegevens en het benodigde toolog sommige signalen van gebruikers van zoektoepassing Hallo Hallo is. Deze signalen geven inhoud die gebruikers zijn geïnteresseerd zijn in en waarmee ze rekening houden met het relevante tootheir moet.

Er zijn twee signalen die Search Traffic Analytics moet:

1. Gebruiker gegenereerde zoekopdracht gebeurtenissen: alleen zoekquery's die zijn geïnitieerd door een gebruiker interessante zijn. Zoeken aanvragen gebruikt toopopulate facetten, aanvullende inhoud en ook geen interne informatie zijn niet belangrijk en leiden tot onjuiste en bijstelling van de resultaten.

2. Gebruiker gegenereerde klikt u op gebeurtenissen: door te klikken in dit document, verwijzen we tooa gebruiker selecteren van een bepaald zoekresultaat geretourneerd van een zoekopdracht. Een Klik in het algemeen betekent dat een document geen relevante resultaat voor een specifieke zoekopdracht.

Door te zoeken en klikt u op gebeurtenissen met een correlatie-id koppelen, is het mogelijk tooanalyze Hallo gedrag van gebruikers in uw toepassing. Deze zoekopdracht inzichten zijn onmogelijk tooobtain met alleen verkeer zoeklogboeken.

## <a name="how-tooimplement-search-traffic-analytics"></a>Hoe tooimplement traffic analytics zoeken

Hallo signalen worden vermeld in de voorgaande Hallo sectie moet worden verzameld van Hallo-zoektoepassing zoals hello wordt gebruikt. Application Insights is een uitbreidbaar bewakingsoplossing, beschikbaar voor meerdere platforms, flexibele instrumentation opties. Informatie over het gebruik van Application Insights kunt u profiteren van rapporten Hallo Power BI zoeken door Azure Search toomake Hallo analyse van gegevens eenvoudiger gemaakt.

In Hallo [portal](https://portal.azure.com) pagina voor uw Azure Search-service, Hallo Search Traffic Analytics blade bevat een referentieoverzicht voor het volgen van dit patroon telemetrie. U kunt ook selecteren of een Application Insights-resource maken. Zie Hallo benodigde gegevens op één plek.

![Search Traffic Analytics instructies][1]

### <a name="1-select-an-application-insights-resource"></a>1. Selecteer een Application Insights-resource

U moet een Application Insights-resource toouse tooselect of een maken als u nog niet hebt. U kunt een resource die al in gebruik toolog Hallo aangepaste gebeurtenissen vereist kunt gebruiken.

Wanneer u een nieuwe Application Insights-resource maakt, zijn alle toepassingstypen geldig voor dit scenario. Selecteer Hallo een die het beste past bij Hallo platform dat u gebruikt.

Hallo-instrumentatiesleutel moet u voor het maken van Hallo telemetrie-client voor uw toepassing. U kunt dit downloaden Hallo Application Insights-portal-dashboard of kunt u dit downloaden van Hallo Search Traffic Analytics pagina gewenste toouse Hallo-exemplaar selecteren.

### <a name="2-instrument-your-application"></a>2. Softwareontwikkelaars van uw toepassing

In deze fase is waar de softwareontwikkelaars van uw eigen zoektoepassing met behulp van Application Insights-resource Hallo uw Hallo worden gemaakt in stap hierboven. Er zijn vier stappen toothis proces:

**IK. Maken van een client telemetrie** dit Hallo-object dat wordt verzonden gebeurtenissen toohello Application Insights-Resource is.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Voor andere talen en platforms, raadpleegt u volledige Hallo [lijst](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Aanvraag een Search-ID voor correlatie** toocorrelate search-aanvragen met klikken, het benodigde toohave een correlatie-id die is gekoppeld van deze twee afzonderlijke gebeurtenissen is. Azure Search biedt een Search-Id wanneer u deze met een header aanvragen:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Logboekgebeurtenissen zoeken**

Elke keer dat een zoekaanvraag is uitgegeven door een gebruiker, u moet zich aanmelden die als een gebeurtenis zoeken Hello schema van een aangepaste gebeurtenis Application Insights te volgen:

**ServiceName**: (tekenreeks) service zoeknaam **zoekcode**: de unieke id (guid) van Hallo-zoekopdracht (komt in het antwoord van de zoekopdracht Hallo) **NaamCommunity**:-zoekindex service (tekenreeks) toobe opgevraagd **QueryTerms**: (tekenreeks) zoektermen ingevoerd door de gebruiker Hallo **ResultCount**: het aantal documenten die zijn geretourneerd (int) (wordt geleverd in het antwoord van de zoekopdracht Hallo)  **ScoringProfile**: naam Hallo score berekenen profiel gebruikt, indien van toepassing (tekenreeks)

> [!NOTE]
> Aantal aanvragen op de gebruiker gegenereerde query's door toe te voegen $count = true tooyour zoekopdracht. Zie voor meer informatie [hier](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Houd er rekening mee tooonly logboek zoekquery's die worden gegenereerd door gebruikers.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Meld u Klik gebeurtenissen**

Elke keer dat een gebruiker een document, dat een signaal dat moet worden geregistreerd voor analysedoeleinden zoekopdracht op. U gebruikt deze gebeurtenissen in het Application Insights aangepaste gebeurtenissen toolog Hello schema te volgen:

**ServiceName**: (tekenreeks) service zoeknaam **SearchId**: de unieke id (guid) van Hallo gerelateerde zoekquery **DocId**: document-id (tekenreeks) **positie** : (int) positie van document in de zoekopdracht Hallo Hallo resultaten pagina

> [!NOTE]
> Positie verwijst toohello kardinaalcurveverbindingslijn volgorde in uw toepassing. U staat op het gratis tooset telefoonnummer, zolang het is altijd Hallo dezelfde tooallow voor vergelijking.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Analyseren met Power BI Desktop

Nadat u hebt uw app geïnstrumenteerd en uw toepassing correct verbonden tooApplication Insights is geverifieerd, kunt u een vooraf gedefinieerde sjabloon is gemaakt met Azure Search voor Power BI desktop.
Deze sjabloon bevat grafieken en tabellen die u helpen u beter geïnformeerde beslissingen tooimprove prestaties en relevantie.

tooinstantiate hello Power BI desktop sjabloon, moet u drie soorten informatie over Application Insights. Deze gegevens vindt u in Hallo Search Traffic Analytics pagina wanneer u Hallo resource toouse selecteert

![Application Insights Data Hallo Search Traffic Analytics-blade][2]

Metrische gegevens in Power BI-bureaubladsjabloon Hallo opgenomen:

*   Klikt u op via snelheid (CTR): ratio van gebruikers die op een bepaald document toohello aantal totale zoekopdrachten.
*   Zoeken zonder te klikken: voorwaarden voor top-query's die geen klikken registreren
*   Meest geklikt documenten: meest geklikt documenten door-ID in Hallo afgelopen 24 uur, 7 dagen en 30 dagen.
*   Paren van populaire term-document: voorwaarden die resulteren in hetzelfde document hebt geklikt, Hallo geordend door te klikken.
*   Tijd tooclick: gerangschikte klikken door tijd sinds het Hallo-zoekopdracht

![Power BI-sjabloon voor het lezen van Application Insights][3]


## <a name="next-steps"></a>Volgende stappen
Uw zoekopdracht tooget krachtige en begrijpelijke manier mee toepassingsgegevens over uw zoekservice softwareontwikkelaars.

U vindt meer informatie over Application Insights [hier](https://go.microsoft.com/fwlink/?linkid=842905). Ga naar Application Insights [pagina met prijzen](https://azure.microsoft.com/pricing/details/application-insights/) toolearn meer informatie over de verschillende Servicelagen.

Meer informatie over het maken van fantastische rapporten. Zie [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) voor meer informatie

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
