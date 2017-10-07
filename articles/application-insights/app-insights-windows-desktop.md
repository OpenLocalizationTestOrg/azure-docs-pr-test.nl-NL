---
title: aaaMonitoring gebruik en prestaties voor Windows desktop-apps
description: Analyseer het gebruik en de prestaties van uw Windows-bureaublad-app met HockeyApp en Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="884e7-103">Gebruik en prestaties bewaken in Windows-bureaublad-apps</span><span class="sxs-lookup"><span data-stu-id="884e7-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="884e7-104">Met [Azure Application Insights](app-insights-overview.md) en [HockeyApp](https://hockeyapp.net) kunt u het gebruik en de prestaties van uw geïmplementeerde toepassing bewaken.</span><span class="sxs-lookup"><span data-stu-id="884e7-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="884e7-105">Het is raadzaam [HockeyApp](https://hockeyapp.net) toodistribute en monitor desktop- en apparaat-apps.</span><span class="sxs-lookup"><span data-stu-id="884e7-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="884e7-106">Met HockeyApp kunt u distributie, livetesten en feedback van gebruikers beheren en gebruiks- en foutrapporten bewaken.</span><span class="sxs-lookup"><span data-stu-id="884e7-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="884e7-107">U kunt ook [uw telemetrie exporteren en query’s hierop uitvoeren met Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="884e7-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="884e7-108">Hoewel telemetrie kan tooApplication inzicht vanuit een bureaubladtoepassing worden verzonden, is dit vooral handig voor foutopsporing en experimentele.</span><span class="sxs-lookup"><span data-stu-id="884e7-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="884e7-109">toosend telemetrie tooApplication inzicht vanuit een Windows-toepassing</span><span class="sxs-lookup"><span data-stu-id="884e7-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="884e7-110">In Hallo [Azure-portal](https://portal.azure.com), [een Application Insights-resource maken](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="884e7-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="884e7-111">Kies ASP.NET-app als het toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="884e7-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="884e7-112">Een kopie van Hallo Instrumentatiesleutel in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="884e7-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="884e7-113">Hallo-sleutel niet vinden in Hallo Essentials vervolgkeuzelijst van Hallo nieuwe bron die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="884e7-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="884e7-114">In Visual Studio bewerken Hallo NuGet-pakketten van uw app-project en voeg Microsoft.ApplicationInsights.WindowsServer toe.</span><span class="sxs-lookup"><span data-stu-id="884e7-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="884e7-115">(Of Microsoft.ApplicationInsights kiezen als u wilt Hallo bare-API, zonder Hallo standaard telemetrie verzameling modules).</span><span class="sxs-lookup"><span data-stu-id="884e7-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="884e7-116">Hallo-instrumentatiesleutel instellen in uw code:</span><span class="sxs-lookup"><span data-stu-id="884e7-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="884e7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *uw sleutel* `";`</span><span class="sxs-lookup"><span data-stu-id="884e7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="884e7-118">of in ApplicationInsights.config (als u een van de Hallo standaard telemetrie pakketten geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="884e7-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="884e7-119">`<InstrumentationKey>`*uw sleutel*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="884e7-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="884e7-120">Als u ApplicationInsights.config gebruikt, controleert u of de eigenschappen in Solution Explorer te zijn ingesteld**Build Action = inhoud, kopie tooOutput Directory = kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="884e7-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="884e7-121">[Hallo-API gebruiken](app-insights-api-custom-events-metrics.md) toosend telemetrie.</span><span class="sxs-lookup"><span data-stu-id="884e7-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="884e7-122">Uitvoeren van uw app en Zie Hallo telemetrie in Hallo-bron die u hebt gemaakt in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="884e7-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="884e7-123"><a name="telemetry"></a>Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="884e7-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="884e7-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="884e7-124">Next steps</span></span>
* [<span data-ttu-id="884e7-125">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="884e7-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="884e7-126">Diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="884e7-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="884e7-127">Metrische gegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="884e7-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="884e7-128">Analytics-query's schrijven</span><span class="sxs-lookup"><span data-stu-id="884e7-128">Write Analytics queries</span></span>](app-insights-analytics.md)

