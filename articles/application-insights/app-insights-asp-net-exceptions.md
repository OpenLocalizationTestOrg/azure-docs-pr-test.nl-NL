---
title: aaaDiagnose fouten en uitzonderingen in web-apps met Azure Application Insights | Microsoft Docs
description: Uitzonderingen op de ASP.NET-apps samen met aanvraagtelemetrie vastleggen.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="691a7-103">Diagnose van uitzonderingen in uw web-apps met Application Insights</span><span class="sxs-lookup"><span data-stu-id="691a7-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="691a7-104">Uitzonderingen in uw live web-app worden gerapporteerd door [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="691a7-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="691a7-105">U kunt mislukte aanvragen correleren met uitzonderingen en andere gebeurtenissen bij zowel Hallo-client en server, zodat u snel kunt u onderzoeken Hallo oorzaken.</span><span class="sxs-lookup"><span data-stu-id="691a7-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="691a7-106">Uitzondering reporting instellen</span><span class="sxs-lookup"><span data-stu-id="691a7-106">Set up exception reporting</span></span>
* <span data-ttu-id="691a7-107">toohave-uitzonderingen die zijn gerapporteerd door uw app server:</span><span class="sxs-lookup"><span data-stu-id="691a7-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="691a7-108">Installeer [Application Insights-SDK](app-insights-asp-net.md) in uw app-code of</span><span class="sxs-lookup"><span data-stu-id="691a7-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="691a7-109">IIS-webservers: Voer [Application Insights-Agent](app-insights-monitor-performance-live-website-now.md); of</span><span class="sxs-lookup"><span data-stu-id="691a7-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="691a7-110">Azure-web-apps: Hallo toevoegen [Application Insights-extensie](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="691a7-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="691a7-111">Java-web-apps: installatie Hallo [Java-agent](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="691a7-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="691a7-112">Hallo installeren [JavaScript-fragment](app-insights-javascript.md) in uw webpagina's toocatch browseruitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="691a7-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="691a7-113">In sommige App-frameworks of met een aantal instellingen, moet u tootake een aantal extra stappen toocatch meer uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="691a7-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="691a7-114">Webformulieren</span><span class="sxs-lookup"><span data-stu-id="691a7-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="691a7-115">MVC</span><span class="sxs-lookup"><span data-stu-id="691a7-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="691a7-116">Web-API-1.*</span><span class="sxs-lookup"><span data-stu-id="691a7-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="691a7-117">Web-API 2.*</span><span class="sxs-lookup"><span data-stu-id="691a7-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="691a7-118">WCF</span><span class="sxs-lookup"><span data-stu-id="691a7-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="691a7-119">Diagnose van uitzonderingen met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="691a7-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="691a7-120">Open Hallo app oplossing in Visual Studio toohelp met foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="691a7-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="691a7-121">Hallo-app, uitvoeren op de server of op uw ontwikkelcomputer met behulp van F5.</span><span class="sxs-lookup"><span data-stu-id="691a7-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="691a7-122">Venster van de Application Insights zoeken Hallo openen in Visual Studio en stel deze toodisplay gebeurtenissen van uw app.</span><span class="sxs-lookup"><span data-stu-id="691a7-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="691a7-123">Terwijl u fouten opspoort, kunt u dit doen door te klikken op de knop Application Insights Hallo.</span><span class="sxs-lookup"><span data-stu-id="691a7-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Met de rechtermuisknop op het Hallo-project en kies Application Insights openen.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="691a7-125">U ziet dat u alleen uitzonderingen voor Hallo rapport tooshow kunt filteren.</span><span class="sxs-lookup"><span data-stu-id="691a7-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="691a7-126">*Er zijn geen uitzonderingen weergegeven? Zie [vastleggen uitzonderingen](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="691a7-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="691a7-127">Klik op een rapport uitzondering tooshow de stacktracering.</span><span class="sxs-lookup"><span data-stu-id="691a7-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="691a7-128">Klik op de verwijzing naar een regel in de stacktracering hello, tooopen Hallo relevante codebestand.</span><span class="sxs-lookup"><span data-stu-id="691a7-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="691a7-129">U ziet dat CodeLens gegevens over Hallo uitzonderingen bevat in Hallo-code:</span><span class="sxs-lookup"><span data-stu-id="691a7-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![CodeLens melding van uitzonderingen.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="691a7-131">Hello Azure-portal met fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="691a7-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="691a7-132">Hallo Application Insights-overzicht van uw app, Hallo fouten tegel ziet u diagrammen van uitzonderingen en mislukte HTTP-aanvragen, samen met een lijst met Hallo aanvragen URL's die ertoe leiden de meest voorkomende fouten Hallo dat.</span><span class="sxs-lookup"><span data-stu-id="691a7-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Instellingen, fouten selecteren](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="691a7-134">Klik door een van de Hallo is mislukt, uitzondering typen in Hallo lijst tooget tooindividual voorvallen Hallo uitzondering, kunt u Hallo details bekijken en stacktracering:</span><span class="sxs-lookup"><span data-stu-id="691a7-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Selecteer een exemplaar van een mislukte aanvraag en onder uitzonderingsdetails, kunt u tooinstances van Hallo-uitzondering.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="691a7-136">**U kunt ook** u kunt starten vanuit Hallo lijst met aanvragen en uitzonderingen gerelateerde tooit.</span><span class="sxs-lookup"><span data-stu-id="691a7-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="691a7-137">*Er zijn geen uitzonderingen weergegeven? Zie [vastleggen uitzonderingen](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="691a7-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="691a7-138">Aangepaste tracering en logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="691a7-138">Custom tracing and log data</span></span>
<span data-ttu-id="691a7-139">tooget diagnostische gegevens specifieke tooyour app, kunt u code toosend uw eigen telemetriegegevens.</span><span class="sxs-lookup"><span data-stu-id="691a7-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="691a7-140">Dit weergegeven in de diagnostische gegevens doorzoeken naast Hallo aanvraag, paginaweergave en andere gegevens automatisch verzameld.</span><span class="sxs-lookup"><span data-stu-id="691a7-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="691a7-141">U hebt verschillende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="691a7-141">You have several options:</span></span>

* <span data-ttu-id="691a7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) wordt doorgaans gebruikt voor het bewaken van gebruikspatronen maar Hallo gegevens ook worden verzonden, wordt weergegeven onder aangepaste gebeurtenissen in diagnostische gegevens doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="691a7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="691a7-143">Gebeurtenissen zijn benoemde beheerverkeersstromen kan uitvoeren en eigenschappen van een verbindingsreeks en numerieke metrische gegevens waarop u kunt [uw diagnostische zoekopdrachten filteren](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="691a7-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="691a7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) kunt u meer gegevens zoals POST informatie verzenden.</span><span class="sxs-lookup"><span data-stu-id="691a7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="691a7-145">[TrackException()](#exceptions) verzendt stack-traces.</span><span class="sxs-lookup"><span data-stu-id="691a7-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="691a7-146">[Meer informatie over uitzonderingen](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="691a7-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="691a7-147">Als u al een framework voor logboekregistratie zoals Log4Net of NLog gebruikt, kunt u [deze logboeken vastleggen](app-insights-asp-net-trace-logs.md) en ze ziet in diagnostische gegevens doorzoeken samen met de aanvraag en uitzonderingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="691a7-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="691a7-148">Deze gebeurtenissen, opent u toosee [Search](app-insights-diagnostic-search.md)Filter openen en kies vervolgens Custom Event, Trace of uitzondering.</span><span class="sxs-lookup"><span data-stu-id="691a7-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![In detail analyseren](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="691a7-150">Als uw app veel telemetrie genereert, beperkt Hallo adaptieve steekproeven module automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden.</span><span class="sxs-lookup"><span data-stu-id="691a7-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="691a7-151">Gebeurtenissen die deel van Hallo dezelfde bewerking worden geselecteerd of gedeselecteerd als groep, uitmaken zodat u tussen gerelateerde gebeurtenissen kunt navigeren.</span><span class="sxs-lookup"><span data-stu-id="691a7-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="691a7-152">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="691a7-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="691a7-153">Hoe toosee postgegevens aanvragen</span><span class="sxs-lookup"><span data-stu-id="691a7-153">How toosee request POST data</span></span>
<span data-ttu-id="691a7-154">Aanvraaggegevens bevatten geen Hallo gegevens tooyour app verzonden in een POST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="691a7-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="691a7-155">toohave deze gegevens vermeld:</span><span class="sxs-lookup"><span data-stu-id="691a7-155">toohave this data reported:</span></span>

* <span data-ttu-id="691a7-156">[Hallo SDK installeren](app-insights-asp-net.md) in uw toepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="691a7-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="691a7-157">Voeg de code in uw toepassing toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="691a7-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="691a7-158">Hallo postgegevens in parameter voor Hallo-bericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="691a7-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="691a7-159">Er is een grootte van de toohello toegestaan beperken zodat u toosend alleen Hallo essentiële gegevens moet proberen.</span><span class="sxs-lookup"><span data-stu-id="691a7-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="691a7-160">Wanneer u bij het onderzoeken van een mislukte aanvraag vinden traceringen Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="691a7-160">When you investigate a failed request, find hello associated traces.</span></span>  

![In detail analyseren](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="691a7-162"><a name="exceptions"></a>Vastleggen van uitzonderingen en verwante diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="691a7-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="691a7-163">Aanvankelijk ziet u niet in de portal Hallo alle Hallo uitzonderingen die ontstaan in uw app problemen.</span><span class="sxs-lookup"><span data-stu-id="691a7-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="691a7-164">Ziet u alle browseruitzonderingen (als u Hallo [JavaScript SDK](app-insights-javascript.md) in uw webpagina's).</span><span class="sxs-lookup"><span data-stu-id="691a7-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="691a7-165">Maar de meeste serveruitzonderingen zijn opgepikt door IIS en u een stukje code toosee toowrite hebt ze.</span><span class="sxs-lookup"><span data-stu-id="691a7-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="691a7-166">U kunt:</span><span class="sxs-lookup"><span data-stu-id="691a7-166">You can:</span></span>

* <span data-ttu-id="691a7-167">**Meld u uitzonderingen expliciet** door code te plaatsen in uitzondering handlers tooreport Hallo uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="691a7-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="691a7-168">**Uitzonderingen automatisch vastleggen** door het configureren van uw ASP.NET-framework.</span><span class="sxs-lookup"><span data-stu-id="691a7-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="691a7-169">Hallo nodig toevoegingen zijn verschillend voor verschillende soorten framework.</span><span class="sxs-lookup"><span data-stu-id="691a7-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="691a7-170">Uitzonderingen expliciet rapportage</span><span class="sxs-lookup"><span data-stu-id="691a7-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="691a7-171">Hallo is eenvoudigste manier een aanroep van tooTrackException() in een uitzonderings-handler tooinsert.</span><span class="sxs-lookup"><span data-stu-id="691a7-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="691a7-172">Javascript</span><span class="sxs-lookup"><span data-stu-id="691a7-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="691a7-173">C#</span><span class="sxs-lookup"><span data-stu-id="691a7-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="691a7-174">VB</span><span class="sxs-lookup"><span data-stu-id="691a7-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="691a7-175">Hallo-eigenschappen en metingen parameters zijn optioneel, maar zijn handig voor [filtering en toe te voegen](app-insights-diagnostic-search.md) extra informatie.</span><span class="sxs-lookup"><span data-stu-id="691a7-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="691a7-176">Als u een app hebt die verschillende games kunt uitvoeren, kan u bijvoorbeeld alle Hallo uitzondering rapporten verwante tooa bepaald spel vinden.</span><span class="sxs-lookup"><span data-stu-id="691a7-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="691a7-177">U kunt zoveel objecten toevoegen als u zoals tooeach woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="691a7-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="691a7-178">Browseruitzonderingen</span><span class="sxs-lookup"><span data-stu-id="691a7-178">Browser exceptions</span></span>
<span data-ttu-id="691a7-179">De meeste browseruitzonderingen worden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="691a7-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="691a7-180">Als de webpagina scriptbestanden van netwerken die inhoud leveren of andere domeinen bevat, zorg ervoor dat uw scriptcode Hallo-kenmerk heeft ```crossorigin="anonymous"```, en verzendt deze server Hallo [CORS headers](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="691a7-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="691a7-181">Hierdoor kunt u een stack-trace tooget en details voor niet-verwerkte JavaScript-uitzonderingen van deze resources.</span><span class="sxs-lookup"><span data-stu-id="691a7-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="691a7-182">Webformulieren</span><span class="sxs-lookup"><span data-stu-id="691a7-182">Web forms</span></span>
<span data-ttu-id="691a7-183">Hallo HTTP-Module zijn voor webformulieren kunnen toocollect Hallo uitzonderingen toe wanneer er geen omleidingen geconfigureerd met CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="691a7-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="691a7-184">Maar als er actieve omleidingen, Hallo volgen regels toohello Application_Error functie in Global.asax.cs toevoegen.</span><span class="sxs-lookup"><span data-stu-id="691a7-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="691a7-185">(Het bestand Global.asax toevoegen als u er nog geen hebt).</span><span class="sxs-lookup"><span data-stu-id="691a7-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="691a7-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="691a7-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="691a7-187">MVC</span><span class="sxs-lookup"><span data-stu-id="691a7-187">MVC</span></span>
<span data-ttu-id="691a7-188">Als hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuratie is `Off`, en vervolgens uitzonderingen beschikbaar voor Hallo zijn [HTTP-Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="691a7-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="691a7-189">Echter, als het `RemoteOnly` (standaard), of `On`, Hallo uitzondering worden gewist en niet beschikbaar voor Application Insights tooautomatically verzamelen.</span><span class="sxs-lookup"><span data-stu-id="691a7-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="691a7-190">U kunt dit oplossen door het overschrijven van Hallo [System.Web.Mvc.HandleErrorAttribute klasse](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), en het toepassen van hallo overschreven klasse zoals weergegeven voor Hallo verschillende MVC versies onderstaande ([github-bron](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="691a7-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="691a7-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="691a7-191">MVC 2</span></span>
<span data-ttu-id="691a7-192">Hallo HandleError kenmerk vervangen door uw nieuw kenmerk in uw domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="691a7-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="691a7-193">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="691a7-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="691a7-194">MVC 3</span></span>
<span data-ttu-id="691a7-195">Registreren `AiHandleErrorAttribute` als globaal filter in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="691a7-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="691a7-196">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="691a7-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="691a7-197">MVC 4, MVC5</span></span>
<span data-ttu-id="691a7-198">Registreer AiHandleErrorAttribute als globaal filter in FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="691a7-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="691a7-199">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="691a7-200">Web-API 1.x</span><span class="sxs-lookup"><span data-stu-id="691a7-200">Web API 1.x</span></span>
<span data-ttu-id="691a7-201">System.Web.Http.Filters.ExceptionFilterAttribute overschrijven:</span><span class="sxs-lookup"><span data-stu-id="691a7-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="691a7-202">U kunt deze overschreven kenmerk toospecific domeincontrollers toevoegt of toohello globaal filterconfiguratie in Hallo WebApiConfig klasse toevoegen:</span><span class="sxs-lookup"><span data-stu-id="691a7-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="691a7-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="691a7-204">Er zijn een aantal cases dat Hallo uitzondering filters kunnen niet worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="691a7-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="691a7-205">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="691a7-205">For example:</span></span>

* <span data-ttu-id="691a7-206">Uitzonderingen uit controller constructors.</span><span class="sxs-lookup"><span data-stu-id="691a7-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="691a7-207">Uitzonderingen uit bericht handlers.</span><span class="sxs-lookup"><span data-stu-id="691a7-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="691a7-208">Uitzonderingen bij routering.</span><span class="sxs-lookup"><span data-stu-id="691a7-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="691a7-209">Uitzonderingen tijdens de serialisatie van reacties inhoud.</span><span class="sxs-lookup"><span data-stu-id="691a7-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="691a7-210">Web-API 2.x</span><span class="sxs-lookup"><span data-stu-id="691a7-210">Web API 2.x</span></span>
<span data-ttu-id="691a7-211">Voeg een implementatie van IExceptionLogger toe:</span><span class="sxs-lookup"><span data-stu-id="691a7-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="691a7-212">Deze services toohello op WebApiConfig toevoegen:</span><span class="sxs-lookup"><span data-stu-id="691a7-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="691a7-213">}</span><span class="sxs-lookup"><span data-stu-id="691a7-213">}</span></span>

[<span data-ttu-id="691a7-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="691a7-215">Als alternatief, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="691a7-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="691a7-216">Vervang Hallo alleen ExceptionHandler met een aangepaste implementatie van IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="691a7-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="691a7-217">Dit wordt alleen genoemd wanneer Hallo-framework is nog steeds kunnen toochoose welke antwoord bericht toosend (niet op Hallo verbinding voor exemplaar is afgebroken)</span><span class="sxs-lookup"><span data-stu-id="691a7-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="691a7-218">Uitzondering Filters (zoals beschreven in de sectie Hallo op Web-API 1.x domeincontrollers hierboven) - is niet in alle gevallen wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="691a7-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="691a7-219">WCF</span><span class="sxs-lookup"><span data-stu-id="691a7-219">WCF</span></span>
<span data-ttu-id="691a7-220">Toevoegen van een klasse met kenmerk uitbreidt en IErrorHandler en IServiceBehavior implementeert.</span><span class="sxs-lookup"><span data-stu-id="691a7-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="691a7-221">Hallo kenmerk toohello-serverimplementaties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="691a7-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="691a7-222">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="691a7-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="691a7-223">Uitzondering-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="691a7-223">Exception performance counters</span></span>
<span data-ttu-id="691a7-224">Als u hebt [Hallo Application Insights-Agent geïnstalleerd](app-insights-monitor-performance-live-website-now.md) op uw server, kunt u een grafiek van Hallo uitzonderingen snelheid, gemeten door .NET krijgen.</span><span class="sxs-lookup"><span data-stu-id="691a7-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="691a7-225">Dit omvat verwerkte en onverwerkte uitzonderingen voor .NET.</span><span class="sxs-lookup"><span data-stu-id="691a7-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="691a7-226">Een metriek Explorer-blade geopend, Voeg een nieuwe grafiek toe en selecteer **uitzondering snelheid**, vermeld onder prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="691a7-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="691a7-227">Hallo .NET framework berekent Hallo snelheid Hallo aantal uitzonderingen in een interval tellen en te delen door Hallo lengte van hello-interval.</span><span class="sxs-lookup"><span data-stu-id="691a7-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="691a7-228">Houd er rekening mee dat deze wordt afwijken van Hallo 'uitzonderingen' aantal berekend door Hallo Application Insights-portal te tellen TrackException rapporten.</span><span class="sxs-lookup"><span data-stu-id="691a7-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="691a7-229">Hallo steekproefintervals zijn verschillend en Hallo SDK niet TrackException rapporten voor alle verwerkte en onverwerkte uitzonderingen verzenden.</span><span class="sxs-lookup"><span data-stu-id="691a7-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="691a7-230">Video</span><span class="sxs-lookup"><span data-stu-id="691a7-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="691a7-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="691a7-231">Next steps</span></span>
* [<span data-ttu-id="691a7-232">REST, SQL en andere toodependencies aanroepen bewaken</span><span class="sxs-lookup"><span data-stu-id="691a7-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="691a7-233">Laadtijden voor pagina's, browseruitzonderingen en AJAX-aanroepen bewaken</span><span class="sxs-lookup"><span data-stu-id="691a7-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="691a7-234">Prestatiemeteritems van monitor</span><span class="sxs-lookup"><span data-stu-id="691a7-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
