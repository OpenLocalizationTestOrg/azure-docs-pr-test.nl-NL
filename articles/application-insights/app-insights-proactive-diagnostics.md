---
title: aaaSmart detectie in Azure Application Insights | Microsoft Docs
description: "Application Insights voert een automatische grondige analyse van uw app Telemetrie en waarschuwt u potentiële problemen."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="8f2f3-103">Slimme detectie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="8f2f3-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="8f2f3-104">Slimme detectie waarschuwt automatisch u over potentiële prestatieproblemen in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="8f2f3-105">Proactieve analyse van Hallo telemetrie die uw app te verzendt worden uitgevoerd[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f3-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8f2f3-106">Als er een plotselinge toename van de fout tarieven of afwijkende patronen in de prestaties van de client of server is, krijgt u een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="8f2f3-107">Deze functie heeft geen configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-107">This feature needs no configuration.</span></span> <span data-ttu-id="8f2f3-108">Dit werkt als uw toepassing voldoende telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="8f2f3-109">U kunt Slimme detectie waarschuwingen openen van e-mailberichten Hallo die u ontvangt, en van Hallo Slimme detectie blade.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="8f2f3-110">Bekijk uw smartcard detecties</span><span class="sxs-lookup"><span data-stu-id="8f2f3-110">Review your Smart Detections</span></span>
<span data-ttu-id="8f2f3-111">U kunt detecteren detecties op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="8f2f3-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="8f2f3-112">**U ontvangt een e-mailbericht** van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="8f2f3-113">Hier volgt een typisch voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8f2f3-113">Here's a typical example:</span></span>
  
    ![E-mailmelding](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="8f2f3-115">Klik op Hallo big knop tooopen gedetailleerder Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="8f2f3-116">**Hallo Slimme detectie tegel** op overzicht van uw app blade ziet u een aantal van recente meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="8f2f3-117">Klik op Hallo tegel toosee een lijst met recente meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-117">Click hello tile toosee a list of recent alerts.</span></span>

![Recente detecties weergeven](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="8f2f3-119">Selecteer een waarschuwing toosee de details ervan.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="8f2f3-120">Welke problemen worden ontdekt?</span><span class="sxs-lookup"><span data-stu-id="8f2f3-120">What problems are detected?</span></span>
<span data-ttu-id="8f2f3-121">Er zijn drie soorten detectie:</span><span class="sxs-lookup"><span data-stu-id="8f2f3-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="8f2f3-122">[Detectie - fout afwijkingen van smartcard](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f3-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="8f2f3-123">We gebruiken machine learning tooset Hallo verwacht aantal mislukte aanvragen voor uw app, correleren met load en andere factoren.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="8f2f3-124">Als percentage van de mislukte Hallo buiten de verwachte envelop hello gaat, verzonden er een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="8f2f3-125">[Detectie - afwijkingen van smartcard](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f3-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="8f2f3-126">Als de reactietijd van een bewerking of een afhankelijkheid duur vergeleken toohistorical basislijn is vertragen of als we een afwijkende patroon in reactietijden of laadtijd van pagina identificeren krijgt u meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="8f2f3-127">[Detectie - problemen met Azure Cloud Service slimme](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="8f2f3-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="8f2f3-128">Als uw app wordt gehost in Azure Cloud Services en een rolinstantie heeft startfouten, vaak worden gerecycled of runtime crashes krijgt u waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="8f2f3-129">(Hallo help-koppelingen in elke melding duren u relevante artikelen toohello.)</span><span class="sxs-lookup"><span data-stu-id="8f2f3-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="8f2f3-130">Video</span><span class="sxs-lookup"><span data-stu-id="8f2f3-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="8f2f3-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f2f3-131">Next steps</span></span>
<span data-ttu-id="8f2f3-132">Deze diagnostische hulpprogramma's kunnen u controleren Hallo telemetrie van uw app:</span><span class="sxs-lookup"><span data-stu-id="8f2f3-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="8f2f3-133">Metrische explorer</span><span class="sxs-lookup"><span data-stu-id="8f2f3-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="8f2f3-134">Search explorer</span><span class="sxs-lookup"><span data-stu-id="8f2f3-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="8f2f3-135">Analytics - krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="8f2f3-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="8f2f3-136">Detectie van de smartcard is volledig automatisch.</span><span class="sxs-lookup"><span data-stu-id="8f2f3-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="8f2f3-137">Maar misschien wilt u tooset van sommige waarschuwingen meer?</span><span class="sxs-lookup"><span data-stu-id="8f2f3-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="8f2f3-138">Handmatig geconfigureerde metrische waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="8f2f3-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="8f2f3-139">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="8f2f3-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

