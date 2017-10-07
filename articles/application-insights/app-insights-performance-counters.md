---
title: aaaPerformance tellers in Application Insights | Microsoft Docs
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
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="a0590-103">Systeemprestatiemeteritems in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a0590-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="a0590-104">Windows biedt een groot aantal [prestatiemeteritems](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) zoals bezetting CPU, geheugen, schijf en netwerkgebruik.</span><span class="sxs-lookup"><span data-stu-id="a0590-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="a0590-105">U kunt ook uw eigen links definiëren.</span><span class="sxs-lookup"><span data-stu-id="a0590-105">You can also define your own.</span></span> <span data-ttu-id="a0590-106">[Application Insights](app-insights-overview.md) kunt weergeven met deze prestatiemeteritems als uw toepassing wordt uitgevoerd onder IIS op een lokale host of virtuele machine toowhich u beheerderstoegang hebben.</span><span class="sxs-lookup"><span data-stu-id="a0590-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="a0590-107">Hallo grafieken geven Hallo resources beschikbaar tooyour live-toepassing en kunnen tooidentify onbalans load tussen serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="a0590-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="a0590-108">Prestatiemeteritems weergegeven in de blade Servers hello, waaronder een tabel die segmenten door server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="a0590-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="a0590-110">(Prestatie-items zijn niet beschikbaar voor Web-Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="a0590-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="a0590-111">Maar u kunt [Azure Diagnostics tooApplication Insights verzenden](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="a0590-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="a0590-112">Items weergeven</span><span class="sxs-lookup"><span data-stu-id="a0590-112">View counters</span></span>
<span data-ttu-id="a0590-113">Hallo Servers blade ziet u een standaardset prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="a0590-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="a0590-114">toosee andere tellers op Hallo grafieken op Hallo Servers blade bewerken of open een nieuw [Metrics Explorer](app-insights-metrics-explorer.md) blade en voegen nieuwe grafieken.</span><span class="sxs-lookup"><span data-stu-id="a0590-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="a0590-115">Hallo beschikbare items worden weergegeven als metrische gegevens wanneer u een grafiek bewerken.</span><span class="sxs-lookup"><span data-stu-id="a0590-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="a0590-117">toosee uw nuttigst grafieken op één plek maken een [dashboard](app-insights-dashboards.md) en tooit vastmaken.</span><span class="sxs-lookup"><span data-stu-id="a0590-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="a0590-118">Items toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0590-118">Add counters</span></span>
<span data-ttu-id="a0590-119">Als Hallo-prestatiemeteritem die u wilt dat niet wordt weergegeven in de lijst Hallo van metrische gegevens, gebeurt dit omdat Hallo Application Insights-SDK wordt niet worden verzameld in uw webserver.</span><span class="sxs-lookup"><span data-stu-id="a0590-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="a0590-120">U kunt deze configureren toodo dus.</span><span class="sxs-lookup"><span data-stu-id="a0590-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="a0590-121">Ontdek welke items beschikbaar in uw server zijn met behulp van deze PowerShell-opdracht op Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="a0590-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="a0590-122">(Zie [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="a0590-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="a0590-123">Open ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="a0590-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="a0590-124">Als u Application Insights tooyour app toegevoegd tijdens de ontwikkeling, bewerk ApplicationInsights.config in uw project en klik vervolgens opnieuw implementeren tooyour servers.</span><span class="sxs-lookup"><span data-stu-id="a0590-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="a0590-125">Als u de Status Monitor tooinstrument een web-app tijdens runtime gebruikt, moet u ApplicationInsights.config vinden in de hoofdmap Hallo van Hallo-app in IIS.</span><span class="sxs-lookup"><span data-stu-id="a0590-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="a0590-126">Deze er op elk serverexemplaar bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a0590-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="a0590-127">Hallo prestaties collector richtlijn bewerken:</span><span class="sxs-lookup"><span data-stu-id="a0590-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="a0590-128">U kunt vastleggen standaard tellers en die dat u zelf hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a0590-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="a0590-129">`\Objects\Processes`een voorbeeld van een standaard prestatiemeteritem is beschikbaar op alle Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="a0590-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="a0590-130">`\Sales(photo)\# Items Sold`is een voorbeeld van een aangepaste teller die mogelijk zijn geïmplementeerd in een webservice.</span><span class="sxs-lookup"><span data-stu-id="a0590-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="a0590-131">Hallo-indeling is `\Category(instance)\Counter"`, of gewoon voor categorieën waarvoor geen exemplaren `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="a0590-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="a0590-132">`ReportAs`is vereist voor de namen van prestatiemeteritems die komen niet overeen met `[a-zA-Z()/-_ \.]+` -dat wil zeggen, ze tekens bevatten die niet zijn opgenomen in de volgende sets Hallo: letters, ronde haakjes, schuine streep, afbreekstreepje, onderstrepingstekens, ruimte, punt.</span><span class="sxs-lookup"><span data-stu-id="a0590-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="a0590-133">Als u een exemplaar opgeeft, worden verzameld als een dimensie 'CounterInstanceName' Hallo metriek gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="a0590-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="a0590-134">Verzamelen van prestatiemeteritems in de code</span><span class="sxs-lookup"><span data-stu-id="a0590-134">Collecting performance counters in code</span></span>
<span data-ttu-id="a0590-135">de systeemprestaties toocollect prestatiemeteritems en verzend tooApplication Insights, kunt u onderstaande Hallo stukje aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a0590-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="a0590-136">Of u kunt doen Hallo hetzelfde met aangepaste metrische gegevens die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="a0590-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="a0590-137">Prestatiemeters in Analytics</span><span class="sxs-lookup"><span data-stu-id="a0590-137">Performance counters in Analytics</span></span>
<span data-ttu-id="a0590-138">U kunt zoeken en weergeven van de teller prestatierapporten in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a0590-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="a0590-139">Hallo **performanceCounters** schema beschrijft Hallo `category`, `counter` naam, en `instance` naam van elk prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="a0590-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="a0590-140">Hallo telemetrie voor elke toepassing ziet u alleen Hallo items voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0590-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="a0590-141">Bijvoorbeeld: toosee welke items zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="a0590-141">For example, toosee what counters are available:</span></span> 

![Prestatiemeters in Application Insights analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="a0590-143">(Exemplaar van prestatiemeteritem toohello hier de instantie' verwijst, niet Hallo functie of servergroep exemplaar van de machine.</span><span class="sxs-lookup"><span data-stu-id="a0590-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="a0590-144">naam exemplaar Prestatiemeter Hallo doorgaans segmenten items zoals processortijd met de naam van de toepassing of proces Hallo Hallo.)</span><span class="sxs-lookup"><span data-stu-id="a0590-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="a0590-145">een grafiek van het beschikbare geheugen over Hallo recente periode tooget:</span><span class="sxs-lookup"><span data-stu-id="a0590-145">tooget a chart of available memory over hello recent period:</span></span> 

![Geheugen timechart in Application Insights analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="a0590-147">Zoals u andere telemetrie **performanceCounters** heeft ook een kolom `cloud_RoleInstance` die aangeeft dat de identiteit Hallo van Hallo host server-exemplaar waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a0590-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="a0590-148">Bijvoorbeeld: toocompare Hallo prestaties van uw app op verschillende computers Hallo:</span><span class="sxs-lookup"><span data-stu-id="a0590-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Prestaties gesegmenteerd op rolinstantie in Application Insights analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="a0590-150">ASP.NET en Application Insights tellingen</span><span class="sxs-lookup"><span data-stu-id="a0590-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="a0590-151">*Wat is Hallo verschil tussen Hallo uitzondering snelheid en uitzonderingen metrische gegevens?*</span><span class="sxs-lookup"><span data-stu-id="a0590-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="a0590-152">*Snelheid van de uitzondering* is van een prestatiemeteritem voor het systeem.</span><span class="sxs-lookup"><span data-stu-id="a0590-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="a0590-153">Hallo CLR telt alle Hallo verwerkte en onverwerkte uitzonderingen die worden gegenereerd en Hallo totaal in een interval van steekproeven verdeelt door Hallo lengte van hello-interval.</span><span class="sxs-lookup"><span data-stu-id="a0590-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="a0590-154">Hallo Application Insights-SDK dit resultaat verzamelt en verzendt het toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="a0590-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="a0590-155">*Uitzonderingen* is een telling van Hallo TrackException-rapporten ontvangen door het Hallo-portal op Hallo steekproefinterval van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="a0590-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="a0590-156">Het bevat alleen Hallo verwerkte uitzonderingen waar u TrackException aanroept in uw code en niet alle opgenomen hebt geschreven [onverwerkte uitzonderingen](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="a0590-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="a0590-157">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="a0590-157">Alerts</span></span>
<span data-ttu-id="a0590-158">Net als andere metrische gegevens, kunt u [een waarschuwing instellen](app-insights-alerts.md) toowarn die u als een prestatiemeteritem gaat buiten een grens die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="a0590-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="a0590-159">Open de blade beveiligingswaarschuwingen Hallo en klik op waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0590-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="a0590-160"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0590-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="a0590-161">Bijhouden van afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="a0590-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="a0590-162">Uitzonderingen bijhouden</span><span class="sxs-lookup"><span data-stu-id="a0590-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

