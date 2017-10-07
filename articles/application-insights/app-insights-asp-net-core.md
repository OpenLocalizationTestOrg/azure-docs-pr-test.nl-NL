---
title: Application Insights voor ASP.NET Core aaaAzure | Microsoft Docs
description: Bewaken van webtoepassingen voor beschikbaarheid, prestaties en het gebruik.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Application Insights voor ASP.NET Core
[Application Insights](app-insights-overview.md) kunt u uw webtoepassing voor beschikbaarheid, prestaties en gebruik te bewaken. Hallo feedback die u over Hallo prestaties en de effectiviteit van uw app in Hallo wilde krijgen, kunt u beslissen Hallo richting van het Hallo-ontwerp in elke ontwikkelingscyclus.

![Voorbeeld](./media/app-insights-asp-net-core/sample.png)

U hebt een abonnement met [Microsoft Azure](http://azure.com). Meld u aan met een Microsoft-account, dat u mogelijk al hebt voor Windows, XBox Live of andere Microsoft-cloudservices. Uw team wellicht een organisatie-abonnement tooAzure: Hallo eigenaar tooadd vraag tooit u met uw Microsoft-account.

## <a name="getting-started"></a>Aan de slag

* In Visual Studio Solution Explorer met de rechtermuisknop op uw project en selecteer **Configure Application Insights**, of **toevoegen > Application Insights**. [Meer informatie](app-insights-asp-net.md).
* Als u deze opdrachten niet ziet, voert u de Hallo [handmatige aan de slag](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Mogelijk moet u toodo dit als uw project is gemaakt met een versie van Visual Studio voordat 2017.

## <a name="using-application-insights"></a>Application Insights gebruiken
Meld u aan bij Hallo [Microsoft Azure-portal](https://portal.azure.com), selecteer **alle Resources** of **Application Insights**, en selecteer vervolgens Hallo resource u toomonitor uw app hebt gemaakt.

Gebruik uw app een tijdje in een apart browservenster. Hier ziet u gegevens verschijnen in Hallo Application Insights-grafieken. (U wellicht tooclick vernieuwen.) Er is een kleine hoeveelheid gegevens terwijl u ontwikkelt, maar deze grafieken echt tot leven komen wanneer u uw app publiceren en veel gebruikers hebben. 

overzichtspagina Hallo toont prestatiegrafieken: serverreactietijd, paginalaadtijd en tellingen van mislukte aanvragen. Klik op een grafiek toosee meer grafieken en gegevens.

Weergaven in de portal Hallo kunnen worden onderverdeeld in drie hoofdcategorieën:

* [Metrics Explorer](app-insights-metrics-explorer.md) grafieken en tabellen van de metrische gegevens en aantallen zoals reactietijden, uitvalpercentage of metrische gegevens ziet u zelf maken met de Hallo [API](app-insights-api-custom-events-metrics.md). Filter en segment Hallo-gegevens door de eigenschap waarden tooget een beter inzicht in uw app en de gebruikers.
* [Zoek Explorer](app-insights-diagnostic-search.md) geeft een lijst van afzonderlijke gebeurtenissen, zoals een specifieke aanvragen, uitzonderingen, logboektraceringen of gebeurtenissen die u zelf hebt gemaakt met de Hallo [API](app-insights-api-custom-events-metrics.md). Filteren op Hallo gebeurtenissen zoeken en navigeren tussen gerelateerde gebeurtenissen tooinvestigate problemen.
* [Analytics](app-insights-analytics.md) kunt u SQL-achtige query's uitvoeren via uw Telemetrie en is een krachtig analytische en diagnostische hulpprogramma.

## <a name="alerts"></a>Waarschuwingen
* Automatisch [proactieve diagnostische waarschuwingen](app-insights-proactive-diagnostics.md) waarmee wordt aangegeven dat u over afwijkende wijzigingen in uitvalpercentage en andere metrische gegevens.
* Instellen van [beschikbaarheidstests](app-insights-monitor-web-app-availability.md) tootest e-mails met uw website voortdurend van locaties wereldwijd en get zodra een mislukt test.
* Instellen van [metrische waarschuwingen](app-insights-monitor-web-app-availability.md) tooknow als metrische gegevens zoals reactietijden of uitzondering tarieven buiten acceptabele grenzen gaat.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Open source
[Lezen en bij te dragen toohello code](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Volgende stappen
* [Voeg telemetrie tooyour webpagina's](app-insights-javascript.md) toomonitor pagina gebruik en prestaties.
* [Afhankelijkheden bewaken](app-insights-asp-net-dependencies.md) toosee als REST, SQL of andere externe bronnen u vertragen.
* [Hallo-API gebruiken](app-insights-api-custom-events-metrics.md) toosend uw eigen gebeurtenissen en metrische gegevens voor een meer gedetailleerde weergave van de prestaties en het gebruik van uw app.
* [Beschikbaarheidstests](app-insights-monitor-web-app-availability.md) controleren van uw app continu uit Hallo wereld. 

