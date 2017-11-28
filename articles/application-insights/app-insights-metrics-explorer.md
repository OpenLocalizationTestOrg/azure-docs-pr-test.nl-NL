---
title: Verkennen van metrische gegevens in Azure Application Insights | Microsoft Docs
description: Grafieken op metrische explorer interpreteren en metrische explorer blades aanpassen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="a4d57-103">Verkennen van metrische gegevens in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a4d57-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="a4d57-104">Metrische gegevens in [Application Insights] [ start] zijn gemeten waarden en het aantal gebeurtenissen die worden verzonden in de telemetrie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4d57-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="a4d57-105">Ze helpen u bij het detecteren van prestatieproblemen en bekijk hoe trends in hoe uw toepassing wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4d57-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="a4d57-106">Er is een breed scala aan standard metrische gegevens en u kunt ook uw eigen aangepaste metrische gegevens en gebeurtenissen maken.</span><span class="sxs-lookup"><span data-stu-id="a4d57-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="a4d57-107">Aantal metrische gegevens en gebeurtenissen worden weergegeven in de grafieken van de geaggregeerde waarden zoals optellen, gemiddelden of aantallen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="a4d57-108">Hier volgt een voorbeeld reeks grafieken:</span><span class="sxs-lookup"><span data-stu-id="a4d57-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="a4d57-109">U vindt metrische gegevens grafieken overal in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="a4d57-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="a4d57-110">In de meeste gevallen kan worden aangepast en u kunt meer grafieken toevoegen aan de blade.</span><span class="sxs-lookup"><span data-stu-id="a4d57-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="a4d57-111">Op de blade overzicht doorklikken voor meer gedetailleerde grafieken (die titels zoals 'Servers') of klik op **Metrics Explorer** om een nieuwe blade waarin u aangepaste grafieken kunt maken te openen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="a4d57-112">Tijdsbereik</span><span class="sxs-lookup"><span data-stu-id="a4d57-112">Time range</span></span>
<span data-ttu-id="a4d57-113">U kunt het tijdbereik wordt gedekt door de grafieken of rasters op een blade wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Open de overzichtsblade van uw toepassing in de Azure portal](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="a4d57-115">Als u binnen enkele gegevens die nog niet zijn geregistreerd verwacht, klikt u op vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="a4d57-116">Grafieken vernieuwd met een interval, maar de intervallen zijn langer van grotere tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="a4d57-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="a4d57-117">Het kan even duren voordat gegevens afkomstig zijn via de pipeline voor analyse naar een diagram.</span><span class="sxs-lookup"><span data-stu-id="a4d57-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="a4d57-118">Als u wilt inzoomen deel uitmaakt van een grafiek, sleept u eroverheen:</span><span class="sxs-lookup"><span data-stu-id="a4d57-118">To zoom into part of a chart, drag over it:</span></span>

![Sleep over een deel van een diagram.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="a4d57-120">Klik op de knop Zoomen ongedaan maken om te herstellen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="a4d57-121">Samenvattingen en punt waarden</span><span class="sxs-lookup"><span data-stu-id="a4d57-121">Granularity and point values</span></span>
<span data-ttu-id="a4d57-122">Beweeg de muis over de grafiek om de waarden van de metrische gegevens op dat moment weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a4d57-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Beweeg de muisaanwijzer over een grafiek](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="a4d57-124">De waarde van de metrische gegevens op een bepaald tijdstip wordt tijdens de vorige steekproefinterval geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="a4d57-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="a4d57-125">De controle-interval of 'granulatie' wordt weergegeven boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="a4d57-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![De koptekst van een blade.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="a4d57-127">U kunt de granulatie in de blade van tijd bereik aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a4d57-127">You can adjust the granularity in the Time range blade:</span></span>

![De koptekst van een blade.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="a4d57-129">De beschikbare granulariteit, is afhankelijk van het tijdsbereik dat u selecteert.</span><span class="sxs-lookup"><span data-stu-id="a4d57-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="a4d57-130">De expliciete granulaties zijn alternatieven voor de 'automatisch' granulatie voor de periode.</span><span class="sxs-lookup"><span data-stu-id="a4d57-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="a4d57-131">Grafieken en rasters bewerken</span><span class="sxs-lookup"><span data-stu-id="a4d57-131">Editing charts and grids</span></span>
<span data-ttu-id="a4d57-132">Een nieuwe grafiek toevoegen aan de blade:</span><span class="sxs-lookup"><span data-stu-id="a4d57-132">To add a new chart to the blade:</span></span>

![Kies in Metrics Explorer grafiek toevoegen](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="a4d57-134">Selecteer **bewerken** in een bestaande of nieuwe grafiek bewerken wat er wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a4d57-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Selecteer een of meer waarden](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="a4d57-136">Hoewel er beperkingen van de combinaties die samen kunnen worden weergegeven, kunt u meer dan een waarde in een grafiek weergeven.</span><span class="sxs-lookup"><span data-stu-id="a4d57-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="a4d57-137">Als u een waarde kiest, zijn sommige van de andere uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a4d57-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="a4d57-138">Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app (aanroepen TrackMetric en TrackEvent) ze worden hier vermeld.</span><span class="sxs-lookup"><span data-stu-id="a4d57-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="a4d57-139">Segmenteren van uw gegevens</span><span class="sxs-lookup"><span data-stu-id="a4d57-139">Segment your data</span></span>
<span data-ttu-id="a4d57-140">U kunt bijvoorbeeld een metriek door eigenschap - splitsen als u wilt vergelijken paginaweergaven op clients met verschillende besturingssystemen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4d57-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="a4d57-141">Selecteer een grafiek of het raster, switch voor de groepering en kies een eigenschap moet worden gegroepeerd:</span><span class="sxs-lookup"><span data-stu-id="a4d57-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Selecteer groepering op set en selecteer vervolgens een eigenschap in Group By](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="a4d57-143">Wanneer u groepering gebruikt, geven de typen gebied en staafdiagram weergegeven in een gestapelde.</span><span class="sxs-lookup"><span data-stu-id="a4d57-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="a4d57-144">Dit is geschikt waarbij de aggregatiemethode Sum.</span><span class="sxs-lookup"><span data-stu-id="a4d57-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="a4d57-145">Maar wanneer het samenvoegingstype gemiddelde is, kiest u de regel of het raster weergave typen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="a4d57-146">Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app en ze waarden van eigenschappen bevatten, u kunt de eigenschap in de lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="a4d57-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="a4d57-147">Is de grafiek te klein voor gesegmenteerde gegevens?</span><span class="sxs-lookup"><span data-stu-id="a4d57-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="a4d57-148">De hoogte aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a4d57-148">Adjust its height:</span></span>

![Stel de schuifregelaar](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="a4d57-150">Aggregatietypen</span><span class="sxs-lookup"><span data-stu-id="a4d57-150">Aggregation types</span></span>
<span data-ttu-id="a4d57-151">De legenda aan de kant standaard toont de cumulatieve waarde meestal gedurende de periode van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a4d57-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="a4d57-152">Als u de muisaanwijzer op de grafiek, wordt de waarde op dat moment.</span><span class="sxs-lookup"><span data-stu-id="a4d57-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="a4d57-153">Elk gegevenspunt in de grafiek wordt een statistische functie van de gegevenswaarden in de voorgaande steekproefinterval of 'granulatie' ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="a4d57-154">De granulatie wordt weergegeven boven aan de blade en is afhankelijk van de algehele tijdschaal van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a4d57-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="a4d57-155">Metrische gegevens kunnen op verschillende manieren worden samengevoegd:</span><span class="sxs-lookup"><span data-stu-id="a4d57-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="a4d57-156">**Aantal** is een aantal van de gebeurtenissen ontvangen in het controle-interval.</span><span class="sxs-lookup"><span data-stu-id="a4d57-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="a4d57-157">Het wordt gebruikt voor gebeurtenissen zoals aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-157">It is used for events such as requests.</span></span> <span data-ttu-id="a4d57-158">Verschillen in de hoogte van de grafiek geeft variaties in de snelheid waarmee de gebeurtenissen plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="a4d57-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="a4d57-159">Maar houd er rekening mee dat de numerieke waarde verandert wanneer u het steekproefinterval wijzigt.</span><span class="sxs-lookup"><span data-stu-id="a4d57-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="a4d57-160">**Som** voegt de waarden van alle gegevenspunten ontvangen via het controle-interval of de periode van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a4d57-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="a4d57-161">**Gemiddelde** verdeelt de som van het aantal gegevenspunten ontvangen over het interval.</span><span class="sxs-lookup"><span data-stu-id="a4d57-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="a4d57-162">**Unieke** tellingen voor aantallen gebruikers en -accounts worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4d57-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="a4d57-163">Via het controle-interval of gedurende de periode van de grafiek ziet de afbeelding u de telling van andere gebruikers in die tijd weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a4d57-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="a4d57-164">**%**-percentage versies van elke aggregatie worden alleen gebruikt met gesegmenteerde grafieken.</span><span class="sxs-lookup"><span data-stu-id="a4d57-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="a4d57-165">Het totale aantal altijd tot wel 100% wordt toegevoegd en de grafiek geeft de relatieve bijdrage van verschillende onderdelen van een totaal.</span><span class="sxs-lookup"><span data-stu-id="a4d57-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Percentage aggregatie](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="a4d57-167">Het samenvoegingstype wijzigen</span><span class="sxs-lookup"><span data-stu-id="a4d57-167">Change the aggregation type</span></span>

![De grafiek bewerken en selecteer vervolgens de samenvoeging](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="a4d57-169">De standaardmethode voor elke waarde wordt weergegeven wanneer u een nieuwe grafiek maakt of wanneer alle metrische gegevens zijn uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="a4d57-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Schakel alle metrische gegevens voor een overzicht van de standaardinstellingen](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="a4d57-171">Y-as pincode</span><span class="sxs-lookup"><span data-stu-id="a4d57-171">Pin Y-axis</span></span> 
<span data-ttu-id="a4d57-172">Standaard bevat een grafiek Y-as waarden vanaf nul tot de maximale waarden in het gegevensbereik geven een visuele representatie van quantum van de waarden.</span><span class="sxs-lookup"><span data-stu-id="a4d57-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="a4d57-173">Maar in sommige gevallen meer dan het quantum mogelijk interessant visueel kleine wijzigingen in de waarden te controleren.</span><span class="sxs-lookup"><span data-stu-id="a4d57-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="a4d57-174">De y-as liggen voor aanpassingen zoals dit gebruik bewerken functie om de waarde voor y-as minimum of maximum op de gewenste plaats vast te maken.</span><span class="sxs-lookup"><span data-stu-id="a4d57-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="a4d57-175">Klik op het selectievakje 'Geavanceerde instellingen' online zetten van het bereik voor y-as instellingen</span><span class="sxs-lookup"><span data-stu-id="a4d57-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Klik op Geavanceerde instellingen aangepast bereik, en selecteer min max-waarden opgeven](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="a4d57-177">Filter uw gegevens</span><span class="sxs-lookup"><span data-stu-id="a4d57-177">Filter your data</span></span>
<span data-ttu-id="a4d57-178">Om te zien alleen de metrische gegevens voor een geselecteerde set met eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="a4d57-178">To see just the metrics for a selected set of property values:</span></span>

![Klik op Filter, vouw een eigenschap en sommige waarden controleren](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="a4d57-180">Als u geen waarden voor een bepaalde eigenschap selecteert, is hetzelfde als wanneer u ze allemaal: Er is geen filter op die eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a4d57-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="a4d57-181">U ziet het aantal gebeurtenissen naast elke eigenschapswaarde.</span><span class="sxs-lookup"><span data-stu-id="a4d57-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="a4d57-182">Wanneer u de waarden van een eigenschap selecteert, wordt het aantal naast andere eigenschapswaarden worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="a4d57-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="a4d57-183">Filters zijn van toepassing op de grafieken op een blade.</span><span class="sxs-lookup"><span data-stu-id="a4d57-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="a4d57-184">Desgewenst kunt u verschillende filters zijn toegepast op verschillende grafieken maken en opslaan van andere metrische gegevens blades.</span><span class="sxs-lookup"><span data-stu-id="a4d57-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="a4d57-185">Als u wilt, kunt u diagrammen van verschillende blades naar het dashboard vastmaken zodat u ze naast elkaar kan zien.</span><span class="sxs-lookup"><span data-stu-id="a4d57-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="a4d57-186">Verkeer van bot en web-test verwijderen</span><span class="sxs-lookup"><span data-stu-id="a4d57-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="a4d57-187">Gebruik het filter **daadwerkelijk of synthetisch verkeer** en Controleer **echte**.</span><span class="sxs-lookup"><span data-stu-id="a4d57-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="a4d57-188">U kunt ook filteren op **bron van synthetisch verkeer**.</span><span class="sxs-lookup"><span data-stu-id="a4d57-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="a4d57-189">Eigenschappen toevoegen aan de lijst met filters</span><span class="sxs-lookup"><span data-stu-id="a4d57-189">To add properties to the filter list</span></span>
<span data-ttu-id="a4d57-190">Wilt u voor het filteren van telemetrie voor een categorie van uw eigen kiezen?</span><span class="sxs-lookup"><span data-stu-id="a4d57-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="a4d57-191">Bijvoorbeeld, misschien verdeelt u van uw gebruikers in verschillende categorieën en u wilt dat uw gegevens te segmenteren in deze categorieën.</span><span class="sxs-lookup"><span data-stu-id="a4d57-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="a4d57-192">[Maak uw eigen eigenschap](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="a4d57-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="a4d57-193">Stel deze een [telemetrie initialisatiefunctie](app-insights-api-custom-events-metrics.md#defaults) zodat deze worden weergegeven in alle telemetrie - waaronder de standaard telemetrie verzonden door de verschillende SDK-modules.</span><span class="sxs-lookup"><span data-stu-id="a4d57-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="a4d57-194">Het grafiektype bewerken</span><span class="sxs-lookup"><span data-stu-id="a4d57-194">Edit the chart type</span></span>
<span data-ttu-id="a4d57-195">Merk op dat u tussen rasters en diagrammen kunt maken schakelen kunt:</span><span class="sxs-lookup"><span data-stu-id="a4d57-195">Notice that you can switch between grids and graphs:</span></span>

![Selecteer een raster of de grafiek en een grafiektype kiezen](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="a4d57-197">De blade metrische gegevens opslaan</span><span class="sxs-lookup"><span data-stu-id="a4d57-197">Save your metrics blade</span></span>
<span data-ttu-id="a4d57-198">Wanneer u sommige grafieken hebt gemaakt, kunt u ze als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="a4d57-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="a4d57-199">U kunt kiezen of worden gedeeld met andere teamleden, als u een organisatie-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4d57-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Kies favoriet](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="a4d57-201">Opnieuw, zodat de blade **gaat u naar de overzichtsblade** en Favorieten openen:</span><span class="sxs-lookup"><span data-stu-id="a4d57-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![Kies in de blade overzicht Favorieten](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="a4d57-203">Als u relatief tijdsbereik kiest wanneer u hebt opgeslagen, wordt de blade worden bijgewerkt met de meest recente metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a4d57-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="a4d57-204">Als u een absoluut tijdsbereik kiest, wordt deze telkens dezelfde gegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="a4d57-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="a4d57-205">De blade opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="a4d57-205">Reset the blade</span></span>
<span data-ttu-id="a4d57-206">Als u een blade bewerken, maar vervolgens u wilt teruggaan naar de oorspronkelijke set opgeslagen, klikt u op opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![In de knoppen aan de bovenkant van de metriek Explorer](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="a4d57-208">Stream Live metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="a4d57-208">Live metrics stream</span></span>

<span data-ttu-id="a4d57-209">Uw telemetrie veel meer direct wilt bekijken, opent u [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="a4d57-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="a4d57-210">De meeste metrische gegevens duren even wilt weergeven, door het proces van aggregatie.</span><span class="sxs-lookup"><span data-stu-id="a4d57-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="a4d57-211">Daarentegen zijn live metrische gegevens geoptimaliseerd voor lage latentie.</span><span class="sxs-lookup"><span data-stu-id="a4d57-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="a4d57-212">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="a4d57-212">Set alerts</span></span>
<span data-ttu-id="a4d57-213">Ontvangen van e-mailadres van ongebruikelijke waarden van alle metrische gegevens, moet u een waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="a4d57-214">U kunt ofwel het e-mailbericht verzenden naar de accountbeheerders, of specifieke e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="a4d57-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![Kies in Metrics Explorer waarschuwingsregels, waarschuwing toevoegen](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="a4d57-216">[Meer informatie over waarschuwingen][alerts].</span><span class="sxs-lookup"><span data-stu-id="a4d57-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="a4d57-217">Continuous Export</span><span class="sxs-lookup"><span data-stu-id="a4d57-217">Continuous Export</span></span>
<span data-ttu-id="a4d57-218">Als u gegevens continu exporteren wilt, zodat u deze extern kan verwerken, kunt u overwegen [continue export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="a4d57-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="a4d57-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="a4d57-219">Power BI</span></span>
<span data-ttu-id="a4d57-220">Als u nog meer weergaven van uw gegevens wilt, kunt u [exporteren naar Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4d57-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="a4d57-221">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="a4d57-221">Analytics</span></span>
<span data-ttu-id="a4d57-222">[Analytics](app-insights-analytics.md) is een flexibeler manier om uw telemetrie met behulp van een krachtige querytaal analyseren.</span><span class="sxs-lookup"><span data-stu-id="a4d57-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="a4d57-223">Te gebruiken als u wilt combineren de resultaten van de metrische gegevens berekenen, of een diepgaande exploratie van recente prestaties van uw app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a4d57-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="a4d57-224">Uit een metrische grafiek, kunt u het pictogram Analytics rechtstreeks naar de equivalente Analytics-query.</span><span class="sxs-lookup"><span data-stu-id="a4d57-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a4d57-225">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="a4d57-225">Troubleshooting</span></span>
<span data-ttu-id="a4d57-226">*Ik zie niet alle gegevens in de grafiek.*</span><span class="sxs-lookup"><span data-stu-id="a4d57-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="a4d57-227">Filters zijn van toepassing op de grafieken op de blade.</span><span class="sxs-lookup"><span data-stu-id="a4d57-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="a4d57-228">Zorg ervoor dat u een filter dat de gegevens op een andere uitsluit niet instellen terwijl u te op één grafiek focussen bent.</span><span class="sxs-lookup"><span data-stu-id="a4d57-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="a4d57-229">Als u verschillende filters instellen voor verschillende grafieken, maakt u deze in verschillende blades wilt, slaat u ze als afzonderlijke Favorieten.</span><span class="sxs-lookup"><span data-stu-id="a4d57-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="a4d57-230">Als u wilt, kunt u ze naar het dashboard vastmaken zodat u ze naast elkaar kan zien.</span><span class="sxs-lookup"><span data-stu-id="a4d57-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="a4d57-231">Als u een grafiek met een eigenschap die is niet gedefinieerd in de metriek groepeert, wordt er niets op de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a4d57-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="a4d57-232">Wist u 'groeperen op' of kies een verschillende groepeerniveaus-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a4d57-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="a4d57-233">Prestatiegegevens (CPU, i/o-snelheid, enzovoort) is beschikbaar voor Java-web-services, Windows desktop-apps, [IIS web-apps en services als u de statusmonitor installeren](app-insights-monitor-performance-live-website-now.md), en [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a4d57-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="a4d57-234">Het is niet beschikbaar voor Azure websites.</span><span class="sxs-lookup"><span data-stu-id="a4d57-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="a4d57-235">Video</span><span class="sxs-lookup"><span data-stu-id="a4d57-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="a4d57-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4d57-236">Next steps</span></span>
* [<span data-ttu-id="a4d57-237">Gebruik met Application Insights controleren</span><span class="sxs-lookup"><span data-stu-id="a4d57-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="a4d57-238">Met behulp van diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="a4d57-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
