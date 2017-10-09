---
title: aaaAzure Mobile Engagement Troubleshooting Guide - analyses
description: Het oplossen van problemen Analytics, bewaking, segmentering en Dashboard in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="c20a9-103">Gids voor probleemoplossing voor problemen die Analytics, bewaking, segmentering en Dashboard</span><span class="sxs-lookup"><span data-stu-id="c20a9-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="c20a9-104">Hallo volgen mogelijke problemen optreden bij hoe Azure Mobile Engagement wordt informatie verzameld over uw toepassingen, apparaten en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c20a9-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="c20a9-105">Ontbrekende/uitgestelde informatie</span><span class="sxs-lookup"><span data-stu-id="c20a9-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="c20a9-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="c20a9-106">Issue</span></span>
* <span data-ttu-id="c20a9-107">Informatie is in die voorkomen in Analytics, segmentering of Dashboard vertraagd.</span><span class="sxs-lookup"><span data-stu-id="c20a9-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="c20a9-108">Er ontbreekt informatie in de bewaking.</span><span class="sxs-lookup"><span data-stu-id="c20a9-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="c20a9-109">Er ontbreekt informatie in Analytics, segmentering of Dashboard.</span><span class="sxs-lookup"><span data-stu-id="c20a9-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="c20a9-110">Roept segmentering beperkt.</span><span class="sxs-lookup"><span data-stu-id="c20a9-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="c20a9-111">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c20a9-111">Causes</span></span>
* <span data-ttu-id="c20a9-112">Kunt u Hallo Analytics API, Monitor-API en segmenten API toosee als gegevens u ontbreekt in Hallo UI zichtbaar via Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="c20a9-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="c20a9-113">Als hello Azure Mobile Engagement SDK is niet correct worden geïntegreerd in uw app niet u de informatie kunnen toosee in Hallo Analytics, segmentering, bewaking of Dashboards.</span><span class="sxs-lookup"><span data-stu-id="c20a9-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="c20a9-114">Segmenten kunnen niet worden gewijzigd als ze zijn gemaakt, segmenten kunnen alleen worden 'gekloonde' (overgenomen) of 'vernietigd' (verwijderd).</span><span class="sxs-lookup"><span data-stu-id="c20a9-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="c20a9-115">Segmenten kunnen alleen 10 criteria bevatten.</span><span class="sxs-lookup"><span data-stu-id="c20a9-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="c20a9-116">Hallo aanbevolen manier tootest ontbreken gegevens van bewaking is toosetup een testapparaat, verwijderen en/of Hallo-app installeren op Hallo testapparaat.</span><span class="sxs-lookup"><span data-stu-id="c20a9-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="c20a9-117">Informatie wordt elke 24 uur vernieuwd voor analyses, segmentering of Dashboards.</span><span class="sxs-lookup"><span data-stu-id="c20a9-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="c20a9-118">Informatie in de nieuwe segmenten mogelijk niet weergegeven tot 24 uur nadat ze zijn gemaakt, zelfs als het Hallo-segment is gebaseerd op eerdere informatie.</span><span class="sxs-lookup"><span data-stu-id="c20a9-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="c20a9-119">Uw analytics gegevens filteren in Hallo UI vindt u voorbeelden alle van dit type ongeacht Hallo-versie van uw app (bijvoorbeeld) "Loopt vast" gefilterd met de naam ziet van versie 1 en versie 2 van uw app).</span><span class="sxs-lookup"><span data-stu-id="c20a9-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="c20a9-120">Hallo is periode voor analyses gebaseerd op Hallo datum in de apparaatinstellingen Hallo gebruikers, zodat een gebruiker waarvan telefoon heeft Hallo datum onjuist ingestelde in Hallo verkeerde periode weergegeven kan.</span><span class="sxs-lookup"><span data-stu-id="c20a9-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="c20a9-121">Er zijn geen gegevens worden geregistreerd wanneer u de knop Hallo serverzijde te 'test' pushes, gegevens alleen worden geregistreerd voor echte pushcampagnes.</span><span class="sxs-lookup"><span data-stu-id="c20a9-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="c20a9-122">Kan items niet vinden in de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="c20a9-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="c20a9-123">Probleem</span><span class="sxs-lookup"><span data-stu-id="c20a9-123">Issue</span></span>
* <span data-ttu-id="c20a9-124">Kan niet op basis van bepaalde ingebouwd in segmenten maken of aangepaste app-gegevens labelen criteria.</span><span class="sxs-lookup"><span data-stu-id="c20a9-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="c20a9-125">Kan niet vinden op bepaalde ingebouwde of aangepaste app-gegevens labelen criteria in Analytics, bewaking of Dashboards.</span><span class="sxs-lookup"><span data-stu-id="c20a9-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="c20a9-126">Hallo-gegevens in Analytics, bewaking, segmentering of Dashboards kunnen niet worden geïnterpreteerd.</span><span class="sxs-lookup"><span data-stu-id="c20a9-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="c20a9-127">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c20a9-127">Causes</span></span>
* <span data-ttu-id="c20a9-128">Sommige items ingebouwde en app-info-codes zijn alleen beschikbaar als push criteria, maar mogelijk niet tooa segment toegevoegd of zichtbaar vanuit Analytics, bewaking of Dashboard.</span><span class="sxs-lookup"><span data-stu-id="c20a9-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="c20a9-129">Voor ingebouwde items en -labels die niet kunnen worden toegevoegd tooa segment app-gegevens, moet u toosetup lijst met doelen criteria in elke campagne tooperform Hallo dezelfde functie uitgevoerd als die gericht is op basis van een segment.</span><span class="sxs-lookup"><span data-stu-id="c20a9-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="c20a9-130">Zie Hallo contextmenu's in Hallo Analytics, bewaking, segmentering en Dashboards secties van hello Azure Mobile Engagement UI voor meer informatie en hoe tooinformation.</span><span class="sxs-lookup"><span data-stu-id="c20a9-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="c20a9-131">Crash het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="c20a9-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="c20a9-132">Probleem</span><span class="sxs-lookup"><span data-stu-id="c20a9-132">Issue</span></span>
* <span data-ttu-id="c20a9-133">Toepassing is vastgelopen verschijnen in Analytics, bewaking of Dashboard.</span><span class="sxs-lookup"><span data-stu-id="c20a9-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="c20a9-134">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c20a9-134">Causes</span></span>
* <span data-ttu-id="c20a9-135">tootroubleshoot toepassing is vastgelopen in Analytics, bewaking of Dashboard weergegeven. Zorg ervoor dat toocheck Hallo release-opmerkingen voor bekende problemen met eerdere versies van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="c20a9-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="c20a9-136">toofurther oplossen toepassing crashes uitvoeren van een gebeurtenis van een testapparaat waarop de toepassing is geïnstalleerd en uw apparaat-ID in de sectie Hallo 'Monitor – gebeurtenissen' Hallo Azure Mobile Engagement-gebruikersinterface worden opgezocht.</span><span class="sxs-lookup"><span data-stu-id="c20a9-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="c20a9-137">Vervolgens Hallo-gebeurtenis die wordt veroorzaakt door uw toepassing toocrash uitvoeren en aanvullende gegevens in de sectie 'Monitor – Crash' hello Azure Mobile Engagement UI Hallo opzoeken.</span><span class="sxs-lookup"><span data-stu-id="c20a9-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

