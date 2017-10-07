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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Gebruik en prestaties bewaken in Windows-bureaublad-apps


Met [Azure Application Insights](app-insights-overview.md) en [HockeyApp](https://hockeyapp.net) kunt u het gebruik en de prestaties van uw geïmplementeerde toepassing bewaken.

> [!IMPORTANT]
> Het is raadzaam [HockeyApp](https://hockeyapp.net) toodistribute en monitor desktop- en apparaat-apps. Met HockeyApp kunt u distributie, livetesten en feedback van gebruikers beheren en gebruiks- en foutrapporten bewaken. U kunt ook [uw telemetrie exporteren en query’s hierop uitvoeren met Analytics](app-insights-hockeyapp-bridge-app.md).
> 
> Hoewel telemetrie kan tooApplication inzicht vanuit een bureaubladtoepassing worden verzonden, is dit vooral handig voor foutopsporing en experimentele.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetrie tooApplication inzicht vanuit een Windows-toepassing
1. In Hallo [Azure-portal](https://portal.azure.com), [een Application Insights-resource maken](app-insights-create-new-resource.md). Kies ASP.NET-app als het toepassingstype.
2. Een kopie van Hallo Instrumentatiesleutel in beslag nemen. Hallo-sleutel niet vinden in Hallo Essentials vervolgkeuzelijst van Hallo nieuwe bron die u zojuist hebt gemaakt. 
3. In Visual Studio bewerken Hallo NuGet-pakketten van uw app-project en voeg Microsoft.ApplicationInsights.WindowsServer toe. (Of Microsoft.ApplicationInsights kiezen als u wilt Hallo bare-API, zonder Hallo standaard telemetrie verzameling modules).
4. Hallo-instrumentatiesleutel instellen in uw code:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *uw sleutel* `";` 
   
    of in ApplicationInsights.config (als u een van de Hallo standaard telemetrie pakketten geïnstalleerd):
   
    `<InstrumentationKey>`*uw sleutel*`</InstrumentationKey>` 
   
    Als u ApplicationInsights.config gebruikt, controleert u of de eigenschappen in Solution Explorer te zijn ingesteld**Build Action = inhoud, kopie tooOutput Directory = kopiëren**.
5. [Hallo-API gebruiken](app-insights-api-custom-events-metrics.md) toosend telemetrie.
6. Uitvoeren van uw app en Zie Hallo telemetrie in Hallo-bron die u hebt gemaakt in hello Azure-Portal.

## <a name="telemetry"></a>Voorbeeldcode
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

## <a name="next-steps"></a>Volgende stappen
* [Een dashboard maken](app-insights-dashboards.md)
* [Diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md)
* [Metrische gegevens verkennen](app-insights-metrics-explorer.md)
* [Analytics-query's schrijven](app-insights-analytics.md)

