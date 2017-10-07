---
title: aaaSet van waarschuwingen voor query's in de Stream Analytics | Microsoft Docs
description: Understanding Stream Analytics waarschuwingen
keywords: waarschuwingen instellen
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Waarschuwingen instellen voor Azure Stream Analytics-taken
## <a name="introduction-monitor-page"></a>: Introductiepagina Monitor
U kunt instellen waarschuwingen tootrigger een waarschuwing wanneer een metriek bereikt een voorwaarde die u opgeeft. U kunt bijvoorbeeld een waarschuwing voor een voorwaarde Hallo volgende instellen:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Regels kunnen worden ingesteld op metrische gegevens via de portal Hallo of kunnen worden geconfigureerd [programmatisch](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Bewerkingslogboeken gegevens.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Stel waarschuwingen in hello Azure-portal
1. Open in hello Azure-portal, Hallo gewenste toocreate een waarschuwing voor Stream Analytics-taak. 

2. In Hallo **taak** blade, klikt u op Hallo **bewaking** sectie.  

3. In Hallo **metriek** blade, klikt u op Hallo **waarschuwing toevoegen** opdracht.

      ![Installatie van de Azure portal](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Voer een naam en beschrijving.

5. Hallo selectoren toodefine Hallo voorwaarde onder welke Hallo-mailwaarschuwing ontvangt gebruiken.

6. Bevatten informatie over waar de waarschuwing Hallo moet gaan.

      ![Instellen van een waarschuwing voor een Azure Streaming Analytics-taak](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Zie voor meer informatie over het configureren van waarschuwingen in hello Azure-portal [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-get-started.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

