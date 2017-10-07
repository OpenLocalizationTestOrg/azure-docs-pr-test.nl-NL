---
title: aaaAzure Veelgestelde vragen over de Application Insights | Microsoft Docs
description: Veelgestelde vragen over Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: Veelgestelde vragen

## <a name="configuration-problems"></a>Configuratieproblemen
*Ik ondervind problemen met het instellen van mijn:*

* [.NET-app](app-insights-asp-net-troubleshoot-no-data.md)
* [Bewaking van een app al actief](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Azure diagnostics](app-insights-azure-diagnostics.md)
* [Java-web-app](app-insights-java-troubleshoot.md)

*Ik heb ophalen geen gegevens uit mijn server*

* [Set firewall-uitzonderingen](app-insights-ip-addresses.md)
* [Een ASP.NET-server instellen](app-insights-monitor-performance-live-website-now.md)
* [Een Java-server instellen](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Kan ik Application Insights met... gebruiken?

* [Web-apps op een IIS-server - op-premises of in een virtuele machine](app-insights-asp-net.md)
* [Java-web-apps](app-insights-java-get-started.md)
* [Node.js-apps](app-insights-nodejs.md)
* [Web-apps in Azure](app-insights-azure-web-apps.md)
* [Cloudservices op Azure](app-insights-cloudservices.md)
* [Appservers die in Docker](app-insights-docker.md)
* [Single-page-web-apps](app-insights-javascript.md)
* [SharePoint](app-insights-sharepoint.md)
* [Windows-bureaublad-app](app-insights-windows-desktop.md)
* [Andere platforms](app-insights-platforms.md)

## <a name="is-it-free"></a>Is het gratis?

Ja, voor experimenteel gebruik. In Hallo basic prijzen plan, kan uw toepassing een bepaalde toegestane gegevens elke maand gratis verzenden. Hallo gratis tegoed is groot genoeg toocover ontwikkeling en publiceren van een app voor een klein aantal gebruikers. U kunt een cap tooprevent meer dan een opgegeven hoeveelheid gegevens instellen worden verwerkt.

Grotere volumes telemetrie door Hallo Gb in rekening worden gebracht. We enkele tips voor het te bieden[uw kosten beperken](app-insights-pricing.md).

Hallo-enterpriseplan leidt ertoe dat kosten met zich mee voor elke dag dat elke webserverknooppunt telemetrie verzendt. Het is geschikt als u wilt dat toouse continue Export op grote schaal.

[Lees Hallo prijzen plan](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Hoeveel is deze kosten

* Open Hallo **functies en prijzen** pagina in een Application Insights-resource. Er is een overzicht van recente informatie over het gebruik. Als u wilt, kunt u een limiet van het volume gegevens instellen.
* Open Hallo [blade facturering Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee rekeningen over alle resources.

## <a name="q14"></a>Wat Application Insights in mijn project wijzigen?
Hallo-details zijn afhankelijk van Hallo type project. Voor een webtoepassing:

* Deze bestanden tooyour project toegevoegd:

  * ApplicationInsights.config.
  * AI.js
* Installeert deze NuGet-pakketten:

  * *Application Insights-API* - hello core-API
  * *Application Insights-API voor webtoepassingen* -toosend telemetrie van Hallo-server gebruikt
  * *Application Insights-API voor JavaScript toepassingen* -toosend telemetrie van Hallo-client gebruikt

    hello-pakketten bevatten deze assembly's:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Hiermee voegt items in:

  * Web.config
  * Packages.config
* (Nieuwe alleen - projecten als u [Application Insights tooan bestaand project toevoegen][start], hebt u toodo dit handmatig.) Voegt codefragmenten in Hallo client en server code tooinitialize ze met Hallo Application Insights-resource-ID. Bijvoorbeeld: code in een MVC-app is ingevoegd in Hallo basispagina Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Hoe voer ik een upgrade van oudere versies van de SDK?
Zie Hallo [release-opmerkingen](app-insights-release-notes.md) geschikt voor Hallo SDK tooyour type toepassing.

## <a name="update"></a>Hoe kan ik welke Azure-resource mijn project gegevens worden verzonden wijzigen?
Klik in Solution Explorer met de rechtermuisknop op `ApplicationInsights.config` en kies **Update Application Insights**. U kunt Hallo gegevens tooan bestaande of nieuwe resource verzenden in Azure. wijzigingen in de wizard Hallo update Hallo instrumentatiesleutel in ApplicationInsights.config, waarmee wordt bepaald wanneer Hallo server SDK verzendt uw gegevens. Tenzij u 'Alles bijwerken' uitschakelt, wordt het Hallo-sleutel waar deze wordt weergegeven in uw webpagina's ook gewijzigd.

## <a name="what-is-status-monitor"></a>Wat is Status Monitor?

Application Insights een bureaublad-app die u kunt gebruiken in uw toohelp IIS web server configureren in web-apps. Deze telemetrie niet verzamelen: u kunt deze stoppen wanneer u een app niet configureert. 

[Meer informatie](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Welke telemetrie in Application Insights worden verzameld?

Vanuit server-web-apps:

* HTTP-aanvragen
* [Afhankelijkheden](app-insights-asp-net-dependencies.md). Aanroepen naar: SQL-Databases. HTTP-aanroepen tooexternal services; Azure DB Cosmos, tabel, blob-opslag en wachtrij. 
* [Uitzonderingen](app-insights-asp-net-exceptions.md) en traceringen.
* [Prestatiemeteritems](app-insights-performance-counters.md) : als u [Status Monitor](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) of Hallo [Application Insights collectd writer](app-insights-java-collectd.md).
* [Aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md) dat u de code.
* [Traceerlogboeken](app-insights-asp-net-trace-logs.md) als u de juiste collector Hallo configureert.

Van [client webpagina's](app-insights-javascript.md):

* [Paginaweergave geteld](app-insights-web-track-usage.md)
* [AJAX-aanroepen](app-insights-asp-net-dependencies.md) aanvragen worden gedaan vanuit een script wordt uitgevoerd.
* Gegevens laden van pagina weergeven
* Telt het aantal gebruikers- en sessiegegevens
* [Geverifieerde gebruikers-id 's](app-insights-api-custom-events-metrics.md#authenticated-users)

Uit andere bronnen, als u ze configureren:

* [Azure diagnostics](app-insights-azure-diagnostics.md)
* [Docker-containers](app-insights-docker.md)
* [Importeren tabellen tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>Kan ik een filter of telemetrie wijzigen?

Ja, in het Hallo-server die u kunt schrijven:

* Telemetrie-Processor toofilter of eigenschappen tooselected telemetrie-items toevoegen voordat ze worden verzonden vanuit uw app.
* Telemetrie initialisatiefunctie tooadd eigenschappen tooall items telemetrie.

Meer informatie voor [ASP.NET](app-insights-api-filtering-sampling.md) of [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Hoe worden stad, land en andere gegevens van de locatie geo berekend?

We Hallo IP-adres (IPv4 of IPv6) van de webclient Hallo met opzoeken [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Browser telemetrie: We verzamelen van de afzender Hallo IP-adres.
* Servertelemetrie: Hallo Application Insights module verzamelt Hallo client-IP-adres. Het is niet verzameld als `X-Forwarded-For` is ingesteld.

U kunt configureren Hallo `ClientIpHeaderTelemetryInitializer` tootake Hallo IP-adres uit een andere koptekst. In sommige systemen, bijvoorbeeld: het is verplaatst door een proxy, load balancer of CDN te`X-Originating-IP`. [Meer informatie](http://apmtips.com/blog/2016/07/05/client-ip-address/).

U kunt [Power BI gebruiken](app-insights-export-power-bi.md) toodisplay de aanvraagtelemetrie van uw op een kaart.


## <a name="data"></a>Hoe lang gegevens bewaard in de portal Hallo? Is het veilig?
Kijk eens naar [bewaren van gegevens en Privacy][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Mogelijk persoonsgegevens (PII) gegevens in verzonden Hallo telemetrie?

Dit is mogelijk als uw code dergelijke gegevens verzendt. Het kan ook gebeuren als variabelen in de stack-traces PII bevatten. Uw ontwikkelteam neemt risico beoordelingen tooensure dat PII goed wordt afgehandeld. [Meer informatie over bewaren van gegevens en privacy](app-insights-data-retention-privacy.md).

de laatste octet Hallo van client-webadres Hallo wordt altijd too0 ingesteld na opname door Hallo-portal.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Mijn iKey is zichtbaar in de bron van mijn webpagina. 

* Dit is gebruikelijk om in de bewaking van oplossingen.
* Het gebruikte toosteal uw gegevens kan niet zijn.
* Het gebruikte tooskew uw gegevens of trigger-waarschuwingen kan worden.
* We hebben geen gehoord dat elke klant dergelijke problemen heeft gehad.

U kunt doen:

* Twee afzonderlijke iKeys (Scheid Application Insights-resources), gebruiken voor gegevens van client en server. of
* Schrijven van een proxy die wordt uitgevoerd op uw server en Hallo webclient verzenden van gegevens via proxyinstellingen hebben.

## <a name="post"></a>Hoe kan ik postgegevens in diagnostische gegevens doorzoeken zien?
Er geen postgegevens automatisch wordt geregistreerd, maar u kunt een aanroep van TrackTrace: Hallo gegevens plaatsen in de parameter voor Hallo-bericht. Dit heeft een langer groottelimiet dan Hallo limieten op de eigenschappen van een verbindingsreeks, maar u kunt niet op het filteren.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Moet ik Application Insights-resources voor één of meerdere gebruiken?

Gebruik één resource voor alle Hallo onderdelen of rollen in een één-systeem. Afzonderlijke resources gebruiken voor ontwikkeling, testen en release-versies, en voor onafhankelijke toepassingen.

* [Zie de beschrijving van Hallo hier](app-insights-separate-resources.md)
* [Voorbeeld - cloudservice met worker en webservice-functies](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Hoe kan ik de instrumentatiesleutel Hallo dynamisch wijzigen?

* [Hier discussie](app-insights-separate-resources.md)
* [Voorbeeld - cloudservice met worker en webservice-functies](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Wat zijn Hallo gebruiker en sessie telt?

* Hallo JavaScript SDK Hiermee stelt u een gebruiker cookie op Hallo webclient, tooidentify terugkerende gebruikers en een sessie cookie toogroup activiteiten.
* Als er geen clientscript, kunt u [cookies worden ingesteld op Hallo server](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Als een echte gebruiker maakt gebruik van uw site in andere browsers of met in-persoonlijke/incognito bladeren of andere machines vervolgens zij wordt meer dan één keer worden geteld.
* Voeg een aanroep te tooidentify een aangemelde gebruiker over machines en browsers,[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a>Hebben ik alles in Application Insights ingeschakeld?
| U ziet | Hoe tooget deze | Gewenste waarom |
| --- | --- | --- |
| Beschikbaarheid grafieken |[Webtests](app-insights-monitor-web-app-availability.md) |Kent dat uw web-app actief is |
| Server app-prestaties: reactietijden,... |[Application Insights tooyour project toevoegen](app-insights-asp-net.md) of [AI Status Monitor installeren op de server](app-insights-monitor-performance-live-website-now.md) (of uw eigen code te schrijven[afhankelijkheden bijhouden](app-insights-api-custom-events-metrics.md#trackdependency)) |Perf problemen detecteren |
| Afhankelijkheidstelemetrie |[AI Status Monitor installeren op server](app-insights-monitor-performance-live-website-now.md) |Problemen met databases of andere externe componenten vaststellen |
| Stack-traces van uitzonderingen ophalen |[TrackException aanroepen invoegen in uw code](app-insights-asp-net-exceptions.md) (maar een aantal automatisch worden gerapporteerd) |Detecteren en onderzoeken van uitzonderingen |
| Logboektraceringen zoeken |[Voeg een adapter logboekregistratie](app-insights-asp-net-trace-logs.md) |Uitzonderingen, perf problemen onderzoeken |
| Basisbeginselen van de client gebruik: paginaweergaven, sessies,... |[JavaScript-initialisatiefunctie in webpagina 's](app-insights-javascript.md) |Gebruiksanalyse |
| Aangepaste metrische gegevens van client |[Bijhouden roept in webpagina 's](app-insights-api-custom-events-metrics.md) |Gebruikerservaring verbeteren |
| Aangepaste metrische gegevens van server |[Bijhouden aanroepen op de server](app-insights-api-custom-events-metrics.md) |Business intelligence |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Waarom worden Hallo telt in zoek- en metrische gegevens grafieken ongelijke?

[Steekproef nemen](app-insights-sampling.md) Hallo aantal telemetrie-items (aanvragen, aangepaste gebeurtenissen, enzovoort) die daadwerkelijk worden verzonden vanuit de portal van uw app toohello verminderd. In de zoekopdracht ziet u Hallo aantal items daadwerkelijk ontvangen. In de metrische diagrammen waarin een aantal gebeurtenissen worden weergegeven, ziet u Hallo aantal oorspronkelijke gebeurtenissen die hebben plaatsgevonden. 

Elk item dat is transmmitted uitvoert een `itemCount` eigenschap die laat hoeveel oorspronkelijke gebeurtenissen dat het item zien vertegenwoordigt. tooobserve steekproef nemen bij bewerking, kunt u deze query kunt uitvoeren in Analytics:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automatisering

### <a name="configuring-application-insights"></a>Application Insights configureren

U kunt [PowerShell-scripts schrijven](app-insights-powershell.md) met Azure Broncontrole naar:

* Maken en bijwerken van Application Insights-resources.
* Hallo plan prijzen ingesteld.
* Hallo-instrumentatiesleutel ophalen.
* Een metriek waarschuwing toevoegen.
* Een beschikbaarheidstest toevoegen.

U kan een rapport metriek Explorer instellen of instellen van continue export.

### <a name="querying-hello-telemetry"></a>Hallo telemetrie opvragen

Gebruik Hallo [REST-API](https://dev.applicationinsights.io/) toorun [Analytics](app-insights-analytics.md) query's.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Hoe kan ik een waarschuwing instellen op een gebeurtenis?

Waarschuwingen van Azure zijn alleen voor metrische gegevens. Maak een aangepaste metrische gegevens die over een drempelwaarde waarde wanneer de gebeurtenis zich voordoet. Vervolgens stelt u een waarschuwing op Hallo metriek. Houd er rekening mee dat: u ontvangt een melding wanneer Hallo metriek Hallo drempelwaarde in beide richtingen bestrijkt; u kunt een melding tot Hallo eerste kruisende, ongeacht of de beginwaarde Hallo hoog of laag is; won't ophalen Er is altijd een latentie van enkele minuten duren.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Zijn er kosten van de gegevens overbrengen tussen een Azure-web-app en de Application Insights?

* Als uw Azure-web-app wordt gehost in een datacenter wanneer er een eindpunt van de verzameling Application Insights, er zijn geen kosten. 
* Als er geen verzamelingseindpunt in uw datacentrum host, wordt de telemetrie van uw app, worden [Azure kosten voor uitgaande](https://azure.microsoft.com/pricing/details/bandwidth/).

Dit wordt niet afhankelijk van waar uw Application Insights-resource wordt gehost. Het afhankelijk Hallo-distributie van onze eindpunten NET.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Kan ik telemetrie toohello Application Insights-portal verzenden?

U wordt aangeraden gebruik onze SDK's en SDK-API (app-insights-api-custom-events-metrics.md) hello gebruiken. Er zijn varianten van Hallo SDK voor verschillende [platforms](app-insights-platforms.md). Deze SDK's verwerken bufferfunctie, compressie, beperking, nieuwe pogingen, enzovoort. Hallo echter [opname schema](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) en [eindpunt protocol](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) zijn openbaar.

## <a name="can-i-monitor-an-intranet-web-server"></a>Kan ik een intranet-webserver bewaken?

Hier zijn twee methoden:

### <a name="firewall-door"></a>De deur van de firewall

Toestaan dat de web server toosend telemetrie tooour eindpunten https://dc.services.visualstudio.com:443 en https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Proxy

Verkeer leiden van de gateway van uw server tooa op uw intranet, dit door in te stellen ApplicationInsights.config:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Uw gateway moet routeren Hallo verkeer toohttps://dc.services.visualstudio.com:443 v2/bijhouden

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>Kan ik webtests voor beschikbaarheid op een intranetserver uitvoeren?

Onze [webtests](app-insights-monitor-web-app-availability.md) uitvoeren op de punten van de aanwezigheid die worden gedistribueerd over Hallo hele wereld. Er zijn twee oplossingen:

* Klep van firewallregels - aanvragen toestaan tooyour server [Hallo lang en wijzigbaar lijst van web testen agents](app-insights-ip-addresses.md).
* Schrijf uw eigen code toosend periodieke aanvragen tooyour server uit binnen uw intranet. U kunt Visual Studio-webtests voor dit doel kan uitvoeren. Hallo-tester kan Hallo resultaten tooApplication Insights Hallo TrackAvailability() API met verzenden.

## <a name="more-answers"></a>Meer antwoorden
* [Application Insights-forum](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
