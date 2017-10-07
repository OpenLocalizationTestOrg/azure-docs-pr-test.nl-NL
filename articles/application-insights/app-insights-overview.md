---
title: de AAA wat is Azure Application Insights? | Microsoft Docs
description: Dit is een service waarmee u de prestaties van toepassingen kunt beheren en het gebruik van uw livewebtoepassing kunt bijhouden.  Met deze service kunt u problemen detecteren, prioriteren en onderzoeken en inzicht krijgen in de manier waarop mensen uw app gebruiken.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a>Wat is Application Insights?
Application Insights is een uitbreidbare APM-service (Application Performance Management) voor webontwikkelaars op meerdere platforms. Gebruik deze toomonitor uw live-webtoepassing. Afwijkende prestaties worden automatisch gedetecteerd. Dit omvat krachtige analytics extra toohelp onderzoeken van problemen en toounderstand met uw app daadwerkelijk wat gebruikers doen.  Het ontworpen toohelp u continu prestaties en bruikbaarheid verbeteren. De Tool werkt voor apps gehost op een groot aantal verschillende platforms, waaronder .NET, Node.js en J2EE, lokaal of in de cloud Hallo. Het kan worden geïntegreerd met uw devOps-proces en heeft verbinding punten tooa aantal ontwikkelingsprogramma's.

![Breng statistieken van gebruikersactiviteiten in kaart of zoom in op specifieke gebeurtenissen.](./media/app-insights-overview/00-sample.png)

[Bekijk het introductiefilmpje hello](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>Hoe werkt Application Insights?
U een kleine instrumentation pakket installeren in uw toepassing en een Application Insights-resource in Microsoft Azure-portal Hallo instellen. Hallo instrumentation bewaakt van uw app en verzendt telemetrie toohello gegevensportal. (overal kan worden uitgevoerd door de toepassing hello - heeft geen toobe gehost in Azure.)

U kunt niet alleen webservicetoepassing hello, maar ook alle onderdelen van de achtergrond softwareontwikkelaars en Hallo JavaScript in Hallo webpagina's zelf. 

![Application Insights instrumentatie in uw app verzendt telemetrie tooyour Application Insights-resource.](./media/app-insights-overview/01-scheme.png)


U kunt bovendien ophalen van telemetrie van de hostomgevingen Hallo zoals prestatiemeteritems of Azure diagnostics Docker-Logboeken. U kunt ook webtests die regelmatig synthetische aanvragen tooyour webservice verzenden instellen.

Alle deze stromen telemetrie zijn geïntegreerd in de Azure-portal, waar u krachtige kunt toepassen Hallo analytische en zoeken extra toohello onbewerkte gegevens.


### <a name="whats-hello-overhead"></a>Wat is de overhead Hallo?
Hallo impact op de prestaties van uw app is erg klein. De aanroepen voor het bijhouden van het appgebruik blokkeren uw app niet en worden batchgewijs in een afzonderlijke thread verzonden.

## <a name="what-does-application-insights-monitor"></a>Wat wordt er door Application Insights gecontroleerd?

Application Insights is gericht op Hallo ontwikkelingsteam, toohelp u begrijpen hoe uw app wordt uitgevoerd en hoe deze wordt gebruikt. Met deze service kunt u het volgende controleren:

* **Aantal aanvragen, reactietijden en foutpercentages** - ga na welke pagina's het populairst zijn op welke tijdstippen van de dag en waar uw gebruikers zich bevinden. Ontdek welke pagina's het beste presteren. Als uw reactietijden en foutpercentages omhoog gaan wanneer er meer aanvragen binnenkomen, hebt u mogelijk te weinig resources. 
* **Aantal afhankelijkheidsrelaties, reactietijden en foutpercentages** - controleer of externe services zorgen voor vertraging.
* **Uitzonderingen** - Analyse Hallo geaggregeerd statistieken, of Kies specifieke exemplaren en inzoomen Hallo stacktracering en verwante aanvragen. Zowel server- als browseruitzonderingen worden gerapporteerd.
* **Paginaweergaven en de prestaties bij het laden van pagina’s** - deze gegevens worden gerapporteerd door de browsers van uw gebruikers.
* **AJAX-aanroepen** van webpagina's - ga na wat het aantal aanroepen, de reactietijden en de foutpercentages zijn.
* **Aantal gebruikers en sessies**.
* **Prestatiemeteritems** van uw Windows- of Linux-servers, zoals die voor CPU-, geheugen- en netwerkgebruik. 
* **Diagnostische gegevens van hosts** van Docker of Azure. 
* **Diagnostische traceerlogboeken** van uw app - met behulp hiervan kunt u de samenhang vaststellen tussen traceergebeurtenissen en aanvragen.
* **Aangepaste gebeurtenissen en metrische gegevens** dat u uzelf in Hallo client of server code, tootrack zakelijke gebeurtenissen schrijven zoals artikelen verkocht of games gewonnen.

## <a name="where-do-i-see-my-telemetry"></a>Waar kan ik mijn telemetrie bekijken?

Er zijn tal van manieren tooexplore uw gegevens. Lees de volgende artikelen:

|  |  |
| --- | --- |
| [**Slimme detectie en handmatige waarschuwingen**](app-insights-proactive-diagnostics.md)<br/>Automatische waarschuwingen aan te passen van tooyour app normale patronen van Telemetrie en trigger wanneer er iets buiten Hallo gebruikelijke patroon. U kunt ook [waarschuwingen instellen](app-insights-alerts.md) voor bepaalde niveaus van aangepaste functies of standaardfuncties voor het verzamelen van metrische gegevens. |![Voorbeeld van een waarschuwing](./media/app-insights-overview/alerts-tn.png) |
| [**Overzicht van de toepassing**](app-insights-app-map.md)<br/>Hallo-onderdelen van uw app, met de belangrijkste metrische gegevens en waarschuwingen. |![Overzicht van de toepassing](./media/app-insights-overview/appmap-tn.png)  |
| [**Profiler**](app-insights-profiler.md)<br/>Hallo uitvoering profielen opgevangen aanvragen te controleren. |![Profiler](./media/app-insights-overview/profiler.png) |
| [**Gebruiksanalyse**](app-insights-usage-overview.md)<br/>Analyseer de segmentatie en retentie van gebruikers.|![Retentie-informatie](./media/app-insights-overview/retention.png) |
| [**Diagnostische zoekactie naar gegevens van bepaalde items**](app-insights-diagnostic-search.md)<br/>U kunt zoeken naar gebeurtenissen, zoals aanvragen, uitzonderingen, afhankelijkheidsaanroepen, logboektraceringen en paginaweergaven en deze gegevens ook filteren.  |![Zoeken in telemetrie](./media/app-insights-overview/search-tn.png) |
| [**Metrics Explorer voor cumulatieve gegevens**](app-insights-metrics-explorer.md)<br/>Verken, filter en segmenteer cumulatieve gegevens, zoals aantallen aanvragen, fouten en uitzonderingen, reactietijden en paginalaadtijden. |![Metrische gegevens](./media/app-insights-overview/metrics-tn.png) |
| [**Dashboards**](app-insights-dashboards.md#dashboards)<br/>Combineer gegevens van meerdere resources tot een mash-up en deel deze met anderen. Dit is ideaal voor toepassingen met meerdere onderdelen en continue weergegeven in de Hallo team ruimte. |![Voorbeelden van dashboards](./media/app-insights-overview/dashboard-tn.png) |
| [**Live Metrics Stream**](app-insights-live-stream.md)<br/>Wanneer u een nieuwe build implementeert, bekijk deze indicatoren toomake voor prestaties near-realtime controleren of alles werkt zoals verwacht. |![Voorbeeld van metrische livegegevens](./media/app-insights-overview/live-metrics-tn.png) |
| [**Analytics**](app-insights-analytics.md)<br/>Beantwoord moeilijke vragen over de prestaties en het gebruik van uw app met behulp van deze krachtige querytaal. |![Voorbeeld van Analytics](./media/app-insights-overview/analytics-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>Zie prestatiegegevens op Hallo-code. Ga toocode van stack-traces.|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Snapshot Debugger**](app-insights-snapshot-debugger.md)<br/>Spoor fouten op in momentopnamen van live activiteiten, inclusief parameterwaarden.|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Integreer metrische gegevens over het gebruik van de toepassing met andere business intelligence.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**REST API**](https://dev.applicationinsights.io/)<br/>Schrijf code toorun query's via uw metrische gegevens en de onbewerkte gegevens.| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [**Continue export**](app-insights-export-telemetry.md)<br/>Het exporteren van de onbewerkte gegevens toostorage bulksgewijs zodra deze binnenkomen. |![Exporteren](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Hoe kan ik Application Insights gebruiken?

### <a name="monitor"></a>Bewaken
Installeer Application Insights in uw app, stel de [beschikbaarheidswebtests](app-insights-monitor-web-app-availability.md) in en ga als volgt te werk:

* Instellen van een [dashboard](app-insights-dashboards.md) voor uw team ruimte tookeep een ogen op load, reactiesnelheid en prestaties van uw afhankelijkheden hello, pagina belasting en AJAX-aanroepen.
* Ontdek welke Hallo traagste en de meeste mislukte aanvragen zijn.
* Bekijk [Live Stream](app-insights-live-stream.md) wanneer u een nieuwe release tooknow onmiddellijk over een verslechtering van implementeert.

### <a name="detect-diagnose"></a>Fouten detecteren en een diagnose stellen
Ga als volgt te werk als u een waarschuwing ontvangt of een probleem detecteert:

* Beoordeel hoeveel gebruikers last hebben van het probleem.
* Ga na of er een verband is tussen fouten en uitzonderingen, afhankelijkheidsaanroepen en traceringen.
* Bekijk de informatie van Profiler, momentopnamen, stackdumps en traceerlogboeken.

### <a name="build-measure-learn"></a>Meten is weten
[Hallo effectiviteit meten](app-insights-usage-overview.md) van elke nieuwe functie die u implementeert.

* Toomeasure plannen hoe klanten nieuwe UX- of business-functies gebruiken.
* Schrijf aangepaste telemetrie in uw code.
* Base Hallo volgende ontwikkeling bladeren op vaste bewijs van uw telemetrie.

## <a name="get-started"></a>Aan de slag
Application Insights is een Hallo veel services die worden gehost in Microsoft Azure en telemetrie er verzonden voor analyse en presentatie. Voordat u iets anders doen, u hoeft dus een abonnement te[Microsoft Azure](http://azure.com). Deze gratis toosign actief is en als u ervoor kiest Hallo basic [prijzen plan](https://azure.microsoft.com/pricing/details/application-insights/) van Application Insights, er zijn geen kosten tot uw toepassing toohave aanzienlijke gebruik is geworden. Als uw organisatie al een abonnement heeft, kunnen ze de tooit van uw Microsoft-account toevoegen.

Er zijn verschillende manieren tooget gestart. Begin op de manier die voor u het beste werkt. U kunt ook Hallo anderen later toevoegen.

* **Uitvoeringstijd at: uw web-app op Hallo-server te instrumenteren.** Update toohello code voorkomt. U moet een beheerserver toegang tooyour.
  * [**IIS on-premises of op een VM**](app-insights-monitor-performance-live-website-now.md)
  * [**Azure web-app of VM**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **Op tijdstip development: Application Insights tooyour code toevoegen.** Hiermee kunt u toowrite aangepaste Telemetrie en tooinstrument back-end en bureaublad-apps.
  * [Visual Studio](app-insights-asp-net.md) 2013 update 2 of hoger.
  * Java in [Eclipse](app-insights-java-eclipse.md) of [andere hulpprogramma’s](app-insights-java-get-started.md)
  * [Node.js](app-insights-nodejs.md)
  * [Andere platforms](app-insights-platforms.md)
* **[Instrumenteer uw webpagina’s](app-insights-javascript.md)** voor paginaweergaven, AJAX-aanroepen en andere telemetrie op de clientzijde.
* **[Beschikbaarheidstests](app-insights-monitor-web-app-availability.md)** - ping uw website regelmatig vanaf onze servers.


## <a name="next-steps"></a>Volgende stappen
Gebruik tijdens runtime:

* [IIS-server](app-insights-monitor-performance-live-website-now.md)
* [J2EE-server](app-insights-java-live.md)

Gebruik tijdens het ontwikkelen:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Ondersteuning en feedback
* Vragen en problemen:
  * [Problemen oplossen][qna]
  * [MSDN-forum](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Uw suggesties:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Application Insights-blog](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Video's

[![Introductievideo](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
