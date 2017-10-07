---
title: aaaHow kan ik... in Azure Application Insights | Microsoft Docs
description: Veelgestelde vragen in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Hoe kan ik ... in Application Insights?
## <a name="get-an-email-when-"></a>Ontvang een e-mail wanneer...
### <a name="email-if-my-site-goes-down"></a>E-mailadres als Mijn site uitvalt
Stel een [beschikbaarheid WebTest](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>E-als Mijn site is overbelast
Stel een [waarschuwing](app-insights-alerts.md) op **serverreactietijd**. Een drempelwaarde tussen 1 en 2 seconden zouden moeten werken.

![](./media/app-insights-how-do-i/030-server.png)

Uw app mogelijk tekenen van stam ook weergeven door te retourneren van de fout-codes. Een waarschuwing instellen voor **mislukte aanvragen**.

Als u wilt dat een waarschuwing tooset op **serveruitzonderingen**, moet u wellicht toodo [enkele aanvullende instellingen](app-insights-asp-net-exceptions.md) in volgorde toosee gegevens.

### <a name="email-on-exceptions"></a>E-uitzonderingen op
1. [Uitzonderingenmonitor instellen](app-insights-asp-net-exceptions.md)
2. [Een waarschuwing instellen](app-insights-alerts.md) tellen metriek op Hallo uitzondering

### <a name="email-on-an-event-in-my-app"></a>E-mail bekijkt op een gebeurtenis in mijn app
Stel de gewenste tooget een e-mailbericht wanneer een bepaalde gebeurtenis plaatsvindt. Application Insights geen biedt deze mogelijkheid rechtstreeks, maar dit kan [een waarschuwing verzonden wanneer een metriek een drempelwaarde overschrijden](app-insights-alerts.md).

Waarschuwingen kunnen worden ingesteld voor [aangepaste metrische gegevens](app-insights-api-custom-events-metrics.md#trackmetric)echter geen aangepaste gebeurtenissen. Schrijf sommige tooincrease code een metriek bij Hallo-gebeurtenis:

    telemetry.TrackMetric("Alarm", 10);

Of:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Omdat waarschuwingen twee statussen hebben, hebt u toosend een lage waarde wanneer u rekening houden met Hallo waarschuwing toohave beëindigd:

    telemetry.TrackMetric("Alarm", 0.5);

Maken van een grafiek in [metrische explorer](app-insights-metrics-explorer.md) toosee uw alarm:

![](./media/app-insights-how-do-i/010-alarm.png)

Een waarschuwing toofire wordt nu ingesteld wanneer Hallo metriek hoger dan de waarde van een mid gedurende een korte periode is:

![](./media/app-insights-how-do-i/020-threshold.png)

Hallo gemiddelde periode toohello minimum ingesteld.

U krijgt e-mailberichten wanneer Hallo metriek boven gaat en onder de drempelwaarde Hallo.

Sommige tooconsider punten:

* Een waarschuwing heeft twee statussen ('waarschuwing' en 'goede'). Hallo staat alleen geëvalueerd wanneer een metriek is ontvangen.
* Een e-mailbericht wordt alleen verzonden wanneer Hallo status verandert. Dit is de reden waarom u toosend hebt metrische gegevens voor hoge en lage waarde.
* tooevaluate hello waarschuwing Hallo gemiddelde is overgenomen van Hallo ontvangen waarden Hallo voorgaande periode. Dit gebeurt telkens wanneer een metriek is ontvangen, zodat e-mailberichten vaker dan de ingestelde periode voor Hallo kunnen worden verzonden.
* Omdat e-mailberichten worden verzonden op 'waarschuwing' en 'goede', kunt u tooconsider opnieuw gegevensclassificatie uw eindresultaat gebeurtenis als een voorwaarde voor twee statussen. Bijvoorbeeld, in plaats van een gebeurtenis 'taak is voltooid' hebben een voorwaarde 'taak wordt uitgevoerd' waarop u e-mailberichten aan Hallo begin en einde van een taak ophalen.

### <a name="set-up-alerts-automatically"></a>Waarschuwingen automatisch instellen
[Gebruik PowerShell toocreate nieuwe waarschuwingen](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>PowerShell tooManage Application Insights gebruiken
* [Maken van nieuwe resources](app-insights-powershell-script-create-resource.md)
* [Nieuwe waarschuwingen maken](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Afzonderlijke telemetrie van verschillende versies

* Meerdere rollen in een app: gebruiken één Application Insights-resource en filtert u op cloud_Rolename. [Meer informatie](app-insights-monitor-multi-role-apps.md)
* Scheiden van ontwikkeling, testen en release-versies: verschillende Application Insights-bronnen worden gebruikt. Hallo instrumentatiesleutels uit web.config worden opgepikt. [Meer informatie](app-insights-separate-resources.md)
* Reporting bouwen versies: een eigenschap met een initialisatiefunctie telemetrie toevoegen. [Meer informatie](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Back-endservers en bureaublad-apps bewaken
[Gebruik de Windows Server SDK module Hallo](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Gegevens visualiseren
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Dashboard met metrische gegevens vanuit meerdere apps
* In [metriek Explorer](app-insights-metrics-explorer.md), de grafiek aanpassen en als favoriet opslaan. Toohello Azure-dashboard vastmaken.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Dashboard met gegevens uit andere bronnen en de Application Insights
* [Exporteren van telemetrie tooPower BI](app-insights-export-power-bi.md).

of

* SharePoint gebruiken als uw dashboard, het weergeven van gegevens in de SharePoint-webonderdelen. [Continue export en Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Gebruik PowerView tooexamine Hallo database en een SharePoint-webonderdeel voor PowerView maken.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Anonieme of geverifieerde gebruikers filteren
Als uw gebruikers zich aanmelden, kunt u instellen Hallo [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users). (Dit gebeurt niet automatisch.)

U kunt vervolgens:

* Zoeken naar specifieke gebruikers-id 's

![](./media/app-insights-how-do-i/110-search.png)

* Metrische gegevens tooeither anonieme of geverifieerde gebruikers filteren

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Wijzig de namen van eigenschappen of waarden
Maak een [filter](app-insights-api-filtering-sampling.md#filtering). Hiermee kunt u wijzigen of filteren van telemetrie voordat deze van uw app tooApplication Insights wordt verzonden.

## <a name="list-specific-users-and-their-usage"></a>Lijst van specifieke gebruikers en hun gebruik
Als u alleen te wilt[zoeken naar specifieke gebruikers](#search-specific-users), kunt u instellen dat Hallo [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users).

Als u wilt dat een lijst met gebruikers met gegevens zoals welke pagina's ze bekijken of hoe vaak deze zich aanmeldt, hebt u twee opties:

* [Set geverifieerde gebruiker-id](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa database exporteren](app-insights-code-sample-export-sql-stream-analytics.md) en geschikte gebruik hulpprogramma's tooanalyze er uw gebruikersgegevens.
* Als u slechts een klein aantal gebruikers hebt, aangepaste gebeurtenissen of metrische gegevens, met behulp van gegevens van belang Hallo Hallo metrische waarde of de gebeurtenisnaam van de en instelling Hallo gebruikers-id als een eigenschap verzenden. tooanalyze paginaweergaven vervangen Hallo standaard JavaScript trackPageView-aanroep. tooanalyze serverzijde telemetrie, een telemetrie telemetrie initialisatiefunctie tooadd Hallo gebruiker-id tooall server gebruiken. Vervolgens kunt u filteren en segment metrische gegevens en zoekopdrachten op Hallo gebruikers-id.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Verminderen het verkeer vanuit Mijn tooApplication app Insights
* In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), alle modules die u hoeft niet dergelijke Hallo prestaties teller collector uitschakelen.
* Gebruik [steekproeven en filteren](app-insights-api-filtering-sampling.md) op Hallo SDK.
* In uw webpagina's Hallo aantal voor elke paginaweergave gemelde Ajax-aanroepen te beperken. In de script-codefragment Hallo na `instrumentationKey:...` , invoegen: `,maxAjaxCallsPerView:3` (of een geschikte getal).
* Als u [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), Hallo aggregatie van batches van metrische waarden voor het verzenden van Hallo resultaat berekenen. Er is een overload van TrackMetric() die voor die biedt.

Meer informatie over [-prijzen en -quota](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Telemetrie uitschakelen
te**dynamisch stoppen en starten** Hallo verzamelen en verzenden van telemetrie van Hallo-server:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



te**uitschakelen geselecteerde standaard collectors** - prestatiemeteritems, bijvoorbeeld, HTTP-aanvragen of afhankelijkheden - verwijderen of Hallo relevante regels in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). U kan doen, bijvoorbeeld, als u uw eigen gegevens TrackRequest toosend wilt.

## <a name="view-system-performance-counters"></a>Systeemprestatiemeteritems weergeven
Tussen Hallo zijn metrische gegevens die u in metrics explorer weergeven kunt een reeks systeemprestatiemeteritems. Er is een vooraf gedefinieerde blade met de titel **Servers** waarin meerdere wordt weergegeven.

![Open uw Application Insights-resource en klik op Servers](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Als er geen gegevens van prestatiemeteritems
* **IIS-server** op uw computer of op een virtuele machine. [Statusmonitor installeren](app-insights-monitor-performance-live-website-now.md).
* **Azure-website** -prestatiemeteritems nog niet ondersteund. Er zijn verschillende metrische gegevens die u als standaardonderdeel van hello Azure-website in het Configuratiescherm krijgt.
* **UNIX-server** - [Installeer collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay meer prestatiemeteritems
* Eerst [toevoegen van een nieuwe grafiek](app-insights-metrics-explorer.md) en zien als Hallo teller in Hallo basic ingesteld wij bieden.
* Als dat niet het geval is, [hello toohello itemset verzameld door de module Hallo prestatiemeteritems toevoegen](app-insights-performance-counters.md).
