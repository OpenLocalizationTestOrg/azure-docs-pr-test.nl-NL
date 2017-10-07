---
title: aaaDependency bijhouden in Azure Application Insights | Microsoft Docs
description: Analyseer het gebruik, de beschikbaarheid en de prestaties van uw on-premises webtoepassing of Microsoft Azure-webtoepassing met Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Application Insights instellen: afhankelijkheid bijhouden
Een *afhankelijkheid* is een externe component die wordt aangeroepen door uw app. Dit is doorgaans een service die is aangeroepen met behulp van HTTP, of een database of een bestandssysteem. [Application Insights](app-insights-overview.md) maatregelen hoe lang de toepassing moet wachten voor afhankelijkheden en hoe vaak een afhankelijkheidsaanroep is mislukt. U kunt specifieke aanroepen te onderzoeken en koppelen toorequests en uitzonderingen.

![voorbeeldgrafieken](./media/app-insights-asp-net-dependencies/10-intro.png)

Hallo out-of-the-box afhankelijkheidsmonitor rapporten momenteel aanroepen toothese typen afhankelijkheden:

* Server
  * SQL-databases
  * ASP.NET-webtoepassingen en WCF-services die gebruikmaken van bindingen op basis van HTTP
  * Lokale of externe HTTP-aanroepen
  * Azure DB Cosmos, tabel, blob-opslag en wachtrij
* Webpagina's
  * AJAX-aanroepen

Bewaking werkt met [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) rond geselecteerde methoden. Prestatieoverhead is minimaal.

U kunt ook schrijven uw eigen SDK-aanroepen toomonitor andere afhankelijkheden, zowel in Hallo client en server code met Hallo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Bewaking van afhankelijkheid ingesteld
Gedeeltelijke afhankelijkheidsgegevens worden automatisch verzameld door Hallo [Application Insights-SDK](app-insights-asp-net.md). tooget volledige gegevens, installeren de desbetreffende agent Hallo voor Hallo host-server.

| Platform | Installeren |
| --- | --- |
| IIS-Server |Beide [Status Monitor installeren op uw server](app-insights-monitor-performance-live-website-now.md) of [Upgrade van uw toepassing too.NET framework 4.6 of hoger](http://go.microsoft.com/fwlink/?LinkId=528259) en installeer Hallo [Application Insights-SDK](app-insights-asp-net.md) in uw app. |
| Azure Web App |In het Configuratiescherm voor web-app [Application Insights-blade open Hallo in uw web-app-Configuratiescherm](app-insights-azure-web-apps.md) en kies installeren als u wordt gevraagd. |
| Azure-Cloudservice |[Gebruik opstarttaak](app-insights-cloudservices.md) of [installeren .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>Waar gegevens voor toofind-afhankelijkheid
* [De toepassingstoewijzing](#application-map) visualiseren van afhankelijkheden tussen uw app en de aangrenzende onderdelen.
* [Prestaties, browser en fout blades](#performance-and-blades) server afhankelijkheidsgegevens worden weergegeven.
* [Blade browsers](#ajax-calls) AJAX-aanroepen vanuit de browsers van uw gebruikers bevat.
* [Klik door vanuit traag of mislukte aanvragen](#diagnose-slow-requests) toocheck hun afhankelijkheidsaanroepen.
* [Analytics](#analytics) gebruikte tooquery afhankelijkheidsgegevens kunnen worden.

## <a name="application-map"></a>Toepassingskaart
De toepassingstoewijzing fungeert als een visuele hulpmiddel toodiscovering afhankelijkheden tussen Hallo onderdelen van uw toepassing. Deze wordt automatisch gegenereerd vanuit Hallo telemetrie van uw app. Dit voorbeeld toont AJAX-aanroepen vanuit Hallo browser scripts en REST-aanroepen van Hallo server app-tootwo externe services.

![Toepassingskaart](./media/app-insights-asp-net-dependencies/08.png)

* **Navigeer in de vakken Hallo** toorelevant afhankelijkheid en andere grafieken.
* **Pincode Hallo kaart** toohello [dashboard](app-insights-dashboards.md), wordt waar deze volledig functioneel.

[Meer informatie](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Prestatie- en blades
de blade performance Hallo bevat Hallo duur van afhankelijkheidsaanroepen die zijn aangebracht door Hallo server app. Er is een overzichtstabel en een tabel gesegmenteerd op aanroep.

![Afhankelijkheid van de prestatiegrafieken-blade](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Klik in de samenvatting grafieken Hallo of Hallo tabel items toosearch onbewerkte instanties van deze aanroepen.

![Afhankelijkheid aanroep exemplaren](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Foutaantallen** worden weergegeven op Hallo **fouten** blade. Een mislukte is een retourcode die zich niet in Hallo bereik 200-399, of onbekend.

> [!NOTE]
> **100% fouten?** -Dit wordt waarschijnlijk geeft aan dat u alleen afhankelijkheidsgegevens van gedeeltelijke krijgt. U moet te[afhankelijkheid bewaking van de juiste tooyour platform instellen](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>AJAX-aanroepen
de blade Browsers Hallo toont Hallo duur en percentage mislukte AJAX-aanroepen van [JavaScript in uw webpagina's](app-insights-javascript.md). Deze worden weergegeven als afhankelijkheden.

## <a name="diagnosis"></a>Diagnose van trage aanvragen
Elke gebeurtenis van de aanvraag is gekoppeld aan afhankelijkheidsaanroepen hello, uitzonderingen en andere gebeurtenissen die worden bijgehouden, terwijl het verwerken van uw app Hallo aanvraag. Dus als bepaalde aanvragen onjuist uitvoert, kunt u vinden of dit is vanwege tooslow antwoorden van een afhankelijkheid.

We gaan een voorbeeld van die doorlopen.

### <a name="tracing-from-requests-toodependencies"></a>Tracering van aanvragen toodependencies
Open de blade Performance Hallo en bekijkt hello raster van aanvragen:

![Lijst met aanvragen met gemiddelden en tellingen](./media/app-insights-asp-net-dependencies/02-reqs.png)

Hallo boven op een zeer lang duurt. Laten we zien als we vindt waarbij Hallo tijd is besteed.

Klik op die rij toosee afzonderlijke gebeurtenissen:

![Lijst van instanties van de aanvraag](./media/app-insights-asp-net-dependencies/03-instances.png)

Klik op een langlopende exemplaar tooinspect deze nog verder en schuif naar beneden toohello externe afhankelijkheid aanroepen gerelateerde toothis aanvraag:

![Aanroepen tooRemote afhankelijkheden vinden, ongebruikelijke duur identificeren](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Het lijkt erop dat de meeste Hallo tijd onderhoud van die deze aanvraag is gespendeerd aan het gesprek tooa lokale service.

Meer informatie voor die rij tooget selecteren:

![Klik op de link die externe afhankelijkheid tooidentify Hallo stackpad](./media/app-insights-asp-net-dependencies/05-detail.png)

Lijkt erop dat dit is waar Hallo probleem is. Wij Hallo probleem hebt nauwkeurige, dus nu we zojuist hebt toofind uit waarom die aanroep te lang duurt.

### <a name="request-timeline"></a>Aanvraag tijdlijn
Er is geen afhankelijkheidsaanroep die is een bijzonder lange in andere gevallen. Maar door overschakelt naar de tijdlijnweergave toohello, kunnen we zien waar Hallo vertraging is opgetreden bij het verwerken van onze interne:

![Aanroepen tooRemote afhankelijkheden vinden, ongebruikelijke duur identificeren](./media/app-insights-asp-net-dependencies/04-1.png)

Er lijkt toobe een gap big na het eerste afhankelijkheidsaanroep hello, zodat we onze toosee code moet bekijken waarom is.

### <a name="profile-your-live-site"></a>Profiel van uw live site

Er is geen idee waar Hallo tijd gaat? Hallo [Application Insights profiler](app-insights-profiler.md) traceringen HTTP-live site tooyour aanroept en ziet u welke functies in uw code duurde Hallo langst.

## <a name="failed-requests"></a>Mislukte aanvragen
Mislukte aanvragen kunnen ook zijn gekoppeld aan toodependencies mislukte aanroepen. We kunnen opnieuw tootrack omlaag Hallo probleem doorklikken.

![Klik op Hallo mislukte aanvragen grafiek](./media/app-insights-asp-net-dependencies/06-fail.png)

Klik op tooan exemplaar van een mislukte aanvraag en de bijbehorende gebeurtenissen bekijken.

![Klik op een aanvraagtype, klikt u op Hallo tooget tooa verschillende instantieweergave van hetzelfde exemplaar hello, klikt u erop tooget uitzonderingsdetails.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analytische gegevens
U kunt volgen afhankelijkheden in Hallo [querytaal van logboekanalyse](https://docs.loganalytics.io/). Hier volgen enkele voorbeelden.

* Alle mislukte afhankelijkheidsaanroepen vinden:

```

    dependencies | where success != "True" | take 10
```

* AJAX-aanroepen vinden:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Afhankelijkheidsaanroepen verband met aanvragen zoeken:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Zoeken naar AJAX-aanroepen die zijn gekoppeld aan paginaweergaven:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Bijhouden van aangepaste afhankelijkheid
Hallo standaard afhankelijkheid bijhouden module detecteert automatisch de externe afhankelijkheden, zoals databases en REST-API's. Maar u kunt een aantal extra onderdelen toobe behandeld in Hallo dezelfde manier.

U kunt code schrijven waarmee afhankelijkheidsinformatie, verzendt met behulp van dezelfde Hallo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) dat wordt gebruikt door Hallo standaard modules.

Bijvoorbeeld, als u uw code met een assembly maken die u zelf niet schrijven, of u alle Hallo aanroepen tooit kan tijd, keren toofind uit wat de bijdrage tooyour antwoord maakt. toohave deze gegevens weergegeven in de afhankelijkheidsgrafiek Hallo in Application Insights verzenden met behulp van `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Als u tooswitch uit Hallo standaard afhankelijkheid bijhouden wilt, verwijdert u Hallo verwijzing tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Problemen oplossen
*Afhankelijkheid geslaagd vlag altijd toont waar of ONWAAR.*

*SQL-query is niet volledig worden weergegeven.*

* Meest recente versie van de toohello van Hallo SDK bijwerken. Als uw versie van .NET minder dan 4.6 is:
  * IIS-host: installeren [Application Insights-Agent](app-insights-monitor-performance-live-website-now.md) op Hallo-hostservers.
  * Azure-web-app: Open Application Insights tabblad Hallo web-app het Configuratiescherm en installeer Application Insights.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen
* [Uitzonderingen](app-insights-asp-net-exceptions.md)
* [Gebruiker- en paginagegevens toevoegen](app-insights-javascript.md)
* [Beschikbaarheid](app-insights-monitor-web-app-availability.md)
