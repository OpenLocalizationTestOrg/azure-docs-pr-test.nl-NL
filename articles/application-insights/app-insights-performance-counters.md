---
title: Prestatiemeters in Application Insights | Microsoft Docs
description: Systeem- en aangepaste .NET-prestatiemeters in Application Insights bewaken.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="61a50-103">Systeemprestatiemeteritems in Application Insights</span><span class="sxs-lookup"><span data-stu-id="61a50-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="61a50-104">Windows biedt een groot aantal [prestatiemeteritems](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) zoals bezetting CPU, geheugen, schijf en netwerkgebruik.</span><span class="sxs-lookup"><span data-stu-id="61a50-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="61a50-105">U kunt ook uw eigen links definiëren.</span><span class="sxs-lookup"><span data-stu-id="61a50-105">You can also define your own.</span></span> <span data-ttu-id="61a50-106">[Application Insights](app-insights-overview.md) weergeven van deze prestatiemeteritems als uw toepassing onder IIS wordt uitgevoerd op een lokale host of virtuele machine waarop u beheerderstoegang hebben.</span><span class="sxs-lookup"><span data-stu-id="61a50-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="61a50-107">De diagrammen geven de resources die beschikbaar zijn voor uw live-toepassing en helpen bij het identificeren van onbalans load tussen serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="61a50-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="61a50-108">Prestatiemeteritems weergegeven in de blade Servers, waaronder een tabel die segmenten door server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="61a50-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="61a50-110">(Prestatie-items zijn niet beschikbaar voor Web-Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="61a50-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="61a50-111">Maar u kunt [diagnostische Azure-gegevens verzenden naar Application Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="61a50-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="61a50-112">Items weergeven</span><span class="sxs-lookup"><span data-stu-id="61a50-112">View counters</span></span>
<span data-ttu-id="61a50-113">De Servers blade ziet u een standaardset prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="61a50-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="61a50-114">Overzicht van andere items op de grafieken op de blade Servers bewerken of open een nieuw [Metrics Explorer](app-insights-metrics-explorer.md) blade en voegen nieuwe grafieken.</span><span class="sxs-lookup"><span data-stu-id="61a50-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="61a50-115">De beschikbare items worden weergegeven als metrische gegevens wanneer u een grafiek bewerken.</span><span class="sxs-lookup"><span data-stu-id="61a50-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="61a50-117">Overzicht van de handigste grafieken op één plek maken een [dashboard](app-insights-dashboards.md) en vastmaken aan.</span><span class="sxs-lookup"><span data-stu-id="61a50-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="61a50-118">Items toevoegen</span><span class="sxs-lookup"><span data-stu-id="61a50-118">Add counters</span></span>
<span data-ttu-id="61a50-119">Als het prestatiemeteritem dat u wilt dat niet wordt weergegeven in de lijst met metrische gegevens, gebeurt dit omdat de Application Insights-SDK wordt niet worden verzameld in uw webserver.</span><span class="sxs-lookup"><span data-stu-id="61a50-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="61a50-120">U kunt deze configureren om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="61a50-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="61a50-121">Ontdek welke items beschikbaar in uw server zijn met behulp van deze PowerShell-opdracht op de server:</span><span class="sxs-lookup"><span data-stu-id="61a50-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="61a50-122">(Zie [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="61a50-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="61a50-123">Open ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="61a50-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="61a50-124">Als u Application Insights hebt toegevoegd aan uw app tijdens de ontwikkeling, bewerk ApplicationInsights.config in uw project en vervolgens opnieuw implementeren op uw servers.</span><span class="sxs-lookup"><span data-stu-id="61a50-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="61a50-125">Als u een web-app tijdens runtime softwareontwikkelaars Status Monitor hebt gebruikt, moet u ApplicationInsights.config vinden in de hoofdmap van de app in IIS.</span><span class="sxs-lookup"><span data-stu-id="61a50-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="61a50-126">Deze er op elk serverexemplaar bijwerken.</span><span class="sxs-lookup"><span data-stu-id="61a50-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="61a50-127">De prestaties collector-instructie bewerken:</span><span class="sxs-lookup"><span data-stu-id="61a50-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="61a50-128">U kunt vastleggen standaard tellers en die dat u zelf hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="61a50-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="61a50-129">`\Objects\Processes`een voorbeeld van een standaard prestatiemeteritem is beschikbaar op alle Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="61a50-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="61a50-130">`\Sales(photo)\# Items Sold`is een voorbeeld van een aangepaste teller die mogelijk zijn geïmplementeerd in een webservice.</span><span class="sxs-lookup"><span data-stu-id="61a50-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="61a50-131">De indeling is `\Category(instance)\Counter"`, of gewoon voor categorieën waarvoor geen exemplaren `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="61a50-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="61a50-132">`ReportAs`is vereist voor de namen van prestatiemeteritems die komen niet overeen met `[a-zA-Z()/-_ \.]+` -dat wil zeggen, ze tekens bevatten die niet zijn opgenomen in de volgende sets: letters, ronde haakjes, schuine streep, afbreekstreepje, onderstrepingstekens, ruimte, punt.</span><span class="sxs-lookup"><span data-stu-id="61a50-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="61a50-133">Als u een exemplaar opgeeft, wordt deze als een dimensie 'CounterInstanceName' van de gerapporteerde metrische gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="61a50-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="61a50-134">Verzamelen van prestatiemeteritems in de code</span><span class="sxs-lookup"><span data-stu-id="61a50-134">Collecting performance counters in code</span></span>
<span data-ttu-id="61a50-135">Om te verzamelen systeemprestatiemeteritems en ze verzenden naar Application Insights, kunt u het onderstaande codefragment aanpassen:</span><span class="sxs-lookup"><span data-stu-id="61a50-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="61a50-136">Of u kunt dit ook doen met aangepaste metrische gegevens die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="61a50-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="61a50-137">Prestatiemeters in Analytics</span><span class="sxs-lookup"><span data-stu-id="61a50-137">Performance counters in Analytics</span></span>
<span data-ttu-id="61a50-138">U kunt zoeken en weergeven van de teller prestatierapporten in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="61a50-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="61a50-139">De **performanceCounters** schema beschrijft de `category`, `counter` naam, en `instance` naam van elk prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="61a50-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="61a50-140">In de telemetrie voor elke toepassing ziet u alleen de items voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="61a50-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="61a50-141">Bijvoorbeeld, als u wilt zien zijn welke items beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="61a50-141">For example, to see what counters are available:</span></span> 

![Prestatiemeters in Application Insights analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="61a50-143">(De instantie' verwijst hier naar het exemplaar van het prestatiemeteritem niet de functie of servergroep machine exemplaar.</span><span class="sxs-lookup"><span data-stu-id="61a50-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="61a50-144">De naam exemplaar Prestatiemeter doorgaans segmenten items zoals processortijd door de naam van de toepassing of proces.)</span><span class="sxs-lookup"><span data-stu-id="61a50-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="61a50-145">Een grafiek van het beschikbare geheugen over de afgelopen periode ophalen:</span><span class="sxs-lookup"><span data-stu-id="61a50-145">To get a chart of available memory over the recent period:</span></span> 

![Geheugen timechart in Application Insights analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="61a50-147">Zoals u andere telemetrie **performanceCounters** heeft ook een kolom `cloud_RoleInstance` die aangeeft dat de identiteit van de host-server-exemplaar waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61a50-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="61a50-148">Als u bijvoorbeeld wilt vergelijken de prestaties van uw app in de verschillende machines:</span><span class="sxs-lookup"><span data-stu-id="61a50-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Prestaties gesegmenteerd op rolinstantie in Application Insights analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="61a50-150">ASP.NET en Application Insights tellingen</span><span class="sxs-lookup"><span data-stu-id="61a50-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="61a50-151">*Wat is het verschil tussen de snelheid van de uitzondering en uitzonderingen metrische gegevens?*</span><span class="sxs-lookup"><span data-stu-id="61a50-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="61a50-152">*Snelheid van de uitzondering* is van een prestatiemeteritem voor het systeem.</span><span class="sxs-lookup"><span data-stu-id="61a50-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="61a50-153">De CLR telt alle verwerkte en onverwerkte uitzonderingen die worden gegenereerd en de totale binnen een interval van steekproeven worden gedeeld door de lengte van het interval.</span><span class="sxs-lookup"><span data-stu-id="61a50-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="61a50-154">De Application Insights-SDK dit resultaat verzamelt en verzendt het naar de portal.</span><span class="sxs-lookup"><span data-stu-id="61a50-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="61a50-155">*Uitzonderingen* is een aantal van de TrackException-rapporten ontvangen door de portal in het controle-interval van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="61a50-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="61a50-156">Het bevat alleen de verwerkte uitzonderingen waar u TrackException aanroept in uw code en niet alle opgenomen hebt geschreven [onverwerkte uitzonderingen](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="61a50-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="61a50-157">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="61a50-157">Alerts</span></span>
<span data-ttu-id="61a50-158">Net als andere metrische gegevens, kunt u [een waarschuwing instellen](app-insights-alerts.md) om u te waarschuwen als een prestatiemeteritem gaat buiten een grens die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="61a50-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="61a50-159">Open de blade waarschuwingen en klik op waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="61a50-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="61a50-160"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61a50-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="61a50-161">Bijhouden van afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="61a50-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="61a50-162">Uitzonderingen bijhouden</span><span class="sxs-lookup"><span data-stu-id="61a50-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

