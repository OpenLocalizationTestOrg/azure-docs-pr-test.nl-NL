---
title: Android SDK-integratie voor Azure Mobile Engagement
description: "Hierin wordt beschreven hoe u Azure Mobile Engagement SDK is geïntegreerd in de Android-apps"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="fa507-103">Android SDK-integratie voor Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fa507-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa507-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="fa507-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="fa507-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fa507-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="fa507-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fa507-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="fa507-107">Android</span><span class="sxs-lookup"><span data-stu-id="fa507-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="fa507-108">Dit document beschrijft alle integratie en configuratie van opties beschikbaar voor het Azure Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="fa507-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa507-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa507-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="fa507-110">Geavanceerde functies</span><span class="sxs-lookup"><span data-stu-id="fa507-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="fa507-111">Rapportagefuncties</span><span class="sxs-lookup"><span data-stu-id="fa507-111">Reporting Features</span></span>
<span data-ttu-id="fa507-112">U kunt deze functies kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fa507-112">You can add these features:</span></span>

1. [<span data-ttu-id="fa507-113">Geavanceerde opties voor rapportage</span><span class="sxs-lookup"><span data-stu-id="fa507-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="fa507-114">Locatie rapportage-opties</span><span class="sxs-lookup"><span data-stu-id="fa507-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="fa507-115">Geavanceerde configuratieopties</span><span class="sxs-lookup"><span data-stu-id="fa507-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="fa507-116">Meldingen:</span><span class="sxs-lookup"><span data-stu-id="fa507-116">Notifications:</span></span>
[<span data-ttu-id="fa507-117">Het bereik (meldingen) integreren in uw Android-app</span><span class="sxs-lookup"><span data-stu-id="fa507-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="fa507-118">Google Cloud Messaging (GCM): [GCM integreren met Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="fa507-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="fa507-119">Amazon Device Messaging (ADM): [ADM integreren met Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="fa507-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="fa507-120">Tag plan implementatie:</span><span class="sxs-lookup"><span data-stu-id="fa507-120">Tag plan implementation:</span></span>
[<span data-ttu-id="fa507-121">Het gebruik van de geavanceerde Mobile Engagement tags API in uw Android-app</span><span class="sxs-lookup"><span data-stu-id="fa507-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="fa507-122">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="fa507-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="fa507-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="fa507-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="fa507-124">Herstel van een crash die zelden optreden kan bij het aanroepen van `EngagementAgentUtils.isInDedicatedEngagementProcess`, die ook wordt gebruikt door de `EngagementApplication` klasse.</span><span class="sxs-lookup"><span data-stu-id="fa507-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="fa507-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="fa507-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="fa507-126">Android 8-ondersteuning (vorige versies van de SDK werken niet in Android 8).</span><span class="sxs-lookup"><span data-stu-id="fa507-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="fa507-127">Er is geen meer afhankelijkheid van ondersteuningsbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fa507-127">No more dependency on support library.</span></span>
* <span data-ttu-id="fa507-128">Verwijder `EngagementFragmentActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="fa507-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="fa507-129">Vanwege [achtergrond uitvoering limieten](https://developer.android.com/preview/features/background.html) op Android 8 logboeken op de achtergrond kunnen worden uitgesteld totdat de gebruiker werkt met het apparaat, wordt dit een invloed hebben op campagne Push **geleverd** en **Systeemmelding weergegeven** statistieken wordt uitgesteld als de slaapstand van het apparaat (de melding wordt nog steeds worden weergegeven, wordt ring en Trillen in realtime zonder problemen).</span><span class="sxs-lookup"><span data-stu-id="fa507-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="fa507-130">Vanwege [achtergrond locatie limieten](https://developer.android.com/preview/features/background-location-limits.html), de locatie op de achtergrond wordt niet regelmatig bijgewerkt op Android 8 realtime.</span><span class="sxs-lookup"><span data-stu-id="fa507-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="fa507-131">Zie voor alle versies, de [voltooien releaseopmerkingen](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="fa507-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="fa507-132">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="fa507-132">Upgrade procedures</span></span>
<span data-ttu-id="fa507-133">Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, raadpleegt u [Procedures Upgrade](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="fa507-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

