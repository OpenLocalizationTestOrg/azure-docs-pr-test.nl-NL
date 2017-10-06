---
title: aaaMonitor de status van uw app en het gebruik met Application Insights
description: Aan de slag met Application Insights. Analyseer gebruik, beschikbaarheid en prestaties van uw on-premises of de Microsoft Azure-toepassingen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="84c3d-104">Prestaties in webtoepassingen controleren</span><span class="sxs-lookup"><span data-stu-id="84c3d-104">Monitor performance in web applications</span></span>


<span data-ttu-id="84c3d-105">Zorg ervoor dat uw toepassing goed presteert en vindt u informatie snel over fouten.</span><span class="sxs-lookup"><span data-stu-id="84c3d-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="84c3d-106">[Application Insights] [ start] u vertellen over prestatieproblemen en uitzonderingen en helpen u te vinden en diagnose Hallo hoofdmap oorzaken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="84c3d-107">Application Insights kunnen Java- en ASP.NET-webtoepassingen en services, WCF-services bewaken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="84c3d-108">Ze kunnen worden gehost op locatie, op virtuele machines, of als Microsoft Azure websites.</span><span class="sxs-lookup"><span data-stu-id="84c3d-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="84c3d-109">Aan de clientzijde hello, Application Insights kan duren voordat telemetrie van webpagina's en een groot aantal apparaten, zoals iOS, Android en Windows Store-apps.</span><span class="sxs-lookup"><span data-stu-id="84c3d-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="84c3d-110">We hebben een nieuwe ervaring beschikbaar gesteld voor langzame pagina's uitvoeren in uw webtoepassing kan vinden.</span><span class="sxs-lookup"><span data-stu-id="84c3d-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="84c3d-111">Als u geen toegang tot tooit, het inschakelen door het configureren van uw opties preview Hello [Preview blade](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="84c3d-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="84c3d-112">Meer informatie over deze nieuwe ervaring in [opsporen en oplossen van knelpunten met Hallo interactieve prestaties onderzoek](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="84c3d-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="84c3d-113"><a name="setup"></a>Instellen van de bewaking van toepassingsprestaties</span><span class="sxs-lookup"><span data-stu-id="84c3d-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="84c3d-114">Als u nog tooyour Application Insights hebt toegevoegd (dat wil zeggen, als er geen ApplicationInsights.config) project, kies een van de volgende manieren tooget gestart:</span><span class="sxs-lookup"><span data-stu-id="84c3d-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="84c3d-115">ASP.NET-web-apps</span><span class="sxs-lookup"><span data-stu-id="84c3d-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="84c3d-116">Uitzondering bewaking toevoegen</span><span class="sxs-lookup"><span data-stu-id="84c3d-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="84c3d-117">Bewaking van afhankelijkheid toevoegen</span><span class="sxs-lookup"><span data-stu-id="84c3d-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="84c3d-118">J2EE-web-apps</span><span class="sxs-lookup"><span data-stu-id="84c3d-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="84c3d-119">Bewaking van afhankelijkheid toevoegen</span><span class="sxs-lookup"><span data-stu-id="84c3d-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="84c3d-120"><a name="view"></a>Maatstaven voor prestaties verkennen</span><span class="sxs-lookup"><span data-stu-id="84c3d-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="84c3d-121">In [hello Azure-portal](https://portal.azure.com), bladeren toohello Application Insights-resource die u hebt ingesteld voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="84c3d-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="84c3d-122">overzichtsblade Hello ziet basic prestatiegegevens:</span><span class="sxs-lookup"><span data-stu-id="84c3d-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="84c3d-123">Klik op een grafiek toosee meer detail en toosee resultaten voor een langere periode.</span><span class="sxs-lookup"><span data-stu-id="84c3d-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="84c3d-124">Klik bijvoorbeeld op Hallo aanvragen tegel en selecteer vervolgens een tijdsbereik:</span><span class="sxs-lookup"><span data-stu-id="84c3d-124">For example, click hello Requests tile and then select a time range:</span></span>

![Klik door toomore gegevens en selecteer een tijdsbereik](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="84c3d-126">Klik op een grafiek toochoose welke metrische gegevens worden weergegeven, of Voeg een nieuwe grafiek toe en selecteer de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="84c3d-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Klik op een grafiek toochoose metrische gegevens](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="84c3d-128">**Schakel alle Hallo metrische gegevens** toosee volledige selectie Hallo die beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="84c3d-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="84c3d-129">Hallo metrische gegevens kunnen worden onderverdeeld in groepen; Wanneer een lid van een groep is geselecteerd, worden alleen hello andere leden van die groep weergegeven.</span><span class="sxs-lookup"><span data-stu-id="84c3d-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="84c3d-130"><a name="metrics"></a>Wat doet u alle gemiddelde?</span><span class="sxs-lookup"><span data-stu-id="84c3d-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="84c3d-131">Tegels van de prestaties en rapporten</span><span class="sxs-lookup"><span data-stu-id="84c3d-131">Performance tiles and reports</span></span>
<span data-ttu-id="84c3d-132">Er zijn verschillende maatstaven voor prestaties die kunt u krijgen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="84c3d-133">Laten we beginnen met degenen die standaard worden weergegeven op de blade voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="84c3d-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="84c3d-134">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="84c3d-134">Requests</span></span>
<span data-ttu-id="84c3d-135">Hallo aantal HTTP-aanvragen ontvangen in een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="84c3d-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="84c3d-136">Vergelijk dit met Hallo resultaten op andere rapporten toosee hoe uw app omgaat als Hallo belasting varieert.</span><span class="sxs-lookup"><span data-stu-id="84c3d-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="84c3d-137">HTTP-aanvragen bevatten alle GET of POST-aanvragen voor pagina's, gegevens en installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="84c3d-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="84c3d-138">Klik op Hallo tegel tooget tellingen voor specifieke URL's.</span><span class="sxs-lookup"><span data-stu-id="84c3d-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="84c3d-139">Gemiddelde reactietijd</span><span class="sxs-lookup"><span data-stu-id="84c3d-139">Average response time</span></span>
<span data-ttu-id="84c3d-140">Metingen Hallo tijd tussen een webaanvraag invoeren van uw toepassing en het Hallo-antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="84c3d-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="84c3d-141">Hallo punten weergeven zwevend gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="84c3d-141">hello points show a moving average.</span></span> <span data-ttu-id="84c3d-142">Als er een groot aantal aanvragen, is er mogelijk enkele die afwijken van Hallo gemiddelde zonder een duidelijke piek of dip in Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="84c3d-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="84c3d-143">Zoek naar ongebruikelijke pieken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-143">Look for unusual peaks.</span></span> <span data-ttu-id="84c3d-144">In het algemeen verwacht antwoord tijd toorise met een toename van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="84c3d-145">Als Hallo aanleiding onevenredige is, kan uw app een limiet resource zoals CPU of Hallo capaciteit van een service die wordt gebruikt raken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="84c3d-146">Klik op Hallo tegel tooget tijden voor specifieke URL's.</span><span class="sxs-lookup"><span data-stu-id="84c3d-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="84c3d-147">Traagste aanvragen</span><span class="sxs-lookup"><span data-stu-id="84c3d-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="84c3d-148">Toont welke aanvragen mogelijk prestaties afstemmen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="84c3d-149">Mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="84c3d-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="84c3d-150">Een aantal aanvragen dat niet-onderschepte uitzonderingen heeft geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="84c3d-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="84c3d-151">Hallo tegel toosee Hallo details van specifieke fouten op en selecteer een afzonderlijke aanvraag toosee de details.</span><span class="sxs-lookup"><span data-stu-id="84c3d-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="84c3d-152">Alleen een representatieve steekproef van fouten wordt voor afzonderlijke inspectie bewaard.</span><span class="sxs-lookup"><span data-stu-id="84c3d-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="84c3d-153">Andere metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="84c3d-153">Other metrics</span></span>
<span data-ttu-id="84c3d-154">toosee welke andere metrische gegevens weergeven, klikt u op een grafiek en schakelt u alle Hallo metrische gegevens toosee Hallo volledige set.</span><span class="sxs-lookup"><span data-stu-id="84c3d-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="84c3d-155">Klik op (i) toosee elke metriek definitie.</span><span class="sxs-lookup"><span data-stu-id="84c3d-155">Click (i) toosee each metric's definition.</span></span>

![Selectie van alle metrische gegevens toosee Hallo hele set opheffen](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="84c3d-157">Selecteren van elke Hallo metrische schakelt Hallo anderen die kan niet worden weergegeven op hetzelfde diagram.</span><span class="sxs-lookup"><span data-stu-id="84c3d-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="84c3d-158">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="84c3d-158">Set alerts</span></span>
<span data-ttu-id="84c3d-159">op de hoogte met e-mailadres van ongebruikelijke waarden van een metriek toobe een waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="84c3d-160">U kunt toohello accountbeheerders voor toosend Hallo e of e-mailadressen toospecific.</span><span class="sxs-lookup"><span data-stu-id="84c3d-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="84c3d-161">Hallo-bron voordat Hallo andere eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="84c3d-162">Kies de Hallo webtest bronnen geen als u wilt dat tooset waarschuwingen van prestaties of de meetgegevens voor softwaregebruik op.</span><span class="sxs-lookup"><span data-stu-id="84c3d-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="84c3d-163">Worden zorgvuldige toonote Hallo eenheden waarin u wordt gevraagd tooenter Hallo drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="84c3d-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="84c3d-164">*Waarschuwing knop Hallo toevoegen wordt niet weergegeven.*</span><span class="sxs-lookup"><span data-stu-id="84c3d-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="84c3d-165">-Is dit een groep account toowhich u alleen-lezen toegang hebben?</span><span class="sxs-lookup"><span data-stu-id="84c3d-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="84c3d-166">Neem contact op met de accountbeheerder Hallo.</span><span class="sxs-lookup"><span data-stu-id="84c3d-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="84c3d-167"><a name="diagnosis"></a>Oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="84c3d-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="84c3d-168">Hier volgen enkele tips voor het zoeken en onderzoeken van prestatieproblemen:</span><span class="sxs-lookup"><span data-stu-id="84c3d-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="84c3d-169">Instellen van [webtests] [ availability] toobe gewaarschuwd als uw website uitvalt of onjuist of traag reageert.</span><span class="sxs-lookup"><span data-stu-id="84c3d-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="84c3d-170">Hallo aanvraag aantal met andere toosee metrische gegevens vergelijken als mislukte of trage reactie gerelateerde tooload zijn.</span><span class="sxs-lookup"><span data-stu-id="84c3d-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="84c3d-171">[Invoegen en zoek trace-instructies] [ diagnostic] in uw code toohelp speldenpunt problemen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="84c3d-172">Bewaken van uw Web-app in bewerking met [livestream metrische gegevens][livestream].</span><span class="sxs-lookup"><span data-stu-id="84c3d-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="84c3d-173">Hallo-status van uw .net-toepassing met vastleggen [momentopname foutopsporingsprogramma][snapshot].</span><span class="sxs-lookup"><span data-stu-id="84c3d-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="84c3d-174">Zoek en corrigeer de knelpunten met een interactieve prestaties onderzoek</span><span class="sxs-lookup"><span data-stu-id="84c3d-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="84c3d-175">U kunt Hallo nieuwe Application Insights interactieve prestaties onderzoek toolocate gebieden van uw Web-app die de algehele prestaties vertragen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="84c3d-176">U kunt snel zoeken naar specifieke's die vertragen en Hallo [Profiling hulpprogramma](app-insights-profiler.md) toosee als er een correlatie tussen deze pagina's.</span><span class="sxs-lookup"><span data-stu-id="84c3d-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="84c3d-177">Een lijst met langzame presterende pagina's maken</span><span class="sxs-lookup"><span data-stu-id="84c3d-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="84c3d-178">Hallo eerste stap voor het vinden van prestatieproblemen is tooget een lijst met Hallo traag reageert pagina's.</span><span class="sxs-lookup"><span data-stu-id="84c3d-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="84c3d-179">de onderstaande schermafdruk Hallo wordt gedemonstreerd met behulp van Hallo prestaties blade tooget een lijst met mogelijke tooinvestigate pagina's verder.</span><span class="sxs-lookup"><span data-stu-id="84c3d-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="84c3d-180">Snel ziet u op deze pagina dat er een vertraging in Hallo reactietijd van Hallo-app op ongeveer 18:00 uur en nogmaals op ongeveer 10 uur was.</span><span class="sxs-lookup"><span data-stu-id="84c3d-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="84c3d-181">U ziet ook dat Hallo GET klantgegevens/bewerking heeft enkele langlopende bewerkingen met een gemiddelde responstijd 507.05 tijd in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="84c3d-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Application Insights interactieve prestaties](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="84c3d-183">Inzoomen op bepaalde pagina 's</span><span class="sxs-lookup"><span data-stu-id="84c3d-183">Drill down on specific pages</span></span>

<span data-ttu-id="84c3d-184">Zodra u een momentopname van de prestaties van uw app hebt, kunt u meer informatie krijgen op specifieke bewerkingen trage prestaties.</span><span class="sxs-lookup"><span data-stu-id="84c3d-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="84c3d-185">Klik op elke bewerking in Hallo lijst toosee Hallo details, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="84c3d-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="84c3d-186">U kunt zien als Hallo prestaties is gebaseerd op een afhankelijkheid uit Hallo grafiek.</span><span class="sxs-lookup"><span data-stu-id="84c3d-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="84c3d-187">Ook ziet u hoeveel gebruikers ervaren Hallo verschillende responstijden.</span><span class="sxs-lookup"><span data-stu-id="84c3d-187">You can also see how many users experienced hello various response times.</span></span> 

![Application Insights operations blade](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="84c3d-189">Inzoomen op een specifieke tijdsperiode</span><span class="sxs-lookup"><span data-stu-id="84c3d-189">Drill down on a specific time period</span></span>

<span data-ttu-id="84c3d-190">Nadat u een punt in tijd tooinvestigate hebt geïdentificeerd, Inzoomen nog verder toolook op Hallo specifieke bewerkingen die mogelijk Hallo prestaties vertraging veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="84c3d-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="84c3d-191">Als u klikt op in een bepaald punt in tijd krijgt u details op Hallo van Hallo pagina zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="84c3d-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="84c3d-192">In Hallo ziet voorbeeld hieronder u Hallo bewerkingen die worden vermeld voor een bepaalde periode samen met reactiecodes Hallo-server en de duur van de Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="84c3d-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="84c3d-193">U hebt ook Hallo-url voor het openen van een TFS-werkitem als u deze informatie tooyour-ontwikkelteam toosend nodig.</span><span class="sxs-lookup"><span data-stu-id="84c3d-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Application Insights tijdsegment](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="84c3d-195">Inzoomen op een specifieke bewerking</span><span class="sxs-lookup"><span data-stu-id="84c3d-195">Drill down on a specific operation</span></span>

<span data-ttu-id="84c3d-196">Nadat u een punt in tijd tooinvestigate hebt geïdentificeerd, Inzoomen nog verder toolook op Hallo specifieke bewerkingen die mogelijk Hallo prestaties vertraging veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="84c3d-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="84c3d-197">Klik op een bewerking van Hallo lijst toosee Hallo details van Hallo bewerking zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="84c3d-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="84c3d-198">In dit voorbeeld u ziet dat Hallo-bewerking is mislukt en Application Insights Hallo details van Hallo is opgegeven heeft een uitzondering Hallo toepassing geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="84c3d-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="84c3d-199">U kunt een TFS-werkitem opnieuw gemakkelijk van deze blade maken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights bewerking blade](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="84c3d-201"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84c3d-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="84c3d-202">[Webtests] [ availability] -hebt verzonden webaanvragen tooyour toepassing met regelmatige tussenpozen van Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="84c3d-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="84c3d-203">[Vastleggen en zoeken van diagnostische traceringen] [ diagnostic] - traceringsaanroepen invoegen en doorzoeken Hallo resultaten toopinpoint problemen.</span><span class="sxs-lookup"><span data-stu-id="84c3d-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="84c3d-204">[Gebruik bijhouden] [ usage] -weten hoe mensen uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="84c3d-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="84c3d-205">[Het oplossen van problemen] [ qna] - en Q & A</span><span class="sxs-lookup"><span data-stu-id="84c3d-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



