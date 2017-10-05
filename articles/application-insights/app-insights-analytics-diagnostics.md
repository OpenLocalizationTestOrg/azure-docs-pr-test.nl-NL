---
title: Diagnostische gegevens van web-app prestaties wijzigingen in Azure Application Insights van smartcard | Microsoft Docs
description: Automatische diagnoses pieken of stappen in de prestatietelemetrie van uw web-app.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="3d4ca-103">Onverwachte wijzigingen in uw app telemetrie onderzoeken</span><span class="sxs-lookup"><span data-stu-id="3d4ca-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="3d4ca-104">*Deze functie is in preview.*</span><span class="sxs-lookup"><span data-stu-id="3d4ca-104">*This feature is in preview.*</span></span>

<span data-ttu-id="3d4ca-105">Diagnose plotselinge veranderingen in uw web-app prestatie- of gebruik met een enkele klik!</span><span class="sxs-lookup"><span data-stu-id="3d4ca-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="3d4ca-106">De functie Smart Diagnostics is beschikbaar wanneer u een grafiek tijd in maakt [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d4ca-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3d4ca-107">Wanneer er ook een ongebruikelijke wijziging van de trend van de resultaten, zoals een piek- of een dip identificeert Smart Diagnostics een patroon van dimensies en de bijbehorende waarden die de wijziging kunnen verklaren.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="3d4ca-108">Zo kunt u snel diagnose van het probleem.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="3d4ca-109">In dit voorbeeld Smart Diagnostics een patroon van eigenschapswaarden die zijn gekoppeld aan de wijziging is geïdentificeerd en markeert het verschil tussen resultaten met en zonder dit patroon:</span><span class="sxs-lookup"><span data-stu-id="3d4ca-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![voorbeeld analytics diagnostics resultaat](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="3d4ca-111">Gegevenswijzigingen onderzoeken</span><span class="sxs-lookup"><span data-stu-id="3d4ca-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="3d4ca-112">Een query in analyses uitvoeren en deze worden weergegeven als een tijd-grafiek.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="3d4ca-113">Klik op elk gewenst moment gemarkeerde piek indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![piek-punt](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="3d4ca-115">Diagnostische gegevens duurt een paar seconden voor het detecteren van een patroon.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="3d4ca-116">Het tabblad diagnostische resultaten bevat een patroon dat de onderbreking van uw gegevens kan verklaren.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![Resultaat](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="3d4ca-118">De tekst bevat de dimensiewaarden die worden weergegeven met elkaar correleren met een verschuiving.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="3d4ca-119">In dit voorbeeld is deze gekoppeld aan een bepaalde aanvraag en een bepaalde browser-versie.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="3d4ca-120">U ziet ook de twee onderdelen van de grafiek, met het filter true en false.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="3d4ca-121">Het onderdeel false toont een trend ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="3d4ca-122">Met andere woorden, is er geen wijziging in de resultaten telemetrie als we de problematisch combinatie van dimensies met diagnostische gegevens geconstateerd uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="3d4ca-123">Daarentegen, worden de resultaten binnen deze combinatie een indrukwekkende wijziging weergegeven binnen het gemarkeerde gebied van onderzoek.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="3d4ca-124">Dit betekent dat diagnostische gegevens van een combinatie van eigenschappen die de wijziging wordt is gevonden.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="3d4ca-125">Als het patroon complex is, moet u de muisaanwijzer op **Alles weergeven** om te zien van de dimensies.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![alles weergeven](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="3d4ca-127">Diagnostische gegevens vindt er geen significante patroon melding versturen over, als de pagina 'geen resultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="3d4ca-128">Op dit moment kunt u uw query wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-128">At this point, you may change your query.</span></span> <span data-ttu-id="3d4ca-129">U kunt bijvoorbeeld beperken het tijdsbereik en binning in Analytics-query voor een verdere analyse en mogelijk betere resultaten.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="3d4ca-130">. Met de wetenschap dat een bepaalde pagina van uw website een probleem op een bepaalde browser heeft, u kunt nu gaat u door naar de pagina van het probleem en onderzoeken van recente wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="3d4ca-131">Probeer de demoversie</span><span class="sxs-lookup"><span data-stu-id="3d4ca-131">Try the demo</span></span>

<span data-ttu-id="3d4ca-132">[Klik hier voor een demonstratie](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) op voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="3d4ca-133">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="3d4ca-133">How it works</span></span>

<span data-ttu-id="3d4ca-134">Smart Diagnostics maakt gebruik van een geavanceerde zonder supervisie machine learning-algoritme op basis van de [DiffPatterns](app-insights-analytics-reference.md) bewerking.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="3d4ca-135">Kandidaat patronen die de gewijzigde gegevens kunnen verklaren zoekt.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="3d4ca-136">Deze analyses van de impact van elke kandidaat voor de metrische gegevens en is het patroon dat beste met de wijziging correleert.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="3d4ca-137">Geen diagnostische punten?</span><span class="sxs-lookup"><span data-stu-id="3d4ca-137">No diagnostic points?</span></span>

<span data-ttu-id="3d4ca-138">Smart Diagnostics werkt alleen wanneer de volgende criteria wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="3d4ca-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="3d4ca-139">Smart Diagnostics-instelling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="3d4ca-140">Zoek in het pictogram instellingen in Analytics.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="3d4ca-141">De optie Slimme diagnostische gegevens in de instellingen is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="3d4ca-142">Tijdas: de x-as van de grafiek moet van het type `datetime`.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="3d4ca-143">Line- of gebied grafiek: Diagnostics werkt alleen deze typen van grafiek.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="3d4ca-144">Gebruik `| render timechart` of `| render areachart` aan het einde van uw query; of Selecteer een regel of vlakdiagram van de selector vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="3d4ca-145">Onderbreking: Er moet een aanzienlijke onderbreking in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="3d4ca-146">Onvoldoende punten te analyseren.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="3d4ca-147">Niet meer dan een overzicht van de component in de query.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="3d4ca-148">Er is geen project-component met een definitie van de naam van voordat de component samenvatten.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="3d4ca-149">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="3d4ca-149">Related articles</span></span>

 * [<span data-ttu-id="3d4ca-150">Analytics-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="3d4ca-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="3d4ca-151">[Detectie van smartcard](app-insights-proactive-diagnostics.md) automatisch wordt u gewezen op prestatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="3d4ca-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>