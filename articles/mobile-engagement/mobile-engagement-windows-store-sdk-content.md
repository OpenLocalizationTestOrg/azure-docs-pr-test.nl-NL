---
title: Windows universele Apps SDK-inhoud
description: Meer informatie over de inhoud van de Windows universele Apps SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="0b0c6-103">Windows universele Apps SDK-inhoud</span><span class="sxs-lookup"><span data-stu-id="0b0c6-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="0b0c6-104">Dit document bevat en beschrijft de inhoud die is geïmplementeerd door de SDK in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="0b0c6-105">De `/Resources` map</span><span class="sxs-lookup"><span data-stu-id="0b0c6-105">The `/Resources` folder</span></span>
<span data-ttu-id="0b0c6-106">Deze map bevat alle resources die behoeften van de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="0b0c6-107">U kunt deze aanpassen aan uw app ook aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="0b0c6-108">`EngagementConfiguration.xml`: De Mobile Engagement-configuratiebestand, dit is waar u de Mobile Engagement-instellingen (Mobile Engagement-verbindingsreeks, rapport crash...) kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="0b0c6-109">de map/HTML</span><span class="sxs-lookup"><span data-stu-id="0b0c6-109">/html folder</span></span>
* <span data-ttu-id="0b0c6-110">`EngagementNotification.html`: De `Notification` webontwerp weergave html voor in-app-banner.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="0b0c6-111">`EngagementAnnouncement.html`: De `Announcement` webontwerp weergave html voor in-app-verspreide weergaven.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="0b0c6-112">de map/images</span><span class="sxs-lookup"><span data-stu-id="0b0c6-112">/images folder</span></span>
* <span data-ttu-id="0b0c6-113">`EngagementIconNotification.png`: Het merk-pictogram weergegeven aan de linkerkant van een melding vervangen deze door uw merk-pictogram.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="0b0c6-114">`EngagementIconOk.png`: De `Ok` pictogram reach inhoudspagina's voor de knop validatie of actie.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="0b0c6-115">`EngagementIconNOK.png`: De `NOK` pictogram dat wordt gebruikt wanneer de knop validatie reach inhoudspagina's is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="0b0c6-116">`EngagementIconClose.png`: De `Close` pictogram van de reach-meldingen en de inhoud voor de knop sluiten.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="0b0c6-117">/overlay map</span><span class="sxs-lookup"><span data-stu-id="0b0c6-117">/overlay folder</span></span>
* <span data-ttu-id="0b0c6-118">`EngagementPageOverlay.cs`: De pagina overlay verantwoordelijk voor het toevoegen van de Engagement-app-gebruikersinterface voor het onderliggende bereiken.</span><span class="sxs-lookup"><span data-stu-id="0b0c6-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

