---
title: aaaExploring HockeyApp-gegevens in Azure Application Insights | Microsoft Docs
description: Analyseer gebruik en prestaties van uw app in Azure met Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="945e3-103">HockeyApp-gegevens in Application Insights verkennen</span><span class="sxs-lookup"><span data-stu-id="945e3-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="945e3-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) wordt aanbevolen Hallo platform voor het bewaken van live desktop- en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="945e3-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="945e3-105">Van HockeyApp, kunt u aangepaste verzenden en telemetrie toomonitor gebruik bijhouden en helpt bij de diagnose (in aanvulling toogetting crashgegevens).</span><span class="sxs-lookup"><span data-stu-id="945e3-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="945e3-106">Deze stroom telemetrie kan worden opgevraagd met Hallo krachtige [Analytics](app-insights-analytics.md) functie van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="945e3-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="945e3-107">Bovendien kunt u [Hallo aangepaste en tracetelemetrie exporteren](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="945e3-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="945e3-108">Deze functies, tooenable brug waarlangs HockeyApp aangepaste gegevens tooApplication Insights doorstuurt instellen.</span><span class="sxs-lookup"><span data-stu-id="945e3-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="945e3-109">Hallo HockeyApp Bridge app</span><span class="sxs-lookup"><span data-stu-id="945e3-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="945e3-110">Hallo HockeyApp brug App is Hallo core functie waarmee u tooaccess uw aangepaste HockeyApp en tracering telemetrie in Application Insights via Hallo Analytics en functies voor continue Export.</span><span class="sxs-lookup"><span data-stu-id="945e3-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="945e3-111">Aangepaste en tracering verzamelde gebeurtenissen per HockeyApp na het maken van Hallo HockeyApp Bridge App Hallo van deze functies toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="945e3-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="945e3-112">Laten we zien hoe tooset slechts één van deze Apps Bridge.</span><span class="sxs-lookup"><span data-stu-id="945e3-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="945e3-113">Open in de HockeyApp, accountinstellingen, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="945e3-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="945e3-114">Een nieuw token maken of een bestaande hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="945e3-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="945e3-115">Hallo minimale rechten vereist zijn 'alleen-lezen'.</span><span class="sxs-lookup"><span data-stu-id="945e3-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="945e3-116">Een kopie van Hallo API token duren.</span><span class="sxs-lookup"><span data-stu-id="945e3-116">Take a copy of hello API token.</span></span>

![Een API HockeyApp-token ophalen](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="945e3-118">Open Hallo Microsoft Azure-portal en [een Application Insights-resource maken](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="945e3-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="945e3-119">Type van de toepassing te instellen 'HockeyApp bridge application':</span><span class="sxs-lookup"><span data-stu-id="945e3-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Nieuwe Application Insights-resource](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="945e3-121">U hoeft niet tooset een naam - dit automatisch uit de naam van de HockeyApp Hallo worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="945e3-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="945e3-122">Hallo HockeyApp bridge velden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="945e3-122">hello HockeyApp bridge fields appear.</span></span> 

![Geef de velden brug](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="945e3-124">Voer Hallo HockeyApp token die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="945e3-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="945e3-125">Deze actie wordt gevuld Hallo 'HockeyApp Application' vervolgkeuzemenu met alle HockeyApp-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="945e3-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="945e3-126">Selecteer Hallo een gewenste toouse en volledige Hallo overige Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="945e3-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="945e3-127">Open de nieuwe resource Hallo.</span><span class="sxs-lookup"><span data-stu-id="945e3-127">Open hello new resource.</span></span> 

<span data-ttu-id="945e3-128">Houd er rekening mee dat Hallo gegevens duurt even voordat toostart stromende.</span><span class="sxs-lookup"><span data-stu-id="945e3-128">Note that hello data takes a while toostart flowing.</span></span>

![Application Insights-resource wachten op gegevens](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="945e3-130">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="945e3-130">That’s it!</span></span> <span data-ttu-id="945e3-131">Aangepaste en tracering verzamelde gegevens in uw app HockeyApp geïnstrumenteerd vanaf dit punt is nu ook beschikbaar tooyou in Hallo Analytics en continue Export functies van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="945e3-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="945e3-132">Laten we kort Bekijk elk van deze functies nu beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="945e3-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="945e3-133">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="945e3-133">Analytics</span></span>
<span data-ttu-id="945e3-134">Analytics is een krachtig hulpmiddel voor ad-hoc query's naar uw gegevens, zodat u toodiagnose en analyseren van uw Telemetrie en snel hoofdoorzaken en patronen te detecteren.</span><span class="sxs-lookup"><span data-stu-id="945e3-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytische gegevens](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="945e3-136">Meer informatie over Analytics</span><span class="sxs-lookup"><span data-stu-id="945e3-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="945e3-137">Continue export</span><span class="sxs-lookup"><span data-stu-id="945e3-137">Continuous export</span></span>
<span data-ttu-id="945e3-138">Continue Export kunt u tooexport uw gegevens in een Azure Blob Storage-container.</span><span class="sxs-lookup"><span data-stu-id="945e3-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="945e3-139">Dit is erg handig als u tookeep uw gegevens langer dan de bewaarperiode Hallo die momenteel worden aangeboden door Application Insights hebt.</span><span class="sxs-lookup"><span data-stu-id="945e3-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="945e3-140">U kunt bewaren Hallo gegevens in blob-opslag, verwerken in een SQL-Database of de oplossing van uw voorkeur gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="945e3-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="945e3-141">Meer informatie over de continue Export</span><span class="sxs-lookup"><span data-stu-id="945e3-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="945e3-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="945e3-142">Next steps</span></span>
* [<span data-ttu-id="945e3-143">Analytics tooyour gegevens toepassen</span><span class="sxs-lookup"><span data-stu-id="945e3-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

