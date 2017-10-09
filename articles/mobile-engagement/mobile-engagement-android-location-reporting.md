---
title: aaaLocation rapportage voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven hoe tooconfigure locatie rapportage voor Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="ea233-103">Locatie rapportage voor Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="ea233-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea233-104">Android</span><span class="sxs-lookup"><span data-stu-id="ea233-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="ea233-105">Dit onderwerp wordt beschreven hoe toodo locatie rapportage voor uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ea233-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea233-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ea233-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="ea233-107">Locatierapportage</span><span class="sxs-lookup"><span data-stu-id="ea233-107">Location reporting</span></span>
<span data-ttu-id="ea233-108">Als u wilt dat locaties toobe gerapporteerd, moet u tooadd een paar regels van configuratie (tussen Hallo `<application>` en `</application>` labels).</span><span class="sxs-lookup"><span data-stu-id="ea233-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="ea233-109">Vertraagde locatiemelding</span><span class="sxs-lookup"><span data-stu-id="ea233-109">Lazy area location reporting</span></span>
<span data-ttu-id="ea233-110">Vertraagde locatiemelding kan reporting Hallo land, streek en plaats die zijn gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="ea233-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="ea233-111">Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="ea233-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="ea233-112">Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="ea233-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="ea233-113">Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft dus lage impact op de accu Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea233-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="ea233-114">Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten.</span><span class="sxs-lookup"><span data-stu-id="ea233-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="ea233-115">Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="ea233-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="ea233-116">U inschakelen vertraagde locatie voor rapportage met Hallo configuratie die eerder is vermeld in deze procedure:</span><span class="sxs-lookup"><span data-stu-id="ea233-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea233-117">U moet ook een machtiging locatie toospecify.</span><span class="sxs-lookup"><span data-stu-id="ea233-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="ea233-118">Deze code gebruikt ``COARSE`` machtiging:</span><span class="sxs-lookup"><span data-stu-id="ea233-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="ea233-119">Als uw app nodig is, kunt u ``ACCESS_FINE_LOCATION`` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="ea233-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="ea233-120">Rapportage van realtime locatie</span><span class="sxs-lookup"><span data-stu-id="ea233-120">Real-time location reporting</span></span>
<span data-ttu-id="ea233-121">Rapportage van realtime locatie kunt reporting Hallo-breedtegraad en lengtegraad die zijn gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="ea233-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="ea233-122">Dit type locatie reporting gebruikt standaard alleen netwerklocaties, op basis van de cel-ID of Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="ea233-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="ea233-123">Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (bijvoorbeeld tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="ea233-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="ea233-124">Realtime locaties zijn *niet* toocompute statistieken gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ea233-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="ea233-125">Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="ea233-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="ea233-126">tooenable realtime locatie reporting, een regel toevoegen van code toowhere u Hallo Engagement verbindingsreeks instellen in Hallo launcher activiteit.</span><span class="sxs-lookup"><span data-stu-id="ea233-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="ea233-127">Hallo resultaat lijkt op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ea233-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="ea233-128">GPS op basis van rapportage</span><span class="sxs-lookup"><span data-stu-id="ea233-128">GPS based reporting</span></span>
<span data-ttu-id="ea233-129">Rapportage van realtime locatie alleen gebruikt standaard locaties op het netwerk.</span><span class="sxs-lookup"><span data-stu-id="ea233-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="ea233-130">tooenable hello op basis van een GPS-locaties die ver nauwkeurigere, gebruiken Hallo configuration-object:</span><span class="sxs-lookup"><span data-stu-id="ea233-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea233-131">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="ea233-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="ea233-132">Achtergrond rapportage</span><span class="sxs-lookup"><span data-stu-id="ea233-132">Background reporting</span></span>
<span data-ttu-id="ea233-133">Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (bijvoorbeeld tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="ea233-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="ea233-134">tooenable hello reporting ook op de achtergrond, gebruik dit configuratieobject:</span><span class="sxs-lookup"><span data-stu-id="ea233-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="ea233-135">Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen locaties op het netwerk worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.</span><span class="sxs-lookup"><span data-stu-id="ea233-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="ea233-136">Als het Hallo-gebruikers hun apparaat opnieuw is opgestart, is Hallo achtergrond locatie rapport gestopt.</span><span class="sxs-lookup"><span data-stu-id="ea233-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="ea233-137">toomake automatisch opnieuw opgestart tijdens het opstarten, voeg deze code.</span><span class="sxs-lookup"><span data-stu-id="ea233-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="ea233-138">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="ea233-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="ea233-139">Android M machtigingen</span><span class="sxs-lookup"><span data-stu-id="ea233-139">Android M permissions</span></span>
<span data-ttu-id="ea233-140">Vanaf Android M, sommige machtigingen tijdens runtime worden beheerd en goedkeuring van een gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="ea233-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="ea233-141">Als u Android-API-niveau 23 richt, zijn Hallo runtime machtigingen standaard uitgeschakeld voor nieuwe installaties van de app.</span><span class="sxs-lookup"><span data-stu-id="ea233-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="ea233-142">Anders zijn ze standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ea233-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="ea233-143">U kunt in-of uitschakelen die machtigingen in Hallo apparaat instellingen.</span><span class="sxs-lookup"><span data-stu-id="ea233-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="ea233-144">Het uitschakelen van machtigingen in Hallo Systeemmenu is funest achtergrondprocessen Hallo Hallo-toepassing, dat is het systeemgedrag van een, en heeft geen invloed op de mogelijkheid tooreceive push op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="ea233-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="ea233-145">In de context van de Hallo van Mobile Engagement locatie reporting, zijn Hallo-machtigingen die moeten worden goedgekeurd tijdens runtime:</span><span class="sxs-lookup"><span data-stu-id="ea233-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="ea233-146">Machtigingen van Hallo-gebruiker met een dialoogvenster standaardbesturingssysteem aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ea233-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="ea233-147">Als de gebruiker Hallo goedkeurt, laat u weten ``EngagementAgent`` tootake die in aanmerking in realtime wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ea233-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="ea233-148">Hallo wijziging is anders verwerkte Hallo volgende tijd Hallo gebruiker gestart Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="ea233-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="ea233-149">Hier volgt een voorbeeld code toouse in een activiteit van uw toorequest Toepassingsmachtigingen en voorwaarts Hallo resultaat als positief te``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="ea233-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
