---
title: aaaOverview van metrische gegevens in Microsoft Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize bewaking grafieken in Azure.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Overzicht van metrische gegevens in Microsoft Azure
Alle Azure-services volgen de belangrijkste metrische gegevens die u toelaten om toomonitor Hallo status, prestaties, beschikbaarheid en informatie over het gebruik van uw services. U kunt deze metrische gegevens weergeven in hello Azure-portal en u kunt ook Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn931930.aspx) of [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Hallo volledige set van metrische gegevens via een programma.

Voor sommige services moet u mogelijk tooturn diagnostische gegevens in de volgorde toosee parameters. U ontvangt een elementaire reeks metrische gegevens voor anderen, zoals virtuele machines, maar moet tooenable Hallo volledige set hoge frequentie metrische gegevens. Zie [inschakelen bewaking en diagnostische gegevens](insights-how-to-use-diagnostics.md) toolearn meer.

## <a name="using-monitoring-charts"></a>Bewaking grafieken gebruiken
U kunt een van de metrische gegevens Hallo grafiek ze gedurende een periode die u kiest.

1. In Hallo [Azure Portal](https://portal.azure.com/), klikt u op **Bladeren**, en vervolgens een resource u geïnteresseerd bent in de bewaking.
2. Hallo **bewaking** sectie bevat Hallo belangrijkste metrische gegevens voor elke Azure-resource. Een web-app heeft bijvoorbeeld **aanvragen en fouten**, waarbij als een virtuele machine zou hebben **CPU-percentage** en **schijf lezen en schrijven**: ![lens voor controle](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Te klikken op een grafiek ziet u Hallo **metriek** blade. Op de blade Hallo bovendien toohello grafiek, is een tabel waarin aggregaties van Hallo metrische gegevens (zoals gemiddelde, minimale en maximale via Hallo tijdsbereik u hebt gekozen). Hieronder die zijn Hallo waarschuwingsregels voor Hallo resource.
    ![Metrische blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. toocustomize hello regels die wordt weergegeven, klikt u op Hallo **bewerken** knop op Hallo grafiek of Hallo **grafiek bewerken** opdracht op Hallo metrische blade.
5. U kunt op Hallo Query bewerken blade drie dingen doen:
   
   * Hallo tijdsbereik wijzigen
   * Hallo vormgeving tussen switch-balk en lijn
   * Kies verschillende metics ![Query bewerken](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Het wijzigen van Hallo tijdsbereik is net zo eenvoudig als het selecteren van een ander bereik (zoals **afgelopen uur**) en te klikken op **opslaan** Hallo Hallo blade onderaan in. U kunt ook **aangepaste**, zodat u kunt toochoose een tijdsperiode via Hallo afgelopen 2 weken. U ziet bijvoorbeeld Hallo hele twee weken of van gisteren slechts 1 uur. Typ in het Hallo tekst vak tooenter een andere uur.
    ![Aangepaste tijdsbereik](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Onderstaande tijdsbereik hello kiest u kanaal een willekeurig aantal tooshow metrische gegevens op Hallo-grafiek.
8. Wanneer u op Opslaan klikken worden uw wijzigingen worden opgeslagen voor die resource. Bijvoorbeeld, als u twee virtuele machines hebt en u een grafiek op een wijzigt, niet van invloed Hallo andere.

## <a name="creating-side-by-side-charts"></a>Side-by-side grafieken maken
Hallo krachtige aanpassing in Hallo-portal kunt u zoveel grafieken als u wilt toevoegen.

1. In Hallo **...**  menu bovenaan Hallo Hallo blade Klik **tegels toevoegen**:  
    ![Menu toevoegen](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Vervolgens, u kunt selecteren Selecteer een grafiek van Hallo **galerie** aan de rechterkant Hallo van het scherm: ![galerie](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Als er geen Hallo metrische gegevens die u wilt, kunt u altijd een toevoegen van Hallo voorinstelling metrische gegevens, en **bewerken** Hallo grafiek tooshow Hallo metrische gegevens die u nodig hebt.

## <a name="monitoring-usage-quotas"></a>Bewaking van de quota voor gebruik
De meeste metrische gegevens tonen u trends na verloop van tijd, maar bepaalde gegevens, zoals quota voor gebruik, zijn gegevens met een drempelwaarde punt in tijd.

U ziet ook quota voor gebruik op de blade Hallo voor bronnen waarvoor quota's:

![Gebruik](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Zoals met metrische gegevens, kunt u Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn931963.aspx) of [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Hallo volledige set van quota voor gebruik via een programma.

## <a name="next-steps"></a>Volgende stappen
* [Meldingen van waarschuwingen ontvangen](insights-receive-alert-notifications.md) wanneer een metriek een drempelwaarde overschrijdt.
* [Inschakelen bewaking en diagnostische gegevens](insights-how-to-use-diagnostics.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.
* [Aantal exemplaren automatisch schalen](insights-how-to-scale.md) toomake ervoor dat uw service beschikbaar is en reageert.
* [Bewaken van toepassingsprestaties](../application-insights/app-insights-azure-web-apps.md) als u wilt dat toounderstand precies hoe uw code uitvoert in de cloud Hallo.
* Gebruik [Application Insights voor JavaScript-apps en webpagina's](../application-insights/app-insights-web-track-usage.md) tooget client analytics over Hallo browsers die een webpagina bezoekt.
* [Beschikbaarheid en reactiesnelheid van een webpagina bewaken](../application-insights/app-insights-monitor-web-app-availability.md) met Application Insights zodat u ontdekken kunt als uw pagina niet beschikbaar is.

