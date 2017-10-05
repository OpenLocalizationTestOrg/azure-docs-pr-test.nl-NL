---
title: De status en informatie over het gebruik met Application Insights van uw app bewaken
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
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="450e1-104">Prestaties in webtoepassingen controleren</span><span class="sxs-lookup"><span data-stu-id="450e1-104">Monitor performance in web applications</span></span>


<span data-ttu-id="450e1-105">Zorg ervoor dat uw toepassing goed presteert en vindt u informatie snel over fouten.</span><span class="sxs-lookup"><span data-stu-id="450e1-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="450e1-106">[Application Insights] [ start] u vertellen over prestatieproblemen en uitzonderingen en kunt u vinden en de hoofdoorzaken analyseren.</span><span class="sxs-lookup"><span data-stu-id="450e1-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="450e1-107">Application Insights kunnen Java- en ASP.NET-webtoepassingen en services, WCF-services bewaken.</span><span class="sxs-lookup"><span data-stu-id="450e1-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="450e1-108">Ze kunnen worden gehost op locatie, op virtuele machines, of als Microsoft Azure websites.</span><span class="sxs-lookup"><span data-stu-id="450e1-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="450e1-109">Application Insights kan duren voordat telemetrie van webpagina's en een groot aantal apparaten, zoals iOS, Android en Windows Store-apps aan de clientzijde.</span><span class="sxs-lookup"><span data-stu-id="450e1-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="450e1-110">We hebben een nieuwe ervaring beschikbaar gesteld voor langzame pagina's uitvoeren in uw webtoepassing kan vinden.</span><span class="sxs-lookup"><span data-stu-id="450e1-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="450e1-111">Als u geen toegang tot deze, inschakelen door het configureren van de preview-opties, waarbij de [Preview blade](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="450e1-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="450e1-112">Meer informatie over deze nieuwe ervaring in [opsporen en oplossen van knelpunten met de interactieve prestaties onderzoek](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="450e1-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="450e1-113"><a name="setup"></a>Instellen van de bewaking van toepassingsprestaties</span><span class="sxs-lookup"><span data-stu-id="450e1-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="450e1-114">Als u dit nog niet hebt (dat wil zeggen, als er geen ApplicationInsights.config) nog Application Insights toegevoegd aan uw project, kies een van de volgende manieren aan de slag:</span><span class="sxs-lookup"><span data-stu-id="450e1-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="450e1-115">ASP.NET-web-apps</span><span class="sxs-lookup"><span data-stu-id="450e1-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="450e1-116">Uitzondering bewaking toevoegen</span><span class="sxs-lookup"><span data-stu-id="450e1-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="450e1-117">Bewaking van afhankelijkheid toevoegen</span><span class="sxs-lookup"><span data-stu-id="450e1-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="450e1-118">J2EE-web-apps</span><span class="sxs-lookup"><span data-stu-id="450e1-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="450e1-119">Bewaking van afhankelijkheid toevoegen</span><span class="sxs-lookup"><span data-stu-id="450e1-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="450e1-120"><a name="view"></a>Maatstaven voor prestaties verkennen</span><span class="sxs-lookup"><span data-stu-id="450e1-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="450e1-121">In [de Azure-portal](https://portal.azure.com), blader naar de Application Insights-resource die u hebt ingesteld voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="450e1-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="450e1-122">De overzichtsblade ziet u eenvoudige prestatiegegevens:</span><span class="sxs-lookup"><span data-stu-id="450e1-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="450e1-123">Klik op een grafiek om meer details en om resultaten te bekijken voor een langere periode.</span><span class="sxs-lookup"><span data-stu-id="450e1-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="450e1-124">Klik bijvoorbeeld op de tegel aanvragen en selecteer vervolgens een tijdsbereik:</span><span class="sxs-lookup"><span data-stu-id="450e1-124">For example, click the Requests tile and then select a time range:</span></span>

![Klik verder voor meer gegevens en selecteer een tijdsbereik](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="450e1-126">Klik op een grafiek om te kiezen welke metrische gegevens worden weergegeven, of Voeg een nieuwe grafiek toe en selecteer de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="450e1-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Klik op een grafiek om metrische gegevens te selecteren](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="450e1-128">**Schakel het selectievakje van de metrische gegevens** om te zien van de volledige selectie die beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="450e1-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="450e1-129">De metrische gegevens kunnen worden onderverdeeld in groepen; Wanneer een lid van een groep is geselecteerd, worden alleen de andere leden van die groep weergegeven.</span><span class="sxs-lookup"><span data-stu-id="450e1-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="450e1-130"><a name="metrics"></a>Wat doet u alle gemiddelde?</span><span class="sxs-lookup"><span data-stu-id="450e1-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="450e1-131">Tegels van de prestaties en rapporten</span><span class="sxs-lookup"><span data-stu-id="450e1-131">Performance tiles and reports</span></span>
<span data-ttu-id="450e1-132">Er zijn verschillende maatstaven voor prestaties die kunt u krijgen.</span><span class="sxs-lookup"><span data-stu-id="450e1-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="450e1-133">Laten we beginnen met degenen die standaard worden weergegeven op de blade van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="450e1-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="450e1-134">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="450e1-134">Requests</span></span>
<span data-ttu-id="450e1-135">Het aantal HTTP-aanvragen ontvangen in een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="450e1-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="450e1-136">Vergelijk deze met de resultaten op andere rapporten om te zien hoe uw app omgaat als de belasting varieert.</span><span class="sxs-lookup"><span data-stu-id="450e1-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="450e1-137">HTTP-aanvragen bevatten alle GET of POST-aanvragen voor pagina's, gegevens en installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="450e1-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="450e1-138">Klik op de tegel voor tellingen voor specifieke URL's.</span><span class="sxs-lookup"><span data-stu-id="450e1-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="450e1-139">Gemiddelde reactietijd</span><span class="sxs-lookup"><span data-stu-id="450e1-139">Average response time</span></span>
<span data-ttu-id="450e1-140">Hiermee wordt de tijd tussen een webaanvraag invoeren van uw toepassing en het antwoord.</span><span class="sxs-lookup"><span data-stu-id="450e1-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="450e1-141">De punten weergeven zwevend gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="450e1-141">The points show a moving average.</span></span> <span data-ttu-id="450e1-142">Als er een groot aantal aanvragen, is er mogelijk een aantal die afwijken van het gemiddelde zonder een duidelijke piek of dip in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="450e1-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="450e1-143">Zoek naar ongebruikelijke pieken.</span><span class="sxs-lookup"><span data-stu-id="450e1-143">Look for unusual peaks.</span></span> <span data-ttu-id="450e1-144">In het algemeen verwachten reactietijd toenemen met een toename van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="450e1-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="450e1-145">Als de stijging onevenredige is, is het mogelijk dat uw app een limiet resource zoals CPU of de capaciteit van een service die wordt gebruikt roept.</span><span class="sxs-lookup"><span data-stu-id="450e1-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="450e1-146">Klik op de tegel voor tijden voor specifieke URL's.</span><span class="sxs-lookup"><span data-stu-id="450e1-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="450e1-147">Traagste aanvragen</span><span class="sxs-lookup"><span data-stu-id="450e1-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="450e1-148">Toont welke aanvragen mogelijk prestaties afstemmen.</span><span class="sxs-lookup"><span data-stu-id="450e1-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="450e1-149">Mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="450e1-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="450e1-150">Een aantal aanvragen dat niet-onderschepte uitzonderingen heeft geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="450e1-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="450e1-151">Klik op de tegel om de details van specifieke problemen en selecteert u een afzonderlijke aanvraag naar de details.</span><span class="sxs-lookup"><span data-stu-id="450e1-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="450e1-152">Alleen een representatieve steekproef van fouten wordt voor afzonderlijke inspectie bewaard.</span><span class="sxs-lookup"><span data-stu-id="450e1-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="450e1-153">Andere metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="450e1-153">Other metrics</span></span>
<span data-ttu-id="450e1-154">Om te zien wat stelt andere metrische gegevens weergeven, klikt u op een grafiek en schakelt u de metrische gegevens voor een overzicht van de volledige beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="450e1-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="450e1-155">Klik (i) voor elke metriek definitie.</span><span class="sxs-lookup"><span data-stu-id="450e1-155">Click (i) to see each metric's definition.</span></span>

![Schakel alle metrische gegevens voor een overzicht van de hele set](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="450e1-157">Een metriek selecteren, schakelt anderen die op dezelfde grafiek kan niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="450e1-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="450e1-158">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="450e1-158">Set alerts</span></span>
<span data-ttu-id="450e1-159">Ontvangen van e-mailadres van ongebruikelijke waarden van alle metrische gegevens, moet u een waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="450e1-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="450e1-160">U kunt ofwel het e-mailbericht verzenden naar de accountbeheerders, of specifieke e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="450e1-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="450e1-161">De bron voor de overige eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="450e1-161">Set the resource before the other properties.</span></span> <span data-ttu-id="450e1-162">Kies de bronnen webtest geen als u wilt waarschuwingen instellen voor prestaties of gebruik metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="450e1-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="450e1-163">Wees voorzichtig te weten de eenheden waarin u wordt gevraagd om in te voeren van de drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="450e1-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="450e1-164">*Ik ziet de waarschuwing toevoegen knop niet.*</span><span class="sxs-lookup"><span data-stu-id="450e1-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="450e1-165">-Is dit een groep account waartoe u alleen-lezen toegang hebben?</span><span class="sxs-lookup"><span data-stu-id="450e1-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="450e1-166">Neem contact op met de accountbeheerder.</span><span class="sxs-lookup"><span data-stu-id="450e1-166">Check with the account administrator.</span></span>

## <span data-ttu-id="450e1-167"><a name="diagnosis"></a>Oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="450e1-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="450e1-168">Hier volgen enkele tips voor het zoeken en onderzoeken van prestatieproblemen:</span><span class="sxs-lookup"><span data-stu-id="450e1-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="450e1-169">Instellen van [webtests] [ availability] om te worden gewaarschuwd als uw website uitvalt of onjuist of traag reageert.</span><span class="sxs-lookup"><span data-stu-id="450e1-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="450e1-170">Vergelijk het aantal verzoeken met andere metrische gegevens om te controleren of het mislukte of trage reactie laden zijn gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="450e1-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="450e1-171">[Invoegen en zoek trace-instructies] [ diagnostic] in uw code te helpen problemen te lokaliseren.</span><span class="sxs-lookup"><span data-stu-id="450e1-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="450e1-172">Bewaken van uw Web-app in bewerking met [livestream metrische gegevens][livestream].</span><span class="sxs-lookup"><span data-stu-id="450e1-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="450e1-173">De status van uw .net-toepassing met vastleggen [momentopname foutopsporingsprogramma][snapshot].</span><span class="sxs-lookup"><span data-stu-id="450e1-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="450e1-174">Zoek en corrigeer de knelpunten met een interactieve prestaties onderzoek</span><span class="sxs-lookup"><span data-stu-id="450e1-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="450e1-175">U kunt het nieuwe Application Insights interactieve prestaties onderzoek opzoeken gebieden van uw Web-app die de algehele prestaties vertragen.</span><span class="sxs-lookup"><span data-stu-id="450e1-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="450e1-176">U kunt snel zoeken naar specifieke's die vertragen en gebruikt de [Profiling hulpprogramma](app-insights-profiler.md) om te zien of er een correlatie tussen deze pagina's.</span><span class="sxs-lookup"><span data-stu-id="450e1-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="450e1-177">Een lijst met langzame presterende pagina's maken</span><span class="sxs-lookup"><span data-stu-id="450e1-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="450e1-178">De eerste stap voor het vinden van prestatieproblemen is voor een lijst van de traag reageert niet meer pagina's.</span><span class="sxs-lookup"><span data-stu-id="450e1-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="450e1-179">De schermafbeelding hieronder ziet u met behulp van de blade Performance om een lijst van mogelijke's verder onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="450e1-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="450e1-180">Snel ziet u op deze pagina dat er een vertraging in de reactietijd van de app op ongeveer 18:00 uur en nogmaals op ongeveer 10 uur was.</span><span class="sxs-lookup"><span data-stu-id="450e1-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="450e1-181">U ziet ook dat de GET-bewerking klantgegevens/bepaalde langlopende bewerkingen met een gemiddelde reactietijd van 507.05 milliseconden had.</span><span class="sxs-lookup"><span data-stu-id="450e1-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Application Insights interactieve prestaties](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="450e1-183">Inzoomen op bepaalde pagina 's</span><span class="sxs-lookup"><span data-stu-id="450e1-183">Drill down on specific pages</span></span>

<span data-ttu-id="450e1-184">Zodra u een momentopname van de prestaties van uw app hebt, kunt u meer informatie krijgen op specifieke bewerkingen trage prestaties.</span><span class="sxs-lookup"><span data-stu-id="450e1-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="450e1-185">Klik op elke bewerking in de lijst om de details te bekijken, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="450e1-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="450e1-186">U kunt zien als de prestaties is gebaseerd op een afhankelijkheid van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="450e1-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="450e1-187">U kunt ook zien hoeveel gebruikers de verschillende reactietijden heeft ondergaan.</span><span class="sxs-lookup"><span data-stu-id="450e1-187">You can also see how many users experienced the various response times.</span></span> 

![Application Insights operations blade](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="450e1-189">Inzoomen op een specifieke tijdsperiode</span><span class="sxs-lookup"><span data-stu-id="450e1-189">Drill down on a specific time period</span></span>

<span data-ttu-id="450e1-190">Nadat u een punt in tijd voor het onderzoeken van hebt geïdentificeerd, kunt u inzoomen zelfs verder blik op de specifieke bewerkingen die er de oorzaak van zijn dat de vertraging van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="450e1-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="450e1-191">Als u klikt op in een bepaald punt in tijd krijgt u de details van de pagina, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="450e1-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="450e1-192">In het voorbeeld hieronder u ziet de bewerkingen die worden vermeld voor een bepaalde periode samen met de server reactiecodes en de duur van de bewerking zijn.</span><span class="sxs-lookup"><span data-stu-id="450e1-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="450e1-193">Hebt u ook de url voor het openen van een TFS-werkitem als u moet deze informatie wordt verzonden naar uw ontwikkelteam.</span><span class="sxs-lookup"><span data-stu-id="450e1-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Application Insights tijdsegment](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="450e1-195">Inzoomen op een specifieke bewerking</span><span class="sxs-lookup"><span data-stu-id="450e1-195">Drill down on a specific operation</span></span>

<span data-ttu-id="450e1-196">Nadat u een punt in tijd voor het onderzoeken van hebt geïdentificeerd, kunt u inzoomen zelfs verder blik op de specifieke bewerkingen die er de oorzaak van zijn dat de vertraging van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="450e1-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="450e1-197">Klik op een bewerking uit de lijst om de details van de bewerking te bekijken, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="450e1-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="450e1-198">In dit voorbeeld ziet u dat de bewerking is mislukt, en Application Insights de details van de uitzondering heeft voor de toepassing heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="450e1-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="450e1-199">U kunt een TFS-werkitem opnieuw gemakkelijk van deze blade maken.</span><span class="sxs-lookup"><span data-stu-id="450e1-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights bewerking blade](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="450e1-201"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="450e1-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="450e1-202">[Webtests] [ availability] -webaanvragen verzonden naar uw toepassing met regelmatige tussenpozen van de hele wereld hebben.</span><span class="sxs-lookup"><span data-stu-id="450e1-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="450e1-203">[Vastleggen en zoeken van diagnostische traceringen] [ diagnostic] - traceringsaanroepen invoegen en de resultaten op de speldenpunt problemen doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="450e1-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="450e1-204">[Gebruik bijhouden] [ usage] -weten hoe mensen uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="450e1-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="450e1-205">[Het oplossen van problemen] [ qna] - en Q & A</span><span class="sxs-lookup"><span data-stu-id="450e1-205">[Troubleshooting][qna] - and Q & A</span></span>



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



