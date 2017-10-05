---
title: .NET-traceerlogboeken in Application Insights verkennen
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
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="a8c28-103">.NET-traceerlogboeken in Application Insights verkennen</span><span class="sxs-lookup"><span data-stu-id="a8c28-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="a8c28-104">Als u NLog, log4Net of System.Diagnostics.Trace voor diagnostische tracering in uw ASP.NET-toepassing kunt u uw verzonden naar Logboeken hebben [Azure Application Insights][start], waar u kunt verkennen en ze te zoeken.</span><span class="sxs-lookup"><span data-stu-id="a8c28-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="a8c28-105">Uw logboeken worden samengevoegd met de andere telemetrie die afkomstig zijn van uw toepassing, zodat de traceringen die zijn gekoppeld aan het onderhoud van de aanvraag van elke gebruiker te identificeren en ze met andere gebeurtenissen en de uitzonderingenrapporten correleren.</span><span class="sxs-lookup"><span data-stu-id="a8c28-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c28-106">Moet u de module toepassingslogboek vastleggen?</span><span class="sxs-lookup"><span data-stu-id="a8c28-106">Do you need the log capture module?</span></span> <span data-ttu-id="a8c28-107">Het is een nuttig adapter voor 3rd derden voorkomen, maar als u niet al gebruikt NLog, log4Net of System.Diagnostics.Trace, kunt u alleen aanroepen [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="a8c28-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="a8c28-108">Aanmelden met uw app installeren</span><span class="sxs-lookup"><span data-stu-id="a8c28-108">Install logging on your app</span></span>
<span data-ttu-id="a8c28-109">Uw framework voor logboekregistratie gekozen installeren in uw project.</span><span class="sxs-lookup"><span data-stu-id="a8c28-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="a8c28-110">Dit moet resulteren in een vermelding in het app.config- of web.config.</span><span class="sxs-lookup"><span data-stu-id="a8c28-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="a8c28-111">Als u van System.Diagnostics.Trace gebruikmaakt, moet u een vermelding toevoegen aan web.config:</span><span class="sxs-lookup"><span data-stu-id="a8c28-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

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
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="a8c28-112">Application Insights voor het verzamelen van logboeken configureren</span><span class="sxs-lookup"><span data-stu-id="a8c28-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="a8c28-113">**[Application Insights toevoegen aan uw project](app-insights-asp-net.md)**  als u die nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="a8c28-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="a8c28-114">Hier ziet u een optie om op te nemen van de logboekverzamelaar.</span><span class="sxs-lookup"><span data-stu-id="a8c28-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="a8c28-115">Of **Configure Application Insights** met de rechtermuisknop op het project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="a8c28-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="a8c28-116">Selecteer de optie voor **trace verzamelen configureren**.</span><span class="sxs-lookup"><span data-stu-id="a8c28-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="a8c28-117">*Er zijn geen menu- of logboekbestand collector de optie Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="a8c28-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="a8c28-118">Probeer [probleemoplossing](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a8c28-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="a8c28-119">Handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="a8c28-119">Manual installation</span></span>
<span data-ttu-id="a8c28-120">Gebruik deze methode als uw projecttype wordt niet ondersteund door de Application Insights-installatieprogramma (bijvoorbeeld een Windows desktop-project).</span><span class="sxs-lookup"><span data-stu-id="a8c28-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="a8c28-121">Als u van plan bent om log4Net of NLog te gebruiken, kunt u deze in uw project installeren.</span><span class="sxs-lookup"><span data-stu-id="a8c28-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="a8c28-122">Klik in Solution Explorer met de rechtermuisknop op uw project en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="a8c28-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="a8c28-123">Naar Application Insights zoeken</span><span class="sxs-lookup"><span data-stu-id="a8c28-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="a8c28-124">Selecteer het juiste pakket - een van:</span><span class="sxs-lookup"><span data-stu-id="a8c28-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="a8c28-125">Microsoft.ApplicationInsights.TraceListener (om vast te leggen System.Diagnostics.Trace aanroepen)</span><span class="sxs-lookup"><span data-stu-id="a8c28-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="a8c28-126">Microsoft.ApplicationInsights.EventSourceListener (vast te leggen EventSource gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="a8c28-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="a8c28-127">Microsoft.ApplicationInsights.EtwListener (om vast te leggen ETW-gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="a8c28-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="a8c28-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="a8c28-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="a8c28-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="a8c28-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="a8c28-130">Het NuGet-pakket installeert de benodigde assembly's en past tevens web.config of app.config.</span><span class="sxs-lookup"><span data-stu-id="a8c28-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="a8c28-131">Diagnostische logboeken aanroepen invoegen</span><span class="sxs-lookup"><span data-stu-id="a8c28-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="a8c28-132">Als u System.Diagnostics.Trace gebruikt, wordt een aanroep van typische zou zijn:</span><span class="sxs-lookup"><span data-stu-id="a8c28-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="a8c28-133">Als u liever log4net of NLog:</span><span class="sxs-lookup"><span data-stu-id="a8c28-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="a8c28-134">Het gebruik van EventSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a8c28-134">Using EventSource events</span></span>
<span data-ttu-id="a8c28-135">U kunt configureren [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gebeurtenissen naar Application Insights als traceringen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="a8c28-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="a8c28-136">Installeer eerst de `Microsoft.ApplicationInsights.EventSourceListener` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="a8c28-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="a8c28-137">Bewerk vervolgens `TelemetryModules` sectie van de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="a8c28-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="a8c28-138">Voor elke bron, kunt u de volgende parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="a8c28-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="a8c28-139">`Name`Hiermee geeft u de naam van de EventSource te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="a8c28-140">`Level`Hiermee geeft u het logboekregistratieniveau te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="a8c28-141">Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="a8c28-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="a8c28-142">`Keywords`(Optioneel) Hiermee geeft u de gehele waarde van combinaties van trefwoorden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a8c28-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="a8c28-143">Het gebruik van DiagnosticSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a8c28-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="a8c28-144">U kunt configureren [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) gebeurtenissen naar Application Insights als traceringen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="a8c28-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="a8c28-145">Installeer eerst de [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="a8c28-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="a8c28-146">Bewerk vervolgens de `TelemetryModules` sectie van de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="a8c28-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="a8c28-147">Voor elke DiagnosticSource die u traceren wilt, Voeg een vermelding met de `Name` -kenmerk ingesteld op de naam van uw DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="a8c28-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="a8c28-148">Met behulp van ETW-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a8c28-148">Using ETW events</span></span>
<span data-ttu-id="a8c28-149">U kunt configureren ETW-gebeurtenissen naar Application Insights als traceringen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="a8c28-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="a8c28-150">Installeer eerst de `Microsoft.ApplicationInsights.EtwCollector` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="a8c28-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="a8c28-151">Bewerk vervolgens `TelemetryModules` sectie van de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="a8c28-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="a8c28-152">ETW-gebeurtenissen kunnen alleen worden verzameld als het proces voor het hosten van de SDK wordt uitgevoerd onder een identiteit die lid is van 'Gebruikers prestatielogboek' of de groep Administrators.</span><span class="sxs-lookup"><span data-stu-id="a8c28-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="a8c28-153">Voor elke bron, kunt u de volgende parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="a8c28-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="a8c28-154">`ProviderName`is de naam van de ETW-provider te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="a8c28-155">`ProviderGuid`Geeft de GUID van de ETW-provider moet worden verzameld, kunnen worden gebruikt in plaats van `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="a8c28-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="a8c28-156">`Level`Hiermee stelt u het logboekregistratieniveau te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="a8c28-157">Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="a8c28-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="a8c28-158">`Keywords`(Optioneel) stelt de integerwaarde van combinaties van trefwoorden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a8c28-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="a8c28-159">De tracering API direct gebruik te maken</span><span class="sxs-lookup"><span data-stu-id="a8c28-159">Using the Trace API directly</span></span>
<span data-ttu-id="a8c28-160">U kunt rechtstreeks de Application Insights trace API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="a8c28-161">De adapters logboekregistratie gebruiken deze API.</span><span class="sxs-lookup"><span data-stu-id="a8c28-161">The logging adapters use this API.</span></span>

<span data-ttu-id="a8c28-162">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a8c28-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="a8c28-163">U kunt relatief lange gegevens plaatsen in het bericht heeft als voordeel van TrackTrace.</span><span class="sxs-lookup"><span data-stu-id="a8c28-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="a8c28-164">U kan bijvoorbeeld er postgegevens coderen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="a8c28-165">U kunt bovendien een urgentieniveau toevoegen aan het bericht.</span><span class="sxs-lookup"><span data-stu-id="a8c28-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="a8c28-166">En net als andere telemetrie u eigenschapswaarden die u gebruiken kunt om te filteren of zoeken naar verschillende sets van traceringen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="a8c28-167">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a8c28-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="a8c28-168">Hiermee kunt u, zou [zoeken][diagnostic], gemakkelijk kunt uitfilteren alle berichten van een bepaalde ernstniveau met betrekking tot een bepaalde database.</span><span class="sxs-lookup"><span data-stu-id="a8c28-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="a8c28-169">Verken uw logboeken</span><span class="sxs-lookup"><span data-stu-id="a8c28-169">Explore your logs</span></span>
<span data-ttu-id="a8c28-170">Uitvoeren van uw app ofwel in de foutopsporingsmodus of live implementeren.</span><span class="sxs-lookup"><span data-stu-id="a8c28-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="a8c28-171">In de overzichtsblade van uw app in [de Application Insights-portal][portal], kies [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="a8c28-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Kies in de Application Insights zoeken](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Search](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="a8c28-174">U kunt, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a8c28-174">You can, for example:</span></span>

* <span data-ttu-id="a8c28-175">Filteren op logboektraceringen of op items met specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a8c28-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="a8c28-176">Een specifiek item in detail te controleren.</span><span class="sxs-lookup"><span data-stu-id="a8c28-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="a8c28-177">Andere telemetrie met betrekking tot de dezelfde gebruikersaanvraag vinden (dat wil zeggen, met de dezelfde OperationId)</span><span class="sxs-lookup"><span data-stu-id="a8c28-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="a8c28-178">De configuratie van deze pagina als favoriet opslaan</span><span class="sxs-lookup"><span data-stu-id="a8c28-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="a8c28-179">**Een steekproef.**</span><span class="sxs-lookup"><span data-stu-id="a8c28-179">**Sampling.**</span></span> <span data-ttu-id="a8c28-180">Als uw toepassing grote hoeveelheden gegevens verzendt en u de Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, stuurt de functie voor adaptieve steekproeven mogelijk slechts een percentage van uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="a8c28-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="a8c28-181">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="a8c28-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="a8c28-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a8c28-182">Next steps</span></span>
<span data-ttu-id="a8c28-183">[Onderzoeken fouten en uitzonderingen in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="a8c28-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="a8c28-184">[Meer informatie over zoekopdracht][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="a8c28-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a8c28-185">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="a8c28-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="a8c28-186">Hoe kan ik deze voor Java?</span><span class="sxs-lookup"><span data-stu-id="a8c28-186">How do I do this for Java?</span></span>
<span data-ttu-id="a8c28-187">Gebruik de [Java logboek adapters](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8c28-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="a8c28-188">Er is geen optie Application Insights in het contextmenu van project</span><span class="sxs-lookup"><span data-stu-id="a8c28-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="a8c28-189">Controle van Application Insights-hulpprogramma's zijn geïnstalleerd op deze machine ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="a8c28-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="a8c28-190">In Visual Studio-menu Extra Zoek uitbreidingen en Updates, naar Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="a8c28-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="a8c28-191">Als deze niet in het tabblad geïnstalleerd, opent u het tabblad Online en installeer deze.</span><span class="sxs-lookup"><span data-stu-id="a8c28-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="a8c28-192">Dit wordt mogelijk een type project niet wordt ondersteund door de Application Insights-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="a8c28-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="a8c28-193">Gebruik [handmatige installatie](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="a8c28-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="a8c28-194">Er is geen optie logboek adapter in het configuratiehulpprogramma</span><span class="sxs-lookup"><span data-stu-id="a8c28-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="a8c28-195">U moet eerst installeren van het framework voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="a8c28-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="a8c28-196">Als u van System.Diagnostics.Trace gebruikmaakt, controleert u of u [geconfigureerd in `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8c28-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="a8c28-197">Hebt u de nieuwste versie van Application Insights hebt?</span><span class="sxs-lookup"><span data-stu-id="a8c28-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="a8c28-198">In Visual Studio **extra** menu kiezen **uitbreidingen en Updates**, en open de **Updates** tabblad. Als u hulpprogramma's voor ontwikkelaars webanalyse aanwezig is, klikt u op om bij te werken.</span><span class="sxs-lookup"><span data-stu-id="a8c28-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="a8c28-199"><a name="emptykey"></a>Een fout ophalen 'instrumentatiesleutel mag niet leeg zijn'</span><span class="sxs-lookup"><span data-stu-id="a8c28-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="a8c28-200">Lijkt erop dat u de logboekregistratie adapter Nuget-pakket geïnstalleerd zonder Application Insights te installeren.</span><span class="sxs-lookup"><span data-stu-id="a8c28-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="a8c28-201">Klik in Solution Explorer met de rechtermuisknop op `ApplicationInsights.config` en kies **Update Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="a8c28-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="a8c28-202">U krijgt een dialoogvenster met een uitnodiging aan te melden bij Azure en maak een Application Insights-resource opnieuw of gebruik een bestaande.</span><span class="sxs-lookup"><span data-stu-id="a8c28-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="a8c28-203">Die het probleem moet oplossen.</span><span class="sxs-lookup"><span data-stu-id="a8c28-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="a8c28-204">Zie ik traceringen in diagnostische gegevens doorzoeken, maar niet de andere gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a8c28-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="a8c28-205">Het kan duren voor de gebeurtenissen en aanvragen voor ophalen via de pipeline.</span><span class="sxs-lookup"><span data-stu-id="a8c28-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="a8c28-206"><a name="limits"></a>Hoeveel gegevens behouden blijven?</span><span class="sxs-lookup"><span data-stu-id="a8c28-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="a8c28-207">Verschillende factoren van invloed op de hoeveelheid gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="a8c28-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="a8c28-208">Zie de [limieten](app-insights-api-custom-events-metrics.md#limits) sectie van de pagina klant gebeurtenis metrische gegevens voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a8c28-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="a8c28-209">Ik zie niet sommige van de logboekvermeldingen die ik verwacht</span><span class="sxs-lookup"><span data-stu-id="a8c28-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="a8c28-210">Als uw toepassing grote hoeveelheden gegevens verzendt en u de Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, stuurt de functie voor adaptieve steekproeven mogelijk slechts een percentage van uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="a8c28-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="a8c28-211">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="a8c28-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="a8c28-212"><a name="add"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a8c28-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="a8c28-213">[Beschikbaarheid en reactiesnelheid tests instellen][availability]</span><span class="sxs-lookup"><span data-stu-id="a8c28-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="a8c28-214">[Problemen oplossen][qna]</span><span class="sxs-lookup"><span data-stu-id="a8c28-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
