---
title: Hoe kan ik... in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="be931-103">Hoe kan ik ... in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="be931-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="be931-104">Ontvang een e-mail wanneer...</span><span class="sxs-lookup"><span data-stu-id="be931-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="be931-105">E-mailadres als Mijn site uitvalt</span><span class="sxs-lookup"><span data-stu-id="be931-105">Email if my site goes down</span></span>
<span data-ttu-id="be931-106">Stel een [beschikbaarheid WebTest](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="be931-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="be931-107">E-als Mijn site is overbelast</span><span class="sxs-lookup"><span data-stu-id="be931-107">Email if my site is overloaded</span></span>
<span data-ttu-id="be931-108">Stel een [waarschuwing](app-insights-alerts.md) op **serverreactietijd**.</span><span class="sxs-lookup"><span data-stu-id="be931-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="be931-109">Een drempelwaarde tussen 1 en 2 seconden zouden moeten werken.</span><span class="sxs-lookup"><span data-stu-id="be931-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="be931-110">Uw app mogelijk tekenen van stam ook weergeven door te retourneren van de fout-codes.</span><span class="sxs-lookup"><span data-stu-id="be931-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="be931-111">Een waarschuwing instellen voor **mislukte aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="be931-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="be931-112">Als u een waarschuwing instellen wilt voor **serveruitzonderingen**, u moet doen [enkele aanvullende instellingen](app-insights-asp-net-exceptions.md) om te zien van gegevens.</span><span class="sxs-lookup"><span data-stu-id="be931-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="be931-113">E-uitzonderingen op</span><span class="sxs-lookup"><span data-stu-id="be931-113">Email on exceptions</span></span>
1. [<span data-ttu-id="be931-114">Uitzonderingenmonitor instellen</span><span class="sxs-lookup"><span data-stu-id="be931-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="be931-115">[Een waarschuwing instellen](app-insights-alerts.md) tellen metrische gegevens voor de uitzondering.</span><span class="sxs-lookup"><span data-stu-id="be931-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="be931-116">E-mail bekijkt op een gebeurtenis in mijn app</span><span class="sxs-lookup"><span data-stu-id="be931-116">Email on an event in my app</span></span>
<span data-ttu-id="be931-117">Stel dat u wil een e-mailbericht ontvangen wanneer een bepaalde gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="be931-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="be931-118">Application Insights geen biedt deze mogelijkheid rechtstreeks, maar dit kan [een waarschuwing verzonden wanneer een metriek een drempelwaarde overschrijden](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="be931-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="be931-119">Waarschuwingen kunnen worden ingesteld voor [aangepaste metrische gegevens](app-insights-api-custom-events-metrics.md#trackmetric)echter geen aangepaste gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="be931-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="be931-120">Code schrijven om een metriek verhogen als de gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="be931-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="be931-121">Of:</span><span class="sxs-lookup"><span data-stu-id="be931-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="be931-122">Omdat waarschuwingen twee statussen hebben, hebt u een lage waarde verzenden wanneer u rekening houden met de waarschuwing is beëindigd:</span><span class="sxs-lookup"><span data-stu-id="be931-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="be931-123">Maken van een grafiek in [metrische explorer](app-insights-metrics-explorer.md) om te zien van uw alarm:</span><span class="sxs-lookup"><span data-stu-id="be931-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="be931-124">Stel nu een waarschuwing activeert wanneer de metriek hoger dan de waarde van een mid gedurende een korte periode is:</span><span class="sxs-lookup"><span data-stu-id="be931-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="be931-125">Het berekenen van gemiddelden periode instellen op het minimum.</span><span class="sxs-lookup"><span data-stu-id="be931-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="be931-126">U krijgt e-mailberichten wanneer de metriek boven gaat en onder de drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="be931-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="be931-127">Enkele punten in overweging moet nemen:</span><span class="sxs-lookup"><span data-stu-id="be931-127">Some points to consider:</span></span>

* <span data-ttu-id="be931-128">Een waarschuwing heeft twee statussen ('waarschuwing' en 'goede').</span><span class="sxs-lookup"><span data-stu-id="be931-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="be931-129">De status alleen geëvalueerd wanneer een metriek is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="be931-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="be931-130">Een e-mailbericht wordt alleen verzonden wanneer de status verandert.</span><span class="sxs-lookup"><span data-stu-id="be931-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="be931-131">Dit is waarom u verzenden hoge en lage waarde metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="be931-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="be931-132">Om de waarschuwing, wordt het gemiddelde genomen van de waarden ontvangen gedurende de afgelopen periode.</span><span class="sxs-lookup"><span data-stu-id="be931-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="be931-133">Dit gebeurt telkens wanneer een metriek is ontvangen, zodat e-mailberichten vaker dan de ingestelde periode kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="be931-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="be931-134">Omdat e-mailberichten worden verzonden op 'waarschuwing' en 'goede', is het raadzaam te overwegen opnieuw gegevensclassificatie uw eindresultaat gebeurtenis als een voorwaarde voor twee statussen.</span><span class="sxs-lookup"><span data-stu-id="be931-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="be931-135">Bijvoorbeeld, in plaats van een gebeurtenis 'taak voltooid' hebben een voorwaarde 'taak wordt uitgevoerd' waarop u e-mailberichten aan het begin en einde van een taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="be931-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="be931-136">Waarschuwingen automatisch instellen</span><span class="sxs-lookup"><span data-stu-id="be931-136">Set up alerts automatically</span></span>
[<span data-ttu-id="be931-137">PowerShell gebruiken voor het maken van nieuwe waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="be931-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="be931-138">PowerShell gebruiken om Application Insights beheren</span><span class="sxs-lookup"><span data-stu-id="be931-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="be931-139">Maken van nieuwe resources</span><span class="sxs-lookup"><span data-stu-id="be931-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="be931-140">Nieuwe waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="be931-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="be931-141">Afzonderlijke telemetrie van verschillende versies</span><span class="sxs-lookup"><span data-stu-id="be931-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="be931-142">Meerdere rollen in een app: gebruiken één Application Insights-resource en filtert u op cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="be931-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="be931-143">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="be931-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="be931-144">Scheiden van ontwikkeling, testen en release-versies: verschillende Application Insights-bronnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be931-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="be931-145">De instrumentatiesleutels uit web.config worden opgepikt. [Meer informatie](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="be931-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="be931-146">Reporting bouwen versies: een eigenschap met een initialisatiefunctie telemetrie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="be931-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="be931-147">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="be931-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="be931-148">Back-endservers en bureaublad-apps bewaken</span><span class="sxs-lookup"><span data-stu-id="be931-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="be931-149">[Gebruik de module Windows Server SDK](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="be931-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="be931-150">Gegevens visualiseren</span><span class="sxs-lookup"><span data-stu-id="be931-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="be931-151">Dashboard met metrische gegevens vanuit meerdere apps</span><span class="sxs-lookup"><span data-stu-id="be931-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="be931-152">In [metriek Explorer](app-insights-metrics-explorer.md), de grafiek aanpassen en als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="be931-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="be931-153">Vastmaken aan de Azure-dashboard.</span><span class="sxs-lookup"><span data-stu-id="be931-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="be931-154">Dashboard met gegevens uit andere bronnen en de Application Insights</span><span class="sxs-lookup"><span data-stu-id="be931-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="be931-155">[Exporteren van telemetrie naar Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="be931-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="be931-156">of</span><span class="sxs-lookup"><span data-stu-id="be931-156">Or</span></span>

* <span data-ttu-id="be931-157">SharePoint gebruiken als uw dashboard, het weergeven van gegevens in de SharePoint-webonderdelen.</span><span class="sxs-lookup"><span data-stu-id="be931-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="be931-158">[Continue export en Stream Analytics gebruiken om te exporteren naar SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="be931-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="be931-159">PowerView gebruiken om te controleren van de database en het maken van een SharePoint-webonderdeel voor PowerView.</span><span class="sxs-lookup"><span data-stu-id="be931-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="be931-160">Anonieme of geverifieerde gebruikers filteren</span><span class="sxs-lookup"><span data-stu-id="be931-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="be931-161">Als uw gebruikers zich aanmelden, kunt u instellen de [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users). (Dit gebeurt niet automatisch.)</span><span class="sxs-lookup"><span data-stu-id="be931-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="be931-162">U kunt vervolgens:</span><span class="sxs-lookup"><span data-stu-id="be931-162">You can then:</span></span>

* <span data-ttu-id="be931-163">Zoeken naar specifieke gebruikers-id 's</span><span class="sxs-lookup"><span data-stu-id="be931-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="be931-164">Metrische gegevens voor anonieme of geverifieerde gebruikers filteren</span><span class="sxs-lookup"><span data-stu-id="be931-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="be931-165">Wijzig de namen van eigenschappen of waarden</span><span class="sxs-lookup"><span data-stu-id="be931-165">Modify property names or values</span></span>
<span data-ttu-id="be931-166">Maak een [filter](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="be931-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="be931-167">Hiermee kunt u wijzigen of filteren van telemetrie voordat deze van uw app naar Application Insights wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="be931-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="be931-168">Lijst van specifieke gebruikers en hun gebruik</span><span class="sxs-lookup"><span data-stu-id="be931-168">List specific users and their usage</span></span>
<span data-ttu-id="be931-169">Als u alleen wilt [zoeken naar specifieke gebruikers](#search-specific-users), kunt u instellen de [geverifieerde gebruikers-id](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="be931-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="be931-170">Als u wilt dat een lijst met gebruikers met gegevens zoals welke pagina's ze bekijken of hoe vaak deze zich aanmeldt, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="be931-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="be931-171">[Set geverifieerde gebruiker-id](app-insights-api-custom-events-metrics.md#authenticated-users), [exporteren naar een database](app-insights-code-sample-export-sql-stream-analytics.md) en geschikt hulpprogramma's gebruiken om de gebruikergegevens er te analyseren.</span><span class="sxs-lookup"><span data-stu-id="be931-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="be931-172">Als u slechts een klein aantal gebruikers hebt, aangepaste gebeurtenissen of maatstaven voor gebruik van de gegevens van belang als de naam van de metrische waarde of gebeurtenis en het instellen van de gebruikers-id als een eigenschap verzenden.</span><span class="sxs-lookup"><span data-stu-id="be931-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="be931-173">Vervang de standaard JavaScript trackPageView-aanroep voor het analyseren van paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="be931-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="be931-174">Gebruik een initialisatiefunctie telemetrie de gebruikers-id toevoegen aan alle servertelemetrie voor het analyseren van serverzijde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="be931-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="be931-175">Vervolgens kunt u filteren en segment metrische gegevens en zoekopdrachten op de gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="be931-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="be931-176">Verminderen het verkeer van mijn app naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="be931-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="be931-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), alle modules die u niet nodig hebt, die de prestaties teller collector uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="be931-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="be931-178">Gebruik [steekproeven en filteren](app-insights-api-filtering-sampling.md) op de SDK.</span><span class="sxs-lookup"><span data-stu-id="be931-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="be931-179">In uw webpagina's, het aantal voor elke paginaweergave gemelde Ajax-aanroepen te beperken.</span><span class="sxs-lookup"><span data-stu-id="be931-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="be931-180">In het codefragment script na `instrumentationKey:...` , invoegen: `,maxAjaxCallsPerView:3` (of een geschikte getal).</span><span class="sxs-lookup"><span data-stu-id="be931-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="be931-181">Als u [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), de statistische functie van batches van metrische waarden voor het verzenden van het resultaat berekenen.</span><span class="sxs-lookup"><span data-stu-id="be931-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="be931-182">Er is een overload van TrackMetric() die voor die biedt.</span><span class="sxs-lookup"><span data-stu-id="be931-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="be931-183">Meer informatie over [-prijzen en -quota](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="be931-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="be931-184">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="be931-184">Disable telemetry</span></span>
<span data-ttu-id="be931-185">Naar **dynamisch stoppen en starten** het verzamelen en verzenden van telemetrie van de server:</span><span class="sxs-lookup"><span data-stu-id="be931-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="be931-186">Naar **uitschakelen geselecteerde standaard collectors** : bijvoorbeeld, prestatiemeteritems, HTTP-aanvragen of afhankelijkheden - verwijderen of de relevante regels in uitcommentariëren [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). U kan doen, bijvoorbeeld, als u wilt de gegevens van uw eigen TrackRequest verzenden.</span><span class="sxs-lookup"><span data-stu-id="be931-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="be931-187">Systeemprestatiemeteritems weergeven</span><span class="sxs-lookup"><span data-stu-id="be931-187">View system performance counters</span></span>
<span data-ttu-id="be931-188">Zijn een set van systeem prestatiemeteritems tussen de metrische gegevens die u in metrics explorer weergeven kunt.</span><span class="sxs-lookup"><span data-stu-id="be931-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="be931-189">Er is een vooraf gedefinieerde blade met de titel **Servers** waarin meerdere wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="be931-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Open uw Application Insights-resource en klik op Servers](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="be931-191">Als er geen gegevens van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="be931-191">If you see no performance counter data</span></span>
* <span data-ttu-id="be931-192">**IIS-server** op uw computer of op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="be931-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="be931-193">[Statusmonitor installeren](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="be931-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="be931-194">**Azure-website** -prestatiemeteritems nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="be931-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="be931-195">Er zijn verschillende metrische gegevens die u als standaardonderdeel van het Azure-website van het Configuratiescherm krijgt.</span><span class="sxs-lookup"><span data-stu-id="be931-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="be931-196">**UNIX-server** - [Installeer collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="be931-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="be931-197">Om meer prestatiemeteritems weer te geven</span><span class="sxs-lookup"><span data-stu-id="be931-197">To display more performance counters</span></span>
* <span data-ttu-id="be931-198">Eerst [toevoegen van een nieuwe grafiek](app-insights-metrics-explorer.md) en controleert u of het item in de basis die wij bieden.</span><span class="sxs-lookup"><span data-stu-id="be931-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="be931-199">Als dat niet het geval is, [de teller toevoegen aan de set die is verzameld door de prestatiemeteritemmodule](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="be931-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
