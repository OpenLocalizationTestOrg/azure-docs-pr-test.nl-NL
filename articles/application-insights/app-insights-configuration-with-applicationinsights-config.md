---
title: aaaApplicationInsights.config referentie - Azure | Microsoft Docs
description: In- of uitschakelen van gegevens verzameling modules en prestatiemeteritems en andere parameters toevoegen.
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Hallo Application Insights-SDK configureren met ApplicationInsights.config of .xml
Hallo Application Insights-SDK voor .NET bestaat uit een aantal NuGet-pakketten. De [core-pakket](http://www.nuget.org/packages/Microsoft.ApplicationInsights) Hallo API biedt voor het verzenden van telemetrie op Hallo van Application Insights. [Extra pakketten](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) bieden telemetrie *modules* en *initializers* voor het automatisch bijhouden van telemetrie van uw toepassing en de context. Door het Hallo-configuratiebestand aanpassen, kunt u inschakelen of uitschakelen van telemetrie-modules en initializers en parameters voor enkele ervan instellen.

Hallo-configuratiebestand heet `ApplicationInsights.config` of `ApplicationInsights.xml`, afhankelijk van uw toepassing hello type. Deze wordt automatisch toegevoegd tooyour project wanneer u [meeste versies van Hallo SDK installeren][start]. Ook wordt toegevoegd tooa web-app door [Status Monitor op een IIS-server][redfield], of wanneer u selecteert Hallo Appplication Insights [uitbreiding voor een Azure-website of virtuele machine](app-insights-azure-web-apps.md).

Er is niet een equivalent bestand toocontrol hello [SDK in een webpagina][client].

Dit document beschrijft Hallo secties die u in Hallo configuratie ziet bestand, en hoe ze Hallo onderdelen van Hallo SDK, beheren en welke NuGet-pakketten laden van deze onderdelen.

## <a name="telemetry-modules-aspnet"></a>Telemetrie-Modules (ASP.NET)
Elke telemetrie-module een specifiek type gegevens verzamelt en Hallo core API toosend Hallo gegevens gebruikt. Hallo-modules zijn geïnstalleerd door verschillende NuGet-pakketten, die ook Hallo vereiste regels toohello .config-bestand toevoegen.

Er is een knooppunt in het Hallo-configuratiebestand voor elke module. een module toodisable Hallo knooppunt verwijderen of opmerking het uit.

### <a name="dependency-tracking"></a>Bijhouden van afhankelijkheid
[Bijhouden van afhankelijkheid](app-insights-asp-net-dependencies.md) verzamelt telemetrie over uw app toodatabases en externe services en databases maakt aanroepen. tooallow deze module toowork in een IIS-server, moet u te[Status Monitor installeren][redfield]. toouse in Azure-web-apps of virtuele machines, [selecteert u de extensie Application Insights Hallo](app-insights-azure-web-apps.md).

U kunt ook uw eigen afhankelijkheid bijhouden met behulp van Hallo code schrijven [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet-pakket.

### <a name="performance-collector"></a>Collector voor prestaties
[Verzamelt systeemprestatiemeteritems](app-insights-performance-counters.md) zoals CPU, geheugen en het netwerk laden van IIS-installaties. U kunt opgeven welke toocollect tellers, met inbegrip van prestatiemeteritems die u zelf hebt ingesteld.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet-pakket.

### <a name="application-insights-diagnostics-telemetry"></a>Diagnostische telemetrie van Application Insights
Hallo `DiagnosticsTelemetryModule` fouten in Application Insights instrumentation code zelf Hallo-rapporten. Bijvoorbeeld, als het Hallo-code heeft geen toegang tot prestatiemeteritems of als een `ITelemetryInitializer` er een uitzondering gegenereerd. Tracetelemetrie bijgehouden door deze module wordt weergegeven in Hallo [diagnostische gegevens doorzoeken][diagnostic]. Diagnostische gegevens toodc.services.vsallin.net verzendt.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet-pakket. Als u alleen dit pakket installeert, wordt niet automatisch Hallo ApplicationInsights.config-bestand gemaakt.

### <a name="developer-mode"></a>Modus voor ontwikkelaars
`DeveloperModeWithDebuggerAttachedTelemetryModule`dwingt Hallo Application Insights `TelemetryChannel` toosend gegevens direct één telemetrie-item op een tijdstip, wanneer een foutopsporingsprogramma is gekoppeld toohello toepassingsproces. Dit vermindert Hallo hoeveelheid tijd tussen Hallo momenteel wanneer uw toepassing worden bijgehouden Telemetrie en wanneer deze op Hallo Application Insights-portal wordt weergegeven. Dit zorgt ervoor dat belangrijke overhead in CPU en netwerkbandbreedte.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet-pakket

### <a name="web-request-tracking"></a>Webaanvraag bijhouden
Rapporten Hallo [tijd en resultaat antwoordcode](app-insights-asp-net.md) van HTTP-aanvragen.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet-pakket

### <a name="exception-tracking"></a>Uitzonderingen bijhouden
`ExceptionTrackingTelemetryModule`houdt de niet-verwerkte uitzonderingen in uw web-app. Zie [fouten en uitzonderingen][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet-pakket
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-nummers [taak uitzonderingen onopgemerkt](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-niet-verwerkte uitzonderingen voor werkrollen, windows-services en consoletoepassingen wordt bijgehouden.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet-pakket.

### <a name="eventsource-tracking"></a>EventSource bijhouden
`EventSourceTelemetryModule`Hiermee kunt u tooconfigure EventSource gebeurtenissen toobe tooApplication Insights als traceringen verzonden. Zie voor meer informatie over het bijhouden van EventSource gebeurtenissen [EventSource gebeurtenissen](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>ETW-gebeurtenissen bijhouden
`EtwCollectorTelemetryModule`Hiermee kunt u tooconfigure gebeurtenissen van ETW-providers toobe tooApplication Insights als traceringen verzonden. Zie voor meer informatie over het bijhouden van ETW-gebeurtenissen [ETW-gebeurtenissen met behulp van](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
Hallo Microsoft.ApplicationInsights pakket biedt Hallo [API core](https://msdn.microsoft.com/library/mt420197.aspx) Hallo SDK. Hallo andere modules telemetrie gebruikt en u kunt ook [toodefine gebruiken uw eigen telemetrie](app-insights-api-custom-events-metrics.md).

* Er is geen vermelding in ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet-pakket. Als u alleen deze NuGet installeert, wordt geen .config-bestand gegenereerd.

## <a name="telemetry-channel"></a>Telemetrie-kanaal
Hallo telemetrie kanaal beheert buffer en verzenden van telemetrie toohello Application Insights-service.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`Hallo standaardkanaal voor services is. Deze buffert gegevens in het geheugen.
* `Microsoft.ApplicationInsights.PersistenceChannel`vormt een alternatief voor consoletoepassingen. Alle unflushed toopersistent gegevensopslag kunt besparen wanneer uw app wordt afgesloten en wordt verzonden wanneer Hallo app opnieuw wordt gestart.

## <a name="telemetry-initializers-aspnet"></a>Telemetrie initalisatiefuncties (ASP.NET)
Telemetrie initalisatiefuncties contexteigenschappen die worden verzonden, samen met elk telemetrie-item worden ingesteld.

U kunt [schrijven van uw eigen initalisatiefuncties](app-insights-api-filtering-sampling.md#add-properties) tooset contexteigenschappen.

Hallo standaard initalisatiefuncties zijn klaar voor gebruik door Hallo Web of WindowsServer NuGet-pakketten:

* `AccountIdTelemetryInitializer`Hallo AccountId eigenschap wordt ingesteld.
* `AuthenticatedUserIdTelemetryInitializer`Hallo AuthenticatedUserId eigenschap ingesteld zoals ingesteld door Hallo JavaScript SDK.
* `AzureRoleEnvironmentTelemetryInitializer`updates Hallo `RoleName` en `RoleInstance` eigenschappen van Hallo `Device` context voor alle telemetrie-items met gegevens uit hello Azure runtime-omgeving.
* `BuildInfoConfigComponentVersionTelemetryInitializer`updates Hallo `Version` eigenschap Hallo `Component` context voor alle telemetrie-items met Hallo-waarde opgehaald uit Hallo `BuildInfo.config` bestand door MS Build gemaakt.
* `ClientIpHeaderTelemetryInitializer`updates `Ip` eigenschap Hallo `Location` context van alle telemetrie-items op basis van Hallo `X-Forwarded-For` HTTP-header van Hallo-aanvraag.
* `DeviceTelemetryInitializer`updates Hallo volgende eigenschappen Hallo `Device` context voor alle telemetrie-items.
  * `Type`te is ingesteld 'PC'
  * `Id`ingesteld toohello-domeinnaam van Hallo-computer waarop de webtoepassing hello wordt uitgevoerd.
  * `OemName`is ingesteld toohello-waarde opgehaald uit Hallo `Win32_ComputerSystem.Manufacturer` veld met WMI.
  * `Model`is ingesteld toohello-waarde opgehaald uit Hallo `Win32_ComputerSystem.Model` veld met WMI.
  * `NetworkType`is ingesteld toohello-waarde opgehaald uit Hallo `NetworkInterface`.
  * `Language`is ingesteld toohello naam Hallo `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`updates Hallo `RoleInstance` eigenschap Hallo `Device` context voor alle telemetrie-items met de domeinnaam Hallo van Hallo-computer waarop de webtoepassing hello wordt uitgevoerd.
* `OperationNameTelemetryInitializer`updates Hallo `Name` eigenschap Hallo `RequestTelemetry` en Hallo `Name` eigenschap Hallo `Operation` context van alle telemetrie-items op basis van Hallo HTTP-methode, evenals de namen van ASP.NET MVC-controller en de actie aangeroepen tooprocess Hallo de aanvraag.
* `OperationIdTelemetryInitializer`of `OperationCorrelationTelemetryInitializer` updates Hallo `Operation.Id` contexteigenschap van alle telemetrie-items bijgehouden tijdens de verwerking van een aanvraag met Hallo automatisch gegenereerd `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`updates Hallo `Id` eigenschap Hallo `Session` context voor alle telemetrie-items met de waarde is opgehaald uit Hallo `ai_session` cookie gegenereerd door Hallo ApplicationInsights JavaScript instrumentation code die wordt uitgevoerd in de browser van Hallo gebruiker.
* `SyntheticTelemetryInitializer`of `SyntheticUserAgentTelemetryInitializer` updates Hallo `User`, `Session` en `Operation` contexten eigenschappen van alle telemetrie-items bijgehouden bij het verwerken van een aanvraag van een synthetische bron, zoals een beschikbaarheid testen of engine bot zoeken. Standaard [Metrics Explorer](app-insights-metrics-explorer.md) synthetische telemetrie niet wordt weergegeven.

    Hallo `<Filters>` instellen van eigenschappen van het Hallo-aanvragen te identificeren.
* `UserAgentTelemetryInitializer`updates Hallo `UserAgent` eigenschap Hallo `User` context van alle telemetrie-items op basis van Hallo `User-Agent` HTTP-header van Hallo-aanvraag.
* `UserTelemetryInitializer`updates Hallo `Id` en `AcquisitionDate` eigenschappen van `User` context voor alle telemetrie-items met waarden die worden opgehaald uit Hallo `ai_user` cookie gegenereerd door Hallo Application Insights JavaScript instrumentation code die wordt uitgevoerd in Hallo de browser van de gebruiker.
* `WebTestTelemetryInitializer`sets Hallo gebruikers-id, de sessie-id en de eigenschappen van synthetische gegevensbron voor HTTP-die afkomstig zijn van van aanvragen [beschikbaarheidstests](app-insights-monitor-web-app-availability.md).
  Hallo `<Filters>` instellen van eigenschappen van het Hallo-aanvragen te identificeren.

Voor .NET-toepassingen in Service Fabric worden uitgevoerd, kunt u Hallo opnemen `Microsoft.ApplicationInsights.ServiceFabric` NuGet-pakket. Dit pakket bevat een `FabricTelemetryInitializer`, zodat het Service Fabric-eigenschappen tootelemetry items wordt toegevoegd. Zie voor meer informatie, Hallo [GitHub-pagina](https://go.microsoft.com/fwlink/?linkid=848457) over Hallo-eigenschappen die zijn toegevoegd door dit pakket NuGet.

## <a name="telemetry-processors-aspnet"></a>Telemetrie-Processors (ASP.NET)
Telemetrie-processors kunnen filteren en wijzigen van elk telemetrie-item vlak voordat deze wordt verzonden vanuit Hallo SDK toohello portal.

U kunt [de processors van uw eigen telemetrie schrijven](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Adaptieve steekproeven telemetrie processor (van 2.0.0-beta3)
Deze optie is standaard ingeschakeld. Als uw app veel telemetrie verzendt, worden deze processor enkele ervan.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

Hallo parameter biedt Hallo doel dat Hallo algoritme probeert tooachieve. Elk exemplaar van Hallo SDK werkt onafhankelijk, dus als uw server een cluster met meerdere machines, daadwerkelijk volume Hallo telemetrie dienovereenkomstig wordt vermenigvuldigd.

[Meer informatie over steekproeven](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Vast aantal steekproeven telemetrie processor (van 2.0.0-beta1)
Er is ook een standaard [steekproef nemen telemetrie processor](app-insights-api-filtering-sampling.md) (van 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Kanaalparameters (Java)
Deze parameters beïnvloeden hoe Hallo Java SDK moet opslaan en leegmaken Hallo telemetrische gegevens die worden verzameld.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
Hallo aantal telemetrie-items die kunnen worden opgeslagen in een van de SDK Hallo geheugenopslag. Wanneer dit aantal is bereikt, Hallo telemetrie buffer moet worden leeggemaakt - dat wil zeggen, de telemetrie-items Hallo toohello Application Insights-server worden verzonden.

* Min: 1
* Max: 1000
* Standaard: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Hiermee wordt bepaald hoe vaak hello gegevens die zijn opgeslagen in Hallo geheugenopslag moet worden leeggemaakt (verzonden tooApplication Insights).

* Min: 1
* Max: 300
* Standaard: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Hallo maximale grootte in MB die is toegewezen voor permanente opslag op de lokale schijf Hallo toohello bepaalt. Deze opslag wordt gebruikt voor persistente telemetrie-items die toobe verzonden toohello Application Insights-eindpunt is mislukt. Wanneer de opslaggrootte Hallo is voldaan, wordt nieuwe telemetrie-items worden genegeerd.

* Min: 1
* Max: 100
* Standaard: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Hiermee bepaalt u Hallo Application Insights-resource waarin uw gegevens worden weergegeven. Doorgaans maakt u een afzonderlijke resource met een afzonderlijke sleutel voor elk van uw toepassingen.

Als u wilt dat tooset Hallo sleutel dynamisch - bijvoorbeeld als u wilt dat toosend resultaten van uw toepassing toodifferent resources - kunt u weglaten Hallo sleutel uit het configuratiebestand Hallo en stel deze in de code in plaats daarvan.

tooset hello sleutel voor alle exemplaren van TelemetryClient, inclusief standaard telemetrie modules, instellen Hallo-sleutel in TelemetryConfiguration.Active. Dit doen in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Als u wilt dat alleen toosend een specifieke set gebeurtenissen tooa andere resource, kunt u Hallo-sleutel voor een specifieke TelemetryClient instellen:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

een nieuwe sleutel tooget [Maak een nieuwe resource in Application Insights-portal Hallo][new].

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Hallo API][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
