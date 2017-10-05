---
title: HockeyApp-gegevens in Azure Application Insights verkennen | Microsoft Docs
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
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="6ef95-103">HockeyApp-gegevens in Application Insights verkennen</span><span class="sxs-lookup"><span data-stu-id="6ef95-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="6ef95-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is het aanbevolen platform voor het bewaken van live desktop- en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="6ef95-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="6ef95-105">U kunt van HockeyApp, aangepaste verzenden en traceren telemetrie in om te controleren van het gebruik en helpt bij de diagnose (naast het ophalen van crashgegevens).</span><span class="sxs-lookup"><span data-stu-id="6ef95-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="6ef95-106">Deze stroom telemetrie kan worden opgevraagd met de krachtige [Analytics](app-insights-analytics.md) functie van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ef95-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6ef95-107">Bovendien kunt u [exporteren van het aangepaste en telemetrie traceren](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="6ef95-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="6ef95-108">Als u wilt dat deze functies, moet u brug waarlangs HockeyApp aangepaste gegevens naar Application Insights doorstuurt instellen.</span><span class="sxs-lookup"><span data-stu-id="6ef95-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="6ef95-109">De app HockeyApp brug</span><span class="sxs-lookup"><span data-stu-id="6ef95-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="6ef95-110">De HockeyApp brug App is de core-functie waarmee u toegang tot uw aangepaste HockeyApp en in Application Insights-tracetelemetrie via de analyses en continue Export-functies.</span><span class="sxs-lookup"><span data-stu-id="6ef95-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="6ef95-111">Aangepaste en tracering verzamelde gebeurtenissen per HockeyApp na het maken van de HockeyApp Bridge App toegankelijk is vanaf deze functies.</span><span class="sxs-lookup"><span data-stu-id="6ef95-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="6ef95-112">Kijken hoe u een van deze Apps Bridge instelt.</span><span class="sxs-lookup"><span data-stu-id="6ef95-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="6ef95-113">Open in de HockeyApp, accountinstellingen, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="6ef95-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="6ef95-114">Een nieuw token maken of een bestaande hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ef95-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="6ef95-115">De minimale rechten vereist zijn 'alleen-lezen'.</span><span class="sxs-lookup"><span data-stu-id="6ef95-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="6ef95-116">Een kopie van de API-token te nemen.</span><span class="sxs-lookup"><span data-stu-id="6ef95-116">Take a copy of the API token.</span></span>

![Een API HockeyApp-token ophalen](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="6ef95-118">Open de Microsoft Azure portal en [een Application Insights-resource maken](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6ef95-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="6ef95-119">Toepassingstype ingesteld op 'HockeyApp bridge application':</span><span class="sxs-lookup"><span data-stu-id="6ef95-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![Nieuwe Application Insights-resource](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="6ef95-121">U hoeft niet in te stellen van een naam - wordt deze automatisch worden ingesteld van de HockeyApp-naam.</span><span class="sxs-lookup"><span data-stu-id="6ef95-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="6ef95-122">De HockeyApp bridge velden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6ef95-122">The HockeyApp bridge fields appear.</span></span> 

![Geef de velden brug](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="6ef95-124">Voer de HockeyApp-token dat u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="6ef95-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="6ef95-125">Deze actie wordt het vervolgkeuzemenu 'HockeyApp Application' met alle HockeyApp-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6ef95-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="6ef95-126">Selecteer de gateway die u wilt gebruiken en voltooi de rest van de velden.</span><span class="sxs-lookup"><span data-stu-id="6ef95-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="6ef95-127">Open de nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="6ef95-127">Open the new resource.</span></span> 

<span data-ttu-id="6ef95-128">Houd er rekening mee dat de gegevens bij te starten waarbij de neemt.</span><span class="sxs-lookup"><span data-stu-id="6ef95-128">Note that the data takes a while to start flowing.</span></span>

![Application Insights-resource wachten op gegevens](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="6ef95-130">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="6ef95-130">That’s it!</span></span> <span data-ttu-id="6ef95-131">Aangepaste en tracering verzamelde gegevens in uw app HockeyApp geïnstrumenteerd vanaf dit punt is nu ook beschikbaar in de analyses en continue Export functies van Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6ef95-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="6ef95-132">Laten we kort Bekijk elk van deze functies nu beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="6ef95-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="6ef95-133">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="6ef95-133">Analytics</span></span>
<span data-ttu-id="6ef95-134">Analytics is een krachtig hulpprogramma ad hoc-query's van uw gegevens, zodat u kunt onderzoeken en analyseren van uw Telemetrie en snel hoofdoorzaken en patronen te detecteren.</span><span class="sxs-lookup"><span data-stu-id="6ef95-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytische gegevens](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="6ef95-136">Meer informatie over Analytics</span><span class="sxs-lookup"><span data-stu-id="6ef95-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="6ef95-137">Continue export</span><span class="sxs-lookup"><span data-stu-id="6ef95-137">Continuous export</span></span>
<span data-ttu-id="6ef95-138">Continue Export kunt u uw gegevens exporteren naar een Azure Blob Storage-container.</span><span class="sxs-lookup"><span data-stu-id="6ef95-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="6ef95-139">Dit is handig als u nodig hebt om uw gegevens langer dan de bewaarperiode die momenteel worden aangeboden door Application Insights te houden.</span><span class="sxs-lookup"><span data-stu-id="6ef95-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="6ef95-140">U kunt dat de gegevens in blob-opslag, in een SQL-Database of de oplossing van uw voorkeur gegevensopslag worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6ef95-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="6ef95-141">Meer informatie over de continue Export</span><span class="sxs-lookup"><span data-stu-id="6ef95-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="6ef95-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ef95-142">Next steps</span></span>
* [<span data-ttu-id="6ef95-143">Analytics toepassen op uw gegevens</span><span class="sxs-lookup"><span data-stu-id="6ef95-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)

