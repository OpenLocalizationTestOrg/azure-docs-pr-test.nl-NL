---
title: aaaAnalytics - Hallo krachtige zoekfunctie van Azure Application Insights | Microsoft Docs
description: 'Overzicht van Analytics, Hallo diagnostische gegevens doorzoeken krachtige hulpprogramma van Application Insights. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Analytics in Application Insights
[Analytics](app-insights-analytics.md) is Hallo krachtige zoekfunctie van [Application Insights](app-insights-overview.md). Deze pagina's worden de Log Analytics query language beschreven. 

* **[Hallo inleidende video bekijken](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet nog gegevens tooApplication Insights verzendt.
* **[SQL-gebruikers cheats blad](https://aka.ms/sql-analytics)**  Hallo meest voorkomende idioms vertaalt.
* **[Taalreferentie](app-insights-analytics-reference.md)**  meer informatie over hoe toouse alle andere van krachtige functies Hallo Log Analytics-querytaal Hallo.


## <a name="queries-in-analytics"></a>Query's in Analytics
Een typische query is een *bron* tabel gevolgd door een reeks *operators* gescheiden door `|`. 

Bijvoorbeeld, we willen weten welk tijdstip van de dag Hallo burgers van Hyderabad probeert de web-app. En hoewel we er, gaan we kijken welke resultaatcodes tootheir HTTP-aanvragen worden geretourneerd. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

We tellen afzonderlijke client-IP-adressen, ze groeperen per uur van de dag Hallo Hallo via Hallo afgelopen 7 dagen. 

> [!NOTE]
> tooget resultaten buiten Hallo vorige 24 uur, 'tijdstempel' expliciet opnemen in uw query of Hallo tijd bereik vervolgkeuzelijst gebruiken.
>

Laten we Hallo resultaten Hello balk grafiek presentatie toostack Hallo resultaten kiezen uit andere reactiecodes weergeven:

![Kies staafdiagram, x en y-as en segmentering](./media/app-insights-analytics/020.png)

Lijkt erop dat de app op lunchpauze en insluiten-tijd in Hyderabad populairste is. (En gaan we deze 500 codes).

Er zijn ook krachtige statistische bewerkingen:

![Resultaten van statistische query](./media/app-insights-analytics/025.png)

Hallo taal heeft veel voordelen bieden:


* [Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) uw app onbewerkte telemetrie op alle velden, met inbegrip van uw aangepaste eigenschappen en metrische gegevens.
* [Deelnemen aan](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) meerdere tabellen – correleer aanvragen met paginaweergaven, afhankelijkheidsaanroepen, uitzonderingen en logboektraceringen.
* Krachtige statistische [aggregaties](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Net zo krachtig zijn als SQL, maar veel eenvoudiger voor complexe query's: in plaats van geneste instructies u Hallo gegevens uit een elementaire bewerking toohello doorsluizen naast.
* Onmiddellijke en krachtige visualisaties.
* [Pincode grafieken tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).
* [Exporteren van query's tooPower BI](app-insights-analytics-using.md#export-to-power-bi).
* Er is een [REST-API](https://dev.applicationinsights.io/) waarmee u toorun query's via een programma, bijvoorbeeld via Powershell kunt.


## <a name="connect-tooyour-application-insights-data"></a>Verbinding maken met gegevens van de Application Insights tooyour
Analytics openen vanuit uw app [overzichtsblade](app-insights-dashboards.md) in Application Insights: 

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Query-voorbeelden

Probeer een van deze scenario's tooillustrate Hallo power Analytics gebruiken:

 *  [Automatische diagnoses van pieken en stap gaat in aanvragen duur](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analyse van prestaties degradations met time series-analyse](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Problemen met toepassingen met autocluster en diffpatterns analyseren](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Geavanceerde vorm detecties met time series-analyse](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Met behulp van verschuivende venster operations tooanalyze toepassingsgebruik (rolling MAU/DAU enzovoort)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Detectie van de serviceonderbrekingen op basis van de analyse van Logboeken voor foutopsporing](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) en een overeenkomende blogbericht [hier](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Profileren van de prestaties van toepassingen met behulp van Logboeken voor eenvoudige foutopsporing](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Hallo duur voor elke stap in uw code-stroom met eenvoudige foutopsporingslogboeken meten](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analyseren met behulp van Logboeken voor eenvoudige foutopsporing gelijktijdigheid](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Volgende stappen
* Het is raadzaam u begint met de Hallo [taal rondleiding](app-insights-analytics-tour.md). 
* Informatie over [met Analytics](app-insights-analytics-using.md). 
* [Taalreferentie](app-insights-analytics-reference.md). 
