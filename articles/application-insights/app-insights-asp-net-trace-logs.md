---
title: aaaExplore traceerlogboeken .NET in Application Insights
description: Zoeken naar Logboeken die worden gegenereerd met Trace, NLog en Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>.NET-traceerlogboeken in Application Insights verkennen
Als u NLog, log4Net of System.Diagnostics.Trace voor diagnostische tracering in uw ASP.NET-toepassing kunt u uw logboeken verzonden te hebben[Azure Application Insights][start], waar u kunt verkennen en zoeken ze. Uw logboeken worden samengevoegd met andere Hallo telemetrie afkomstig zijn van uw toepassing, zodat u kunt identificeren Hallo traceringen die zijn gekoppeld aan het onderhoud van de aanvraag van elke gebruiker en ze te correleren met andere gebeurtenissen en de uitzonderingenrapporten.

> [!NOTE]
> Moet u de logboekmodule vastleggen Hallo? Het is een nuttig adapter voor 3rd derden voorkomen, maar als u niet al gebruikt NLog, log4Net of System.Diagnostics.Trace, kunt u alleen aanroepen [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) rechtstreeks.
>
>

## <a name="install-logging-on-your-app"></a>Aanmelden met uw app installeren
Uw framework voor logboekregistratie gekozen installeren in uw project. Dit moet resulteren in een vermelding in het app.config- of web.config.

Als u van System.Diagnostics.Trace gebruikmaakt, moet u een vermelding tooweb.config tooadd:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Application Insights toocollect logboeken configureren
**[Application Insights tooyour project toevoegen](app-insights-asp-net.md)**  als u die nog niet hebt gedaan. Hier ziet u een optie tooinclude Hallo-logboekverzamelaar.

Of **Configure Application Insights** met de rechtermuisknop op het project in Solution Explorer. Hallo-optie te selecteren**trace verzamelen configureren**.

*Er zijn geen menu- of logboekbestand collector de optie Application Insights?* Probeer [probleemoplossing](#troubleshooting).

## <a name="manual-installation"></a>Handmatige installatie
Gebruik deze methode als uw projecttype wordt niet ondersteund door Hallo Application Insights-installatieprogramma (bijvoorbeeld een Windows desktop-project).

1. Als u van plan toouse log4Net of NLog bent, kunt u deze in uw project installeren.
2. Klik in Solution Explorer met de rechtermuisknop op uw project en kies **NuGet-pakketten beheren**.
3. Naar Application Insights zoeken
4. Selecteer de juiste pakket Hallo - een van:

   * Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace aanroepen)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource gebeurtenissen)
   * Microsoft.ApplicationInsights.EtwListener (toocapture ETW-gebeurtenissen)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

Hallo NuGet-pakket installeert de benodigde assembly Hallo en past tevens web.config of app.config.

## <a name="insert-diagnostic-log-calls"></a>Diagnostische logboeken aanroepen invoegen
Als u System.Diagnostics.Trace gebruikt, wordt een aanroep van typische zou zijn:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Als u liever log4net of NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Het gebruik van EventSource gebeurtenissen
U kunt configureren [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gebeurtenissen toobe verzonden tooApplication Insights als traceringen. Installeer eerst Hallo `Microsoft.ApplicationInsights.EventSourceListener` NuGet-pakket. Bewerk vervolgens `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

U kunt voor elke bron Hallo volgende parameters instellen:
 * `Name`Geeft de naam Hallo van Hallo EventSource toocollect.
 * `Level`Hiermee geeft u Hallo niveau toocollect logboekregistratie. Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Optioneel) bevat trefwoorden combinaties toouse Hallo gehele getal.

## <a name="using-diagnosticsource-events"></a>Het gebruik van DiagnosticSource gebeurtenissen
U kunt configureren [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) gebeurtenissen toobe verzonden tooApplication Insights als traceringen. Installeer eerst Hallo [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet-pakket. Bewerk vervolgens Hallo `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Voor elke DiagnosticSource gewenste tootrace, Voeg een vermelding Hello `Name` kenmerk toohello naam van uw DiagnosticSource instellen.

## <a name="using-etw-events"></a>Met behulp van ETW-gebeurtenissen
U kunt ETW-gebeurtenissen toobe tooApplication Insights verzonden als traceringen configureren. Installeer eerst Hallo `Microsoft.ApplicationInsights.EtwCollector` NuGet-pakket. Bewerk vervolgens `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.

> [!NOTE] 
> ETW-gebeurtenissen kunnen alleen worden verzameld als Hallo proces hosting Hallo SDK wordt uitgevoerd onder een identiteit die lid is van 'Gebruikers prestatielogboek' of de groep Administrators.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

U kunt voor elke bron Hallo volgende parameters instellen:
 * `ProviderName`Hallo-naam van Hallo ETW-provider toocollect is.
 * `ProviderGuid`Hiermee geeft u op Hallo GUID van Hallo ETW-provider toocollect kan worden gebruikt in plaats van `ProviderName`.
 * `Level`Hiermee stelt u Hallo niveau toocollect logboekregistratie. Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Optioneel) sets Hallo sleutelwoord combinaties toouse gehele getal.

## <a name="using-hello-trace-api-directly"></a>Hallo API Trace direct gebruik te maken
U kunt rechtstreeks Hallo Application Insights trace-API aanroepen. Hallo logboekregistratie adapters deze API gebruikt.

Bijvoorbeeld:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

U kunt relatief lange gegevens plaatsen in het Hallo-bericht heeft als voordeel van TrackTrace. U kan bijvoorbeeld er postgegevens coderen.

Bovendien kunt u een bericht van ernst niveau tooyour toevoegen. En net als andere telemetrie u eigenschapswaarden waarmee u toohelp filter of zoeken naar verschillende sets van traceringen kunt kunt toevoegen. Bijvoorbeeld:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Hiermee kunt u, zou [zoeken][diagnostic], tooeasily uitfilteren alle Hallo-berichten van een bepaalde ernstniveau betreffende tooa bepaalde database.

## <a name="explore-your-logs"></a>Verken uw logboeken
Uitvoeren van uw app ofwel in de foutopsporingsmodus of live implementeren.

In de overzichtsblade van uw app in [Hallo Application Insights-portal][portal], kies [Search][diagnostic].

![Kies in de Application Insights zoeken](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Search](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

U kunt, bijvoorbeeld:

* Filteren op logboektraceringen of op items met specifieke eigenschappen
* Een specifiek item in detail te controleren.
* Andere telemetrie betreffende toohello vinden dezelfde gebruikersaanvraag (Hallo dat wil zeggen, met dezelfde OperationId)
* Hallo-configuratie van deze pagina als favoriet opslaan

> [!NOTE]
> **Een steekproef.** Als uw toepassing grote hoeveelheden gegevens verzendt en u Hallo Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden. [Meer informatie over steekproeven.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Volgende stappen
[Onderzoeken fouten en uitzonderingen in ASP.NET][exceptions]

[Meer informatie over zoekopdracht][diagnostic].

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="how-do-i-do-this-for-java"></a>Hoe kan ik deze voor Java?
Gebruik Hallo [Java logboek adapters](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Er is geen optie Application Insights in contextmenu Hallo-project
* Controle van Application Insights-hulpprogramma's zijn geïnstalleerd op deze machine ontwikkeling. In Visual Studio-menu Extra Zoek uitbreidingen en Updates, naar Application Insights Tools. Als deze niet in Hallo geïnstalleerde tabblad, open het tabblad Online Hallo en installeer deze.
* Dit wordt mogelijk een type project niet wordt ondersteund door de Application Insights-hulpprogramma's. Gebruik [handmatige installatie](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Geen optie logboek adapter Hallo-configuratieprogramma
* Moet u eerst framework voor logboekregistratie van tooinstall Hallo.
* Als u van System.Diagnostics.Trace gebruikmaakt, controleert u of u [geconfigureerd in `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* Hebt u de meest recente versie Hallo van Application Insights hebt? In Visual Studio **extra** menu kiezen **uitbreidingen en Updates**, en open Hallo **Updates** tabblad. Als u hulpprogramma's voor ontwikkelaars webanalyse aanwezig is, klikt u op tooupdate deze.

### <a name="emptykey"></a>Een fout ophalen 'instrumentatiesleutel mag niet leeg zijn'
Lijkt erop dat u Hallo adapter Nuget-pakket registreren zonder dat u installeert Application Insights hebt geïnstalleerd.

Klik in Solution Explorer met de rechtermuisknop op `ApplicationInsights.config` en kies **Update Application Insights**. U krijgt een dialoogvenster met een uitnodiging toosign in tooAzure en maak een Application Insights-resource opnieuw of gebruik een bestaande. Die het probleem moet oplossen.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Ik kan Zie traceringen in diagnostische gegevens doorzoeken, maar niet Hallo andere gebeurtenissen
Het kan duren voor alle Hallo-gebeurtenissen en aanvragen tooget via Hallo pipeline.

### <a name="limits"></a>Hoeveel gegevens behouden blijven?
Verschillende factoren van invloed op Hallo en de hoeveelheid gegevens behouden. Zie Hallo [limieten](app-insights-api-custom-events-metrics.md#limits) sectie van de pagina van Hallo klant gebeurtenis metrische gegevens voor meer informatie. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Ik ben aantal logboekvermeldingen Hallo verwachte niet te zien
Als uw toepassing grote hoeveelheden gegevens verzendt en u Hallo Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden. [Meer informatie over steekproeven.](app-insights-sampling.md)

## <a name="add"></a>Volgende stappen
* [Beschikbaarheid en reactiesnelheid tests instellen][availability]
* [Problemen oplossen][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
