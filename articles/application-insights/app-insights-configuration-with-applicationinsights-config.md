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
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="1f456-103">Hallo Application Insights-SDK configureren met ApplicationInsights.config of .xml</span><span class="sxs-lookup"><span data-stu-id="1f456-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="1f456-104">Hallo Application Insights-SDK voor .NET bestaat uit een aantal NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="1f456-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="1f456-105">De [core-pakket](http://www.nuget.org/packages/Microsoft.ApplicationInsights) Hallo API biedt voor het verzenden van telemetrie op Hallo van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1f456-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="1f456-106">[Extra pakketten](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) bieden telemetrie *modules* en *initializers* voor het automatisch bijhouden van telemetrie van uw toepassing en de context.</span><span class="sxs-lookup"><span data-stu-id="1f456-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="1f456-107">Door het Hallo-configuratiebestand aanpassen, kunt u inschakelen of uitschakelen van telemetrie-modules en initializers en parameters voor enkele ervan instellen.</span><span class="sxs-lookup"><span data-stu-id="1f456-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="1f456-108">Hallo-configuratiebestand heet `ApplicationInsights.config` of `ApplicationInsights.xml`, afhankelijk van uw toepassing hello type.</span><span class="sxs-lookup"><span data-stu-id="1f456-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="1f456-109">Deze wordt automatisch toegevoegd tooyour project wanneer u [meeste versies van Hallo SDK installeren][start].</span><span class="sxs-lookup"><span data-stu-id="1f456-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="1f456-110">Ook wordt toegevoegd tooa web-app door [Status Monitor op een IIS-server][redfield], of wanneer u selecteert Hallo Appplication Insights [uitbreiding voor een Azure-website of virtuele machine](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1f456-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1f456-111">Er is niet een equivalent bestand toocontrol hello [SDK in een webpagina][client].</span><span class="sxs-lookup"><span data-stu-id="1f456-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="1f456-112">Dit document beschrijft Hallo secties die u in Hallo configuratie ziet bestand, en hoe ze Hallo onderdelen van Hallo SDK, beheren en welke NuGet-pakketten laden van deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="1f456-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="1f456-113">Telemetrie-Modules (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f456-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="1f456-114">Elke telemetrie-module een specifiek type gegevens verzamelt en Hallo core API toosend Hallo gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f456-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="1f456-115">Hallo-modules zijn geïnstalleerd door verschillende NuGet-pakketten, die ook Hallo vereiste regels toohello .config-bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f456-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="1f456-116">Er is een knooppunt in het Hallo-configuratiebestand voor elke module.</span><span class="sxs-lookup"><span data-stu-id="1f456-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="1f456-117">een module toodisable Hallo knooppunt verwijderen of opmerking het uit.</span><span class="sxs-lookup"><span data-stu-id="1f456-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="1f456-118">Bijhouden van afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="1f456-118">Dependency Tracking</span></span>
<span data-ttu-id="1f456-119">[Bijhouden van afhankelijkheid](app-insights-asp-net-dependencies.md) verzamelt telemetrie over uw app toodatabases en externe services en databases maakt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1f456-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="1f456-120">tooallow deze module toowork in een IIS-server, moet u te[Status Monitor installeren][redfield].</span><span class="sxs-lookup"><span data-stu-id="1f456-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="1f456-121">toouse in Azure-web-apps of virtuele machines, [selecteert u de extensie Application Insights Hallo](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1f456-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1f456-122">U kunt ook uw eigen afhankelijkheid bijhouden met behulp van Hallo code schrijven [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="1f456-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="1f456-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="1f456-124">Collector voor prestaties</span><span class="sxs-lookup"><span data-stu-id="1f456-124">Performance collector</span></span>
<span data-ttu-id="1f456-125">[Verzamelt systeemprestatiemeteritems](app-insights-performance-counters.md) zoals CPU, geheugen en het netwerk laden van IIS-installaties.</span><span class="sxs-lookup"><span data-stu-id="1f456-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="1f456-126">U kunt opgeven welke toocollect tellers, met inbegrip van prestatiemeteritems die u zelf hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f456-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="1f456-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="1f456-128">Diagnostische telemetrie van Application Insights</span><span class="sxs-lookup"><span data-stu-id="1f456-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="1f456-129">Hallo `DiagnosticsTelemetryModule` fouten in Application Insights instrumentation code zelf Hallo-rapporten.</span><span class="sxs-lookup"><span data-stu-id="1f456-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="1f456-130">Bijvoorbeeld, als het Hallo-code heeft geen toegang tot prestatiemeteritems of als een `ITelemetryInitializer` er een uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1f456-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="1f456-131">Tracetelemetrie bijgehouden door deze module wordt weergegeven in Hallo [diagnostische gegevens doorzoeken][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1f456-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="1f456-132">Diagnostische gegevens toodc.services.vsallin.net verzendt.</span><span class="sxs-lookup"><span data-stu-id="1f456-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="1f456-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1f456-134">Als u alleen dit pakket installeert, wordt niet automatisch Hallo ApplicationInsights.config-bestand gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1f456-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="1f456-135">Modus voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1f456-135">Developer Mode</span></span>
<span data-ttu-id="1f456-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`dwingt Hallo Application Insights `TelemetryChannel` toosend gegevens direct één telemetrie-item op een tijdstip, wanneer een foutopsporingsprogramma is gekoppeld toohello toepassingsproces.</span><span class="sxs-lookup"><span data-stu-id="1f456-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="1f456-137">Dit vermindert Hallo hoeveelheid tijd tussen Hallo momenteel wanneer uw toepassing worden bijgehouden Telemetrie en wanneer deze op Hallo Application Insights-portal wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f456-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="1f456-138">Dit zorgt ervoor dat belangrijke overhead in CPU en netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="1f456-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="1f456-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="1f456-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="1f456-140">Webaanvraag bijhouden</span><span class="sxs-lookup"><span data-stu-id="1f456-140">Web Request Tracking</span></span>
<span data-ttu-id="1f456-141">Rapporten Hallo [tijd en resultaat antwoordcode](app-insights-asp-net.md) van HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1f456-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="1f456-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="1f456-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="1f456-143">Uitzonderingen bijhouden</span><span class="sxs-lookup"><span data-stu-id="1f456-143">Exception tracking</span></span>
<span data-ttu-id="1f456-144">`ExceptionTrackingTelemetryModule`houdt de niet-verwerkte uitzonderingen in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="1f456-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="1f456-145">Zie [fouten en uitzonderingen][exceptions].</span><span class="sxs-lookup"><span data-stu-id="1f456-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="1f456-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="1f456-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="1f456-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-nummers [taak uitzonderingen onopgemerkt](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f456-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="1f456-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-niet-verwerkte uitzonderingen voor werkrollen, windows-services en consoletoepassingen wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="1f456-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="1f456-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="1f456-150">EventSource bijhouden</span><span class="sxs-lookup"><span data-stu-id="1f456-150">EventSource Tracking</span></span>
<span data-ttu-id="1f456-151">`EventSourceTelemetryModule`Hiermee kunt u tooconfigure EventSource gebeurtenissen toobe tooApplication Insights als traceringen verzonden.</span><span class="sxs-lookup"><span data-stu-id="1f456-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1f456-152">Zie voor meer informatie over het bijhouden van EventSource gebeurtenissen [EventSource gebeurtenissen](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="1f456-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="1f456-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="1f456-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="1f456-154">ETW-gebeurtenissen bijhouden</span><span class="sxs-lookup"><span data-stu-id="1f456-154">ETW Event Tracking</span></span>
<span data-ttu-id="1f456-155">`EtwCollectorTelemetryModule`Hiermee kunt u tooconfigure gebeurtenissen van ETW-providers toobe tooApplication Insights als traceringen verzonden.</span><span class="sxs-lookup"><span data-stu-id="1f456-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1f456-156">Zie voor meer informatie over het bijhouden van ETW-gebeurtenissen [ETW-gebeurtenissen met behulp van](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="1f456-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="1f456-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="1f456-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="1f456-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="1f456-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="1f456-159">Hallo Microsoft.ApplicationInsights pakket biedt Hallo [API core](https://msdn.microsoft.com/library/mt420197.aspx) Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="1f456-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="1f456-160">Hallo andere modules telemetrie gebruikt en u kunt ook [toodefine gebruiken uw eigen telemetrie](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="1f456-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="1f456-161">Er is geen vermelding in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="1f456-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="1f456-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1f456-163">Als u alleen deze NuGet installeert, wordt geen .config-bestand gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1f456-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="1f456-164">Telemetrie-kanaal</span><span class="sxs-lookup"><span data-stu-id="1f456-164">Telemetry Channel</span></span>
<span data-ttu-id="1f456-165">Hallo telemetrie kanaal beheert buffer en verzenden van telemetrie toohello Application Insights-service.</span><span class="sxs-lookup"><span data-stu-id="1f456-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="1f456-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`Hallo standaardkanaal voor services is.</span><span class="sxs-lookup"><span data-stu-id="1f456-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="1f456-167">Deze buffert gegevens in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="1f456-167">It buffers data in memory.</span></span>
* <span data-ttu-id="1f456-168">`Microsoft.ApplicationInsights.PersistenceChannel`vormt een alternatief voor consoletoepassingen.</span><span class="sxs-lookup"><span data-stu-id="1f456-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="1f456-169">Alle unflushed toopersistent gegevensopslag kunt besparen wanneer uw app wordt afgesloten en wordt verzonden wanneer Hallo app opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="1f456-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="1f456-170">Telemetrie initalisatiefuncties (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f456-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="1f456-171">Telemetrie initalisatiefuncties contexteigenschappen die worden verzonden, samen met elk telemetrie-item worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f456-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="1f456-172">U kunt [schrijven van uw eigen initalisatiefuncties](app-insights-api-filtering-sampling.md#add-properties) tooset contexteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1f456-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="1f456-173">Hallo standaard initalisatiefuncties zijn klaar voor gebruik door Hallo Web of WindowsServer NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="1f456-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="1f456-174">`AccountIdTelemetryInitializer`Hallo AccountId eigenschap wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f456-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="1f456-175">`AuthenticatedUserIdTelemetryInitializer`Hallo AuthenticatedUserId eigenschap ingesteld zoals ingesteld door Hallo JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="1f456-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="1f456-176">`AzureRoleEnvironmentTelemetryInitializer`updates Hallo `RoleName` en `RoleInstance` eigenschappen van Hallo `Device` context voor alle telemetrie-items met gegevens uit hello Azure runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f456-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="1f456-177">`BuildInfoConfigComponentVersionTelemetryInitializer`updates Hallo `Version` eigenschap Hallo `Component` context voor alle telemetrie-items met Hallo-waarde opgehaald uit Hallo `BuildInfo.config` bestand door MS Build gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1f456-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="1f456-178">`ClientIpHeaderTelemetryInitializer`updates `Ip` eigenschap Hallo `Location` context van alle telemetrie-items op basis van Hallo `X-Forwarded-For` HTTP-header van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1f456-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="1f456-179">`DeviceTelemetryInitializer`updates Hallo volgende eigenschappen Hallo `Device` context voor alle telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="1f456-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="1f456-180">`Type`te is ingesteld 'PC'</span><span class="sxs-lookup"><span data-stu-id="1f456-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="1f456-181">`Id`ingesteld toohello-domeinnaam van Hallo-computer waarop de webtoepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f456-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="1f456-182">`OemName`is ingesteld toohello-waarde opgehaald uit Hallo `Win32_ComputerSystem.Manufacturer` veld met WMI.</span><span class="sxs-lookup"><span data-stu-id="1f456-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="1f456-183">`Model`is ingesteld toohello-waarde opgehaald uit Hallo `Win32_ComputerSystem.Model` veld met WMI.</span><span class="sxs-lookup"><span data-stu-id="1f456-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="1f456-184">`NetworkType`is ingesteld toohello-waarde opgehaald uit Hallo `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="1f456-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="1f456-185">`Language`is ingesteld toohello naam Hallo `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="1f456-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="1f456-186">`DomainNameRoleInstanceTelemetryInitializer`updates Hallo `RoleInstance` eigenschap Hallo `Device` context voor alle telemetrie-items met de domeinnaam Hallo van Hallo-computer waarop de webtoepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f456-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="1f456-187">`OperationNameTelemetryInitializer`updates Hallo `Name` eigenschap Hallo `RequestTelemetry` en Hallo `Name` eigenschap Hallo `Operation` context van alle telemetrie-items op basis van Hallo HTTP-methode, evenals de namen van ASP.NET MVC-controller en de actie aangeroepen tooprocess Hallo de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1f456-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="1f456-188">`OperationIdTelemetryInitializer`of `OperationCorrelationTelemetryInitializer` updates Hallo `Operation.Id` contexteigenschap van alle telemetrie-items bijgehouden tijdens de verwerking van een aanvraag met Hallo automatisch gegenereerd `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="1f456-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="1f456-189">`SessionTelemetryInitializer`updates Hallo `Id` eigenschap Hallo `Session` context voor alle telemetrie-items met de waarde is opgehaald uit Hallo `ai_session` cookie gegenereerd door Hallo ApplicationInsights JavaScript instrumentation code die wordt uitgevoerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1f456-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1f456-190">`SyntheticTelemetryInitializer`of `SyntheticUserAgentTelemetryInitializer` updates Hallo `User`, `Session` en `Operation` contexten eigenschappen van alle telemetrie-items bijgehouden bij het verwerken van een aanvraag van een synthetische bron, zoals een beschikbaarheid testen of engine bot zoeken.</span><span class="sxs-lookup"><span data-stu-id="1f456-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="1f456-191">Standaard [Metrics Explorer](app-insights-metrics-explorer.md) synthetische telemetrie niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f456-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="1f456-192">Hallo `<Filters>` instellen van eigenschappen van het Hallo-aanvragen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="1f456-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="1f456-193">`UserAgentTelemetryInitializer`updates Hallo `UserAgent` eigenschap Hallo `User` context van alle telemetrie-items op basis van Hallo `User-Agent` HTTP-header van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1f456-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="1f456-194">`UserTelemetryInitializer`updates Hallo `Id` en `AcquisitionDate` eigenschappen van `User` context voor alle telemetrie-items met waarden die worden opgehaald uit Hallo `ai_user` cookie gegenereerd door Hallo Application Insights JavaScript instrumentation code die wordt uitgevoerd in Hallo de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1f456-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1f456-195">`WebTestTelemetryInitializer`sets Hallo gebruikers-id, de sessie-id en de eigenschappen van synthetische gegevensbron voor HTTP-die afkomstig zijn van van aanvragen [beschikbaarheidstests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="1f456-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="1f456-196">Hallo `<Filters>` instellen van eigenschappen van het Hallo-aanvragen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="1f456-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="1f456-197">Voor .NET-toepassingen in Service Fabric worden uitgevoerd, kunt u Hallo opnemen `Microsoft.ApplicationInsights.ServiceFabric` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="1f456-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="1f456-198">Dit pakket bevat een `FabricTelemetryInitializer`, zodat het Service Fabric-eigenschappen tootelemetry items wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1f456-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="1f456-199">Zie voor meer informatie, Hallo [GitHub-pagina](https://go.microsoft.com/fwlink/?linkid=848457) over Hallo-eigenschappen die zijn toegevoegd door dit pakket NuGet.</span><span class="sxs-lookup"><span data-stu-id="1f456-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="1f456-200">Telemetrie-Processors (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f456-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="1f456-201">Telemetrie-processors kunnen filteren en wijzigen van elk telemetrie-item vlak voordat deze wordt verzonden vanuit Hallo SDK toohello portal.</span><span class="sxs-lookup"><span data-stu-id="1f456-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="1f456-202">U kunt [de processors van uw eigen telemetrie schrijven](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="1f456-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="1f456-203">Adaptieve steekproeven telemetrie processor (van 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="1f456-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="1f456-204">Deze optie is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1f456-204">This is enabled by default.</span></span> <span data-ttu-id="1f456-205">Als uw app veel telemetrie verzendt, worden deze processor enkele ervan.</span><span class="sxs-lookup"><span data-stu-id="1f456-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="1f456-206">Hallo parameter biedt Hallo doel dat Hallo algoritme probeert tooachieve.</span><span class="sxs-lookup"><span data-stu-id="1f456-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="1f456-207">Elk exemplaar van Hallo SDK werkt onafhankelijk, dus als uw server een cluster met meerdere machines, daadwerkelijk volume Hallo telemetrie dienovereenkomstig wordt vermenigvuldigd.</span><span class="sxs-lookup"><span data-stu-id="1f456-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="1f456-208">[Meer informatie over steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="1f456-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="1f456-209">Vast aantal steekproeven telemetrie processor (van 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="1f456-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="1f456-210">Er is ook een standaard [steekproef nemen telemetrie processor](app-insights-api-filtering-sampling.md) (van 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="1f456-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="1f456-211">Kanaalparameters (Java)</span><span class="sxs-lookup"><span data-stu-id="1f456-211">Channel parameters (Java)</span></span>
<span data-ttu-id="1f456-212">Deze parameters beïnvloeden hoe Hallo Java SDK moet opslaan en leegmaken Hallo telemetrische gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="1f456-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="1f456-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="1f456-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="1f456-214">Hallo aantal telemetrie-items die kunnen worden opgeslagen in een van de SDK Hallo geheugenopslag.</span><span class="sxs-lookup"><span data-stu-id="1f456-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="1f456-215">Wanneer dit aantal is bereikt, Hallo telemetrie buffer moet worden leeggemaakt - dat wil zeggen, de telemetrie-items Hallo toohello Application Insights-server worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="1f456-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="1f456-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1f456-216">Min: 1</span></span>
* <span data-ttu-id="1f456-217">Max: 1000</span><span class="sxs-lookup"><span data-stu-id="1f456-217">Max: 1000</span></span>
* <span data-ttu-id="1f456-218">Standaard: 500</span><span class="sxs-lookup"><span data-stu-id="1f456-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="1f456-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="1f456-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="1f456-220">Hiermee wordt bepaald hoe vaak hello gegevens die zijn opgeslagen in Hallo geheugenopslag moet worden leeggemaakt (verzonden tooApplication Insights).</span><span class="sxs-lookup"><span data-stu-id="1f456-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="1f456-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1f456-221">Min: 1</span></span>
* <span data-ttu-id="1f456-222">Max: 300</span><span class="sxs-lookup"><span data-stu-id="1f456-222">Max: 300</span></span>
* <span data-ttu-id="1f456-223">Standaard: 5</span><span class="sxs-lookup"><span data-stu-id="1f456-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="1f456-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="1f456-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="1f456-225">Hallo maximale grootte in MB die is toegewezen voor permanente opslag op de lokale schijf Hallo toohello bepaalt.</span><span class="sxs-lookup"><span data-stu-id="1f456-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="1f456-226">Deze opslag wordt gebruikt voor persistente telemetrie-items die toobe verzonden toohello Application Insights-eindpunt is mislukt.</span><span class="sxs-lookup"><span data-stu-id="1f456-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="1f456-227">Wanneer de opslaggrootte Hallo is voldaan, wordt nieuwe telemetrie-items worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="1f456-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="1f456-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1f456-228">Min: 1</span></span>
* <span data-ttu-id="1f456-229">Max: 100</span><span class="sxs-lookup"><span data-stu-id="1f456-229">Max: 100</span></span>
* <span data-ttu-id="1f456-230">Standaard: 10</span><span class="sxs-lookup"><span data-stu-id="1f456-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="1f456-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="1f456-231">InstrumentationKey</span></span>
<span data-ttu-id="1f456-232">Hiermee bepaalt u Hallo Application Insights-resource waarin uw gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f456-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="1f456-233">Doorgaans maakt u een afzonderlijke resource met een afzonderlijke sleutel voor elk van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1f456-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="1f456-234">Als u wilt dat tooset Hallo sleutel dynamisch - bijvoorbeeld als u wilt dat toosend resultaten van uw toepassing toodifferent resources - kunt u weglaten Hallo sleutel uit het configuratiebestand Hallo en stel deze in de code in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="1f456-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="1f456-235">tooset hello sleutel voor alle exemplaren van TelemetryClient, inclusief standaard telemetrie modules, instellen Hallo-sleutel in TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="1f456-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="1f456-236">Dit doen in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice:</span><span class="sxs-lookup"><span data-stu-id="1f456-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="1f456-237">Als u wilt dat alleen toosend een specifieke set gebeurtenissen tooa andere resource, kunt u Hallo-sleutel voor een specifieke TelemetryClient instellen:</span><span class="sxs-lookup"><span data-stu-id="1f456-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="1f456-238">een nieuwe sleutel tooget [Maak een nieuwe resource in Application Insights-portal Hallo][new].</span><span class="sxs-lookup"><span data-stu-id="1f456-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f456-239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f456-239">Next steps</span></span>
<span data-ttu-id="1f456-240">[Meer informatie over Hallo API][api].</span><span class="sxs-lookup"><span data-stu-id="1f456-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
