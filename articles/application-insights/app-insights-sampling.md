---
title: aaaTelemetry steekproeven in Azure Application Insights | Microsoft Docs
description: Hoe Hallo tookeep volume telemetrie onder controle.
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="cc4fb-103">Steekproeven in Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc4fb-103">Sampling in Application Insights</span></span>


<span data-ttu-id="cc4fb-104">Steekproeven is een functie in [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="cc4fb-105">Is Hallo aanbevolen manier tooreduce telemetrie verkeer en opslag, met behoud van een statistisch correcte analyse van toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="cc4fb-106">Hallo filter selecteert items die zijn gerelateerd, zodat u tussen items navigeren kunt als u de diagnostische onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="cc4fb-107">Wanneer metrische aantallen worden tooyou op Hallo portal worden weergegeven, zijn ze renormalized tootake account Hallo steekproef nemen toominimize een effect op Hallo statistieken.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="cc4fb-108">Steekproeven verlaagt de kosten van verkeer en gegevens en kunt u voorkomen beperking.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="cc4fb-109">Kort gezegd:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-109">In brief:</span></span>
* <span data-ttu-id="cc4fb-110">Steekproeven behoudt 1 in  *n*  Hallo rest wordt teruggezet en registreert.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="cc4fb-111">Het kan bijvoorbeeld een samplefrequentie van 20% 1: 5 gebeurtenissen behouden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="cc4fb-112">Steekproeven gebeurt automatisch als uw toepassing veel telemetrie, in ASP.NET web server-apps verzendt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="cc4fb-113">U kunt ook instellen dat wordt handmatig, hetzij in Hallo portal op Hallo prijzen pagina. of in Hallo ASP.NET-SDK in Hallo .config-bestand, tooalso Hallo netwerkverkeer te verminderen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="cc4fb-114">Als u aangepaste gebeurtenissen en u ervoor wilt dat een verzameling van gebeurtenissen wordt behouden of verwijderd samen toomake, ervoor zorgen dat ze dezelfde OperationId waarde hebben Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="cc4fb-115">Hallo steekproeven deler  *n*  wordt gerapporteerd in elke record in de eigenschap Hallo `itemCount`, die in de zoekopdracht wordt weergegeven onder Hallo beschrijvende naam 'aanvraag aantal' of 'gebeurtenis aantal'.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="cc4fb-116">Wanneer steekproeven niet uitgevoerd is, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="cc4fb-117">Als u analysequery's schrijft, moet u [rekening houden met steekproeven](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="cc4fb-118">In het bijzonder in plaats van gewoon telling registreert, moet u `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="cc4fb-119">Typen steekproeven</span><span class="sxs-lookup"><span data-stu-id="cc4fb-119">Types of sampling</span></span>
<span data-ttu-id="cc4fb-120">Er zijn drie steekproeven van alternatieve methoden:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="cc4fb-121">**Adaptieve steekproeven** automatisch wordt aangepast volume Hallo van telemetrie vanaf Hallo SDK in uw ASP.NET-app verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="cc4fb-122">De standaardinstelling van SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="cc4fb-123">Momenteel beschikbaar voor ASP.NET-serverzijde telemetrie alleen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="cc4fb-124">**Vast aantal steekproeven** vermindert Hallo volume telemetrie verzonden van zowel uw ASP.NET-server en de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="cc4fb-125">U instellen Hallo frequentie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-125">You set hello rate.</span></span> <span data-ttu-id="cc4fb-126">Hallo-client en server synchroniseert de steekproeven zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="cc4fb-127">**Opname steekproeven** werkt in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="cc4fb-128">Het aantal Hallo telemetrie van uw app, met een frequentie die u instelt binnenkomt wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="cc4fb-129">Niet verminderen het verkeer van telemetrie, maar u kunt houden binnen uw maandelijkse quotum.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="cc4fb-130">Hallo groot voordeel van opname steekproeven is dat u dit instellen kunt zonder dat uw app en het op uniforme wijze voor alle servers en clients werkt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="cc4fb-131">Als Adaptief of vast aantal steekproeven in bewerking, is opname steekproeven uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="cc4fb-132">Opname steekproeven</span><span class="sxs-lookup"><span data-stu-id="cc4fb-132">Ingestion sampling</span></span>
<span data-ttu-id="cc4fb-133">Deze vorm van steekproeven werkt op Hallo punt waar Hallo telemetrie van uw webserver, browsers en apparaten Hallo Application Insights-service-eindpunt is bereikt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="cc4fb-134">Hoewel het Hallo telemetrie verkeer dat wordt verzonden vanuit uw app niet verkleinen, vermindert het Hallo bedrag verwerkt en bewaard (en in rekening gebracht voor) door Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="cc4fb-135">Gebruik dit type steekproeven als uw app vaak via het maandelijkse quotum wordt en er geen Hallo-optie van het gebruik van Hallo SDK gebaseerde typen steekproeven.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="cc4fb-136">Hallo samplefrequentie in Hallo quota's en prijzen blade instellen:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Hallo toepassing overzicht blade, klik op instellingen, Quota, voorbeelden, en vervolgens een samplefrequentie selecteren en klik op bijwerken.](./media/app-insights-sampling/04.png)

<span data-ttu-id="cc4fb-138">Net als andere soorten steekproeven behoudt Hallo algoritme gerelateerde telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="cc4fb-139">Bijvoorbeeld, wanneer u Hallo telemetrie in de zoekopdracht te bekijken bent, u hebt mogelijk toofind Hallo aanvraag gerelateerde tooa bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="cc4fb-140">Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering correct blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="cc4fb-141">Gegevenspunten die zijn verwijderd door steekproeven zijn niet beschikbaar in de Application Insights-functies, zoals [continue Export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="cc4fb-142">Opname steekproeven functioneren niet terwijl er op basis van SDK adaptieve of vast aantal steekproeven wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="cc4fb-143">Als de samplefrequentie Hallo op Hallo SDK is minder dan 100%, wordt vervolgens hello opname samplefrequentie die u instelt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="cc4fb-144">Hallo-waarde die wordt weergegeven op de tegel Hallo geeft Hallo-waarde die u voor opname steekproeven instelt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="cc4fb-145">Het vertegenwoordigen niet Hallo werkelijke samplefrequentie als SDK steekproeven uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="cc4fb-146">Adaptieve steekproeven op uw webserver</span><span class="sxs-lookup"><span data-stu-id="cc4fb-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="cc4fb-147">Adaptieve steekproeven is beschikbaar voor Hallo Application Insights-SDK voor ASP.NET v 2.0.0-beta3 of hoger, en is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="cc4fb-148">Adaptieve steekproeven is van invloed op Hallo volume telemetrie van uw web server app toohello Application Insights-service is verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="cc4fb-149">Hallo volume automatisch wordt aangepast tookeep binnen de opgegeven maximale overdrachtssnelheid van verkeer.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="cc4fb-150">Deze werkt niet op lage volumes telemetrie, dus een app in foutopsporing of een website met geringe gebruiksduur, worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="cc4fb-151">tooachieve hello doelvolume, aantal Hallo telemetrie die is gegenereerd, wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="cc4fb-152">Maar net als andere soorten steekproeven behoudt Hallo algoritme gerelateerde telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="cc4fb-153">Bijvoorbeeld, wanneer u Hallo telemetrie in de zoekopdracht te bekijken bent, u hebt mogelijk toofind Hallo aanvraag gerelateerde tooa bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="cc4fb-154">Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering zich gecorrigeerde toocompensate voor Hallo steekproef nemen frequentie, zodat ze ongeveer juiste waarden in de metriek Explorer tonen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="cc4fb-155">**Bijwerken van uw project NuGet** toohello nieuwste pakketten *voorlopige versie* versie van Application Insights: Hallo-project in Solution Explorer met de rechtermuisknop, kies NuGet-pakketten beheren controleren **opnemen voorlopige** en zoek naar Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="cc4fb-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), kunt u verschillende parameters in Hallo `AdaptiveSamplingTelemetryProcessor` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="cc4fb-157">Hallo cijfers zijn Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="cc4fb-158">Hallo doel snelheid waarmee Hallo adaptieve algoritme is erop gericht voor **op elke server-host**.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="cc4fb-159">Als uw web-app wordt uitgevoerd op veel hosts, verminderen door deze waarde dus als tooremain binnen de snelheid van uw doel van het verkeer op Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="cc4fb-160">Hallo-interval op welke Hallo huidige frequentie van telemetrie opnieuw geëvalueerd is.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="cc4fb-161">Evaluatie wordt uitgevoerd als een zwevend gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="cc4fb-162">U kunt de tooshorten dit interval als uw telemetrie aansprakelijk toosudden bursts.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="cc4fb-163">Als u steekproeven percentage waarde, hoe snel nadat er worden wijzigingen aangebracht mogen we toolower percentage opnieuw wordt toocapture minder gegevens.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="cc4fb-164">Als er steekproeven percentage waarde wijzigingen, hoe snel nadat we toegestaan tooincrease percentage opnieuw wordt toocapture meer gegevens.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="cc4fb-165">Als percentage steekproef varieert, wat is de minimale waarde Hallo we tooset zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="cc4fb-166">Als percentage steekproef varieert, wat is de maximumwaarde Hallo we tooset zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="cc4fb-167">In de berekening Hallo Hallo zwevend gemiddelde toegewezen Hallo gewicht toohello meest recente waarde.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="cc4fb-168">Gebruik een waarde gelijk tooor kleiner is dan 1.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="cc4fb-169">Lagere waarden worden Hallo algoritme op minder reactieve toosudden wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="cc4fb-170">Hallo waarde toegewezen wanneer Hallo app NET is gestart.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="cc4fb-171">Niet verlaagt dit terwijl u fouten opspoort.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="cc4fb-172">Puntkomma's gescheiden lijst van typen die u niet dat door actieve toobe wilt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="cc4fb-173">Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="cc4fb-174">Alle exemplaren van Hallo opgegeven typen worden verzonden; Hallo-typen die niet zijn opgegeven, worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="cc4fb-175">Puntkomma's gescheiden lijst van typen die u wilt dat door actieve toobe.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="cc4fb-176">Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="cc4fb-177">Hallo opgegeven typen steekproeven worden genomen; alle exemplaren van Hallo de andere typen altijd worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="cc4fb-178">**tooswitch uit** adaptieve steekproeven, verwijder Hallo AdaptiveSamplingTelemetryProcessor knooppunt uit applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="cc4fb-179">Alternatief: adaptieve steekproeven in code configureren</span><span class="sxs-lookup"><span data-stu-id="cc4fb-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="cc4fb-180">In plaats van steekproeven in Hallo .config-bestand aanpassen, kunt u code.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="cc4fb-181">Hiermee kunt u toospecify een callbackfunctie die wordt aangeroepen wanneer de samplefrequentie Hallo opnieuw geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="cc4fb-182">U kunt dit gebruiken, bijvoorbeeld toofind uit welke samplefrequentie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="cc4fb-183">Hallo verwijderen `AdaptiveSamplingTelemetryProcessor` knooppunt uit Hallo .config-bestand.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="cc4fb-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="cc4fb-185">([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="cc4fb-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="cc4fb-186">Steekproef voor webpagina's met JavaScript</span><span class="sxs-lookup"><span data-stu-id="cc4fb-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="cc4fb-187">U kunt de webpagina's voor vast tarief steekproeven vanaf een willekeurige server configureren.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="cc4fb-188">Wanneer u [Hallo webpagina's configureren voor Application Insights](app-insights-javascript.md), Hallo codefragment die u via de Application Insights-portal Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="cc4fb-189">(In ASP.NET-apps Hallo codefragment doorgaans gaat in _Layout.cshtml.)  Voeg een regel zoals `samplingPercentage: 10,` voordat de instrumentatiesleutel Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="cc4fb-190">Voor voorbeeldpercentage hello, kiest u een percentage dat is sluiten too100/N, waarbij N een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="cc4fb-191">Momenteel wordt biedt geen ondersteuning voor andere waarden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="cc4fb-192">Als u tevens vast aantal steekproeven op Hallo server inschakelt, synchroniseren Hallo-clients en de server zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="cc4fb-193">Vast aantal steekproeven voor ASP.NET-websites</span><span class="sxs-lookup"><span data-stu-id="cc4fb-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="cc4fb-194">Vast tarief steekproeven vermindert Hallo verkeer dat wordt verzonden van uw webserver en webbrowsers.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="cc4fb-195">In tegenstelling tot adaptieve steekproeven wordt telemetrie tegen een vast tarief dat u hebt besloten gereduceerd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="cc4fb-196">Het ook synchroniseert Hallo-client en server steekproeven zodat verwante items worden bewaard - bijvoorbeeld, zodat als u de weergave van een pagina in de zoekopdracht bekijkt, kunt u de gerelateerde aanvraag vinden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="cc4fb-197">Hallo steekproeven algoritme behoudt verwante items.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="cc4fb-198">Voor elke aanvraag HTTP-worden gebeurtenissen, deze en gerelateerde gebeurtenissen genegeerd of verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="cc4fb-199">In Metrics Explorer tarieven zoals het aantal aanvragen en uitzonderingen vermenigvuldigd met een factor toocompensate voor Hallo samplefrequentie, zodat ze ongeveer juist zijn.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="cc4fb-200">**Bijwerken van uw project NuGet-pakketten** toohello nieuwste *voorlopige versie* versie van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="cc4fb-201">Hallo-project in Solution Explorer met de rechtermuisknop, kies NuGet-pakketten beheren controleren **Include prerelease** en zoek naar Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="cc4fb-202">**Uitschakelen van adaptieve steekproeven**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), verwijderen of uitcommentariëren hello `AdaptiveSamplingTelemetryProcessor` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="cc4fb-203">**Hallo vast tarief steekproeven module inschakelen.**</span><span class="sxs-lookup"><span data-stu-id="cc4fb-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="cc4fb-204">In dit fragment te toevoegen[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="cc4fb-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="cc4fb-205">Voor voorbeeldpercentage hello, kiest u een percentage dat is sluiten too100/N, waarbij N een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="cc4fb-206">Momenteel wordt biedt geen ondersteuning voor andere waarden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="cc4fb-207">Alternatief: vast tarief steekproeven in uw servercode inschakelen</span><span class="sxs-lookup"><span data-stu-id="cc4fb-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="cc4fb-208">In plaats van u Hallo steekproeven parameter in Hallo .config-bestand instelt, kunt u code.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="cc4fb-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-209">*C#*</span></span>

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

<span data-ttu-id="cc4fb-210">([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="cc4fb-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="cc4fb-211">Wanneer toouse steekproeven?</span><span class="sxs-lookup"><span data-stu-id="cc4fb-211">When toouse sampling?</span></span>
<span data-ttu-id="cc4fb-212">Adaptieve steekproeven wordt automatisch ingeschakeld als u Hallo ASP.NET-SDK-versie 2.0.0-beta3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="cc4fb-213">Ongeacht welke SDK versie die u gebruikt, kunt u opname steekproeven (op onze server).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="cc4fb-214">U hoeft niet steekproeven voor de meeste grootte voor kleine en middelgrote toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="cc4fb-215">Hallo nuttigst diagnostische gegevens en de meest nauwkeurige statistieken worden verkregen door het verzamelen van gegevens op alle activiteiten van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="cc4fb-216">belangrijkste voordelen van steekproeven Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="cc4fb-217">Application Insights-service verwijdert ('vertragingen') gegevenspunten wanneer uw app verzendt een zeer hoge frequentie van telemetrie in korte tijd interval.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="cc4fb-218">tookeep binnen Hallo [quotum](app-insights-pricing.md) van gegevenspunten voor uw prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="cc4fb-219">netwerkverkeer tooreduce van Hallo-verzameling van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="cc4fb-220">Welk type steekproeven moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="cc4fb-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="cc4fb-221">**Gebruik de opname steekproef nemen als:**</span><span class="sxs-lookup"><span data-stu-id="cc4fb-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="cc4fb-222">U doorlopen uw maandelijkse quotum telemetrie vaak.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="cc4fb-223">U gebruikt een versie van het Hallo-SDK die biedt geen ondersteuning voor sampling - voorbeeld, Hallo Java SDK of ASP.NET-versies ouder is dan 2.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="cc4fb-224">U krijgt een groot aantal telemetrie van uw gebruikers webbrowsers.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="cc4fb-225">**Gebruik vast tarief steekproef nemen als:**</span><span class="sxs-lookup"><span data-stu-id="cc4fb-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="cc4fb-226">U Hallo Application Insights-SDK voor ASP.NET-web-services versie 2.0.0 of hoger, en</span><span class="sxs-lookup"><span data-stu-id="cc4fb-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="cc4fb-227">U wilt dat gesynchroniseerde meting tussen client en server, zodat, wanneer u gebeurtenissen in onderzoeken [Search](app-insights-diagnostic-search.md), kunt u navigeren tussen gerelateerde gebeurtenissen op Hallo-client en server, zoals paginaweergaven en http-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="cc4fb-228">Bent u er zeker van zijn van de juiste voorbeeldpercentage Hallo voor uw app.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="cc4fb-229">Het moet hoog genoeg tooget nauwkeurige meetgegevens, maar hieronder Hallo snelheid waarmee uw prijscategorie quotum wordt overschreden en Hallo beperking limieten.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="cc4fb-230">**Gebruik adaptieve steekproeven:**</span><span class="sxs-lookup"><span data-stu-id="cc4fb-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="cc4fb-231">Anders wordt aangeraden adaptieve steekproeven.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="cc4fb-232">Dit is standaard ingeschakeld in Hallo ASP.NET server SDK-versie 2.0.0-beta3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="cc4fb-233">Het verminderen niet het verkeer totdat een bepaalde minimale frequentie, zodat dit geen invloed op een site intensief wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="cc4fb-234">Hoe weet ik of steekproeven uitgevoerd wordt?</span><span class="sxs-lookup"><span data-stu-id="cc4fb-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="cc4fb-235">toodiscover hello werkelijke snelheid ongeacht waar deze zijn toegepast, wordt gebruikt een [Analytics query](app-insights-analytics.md) zoals deze:</span><span class="sxs-lookup"><span data-stu-id="cc4fb-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="cc4fb-236">In elk bewaard record, `itemCount` geeft het aantal oorspronkelijke records die deze vertegenwoordigt, gelijk too1 + aantal eerdere verwijderde records Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="cc4fb-237">Hoe werkt steekproeven?</span><span class="sxs-lookup"><span data-stu-id="cc4fb-237">How does sampling work?</span></span>
<span data-ttu-id="cc4fb-238">Vaste snelheid en adaptieve steekproeven zijn een functie van Hallo SDK in ASP.NET-versies van 2.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="cc4fb-239">Opname steekproeven is een functie van Hallo Application Insights-service en kan zich in de bewerking als Hallo SDK steekproeven niet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="cc4fb-240">Hallo steekproeven algoritme besluit welke toodrop telemetrie-items en welke tookeep zijn (of het is in Hallo SDK of Hallo Application Insights-service).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="cc4fb-241">Hallo steekproeven beslissing is gebaseerd op verschillende regels die gericht toopreserve alle gerelateerde gegevenspunten intact onderhouden van een diagnostische ervaring in Application Insights die actie worden uitgevoerd en betrouwbare zelfs met een beperkte set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="cc4fb-242">Bijvoorbeeld, als voor een mislukte aanvraag verzendt uw app aanvullende telemetrie-items (zoals uitzondering en traceringen van deze aanvraag wordt vastgelegd), steekproeven niet gesplitst deze aanvraag en andere telemetrie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="cc4fb-243">Het behouden of ze elkaar zakt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="cc4fb-244">Wanneer u gegevens voor de aanvraag in Application Insights Hallo bekijkt, kunt u als gevolg hiervan altijd Hallo aanvraag samen met de bijbehorende telemetrie-items zien.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="cc4fb-245">Voor toepassingen die definiëren 'gebruiker' (dat wil zeggen, meest voorkomende webtoepassingen), Hallo steekproeven beslissing is gebaseerd op Hallo hash van de gebruikers-id hello, wat betekent dat alle telemetrie voor een bepaalde gebruiker wordt behouden of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="cc4fb-246">Voor Hallo typen toepassingen die geen gebruikers (zoals web-services) opgeven is Hallo steekproeven beslissing gebaseerd op Hallo bewerkings-id van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="cc4fb-247">Ten slotte voor Hallo telemetrie-items waarvoor geen gebruiker noch bewerking-id ingesteld (voor voorbeeld telemetrie-items is gerapporteerd door asynchrone threads met geen http-context) bevat steekproeven gewoon een percentage van de telemetrie-items van elk type.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="cc4fb-248">Bij het weergeven van telemetrie back tooyou Hallo Hallo Application Insights-service wordt aangepast Hallo metrische gegevens door dezelfde voorbeeldpercentage die is gebruikt tijdens het Hallo van verzameling, toocompensate voor Hallo ontbrekende gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="cc4fb-249">Daarom wanneer bekijkt hello telemetrie in Application Insights, zien Hallo gebruikers statistisch correcte benaderingen die zich dicht toohello real getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="cc4fb-250">Hallo nauwkeurig Hallo aanpassing is grotendeels afhankelijk van voorbeeldpercentage Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="cc4fb-251">Hallo nauwkeurigheid verhoogt ook, voor toepassingen die een groot aantal in het algemeen soortgelijke aanvragen van een groot aantal gebruikers verwerken.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="cc4fb-252">Op Hallo daarentegen voor toepassingen die niet met een aanzienlijke belasting werken, steekproeven is niet nodig als u deze toepassingen kunnen doorgaans alle hun telemetrie verzenden bijwerkt binnen quota hello, zonder verlies van gegevens van de beperking.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="cc4fb-253">Houd er rekening mee dat Application Insights biedt geen telemetrie-typen, metrische gegevens en sessies, sinds het voorbeeld voor deze typen, verminderde Hallo precisie mag maximaal ongewenste.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="cc4fb-254">Adaptieve steekproeven</span><span class="sxs-lookup"><span data-stu-id="cc4fb-254">Adaptive sampling</span></span>
<span data-ttu-id="cc4fb-255">Adaptieve steekproeven voegt een onderdeel dat monitors Hallo huidige snelheid van de verzending van Hallo SDK en aangepast Hallo steekproeven percentage tootry toostay binnen Hallo doel maximale snelheid.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="cc4fb-256">Hallo aanpassing is berekend met regelmatige tussenpozen en is gebaseerd op een zwevend gemiddelde Hallo uitgaande verzending snelheid.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="cc4fb-257">Steekproeven en Hallo JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="cc4fb-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="cc4fb-258">Hallo-clientzijde (JavaScript) SDK deelneemt aan vast tarief steekproeven in combinatie met Hallo serverzijde SDK.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="cc4fb-259">Hallo geïnstrumenteerd pagina's wordt alleen verzonden clientzijde telemetrie van Hallo dezelfde gebruikers voor welke Hallo serverzijde de beslissing genomen te 'steekproef in."</span><span class="sxs-lookup"><span data-stu-id="cc4fb-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="cc4fb-260">Deze logica is ontworpen toomaintain integriteit van de gebruikerssessie tussen de client - en server-zijde.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="cc4fb-261">Als gevolg hiervan op een bepaalde telemetrie-item in de Application Insights kunt u alle overige telemetrie-items voor deze gebruiker of de sessie vinden.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="cc4fb-262">*Client- en serverzijde telemetrie weergeven niet gecoördineerde voorbeelden zoals hierboven worden beschreven.*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="cc4fb-263">Controleer of u vast aantal steekproeven op server en client ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="cc4fb-264">Zorg ervoor dat Hallo SDK-versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="cc4fb-265">Controleer of u ingestelde Hallo dezelfde steekproef nemen percentage in zowel Hallo-client en server.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="cc4fb-266">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="cc4fb-266">Frequently Asked Questions</span></span>
<span data-ttu-id="cc4fb-267">*Waarom wordt niet wordt een eenvoudige 'verzamelen X procent van elk type telemetrie'?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="cc4fb-268">Terwijl deze benadering steekproeven met een zeer hoge precisie in metrische benaderingen opgeven wilt, zou deze mogelijkheid toocorrelate diagnostische gegevens per gebruiker, sessie en verzoek, wat van essentieel belang voor diagnostische gegevens worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="cc4fb-269">Steekproef werkt daarom beter met "verzamelen alle telemetrie-items voor X procent van de app-gebruikers" of 'verzamelen alle telemetrie voor X percentage aanvragen dat app' logica.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="cc4fb-270">Voor Hallo telemetrie-items niet zijn gekoppeld aan het Hallo-aanvragen (zoals achtergrond asynchrone verwerking), is Hallo vallen terug te 'verzamelen X percentage van alle items voor elk type telemetrie."</span><span class="sxs-lookup"><span data-stu-id="cc4fb-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="cc4fb-271">*Kan het voorbeeldpercentage Hallo na verloop van tijd wijzigen?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="cc4fb-272">Ja, adaptieve steekproef nemen geleidelijk Hallo voorbeeldpercentage, op basis van waargenomen momenteel volume Hallo telemetrie Hallo wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="cc4fb-273">*Als ik vast tarief steekproeven gebruikt, hoe weet ik welke steekproeven percentage werkt Hallo aanbevolen voor mijn app?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="cc4fb-274">Uitzoeken wat waardering geven betaalt op een manier is toostart met adaptieve steekproeven, (Zie Hallo hierboven vraag), en vervolgens switch toofixed rate-meting met behulp van dit percentage.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="cc4fb-275">Anders kunt u tooguess hebben.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="cc4fb-276">Het gebruik van uw huidige telemetrie in AI analyseren, ziet u een beperking die optreden en schatting Hallo volume Hallo verzameld telemetrie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cc4fb-277">Deze drie invoer, samen met de geselecteerde prijscategorie voorstellen die u mogelijk wilt tooreduce Hallo volume Hallo verzameld telemetrie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cc4fb-278">Echter, een toename van Hallo-nummer van uw gebruikers- of sommige andere shift in Hallo volume telemetrie mogelijk uw schatting ongeldig.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="cc4fb-279">*Wat gebeurt er als ik voorbeeldpercentage te laag configureren?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="cc4fb-280">Uitzonderlijk lage voorbeeldpercentage (over-aggressive steekproeven) vermindert Hallo nauwkeurig Hallo benaderingen, wanneer Application Insights toocompensate Hallo visualisatie van gegevens Hallo Hallo gegevens volume te beperken probeert.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="cc4fb-281">Ook diagnostische ervaring mogelijk negatieve gevolgen hebben, zoals sommigen Hallo zelden mislukt of trage aanvragen mogen voorbeelden worden gemaakt uit.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="cc4fb-282">*Wat gebeurt er als ik voorbeeldpercentage te hoog configureren?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="cc4fb-283">Configureren steekproeven te hoog percentage (geen agressieve genoeg) resultaten in een onvoldoende vermindering van volume Hallo Hallo verzameld telemetrie.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cc4fb-284">Telemetrie verlies van gegevens gerelateerd toothrottling en Hallo kosten van het gebruik van Application Insights kan niet hoger zijn dan u geplande einddatum toooverage kosten kunnen zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="cc4fb-285">*Op welke platforms kan ik steekproeven gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="cc4fb-286">Opname steekproeven kan automatisch voor alle telemetrie boven een bepaald volume optreden als Hallo SDK niet bezig is met steekproeven.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="cc4fb-287">Dit zou werkt, bijvoorbeeld, als uw app gebruikmaakt van een Java-server of als u een oudere versie van ASP.NET-SDK Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="cc4fb-288">Als u ASP.NET-SDK-versies 2.0.0 en hoger (gehost in Azure of een eigen server), krijgt u adaptieve steekproef nemen standaard, maar u kunt toofixed snelheid overschakelen zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="cc4fb-289">Met vast tarief steekproeven Hallo browser SDK worden automatisch gesynchroniseerd toosample gerelateerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="cc4fb-290">*Er zijn bepaalde zeldzame gebeurtenissen wilt altijd toosee. Hoe krijg ik ze uit het verleden Hallo steekproeven module?*</span><span class="sxs-lookup"><span data-stu-id="cc4fb-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="cc4fb-291">Initialiseren van een afzonderlijk exemplaar van TelemetryClient met een nieuwe TelemetryConfiguration (geen Hallo standaard actief).</span><span class="sxs-lookup"><span data-stu-id="cc4fb-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="cc4fb-292">Die toosend uw zeldzame gebeurtenissen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc4fb-293">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc4fb-293">Next steps</span></span>
* <span data-ttu-id="cc4fb-294">[Filteren](app-insights-api-filtering-sampling.md) krijgt u meer strikte controle over wat uw SDK verzendt.</span><span class="sxs-lookup"><span data-stu-id="cc4fb-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

