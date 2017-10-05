---
title: Dashboards en navigatie in de Azure Application Insights | Microsoft Docs
description: Weergaven maken van uw belangrijkste APM-grafieken en query's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="15399-103">Navigatie en Dashboards in de Application Insights-portal</span><span class="sxs-lookup"><span data-stu-id="15399-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="15399-104">Nadat u hebt [Application Insights instellen op uw project](app-insights-overview.md), telemetriegegevens over de prestaties en het gebruik van uw app wordt weergegeven in Application Insights-resource voor uw project in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15399-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="15399-105">Uw telemetrie vinden</span><span class="sxs-lookup"><span data-stu-id="15399-105">Find your telemetry</span></span>
<span data-ttu-id="15399-106">Aanmelden bij de [Azure-portal](https://portal.azure.com) en navigeer naar de Application Insights-resource die u hebt gemaakt voor uw app.</span><span class="sxs-lookup"><span data-stu-id="15399-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Klik op Bladeren en selecteer Application Insights en vervolgens uw app.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="15399-108">Overzichtsblade (pagina) voor uw app bevat een overzicht van de belangrijkste metrische diagnostische gegevens van uw app en is een gateway naar de andere functies van de portal.</span><span class="sxs-lookup"><span data-stu-id="15399-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Belangrijke routes naar uw telemetrie weergeven](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="15399-110">U kunt een van de grafieken en rasters aanpassen en aan een dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="15399-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="15399-111">Op die manier u kunt overbrengen samen de belangrijkste telemetrie van andere apps op een centrale dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="15399-112">Dashboards</span><span class="sxs-lookup"><span data-stu-id="15399-112">Dashboards</span></span>
<span data-ttu-id="15399-113">Het eerste wat u ziet nadat u zich aanmeldt bij de [Microsoft Azure-portal](https://portal.azure.com) wordt een dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="15399-114">Hier kunt u overbrengen samen de diagrammen die zeer belangrijk voor u over alle Azure-resources zijn, met inbegrip van telemetrie van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15399-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Een aangepaste dashboard.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="15399-116">**Navigeer naar de specifieke resources** zoals uw app in Application Insights: de linkerbalk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="15399-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="15399-117">**Keer terug naar de huidige dashboard**, of schakel over naar andere recente weergaven: Gebruik de vervolgkeuzelijst linksboven.</span><span class="sxs-lookup"><span data-stu-id="15399-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="15399-118">**Overschakelen van dashboards**: Gebruik de vervolgkeuzelijst op de titel van het dashboard</span><span class="sxs-lookup"><span data-stu-id="15399-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="15399-119">**Maken, bewerken en dashboards delen** op de werkbalk van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="15399-120">**Het dashboard bewerken**: Beweeg de muisaanwijzer over een tegel en vervolgens met de bovenste balk verplaatsen, aanpassen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="15399-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="15399-121">Toevoegen aan een dashboard</span><span class="sxs-lookup"><span data-stu-id="15399-121">Add to a dashboard</span></span>
<span data-ttu-id="15399-122">Wanneer u een blade of een set van grafieken die interessants kijkt, kunt u een kopie van het naar het dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="15399-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="15399-123">U ziet het volgende keer dat u terugkeert.</span><span class="sxs-lookup"><span data-stu-id="15399-123">You'll see it next time you return there.</span></span>

![Beweeg de muisaanwijzer over het om een grafiek, en klik op '...' in de header.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="15399-125">Grafiek vastmaken aan dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-125">Pin chart to dashboard.</span></span> <span data-ttu-id="15399-126">Een kopie van de grafiek wordt weergegeven op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="15399-127">De hele blade naar het dashboard vastmaken - deze wordt weergegeven op het dashboard als tegel die u kunt doorklikken.</span><span class="sxs-lookup"><span data-stu-id="15399-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="15399-128">Klik op de linkerbovenhoek om terug te keren naar het huidige dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="15399-129">Vervolgens kunt u de vervolgkeuzelijst om terug te keren naar de huidige weergave.</span><span class="sxs-lookup"><span data-stu-id="15399-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="15399-130">U ziet dat de grafieken worden gegroepeerd in tegels: een tegel kan meer dan één grafiek bevatten.</span><span class="sxs-lookup"><span data-stu-id="15399-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="15399-131">U vastmaken de hele tegel aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="15399-132">De grafiek worden automatisch vernieuwd met een frequentie die afhankelijk zijn van de grafiek tijdsbereik:</span><span class="sxs-lookup"><span data-stu-id="15399-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="15399-133">Tijd tot een uur liggen: vernieuwen om de 5 minuten</span><span class="sxs-lookup"><span data-stu-id="15399-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="15399-134">Bereik 1-24 uur tijd: vernieuwen om de 15 minuten</span><span class="sxs-lookup"><span data-stu-id="15399-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="15399-135">Tijdsbereik hierboven 24 uur: (tijdsbereik) / 60.</span><span class="sxs-lookup"><span data-stu-id="15399-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="15399-136">Een query in Analytics vastmaken</span><span class="sxs-lookup"><span data-stu-id="15399-136">Pin any query in Analytics</span></span>
<span data-ttu-id="15399-137">U kunt ook [Analytics vastmaken](app-insights-analytics-using.md#pin-to-dashboard) grafieken naar een [gedeelde](#share-dashboards-with-your-team) dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="15399-138">Hiermee kunt u diagrammen van elke willekeurige query naast de standaard metrische gegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15399-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="15399-139">Resultaten automatisch opnieuw elk uur berekend.</span><span class="sxs-lookup"><span data-stu-id="15399-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="15399-140">Klik op het pictogram Vernieuwen op de grafiek worden onmiddellijk berekend.</span><span class="sxs-lookup"><span data-stu-id="15399-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="15399-141">(Browser vernieuwen wordt niet opnieuw worden berekend.)</span><span class="sxs-lookup"><span data-stu-id="15399-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="15399-142">Een tegel op het dashboard aanpassen</span><span class="sxs-lookup"><span data-stu-id="15399-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="15399-143">Zodra een tegel op het dashboard, kunt u het kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="15399-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Beweeg de muisaanwijzer over een grafiek om deze te bewerken.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="15399-145">Een grafiek toevoegen aan de tegel.</span><span class="sxs-lookup"><span data-stu-id="15399-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="15399-146">Stel de metriek, groeperen op dimensie en stijl (tabel, grafiek) van een grafiek.</span><span class="sxs-lookup"><span data-stu-id="15399-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="15399-147">Sleep over het diagram om in te zoomen; Klik op de knop ongedaan maken om in te stellen de timespan; Filtereigenschappen voor de grafieken worden ingesteld op de tegel.</span><span class="sxs-lookup"><span data-stu-id="15399-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="15399-148">Titel van de tegel instellen.</span><span class="sxs-lookup"><span data-stu-id="15399-148">Set tile title.</span></span>

<span data-ttu-id="15399-149">Tegels die zijn vastgemaakt vanuit metrische explorer blades hebben opties voor het bewerken van meer dan tegels die zijn vastgemaakt vanuit een overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="15399-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="15399-150">De oorspronkelijke tegel die u hebt vastgemaakt wordt niet beïnvloed door uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="15399-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="15399-151">Schakelen tussen dashboards</span><span class="sxs-lookup"><span data-stu-id="15399-151">Switch between dashboards</span></span>
<span data-ttu-id="15399-152">U kunt meer dan één dashboard opslaan en tussen deze twee schakelt.</span><span class="sxs-lookup"><span data-stu-id="15399-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="15399-153">Wanneer u een grafiek of blade vastmaken, zijn ze toegevoegd aan het huidige dashboard.</span><span class="sxs-lookup"><span data-stu-id="15399-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Schakelen tussen dashboards, klik op Dashboard en een opgeslagen dashboard selecteren.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="15399-157">U wellicht bijvoorbeeld één dashboard voor het volledige scherm wordt weergegeven in de ruimte van het team en een voor algemene ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="15399-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="15399-158">Op het dashboard, een blade wordt weergegeven als een tegel: Klik hierop om naar de blade te gaan.</span><span class="sxs-lookup"><span data-stu-id="15399-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="15399-159">Een grafiek repliceert de grafiek in de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="15399-159">A chart replicates the chart in its original location.</span></span>

![Klik op een tegel om de blade vertegenwoordigt te openen](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="15399-161">Dashboards delen</span><span class="sxs-lookup"><span data-stu-id="15399-161">Share dashboards</span></span>
<span data-ttu-id="15399-162">Wanneer u een dashboard hebt gemaakt, kunt u het delen met andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="15399-162">When you've created a dashboard, you can share it with other users.</span></span>

![Klik in de header dashboard delen](./media/app-insights-dashboards/41.png)

<span data-ttu-id="15399-164">Meer informatie over [functies en toegangsbeheer](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="15399-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="15399-165">App-navigatie</span><span class="sxs-lookup"><span data-stu-id="15399-165">App navigation</span></span>
<span data-ttu-id="15399-166">De overzichtsblade is de gateway naar meer informatie over uw app.</span><span class="sxs-lookup"><span data-stu-id="15399-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="15399-167">**Een grafiek of tegel** : klik op een tegel of grafiek voor meer details over wat Hiermee wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="15399-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="15399-168">Overzicht blade knoppen</span><span class="sxs-lookup"><span data-stu-id="15399-168">Overview blade buttons</span></span>
![Overzicht blade bovenste navigatiebalk](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="15399-170">[**Metrics Explorer** ](app-insights-metrics-explorer.md) -grafieken van de prestaties en gebruik te maken.</span><span class="sxs-lookup"><span data-stu-id="15399-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="15399-171">[**Search** ](app-insights-diagnostic-search.md) - specifieke exemplaren van gebeurtenissen, zoals aanvragen, uitzonderingen, te onderzoeken of meld u traceringen.</span><span class="sxs-lookup"><span data-stu-id="15399-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="15399-172">[**Analytics** ](app-insights-analytics.md) -krachtige query's over uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="15399-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="15399-173">**Tijdsbereik** -het bereik dat wordt weergegeven in de grafieken op de blade aanpassen.</span><span class="sxs-lookup"><span data-stu-id="15399-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="15399-174">**Verwijder** -verwijderen van de Application Insights-resource voor deze app.</span><span class="sxs-lookup"><span data-stu-id="15399-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="15399-175">U moet ook Verwijder de Application Insights-pakketten van uw app-code of bewerk de [instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) in uw app telemetrie aan een andere Application Insights-resource wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="15399-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="15399-176">Tabblad met essentiële gegevens</span><span class="sxs-lookup"><span data-stu-id="15399-176">Essentials tab</span></span>
* <span data-ttu-id="15399-177">[Instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) -deze app resource identificeert.</span><span class="sxs-lookup"><span data-stu-id="15399-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="15399-178">Prijzen - functies beschikbaar is en stel volume caps maken.</span><span class="sxs-lookup"><span data-stu-id="15399-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="15399-179">App-navigatiebalk</span><span class="sxs-lookup"><span data-stu-id="15399-179">App navigation bar</span></span>
![Linkernavigatiebalk](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="15399-181">**Overzicht** -terug naar de blade app overzicht.</span><span class="sxs-lookup"><span data-stu-id="15399-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="15399-182">**Activiteitenlogboek** -waarschuwingen en Azure Beheergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="15399-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="15399-183">[**Toegangsbeheer** ](app-insights-resources-roles-access-control.md) -toegang geven tot teamleden en anderen.</span><span class="sxs-lookup"><span data-stu-id="15399-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="15399-184">[**Labels** ](../azure-resource-manager/resource-group-using-tags.md) -codes gebruiken om de groep van uw app met anderen.</span><span class="sxs-lookup"><span data-stu-id="15399-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="15399-185">ONDERZOEKEN</span><span class="sxs-lookup"><span data-stu-id="15399-185">INVESTIGATE</span></span>

* <span data-ttu-id="15399-186">[**De toepassingstoewijzing** ](app-insights-app-map.md) -Active kaart en geeft de onderdelen van uw toepassing die is afgeleid van afhankelijkheidsinformatie.</span><span class="sxs-lookup"><span data-stu-id="15399-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="15399-187">[**Detectie van smartcard** ](app-insights-proactive-diagnostics.md) -recente prestatiewaarschuwingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="15399-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="15399-188">[**Livestream** ](app-insights-live-stream.md) : een vaste set nuttig bij het implementeren van een nieuwe build handomdraai maatstaven of foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="15399-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="15399-189">[**Beschikbaarheid / Webtests** ](app-insights-monitor-web-app-availability.md) -reguliere aanvragen verzenden naar uw web-app rond de world.*</span><span class="sxs-lookup"><span data-stu-id="15399-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="15399-190">[**Fouten, prestaties** ](app-insights-web-monitor-performance.md) -uitzonderingen, uitvalpercentage en responstijden voor aanvragen voor uw app en voor het aanvragen van uw app [afhankelijkheden](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="15399-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="15399-191">[**Prestaties** ](app-insights-web-monitor-performance.md) -reactietijd, reactietijden afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="15399-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="15399-192">[Servers](app-insights-web-monitor-performance.md) -prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="15399-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="15399-193">Beschikbaar als u [Status Monitor installeren](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="15399-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="15399-194">**Browser** -pagina-weergave en AJAX-prestaties.</span><span class="sxs-lookup"><span data-stu-id="15399-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="15399-195">Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="15399-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="15399-196">**Gebruik** -weergave, gebruiker en sessie aantallen pagina.</span><span class="sxs-lookup"><span data-stu-id="15399-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="15399-197">Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="15399-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="15399-198">CONFIGUREREN</span><span class="sxs-lookup"><span data-stu-id="15399-198">CONFIGURE</span></span>

* <span data-ttu-id="15399-199">**Aan de slag** -inline-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="15399-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="15399-200">**Eigenschappen** -instrumentatiesleutel, abonnement en de resource-id.</span><span class="sxs-lookup"><span data-stu-id="15399-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="15399-201">[Waarschuwingen](app-insights-alerts.md) -metrische configuratie van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="15399-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="15399-202">[Continue export](app-insights-export-telemetry.md) -exporteren van telemetrie naar Azure-opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="15399-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="15399-203">[Prestaties testen](app-insights-monitor-web-app-availability.md#performance-tests) -een synthetische werklast op uw website instellen.</span><span class="sxs-lookup"><span data-stu-id="15399-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="15399-204">[Quotum en prijzen](app-insights-pricing.md) en [opname steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="15399-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="15399-205">**API-toegang** -maken [release aantekeningen](app-insights-annotations.md) en voor de Data Access-API.</span><span class="sxs-lookup"><span data-stu-id="15399-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="15399-206">[**Werkitems** ](app-insights-diagnostic-search.md#create-work-item) -verbinding maken met een werk traceringssysteem zodat u fouten tijdens de inspectie van telemetrie kunt maken.</span><span class="sxs-lookup"><span data-stu-id="15399-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="15399-207">INSTELLINGEN</span><span class="sxs-lookup"><span data-stu-id="15399-207">SETTINGS</span></span>

* <span data-ttu-id="15399-208">[**Hiermee vergrendelt u** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure-resources vergrendelen</span><span class="sxs-lookup"><span data-stu-id="15399-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="15399-209">[**Automatiseringsscript** ](app-insights-powershell.md) -exporteren van een definitie van de Azure-resource, zodat u deze als sjabloon gebruiken kunt voor het maken van nieuwe resources.</span><span class="sxs-lookup"><span data-stu-id="15399-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="15399-210">Video</span><span class="sxs-lookup"><span data-stu-id="15399-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="15399-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15399-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="15399-212">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="15399-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="15399-213">Metrische gegevens filteren en segment</span><span class="sxs-lookup"><span data-stu-id="15399-213">Filter and segment metrics</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="15399-215">Diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="15399-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="15399-216">Zoeken en gebeurtenissen, gerelateerde gebeurtenissen controleren en maken van fouten</span><span class="sxs-lookup"><span data-stu-id="15399-216">Find and inspect events, related events, and create bugs</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="15399-218">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="15399-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="15399-219">Krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="15399-219">Powerful query language</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/63.png) |
