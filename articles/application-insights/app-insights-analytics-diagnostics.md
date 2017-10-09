---
title: aaaSmart diagnostische gegevens van web-app prestaties wijzigingen in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="533b9-103">Onverwachte wijzigingen in uw app telemetrie onderzoeken</span><span class="sxs-lookup"><span data-stu-id="533b9-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="533b9-104">*Deze functie is in preview.*</span><span class="sxs-lookup"><span data-stu-id="533b9-104">*This feature is in preview.*</span></span>

<span data-ttu-id="533b9-105">Diagnose plotselinge veranderingen in uw web-app prestatie- of gebruik met een enkele klik!</span><span class="sxs-lookup"><span data-stu-id="533b9-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="533b9-106">Hallo Smart Diagnostics functie is beschikbaar wanneer u een grafiek tijd in maakt [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="533b9-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="533b9-107">Wanneer er ook een ongebruikelijke wijzigingen van de trend van uw resultaten, zoals een piek- of een dip Hallo identificeert Smart Diagnostics een patroon van dimensies en de bijbehorende waarden die Hallo wijzigen verklaren kunnen.</span><span class="sxs-lookup"><span data-stu-id="533b9-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="533b9-108">Zo kunt u snel Hallo probleem opsporen.</span><span class="sxs-lookup"><span data-stu-id="533b9-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="533b9-109">In dit voorbeeld Smart Diagnostics geconstateerd een patroon van eigenschapswaarden met Hallo wijziging en licht Hallo verschil tussen de resultaten met en zonder dit patroon:</span><span class="sxs-lookup"><span data-stu-id="533b9-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![voorbeeld analytics diagnostics resultaat](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="533b9-111">Gegevenswijzigingen onderzoeken</span><span class="sxs-lookup"><span data-stu-id="533b9-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="533b9-112">Een query in analyses uitvoeren en deze worden weergegeven als een tijd-grafiek.</span><span class="sxs-lookup"><span data-stu-id="533b9-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="533b9-113">Klik op elk gewenst moment gemarkeerde piek indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="533b9-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![piek-punt](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="533b9-115">Diagnostische gegevens duurt een paar seconden toodiscover een patroon.</span><span class="sxs-lookup"><span data-stu-id="533b9-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="533b9-116">Hallo diagnostische resultaten tabblad ziet u een patroon dat de onderbreking van uw gegevens kan verklaren.</span><span class="sxs-lookup"><span data-stu-id="533b9-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![Resultaat](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="533b9-118">Hallo tekst weergegeven hello dimensiewaarden die worden weergegeven toocorrelate met Hallo shift.</span><span class="sxs-lookup"><span data-stu-id="533b9-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="533b9-119">In dit voorbeeld is deze gekoppeld aan een bepaalde aanvraag en een bepaalde browser-versie.</span><span class="sxs-lookup"><span data-stu-id="533b9-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="533b9-120">U ziet ook Hallo twee onderdelen van de grafiek hello, met Hallo filter true en false.</span><span class="sxs-lookup"><span data-stu-id="533b9-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="533b9-121">Hallo false onderdeel toont een trend ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="533b9-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="533b9-122">Met andere woorden, is er geen wijziging in de resultaten van de telemetrie hello, als we uitsluiten Hallo problematisch combinatie van dimensies die Diagnostics is geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="533b9-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="533b9-123">Daarentegen, Hallo resultaten binnen deze combinatie een indrukwekkende wijziging binnen Hallo gemarkeerd gebied van onderzoek worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="533b9-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="533b9-124">Dit betekent dat diagnostische gegevens van een combinatie van eigenschappen die Hallo wijziging wordt heeft gevonden.</span><span class="sxs-lookup"><span data-stu-id="533b9-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="533b9-125">Als het Hallo-patroon complex is, moet u toohover via **Alles weergeven** toosee Hallo dimensies.</span><span class="sxs-lookup"><span data-stu-id="533b9-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![alles weergeven](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="533b9-127">Als diagnostische gegevens er geen significante patroon toonotify over Hallo vindt ' geen ' resultatenpagina krijgt.</span><span class="sxs-lookup"><span data-stu-id="533b9-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="533b9-128">Op dit moment kunt u uw query wijzigen.</span><span class="sxs-lookup"><span data-stu-id="533b9-128">At this point, you may change your query.</span></span> <span data-ttu-id="533b9-129">U kan bijvoorbeeld Hallo tijdsbereik en binning in Analytics-query voor een verdere analyse en mogelijk betere resultaten beperken.</span><span class="sxs-lookup"><span data-stu-id="533b9-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="533b9-130">. Met een bepaalde pagina van uw website is een probleem op een bepaalde browser Hallo-kennis, u kunt nu rechte toohello probleem pagina gaan en onderzoeken van recente wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="533b9-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="533b9-131">Probeer het Hallo-demo</span><span class="sxs-lookup"><span data-stu-id="533b9-131">Try hello demo</span></span>

<span data-ttu-id="533b9-132">[Klik hier toosee een demonstratie](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) op voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="533b9-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="533b9-133">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="533b9-133">How it works</span></span>

<span data-ttu-id="533b9-134">Smart Diagnostics maakt gebruik van een geavanceerde zonder supervisie machine learning-algoritme op basis van Hallo [DiffPatterns](app-insights-analytics-reference.md) bewerking.</span><span class="sxs-lookup"><span data-stu-id="533b9-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="533b9-135">Het lijkt erop voor candidate patronen die Hallo gegevens wijzigen verklaren kunnen.</span><span class="sxs-lookup"><span data-stu-id="533b9-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="533b9-136">Het Hallo-impact van elke kandidaat op Hallo metrische gegevens analyseert en bevat Hallo-patroon dat beste met Hallo wijziging correleert.</span><span class="sxs-lookup"><span data-stu-id="533b9-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="533b9-137">Geen diagnostische punten?</span><span class="sxs-lookup"><span data-stu-id="533b9-137">No diagnostic points?</span></span>

<span data-ttu-id="533b9-138">Smart Diagnostics werkt alleen wanneer Hallo volgende criteria wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="533b9-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="533b9-139">Smart Diagnostics-instelling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="533b9-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="533b9-140">Zoek in de Instellingenpictogram Hallo in Analytics.</span><span class="sxs-lookup"><span data-stu-id="533b9-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="533b9-141">Hallo Smart Diagnostics optie in de instellingen is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="533b9-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="533b9-142">Tijdas: Hallo x-as van grafiekgebied Hallo moet van het type `datetime`.</span><span class="sxs-lookup"><span data-stu-id="533b9-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="533b9-143">Line- of gebied grafiek: Diagnostics werkt alleen deze typen van grafiek.</span><span class="sxs-lookup"><span data-stu-id="533b9-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="533b9-144">Gebruik `| render timechart` of `| render areachart` aan Hallo einde van uw query; of Selecteer een regel of vlakdiagram Hallo vervolgkeuzelijst selector.</span><span class="sxs-lookup"><span data-stu-id="533b9-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="533b9-145">Onderbreking: Er moet een aanzienlijke onderbreking Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="533b9-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="533b9-146">Onvoldoende punten tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="533b9-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="533b9-147">Niet meer dan een overzicht van de component in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="533b9-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="533b9-148">Geen project-component met de definitie van een naam voordat Hallo overzicht van de component.</span><span class="sxs-lookup"><span data-stu-id="533b9-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="533b9-149">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="533b9-149">Related articles</span></span>

 * [<span data-ttu-id="533b9-150">Analytics-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="533b9-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="533b9-151">[Detectie van smartcard](app-insights-proactive-diagnostics.md) waarschuwt u automatisch tooperformance problemen.</span><span class="sxs-lookup"><span data-stu-id="533b9-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
