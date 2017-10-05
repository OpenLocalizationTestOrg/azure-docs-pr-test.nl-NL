---
title: Slimme detectie in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="1656a-103">Slimme detectie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="1656a-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="1656a-104">Slimme detectie waarschuwt automatisch u over potentiële prestatieproblemen in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1656a-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="1656a-105">Proactieve analyse van de telemetrie die uw app naar verzendt uitgevoerd [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1656a-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1656a-106">Als er een plotselinge toename van de fout tarieven of afwijkende patronen in de prestaties van de client of server is, krijgt u een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="1656a-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="1656a-107">Deze functie heeft geen configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="1656a-107">This feature needs no configuration.</span></span> <span data-ttu-id="1656a-108">Dit werkt als uw toepassing voldoende telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="1656a-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="1656a-109">U kunt toegang verkrijgen tot de Slimme detectie waarschuwingen van de e-mails die u ontvangt, en van de blade Slimme detectie.</span><span class="sxs-lookup"><span data-stu-id="1656a-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="1656a-110">Bekijk uw smartcard detecties</span><span class="sxs-lookup"><span data-stu-id="1656a-110">Review your Smart Detections</span></span>
<span data-ttu-id="1656a-111">U kunt detecteren detecties op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="1656a-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="1656a-112">**U ontvangt een e-mailbericht** van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1656a-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="1656a-113">Hier volgt een typisch voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1656a-113">Here's a typical example:</span></span>
  
    ![E-mailmelding](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="1656a-115">Klik op de grote knop om meer details in de portal.</span><span class="sxs-lookup"><span data-stu-id="1656a-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="1656a-116">**De tegel Slimme detectie** op overzicht van uw app blade ziet u een aantal van recente meldingen.</span><span class="sxs-lookup"><span data-stu-id="1656a-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="1656a-117">Klik op de tegel om een lijst met recente waarschuwingen weer.</span><span class="sxs-lookup"><span data-stu-id="1656a-117">Click the tile to see a list of recent alerts.</span></span>

![Recente detecties weergeven](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="1656a-119">Selecteer een waarschuwing om de details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="1656a-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="1656a-120">Welke problemen worden ontdekt?</span><span class="sxs-lookup"><span data-stu-id="1656a-120">What problems are detected?</span></span>
<span data-ttu-id="1656a-121">Er zijn drie soorten detectie:</span><span class="sxs-lookup"><span data-stu-id="1656a-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="1656a-122">[Detectie - fout afwijkingen van smartcard](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1656a-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="1656a-123">We gebruiken machine learning voor het instellen van de verwachte frequentie van mislukte aanvragen voor uw app correleren met load en andere factoren.</span><span class="sxs-lookup"><span data-stu-id="1656a-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="1656a-124">Als het Faalpercentage buiten de verwachte envelop gaat, sturen we een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="1656a-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="1656a-125">[Detectie - afwijkingen van smartcard](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1656a-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="1656a-126">Als de reactietijd van een bewerking of een afhankelijkheid duur is langzaam wordt vergeleken met de historische basislijn of als we een afwijkende patroon in reactietijden of laadtijd van pagina identificeren krijgt u meldingen.</span><span class="sxs-lookup"><span data-stu-id="1656a-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="1656a-127">[Detectie - problemen met Azure Cloud Service slimme](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="1656a-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="1656a-128">Als uw app wordt gehost in Azure Cloud Services en een rolinstantie heeft startfouten, vaak worden gerecycled of runtime crashes krijgt u waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="1656a-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="1656a-129">(De help-koppelingen in elke melding gaat u naar de relevante artikelen.)</span><span class="sxs-lookup"><span data-stu-id="1656a-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="1656a-130">Video</span><span class="sxs-lookup"><span data-stu-id="1656a-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="1656a-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1656a-131">Next steps</span></span>
<span data-ttu-id="1656a-132">Deze diagnostische hulpprogramma's kunnen u de telemetrie van uw app te controleren:</span><span class="sxs-lookup"><span data-stu-id="1656a-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="1656a-133">Metrische explorer</span><span class="sxs-lookup"><span data-stu-id="1656a-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1656a-134">Search explorer</span><span class="sxs-lookup"><span data-stu-id="1656a-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1656a-135">Analytics - krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="1656a-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="1656a-136">Detectie van de smartcard is volledig automatisch.</span><span class="sxs-lookup"><span data-stu-id="1656a-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="1656a-137">Maar misschien u sommige meer waarschuwingen instellen?</span><span class="sxs-lookup"><span data-stu-id="1656a-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="1656a-138">Handmatig geconfigureerde metrische waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="1656a-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="1656a-139">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="1656a-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

