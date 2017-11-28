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
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="17d8e-104">Waarschuwingen instellen voor Azure Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="17d8e-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="17d8e-105">: Introductiepagina Monitor</span><span class="sxs-lookup"><span data-stu-id="17d8e-105">Introduction: Monitor page</span></span>
<span data-ttu-id="17d8e-106">U kunt instellen waarschuwingen tootrigger een waarschuwing wanneer een metriek bereikt een voorwaarde die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="17d8e-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="17d8e-107">U kunt bijvoorbeeld een waarschuwing voor een voorwaarde Hallo volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="17d8e-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="17d8e-108">Regels kunnen worden ingesteld op metrische gegevens via de portal Hallo of kunnen worden geconfigureerd [programmatisch](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Bewerkingslogboeken gegevens.</span><span class="sxs-lookup"><span data-stu-id="17d8e-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="17d8e-109">Stel waarschuwingen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="17d8e-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="17d8e-110">Open in hello Azure-portal, Hallo gewenste toocreate een waarschuwing voor Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="17d8e-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="17d8e-111">In Hallo **taak** blade, klikt u op Hallo **bewaking** sectie.</span><span class="sxs-lookup"><span data-stu-id="17d8e-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="17d8e-112">In Hallo **metriek** blade, klikt u op Hallo **waarschuwing toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="17d8e-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Installatie van de Azure portal](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="17d8e-114">Voer een naam en beschrijving.</span><span class="sxs-lookup"><span data-stu-id="17d8e-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="17d8e-115">Hallo selectoren toodefine Hallo voorwaarde onder welke Hallo-mailwaarschuwing ontvangt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17d8e-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="17d8e-116">Bevatten informatie over waar de waarschuwing Hallo moet gaan.</span><span class="sxs-lookup"><span data-stu-id="17d8e-116">Provide information about where hello alert should go.</span></span>

      ![Instellen van een waarschuwing voor een Azure Streaming Analytics-taak](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="17d8e-118">Zie voor meer informatie over het configureren van waarschuwingen in hello Azure-portal [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="17d8e-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="17d8e-119">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="17d8e-119">Get help</span></span>
<span data-ttu-id="17d8e-120">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="17d8e-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="17d8e-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17d8e-121">Next steps</span></span>
* [<span data-ttu-id="17d8e-122">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17d8e-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="17d8e-123">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17d8e-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="17d8e-124">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="17d8e-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="17d8e-125">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="17d8e-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="17d8e-126">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="17d8e-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

