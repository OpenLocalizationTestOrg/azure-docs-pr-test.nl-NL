---
title: aaaExploring metrische gegevens in Azure Application Insights | Microsoft Docs
description: Hoe toointerpret op metrische explorer-grafieken en hoe toocustomize metrische explorer blades.
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
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="6bd05-103">Verkennen van metrische gegevens in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6bd05-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="6bd05-104">Metrische gegevens in [Application Insights] [ start] zijn gemeten waarden en het aantal gebeurtenissen die worden verzonden in de telemetrie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6bd05-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="6bd05-105">Ze helpen u bij het detecteren van prestatieproblemen en bekijk hoe trends in hoe uw toepassing wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bd05-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="6bd05-106">Er is een breed scala aan standard metrische gegevens en u kunt ook uw eigen aangepaste metrische gegevens en gebeurtenissen maken.</span><span class="sxs-lookup"><span data-stu-id="6bd05-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="6bd05-107">Aantal metrische gegevens en gebeurtenissen worden weergegeven in de grafieken van de geaggregeerde waarden zoals optellen, gemiddelden of aantallen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="6bd05-108">Hier volgt een voorbeeld reeks grafieken:</span><span class="sxs-lookup"><span data-stu-id="6bd05-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="6bd05-109">U vindt metrische gegevens grafieken overal in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="6bd05-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="6bd05-110">In de meeste gevallen kan worden aangepast en u kunt meer grafieken toohello blade toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="6bd05-111">Hallo overzicht blade doorklikken toomore gedetailleerde grafieken (die titels zoals 'Servers'), of klik op **Metrics Explorer** tooopen een nieuwe blade waarin u aangepaste grafieken kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6bd05-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="6bd05-112">Tijdsbereik</span><span class="sxs-lookup"><span data-stu-id="6bd05-112">Time range</span></span>
<span data-ttu-id="6bd05-113">Hallo tijdsbereik Hallo grafieken of rasters op een blade vallen, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Overzichtsblade Open Hallo van uw toepassing hello Azure-portal](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="6bd05-115">Als u binnen enkele gegevens die nog niet zijn geregistreerd verwacht, klikt u op vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="6bd05-116">Grafieken vernieuwd met een interval, maar hello-intervallen zijn langer van grotere tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="6bd05-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="6bd05-117">Het kan even toocome via Hallo analysis pipeline gegevens naar een diagram duren.</span><span class="sxs-lookup"><span data-stu-id="6bd05-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="6bd05-118">toozoom in deel van een grafiek Sleep eroverheen:</span><span class="sxs-lookup"><span data-stu-id="6bd05-118">toozoom into part of a chart, drag over it:</span></span>

![Sleep over een deel van een diagram.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="6bd05-120">Klik op Hallo ongedaan zoomen knop toorestore deze.</span><span class="sxs-lookup"><span data-stu-id="6bd05-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="6bd05-121">Samenvattingen en punt waarden</span><span class="sxs-lookup"><span data-stu-id="6bd05-121">Granularity and point values</span></span>
<span data-ttu-id="6bd05-122">De muisaanwijzer op Hallo toodisplay Hallo grafiekwaarden van Hallo metrische gegevens op dat moment.</span><span class="sxs-lookup"><span data-stu-id="6bd05-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Beweeg de muisaanwijzer Hallo over een grafiek](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="6bd05-124">Hallo-waarde van Hallo metriek op een bepaald punt wordt tijdens de voorgaande steekproefinterval Hallo geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="6bd05-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="6bd05-125">Hallo steekproefinterval of 'granulatie' wordt hello boven aan het Hallo-blade weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6bd05-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![Hallo-header van een blade.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="6bd05-127">U kunt Hallo granulatie Hallo tijd bereik blade aanpassen:</span><span class="sxs-lookup"><span data-stu-id="6bd05-127">You can adjust hello granularity in hello Time range blade:</span></span>

![Hallo-header van een blade.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="6bd05-129">Hallo granulariteit beschikbaar, is afhankelijk van Hallo tijdsbereik die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="6bd05-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="6bd05-130">Hallo expliciete granulaties zijn alternatieven toohello 'automatisch' verfijning voor Hallo tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="6bd05-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="6bd05-131">Grafieken en rasters bewerken</span><span class="sxs-lookup"><span data-stu-id="6bd05-131">Editing charts and grids</span></span>
<span data-ttu-id="6bd05-132">een nieuwe grafiek toohello blade tooadd:</span><span class="sxs-lookup"><span data-stu-id="6bd05-132">tooadd a new chart toohello blade:</span></span>

![Kies in Metrics Explorer grafiek toevoegen](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="6bd05-134">Selecteer **bewerken** op een bestaande of nieuwe grafiek tooedit wat er wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6bd05-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Selecteer een of meer waarden](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="6bd05-136">Hoewel er beperkingen van het Hallo-combinaties die samen kunnen worden weergegeven, kunt u meer dan een waarde in een grafiek weergeven.</span><span class="sxs-lookup"><span data-stu-id="6bd05-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="6bd05-137">Als u een waarde, aantal Hallo die andere protocollen zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6bd05-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="6bd05-138">Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app (aanroepen tooTrackMetric en TrackEvent) ze worden hier vermeld.</span><span class="sxs-lookup"><span data-stu-id="6bd05-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="6bd05-139">Segmenteren van uw gegevens</span><span class="sxs-lookup"><span data-stu-id="6bd05-139">Segment your data</span></span>
<span data-ttu-id="6bd05-140">U kunt een waarde splitsen door eigenschap - bijvoorbeeld toocompare paginaweergaven op clients met verschillende besturingssystemen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bd05-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="6bd05-141">Selecteer een grafiek of het raster, switch voor de groepering en kies een eigenschap toogroup door:</span><span class="sxs-lookup"><span data-stu-id="6bd05-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Selecteer groepering op set en selecteer vervolgens een eigenschap in Group By](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="6bd05-143">Wanneer u groepering gebruikt, geef Hallo gebied en staafdiagram typen een gestapelde weergave.</span><span class="sxs-lookup"><span data-stu-id="6bd05-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="6bd05-144">Dit is geschikt waarbij Hallo aggregatiemethode Sum.</span><span class="sxs-lookup"><span data-stu-id="6bd05-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="6bd05-145">Maar wanneer Hallo samenvoegingstype gemiddelde, ervoor kiezen de Hallo Line- of het raster weergave typen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="6bd05-146">Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app en ze waarden van eigenschappen bevatten, u kunt tooselect Hallo-eigenschap in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="6bd05-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="6bd05-147">Is Hallo-diagram te klein voor gesegmenteerde gegevens?</span><span class="sxs-lookup"><span data-stu-id="6bd05-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="6bd05-148">De hoogte aanpassen:</span><span class="sxs-lookup"><span data-stu-id="6bd05-148">Adjust its height:</span></span>

![Hallo schuifregelaar aanpassen](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="6bd05-150">Aggregatietypen</span><span class="sxs-lookup"><span data-stu-id="6bd05-150">Aggregation types</span></span>
<span data-ttu-id="6bd05-151">Hallo legenda Hallo side standaard geeft meestal Hallo geaggregeerd waarde gedurende de periode Hallo van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="6bd05-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="6bd05-152">Als u de muisaanwijzer op Hallo grafiek, toont het Hallo-waarde op dat moment.</span><span class="sxs-lookup"><span data-stu-id="6bd05-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="6bd05-153">Elk gegevenspunt op Hallo grafiek is een totaal van Hallo gegevenswaarden in de vorige steekproef nemen interval of 'granulatie' hello ontvangen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="6bd05-154">Hallo granulatie Hallo boven aan het Hallo-blade wordt weergegeven en is afhankelijk van Hallo algehele tijdschaal van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="6bd05-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="6bd05-155">Metrische gegevens kunnen op verschillende manieren worden samengevoegd:</span><span class="sxs-lookup"><span data-stu-id="6bd05-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="6bd05-156">**Aantal** is een telling van Hallo-gebeurtenissen ontvangen in Hallo steekproefinterval.</span><span class="sxs-lookup"><span data-stu-id="6bd05-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="6bd05-157">Het wordt gebruikt voor gebeurtenissen zoals aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-157">It is used for events such as requests.</span></span> <span data-ttu-id="6bd05-158">Verschillen in de Hallo hoogte van de grafiek Hallo geeft variaties in Hallo snelheid waarmee Hallo gebeurtenissen plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="6bd05-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="6bd05-159">Maar houd er rekening mee dat Hallo numerieke waarde verandert wanneer u Hallo steekproefinterval wijzigt.</span><span class="sxs-lookup"><span data-stu-id="6bd05-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="6bd05-160">**Som** Hallo waarden van alle Hallo gegevenspunten ontvangen via Hallo steekproefinterval of Hallo periode van Hallo grafiek worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6bd05-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="6bd05-161">**Gemiddelde** delen Hallo som door Hallo aantal gegevenspunten ontvangen via hello-interval.</span><span class="sxs-lookup"><span data-stu-id="6bd05-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="6bd05-162">**Unieke** tellingen voor aantallen gebruikers en -accounts worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bd05-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="6bd05-163">Via Hallo steekproefinterval of gedurende de periode Hallo van grafiek Hallo ziet Hallo afbeelding u Hallo-telling van andere gebruikers in die tijd weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6bd05-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="6bd05-164">**%**-percentage versies van elke aggregatie worden alleen gebruikt met gesegmenteerde grafieken.</span><span class="sxs-lookup"><span data-stu-id="6bd05-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="6bd05-165">Hallo totale wordt altijd een too100% en Hallo diagram toont de relatieve bijdrage Hallo van verschillende onderdelen van een totaal.</span><span class="sxs-lookup"><span data-stu-id="6bd05-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Percentage aggregatie](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="6bd05-167">Hallo samenvoegingstype wijzigen</span><span class="sxs-lookup"><span data-stu-id="6bd05-167">Change hello aggregation type</span></span>

![Hallo grafiek bewerken en selecteer vervolgens aggregatie](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="6bd05-169">Hallo standaardmethode voor elke waarde wordt weergegeven wanneer u een nieuwe grafiek of wanneer alle metrische gegevens zijn uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="6bd05-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Schakel alle metrische gegevens toosee Hallo standaardwaarden](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="6bd05-171">Y-as pincode</span><span class="sxs-lookup"><span data-stu-id="6bd05-171">Pin Y-axis</span></span> 
<span data-ttu-id="6bd05-172">Standaard bevat een grafiek Y-as waarden vanaf nul tot de maximale waarden in het gegevensbereik hello, toogive een visuele representatie van quantum van Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="6bd05-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="6bd05-173">Maar in sommige gevallen meer dan Hallo quantum mogelijk interessant toovisually inspecteren kleine wijzigingen in waarden.</span><span class="sxs-lookup"><span data-stu-id="6bd05-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="6bd05-174">Voor aanpassingen als Hallo dit gebruik y-as bewerken functie toopin Hallo y-as minimum of maximum bereikwaarde op het gewenste plaats.</span><span class="sxs-lookup"><span data-stu-id="6bd05-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="6bd05-175">Klik op 'Advanced instellingen' selectievakje toobring up Hallo bereik voor y-as instellingen</span><span class="sxs-lookup"><span data-stu-id="6bd05-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Klik op Geavanceerde instellingen aangepast bereik, en selecteer min max-waarden opgeven](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="6bd05-177">Filter uw gegevens</span><span class="sxs-lookup"><span data-stu-id="6bd05-177">Filter your data</span></span>
<span data-ttu-id="6bd05-178">toosee alleen Hallo metrische gegevens voor een geselecteerde set met eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="6bd05-178">toosee just hello metrics for a selected set of property values:</span></span>

![Klik op Filter, vouw een eigenschap en sommige waarden controleren](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="6bd05-180">Als u geen waarden voor een bepaalde eigenschap selecteert, is deze gelijk aan te vinken ze allemaal Hallo: Er is geen filter op die eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6bd05-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="6bd05-181">Kennisgeving Hallo telt van gebeurtenissen naast elke eigenschapswaarde.</span><span class="sxs-lookup"><span data-stu-id="6bd05-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="6bd05-182">Wanneer u de waarden van een eigenschap selecteert, telt Hallo naast een andere eigenschap waarden worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="6bd05-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="6bd05-183">Tooall hello grafieken toepassen filters op een blade.</span><span class="sxs-lookup"><span data-stu-id="6bd05-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="6bd05-184">Als u verschillende filters zijn toegepast toodifferent grafieken, maken en opslaan van andere metrische gegevens blades.</span><span class="sxs-lookup"><span data-stu-id="6bd05-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="6bd05-185">Als u wilt, kunt u diagrammen in verschillende blades toohello dashboard vastmaken zodat u ze naast elkaar kan zien.</span><span class="sxs-lookup"><span data-stu-id="6bd05-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="6bd05-186">Verkeer van bot en web-test verwijderen</span><span class="sxs-lookup"><span data-stu-id="6bd05-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="6bd05-187">Gebruik Hallo filter **daadwerkelijk of synthetisch verkeer** en Controleer **echte**.</span><span class="sxs-lookup"><span data-stu-id="6bd05-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="6bd05-188">U kunt ook filteren op **bron van synthetisch verkeer**.</span><span class="sxs-lookup"><span data-stu-id="6bd05-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="6bd05-189">tooadd eigenschappen toohello-filterlijst</span><span class="sxs-lookup"><span data-stu-id="6bd05-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="6bd05-190">Wilt u toofilter telemetrie voor een categorie van uw eigen kiezen?</span><span class="sxs-lookup"><span data-stu-id="6bd05-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="6bd05-191">Bijvoorbeeld, misschien verdeelt u van uw gebruikers in verschillende categorieën en u wilt dat uw gegevens te segmenteren in deze categorieën.</span><span class="sxs-lookup"><span data-stu-id="6bd05-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="6bd05-192">[Maak uw eigen eigenschap](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="6bd05-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="6bd05-193">Stel deze een [telemetrie initialisatiefunctie](app-insights-api-custom-events-metrics.md#defaults) toohave wordt dit weergegeven in alle telemetrie - inclusief Hallo standaard telemetrie verzonden door de verschillende SDK-modules.</span><span class="sxs-lookup"><span data-stu-id="6bd05-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="6bd05-194">Hallo grafiektype bewerken</span><span class="sxs-lookup"><span data-stu-id="6bd05-194">Edit hello chart type</span></span>
<span data-ttu-id="6bd05-195">Merk op dat u tussen rasters en diagrammen kunt maken schakelen kunt:</span><span class="sxs-lookup"><span data-stu-id="6bd05-195">Notice that you can switch between grids and graphs:</span></span>

![Selecteer een raster of de grafiek en een grafiektype kiezen](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="6bd05-197">De blade metrische gegevens opslaan</span><span class="sxs-lookup"><span data-stu-id="6bd05-197">Save your metrics blade</span></span>
<span data-ttu-id="6bd05-198">Wanneer u sommige grafieken hebt gemaakt, kunt u ze als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="6bd05-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="6bd05-199">U kunt kiezen of tooshare met andere teamleden, als u een organisatie-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bd05-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Kies favoriet](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="6bd05-201">Hallo blade opnieuw toosee **Ga toohello overzichtsblade** en Favorieten openen:</span><span class="sxs-lookup"><span data-stu-id="6bd05-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Kies in de overzichtsblade Hallo Favorieten](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="6bd05-203">Als u relatief tijdsbereik kiest wanneer u hebt opgeslagen, wordt met de meest recente metrische gegevens Hallo Hallo blade bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6bd05-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="6bd05-204">Als u een absoluut tijdsbereik kiest, wordt het weergegeven Hallo dezelfde gegevens elke keer.</span><span class="sxs-lookup"><span data-stu-id="6bd05-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="6bd05-205">Hallo-blade opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6bd05-205">Reset hello blade</span></span>
<span data-ttu-id="6bd05-206">Als u een blade bewerken, maar vervolgens de gewenste tooget back toohello oorspronkelijke opgeslagen instellen, klikt u op opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![In de knoppen Hallo Hallo boven aan het metriek Explorer](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="6bd05-208">Stream Live metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="6bd05-208">Live metrics stream</span></span>

<span data-ttu-id="6bd05-209">Uw telemetrie veel meer direct wilt bekijken, opent u [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="6bd05-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="6bd05-210">De meeste metrische gegevens nemen een paar minuten tooappear, vanwege Hallo-proces voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="6bd05-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="6bd05-211">Daarentegen zijn live metrische gegevens geoptimaliseerd voor lage latentie.</span><span class="sxs-lookup"><span data-stu-id="6bd05-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="6bd05-212">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="6bd05-212">Set alerts</span></span>
<span data-ttu-id="6bd05-213">op de hoogte met e-mailadres van ongebruikelijke waarden van een metriek toobe een waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6bd05-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="6bd05-214">U kunt toohello accountbeheerders voor toosend Hallo e of e-mailadressen toospecific.</span><span class="sxs-lookup"><span data-stu-id="6bd05-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![Kies in Metrics Explorer waarschuwingsregels, waarschuwing toevoegen](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="6bd05-216">[Meer informatie over waarschuwingen][alerts].</span><span class="sxs-lookup"><span data-stu-id="6bd05-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="6bd05-217">Continuous Export</span><span class="sxs-lookup"><span data-stu-id="6bd05-217">Continuous Export</span></span>
<span data-ttu-id="6bd05-218">Als u gegevens continu exporteren wilt, zodat u deze extern kan verwerken, kunt u overwegen [continue export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="6bd05-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="6bd05-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="6bd05-219">Power BI</span></span>
<span data-ttu-id="6bd05-220">Als u nog meer weergaven van uw gegevens wilt, kunt u [tooPower BI exporteren](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bd05-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="6bd05-221">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="6bd05-221">Analytics</span></span>
<span data-ttu-id="6bd05-222">[Analytics](app-insights-analytics.md) is een flexibeler manier tooanalyze uw telemetrie met behulp van een krachtige querytaal.</span><span class="sxs-lookup"><span data-stu-id="6bd05-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="6bd05-223">Te gebruiken als u toocombine wilt berekenen van de resultaten van de metrische gegevens, of een diepgaande exploratie van recente prestaties van uw app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6bd05-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="6bd05-224">In een grafiek metrische, klikt u op Hallo Analytics pictogram tooget rechtstreeks toohello gelijkwaardige Analytics-query.</span><span class="sxs-lookup"><span data-stu-id="6bd05-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6bd05-225">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6bd05-225">Troubleshooting</span></span>
<span data-ttu-id="6bd05-226">*Ik zie niet alle gegevens in de grafiek.*</span><span class="sxs-lookup"><span data-stu-id="6bd05-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="6bd05-227">Tooall hello grafieken toepassen filters op Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="6bd05-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="6bd05-228">Zorg ervoor dat u een filter dat alle Hallo gegevens op een andere uitsluit niet instellen terwijl u te op één grafiek focussen bent.</span><span class="sxs-lookup"><span data-stu-id="6bd05-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="6bd05-229">Als u tooset verschillende filters in verschillende grafieken wilt, maken ze in verschillende blades, opslaan als afzonderlijke Favorieten.</span><span class="sxs-lookup"><span data-stu-id="6bd05-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="6bd05-230">Als u wilt, kunt u ze vastmaken als toohello dashboard zodat u ze naast elkaar kan zien.</span><span class="sxs-lookup"><span data-stu-id="6bd05-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="6bd05-231">Als u een grafiek met een eigenschap die niet is gedefinieerd op Hallo metriek groepeert, wordt er niets op Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="6bd05-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="6bd05-232">Wist u 'groeperen op' of kies een verschillende groepeerniveaus-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6bd05-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="6bd05-233">Prestatiegegevens (CPU, i/o-snelheid, enzovoort) is beschikbaar voor Java-web-services, Windows desktop-apps, [IIS web-apps en services als u de statusmonitor installeren](app-insights-monitor-performance-live-website-now.md), en [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6bd05-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="6bd05-234">Het is niet beschikbaar voor Azure websites.</span><span class="sxs-lookup"><span data-stu-id="6bd05-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="6bd05-235">Video</span><span class="sxs-lookup"><span data-stu-id="6bd05-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="6bd05-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bd05-236">Next steps</span></span>
* [<span data-ttu-id="6bd05-237">Gebruik met Application Insights controleren</span><span class="sxs-lookup"><span data-stu-id="6bd05-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="6bd05-238">Met behulp van diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="6bd05-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
