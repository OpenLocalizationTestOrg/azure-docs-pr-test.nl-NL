---
title: aaaLive metrische gegevensstroom met aangepaste metrische gegevens en diagnostische gegevens in Azure Application Insights | Microsoft Docs
description: Bewaken van uw web-app in realtime met aangepaste metrische gegevens en onderzoeken van problemen met een live feed fouten, traceringen en gebeurtenissen.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Livestream metrische gegevens: De Monitor & spoor met een latentie van 1 seconde 

Hallo kloppen in de race hart van uw webtoepassing live, in productie-test met behulp van livestream metrische gegevens van [Application Insights](app-insights-overview.md). Selecteer en metrische gegevens en prestaties tellers toowatch in real-time, zonder eventuele verstoringen tooyour service filteren. Inspecteer de stack-traces van voorbeeld kan aanvragen en uitzonderingen. Samen met [Profiler](app-insights-profiler.md), [momentopname foutopsporingsprogramma](app-insights-snapshot-debugger.md), en [prestatietests](app-insights-monitor-web-app-availability.md#performance-tests), metrische gegevens livestream biedt een krachtige en niet-Invasief diagnostisch hulpprogramma van uw live web site.

U kunt met livestream metrische gegevens:

* Valideren van een oplossing, terwijl deze wordt uitgebracht, prestaties en mislukte aantallen volgen.
* Bekijkt hello effect van belasting te testen en problemen diagnosticeren live. 
* Zich richten op bepaalde test sessies of bekende problemen door te selecteren en filteren Hallo metrische gegevens die u wilt dat toowatch filteren.
* Uitzondering traceringen meteen worden opgehaald.
* Experiment met filters toofind Hallo meest relevante KPI's.
* Alle vensters prestaties meteritem live bewaken.
* Zoek een server die problemen ondervindt, en eenvoudig alle Hallo KPI/live feed toojust filteren die server.

[![Live video van de gegevensstroom van de metrische](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Metrische gegevens livestream is momenteel beschikbaar op lokale met ASP.NET-apps of in Hallo Cloud. 

## <a name="get-started"></a>Aan de slag

1. Als u nog niet hebt [Application Insights geïnstalleerd](app-insights-asp-net.md) in uw ASP.NET-web-app of [app voor Windows server](app-insights-windows-services.md), doet u dat nu. 
2. **Meest recente versie van de update toohello** van Hallo Application Insights-pakket. In Visual Studio met de rechtermuisknop op uw project en kies **beheren Nuget-pakketten**. Open Hallo **Updates** tabblad selectievakje **Include prerelease**, en selecteer alle Hallo Microsoft.ApplicationInsights.* pakketten.

    Implementeer uw app opnieuw.

3. In Hallo [Azure-portal](https://portal.azure.com)Hallo Application Insights-resource voor uw app openen en open vervolgens Live Stream.

4. [Beveiligde Hallo besturingskanaal](#secure-the-control-channel) als u mogelijk gevoelige gegevens zoals klantnamen in filters.


![Klik op Hallo overzichtsblade Live Stream](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Zijn er geen gegevens? Controleer de firewall van uw server

Controleer Hallo [uitgaande poorten voor de metrische gegevens livestream](app-insights-ip-addresses.md#outgoing-ports) zijn geopend in de firewall van uw servers Hallo. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Hoe verschilt livestream metrische gegevens van Metrics Explorer en Analytics?

| |Live Stream | Metrics Explorer en analyses |
|---|---|---|
|Latentie|Gegevens die worden weergegeven binnen één seconde|Geaggregeerd in minuten|
|Er geen bewaarperiode|Gegevens zich blijft voordoen terwijl deze op Hallo grafiek en vervolgens wordt verwijderd|[Gegevens bewaard gedurende 90 dagen](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|Op aanvraag|Gegevens gestreamd tijdens het openen van Live metrische gegevens|Gegevens worden verzonden wanneer Hallo SDK is geïnstalleerd en ingeschakeld|
|Gratis|Er zijn geen kosten voor Live Stream gegevens|Onderwerpnaam te[prijzen](app-insights-pricing.md)
|Steekproeven|Alle geselecteerde metrische gegevens en prestatiemeteritems worden verzonden. Fouten en stack-traces steekproeven worden genomen. TelemetryProcessors worden niet toegepast.|Mogelijk zijn gebeurtenissen [door actieve](app-insights-api-filtering-sampling.md)|
|Besturingskanaal|Filter besturingselement signalen verzonden toohello SDK. We raden u [secure dit kanaal](#secure-channel).|Communicatie kan niet worden teruggedraaid, toohello portal|


## <a name="select-and-filter-your-metrics"></a>Selecteer en metrische gegevens over uw filteren

(Beschikbaar op klassieke ASP.NET-apps met Hallo nieuwste SDK.)

U kunt aangepaste KPI live bewaken door willekeurige filters zijn toegepast op alle telemetrie voor Application Insights van Hallo-portal. Klik op Hallo filterbesturingselement waarin wordt weergegeven wanneer u muis van Hallo grafieken. Hallo volgende grafiek met het uitzetten van een aangepaste aanvraag aantal KPI met filters op de URL en de duur van de kenmerken. Filters Hello stroom Preview sectie ziet u een live feed telemetrie die overeenkomt met de Hallo criteria die u hebt opgegeven op elk punt in tijd valideren. 

![Aangepaste aanvraag KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

U kunt een andere waarde dan het aantal bewaken. Hallo-opties, is afhankelijk van Hallo type stream, wat erop kan telemetrie voor Application Insights: aanvragen, afhankelijkheden, uitzonderingen, traceringen, gebeurtenissen of metrische gegevens. Het kan ook uw eigen [aangepaste meting](app-insights-api-custom-events-metrics.md#properties):

![Opties voor](./media/app-insights-live-stream/live-stream-valueoptions.png)

Bovendien tooApplication Insights telemetry, u kunt ook bewaken Windows-prestatiemeteritem door selecteren die uit Hallo stroom opties, en het Hallo-naam van het prestatiemeteritem Hallo leveren.

Live metrische gegevens worden samengevoegd op twee punten: lokaal op elke server en klik vervolgens op alle servers. U kunt Hallo standaard op door een andere opties selecteren in Hallo respectieve vervolgkeuzelijsten wijzigen.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Voorbeeld telemetrie: Aangepaste Live diagnostische gebeurtenissen
Standaard ziet live feed Hallo van gebeurtenissen u voorbeelden van mislukte aanvragen en afhankelijkheidsaanroepen, uitzonderingen, gebeurtenissen en traceringen. Klik op Hallo pictogram toosee Hallo toegepast filtercriteria op elk gewenst moment in de tijd. 

![Standaard live feed](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Als met metrische gegevens, kunt u elke willekeurige criteria tooany Hallo Application Insights telemetrie typen. In dit voorbeeld selecteren we, traceringen en gebeurtenissen voor mislukte aanvragen voor specifieke. Er worden ook alle uitzonderingen en fouten van afhankelijkheid selecteren.

![Aangepaste live feed](./media/app-insights-live-stream/live-stream-events.png)

Opmerking: Op dit moment voor de criteria voor op basis van een bericht van uitzondering gebruiken buitenste uitzondering het Hallo-bericht. In het voorgaande voorbeeld Hallo toofilter uit Hallo onschadelijk uitzondering met het InnerException-bericht (volgt hello "<--' scheidingsteken)"Hallo-client is verbroken." Gebruik een bericht bevat niet-'Fout bij het lezen van de aanvraaginhoud' criteria.

Zie de details van de Hallo van een item in Hallo feed live door erop te klikken. U kunt onderbreken Hallo feed door te klikken op **onderbreken** gewoon omlaag schuiven, of op een item te klikken. Live feed wordt hervat nadat u schuift in back toohello top of door te klikken op Hallo teller van items die zijn verzameld tijdens het programma is onderbroken.

![Steekproef live fouten](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filteren op server-exemplaar

Als u een bepaalde server rolinstantie toomonitor wilt, kunt u filteren op de server.

![Steekproef live fouten](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>SDK-vereisten
Aangepaste metrische gegevens livestream is beschikbaar met versie 2.4.0-beta2 of nieuwere van [Application Insights-SDK voor web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Houd er rekening mee tooselect 'Prerelease opnemen' optie uit de NuGet-Pakketbeheer.

## <a name="secure-hello-control-channel"></a>Hallo-besturingskanaal beveiligen
Hallo aangepaste filters criteria die u opgeeft worden verzonden back toohello Live metrische gegevens onderdeel Hallo Application Insights-SDK. Hallo filters kunnen mogelijk vertrouwelijke gegevens zoals customerIDs bevatten. U kunt beveiligen met een geheime sleutel van de API bovendien toohello instrumentatiesleutel Hallo-kanaal.
### <a name="create-an-api-key"></a>Maak een API-sleutel

![Api-sleutel maken](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>API-sleutel tooConfiguration toevoegen
Voeg Hallo AuthenticationApiKey toohello QuickPulseTelemetryModule in Hallo applicationinsights.config-bestand:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Of in code wordt ingesteld op Hallo QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Als u kent en vertrouwt dat alle gekoppelde servers hello, kunt u aangepaste filters Hallo zonder Hallo geverifieerde kanaal proberen. Deze optie is beschikbaar voor zes maanden. Met deze overschrijving is vereist eenmaal elke nieuwe sessie of als een nieuwe server online is.

![Live metrische gegevens Auth-opties](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Het is raadzaam dat u Hallo geverifieerde kanaal instellen voordat u een potentieel gevoelige informatie, zoals CustomerID in Hallo filtercriteria invoert.
>

## <a name="generating-a-performance-test-load"></a>Een test prestatiebelasting genereren

Als u wilt dat toowatch Hallo effect van een werklast verhogen, gebruik Hallo prestatietest blade. Het simuleert aanvragen van een aantal gelijktijdige gebruikers. Beide 'handmatig 'tests uit te voeren (ping-tests) van één URL of uit te voeren een [WebTest met meerdere stappen prestatietest](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (in hello dezelfde manier als voor een beschikbaarheid testen) te uploaden.

> [!TIP]
> Nadat u de prestatietest Hallo hebt gemaakt, opent u Hallo test en Hallo Live Stream blade in afzonderlijke vensters. U kunt zien wanneer Hallo in de wachtrij prestaties test start en Bekijk live stream op Hallo hetzelfde moment.
>


## <a name="troubleshooting"></a>Problemen oplossen

Zijn er geen gegevens? Als uw toepassing bevindt zich in een beveiligd netwerk: metrische gegevens Stream Live maakt gebruik van een ander IP-adressen dan andere telemetrie voor Application Insights. Zorg ervoor dat [die IP-adressen](app-insights-ip-addresses.md) zijn geopend in uw firewall.



## <a name="next-steps"></a>Volgende stappen
* [Gebruik met Application Insights controleren](app-insights-web-track-usage.md)
* [Met behulp van diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md)
* [Profiler](app-insights-profiler.md)
* [Momentopname-foutopsporingsprogramma](app-insights-snapshot-debugger.md)
