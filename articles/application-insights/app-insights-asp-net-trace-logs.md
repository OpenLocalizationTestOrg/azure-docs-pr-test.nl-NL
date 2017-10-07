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
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="fd104-103">.NET-traceerlogboeken in Application Insights verkennen</span><span class="sxs-lookup"><span data-stu-id="fd104-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="fd104-104">Als u NLog, log4Net of System.Diagnostics.Trace voor diagnostische tracering in uw ASP.NET-toepassing kunt u uw logboeken verzonden te hebben[Azure Application Insights][start], waar u kunt verkennen en zoeken ze.</span><span class="sxs-lookup"><span data-stu-id="fd104-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="fd104-105">Uw logboeken worden samengevoegd met andere Hallo telemetrie afkomstig zijn van uw toepassing, zodat u kunt identificeren Hallo traceringen die zijn gekoppeld aan het onderhoud van de aanvraag van elke gebruiker en ze te correleren met andere gebeurtenissen en de uitzonderingenrapporten.</span><span class="sxs-lookup"><span data-stu-id="fd104-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="fd104-106">Moet u de logboekmodule vastleggen Hallo?</span><span class="sxs-lookup"><span data-stu-id="fd104-106">Do you need hello log capture module?</span></span> <span data-ttu-id="fd104-107">Het is een nuttig adapter voor 3rd derden voorkomen, maar als u niet al gebruikt NLog, log4Net of System.Diagnostics.Trace, kunt u alleen aanroepen [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="fd104-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="fd104-108">Aanmelden met uw app installeren</span><span class="sxs-lookup"><span data-stu-id="fd104-108">Install logging on your app</span></span>
<span data-ttu-id="fd104-109">Uw framework voor logboekregistratie gekozen installeren in uw project.</span><span class="sxs-lookup"><span data-stu-id="fd104-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="fd104-110">Dit moet resulteren in een vermelding in het app.config- of web.config.</span><span class="sxs-lookup"><span data-stu-id="fd104-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="fd104-111">Als u van System.Diagnostics.Trace gebruikmaakt, moet u een vermelding tooweb.config tooadd:</span><span class="sxs-lookup"><span data-stu-id="fd104-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="fd104-112">Application Insights toocollect logboeken configureren</span><span class="sxs-lookup"><span data-stu-id="fd104-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="fd104-113">**[Application Insights tooyour project toevoegen](app-insights-asp-net.md)**  als u die nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="fd104-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="fd104-114">Hier ziet u een optie tooinclude Hallo-logboekverzamelaar.</span><span class="sxs-lookup"><span data-stu-id="fd104-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="fd104-115">Of **Configure Application Insights** met de rechtermuisknop op het project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="fd104-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="fd104-116">Hallo-optie te selecteren**trace verzamelen configureren**.</span><span class="sxs-lookup"><span data-stu-id="fd104-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="fd104-117">*Er zijn geen menu- of logboekbestand collector de optie Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="fd104-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="fd104-118">Probeer [probleemoplossing](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="fd104-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="fd104-119">Handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="fd104-119">Manual installation</span></span>
<span data-ttu-id="fd104-120">Gebruik deze methode als uw projecttype wordt niet ondersteund door Hallo Application Insights-installatieprogramma (bijvoorbeeld een Windows desktop-project).</span><span class="sxs-lookup"><span data-stu-id="fd104-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="fd104-121">Als u van plan toouse log4Net of NLog bent, kunt u deze in uw project installeren.</span><span class="sxs-lookup"><span data-stu-id="fd104-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="fd104-122">Klik in Solution Explorer met de rechtermuisknop op uw project en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="fd104-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="fd104-123">Naar Application Insights zoeken</span><span class="sxs-lookup"><span data-stu-id="fd104-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="fd104-124">Selecteer de juiste pakket Hallo - een van:</span><span class="sxs-lookup"><span data-stu-id="fd104-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="fd104-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace aanroepen)</span><span class="sxs-lookup"><span data-stu-id="fd104-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="fd104-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="fd104-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="fd104-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW-gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="fd104-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="fd104-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="fd104-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="fd104-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="fd104-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="fd104-130">Hallo NuGet-pakket installeert de benodigde assembly Hallo en past tevens web.config of app.config.</span><span class="sxs-lookup"><span data-stu-id="fd104-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="fd104-131">Diagnostische logboeken aanroepen invoegen</span><span class="sxs-lookup"><span data-stu-id="fd104-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="fd104-132">Als u System.Diagnostics.Trace gebruikt, wordt een aanroep van typische zou zijn:</span><span class="sxs-lookup"><span data-stu-id="fd104-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="fd104-133">Als u liever log4net of NLog:</span><span class="sxs-lookup"><span data-stu-id="fd104-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="fd104-134">Het gebruik van EventSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fd104-134">Using EventSource events</span></span>
<span data-ttu-id="fd104-135">U kunt configureren [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gebeurtenissen toobe verzonden tooApplication Insights als traceringen.</span><span class="sxs-lookup"><span data-stu-id="fd104-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="fd104-136">Installeer eerst Hallo `Microsoft.ApplicationInsights.EventSourceListener` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="fd104-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="fd104-137">Bewerk vervolgens `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="fd104-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="fd104-138">U kunt voor elke bron Hallo volgende parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="fd104-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="fd104-139">`Name`Geeft de naam Hallo van Hallo EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="fd104-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="fd104-140">`Level`Hiermee geeft u Hallo niveau toocollect logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="fd104-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="fd104-141">Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="fd104-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="fd104-142">`Keywords`(Optioneel) bevat trefwoorden combinaties toouse Hallo gehele getal.</span><span class="sxs-lookup"><span data-stu-id="fd104-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="fd104-143">Het gebruik van DiagnosticSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fd104-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="fd104-144">U kunt configureren [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) gebeurtenissen toobe verzonden tooApplication Insights als traceringen.</span><span class="sxs-lookup"><span data-stu-id="fd104-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="fd104-145">Installeer eerst Hallo [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="fd104-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="fd104-146">Bewerk vervolgens Hallo `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="fd104-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="fd104-147">Voor elke DiagnosticSource gewenste tootrace, Voeg een vermelding Hello `Name` kenmerk toohello naam van uw DiagnosticSource instellen.</span><span class="sxs-lookup"><span data-stu-id="fd104-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="fd104-148">Met behulp van ETW-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fd104-148">Using ETW events</span></span>
<span data-ttu-id="fd104-149">U kunt ETW-gebeurtenissen toobe tooApplication Insights verzonden als traceringen configureren.</span><span class="sxs-lookup"><span data-stu-id="fd104-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="fd104-150">Installeer eerst Hallo `Microsoft.ApplicationInsights.EtwCollector` NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="fd104-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="fd104-151">Bewerk vervolgens `TelemetryModules` sectie Hallo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) bestand.</span><span class="sxs-lookup"><span data-stu-id="fd104-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="fd104-152">ETW-gebeurtenissen kunnen alleen worden verzameld als Hallo proces hosting Hallo SDK wordt uitgevoerd onder een identiteit die lid is van 'Gebruikers prestatielogboek' of de groep Administrators.</span><span class="sxs-lookup"><span data-stu-id="fd104-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="fd104-153">U kunt voor elke bron Hallo volgende parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="fd104-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="fd104-154">`ProviderName`Hallo-naam van Hallo ETW-provider toocollect is.</span><span class="sxs-lookup"><span data-stu-id="fd104-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="fd104-155">`ProviderGuid`Hiermee geeft u op Hallo GUID van Hallo ETW-provider toocollect kan worden gebruikt in plaats van `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="fd104-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="fd104-156">`Level`Hiermee stelt u Hallo niveau toocollect logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="fd104-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="fd104-157">Een van `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="fd104-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="fd104-158">`Keywords`(Optioneel) sets Hallo sleutelwoord combinaties toouse gehele getal.</span><span class="sxs-lookup"><span data-stu-id="fd104-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="fd104-159">Hallo API Trace direct gebruik te maken</span><span class="sxs-lookup"><span data-stu-id="fd104-159">Using hello Trace API directly</span></span>
<span data-ttu-id="fd104-160">U kunt rechtstreeks Hallo Application Insights trace-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="fd104-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="fd104-161">Hallo logboekregistratie adapters deze API gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fd104-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="fd104-162">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fd104-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="fd104-163">U kunt relatief lange gegevens plaatsen in het Hallo-bericht heeft als voordeel van TrackTrace.</span><span class="sxs-lookup"><span data-stu-id="fd104-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="fd104-164">U kan bijvoorbeeld er postgegevens coderen.</span><span class="sxs-lookup"><span data-stu-id="fd104-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="fd104-165">Bovendien kunt u een bericht van ernst niveau tooyour toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fd104-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="fd104-166">En net als andere telemetrie u eigenschapswaarden waarmee u toohelp filter of zoeken naar verschillende sets van traceringen kunt kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fd104-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="fd104-167">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fd104-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="fd104-168">Hiermee kunt u, zou [zoeken][diagnostic], tooeasily uitfilteren alle Hallo-berichten van een bepaalde ernstniveau betreffende tooa bepaalde database.</span><span class="sxs-lookup"><span data-stu-id="fd104-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="fd104-169">Verken uw logboeken</span><span class="sxs-lookup"><span data-stu-id="fd104-169">Explore your logs</span></span>
<span data-ttu-id="fd104-170">Uitvoeren van uw app ofwel in de foutopsporingsmodus of live implementeren.</span><span class="sxs-lookup"><span data-stu-id="fd104-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="fd104-171">In de overzichtsblade van uw app in [Hallo Application Insights-portal][portal], kies [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="fd104-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Kies in de Application Insights zoeken](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Search](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="fd104-174">U kunt, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fd104-174">You can, for example:</span></span>

* <span data-ttu-id="fd104-175">Filteren op logboektraceringen of op items met specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="fd104-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="fd104-176">Een specifiek item in detail te controleren.</span><span class="sxs-lookup"><span data-stu-id="fd104-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="fd104-177">Andere telemetrie betreffende toohello vinden dezelfde gebruikersaanvraag (Hallo dat wil zeggen, met dezelfde OperationId)</span><span class="sxs-lookup"><span data-stu-id="fd104-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="fd104-178">Hallo-configuratie van deze pagina als favoriet opslaan</span><span class="sxs-lookup"><span data-stu-id="fd104-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="fd104-179">**Een steekproef.**</span><span class="sxs-lookup"><span data-stu-id="fd104-179">**Sampling.**</span></span> <span data-ttu-id="fd104-180">Als uw toepassing grote hoeveelheden gegevens verzendt en u Hallo Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="fd104-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="fd104-181">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="fd104-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="fd104-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fd104-182">Next steps</span></span>
<span data-ttu-id="fd104-183">[Onderzoeken fouten en uitzonderingen in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="fd104-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="fd104-184">[Meer informatie over zoekopdracht][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="fd104-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fd104-185">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="fd104-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="fd104-186">Hoe kan ik deze voor Java?</span><span class="sxs-lookup"><span data-stu-id="fd104-186">How do I do this for Java?</span></span>
<span data-ttu-id="fd104-187">Gebruik Hallo [Java logboek adapters](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="fd104-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="fd104-188">Er is geen optie Application Insights in contextmenu Hallo-project</span><span class="sxs-lookup"><span data-stu-id="fd104-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="fd104-189">Controle van Application Insights-hulpprogramma's zijn geïnstalleerd op deze machine ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="fd104-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="fd104-190">In Visual Studio-menu Extra Zoek uitbreidingen en Updates, naar Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="fd104-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="fd104-191">Als deze niet in Hallo geïnstalleerde tabblad, open het tabblad Online Hallo en installeer deze.</span><span class="sxs-lookup"><span data-stu-id="fd104-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="fd104-192">Dit wordt mogelijk een type project niet wordt ondersteund door de Application Insights-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="fd104-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="fd104-193">Gebruik [handmatige installatie](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="fd104-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="fd104-194">Geen optie logboek adapter Hallo-configuratieprogramma</span><span class="sxs-lookup"><span data-stu-id="fd104-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="fd104-195">Moet u eerst framework voor logboekregistratie van tooinstall Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd104-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="fd104-196">Als u van System.Diagnostics.Trace gebruikmaakt, controleert u of u [geconfigureerd in `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd104-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="fd104-197">Hebt u de meest recente versie Hallo van Application Insights hebt?</span><span class="sxs-lookup"><span data-stu-id="fd104-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="fd104-198">In Visual Studio **extra** menu kiezen **uitbreidingen en Updates**, en open Hallo **Updates** tabblad. Als u hulpprogramma's voor ontwikkelaars webanalyse aanwezig is, klikt u op tooupdate deze.</span><span class="sxs-lookup"><span data-stu-id="fd104-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="fd104-199"><a name="emptykey"></a>Een fout ophalen 'instrumentatiesleutel mag niet leeg zijn'</span><span class="sxs-lookup"><span data-stu-id="fd104-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="fd104-200">Lijkt erop dat u Hallo adapter Nuget-pakket registreren zonder dat u installeert Application Insights hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="fd104-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="fd104-201">Klik in Solution Explorer met de rechtermuisknop op `ApplicationInsights.config` en kies **Update Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="fd104-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="fd104-202">U krijgt een dialoogvenster met een uitnodiging toosign in tooAzure en maak een Application Insights-resource opnieuw of gebruik een bestaande.</span><span class="sxs-lookup"><span data-stu-id="fd104-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="fd104-203">Die het probleem moet oplossen.</span><span class="sxs-lookup"><span data-stu-id="fd104-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="fd104-204">Ik kan Zie traceringen in diagnostische gegevens doorzoeken, maar niet Hallo andere gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fd104-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="fd104-205">Het kan duren voor alle Hallo-gebeurtenissen en aanvragen tooget via Hallo pipeline.</span><span class="sxs-lookup"><span data-stu-id="fd104-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="fd104-206"><a name="limits"></a>Hoeveel gegevens behouden blijven?</span><span class="sxs-lookup"><span data-stu-id="fd104-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="fd104-207">Verschillende factoren van invloed op Hallo en de hoeveelheid gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="fd104-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="fd104-208">Zie Hallo [limieten](app-insights-api-custom-events-metrics.md#limits) sectie van de pagina van Hallo klant gebeurtenis metrische gegevens voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fd104-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="fd104-209">Ik ben aantal logboekvermeldingen Hallo verwachte niet te zien</span><span class="sxs-lookup"><span data-stu-id="fd104-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="fd104-210">Als uw toepassing grote hoeveelheden gegevens verzendt en u Hallo Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of hoger gebruikt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="fd104-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="fd104-211">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="fd104-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="fd104-212"><a name="add"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fd104-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="fd104-213">[Beschikbaarheid en reactiesnelheid tests instellen][availability]</span><span class="sxs-lookup"><span data-stu-id="fd104-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="fd104-214">[Problemen oplossen][qna]</span><span class="sxs-lookup"><span data-stu-id="fd104-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
