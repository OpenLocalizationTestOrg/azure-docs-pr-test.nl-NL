---
title: aaaApplication kaart in Azure Application Insights | Microsoft Docs
description: Een visuele presentatie van Hallo afhankelijkheden tussen de onderdelen van de app, voorzien van KPI's en waarschuwingen.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="0be36-103">De toepassingstoewijzing in Application Insights</span><span class="sxs-lookup"><span data-stu-id="0be36-103">Application Map in Application Insights</span></span>
<span data-ttu-id="0be36-104">In [Azure Application Insights](app-insights-overview.md), toepassingstoewijzing is een visuele indeling van Hallo afhankelijkheidsrelaties tussen onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0be36-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="0be36-105">Elk onderdeel toont KPI's zoals belasting, prestaties, fouten en waarschuwingen, toohelp detecteren van de onderdelen die zijn veroorzaakt door een prestatieprobleem of fout.</span><span class="sxs-lookup"><span data-stu-id="0be36-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="0be36-106">U kunt doorklikken van elk onderdeel toomore gedetailleerde diagnostische gegevens, zoals Application Insights-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="0be36-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="0be36-107">Als uw app gebruikmaakt van Azure-services, kunt u ook doorklikken tooAzure diagnostische gegevens, zoals SQL Database Advisor aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="0be36-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="0be36-108">U kunt een toepassing kaart toohello Azure-dashboard, waar deze zich volledig functioneel vastmaken zoals andere grafieken.</span><span class="sxs-lookup"><span data-stu-id="0be36-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="0be36-109">Open Hallo toepassingstoewijzing</span><span class="sxs-lookup"><span data-stu-id="0be36-109">Open hello application map</span></span>
<span data-ttu-id="0be36-110">Open Hallo toewijzing van de overzichtsblade Hallo voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="0be36-110">Open hello map from hello overview blade for your application:</span></span>

![Open de app-kaart](./media/app-insights-app-map/01.png)

![App-kaart](./media/app-insights-app-map/02.png)

<span data-ttu-id="0be36-113">Hallo-kaart toont:</span><span class="sxs-lookup"><span data-stu-id="0be36-113">hello map shows:</span></span>

* <span data-ttu-id="0be36-114">Beschikbaarheidstests</span><span class="sxs-lookup"><span data-stu-id="0be36-114">Availability tests</span></span>
* <span data-ttu-id="0be36-115">Client-side-onderdeel (bewaakt met Hallo JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="0be36-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="0be36-116">Server-side-onderdeel</span><span class="sxs-lookup"><span data-stu-id="0be36-116">Server-side component</span></span>
* <span data-ttu-id="0be36-117">Afhankelijkheden van de client- en serveronderdelen Hallo</span><span class="sxs-lookup"><span data-stu-id="0be36-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="0be36-118">U kunt uitvouwen en samenvouwen afhankelijkheid koppeling groepen:</span><span class="sxs-lookup"><span data-stu-id="0be36-118">You can expand and collapse dependency link groups:</span></span>

![samenvouwen](./media/app-insights-app-map/03.png)

<span data-ttu-id="0be36-120">Als er veel afhankelijkheden van een bepaald type (SQL, HTTP-enzovoort), kunnen ze gegroepeerde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0be36-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![gegroepeerde afhankelijkheden](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="0be36-122">Ter plaatse problemen</span><span class="sxs-lookup"><span data-stu-id="0be36-122">Spot problems</span></span>
<span data-ttu-id="0be36-123">Elk knooppunt heeft relevante prestatie-indicatoren, zoals Hallo belasting, prestaties en fout tarieven voor het desbetreffende onderdeel.</span><span class="sxs-lookup"><span data-stu-id="0be36-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="0be36-124">De pictogrammen waarschuwing Markeer mogelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="0be36-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="0be36-125">Een oranje waarschuwing betekent dat er fouten zijn in aanvragen, paginaweergaven of afhankelijkheidsaanroepen.</span><span class="sxs-lookup"><span data-stu-id="0be36-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="0be36-126">Rood betekent een Faalpercentage 5% of hoger.</span><span class="sxs-lookup"><span data-stu-id="0be36-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="0be36-127">Als u deze drempels tooadjust wilt, opent u de opties.</span><span class="sxs-lookup"><span data-stu-id="0be36-127">If you want tooadjust these thresholds, open Options.</span></span>

![Fout pictogrammen](./media/app-insights-app-map/04.png)

<span data-ttu-id="0be36-129">Actieve waarschuwingen ook weergeven van:</span><span class="sxs-lookup"><span data-stu-id="0be36-129">Active alerts also show up:</span></span> 

![actieve waarschuwingen](./media/app-insights-app-map/05.png)

<span data-ttu-id="0be36-131">Als u SQL Azure gebruikt, is er een pictogram dat ziet u wanneer er zijn aanbevelingen voor hoe u kunt de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="0be36-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure aanbeveling](./media/app-insights-app-map/06.png)

<span data-ttu-id="0be36-133">Klik op een pictogram tooget meer informatie:</span><span class="sxs-lookup"><span data-stu-id="0be36-133">Click any icon tooget more details:</span></span>

![Azure aanbeveling](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="0be36-135">Diagnostische klik door</span><span class="sxs-lookup"><span data-stu-id="0be36-135">Diagnostic click through</span></span>
<span data-ttu-id="0be36-136">Elk knooppunt op Hallo kaart Hallo biedt gerichte klik door voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0be36-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="0be36-137">Hallo-opties zijn afhankelijk van Hallo type Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0be36-137">hello options vary depending on hello type of hello node.</span></span>

![Serveropties](./media/app-insights-app-map/09.png)

<span data-ttu-id="0be36-139">Hallo-opties, voor de onderdelen die worden gehost in Azure, directe koppelingen toothem zijn.</span><span class="sxs-lookup"><span data-stu-id="0be36-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="0be36-140">Filters en tijdsbereik</span><span class="sxs-lookup"><span data-stu-id="0be36-140">Filters and time range</span></span>
<span data-ttu-id="0be36-141">Standaard Hallo kaart bevat een overzicht van alle Hallo gegevens beschikbaar voor Hallo gekozen tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="0be36-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="0be36-142">Maar u kunt deze filteren tooinclude alleen specifieke bewerking namen of afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0be36-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="0be36-143">Naam van de bewerking: dit omvat zowel paginaweergaven en serverzijde aanvraagtypen.</span><span class="sxs-lookup"><span data-stu-id="0be36-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="0be36-144">Met deze optie Hallo Hallo kaart toont KPI op Hallo server-clientzijde knooppunt voor bewerkingen alleen Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0be36-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="0be36-145">Hallo afhankelijkheden aangeroepen in de context Hallo van deze specifieke bewerkingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0be36-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="0be36-146">Basisnaam voor afhankelijkheid: dit omvat Hallo AJAX browser afhankelijkheden en afhankelijkheden van de serverzijde.</span><span class="sxs-lookup"><span data-stu-id="0be36-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="0be36-147">Als u aangepaste afhankelijkheidstelemetrie Hello TrackDependency API, weergegeven ze ook hier.</span><span class="sxs-lookup"><span data-stu-id="0be36-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="0be36-148">Hallo afhankelijkheden tooshow op Hallo-kaart, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="0be36-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="0be36-149">Deze selectie filteren op dit moment niet Hallo serverzijde aanvragen of Hallo clientzijde paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="0be36-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Filters instellen](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="0be36-151">Filters opslaan</span><span class="sxs-lookup"><span data-stu-id="0be36-151">Save filters</span></span>
<span data-ttu-id="0be36-152">toosave hello filters die u hebt toegepast, pincode Hallo gefilterde weergave naar een [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="0be36-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Pincode toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="0be36-154">Foutvenster</span><span class="sxs-lookup"><span data-stu-id="0be36-154">Error pane</span></span>
<span data-ttu-id="0be36-155">Als u op een knooppunt in het Hallo-kaart, wordt een foutvenster weergegeven aan de rechterkant Hallo samenvatten fouten voor dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0be36-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="0be36-156">Fouten zijn gegroepeerd eerst op bewerkings-ID en vervolgens gegroepeerd op probleem-ID.</span><span class="sxs-lookup"><span data-stu-id="0be36-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Foutvenster](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="0be36-158">Op een fout te klikken, gaat u toohello meest recente exemplaar van deze fout.</span><span class="sxs-lookup"><span data-stu-id="0be36-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="0be36-159">Status van resources</span><span class="sxs-lookup"><span data-stu-id="0be36-159">Resource health</span></span>
<span data-ttu-id="0be36-160">Voor sommige brontypen resourcestatus Hallo boven aan het foutvenster Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0be36-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="0be36-161">Bijvoorbeeld, ziet te klikken op een SQL-knooppunt Hallo database status en waarschuwingen die zijn gestart.</span><span class="sxs-lookup"><span data-stu-id="0be36-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Status van resources](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="0be36-163">U kunt klikken op Hallo resource naam tooview standaard overzicht metrische gegevens voor die bron.</span><span class="sxs-lookup"><span data-stu-id="0be36-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="0be36-164">End-to-end-systeem app maps</span><span class="sxs-lookup"><span data-stu-id="0be36-164">End-to-end system app maps</span></span>

<span data-ttu-id="0be36-165">*SDK-versie 2.3 of hoger vereist*</span><span class="sxs-lookup"><span data-stu-id="0be36-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="0be36-166">Als u uw toepassing heeft verschillende onderdelen - bijvoorbeeld een back-endservice bovendien toohello web-app- en u kunt weergeven ze allemaal op één geïntegreerde app-kaart.</span><span class="sxs-lookup"><span data-stu-id="0be36-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Filters instellen](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="0be36-168">Hallo app kaart wordt opgezocht serverknooppunten HTTP afhankelijkheid-aanroepen tussen servers met Hallo die Application Insights-SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0be36-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="0be36-169">Elke Application Insights-resource wordt uitgegaan van één server toocontain.</span><span class="sxs-lookup"><span data-stu-id="0be36-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="0be36-170">Met meerdere functie-app-kaart (preview)</span><span class="sxs-lookup"><span data-stu-id="0be36-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="0be36-171">Hallo preview met meerdere functie-app kaartfunctie kunt u toouse Hallo app kaart met meerdere servers voor het verzenden van gegevens toohello dezelfde Application Insights-resource / instrumentatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="0be36-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="0be36-172">Servers in kaart Hallo zijn gesegmenteerd op Hallo cloud_RoleName-eigenschap op telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="0be36-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="0be36-173">Stel *toepassing van meerdere rollenoverzicht* te*op* Hallo van Previews blade tooenable deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="0be36-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="0be36-174">Deze aanpak is het wellicht wenselijk in een toepassing micro-services of in andere scenario's waar u toocorrelate gebeurtenissen op meerdere servers binnen één Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="0be36-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="0be36-175">Video</span><span class="sxs-lookup"><span data-stu-id="0be36-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="0be36-176">Feedback</span><span class="sxs-lookup"><span data-stu-id="0be36-176">Feedback</span></span>
<span data-ttu-id="0be36-177">Geef feedback via Hallo portal feedbackoptie.</span><span class="sxs-lookup"><span data-stu-id="0be36-177">Please provide feedback through hello portal feedback option.</span></span>

![Afbeelding van MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="0be36-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0be36-179">Next steps</span></span>

* [<span data-ttu-id="0be36-180">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0be36-180">Azure portal</span></span>](https://portal.azure.com)
