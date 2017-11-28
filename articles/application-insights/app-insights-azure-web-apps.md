---
title: aaaMonitor prestaties van Azure-web-app | Microsoft Docs
description: Prestaties controleren voor Azure-web-apps. Laad- en reactietijd voor grafieken, afhankelijkheidsinformatie en waarschuwingen instellen voor prestaties.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="5a411-104">Prestaties van Azure-web-apps controleren</span><span class="sxs-lookup"><span data-stu-id="5a411-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="5a411-105">In Hallo [Azure Portal](https://portal.azure.com) kunt u een application performance monitoring instellen uw [Azure-web-apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a411-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="5a411-106">[Azure Application Insights](app-insights-overview.md) instrumenten van uw app toosend telemetrie over de activiteiten toohello Application Insights-service, waar ze worden opgeslagen en geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="5a411-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="5a411-107">Daar metrische grafieken en zoekfuncties kunnen worden gebruikt toohelp vaststellen van problemen met de prestaties verbeteren en beoordelen van informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="5a411-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="5a411-108">Runtime of buildtime</span><span class="sxs-lookup"><span data-stu-id="5a411-108">Run time or build time</span></span>
<span data-ttu-id="5a411-109">U kunt configureren om bewaking in door te instrumenteren Hallo-app op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="5a411-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="5a411-110">**Runtime**: u kunt een uitbreiding van de prestatiecontrole selecteren wanneer uw web-app al gepubliceerd is.</span><span class="sxs-lookup"><span data-stu-id="5a411-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="5a411-111">Het is niet nodig toorebuild of uw app opnieuw te installeren.</span><span class="sxs-lookup"><span data-stu-id="5a411-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="5a411-112">U ontvangt een standaardset aan pakketten voor het controleren van reactietijden, succespercentages, uitzonderingen, afhankelijkheden, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="5a411-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="5a411-113">**Buildtime**: u kunt een pakket installeren in uw app in ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="5a411-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="5a411-114">Deze optie is veelzijdiger.</span><span class="sxs-lookup"><span data-stu-id="5a411-114">This option is more versatile.</span></span> <span data-ttu-id="5a411-115">In aanvulling toohello dezelfde standaard pakketten, kunt u code toocustomize Hallo telemetrie of toosend uw eigen telemetrie.</span><span class="sxs-lookup"><span data-stu-id="5a411-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="5a411-116">U kunt specifieke activiteiten of record gebeurtenissen op basis van toohello semantiek van het domein van uw app registreren.</span><span class="sxs-lookup"><span data-stu-id="5a411-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="5a411-117">Runtime-instrumentatiesleutel met Application Insights</span><span class="sxs-lookup"><span data-stu-id="5a411-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="5a411-118">Als u al een web-app uitvoert in Azure, is er al sprake van enige controle: frequentie van aanvragen en fouten.</span><span class="sxs-lookup"><span data-stu-id="5a411-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="5a411-119">Application Insights tooget meer, zoals reactietijden, bewaking aanroepen toodependencies Slimme detectie en krachtige logboekanalyse Hallo-querytaal toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a411-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="5a411-120">**Selecteer Application Insights** in hello Azure Configuratiescherm voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5a411-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![Kies Application Insights onder Controleren.](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="5a411-122">Kies toocreate een nieuwe resource, tenzij u al ingesteld voor deze app een Application Insights-resource door andere route.</span><span class="sxs-lookup"><span data-stu-id="5a411-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="5a411-123">**Instrumenteer uw web-app** nadat Application Insights is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5a411-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Uw web-app instrumenteren](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="5a411-125">**Schakel bewaking aan clientzijde in** voor paginaweergave- en gebruikerstelemetrie.</span><span class="sxs-lookup"><span data-stu-id="5a411-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="5a411-126">Selecteer Instellingen > Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="5a411-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="5a411-127">Voeg een nieuw sleutelwaardepaar toe bij App-instellingen:</span><span class="sxs-lookup"><span data-stu-id="5a411-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="5a411-128">Sleutel: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="5a411-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="5a411-129">Waarde:`true`</span><span class="sxs-lookup"><span data-stu-id="5a411-129">Value: `true`</span></span>
   * <span data-ttu-id="5a411-130">**Sla** Hallo instellingen en **opnieuw** uw app.</span><span class="sxs-lookup"><span data-stu-id="5a411-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="5a411-131">**Controleer uw app**.</span><span class="sxs-lookup"><span data-stu-id="5a411-131">**Monitor your app**.</span></span>  <span data-ttu-id="5a411-132">[Expore hello gegevens](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="5a411-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="5a411-133">Als u wilt, kunt u later Hallo-app met Application Insights maken.</span><span class="sxs-lookup"><span data-stu-id="5a411-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="5a411-134">*Hoe ik Application Insights verwijderen, of schakel toosending tooanother resource?*</span><span class="sxs-lookup"><span data-stu-id="5a411-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="5a411-135">Open in Azure, open Hallo blade web-app besturingselement en onder ontwikkelingsprogramma's **extensies**.</span><span class="sxs-lookup"><span data-stu-id="5a411-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="5a411-136">Verwijder de extensie Application Insights Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a411-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="5a411-137">Klik onder controle, kies Application Insights en maak of selecteer Hallo-bron die u wilt.</span><span class="sxs-lookup"><span data-stu-id="5a411-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="5a411-138">Hallo-app met Application Insights bouwen</span><span class="sxs-lookup"><span data-stu-id="5a411-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="5a411-139">Application Insights kan gedetailleerdere telemetrie verstrekken door een SDK in uw app te installeren.</span><span class="sxs-lookup"><span data-stu-id="5a411-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="5a411-140">U kunt met name traceerlogboeken verzamelen, [aangepaste telemetrie schrijven](app-insights-api-custom-events-metrics.md) en gedetailleerdere uitzonderingsrapporten ophalen.</span><span class="sxs-lookup"><span data-stu-id="5a411-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="5a411-141">Configureer **in Visual Studio** (2013-update 2 of hoger) Application Insights voor uw project.</span><span class="sxs-lookup"><span data-stu-id="5a411-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="5a411-142">Met de rechtermuisknop op het Hallo-webproject en selecteer **toevoegen > Application Insights** of **Configure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5a411-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Met de rechtermuisknop op het Hallo-webproject en het toevoegen of configureren van Application Insights kiezen](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="5a411-144">Als u wordt gevraagd toosign in, moet u Hallo referenties gebruikt voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5a411-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="5a411-145">Hallo-bewerking heeft twee gevolgen:</span><span class="sxs-lookup"><span data-stu-id="5a411-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="5a411-146">Maakt een Application Insights-resource in Azure, waarbij telemetrie wordt opgeslagen, geanalyseerd en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5a411-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="5a411-147">Voegt Hallo Application Insights NuGet-pakket tooyour code (indien deze nog niet er), en configureert deze toosend telemetrie toohello Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="5a411-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="5a411-148">**Hallo telemetrie testen** door actieve Hallo-app in uw ontwikkelcomputer (F5).</span><span class="sxs-lookup"><span data-stu-id="5a411-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="5a411-149">**Hallo-app publiceren** tooAzure in Hallo gebruikelijke manier.</span><span class="sxs-lookup"><span data-stu-id="5a411-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="5a411-150">*Hoe schakel ik toosending tooa verschillende Application Insights-resource*</span><span class="sxs-lookup"><span data-stu-id="5a411-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="5a411-151">Kies in Visual Studio-project met de rechtermuisknop op Hallo **Configure Application Insights** en kies de gewenste Hallo-bron.</span><span class="sxs-lookup"><span data-stu-id="5a411-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="5a411-152">U Hallo optie toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="5a411-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="5a411-153">Opnieuw maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="5a411-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="5a411-154">Hallo-gegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="5a411-154">Explore hello data</span></span>
1. <span data-ttu-id="5a411-155">Hallo Application Insights-blade van uw web-app in het Configuratiescherm, ziet u Live metrische gegevens, waarin aanvragen en fouten binnen een tweede of twee van deze optreden.</span><span class="sxs-lookup"><span data-stu-id="5a411-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="5a411-156">Dit is bijzonder handige informatie wanneer u uw app opnieuw publiceert, omdat u problemen onmiddellijk te zien krijgt.</span><span class="sxs-lookup"><span data-stu-id="5a411-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="5a411-157">Klik in de volledige Application Insights-resource toohello.</span><span class="sxs-lookup"><span data-stu-id="5a411-157">Click through toohello full Application Insights resource.</span></span>

    ![Doorklikken](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="5a411-159">U kunt er ook rechtstreeks naartoe gaan via Azure-resourcenavigatie.</span><span class="sxs-lookup"><span data-stu-id="5a411-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="5a411-160">Klik op via een grafiek tooget meer detail:</span><span class="sxs-lookup"><span data-stu-id="5a411-160">Click through any chart tooget more detail:</span></span>
   
    ![Klik op de overzichtsblade van Hallo Application Insights in een grafiek](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="5a411-162">U kunt [metrische blades aanpassen](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="5a411-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="5a411-163">Klik in het verdere toosee afzonderlijke gebeurtenissen en hun eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5a411-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Klik op een gebeurtenis type tooopen een zoekopdracht op dat type gefilterd](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="5a411-165">U ziet Hallo '...' koppeling tooopen alle eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5a411-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="5a411-166">U kunt [zoekacties aanpassen](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="5a411-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="5a411-167">Gebruik voor krachtigere zoekopdrachten via uw telemetrie Hallo [querytaal van logboekanalyse](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="5a411-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="5a411-168">Meer telemetrie</span><span class="sxs-lookup"><span data-stu-id="5a411-168">More telemetry</span></span>

* [<span data-ttu-id="5a411-169">Gegevens voor laden van webpagina</span><span class="sxs-lookup"><span data-stu-id="5a411-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="5a411-170">Aangepaste telemetrie</span><span class="sxs-lookup"><span data-stu-id="5a411-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="5a411-171">Video</span><span class="sxs-lookup"><span data-stu-id="5a411-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="5a411-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a411-172">Next steps</span></span>
* <span data-ttu-id="5a411-173">[Hallo profiler uitvoeren op uw live app](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="5a411-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="5a411-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample): Azure Functions bewaken met Application Insights</span><span class="sxs-lookup"><span data-stu-id="5a411-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="5a411-175">[Inschakelen van Azure diagnostics](app-insights-azure-diagnostics.md) toobe verzonden tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="5a411-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="5a411-176">[Service health metrische gegevens controleren](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.</span><span class="sxs-lookup"><span data-stu-id="5a411-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="5a411-177">[Ontvang waarschuwingsmeldingen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) wanneer er operationele gebeurtenissen plaatsvinden of metrische gegevens een drempelwaarde overschrijden.</span><span class="sxs-lookup"><span data-stu-id="5a411-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="5a411-178">Gebruik [Application Insights voor JavaScript-apps en webpagina's](app-insights-javascript.md) tooget client telemetrie Hallo browsers die een webpagina bezoekt.</span><span class="sxs-lookup"><span data-stu-id="5a411-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="5a411-179">[Webtests voor beschikbaarheid instellen](app-insights-monitor-web-app-availability.md) toobe gewaarschuwd als uw site is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5a411-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

