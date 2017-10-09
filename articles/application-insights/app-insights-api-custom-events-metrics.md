---
title: aaaApplication Insights-API voor aangepaste gebeurtenissen en metrische gegevens | Microsoft Docs
description: Invoegen van een paar regels code in het gebruik van uw apparaat of bureaublad-app, een webpagina of service, tootrack en onderzoeken van problemen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens

Een paar regels code in uw toepassing toofind uit wat gebruikers met het doen invoegen of toohelp vaststellen van problemen. U kunt telemetrie verzenden van apparaat- en bureaublad-apps, webserver en webclients en webservers. Gebruik Hallo [Azure Application Insights](app-insights-overview.md) telemetrie-API toosend aangepaste gebeurtenissen en metrische gegevens en uw eigen versies standaardtelemetrie core. Deze API is Hallo dezelfde API die Hallo standaard Application Insights gegevens collectors gebruiken.

## <a name="api-summary"></a>API-overzicht
Hallo API is uniform op alle platforms, naast een paar kleine verschillen.

| Methode | Gebruikt voor |
| --- | --- |
| [`TrackPageView`](#page-views) |Pagina's, schermen, blades of formulieren. |
| [`TrackEvent`](#trackevent) |Acties van gebruikers en andere gebeurtenissen. Tootrack gebruiker gedrag of toomonitor prestaties gebruikt. |
| [`TrackMetric`](#trackmetric) |Prestatiemetingen zoals wachtrij lengten niet gerelateerd toospecific gebeurtenissen. |
| [`TrackException`](#trackexception) |Logboekregistratie uitzonderingen voor diagnose. Traceren waarin ze in de relatie tooother gebeurtenissen optreden en stack-traces onderzoeken. |
| [`TrackRequest`](#trackrequest) |Logboekregistratie Hallo frequentie en duur van serveraanvragen voor analyse van prestaties. |
| [`TrackTrace`](#tracktrace) |Diagnostische logboeken-berichten. U kunt ook de logboeken van derden vastleggen. |
| [`TrackDependency`](#trackdependency) |Logboekregistratie Hallo duur en frequentie van aanroepen tooexternal onderdelen die afhankelijk van uw app. |

U kunt [eigenschappen en metrische gegevens koppelen](#properties) toomost telemetrie aanroepen.

## <a name="prep"></a>Voordat u begint
Als u nog een verwijzing op Application Insights-SDK hebt:

* Hallo Application Insights-SDK tooyour project toevoegen:

  * [ASP.NET-project](app-insights-asp-net.md)
  * [Java-project](app-insights-java-get-started.md)
  * [JavaScript in elke webpagina](app-insights-javascript.md) 
* In uw servercode apparaat of een webtoepassing omvatten:

    *C#:*`using Microsoft.ApplicationInsights;`

    *Visual Basic:*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Een exemplaar TelemetryClient maken
Maken van een exemplaar van `TelemetryClient` (behalve in JavaScript in webpagina's):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient is thread-safe.

Het is raadzaam om gebruik te maken van een instantie van TelemetryClient voor elke module van uw app. Bijvoorbeeld: mogelijk hebt u één exemplaar van TelemetryClient in uw web-service tooreport binnenkomende HTTP-aanvragen en andere in een middleware klasse tooreport zakelijke logica gebeurtenissen. U kunt eigenschappen instellen, zoals `TelemetryClient.Context.User.Id` tootrack gebruikers en sessies, of `TelemetryClient.Context.Device.Id` tooidentify Hallo machine. Deze informatie is aangesloten tooall gebeurtenissen die Hallo exemplaar verzendt.

## <a name="trackevent"></a>TrackEvent
In Application Insights, een *aangepaste gebeurtenis* is van een gegevenspunt geldt dat u kunt weergeven in [Metrics Explorer](app-insights-metrics-explorer.md) als een verzamelde aantal en in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md) als afzonderlijke exemplaren. (Niet verwant tooMVC of andere framework 'gebeurtenissen'.)

Invoegen `TrackEvent` roept in uw code toocount diverse gebeurtenissen. Hoe vaak gebruikers kiest voor een bepaalde functie, hoe vaak ze bepaalde doelen bereiken of zij mogelijk hoe vaak voor bepaalde soorten fouten.

Bijvoorbeeld in een gameapps een gebeurtenis wanneer een gebruiker wins Hallo game verzenden:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>De gebeurtenissen in Microsoft Azure-portal Hallo weergeven
toosee een aantal van uw gebeurtenissen, open een [Metrics Explorer](app-insights-metrics-explorer.md) blade, Voeg een nieuwe grafiek toe en selecteer **gebeurtenissen**.  

![Zie een aantal aangepaste gebeurtenissen](./media/app-insights-api-custom-events-metrics/01-custom.png)

toocompare hello tellingen van verschillende gebeurtenissen ingesteld Hallo grafiektype te**raster**, and -groep met de gebeurtenisnaam:

![Hallo grafiektype en groepering instellen](./media/app-insights-api-custom-events-metrics/07-grid.png)

Klik op Hallo raster in een gebeurtenis naam toosee afzonderlijke exemplaren van deze gebeurtenis. toosee specifieke - klikt u op elk exemplaar in Hallo-lijst.

![Drillthrough-Hallo-gebeurtenissen](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus van specifieke gebeurtenissen in de zoekopdracht of Metrics Explorer set Hallo blade filter toohello gebeurtenisnamen die u geïnteresseerd bent in:

![Open Filters, vouw de naam van de gebeurtenis en selecteer een of meer waarden](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Aangepaste gebeurtenissen in Analytics

Hallo telemetrie is beschikbaar in Hallo `customEvents` in tabel [Application Insights Analytics](app-insights-analytics.md). Elke rij vertegenwoordigt een gesprek te`trackEvent(..)` in uw app. 

Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1. Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackEvent(), Hallo steekproeven proces alleen één van beide verzonden. tooget het juiste aantal aangepaste gebeurtenissen, moet u daarom code gebruiken zoals `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights kunnen metrische gegevens die niet aangesloten tooparticular gebeurtenissen zijn van grafiekgebied. U kan bijvoorbeeld een wachtrijlengte bewaken met regelmatige tussenpozen. Hallo afzonderlijke metingen zijn minder interessant dan Hallo variaties en trends met metrische gegevens, en dus statistische kolomdiagrammen zijn nuttig.

In order toosend metrische gegevens tooApplication inzichten, kunt u Hallo `TrackMetric(..)` API. Er zijn twee manieren toosend metric: 

* Enkele waarde. Telkens wanneer u een meting in uw toepassing uitvoert, verzendt u overeenkomende waarde Hallo tooApplication Insights. Bijvoorbeeld, wordt ervan uitgegaan dat u hebt een metriek Hallo aantal items in een container te beschrijven. U voor het eerst drie items in Hallo container geplaatst en verwijder vervolgens twee items gedurende een bepaalde periode. Dienovereenkomstig, roept u `TrackMetric` tweemaal: eerst doorgegeven waarde Hallo `3` en vervolgens Hallo waarde `-2`. Application Insights worden beide waarden opgeslagen namens jou. 

* Aggregatie. Als u werkt met metrische gegevens, wordt elke meting zelden is van belang. In plaats daarvan is een overzicht van wat er gebeurd gedurende een bepaalde periode is belangrijk. Dergelijke samenvatting heet _aggregatie_. Hallo hierboven voorbeeld Hallo cumulatieve metrische som gedurende deze periode is `1` en Hallo Hallo metrische waarden aantal `2`. Wanneer u Hallo aggregatie benadering, u alleen aanroepen `TrackMetric` eenmaal per periode en verzenden Hallo geaggregeerde tijdwaarden. Dit is Hallo aanbevolen benadering omdat Hallo kosten aantasten kan en prestaties van de overhead door minder gegevens te verzenden tooApplication Insights, punten tijdens het verzamelen van nog steeds alle relevante informatie.

### <a name="examples"></a>Voorbeelden:

#### <a name="single-values"></a>Enkele waarden

toosend metrische waarde voor een enkele:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Samenvoegen van metrische gegevens

Het verdient aanbeveling tooaggregate metrische gegevens voordat ze worden verzonden vanuit uw app, tooreduce bandbreedte, kosten en tooimprove prestaties.
Hier volgt een voorbeeld van code verzamelen:

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Aangepaste metrische gegevens in Metrics Explorer

toosee hello resultaten Metrics Explorer openen en een nieuwe grafiek toevoegen. Hallo grafiek tooshow uw metriek bewerken.

> [!NOTE]
> Uw aangepaste metric duurt enkele minuten tooappear in Hallo lijst met beschikbare metrische gegevens.
>

![Voeg een nieuwe grafiek toe of Selecteer een grafiek en onder aangepast, selecteer uw metrische gegevens](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Aangepaste metrische gegevens in Analytics

Hallo telemetrie is beschikbaar in Hallo `customMetrics` in tabel [Application Insights Analytics](app-insights-analytics.md). Elke rij vertegenwoordigt een gesprek te`trackMetric(..)` in uw app.
* `valueSum`-Dit is de som Hallo Hallo metingen. tooget hello gemiddelde waarde delen door `valueCount`.
* `valueCount`-aantal van de metingen die zijn samengevoegd in dit Hallo `trackMetric(..)` aanroepen.

## <a name="page-views"></a>Paginaweergaven
In een app-apparaat of webpagina telemetrie van paginaweergaven standaard verzonden wanneer elke pagina of het scherm wordt geladen. Maar u kunt deze paginaweergaven tootrack wijzigen op aanvullende of verschillende tijdstippen. Bijvoorbeeld in een app die wordt weergegeven voor tabbladen of blades, kunt u een pagina tootrack wanneer Hallo gebruiker een nieuwe blade opent.

![Gebruik lens op de blade overzicht](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Gebruikers- en sessiegegevens gegevens verzonden zoals eigenschappen samen met paginaweergaven, zodat gebruikers- en sessiegegevens grafieken tot leven komen als er telemetrie van paginaweergaven Hallo.

### <a name="custom-page-views"></a>Aangepaste paginaweergaven
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Als u meerdere tabbladen binnen andere HTML-pagina's hebt, kunt u Hallo-URL te opgeven:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Timing van paginaweergaven
Standaard Hallo keren gerapporteerd als **laadtijd voor paginaweergave** worden gemeten vanuit de browser Hallo Hallo-aanvraag verzendt totdat van de browser van het Hallo-gebeurtenis voor het laden van pagina wordt aangeroepen.

In plaats daarvan kunt u:

* Instellen van een expliciete duur in Hallo [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) aanroepen: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Hallo pagina weergave timing aanroepen gebruiken `startTrackPage` en `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Hallo naam die u gebruikt als de eerste parameter Hallo Hallo start koppelt en stop de aanroepen. Wordt standaard de naam van toohello huidige pagina.

Hallo resulterende laadtijd weergegeven in Metrics Explorer duur zijn afgeleid van hello-interval tussen Hallo starten en stoppen van aanroepen. Is tooyou welke interval die u daadwerkelijk tijd.

### <a name="page-telemetry-in-analytics"></a>Pagina telemetrie in Analytics

In [Analytics](app-insights-analytics.md) twee tabellen bevatten gegevens van de browser bewerkingen:

* Hallo `pageViews` tabel bevat gegevens over de URL- en titel Hallo
* Hallo `browserTimings` tabel bevat gegevens over de prestaties van de client, zoals Hallo tijd tooprocess Hallo binnenkomende gegevens

toofind hoe lang Hallo browser duurt tooprocess verschillende pagina's:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover hello popularities van verschillende browsers:

```
pageViews | summarize count() by client_Browser
```

aanmelden bij tooassociate pagina weergaven tooAJAX aanroepen met afhankelijkheden:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
Hallo server SDK gebruikt TrackRequest toolog HTTP-aanvragen.

U kunt deze zelf ook aanroepen als u wilt dat toosimulate aanvragen in een context waarin er geen Hallo web service-module die wordt uitgevoerd.

Hallo wordt echter aanbevolen manier toosend aanvraagtelemetrie is waar Hallo aanvraag fungeert als een <a href="#operation-context">bewerking context</a>.

## <a name="operation-context"></a>Bewerking context
U kunt telemetrie-items bij elkaar koppelen door het koppelen van toothem een algemene bewerking-ID. Hallo standaard aanvraag bijhouden module doet dit voor uitzonderingen en andere gebeurtenissen die worden verzonden tijdens het verwerken van een HTTP-aanvraag. In [Search](app-insights-diagnostic-search.md) en [Analytics](app-insights-analytics.md), kunt u Hallo ID tooeasily zoeken naar alle gebeurtenissen die zijn gekoppeld aan het Hallo-aanvraag.

Hallo gemakkelijkste manier tooset Hallo-ID is tooset de context van een bewerking met behulp van dit patroon:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Samen met het instellen van de context van een bewerking `StartOperation` maakt een telemetrie-item van het Hallo-type dat u opgeeft. Het Hallo telemetrie item verzendt wanneer buitengebruikstelling Hallo opnieuw, of als u niet expliciet aanroepen `StopOperation`. Als u `RequestTelemetry` als Hallo telemetrie type, de duur is een time-out opgetreden toohello interval tussen starten en stoppen is ingesteld.

Bewerking contexten kunnen niet worden genest. Als er al een bewerking context bestaat, wordt de bijbehorende ID gekoppeld aan alle Hallo opgenomen items is, inclusief Hallo item dat is gemaakt met `StartOperation`.

In de zoekopdracht op Hallo bewerking context is gebruikte toocreate Hallo **verwante Items** lijst:

![Verwante items](./media/app-insights-api-custom-events-metrics/21.png)

Zie [toepassing-insights-aangepaste-bewerkingen-tracking.md] voor meer informatie over aangepaste bewerkingen bijhouden.

### <a name="requests-in-analytics"></a>Aanvragen in Analytics 

In [Application Insights Analytics](app-insights-analytics.md), weergeven van aanvragen in Hallo `requests` tabel.

Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount eigenschap ziet een waarde groter dan 1. Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackRequest(), Hallo steekproeven proces alleen één van beide verzonden. tooget het juiste aantal aanvragen en de gemiddelde duur gesegmenteerd op aanvraag namen, zoals code gebruiken:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Uitzonderingen tooApplication Insights verzenden:

* te[tellen](app-insights-metrics-explorer.md), als een indicatie van Hallo frequentie van een probleem.
* te[onderzoeken van afzonderlijke exemplaren](app-insights-diagnostic-search.md).

Hallo-rapporten bevatten Hallo stack-traces.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

Hallo-SDK's catch veel uitzonderingen automatisch, dus u niet altijd toocall TrackException expliciet hebt.

* ASP.NET: [code schrijven toocatch uitzonderingen](app-insights-asp-net-exceptions.md).
* J2EE: [uitzonderingen worden aangetroffen, automatisch](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Uitzonderingen worden automatisch aangetroffen. Als u toodisable automatische verzameling wilt, voegt u een regel toohello codefragment waarmee u in uw webpagina's invoegen:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Uitzonderingen in Analytics

In [Application Insights Analytics](app-insights-analytics.md), uitzonderingen weergegeven in Hallo `exceptions` tabel.

Als [steekproeven](app-insights-sampling.md) is uitgevoerd, hello `itemCount` eigenschap geeft een waarde groter dan 1. Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackException(), Hallo steekproeven proces alleen één van beide verzonden. tooget het juiste aantal uitzonderingen gesegmenteerd op type uitzondering, zoals code gebruiken:

```
exceptions | summarize sum(itemCount) by type
```

De meeste van belangrijke informatie over de stack al wordt geëxtraheerd in verschillende variabelen, maar u kunt pull-elkaar Hallo Hallo `details` structuur tooget meer. Aangezien deze structuur dynamisch is, moet u uitbrengt Hallo toohello resultaattype die u verwacht. Bijvoorbeeld:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

tooassociate uitzonderingen met hun verwante aanvragen, gebruikt u een join:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Gebruik TrackTrace toohelp analyseren van problemen door een 'breadcrumb audittrail' tooApplication Insights verzenden. U kunt segmenten van diagnostische gegevens verzenden en controleren ze op in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).

[Meld u adapters](app-insights-asp-net-trace-logs.md) deze API toosend van derden logboeken toohello portal gebruiken.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


U kunt zoeken op de inhoud van het bericht, maar (in tegenstelling tot eigenschapswaarden) u kunt niet filteren op het.

de maximumgrootte Hallo op `message` veel hoger is dan de limiet Hallo op Eigenschappen.
U kunt relatief lange gegevens plaatsen in het Hallo-bericht heeft als voordeel van TrackTrace. U kunt bijvoorbeeld er postgegevens coderen.  

Bovendien kunt u een bericht van ernst niveau tooyour toevoegen. En net als andere telemetrie u eigenschap waarden toohelp die u filteren of zoeken naar verschillende sets van traceringen kunt toevoegen. Bijvoorbeeld:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

In [Search](app-insights-diagnostic-search.md), u kunt eenvoudig filteren vervolgens alle Hallo-berichten van een bepaalde ernstniveau worden weergegeven die betrekking tooa bepaalde database hebben.


### <a name="traces-in-analytics"></a>Traceringen in Analytics

In [Application Insights Analytics](app-insights-analytics.md), belt tooTrackTrace weergeven in Hallo `traces` tabel.

Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1. Voor een voorbeeld itemCount == 10 betekent dat van 10 te aanroepen`trackTrace()`, Hallo steekproeven proces verzonden slechts één van beide. het juiste aantal traceringsaanroepen tooget, moet u daarom code zoals `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Gebruik Hallo TrackDependency aanroepen tootrack Hallo responstijden en het succespercentage van aanroepen tooan externe stuk code. Hallo-resultaten verschijnen in de afhankelijkheidsgrafiek Hallo in Hallo-portal.

```C#
var success = false;
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

Houd er rekening mee dat Hallo server SDK's bevatten een [afhankelijkheid module](app-insights-asp-net-dependencies.md) die worden gedetecteerd en bepaalde afhankelijkheidsaanroepen automatisch--bijgehouden bijvoorbeeld toodatabases en REST-API's. U hebt tooinstall een agent op uw server toomake Hallo module werken. U kunt deze aanroep gebruiken als u wilt dat tootrack aanroepen die geautomatiseerde bijhouden Hallo niet catch- of als u niet wilt tooinstall Hallo agent.

tooturn uitschakelen Hallo standaard afhankelijkheid bijhouden module bewerken [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) en Hallo verwijzing te verwijderen`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Afhankelijkheden in Analytics

In [Application Insights Analytics](app-insights-analytics.md), trackDependency aanroepen weergegeven in Hallo `dependencies` tabel.

Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1. Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackDependency(), Hallo steekproeven proces alleen één van beide verzonden. tooget het juiste aantal afhankelijkheden gesegmenteerd op target-component, zoals code gebruiken:

```
dependencies | summarize sum(itemCount) by target
```

tooassociate afhankelijkheden met hun verwante aanvragen, gebruikt u een join:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Gegevens leegmaken
Normaal gesproken verzendt Hallo SDK op tijdstippen toominimize Hallo impact op Hallo gebruiker gekozen. In sommige gevallen wilt u echter mogelijk tooflush Hallo buffer--bijvoorbeeld, als u gebruikmaakt van Hallo SDK in een toepassing die wordt afgesloten.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Houd er rekening mee dat Hallo functie asynchrone voor Hallo [telemetrie-serverkanaal](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Geverifieerde gebruikers
In een web-app, worden gebruikers (standaard) geïdentificeerd door cookies. Een gebruiker mogelijk meer dan één keer worden geteld als ze toegang krijgen tot uw app uit een andere computer of de browser, of als het verwijderen van cookies.

Als gebruikers zich tooyour app, kunt u een meer nauwkeurige telling krijgen Hallo geverifieerde gebruikers-ID door in te stellen Hallo browser code:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

In een ASP.NET-webtoepassing MVC-toepassing, bijvoorbeeld:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Het is niet nodig toouse Hallo werkelijke aanmelden gebruikersnaam. Alleen heeft toobe een ID die unieke toothat gebruiker. Mag geen spaties of Hallo tekens bevatten `,;=|`.

Hallo gebruikers-ID is ook in een sessiecookie ingesteld en toohello server verzonden. Als Hallo server SDK is geïnstalleerd, geverifieerd Hallo gebruiker-ID wordt verzonden als onderdeel van Hallo contexteigenschappen van zowel client als server telemetrie. Vervolgens kunt u filteren en zoekt u erop.

Als uw app gebruikers naar accounts groepen, kunt u ook een id voor Hallo account doorgeven (Hello teken dezelfde beperkingen).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

In [Metrics Explorer](app-insights-metrics-explorer.md), kunt u een diagram waarin telt **geverifieerde gebruikers,**, en **gebruikersaccounts**.

U kunt ook [search](app-insights-diagnostic-search.md) voor client gegevenspunten met specifieke gebruikersnamen en accounts.

## <a name="properties"></a>Filteren, zoeken en segmenteren van uw gegevens met behulp van eigenschappen
U kunt de eigenschappen en metingen tooyour gebeurtenissen (en ook toometrics, paginaweergaven, uitzonderingen en andere telemetriegegevens) koppelen.

*Eigenschappen* waarmee u toofilter uw telemetrie in gebruiksrapporten Hallo kunt tekenreekswaarden zijn. Bijvoorbeeld, als uw app verschillende games biedt, kunt u koppelen Hallo-naam van Hallo game tooeach gebeurtenis zodat u kunt zien welke games populairder zijn.

Er is een limiet van 8192 op Hallo string-lengte. (Als u toosend grote reeksen gegevens wilt, gebruikt u Hallo-bericht parameter van [TrackTrace](#track-trace).)

*Metrische gegevens* zijn numerieke waarden die kunnen worden weergegeven als geïllustreerd. Bijvoorbeeld, kunt u toosee als er een geleidelijke toename van Hallo scores die uw gamers bereiken. Hallo grafieken kunnen worden gesegmenteerd op Hallo scheiden van de eigenschappen die worden verzonden met Hallo gebeurtenis, zodat u kunt ophalen of gestapelde grafieken voor verschillende games.

Voor metrische waarden toobe juist weergegeven, moeten ze too0 groter dan of gelijk zijn.

Er zijn een aantal [limieten op Hallo aantal eigenschappen en eigenschapswaarden metrische gegevens](#limits) die u kunt gebruiken.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Wees voorzichtig niet toolog persoonlijk herleidbare informatie in de eigenschappen.
>
>

*Als u metrische gegevens gebruikt*, opent u Metrics Explorer en selecteer Hallo metric in Hallo **aangepaste** groep:

![Open van Metrics Explorer, selecteer Hallo grafiek, en selecteer Hallo metrische gegevens](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Als uw metriek niet wordt weergegeven, of als hello **aangepaste** kop niet het geval is, sluit Hallo selectie blade en probeer het later opnieuw. Metrische gegevens kan soms een uur duren toobe via Hallo pipeline geaggregeerd.

*Als u de eigenschappen en metrische gegevens gebruikt*, Hallo metriek segmenteren door Hallo-eigenschap:

![Ingesteld groeperen en selecteer vervolgens de eigenschap Hallo onder groeperen op](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*In Diagnostic Search*, kunt u Hallo eigenschappen en metrische gegevens van afzonderlijke instanties van een gebeurtenis bekijken.

![Selecteer een exemplaar en selecteer vervolgens '...'](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Gebruik Hallo **Search** veld toosee gebeurtenis instanties die een bepaalde eigenschappenwaarde hebben.

![Typ een term in zoeken](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Meer informatie over zoekopdracht expressies](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Andere manier tooset eigenschappen en metrische gegevens
Als het is eenvoudiger, kunt u Hallo parameters van een gebeurtenis in een afzonderlijk object verzamelen:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Hallo niet gebruiken hetzelfde exemplaar van de telemetrie-item (`event` in dit voorbeeld) toocall Track*() meerdere keren. Dit kan leiden tot telemetrie toobe verzonden met een onjuiste configuratie.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Aangepaste metingen en eigenschappen in Analytics

In [Analytics](app-insights-analytics.md), eigenschappen en aangepaste metrische gegevens weergeven in Hallo `customMeasurements` en `customDimensions` kenmerken van elke record telemetrie.

Bijvoorbeeld, als u een eigenschap genaamd 'spel' tooyour aanvraagtelemetrie hebt toegevoegd, deze query telt Hallo instanties van verschillende waarden van 'spel' en gemiddelde Hallo Hallo aangepaste metrische 'score' weergeven:

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

U ziet dat:

* Wanneer u een waarde van Hallo customDimensions of customMeasurements JSON uitpakt, hieraan dynamische type, en zodat u dit casten `tostring` of `todouble`.
* account van de mogelijkheid Hallo van tootake [steekproeven](app-insights-sampling.md), moet u `sum(itemCount)`, niet `count()`.



## <a name="timed"></a>Timing van gebeurtenissen
Soms wilt u toochart hoe lang het duurt tooperform een actie. U kunt bijvoorbeeld tooknow hoe lang gebruikers tooconsider opties worden in een spel. Hiervoor kunt u Hallo meting parameter.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Standaard-eigenschappen voor aangepaste telemetrie
Als u tooset eigenschap standaardwaarden voor een aantal aangepaste gebeurtenissen Hallo die u schrijft wilt, kunt u ze in een exemplaar van TelemetryClient instellen. Ze zijn aangesloten tooevery telemetrie-item dat wordt verzonden door de client.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Afzonderlijke telemetrie aanroepen kunnen Hallo standaardwaarden in hun woordenlijsten eigenschap te overschrijven.

*Web voor JavaScript-clients*, [gebruik van JavaScript telemetrie initalisatiefuncties](#js-initializer).

*tooadd eigenschappen tooall telemetrie*, met inbegrip van gegevens van de standaardregel voor verzameling modules, Hallo [implementeren `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Steekproef nemen en verwerken van telemetrie filteren
U kunt code tooprocess uw telemetrie schrijven voordat deze wordt verzonden van Hallo SDK. Hallo verwerking omvat gegevens dat wordt verzonden door Hallo standaard telemetrie modules, zoals de verzameling van de HTTP-aanvragen en afhankelijkheid verzameling.

[Eigenschappen toevoegen](app-insights-api-filtering-sampling.md#add-properties) tootelemetry door het implementeren van `ITelemetryInitializer`. U kunt bijvoorbeeld versienummers of berekende waarden toevoegen van andere eigenschappen.

[Filteren](app-insights-api-filtering-sampling.md#filtering) kunt wijzigen of verwijderen van telemetrie voordat het wordt verzonden door Hallo SDK door het implementeren van `ITelemetryProcesor`. U bepaalt wat wordt verzonden naar of verwijderd, maar u tooaccount voor Hallo effect op uw metrische gegevens hebben. Afhankelijk van hoe u items negeren, kunt u Hallo mogelijkheid toonavigate tussen verwante items verliezen.

[Steekproef nemen](app-insights-api-filtering-sampling.md) is een volume verpakte oplossing tooreduce Hallo van gegevens die worden verzonden vanuit uw app toohello-portal. Dit gebeurt zonder Hallo weergegeven metrische gegevens. En zonder die betrekking hebben op uw mogelijkheid toodiagnose problemen door te navigeren tussen verwante items zoals uitzonderingen, aanvragen en paginaweergaven.

[Meer informatie](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Telemetrie uitschakelen
te*dynamisch stoppen en starten* Hallo verzamelen en verzenden van telemetrie:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

te*uitschakelen geselecteerde standaard collectors*--bijvoorbeeld, prestatiemeteritems, HTTP-aanvragen of afhankelijkheden--verwijderen of Hallo relevante regels in uitcommentariëren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). U kunt dit bijvoorbeeld doen als u uw eigen gegevens TrackRequest toosend wilt.

## <a name="debug"></a>Modus voor ontwikkelaars
Tijdens de foutopsporing, is het nuttig toohave uw telemetrie doorgegeven Hallo pipeline, direct zodat u resultaten onmiddellijk kunt zien. U ook get extra berichten sturen die u helpen traceren problemen met Hallo telemetrie. Schakel deze uit in productie, omdat dit kan uw app vertragen.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>De instrumentatiesleutel Hallo voor de geselecteerde aangepaste telemetrie instellen
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a>Dynamische instrumentatiesleutel
tooavoid combinatie van telemetrie van ontwikkeling, testen en productieomgevingen, kunt u [afzonderlijke Application Insights-resources maken](app-insights-create-new-resource.md) en wijzigt u de sleutels, afhankelijk van het Hallo-omgeving.

In plaats van het Hallo-instrumentatiesleutel ophalen uit het Hallo-configuratiebestand en kunt u dit instellen in uw code. Hallo-sleutel in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice ingesteld:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



In webpagina's, kunt u tooset op Hallo van de webserver status, in plaats van letterlijk coderen in Hallo-script. Bijvoorbeeld in een webpagina in een ASP.NET-app gegenereerd:

*JavaScript in Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient heeft een contexteigenschap die waarden bevat die samen met alle telemetriegegevens worden verzonden. Normaal gesproken zijn ingesteld door Hallo standaard telemetrie modules, maar u kunt ook instellen ze zelf. Bijvoorbeeld:

    telemetry.Context.Operation.Name = "MyOperationName";

Als u een van deze waarden zelf, overweeg te verwijderen van de betreffende regel Hallo van [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), zodat uw en Hallo standaard waarden niet veranderen.

* **Onderdeel**: Hallo-app en de versie ervan.
* **Apparaat**: gegevens over het Hallo-apparaat waarop Hallo-app wordt uitgevoerd. (In web-apps is dit Hallo-server of client-apparaat dat Hallo telemetrie is verzonden vanaf.)
* **InstrumentationKey**: Hallo Application Insights-resource in Azure waar Hallo telemetrie worden weergegeven. Dit wordt gewoonlijk opgenomen in ApplicationInsights.config.
* **Locatie**: Hallo geografische locatie van Hallo-apparaat.
* **Bewerking**: Hallo In web-apps, huidige HTTP-aanvraag. In andere typen Apps kunt u deze gebeurtenissen toogroup samen instellen.
  * **Id**: een gegenereerde waarde die verschillende gebeurtenissen, zodat wanneer u een gebeurtenis in Diagnostic Search inspecteert, u vindt verwante objecten.
  * **Naam**: een meestal Hallo URL van Hallo HTTP-aanvraag-id.
  * **SyntheticSource**: als niet null of leeg is, een tekenreeks die of Hallo het bronbestand van Hallo-aanvraag aangeeft is geïdentificeerd als een robot of web-test. Standaard wordt het uitgesloten van berekeningen in Metrics Explorer.
* **Eigenschappen**: eigenschappen die worden verzonden met alle telemetriegegevens. Deze kan worden genegeerd in afzonderlijke bijhouden * aanroepen.
* **Sessie**: Hallo gebruikerssessie. Hallo-ID is gegenereerd tooa waarde, die wordt gewijzigd wanneer het Hallo-gebruiker niet actief is geweest even ingesteld.
* **Gebruiker**: gebruikersgegevens.

## <a name="limits"></a>Limieten
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

Hallo limiet, gebruik roept tooavoid [steekproeven](app-insights-sampling.md).

toodetermine hoe lang gegevens worden bewaard raadpleegt [bewaren van gegevens en privacy](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Referentiedocumenten
* [ASP.NET-verwijzing](https://msdn.microsoft.com/library/dn817570.aspx)
* [Naslaginformatie over Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Verwijzing in JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android-SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS-SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>SDK-code
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Windows Server-pakketten](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)
* [Alle platforms](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Vragen
* *Welke uitzonderingen's Track_() aanroepen weggooien*

    Geen. U hoeft niet toowrap ze in trycatch-componenten. Als er problemen Hallo SDK, wordt deze berichten aanmelden Hallo foutopsporing console-uitvoer en--als hello berichten ophalen via--in diagnostische gegevens doorzoeken.
* *Is er een REST-API tooget gegevens vanuit de portal Hallo?*

    Ja, Hallo [data access-API](https://dev.applicationinsights.io/). Andere manieren tooextract gegevens omvatten [exporteren vanuit Analytics tooPower BI](app-insights-export-power-bi.md) en [continue export](app-insights-export-telemetry.md).

## <a name="next"></a>Volgende stappen
* [Zoekopdracht gebeurtenissen en Logboeken](app-insights-diagnostic-search.md)

* [Problemen oplossen](app-insights-troubleshoot-faq.md)


