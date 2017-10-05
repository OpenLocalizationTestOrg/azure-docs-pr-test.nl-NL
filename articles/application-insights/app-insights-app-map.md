---
title: Kaart van de toepassing in Azure Application Insights | Microsoft Docs
description: Een visuele presentatie van de afhankelijkheden tussen de onderdelen van de app, voorzien van KPI's en waarschuwingen.
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
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="e2037-103">De toepassingstoewijzing in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2037-103">Application Map in Application Insights</span></span>
<span data-ttu-id="e2037-104">In [Azure Application Insights](app-insights-overview.md), toewijzing van de toepassing is een visuele indeling van de afhankelijkheidsrelaties tussen onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2037-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="e2037-105">Elk onderdeel toont KPI's zoals belasting, prestaties, fouten en waarschuwingen, om te zien van de onderdelen die zijn veroorzaakt door een prestatieprobleem of fout.</span><span class="sxs-lookup"><span data-stu-id="e2037-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="e2037-106">U kunt via van elk onderdeel klikken om meer gedetailleerde diagnostische gegevens, zoals Application Insights-gebeurtenissen te.</span><span class="sxs-lookup"><span data-stu-id="e2037-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="e2037-107">Als uw app gebruikmaakt van Azure-services, kunt u ook doorklikken naar Azure diagnostics, zoals SQL Database Advisor aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="e2037-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="e2037-108">U kunt een toepassing toewijzen aan de Azure-dashboard, waar deze zich volledig functioneel vastmaken zoals andere grafieken.</span><span class="sxs-lookup"><span data-stu-id="e2037-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="e2037-109">Open de toepassing-kaart</span><span class="sxs-lookup"><span data-stu-id="e2037-109">Open the application map</span></span>
<span data-ttu-id="e2037-110">De kaart openen vanuit de overzichtsblade van uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="e2037-110">Open the map from the overview blade for your application:</span></span>

![Open de app-kaart](./media/app-insights-app-map/01.png)

![App-kaart](./media/app-insights-app-map/02.png)

<span data-ttu-id="e2037-113">De kaart wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e2037-113">The map shows:</span></span>

* <span data-ttu-id="e2037-114">Beschikbaarheidstests</span><span class="sxs-lookup"><span data-stu-id="e2037-114">Availability tests</span></span>
* <span data-ttu-id="e2037-115">Client-side-onderdeel (bewaakt met de JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="e2037-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="e2037-116">Server-side-onderdeel</span><span class="sxs-lookup"><span data-stu-id="e2037-116">Server-side component</span></span>
* <span data-ttu-id="e2037-117">Afhankelijkheden van de client en server-onderdelen</span><span class="sxs-lookup"><span data-stu-id="e2037-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="e2037-118">U kunt uitvouwen en samenvouwen afhankelijkheid koppeling groepen:</span><span class="sxs-lookup"><span data-stu-id="e2037-118">You can expand and collapse dependency link groups:</span></span>

![samenvouwen](./media/app-insights-app-map/03.png)

<span data-ttu-id="e2037-120">Als er veel afhankelijkheden van een bepaald type (SQL, HTTP-enzovoort), kunnen ze gegroepeerde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e2037-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![gegroepeerde afhankelijkheden](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="e2037-122">Ter plaatse problemen</span><span class="sxs-lookup"><span data-stu-id="e2037-122">Spot problems</span></span>
<span data-ttu-id="e2037-123">Elk knooppunt heeft relevante prestatie-indicatoren, zoals de belasting, prestaties en fout tarieven voor het desbetreffende onderdeel.</span><span class="sxs-lookup"><span data-stu-id="e2037-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="e2037-124">De pictogrammen waarschuwing Markeer mogelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="e2037-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="e2037-125">Een oranje waarschuwing betekent dat er fouten zijn in aanvragen, paginaweergaven of afhankelijkheidsaanroepen.</span><span class="sxs-lookup"><span data-stu-id="e2037-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="e2037-126">Rood betekent een Faalpercentage 5% of hoger.</span><span class="sxs-lookup"><span data-stu-id="e2037-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="e2037-127">Als u deze drempels aanpassen wilt, opent u de opties.</span><span class="sxs-lookup"><span data-stu-id="e2037-127">If you want to adjust these thresholds, open Options.</span></span>

![Fout pictogrammen](./media/app-insights-app-map/04.png)

<span data-ttu-id="e2037-129">Actieve waarschuwingen ook weergeven van:</span><span class="sxs-lookup"><span data-stu-id="e2037-129">Active alerts also show up:</span></span> 

![actieve waarschuwingen](./media/app-insights-app-map/05.png)

<span data-ttu-id="e2037-131">Als u SQL Azure gebruikt, is er een pictogram dat ziet u wanneer er zijn aanbevelingen voor hoe u kunt de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="e2037-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure aanbeveling](./media/app-insights-app-map/06.png)

<span data-ttu-id="e2037-133">Klik op een pictogram voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="e2037-133">Click any icon to get more details:</span></span>

![Azure aanbeveling](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="e2037-135">Diagnostische klik door</span><span class="sxs-lookup"><span data-stu-id="e2037-135">Diagnostic click through</span></span>
<span data-ttu-id="e2037-136">Elk van de knooppunten op de kaart biedt gerichte klik door voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2037-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="e2037-137">De opties variëren afhankelijk van het type van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e2037-137">The options vary depending on the type of the node.</span></span>

![Serveropties](./media/app-insights-app-map/09.png)

<span data-ttu-id="e2037-139">De opties omvatten voor onderdelen die worden gehost in Azure, directe koppelingen naar deze.</span><span class="sxs-lookup"><span data-stu-id="e2037-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="e2037-140">Filters en tijdsbereik</span><span class="sxs-lookup"><span data-stu-id="e2037-140">Filters and time range</span></span>
<span data-ttu-id="e2037-141">Standaard de kaart bevat een overzicht van alle gegevens die beschikbaar zijn voor het gekozen tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="e2037-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="e2037-142">Maar u kunt deze zodanig dat alleen de namen van de specifieke bewerking of afhankelijkheden filteren.</span><span class="sxs-lookup"><span data-stu-id="e2037-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="e2037-143">Naam van de bewerking: dit omvat zowel paginaweergaven en serverzijde aanvraagtypen.</span><span class="sxs-lookup"><span data-stu-id="e2037-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="e2037-144">Met deze optie wordt de kaart de KPI op het knooppunt server-clientzijde voor de geselecteerde bewerkingen alleen.</span><span class="sxs-lookup"><span data-stu-id="e2037-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="e2037-145">De afhankelijkheden aangeroepen in de context van deze specifieke bewerkingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e2037-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="e2037-146">Basisnaam voor afhankelijkheid: dit omvat de AJAX browser afhankelijkheden en afhankelijkheden van de serverzijde.</span><span class="sxs-lookup"><span data-stu-id="e2037-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="e2037-147">Als u aangepaste afhankelijkheidstelemetrie met de API TrackDependency rapporteert, weergegeven ze ook hier.</span><span class="sxs-lookup"><span data-stu-id="e2037-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="e2037-148">U kunt de afhankelijkheden om weer te geven op de kaart selecteren.</span><span class="sxs-lookup"><span data-stu-id="e2037-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="e2037-149">Deze selectie filteren op dit moment niet de aanvragen van de server of de client-side paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="e2037-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![Filters instellen](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="e2037-151">Filters opslaan</span><span class="sxs-lookup"><span data-stu-id="e2037-151">Save filters</span></span>
<span data-ttu-id="e2037-152">Pincode voor het opslaan van de filters die u hebt toegepast, de gefilterde weergave naar een [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="e2037-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Vastmaken aan dashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="e2037-154">Foutvenster</span><span class="sxs-lookup"><span data-stu-id="e2037-154">Error pane</span></span>
<span data-ttu-id="e2037-155">Wanneer u een knooppunt in het overzicht klikt, wordt een foutvenster weergegeven aan de rechterkant van fouten voor dat knooppunt samen te vatten.</span><span class="sxs-lookup"><span data-stu-id="e2037-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="e2037-156">Fouten zijn gegroepeerd eerst op bewerkings-ID en vervolgens gegroepeerd op probleem-ID.</span><span class="sxs-lookup"><span data-stu-id="e2037-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Foutvenster](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="e2037-158">Op een fout te klikken, gaat u naar de meest recente exemplaar van deze fout.</span><span class="sxs-lookup"><span data-stu-id="e2037-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="e2037-159">Status van resources</span><span class="sxs-lookup"><span data-stu-id="e2037-159">Resource health</span></span>
<span data-ttu-id="e2037-160">Voor sommige brontypen resourcestatus weergegeven aan de bovenkant van het deelvenster fout.</span><span class="sxs-lookup"><span data-stu-id="e2037-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="e2037-161">Bijvoorbeeld, ziet te klikken op een SQL-knooppunt de status van de database en waarschuwingen die zijn gestart.</span><span class="sxs-lookup"><span data-stu-id="e2037-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![Status van resources](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="e2037-163">U kunt klikken op de naam van de resource standaard overzicht metrische gegevens voor die bron weergeven.</span><span class="sxs-lookup"><span data-stu-id="e2037-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="e2037-164">End-to-end-systeem app maps</span><span class="sxs-lookup"><span data-stu-id="e2037-164">End-to-end system app maps</span></span>

<span data-ttu-id="e2037-165">*SDK-versie 2.3 of hoger vereist*</span><span class="sxs-lookup"><span data-stu-id="e2037-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="e2037-166">Als uw toepassing verschillende onderdelen - bijvoorbeeld een back-endservice verder naar de web-app heeft - moet u ze kunt weergeven op één geïntegreerde app-kaart.</span><span class="sxs-lookup"><span data-stu-id="e2037-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![Filters instellen](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="e2037-168">De app-kaart wordt opgezocht serverknooppunten HTTP afhankelijkheid-aanroepen tussen servers met de Application Insights-SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e2037-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="e2037-169">Elke Application Insights-resource wordt uitgegaan van één server bevatten.</span><span class="sxs-lookup"><span data-stu-id="e2037-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="e2037-170">Met meerdere functie-app-kaart (preview)</span><span class="sxs-lookup"><span data-stu-id="e2037-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="e2037-171">De preview-functie voor het toewijzen van meerdere functie-app kunt u de app-kaart gebruiken met meerdere servers die gegevens te verzenden naar dezelfde Application Insights-resource / instrumentatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="e2037-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="e2037-172">Servers in de kaart worden gesegmenteerd op de eigenschap cloud_RoleName op telemetrie-items.</span><span class="sxs-lookup"><span data-stu-id="e2037-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="e2037-173">Ingesteld *toepassing van meerdere rollenoverzicht* naar *op* op de blade Previews zodat deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="e2037-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="e2037-174">Deze aanpak is het wellicht wenselijk in een toepassing micro-services of in andere scenario's waarvoor gebeurtenissen met elkaar correleren over meerdere servers in één Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="e2037-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="e2037-175">Video</span><span class="sxs-lookup"><span data-stu-id="e2037-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="e2037-176">Feedback</span><span class="sxs-lookup"><span data-stu-id="e2037-176">Feedback</span></span>
<span data-ttu-id="e2037-177">Geef feedback via de portal feedbackoptie.</span><span class="sxs-lookup"><span data-stu-id="e2037-177">Please provide feedback through the portal feedback option.</span></span>

![Afbeelding van MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="e2037-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2037-179">Next steps</span></span>

* [<span data-ttu-id="e2037-180">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e2037-180">Azure portal</span></span>](https://portal.azure.com)
