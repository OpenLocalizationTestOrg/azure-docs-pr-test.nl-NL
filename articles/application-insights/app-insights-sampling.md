---
title: Telemetrie steekproeven in Azure Application Insights | Microsoft Docs
description: Hoe het volume van telemetrie onder controle te houden.
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="4877b-103">Steekproeven in Application Insights</span><span class="sxs-lookup"><span data-stu-id="4877b-103">Sampling in Application Insights</span></span>


<span data-ttu-id="4877b-104">Steekproeven is een functie in [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4877b-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="4877b-105">Dit is de aanbevolen manier om te beperken van telemetrie verkeer en opslag, behoud een statistisch correcte analyse van toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="4877b-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="4877b-106">Het filter selecteert items die zijn gerelateerd, zodat u tussen items navigeren kunt als u de diagnostische onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="4877b-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="4877b-107">Wanneer metrische aantallen bij u in de portal worden aangebracht, zijn ze renormalized rekening te houden met de steekproeven, om te beperken van invloed zijn op de statistieken.</span><span class="sxs-lookup"><span data-stu-id="4877b-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="4877b-108">Steekproeven verlaagt de kosten van verkeer en gegevens en kunt u voorkomen beperking.</span><span class="sxs-lookup"><span data-stu-id="4877b-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="4877b-109">Kort gezegd:</span><span class="sxs-lookup"><span data-stu-id="4877b-109">In brief:</span></span>
* <span data-ttu-id="4877b-110">Steekproeven behoudt 1 in  *n*  registreert en de rest wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="4877b-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="4877b-111">Het kan bijvoorbeeld een samplefrequentie van 20% 1: 5 gebeurtenissen behouden.</span><span class="sxs-lookup"><span data-stu-id="4877b-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="4877b-112">Steekproeven gebeurt automatisch als uw toepassing veel telemetrie, in ASP.NET web server-apps verzendt.</span><span class="sxs-lookup"><span data-stu-id="4877b-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="4877b-113">U kunt ook instellen steekproef nemen handmatig, hetzij in de portal op de pagina met prijzen; of in de ASP.NET-SDK in het .config-bestand ook het om netwerkverkeer te beperken.</span><span class="sxs-lookup"><span data-stu-id="4877b-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="4877b-114">Als u aangepaste gebeurtenissen en u ervoor zorgen wilt dat een verzameling van gebeurtenissen wordt behouden of verwijderd samen, zorg dat zij dezelfde OperationId waarde hebben.</span><span class="sxs-lookup"><span data-stu-id="4877b-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="4877b-115">De deler steekproeven  *n*  in elke record in de eigenschap wordt gerapporteerd `itemCount`, die in de zoekopdracht wordt weergegeven onder de beschrijvende naam van de aanvraag 'aantal' of 'gebeurtenis aantal'.</span><span class="sxs-lookup"><span data-stu-id="4877b-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="4877b-116">Wanneer steekproeven niet uitgevoerd is, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="4877b-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="4877b-117">Als u analysequery's schrijft, moet u [rekening houden met steekproeven](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="4877b-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="4877b-118">In het bijzonder in plaats van gewoon telling registreert, moet u `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="4877b-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="4877b-119">Typen steekproeven</span><span class="sxs-lookup"><span data-stu-id="4877b-119">Types of sampling</span></span>
<span data-ttu-id="4877b-120">Er zijn drie steekproeven van alternatieve methoden:</span><span class="sxs-lookup"><span data-stu-id="4877b-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="4877b-121">**Adaptieve steekproeven** automatisch het volume van telemetrie uit de SDK in uw ASP.NET-app verzonden.</span><span class="sxs-lookup"><span data-stu-id="4877b-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="4877b-122">De standaardinstelling van SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="4877b-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="4877b-123">Momenteel beschikbaar voor ASP.NET-serverzijde telemetrie alleen.</span><span class="sxs-lookup"><span data-stu-id="4877b-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="4877b-124">**Vast aantal steekproeven** vermindert het volume van telemetrie verzonden van zowel uw ASP.NET-server en de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4877b-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="4877b-125">Stelt u het tarief.</span><span class="sxs-lookup"><span data-stu-id="4877b-125">You set the rate.</span></span> <span data-ttu-id="4877b-126">De client en server synchroniseert de steekproeven zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.</span><span class="sxs-lookup"><span data-stu-id="4877b-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="4877b-127">**Opname steekproeven** werkt in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4877b-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="4877b-128">Het aantal de telemetrie van uw app, met een frequentie die u instelt binnenkomt wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4877b-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="4877b-129">Niet verminderen het verkeer van telemetrie, maar u kunt houden binnen uw maandelijkse quotum.</span><span class="sxs-lookup"><span data-stu-id="4877b-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="4877b-130">Het grote voordeel van opname steekproeven is dat u dit instellen kunt zonder dat uw app en het op uniforme wijze voor alle servers en clients werkt.</span><span class="sxs-lookup"><span data-stu-id="4877b-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="4877b-131">Als Adaptief of vast aantal steekproeven in bewerking, is opname steekproeven uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4877b-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="4877b-132">Opname steekproeven</span><span class="sxs-lookup"><span data-stu-id="4877b-132">Ingestion sampling</span></span>
<span data-ttu-id="4877b-133">Deze vorm van steekproeven werkt op het punt waar de telemetrie van uw webserver, browsers en apparaten bereikt voor het Application Insights-service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4877b-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="4877b-134">Hoewel dit niet de telemetrie verkeer dat wordt verzonden vanuit uw app beperken, het minder verwerkt en bewaard (en in rekening gebracht voor) door Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4877b-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="4877b-135">Gebruik dit type steekproeven als uw app vaak via het maandelijkse quotum wordt en u de optie hoeft van het gebruik van een van de typen SDK op basis van steekproeven.</span><span class="sxs-lookup"><span data-stu-id="4877b-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="4877b-136">De samplingfrequentie in de quota en prijzen van blade ingesteld:</span><span class="sxs-lookup"><span data-stu-id="4877b-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![Vanuit de blade overzicht van toepassing, klik op instellingen, Quota, voorbeelden, en vervolgens een samplefrequentie selecteren en klik op bijwerken.](./media/app-insights-sampling/04.png)

<span data-ttu-id="4877b-138">Net als andere soorten steekproeven behoudt de algoritme gerelateerde telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="4877b-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="4877b-139">Bijvoorbeeld, wanneer u de telemetrie in de zoekopdracht bekijken wilt, zult u kunnen vinden van de aanvraag die betrekking hebben op een bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="4877b-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="4877b-140">Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering correct blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="4877b-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="4877b-141">Gegevenspunten die zijn verwijderd door steekproeven zijn niet beschikbaar in de Application Insights-functies, zoals [continue Export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="4877b-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="4877b-142">Opname steekproeven functioneren niet terwijl er op basis van SDK adaptieve of vast aantal steekproeven wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4877b-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="4877b-143">Als u de samplingfrequentie op de SDK is minder dan 100%, wordt de samplefrequentie voor opname die u instelt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="4877b-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="4877b-144">De waarde die wordt weergegeven op de tegel geeft de waarde die u voor de opname steekproeven instellen.</span><span class="sxs-lookup"><span data-stu-id="4877b-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="4877b-145">Het vertegenwoordigen niet de werkelijke samplefrequentie als SDK steekproeven uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="4877b-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="4877b-146">Adaptieve steekproeven op uw webserver</span><span class="sxs-lookup"><span data-stu-id="4877b-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="4877b-147">Adaptieve steekproeven is beschikbaar voor de Application Insights-SDK voor ASP.NET v 2.0.0-beta3 of hoger, en is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4877b-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="4877b-148">Adaptieve steekproeven is van invloed op het volume van de telemetrie van uw web-app-server naar de Application Insights-service verzonden.</span><span class="sxs-lookup"><span data-stu-id="4877b-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="4877b-149">Het volume wordt automatisch aangepast behouden in de opgegeven maximale overdrachtssnelheid van verkeer.</span><span class="sxs-lookup"><span data-stu-id="4877b-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="4877b-150">Deze werkt niet op lage volumes telemetrie, dus een app in foutopsporing of een website met geringe gebruiksduur, worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="4877b-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="4877b-151">Zodat het doelvolume enkele van de telemetrie die is gegenereerd wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="4877b-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="4877b-152">Maar net als andere soorten steekproeven, behoudt de algoritme gerelateerde telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="4877b-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="4877b-153">Bijvoorbeeld, wanneer u de telemetrie in de zoekopdracht bekijken wilt, zult u kunnen vinden van de aanvraag die betrekking hebben op een bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="4877b-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="4877b-154">Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering worden aangepast om te compenseren voor de samplefrequentie zodat ze ongeveer juiste waarden in de metriek Explorer tonen.</span><span class="sxs-lookup"><span data-stu-id="4877b-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="4877b-155">**Bijwerken van uw project NuGet** pakketten naar de meest recente *voorlopige versie* versie van Application Insights: met de rechtermuisknop op het project in Solution Explorer, kiest u NuGet-pakketten beheren controleren **opnemen voorlopige** en zoek naar Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="4877b-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="4877b-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), kunt u verschillende parameters in de `AdaptiveSamplingTelemetryProcessor` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4877b-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="4877b-157">De cijfers die wordt weergegeven, zijn de standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="4877b-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="4877b-158">De doel-snelheid waarmee de adaptieve algoritme is erop gericht voor **op elke server-host**.</span><span class="sxs-lookup"><span data-stu-id="4877b-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="4877b-159">Als uw web-app wordt uitgevoerd op veel hosts, verlaagt u deze waarde om te voorkomen binnen de snelheid van uw doel van het verkeer op de Application Insights-portal blijven.</span><span class="sxs-lookup"><span data-stu-id="4877b-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="4877b-160">Het interval waarmee de huidige frequentie van telemetrie opnieuw geëvalueerd is.</span><span class="sxs-lookup"><span data-stu-id="4877b-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="4877b-161">Evaluatie wordt uitgevoerd als een zwevend gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="4877b-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="4877b-162">U kunt dit interval verkorten als uw telemetrie onderhevig aan plotselinge bursts is.</span><span class="sxs-lookup"><span data-stu-id="4877b-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="4877b-163">Wanneer steekproef nemen percentage waarde verandert, hoe snel nadat we mogen voorbeeldpercentage opnieuw om vast te leggen minder gegevens te verlagen.</span><span class="sxs-lookup"><span data-stu-id="4877b-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="4877b-164">Wanneer steekproef nemen percentage waarde verandert, hoe snel nadat we mogen steekproeven percentage opnieuw voor het vastleggen van meer gegevens te verhogen.</span><span class="sxs-lookup"><span data-stu-id="4877b-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="4877b-165">Wat is de minimumwaarde mag we ingesteld als percentage steekproef varieert.</span><span class="sxs-lookup"><span data-stu-id="4877b-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="4877b-166">Als percentage steekproef varieert, is wat de toegestane maximumwaarde we klaar om in te stellen.</span><span class="sxs-lookup"><span data-stu-id="4877b-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="4877b-167">In de berekening van zwevend gemiddelde, het gewicht aan de meest recente waarde toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4877b-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="4877b-168">Gebruik een waarde die gelijk is aan of kleiner is dan 1.</span><span class="sxs-lookup"><span data-stu-id="4877b-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="4877b-169">Lagere waarden wordt de algoritme van minder reactieve naar plotselinge wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="4877b-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="4877b-170">De waarde die wordt toegewezen wanneer de app NET is gestart.</span><span class="sxs-lookup"><span data-stu-id="4877b-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="4877b-171">Niet verlaagt dit terwijl u fouten opspoort.</span><span class="sxs-lookup"><span data-stu-id="4877b-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="4877b-172">Puntkomma's gescheiden lijst van typen die u niet wilt op te nemen.</span><span class="sxs-lookup"><span data-stu-id="4877b-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="4877b-173">Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace.</span><span class="sxs-lookup"><span data-stu-id="4877b-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="4877b-174">Alle exemplaren van de opgegeven typen worden verzonden; de typen die niet zijn opgegeven, worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="4877b-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="4877b-175">Puntkomma's gescheiden lijst met typen die u wenst op te nemen.</span><span class="sxs-lookup"><span data-stu-id="4877b-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="4877b-176">Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace.</span><span class="sxs-lookup"><span data-stu-id="4877b-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="4877b-177">De opgegeven typen steekproeven worden genomen; alle exemplaren van de andere typen altijd verzonden.</span><span class="sxs-lookup"><span data-stu-id="4877b-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="4877b-178">**Uitschakelen** adaptieve steekproef nemen, verwijdert u het knooppunt AdaptiveSamplingTelemetryProcessor uit applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="4877b-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="4877b-179">Alternatief: adaptieve steekproeven in code configureren</span><span class="sxs-lookup"><span data-stu-id="4877b-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="4877b-180">In plaats van steekproeven in het .config-bestand aanpassen, kunt u code.</span><span class="sxs-lookup"><span data-stu-id="4877b-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="4877b-181">Hiermee kunt u opgeven van een callbackfunctie die wordt aangeroepen wanneer de samplefrequentie opnieuw geëvalueerd wordt.</span><span class="sxs-lookup"><span data-stu-id="4877b-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="4877b-182">U kunt dit bijvoorbeeld gebruiken om erachter te komen welke samplefrequentie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4877b-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="4877b-183">Verwijder de `AdaptiveSamplingTelemetryProcessor` knooppunt uit het .config-bestand.</span><span class="sxs-lookup"><span data-stu-id="4877b-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="4877b-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="4877b-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="4877b-185">([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="4877b-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="4877b-186">Steekproef voor webpagina's met JavaScript</span><span class="sxs-lookup"><span data-stu-id="4877b-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="4877b-187">U kunt de webpagina's voor vast tarief steekproeven vanaf een willekeurige server configureren.</span><span class="sxs-lookup"><span data-stu-id="4877b-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="4877b-188">Wanneer u [de webpagina's configureren voor Application Insights](app-insights-javascript.md), wijzigt u het codefragment die u via de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="4877b-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="4877b-189">(In ASP.NET-apps het fragment doorgaans gaat in _Layout.cshtml.)  Voeg een regel zoals `samplingPercentage: 10,` voordat de instrumentatiesleutel:</span><span class="sxs-lookup"><span data-stu-id="4877b-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="4877b-190">Kies een percentage dat bijna 100/N waarbij N staat voor een geheel getal voor het voorbeeldpercentage.</span><span class="sxs-lookup"><span data-stu-id="4877b-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="4877b-191">Momenteel wordt biedt geen ondersteuning voor andere waarden.</span><span class="sxs-lookup"><span data-stu-id="4877b-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="4877b-192">Als u tevens vast aantal steekproeven op de server inschakelt, worden de clients en de server worden gesynchroniseerd zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.</span><span class="sxs-lookup"><span data-stu-id="4877b-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="4877b-193">Vast aantal steekproeven voor ASP.NET-websites</span><span class="sxs-lookup"><span data-stu-id="4877b-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="4877b-194">Vast tarief steekproeven vermindert het verkeer van uw webserver en webbrowsers worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="4877b-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="4877b-195">In tegenstelling tot adaptieve steekproeven wordt telemetrie tegen een vast tarief dat u hebt besloten gereduceerd.</span><span class="sxs-lookup"><span data-stu-id="4877b-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="4877b-196">Het ook synchroniseert de client en server steekproeven zodat verwante items worden bewaard - bijvoorbeeld, zodat als u de weergave van een pagina in de zoekopdracht bekijkt, kunt u de gerelateerde aanvraag vinden.</span><span class="sxs-lookup"><span data-stu-id="4877b-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="4877b-197">Het algoritme steekproeven behoudt verwante items.</span><span class="sxs-lookup"><span data-stu-id="4877b-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="4877b-198">Voor elke aanvraag HTTP-worden gebeurtenissen, deze en gerelateerde gebeurtenissen genegeerd of verzonden.</span><span class="sxs-lookup"><span data-stu-id="4877b-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="4877b-199">In Metrics Explorer tarieven zoals aanvragen en uitzonderingen aantallen vermenigvuldigd met een factor om te compenseren voor de samplefrequentie zodat ze ongeveer juist zijn.</span><span class="sxs-lookup"><span data-stu-id="4877b-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="4877b-200">**Bijwerken van uw project NuGet-pakketten** naar de meest recente *voorlopige versie* versie van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4877b-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="4877b-201">Met de rechtermuisknop op het project in Solution Explorer, kiest u NuGet-pakketten beheren controleren **Include prerelease** en zoek naar Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="4877b-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="4877b-202">**Uitschakelen van adaptieve steekproeven**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), verwijderen of uitcommentariëren de `AdaptiveSamplingTelemetryProcessor` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4877b-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="4877b-203">**De module vast tarief steekproeven inschakelen.**</span><span class="sxs-lookup"><span data-stu-id="4877b-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="4877b-204">Voeg dit codefragment aan [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="4877b-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="4877b-205">Kies een percentage dat bijna 100/N waarbij N staat voor een geheel getal voor het voorbeeldpercentage.</span><span class="sxs-lookup"><span data-stu-id="4877b-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="4877b-206">Momenteel wordt biedt geen ondersteuning voor andere waarden.</span><span class="sxs-lookup"><span data-stu-id="4877b-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="4877b-207">Alternatief: vast tarief steekproeven in uw servercode inschakelen</span><span class="sxs-lookup"><span data-stu-id="4877b-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="4877b-208">In plaats van de parameter steekproeven instellen in het .config-bestand, kunt u code.</span><span class="sxs-lookup"><span data-stu-id="4877b-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="4877b-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="4877b-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="4877b-210">([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="4877b-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="4877b-211">Het gebruik van steekproeven?</span><span class="sxs-lookup"><span data-stu-id="4877b-211">When to use sampling?</span></span>
<span data-ttu-id="4877b-212">Adaptieve steekproeven wordt automatisch ingeschakeld als u de ASP.NET-SDK-versie 2.0.0-beta3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4877b-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="4877b-213">Ongeacht welke SDK versie die u gebruikt, kunt u opname steekproeven (op onze server).</span><span class="sxs-lookup"><span data-stu-id="4877b-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="4877b-214">U hoeft niet steekproeven voor de meeste grootte voor kleine en middelgrote toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4877b-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="4877b-215">De nuttigste diagnostische gegevens en de meest nauwkeurige statistieken worden verkregen door het verzamelen van gegevens op alle activiteiten van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4877b-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="4877b-216">De belangrijkste voordelen van steekproeven zijn:</span><span class="sxs-lookup"><span data-stu-id="4877b-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="4877b-217">Application Insights-service verwijdert ('vertragingen') gegevenspunten wanneer uw app verzendt een zeer hoge frequentie van telemetrie in korte tijd interval.</span><span class="sxs-lookup"><span data-stu-id="4877b-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="4877b-218">Om te behouden in de [quotum](app-insights-pricing.md) van gegevenspunten voor uw prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="4877b-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="4877b-219">Om netwerkverkeer te beperken van de verzameling van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4877b-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="4877b-220">Welk type steekproeven moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="4877b-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="4877b-221">**Gebruik de opname steekproef nemen als:**</span><span class="sxs-lookup"><span data-stu-id="4877b-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="4877b-222">U doorlopen uw maandelijkse quotum telemetrie vaak.</span><span class="sxs-lookup"><span data-stu-id="4877b-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="4877b-223">U gebruikt een versie van de SDK die biedt geen ondersteuning voor sampling - bijvoorbeeld, de Java SDK of ASP.NET-versies ouder is dan 2.</span><span class="sxs-lookup"><span data-stu-id="4877b-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="4877b-224">U krijgt een groot aantal telemetrie van uw gebruikers webbrowsers.</span><span class="sxs-lookup"><span data-stu-id="4877b-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="4877b-225">**Gebruik vast tarief steekproef nemen als:**</span><span class="sxs-lookup"><span data-stu-id="4877b-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="4877b-226">U gebruikt de Application Insights-SDK voor ASP.NET-web-services versie 2.0.0 of hoger, en</span><span class="sxs-lookup"><span data-stu-id="4877b-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="4877b-227">U wilt dat gesynchroniseerde meting tussen client en server, zodat, wanneer u gebeurtenissen in onderzoeken [Search](app-insights-diagnostic-search.md), kunt u navigeren tussen gerelateerde gebeurtenissen op de client en server, zoals paginaweergaven en http-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4877b-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="4877b-228">Bent u er zeker van zijn van het juiste voorbeeldpercentage voor uw app.</span><span class="sxs-lookup"><span data-stu-id="4877b-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="4877b-229">Moet hoog genoeg zijn voor het verkrijgen van nauwkeurige meetgegevens, maar lager dan de frequentie die overschrijdt het quotum voor uw prijscategorie en de bandbreedteregeling limieten.</span><span class="sxs-lookup"><span data-stu-id="4877b-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="4877b-230">**Gebruik adaptieve steekproeven:**</span><span class="sxs-lookup"><span data-stu-id="4877b-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="4877b-231">Anders wordt aangeraden adaptieve steekproeven.</span><span class="sxs-lookup"><span data-stu-id="4877b-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="4877b-232">Dit is standaard ingeschakeld in de ASP.NET-server SDK-versie 2.0.0-beta3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4877b-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="4877b-233">Het verminderen niet het verkeer totdat een bepaalde minimale frequentie, zodat dit geen invloed op een site intensief wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4877b-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="4877b-234">Hoe weet ik of steekproeven uitgevoerd wordt?</span><span class="sxs-lookup"><span data-stu-id="4877b-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="4877b-235">Voor het detecteren van de werkelijke samplefrequentie ongeacht waar deze is toegepast, gebruikt u een [Analytics query](app-insights-analytics.md) zoals deze:</span><span class="sxs-lookup"><span data-stu-id="4877b-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="4877b-236">In elk bewaard record, `itemCount` geeft het aantal oorspronkelijke records die deze vertegenwoordigt, gelijk zijn aan 1 + het aantal eerdere verwijderde records.</span><span class="sxs-lookup"><span data-stu-id="4877b-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="4877b-237">Hoe werkt steekproeven?</span><span class="sxs-lookup"><span data-stu-id="4877b-237">How does sampling work?</span></span>
<span data-ttu-id="4877b-238">Vaste snelheid en adaptieve steekproeven zijn een functie van de SDK in ASP.NET-versies van 2.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="4877b-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="4877b-239">Opname steekproeven is een functie van de Application Insights-service en kan zich in de bewerking als de SDK niet steekproeven uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4877b-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="4877b-240">Het algoritme steekproeven besluit welke telemetrie-items verwijderen en welke u wilt behouden (ongeacht of deze in de SDK of in de Application Insights-service is).</span><span class="sxs-lookup"><span data-stu-id="4877b-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="4877b-241">De beslissing steekproeven is gebaseerd op verschillende regels die richt u op alle verwante gegevenspunten intact onderhouden van een diagnostische ervaring in Application Insights die actie worden uitgevoerd en betrouwbare zelfs met een beperkte set gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="4877b-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="4877b-242">Bijvoorbeeld, als voor een mislukte aanvraag verzendt uw app aanvullende telemetrie-items (zoals uitzondering en traceringen van deze aanvraag wordt vastgelegd), steekproeven niet gesplitst deze aanvraag en andere telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4877b-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="4877b-243">Het behouden of ze elkaar zakt.</span><span class="sxs-lookup"><span data-stu-id="4877b-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="4877b-244">Wanneer u de aanvraagdetails van de in Application Insights bekijkt, kunt u als gevolg hiervan altijd de aanvraag samen met de bijbehorende telemetrie-items zien.</span><span class="sxs-lookup"><span data-stu-id="4877b-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="4877b-245">Voor toepassingen die definiëren 'gebruiker' (dat wil zeggen, meest voorkomende webtoepassingen), de beschikking steekproeven is gebaseerd op de hash van de gebruikers-id, wat betekent dat alle telemetrie voor een bepaalde gebruiker wordt behouden of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4877b-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="4877b-246">De beslissing steekproeven is voor de typen toepassingen die geen gebruikers (zoals web-services) opgeven op basis van de bewerkings-id van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4877b-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="4877b-247">Ten slotte voor de telemetrie-items waarvoor geen gebruiker noch bewerking-id ingesteld (voor voorbeeld telemetrie-items is gerapporteerd door asynchrone threads met geen http-context) bevat steekproeven gewoon een percentage van de telemetrie-items van elk type.</span><span class="sxs-lookup"><span data-stu-id="4877b-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="4877b-248">Bij het weergeven van telemetrie naar u terug, past de Application Insights-service de metrische gegevens die door de dezelfde voorbeeldpercentage die is gebruikt op het moment van verzameling, om te compenseren voor de ontbrekende gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="4877b-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="4877b-249">Daarom bij het onderzoeken van de telemetrie in Application Insights, zien de gebruikers statistisch correcte benaderingen die heel dicht bij de reële getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="4877b-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="4877b-250">De nauwkeurigheid van de aanpassing is grotendeels afhankelijk van het geconfigureerde voorbeeldpercentage.</span><span class="sxs-lookup"><span data-stu-id="4877b-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="4877b-251">De nauwkeurigheid verhoogt ook, voor toepassingen die een groot aantal in het algemeen soortgelijke aanvragen van een groot aantal gebruikers verwerken.</span><span class="sxs-lookup"><span data-stu-id="4877b-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="4877b-252">Aan de andere kant voor toepassingen die niet met een aanzienlijke belasting werken is steekproeven niet nodig als u deze toepassingen kunnen doorgaans alle hun telemetrie verzenden bijwerkt binnen het quotum zonder verlies van gegevens van de beperking.</span><span class="sxs-lookup"><span data-stu-id="4877b-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="4877b-253">Houd er rekening mee dat Application Insights biedt geen telemetrie-typen, metrische gegevens en sessies, sinds het voorbeeld voor deze typen, vermindering van de precisie mag maximaal ongewenste.</span><span class="sxs-lookup"><span data-stu-id="4877b-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="4877b-254">Adaptieve steekproeven</span><span class="sxs-lookup"><span data-stu-id="4877b-254">Adaptive sampling</span></span>
<span data-ttu-id="4877b-255">Adaptieve steekproeven wordt toegevoegd een component die wordt bewaakt de huidige frequentie van de overdracht van de SDK en past u het voorbeeldpercentage om te blijven binnen de maximale snelheid doel.</span><span class="sxs-lookup"><span data-stu-id="4877b-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="4877b-256">De aanpassing is berekend met regelmatige tussenpozen en is gebaseerd op een zwevend gemiddelde van de uitgaande verzending snelheid.</span><span class="sxs-lookup"><span data-stu-id="4877b-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="4877b-257">Steekproeven en de JavaScript-SDK</span><span class="sxs-lookup"><span data-stu-id="4877b-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="4877b-258">De client (JavaScript) SDK deelneemt aan vast tarief steekproeven in combinatie met de SDK-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="4877b-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="4877b-259">De providers's verzendt alleen clientzijde telemetrie uit dezelfde gebruikers waarvoor het include-bestand de beslissing genomen om te 'voorbeeld in'.</span><span class="sxs-lookup"><span data-stu-id="4877b-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="4877b-260">Deze logica is ontworpen om de integriteit van de gebruikerssessie onderhouden tussen de client - en server-zijde.</span><span class="sxs-lookup"><span data-stu-id="4877b-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="4877b-261">Als gevolg hiervan op een bepaalde telemetrie-item in de Application Insights kunt u alle overige telemetrie-items voor deze gebruiker of de sessie vinden.</span><span class="sxs-lookup"><span data-stu-id="4877b-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="4877b-262">*Client- en serverzijde telemetrie weergeven niet gecoördineerde voorbeelden zoals hierboven worden beschreven.*</span><span class="sxs-lookup"><span data-stu-id="4877b-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="4877b-263">Controleer of u vast aantal steekproeven op server en client ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4877b-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="4877b-264">Zorg ervoor dat de SDK-versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4877b-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="4877b-265">Controleer of u de dezelfde voorbeeldpercentage ingesteld in de client en de server.</span><span class="sxs-lookup"><span data-stu-id="4877b-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="4877b-266">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="4877b-266">Frequently Asked Questions</span></span>
<span data-ttu-id="4877b-267">*Waarom wordt niet wordt een eenvoudige 'verzamelen X procent van elk type telemetrie'?*</span><span class="sxs-lookup"><span data-stu-id="4877b-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="4877b-268">Terwijl deze benadering steekproeven met een zeer hoge precisie in metrische benaderingen opgeven wilt, zou het correleren van diagnostische gegevens per gebruiker, sessie en verzoek, wat van essentieel belang voor diagnostische gegevens kunnen worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="4877b-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="4877b-269">Steekproef werkt daarom beter met "verzamelen alle telemetrie-items voor X procent van de app-gebruikers" of 'verzamelen alle telemetrie voor X percentage aanvragen dat app' logica.</span><span class="sxs-lookup"><span data-stu-id="4877b-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="4877b-270">Voor de telemetrie-items niet zijn gekoppeld aan de verzoeken (zoals achtergrond asynchrone verwerking), is het de terugvallen te "verzamelen X percentage van alle items voor elk type telemetrie."</span><span class="sxs-lookup"><span data-stu-id="4877b-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="4877b-271">*Kan het voorbeeldpercentage na verloop van tijd wijzigen?*</span><span class="sxs-lookup"><span data-stu-id="4877b-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="4877b-272">Ja, verandert adaptieve steekproeven geleidelijk het voorbeeldpercentage op basis van de momenteel waargenomen volume van de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4877b-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="4877b-273">*Als ik vast tarief steekproeven gebruikt, hoe weet ik welke steekproeven percentage werkt het meest geschikt voor mijn app?*</span><span class="sxs-lookup"><span data-stu-id="4877b-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="4877b-274">Een manier worden gestart met adaptieve steekproeven, uitzoeken wat waardering geven vereffent op (Zie de bovenstaande vraag) en ga vervolgens naar vast tarief voert sampling uit met behulp van dit percentage.</span><span class="sxs-lookup"><span data-stu-id="4877b-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="4877b-275">U hebt anders te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="4877b-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="4877b-276">Het gebruik van uw huidige telemetrie in AI analyseren, observeren beperking die zich voordoet en schatting maken van het volume van de verzamelde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4877b-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="4877b-277">Deze drie invoer, samen met de geselecteerde prijscategorie voorgesteld hoeveel kunt u het volume van de verzamelde telemetrie verminderen.</span><span class="sxs-lookup"><span data-stu-id="4877b-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="4877b-278">Echter, een toename van het nummer van uw gebruikers- of enige andere verschuiving van het volume van telemetrie mogelijk uw schatting ongeldig.</span><span class="sxs-lookup"><span data-stu-id="4877b-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="4877b-279">*Wat gebeurt er als ik voorbeeldpercentage te laag configureren?*</span><span class="sxs-lookup"><span data-stu-id="4877b-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="4877b-280">Uitzonderlijk lage voorbeeldpercentage (over-aggressive steekproeven) vermindert de nauwkeurigheid van de benaderingen, wanneer Application Insights probeert om te compenseren de visualisatie van de gegevens voor het volume gegevens verminderen.</span><span class="sxs-lookup"><span data-stu-id="4877b-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="4877b-281">Ook diagnostische ervaring mogelijk negatieve gevolgen hebben, zoals enkele van de aanvragen zelden beschadigde of traag mogen voorbeelden worden gemaakt uit.</span><span class="sxs-lookup"><span data-stu-id="4877b-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="4877b-282">*Wat gebeurt er als ik voorbeeldpercentage te hoog configureren?*</span><span class="sxs-lookup"><span data-stu-id="4877b-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="4877b-283">Configureren (niet agressief genoeg) te hoog voorbeeldpercentage resulteert in een onvoldoende vermindering van het volume van de verzamelde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4877b-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="4877b-284">Telemetrie gegevensverlies gerelateerd aan de beperking kunnen nog steeds optreden en de kosten van het gebruik van Application Insights is mogelijk hoger is dan u geplande vanwege overschrijding kosten.</span><span class="sxs-lookup"><span data-stu-id="4877b-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="4877b-285">*Op welke platforms kan ik steekproeven gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="4877b-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="4877b-286">Opname steekproeven kan automatisch voor alle telemetrie boven een bepaald volume optreden als de SDK niet bezig is met steekproeven.</span><span class="sxs-lookup"><span data-stu-id="4877b-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="4877b-287">Dit zou bijvoorbeeld werken als uw app gebruikmaakt van een Java-server, of als u een oudere versie van de ASP.NET-SDK.</span><span class="sxs-lookup"><span data-stu-id="4877b-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="4877b-288">Als u ASP.NET-SDK-versies 2.0.0 en hoger (gehost in Azure of een eigen server), krijgt u adaptieve steekproef nemen standaard, maar u kunt overschakelen naar vast tarief zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="4877b-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="4877b-289">Met vast tarief steekproeven, de browser SDK worden automatisch gesynchroniseerd voor een steekproef van gerelateerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="4877b-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="4877b-290">*Er zijn bepaalde zeldzame gebeurtenissen die ik altijd wilt zien. Hoe krijg ik ze voorbij de module steekproeven?*</span><span class="sxs-lookup"><span data-stu-id="4877b-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="4877b-291">Initialiseren van een afzonderlijk exemplaar van TelemetryClient met een nieuwe TelemetryConfiguration (niet de standaard actief).</span><span class="sxs-lookup"><span data-stu-id="4877b-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="4877b-292">Gebruikt u dat uw zeldzame gebeurtenissen verzendt.</span><span class="sxs-lookup"><span data-stu-id="4877b-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4877b-293">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4877b-293">Next steps</span></span>
* <span data-ttu-id="4877b-294">[Filteren](app-insights-api-filtering-sampling.md) krijgt u meer strikte controle over wat uw SDK verzendt.</span><span class="sxs-lookup"><span data-stu-id="4877b-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

