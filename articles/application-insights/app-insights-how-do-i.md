---
title: aaaHow kan ik... in Azure Application Insights | Microsoft Docs
description: Veelgestelde vragen in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="dc2d2-103">Hoe kan ik ... in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="dc2d2-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="dc2d2-104">Ontvang een e-mail wanneer...</span><span class="sxs-lookup"><span data-stu-id="dc2d2-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="dc2d2-105">E-mailadres als Mijn site uitvalt</span><span class="sxs-lookup"><span data-stu-id="dc2d2-105">Email if my site goes down</span></span>
<span data-ttu-id="dc2d2-106">Stel een [beschikbaarheid WebTest](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="dc2d2-107">E-als Mijn site is overbelast</span><span class="sxs-lookup"><span data-stu-id="dc2d2-107">Email if my site is overloaded</span></span>
<span data-ttu-id="dc2d2-108">Stel een [waarschuwing](app-insights-alerts.md) op **serverreactietijd**.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="dc2d2-109">Een drempelwaarde tussen 1 en 2 seconden zouden moeten werken.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="dc2d2-110">Uw app mogelijk tekenen van stam ook weergeven door te retourneren van de fout-codes.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="dc2d2-111">Een waarschuwing instellen voor **mislukte aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="dc2d2-112">Als u wilt dat een waarschuwing tooset op **serveruitzonderingen**, moet u wellicht toodo [enkele aanvullende instellingen](app-insights-asp-net-exceptions.md) in volgorde toosee gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="dc2d2-113">E-uitzonderingen op</span><span class="sxs-lookup"><span data-stu-id="dc2d2-113">Email on exceptions</span></span>
1. [<span data-ttu-id="dc2d2-114">Uitzonderingenmonitor instellen</span><span class="sxs-lookup"><span data-stu-id="dc2d2-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="dc2d2-115">[Een waarschuwing instellen](app-insights-alerts.md) tellen metriek op Hallo uitzondering</span><span class="sxs-lookup"><span data-stu-id="dc2d2-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="dc2d2-116">E-mail bekijkt op een gebeurtenis in mijn app</span><span class="sxs-lookup"><span data-stu-id="dc2d2-116">Email on an event in my app</span></span>
<span data-ttu-id="dc2d2-117">Stel de gewenste tooget een e-mailbericht wanneer een bepaalde gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="dc2d2-118">Application Insights geen biedt deze mogelijkheid rechtstreeks, maar dit kan [een waarschuwing verzonden wanneer een metriek een drempelwaarde overschrijden](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="dc2d2-119">Waarschuwingen kunnen worden ingesteld voor [aangepaste metrische gegevens](app-insights-api-custom-events-metrics.md#trackmetric)echter geen aangepaste gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="dc2d2-120">Schrijf sommige tooincrease code een metriek bij Hallo-gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="dc2d2-121">Of:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="dc2d2-122">Omdat waarschuwingen twee statussen hebben, hebt u toosend een lage waarde wanneer u rekening houden met Hallo waarschuwing toohave beëindigd:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="dc2d2-123">Maken van een grafiek in [metrische explorer](app-insights-metrics-explorer.md) toosee uw alarm:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="dc2d2-124">Een waarschuwing toofire wordt nu ingesteld wanneer Hallo metriek hoger dan de waarde van een mid gedurende een korte periode is:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="dc2d2-125">Hallo gemiddelde periode toohello minimum ingesteld.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="dc2d2-126">U krijgt e-mailberichten wanneer Hallo metriek boven gaat en onder de drempelwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="dc2d2-127">Sommige tooconsider punten:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-127">Some points tooconsider:</span></span>

* <span data-ttu-id="dc2d2-128">Een waarschuwing heeft twee statussen ('waarschuwing' en 'goede').</span><span class="sxs-lookup"><span data-stu-id="dc2d2-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="dc2d2-129">Hallo staat alleen geëvalueerd wanneer een metriek is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="dc2d2-130">Een e-mailbericht wordt alleen verzonden wanneer Hallo status verandert.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="dc2d2-131">Dit is de reden waarom u toosend hebt metrische gegevens voor hoge en lage waarde.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="dc2d2-132">tooevaluate hello waarschuwing Hallo gemiddelde is overgenomen van Hallo ontvangen waarden Hallo voorgaande periode.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="dc2d2-133">Dit gebeurt telkens wanneer een metriek is ontvangen, zodat e-mailberichten vaker dan de ingestelde periode voor Hallo kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="dc2d2-134">Omdat e-mailberichten worden verzonden op 'waarschuwing' en 'goede', kunt u tooconsider opnieuw gegevensclassificatie uw eindresultaat gebeurtenis als een voorwaarde voor twee statussen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="dc2d2-135">Bijvoorbeeld, in plaats van een gebeurtenis 'taak is voltooid' hebben een voorwaarde 'taak wordt uitgevoerd' waarop u e-mailberichten aan Hallo begin en einde van een taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="dc2d2-136">Waarschuwingen automatisch instellen</span><span class="sxs-lookup"><span data-stu-id="dc2d2-136">Set up alerts automatically</span></span>
[<span data-ttu-id="dc2d2-137">Gebruik PowerShell toocreate nieuwe waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="dc2d2-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="dc2d2-138">PowerShell tooManage Application Insights gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc2d2-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="dc2d2-139">Maken van nieuwe resources</span><span class="sxs-lookup"><span data-stu-id="dc2d2-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="dc2d2-140">Nieuwe waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="dc2d2-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="dc2d2-141">Afzonderlijke telemetrie van verschillende versies</span><span class="sxs-lookup"><span data-stu-id="dc2d2-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="dc2d2-142">Meerdere rollen in een app: gebruiken één Application Insights-resource en filtert u op cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="dc2d2-143">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="dc2d2-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="dc2d2-144">Scheiden van ontwikkeling, testen en release-versies: verschillende Application Insights-bronnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="dc2d2-145">Hallo instrumentatiesleutels uit web.config worden opgepikt. [Meer informatie](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="dc2d2-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="dc2d2-146">Reporting bouwen versies: een eigenschap met een initialisatiefunctie telemetrie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="dc2d2-147">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="dc2d2-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="dc2d2-148">Back-endservers en bureaublad-apps bewaken</span><span class="sxs-lookup"><span data-stu-id="dc2d2-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="dc2d2-149">[Gebruik de Windows Server SDK module Hallo](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="dc2d2-150">Gegevens visualiseren</span><span class="sxs-lookup"><span data-stu-id="dc2d2-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="dc2d2-151">Dashboard met metrische gegevens vanuit meerdere apps</span><span class="sxs-lookup"><span data-stu-id="dc2d2-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="dc2d2-152">In [metriek Explorer](app-insights-metrics-explorer.md), de grafiek aanpassen en als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="dc2d2-153">Toohello Azure-dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="dc2d2-154">Dashboard met gegevens uit andere bronnen en de Application Insights</span><span class="sxs-lookup"><span data-stu-id="dc2d2-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="dc2d2-155">[Exporteren van telemetrie tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="dc2d2-156">of</span><span class="sxs-lookup"><span data-stu-id="dc2d2-156">Or</span></span>

* <span data-ttu-id="dc2d2-157">SharePoint gebruiken als uw dashboard, het weergeven van gegevens in de SharePoint-webonderdelen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="dc2d2-158">[Continue export en Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="dc2d2-159">Gebruik PowerView tooexamine Hallo database en een SharePoint-webonderdeel voor PowerView maken.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="dc2d2-160">Anonieme of geverifieerde gebruikers filteren</span><span class="sxs-lookup"><span data-stu-id="dc2d2-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="dc2d2-161">Als uw gebruikers zich aanmelden, kunt u instellen Hallo [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users). (Dit gebeurt niet automatisch.)</span><span class="sxs-lookup"><span data-stu-id="dc2d2-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="dc2d2-162">U kunt vervolgens:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-162">You can then:</span></span>

* <span data-ttu-id="dc2d2-163">Zoeken naar specifieke gebruikers-id 's</span><span class="sxs-lookup"><span data-stu-id="dc2d2-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="dc2d2-164">Metrische gegevens tooeither anonieme of geverifieerde gebruikers filteren</span><span class="sxs-lookup"><span data-stu-id="dc2d2-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="dc2d2-165">Wijzig de namen van eigenschappen of waarden</span><span class="sxs-lookup"><span data-stu-id="dc2d2-165">Modify property names or values</span></span>
<span data-ttu-id="dc2d2-166">Maak een [filter](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="dc2d2-167">Hiermee kunt u wijzigen of filteren van telemetrie voordat deze van uw app tooApplication Insights wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="dc2d2-168">Lijst van specifieke gebruikers en hun gebruik</span><span class="sxs-lookup"><span data-stu-id="dc2d2-168">List specific users and their usage</span></span>
<span data-ttu-id="dc2d2-169">Als u alleen te wilt[zoeken naar specifieke gebruikers](#search-specific-users), kunt u instellen dat Hallo [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="dc2d2-170">Als u wilt dat een lijst met gebruikers met gegevens zoals welke pagina's ze bekijken of hoe vaak deze zich aanmeldt, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="dc2d2-171">[Set geverifieerde gebruiker-id](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa database exporteren](app-insights-code-sample-export-sql-stream-analytics.md) en geschikte gebruik hulpprogramma's tooanalyze er uw gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="dc2d2-172">Als u slechts een klein aantal gebruikers hebt, aangepaste gebeurtenissen of metrische gegevens, met behulp van gegevens van belang Hallo Hallo metrische waarde of de gebeurtenisnaam van de en instelling Hallo gebruikers-id als een eigenschap verzenden.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="dc2d2-173">tooanalyze paginaweergaven vervangen Hallo standaard JavaScript trackPageView-aanroep.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="dc2d2-174">tooanalyze serverzijde telemetrie, een telemetrie telemetrie initialisatiefunctie tooadd Hallo gebruiker-id tooall server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="dc2d2-175">Vervolgens kunt u filteren en segment metrische gegevens en zoekopdrachten op Hallo gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="dc2d2-176">Verminderen het verkeer vanuit Mijn tooApplication app Insights</span><span class="sxs-lookup"><span data-stu-id="dc2d2-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="dc2d2-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), alle modules die u hoeft niet dergelijke Hallo prestaties teller collector uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="dc2d2-178">Gebruik [steekproeven en filteren](app-insights-api-filtering-sampling.md) op Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="dc2d2-179">In uw webpagina's Hallo aantal voor elke paginaweergave gemelde Ajax-aanroepen te beperken.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="dc2d2-180">In de script-codefragment Hallo na `instrumentationKey:...` , invoegen: `,maxAjaxCallsPerView:3` (of een geschikte getal).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="dc2d2-181">Als u [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), Hallo aggregatie van batches van metrische waarden voor het verzenden van Hallo resultaat berekenen.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="dc2d2-182">Er is een overload van TrackMetric() die voor die biedt.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="dc2d2-183">Meer informatie over [-prijzen en -quota](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="dc2d2-184">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="dc2d2-184">Disable telemetry</span></span>
<span data-ttu-id="dc2d2-185">te**dynamisch stoppen en starten** Hallo verzamelen en verzenden van telemetrie van Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="dc2d2-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="dc2d2-186">te**uitschakelen geselecteerde standaard collectors** - prestatiemeteritems, bijvoorbeeld, HTTP-aanvragen of afhankelijkheden - verwijderen of Hallo relevante regels in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). U kan doen, bijvoorbeeld, als u uw eigen gegevens TrackRequest toosend wilt.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="dc2d2-187">Systeemprestatiemeteritems weergeven</span><span class="sxs-lookup"><span data-stu-id="dc2d2-187">View system performance counters</span></span>
<span data-ttu-id="dc2d2-188">Tussen Hallo zijn metrische gegevens die u in metrics explorer weergeven kunt een reeks systeemprestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="dc2d2-189">Er is een vooraf gedefinieerde blade met de titel **Servers** waarin meerdere wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Open uw Application Insights-resource en klik op Servers](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="dc2d2-191">Als er geen gegevens van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="dc2d2-191">If you see no performance counter data</span></span>
* <span data-ttu-id="dc2d2-192">**IIS-server** op uw computer of op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="dc2d2-193">[Statusmonitor installeren](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="dc2d2-194">**Azure-website** -prestatiemeteritems nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="dc2d2-195">Er zijn verschillende metrische gegevens die u als standaardonderdeel van hello Azure-website in het Configuratiescherm krijgt.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="dc2d2-196">**UNIX-server** - [Installeer collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="dc2d2-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="dc2d2-197">toodisplay meer prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="dc2d2-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="dc2d2-198">Eerst [toevoegen van een nieuwe grafiek](app-insights-metrics-explorer.md) en zien als Hallo teller in Hallo basic ingesteld wij bieden.</span><span class="sxs-lookup"><span data-stu-id="dc2d2-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="dc2d2-199">Als dat niet het geval is, [hello toohello itemset verzameld door de module Hallo prestatiemeteritems toevoegen](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d2-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
