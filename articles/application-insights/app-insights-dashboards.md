---
title: aaaDashboards en navigatie in hello Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="a4b37-103">Navigatie en Dashboards in Hallo Application Insights-portal</span><span class="sxs-lookup"><span data-stu-id="a4b37-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="a4b37-104">Nadat u hebt [Application Insights instellen op uw project](app-insights-overview.md), telemetriegegevens over de prestaties en het gebruik van uw app wordt weergegeven in uw project Application Insights-resource in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4b37-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="a4b37-105">Uw telemetrie vinden</span><span class="sxs-lookup"><span data-stu-id="a4b37-105">Find your telemetry</span></span>
<span data-ttu-id="a4b37-106">Meld u aan toohello [Azure-portal](https://portal.azure.com) en navigeer toohello Application Insights-resource die u hebt gemaakt voor uw app.</span><span class="sxs-lookup"><span data-stu-id="a4b37-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Klik op Bladeren en selecteer Application Insights en vervolgens uw app.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="a4b37-108">Hallo overzichtsblade (pagina) voor uw app bevat een overzicht van Hallo belangrijkste diagnostische metrische gegevens van uw app en is een gateway toohello andere functies van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="a4b37-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Primaire routes tooview uw telemetrie](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="a4b37-110">U kunt een van de Hallo grafieken en rasters aanpassen en tooa dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="a4b37-111">Op die manier u kunt samenbrengen Hallo sleutel telemetrie van andere apps op een centrale dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="a4b37-112">Dashboards</span><span class="sxs-lookup"><span data-stu-id="a4b37-112">Dashboards</span></span>
<span data-ttu-id="a4b37-113">Hallo eerst te beginnen u ziet nadat u zich aanmeldt toohello [Microsoft Azure-portal](https://portal.azure.com) wordt een dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="a4b37-114">Hier kunt u overbrengen samen Hallo grafieken die belangrijkste tooyou binnen alle Azure-resources zijn, met inbegrip van telemetrie van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Een aangepaste dashboard.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="a4b37-116">**Navigeer toospecific resources** zoals uw app in Application Insights: gebruik Hallo linkerbalk.</span><span class="sxs-lookup"><span data-stu-id="a4b37-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="a4b37-117">**Huidige dashboard Return toohello**, of schakel over recente weergaven tooother: gebruik Hallo vervolgkeuzelijst bovenaan links.</span><span class="sxs-lookup"><span data-stu-id="a4b37-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="a4b37-118">**Overschakelen van dashboards**: gebruik Hallo vervolgkeuzemenu op Hallo dashboard titel</span><span class="sxs-lookup"><span data-stu-id="a4b37-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="a4b37-119">**Maken, bewerken en dashboards delen** op Hallo dashboard werkbalk.</span><span class="sxs-lookup"><span data-stu-id="a4b37-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="a4b37-120">**Hallo dashboard bewerken**: Beweeg de muisaanwijzer over een tegel en gebruik vervolgens de bovenste balk toomove, aanpassen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="a4b37-121">Tooa dashboard toevoegen</span><span class="sxs-lookup"><span data-stu-id="a4b37-121">Add tooa dashboard</span></span>
<span data-ttu-id="a4b37-122">Wanneer u een blade of een set van grafieken die interessants kijkt, kunt u een kopie van het toohello dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="a4b37-123">U ziet het volgende keer dat u terugkeert.</span><span class="sxs-lookup"><span data-stu-id="a4b37-123">You'll see it next time you return there.</span></span>

![een grafiek toopin Beweeg de muisaanwijzer over het en klik op '...' in de header Hallo.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="a4b37-125">Grafiek toodashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-125">Pin chart toodashboard.</span></span> <span data-ttu-id="a4b37-126">Er verschijnt een kopie van de grafiek Hallo op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="a4b37-127">Pincode Hallo hele blade toohello dashboard - blijkt op Hallo dashboard als tegel die u kunt doorklikken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="a4b37-128">Klik op Hallo linkerbovenhoek tooreturn toohello huidige dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="a4b37-129">Vervolgens kunt u Hallo vervolgkeuzelijst tooreturn toohello huidige weergave.</span><span class="sxs-lookup"><span data-stu-id="a4b37-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="a4b37-130">U ziet dat de grafieken worden gegroepeerd in tegels: een tegel kan meer dan één grafiek bevatten.</span><span class="sxs-lookup"><span data-stu-id="a4b37-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="a4b37-131">U vastmaken Hallo hele tegel toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="a4b37-132">Hallo grafiek wordt automatisch vernieuwd met een frequentie die afhankelijk is van de grafiek Hallo tijdsbereik:</span><span class="sxs-lookup"><span data-stu-id="a4b37-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="a4b37-133">Tijdsbereik up too1 uur: vernieuwen om de 5 minuten</span><span class="sxs-lookup"><span data-stu-id="a4b37-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="a4b37-134">Bereik 1-24 uur tijd: vernieuwen om de 15 minuten</span><span class="sxs-lookup"><span data-stu-id="a4b37-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="a4b37-135">Tijdsbereik hierboven 24 uur: (tijdsbereik) / 60.</span><span class="sxs-lookup"><span data-stu-id="a4b37-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="a4b37-136">Een query in Analytics vastmaken</span><span class="sxs-lookup"><span data-stu-id="a4b37-136">Pin any query in Analytics</span></span>
<span data-ttu-id="a4b37-137">U kunt ook [Analytics vastmaken](app-insights-analytics-using.md#pin-to-dashboard) grafieken tooa [gedeelde](#share-dashboards-with-your-team) dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b37-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="a4b37-138">Hiermee kunt u tooadd grafieken van elke willekeurige query naast Hallo standaard metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a4b37-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="a4b37-139">Resultaten automatisch opnieuw elk uur berekend.</span><span class="sxs-lookup"><span data-stu-id="a4b37-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="a4b37-140">Pictogram Hallo op Hallo grafiek toorecalculate onmiddellijk klikt u op.</span><span class="sxs-lookup"><span data-stu-id="a4b37-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="a4b37-141">(Browser vernieuwen wordt niet opnieuw worden berekend.)</span><span class="sxs-lookup"><span data-stu-id="a4b37-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="a4b37-142">Een tegel op Hallo dashboard aanpassen</span><span class="sxs-lookup"><span data-stu-id="a4b37-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="a4b37-143">Zodra een tegel op Hallo dashboard, kunt u het kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Beweeg de muisaanwijzer over een grafiek in volgorde tooedit deze.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="a4b37-145">Een grafiek toohello tegel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="a4b37-146">Hallo metriek, groeperen op dimensie en stijl (tabel, grafiek) van een grafiek instellen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="a4b37-147">Sleep over Hallo diagram toozoom Klik op Hallo ongedaan maken knop tooreset Hallo timespan; filtereigenschappen instellen voor Hallo grafieken op Hallo tegel.</span><span class="sxs-lookup"><span data-stu-id="a4b37-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="a4b37-148">Titel van de tegel instellen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-148">Set tile title.</span></span>

<span data-ttu-id="a4b37-149">Tegels die zijn vastgemaakt vanuit metrische explorer blades hebben opties voor het bewerken van meer dan tegels die zijn vastgemaakt vanuit een overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="a4b37-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="a4b37-150">Hallo oorspronkelijke tegel die u hebt vastgemaakt wordt niet beïnvloed door uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="a4b37-151">Schakelen tussen dashboards</span><span class="sxs-lookup"><span data-stu-id="a4b37-151">Switch between dashboards</span></span>
<span data-ttu-id="a4b37-152">U kunt meer dan één dashboard opslaan en tussen deze twee schakelt.</span><span class="sxs-lookup"><span data-stu-id="a4b37-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="a4b37-153">Wanneer u een grafiek of blade vastmaken, zijn ze toohello huidige dashboard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a4b37-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch tussen dashboards, klik op Dashboard en selecteer een opgeslagen dashboard.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="a4b37-157">U wellicht bijvoorbeeld één dashboard voor het weergeven van volledig scherm in Hallo team ruimte en een voor algemene ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="a4b37-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="a4b37-158">Op Hallo dashboard, een blade wordt weergegeven als een tegel: klik op de toogo toohello blade.</span><span class="sxs-lookup"><span data-stu-id="a4b37-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="a4b37-159">Een grafiek repliceert Hallo grafiek in de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="a4b37-159">A chart replicates hello chart in its original location.</span></span>

![Klik op een tegel tooopen Hallo blade vertegenwoordigt](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="a4b37-161">Dashboards delen</span><span class="sxs-lookup"><span data-stu-id="a4b37-161">Share dashboards</span></span>
<span data-ttu-id="a4b37-162">Wanneer u een dashboard hebt gemaakt, kunt u het delen met andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a4b37-162">When you've created a dashboard, you can share it with other users.</span></span>

![In de header Hallo dashboard, klikt u op delen](./media/app-insights-dashboards/41.png)

<span data-ttu-id="a4b37-164">Meer informatie over [functies en toegangsbeheer](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="a4b37-165">App-navigatie</span><span class="sxs-lookup"><span data-stu-id="a4b37-165">App navigation</span></span>
<span data-ttu-id="a4b37-166">overzichtsblade Hello is Hallo gateway toomore informatie over uw app.</span><span class="sxs-lookup"><span data-stu-id="a4b37-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="a4b37-167">**Een grafiek of tegel** : klik op een tegel of grafiek toosee meer informatie over wat Hiermee wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a4b37-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="a4b37-168">Overzicht blade knoppen</span><span class="sxs-lookup"><span data-stu-id="a4b37-168">Overview blade buttons</span></span>
![Overzicht blade bovenste navigatiebalk](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="a4b37-170">[**Metrics Explorer** ](app-insights-metrics-explorer.md) -grafieken van de prestaties en gebruik te maken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="a4b37-171">[**Search** ](app-insights-diagnostic-search.md) - specifieke exemplaren van gebeurtenissen, zoals aanvragen, uitzonderingen, te onderzoeken of meld u traceringen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="a4b37-172">[**Analytics** ](app-insights-analytics.md) -krachtige query's over uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="a4b37-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="a4b37-173">**Tijdsbereik** -Hallo bereik weergegeven door alle Hallo grafieken op Hallo blade aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="a4b37-174">**Verwijder** -Hallo Application Insights-resource voor deze app te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="a4b37-175">U moet ook Verwijder Hallo Application Insights-pakketten van uw app-code of Hallo bewerken [instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) in uw app toodirect telemetrie tooa verschillende Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="a4b37-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="a4b37-176">Tabblad met essentiële gegevens</span><span class="sxs-lookup"><span data-stu-id="a4b37-176">Essentials tab</span></span>
* <span data-ttu-id="a4b37-177">[Instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) -deze app resource identificeert.</span><span class="sxs-lookup"><span data-stu-id="a4b37-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="a4b37-178">Prijzen - functies beschikbaar is en stel volume caps maken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="a4b37-179">App-navigatiebalk</span><span class="sxs-lookup"><span data-stu-id="a4b37-179">App navigation bar</span></span>
![Linkernavigatiebalk](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="a4b37-181">**Overzicht** -Return toohello app overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="a4b37-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="a4b37-182">**Activiteitenlogboek** -waarschuwingen en Azure Beheergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="a4b37-183">[**Toegangsbeheer** ](app-insights-resources-roles-access-control.md) -toegang tooteam leden en andere bieden.</span><span class="sxs-lookup"><span data-stu-id="a4b37-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="a4b37-184">[**Labels** ](../azure-resource-manager/resource-group-using-tags.md) -gebruik tags toogroup uw app met anderen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="a4b37-185">ONDERZOEKEN</span><span class="sxs-lookup"><span data-stu-id="a4b37-185">INVESTIGATE</span></span>

* <span data-ttu-id="a4b37-186">[**De toepassingstoewijzing** ](app-insights-app-map.md) -actieve toewijzing Hallo-onderdelen van uw toepassing wordt weergegeven die zijn afgeleid van Hallo afhankelijkheidsinformatie.</span><span class="sxs-lookup"><span data-stu-id="a4b37-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="a4b37-187">[**Detectie van smartcard** ](app-insights-proactive-diagnostics.md) -recente prestatiewaarschuwingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="a4b37-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="a4b37-188">[**Livestream** ](app-insights-live-stream.md) : een vaste set nuttig bij het implementeren van een nieuwe build handomdraai maatstaven of foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a4b37-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="a4b37-189">[**Beschikbaarheid / Webtests** ](app-insights-monitor-web-app-availability.md) -verzenden reguliere aanvragen tooyour web-app uit rond hallo world.*</span><span class="sxs-lookup"><span data-stu-id="a4b37-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="a4b37-190">[**Fouten, prestaties** ](app-insights-web-monitor-performance.md) -uitzonderingen, uitvalpercentage en de reactie time-out voor aanvragen tooyour app en voor aanvragen van uw app te[afhankelijkheden](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="a4b37-191">[**Prestaties** ](app-insights-web-monitor-performance.md) -reactietijd, reactietijden afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="a4b37-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="a4b37-192">[Servers](app-insights-web-monitor-performance.md) -prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="a4b37-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="a4b37-193">Beschikbaar als u [Status Monitor installeren](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="a4b37-194">**Browser** -pagina-weergave en AJAX-prestaties.</span><span class="sxs-lookup"><span data-stu-id="a4b37-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="a4b37-195">Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="a4b37-196">**Gebruik** -weergave, gebruiker en sessie aantallen pagina.</span><span class="sxs-lookup"><span data-stu-id="a4b37-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="a4b37-197">Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="a4b37-198">CONFIGUREREN</span><span class="sxs-lookup"><span data-stu-id="a4b37-198">CONFIGURE</span></span>

* <span data-ttu-id="a4b37-199">**Aan de slag** -inline-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4b37-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="a4b37-200">**Eigenschappen** -instrumentatiesleutel, abonnement en de resource-id.</span><span class="sxs-lookup"><span data-stu-id="a4b37-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="a4b37-201">[Waarschuwingen](app-insights-alerts.md) -metrische configuratie van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="a4b37-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="a4b37-202">[Continue export](app-insights-export-telemetry.md) -exporteren van telemetrie tooAzure opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="a4b37-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="a4b37-203">[Prestaties testen](app-insights-monitor-web-app-availability.md#performance-tests) -een synthetische werklast op uw website instellen.</span><span class="sxs-lookup"><span data-stu-id="a4b37-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="a4b37-204">[Quotum en prijzen](app-insights-pricing.md) en [opname steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="a4b37-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="a4b37-205">**API-toegang** -maken [release aantekeningen](app-insights-annotations.md) en voor Hallo Data Access-API.</span><span class="sxs-lookup"><span data-stu-id="a4b37-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="a4b37-206">[**Werkitems** ](app-insights-diagnostic-search.md#create-work-item) -verbinding tooa werk traceringssysteem zodat u fouten tijdens de inspectie van telemetrie kunt maken.</span><span class="sxs-lookup"><span data-stu-id="a4b37-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="a4b37-207">INSTELLINGEN</span><span class="sxs-lookup"><span data-stu-id="a4b37-207">SETTINGS</span></span>

* <span data-ttu-id="a4b37-208">[**Hiermee vergrendelt u** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure-resources vergrendelen</span><span class="sxs-lookup"><span data-stu-id="a4b37-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="a4b37-209">[**Automatiseringsscript** ](app-insights-powershell.md) -een definitie van hello Azure-resource exporteren, zodat u deze als een sjabloon toocreate nieuwe resources gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a4b37-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="a4b37-210">Video</span><span class="sxs-lookup"><span data-stu-id="a4b37-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="a4b37-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4b37-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="a4b37-212">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="a4b37-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="a4b37-213">Metrische gegevens filteren en segment</span><span class="sxs-lookup"><span data-stu-id="a4b37-213">Filter and segment metrics</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="a4b37-215">Diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="a4b37-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="a4b37-216">Zoeken en gebeurtenissen, gerelateerde gebeurtenissen controleren en maken van fouten</span><span class="sxs-lookup"><span data-stu-id="a4b37-216">Find and inspect events, related events, and create bugs</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="a4b37-218">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="a4b37-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="a4b37-219">Krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="a4b37-219">Powerful query language</span></span> |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/63.png) |
