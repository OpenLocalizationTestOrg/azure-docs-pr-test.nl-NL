---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="f644f-103">Hoe tooIntegrate Engagement voor Android</span><span class="sxs-lookup"><span data-stu-id="f644f-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f644f-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f644f-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="f644f-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f644f-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f644f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f644f-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f644f-107">Android</span><span class="sxs-lookup"><span data-stu-id="f644f-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="f644f-108">Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f644f-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f644f-109">Het minimale Android SDK-API-niveau moet 10 of hoger (Android 2.3.3 of hoger).</span><span class="sxs-lookup"><span data-stu-id="f644f-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="f644f-110">Hallo stappen te volgen zijn dat onvoldoende tooactivates Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals.</span><span class="sxs-lookup"><span data-stu-id="f644f-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f644f-111">rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement in uw Android-API tagging geavanceerde](mobile-engagement-android-use-engagement-api.md) sinds deze statistieken zijn afhankelijk van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f644f-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="f644f-112">Hallo Engagement SDK en service insluiten in uw Android-project</span><span class="sxs-lookup"><span data-stu-id="f644f-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="f644f-113">Download de Android SDK van Hallo [hier](https://aka.ms/vq9mfn) ophalen `mobile-engagement-VERSION.jar` naar Hallo `libs` map van uw Android-project (de map libs Hallo maken als deze nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="f644f-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f644f-114">Als u uw toepassingspakket met ProGuard bouwt, moet u tookeep sommige klassen.</span><span class="sxs-lookup"><span data-stu-id="f644f-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="f644f-115">U kunt na configuratie codefragment hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f644f-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="f644f-116">-openbare klasse houden * breidt android.os.IInterface-klasse com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {houden</span><span class="sxs-lookup"><span data-stu-id="f644f-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="f644f-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="f644f-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="f644f-118">Geef de verbindingsreeks Engagement door aanroepen Hallo methode in Hallo launcher activiteit te volgen:</span><span class="sxs-lookup"><span data-stu-id="f644f-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f644f-119">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f644f-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="f644f-120">Indien deze ontbreken, Hallo volgende Android machtigingen toevoegen (voordat Hallo `<application>` tag):</span><span class="sxs-lookup"><span data-stu-id="f644f-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="f644f-121">Toevoegen van de volgende sectie hello (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="f644f-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="f644f-122">Wijziging `<Your application name>` door Hallo-naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f644f-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="f644f-123">Hallo `android:label` kenmerk kunt u toochoose Hallo naam Hallo Engagement service die toohello eindgebruikers in 'Services wordt uitgevoerd' welkomstscherm van hun telefoonnummer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f644f-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="f644f-124">Het is aanbevolen tooset dit kenmerk te`"<Your application name>Service"` (bijvoorbeeld `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="f644f-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="f644f-125">Geven Hallo `android:process` kenmerk zorgt ervoor dat Hallo Engagement service wordt uitgevoerd in een eigen proces (Engagement uitgevoerd in dezelfde verwerken als uw toepassing wordt Controleer uw main/UI-thread mogelijk minder goed Hallo).</span><span class="sxs-lookup"><span data-stu-id="f644f-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="f644f-126">Alle code die u in plaatsen `Application.onCreate()` en andere retouraanroepen toepassing wordt uitgevoerd voor de processen van uw toepassing, met inbegrip van Hallo Engagement service.</span><span class="sxs-lookup"><span data-stu-id="f644f-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="f644f-127">Er kunnen ongewenste neveneffecten (zoals overbodige geheugentoewijzingen en threads in Hallo Engagement proces, dubbele broadcast ontvangers of services).</span><span class="sxs-lookup"><span data-stu-id="f644f-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="f644f-128">Als u negeren `Application.onCreate()`, het is aanbevolen tooadd Hallo volgende codefragment aan Hallo begin van uw `Application.onCreate()` functie:</span><span class="sxs-lookup"><span data-stu-id="f644f-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="f644f-129">U kunt doen Hallo hetzelfde geldt voor `Application.onTerminate()`, `Application.onLowMemory()` en `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="f644f-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="f644f-130">U kunt ook uitbreiden `EngagementApplication` in plaats van het uitbreiden van `Application`: Hallo callback `Application.onCreate()` Hallo proces controleren en aanroepen `Application.onApplicationProcessCreate()` alleen als het huidige proces Hallo niet Hallo één hosting Hallo Engagement service, hello gelden dezelfde regels voor Hallo andere retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="f644f-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="f644f-131">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="f644f-132">Aanbevolen methode: overbelasting uw `Activity` klassen</span><span class="sxs-lookup"><span data-stu-id="f644f-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="f644f-133">In de volgorde tooactivate Hallo rapport van alle Hallo logboeken vereist voor Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken, hebt u alleen toomake alle uw `*Activity` onderliggende klassen overnemen Hallo overeenkomt `Engagement*Activity` klassen (bijvoorbeeld als uw verouderde activiteit breidt `ListActivity`, zorg er breidt `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="f644f-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="f644f-134">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f644f-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="f644f-135">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f644f-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="f644f-136">Wanneer u `EngagementListActivity` of `EngagementExpandableListActivity`, zorg ervoor dat alle aanroepen te`requestWindowFeature(...);` voor Hallo-aanroep is uitgevoerd, te`super.onCreate(...);`, anders een crash wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f644f-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="f644f-137">U vindt deze klassen in Hallo `src` map, en kunt kopiëren naar uw project.</span><span class="sxs-lookup"><span data-stu-id="f644f-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="f644f-138">Hallo klassen bevinden zich ook in Hallo **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="f644f-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="f644f-139">Alternatieve methode: call `startActivity()` en `endActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="f644f-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="f644f-140">Als u niet kunt of toooverload niet wilt dat uw `Activity` klassen, u kunt in plaats daarvan starten en beëindigen van uw activiteiten door aan te roepen `EngagementAgent`van methoden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="f644f-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f644f-141">Hallo Android SDK wordt nooit aangeroepen door Hallo `endActivity()` methode, zelfs als de toepassing hello is gesloten (voor Android toepassingen zijn daadwerkelijk nooit gesloten).</span><span class="sxs-lookup"><span data-stu-id="f644f-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="f644f-142">Het is dus *maximaal* toocall Hallo aanbevolen `startActivity()` methode in Hallo `onResume` retouraanroep van *alle* uw activiteiten en Hallo `endActivity()` methode in Hallo `onPause()` retouraanroep van *alle* uw activiteiten.</span><span class="sxs-lookup"><span data-stu-id="f644f-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="f644f-143">Dit is Hallo alleen manier toobe ervoor dat sessies niet wordt gelekt.</span><span class="sxs-lookup"><span data-stu-id="f644f-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="f644f-144">Als een sessie is gelekt, verbreekt Hallo Engagement service nooit van back-end Hallo Engagement (omdat Hallo service verbonden blijft als een sessie in behandeling is).</span><span class="sxs-lookup"><span data-stu-id="f644f-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="f644f-145">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f644f-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="f644f-146">In dit voorbeeld vergelijkbaar toohello `EngagementActivity` klasse en varianten, waarvan de broncode wordt verstrekt in Hallo `src` map.</span><span class="sxs-lookup"><span data-stu-id="f644f-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="f644f-147">Test</span><span class="sxs-lookup"><span data-stu-id="f644f-147">Test</span></span>
<span data-ttu-id="f644f-148">Nu uw integratie controleren door te voeren van uw mobiele app in een emulator of het apparaat en verifiëren van de registratie van een sessie op het tabblad Hallo-Monitor.</span><span class="sxs-lookup"><span data-stu-id="f644f-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="f644f-149">de volgende secties Hallo zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="f644f-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="f644f-150">Locatierapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-150">Location reporting</span></span>
<span data-ttu-id="f644f-151">Als u wilt dat locaties toobe gerapporteerd, moet u tooadd een paar regels van configuratie (tussen Hallo `<application>` en `</application>` labels).</span><span class="sxs-lookup"><span data-stu-id="f644f-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="f644f-152">Vertraagde locatiemelding</span><span class="sxs-lookup"><span data-stu-id="f644f-152">Lazy area location reporting</span></span>
<span data-ttu-id="f644f-153">Vertraagde locatiemelding kunt tooreport Hallo land, streek en plaats die zijn gekoppeld toodevices.</span><span class="sxs-lookup"><span data-stu-id="f644f-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="f644f-154">Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="f644f-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="f644f-155">Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="f644f-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="f644f-156">Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft slechts weinig dus (geen toosay geen) impact op de accu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f644f-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="f644f-157">Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten.</span><span class="sxs-lookup"><span data-stu-id="f644f-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="f644f-158">Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="f644f-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="f644f-159">tooenable vertraagde locatie voor rapportage, u kunt dit doen met behulp van Hallo configuratie die eerder is vermeld in deze procedure:</span><span class="sxs-lookup"><span data-stu-id="f644f-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f644f-160">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="f644f-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f644f-161">Of u kunt blijven gebruiken ``ACCESS_FINE_LOCATION`` als u al in uw toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f644f-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="f644f-162">Rapportage van realtime locatie</span><span class="sxs-lookup"><span data-stu-id="f644f-162">Real time location reporting</span></span>
<span data-ttu-id="f644f-163">Rapportage van realtime locatie kunt tooreport Hallo breedtegraad en lengtegraad gekoppeld toodevices.</span><span class="sxs-lookup"><span data-stu-id="f644f-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="f644f-164">Standaard alleen gebruik van dit type locatie reporting netwerklocaties (gebaseerd op de cel-ID of Wi-Fi), en Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="f644f-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="f644f-165">Realtime-locaties zijn *niet* toocompute statistieken gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f644f-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="f644f-166">Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="f644f-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="f644f-167">tooenable realtime locatie rapportage, u kunt dit doen met behulp van Hallo configuratie die eerder is vermeld in deze procedure:</span><span class="sxs-lookup"><span data-stu-id="f644f-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f644f-168">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="f644f-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f644f-169">Of u kunt blijven gebruiken ``ACCESS_FINE_LOCATION`` als u al in uw toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f644f-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="f644f-170">GPS op basis van rapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-170">GPS based reporting</span></span>
<span data-ttu-id="f644f-171">Rapportage van realtime locatie alleen gebruikt standaard op basis van netwerklocaties.</span><span class="sxs-lookup"><span data-stu-id="f644f-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="f644f-172">tooenable hello gebruik van GPS op basis van locaties (die veel meer nauwkeurige), gebruikt u Hallo configuration-object:</span><span class="sxs-lookup"><span data-stu-id="f644f-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f644f-173">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="f644f-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="f644f-174">Achtergrond rapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-174">Background reporting</span></span>
<span data-ttu-id="f644f-175">Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="f644f-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="f644f-176">tooenable hello ook op de achtergrond, worden gebruikt door reporting Hallo configuration-object:</span><span class="sxs-lookup"><span data-stu-id="f644f-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="f644f-177">Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen op basis van netwerklocaties worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.</span><span class="sxs-lookup"><span data-stu-id="f644f-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="f644f-178">Hallo achtergrond locatie rapport wordt gestopt als Hallo gebruiker het apparaat opnieuw is opgestart, kunt u deze automatisch opnieuw opgestart tijdens het opstarten toomake toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f644f-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="f644f-179">U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="f644f-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="f644f-180">Android M machtigingen</span><span class="sxs-lookup"><span data-stu-id="f644f-180">Android M permissions</span></span>
<span data-ttu-id="f644f-181">Vanaf Android M, sommige machtigingen tijdens runtime worden beheerd en moet de goedkeuring van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f644f-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="f644f-182">Hallo runtime machtigingen worden uitgeschakeld voor nieuwe installaties van apps standaard als u Android-API-niveau 23 richt.</span><span class="sxs-lookup"><span data-stu-id="f644f-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="f644f-183">Anders zal het worden standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f644f-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="f644f-184">Hallo-gebruiker kunt in-of uitschakelen die machtigingen in Hallo apparaat instellingen.</span><span class="sxs-lookup"><span data-stu-id="f644f-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="f644f-185">Het uitschakelen van machtigingen van Systeemmenu is funest achtergrondprocessen van de toepassing hello, dit is een systeemgedrag en heeft geen invloed op de mogelijkheid tooreceive push op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="f644f-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="f644f-186">In de context van de Hallo van Mobile Engagement zijn Hallo-machtigingen die moeten worden goedgekeurd tijdens runtime:</span><span class="sxs-lookup"><span data-stu-id="f644f-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="f644f-187">`WRITE_EXTERNAL_STORAGE`(alleen bij Android-API-niveau 23 voor deze doelen)</span><span class="sxs-lookup"><span data-stu-id="f644f-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="f644f-188">Hallo externe opslag wordt alleen gebruikt voor Reach grote afbeelding functie.</span><span class="sxs-lookup"><span data-stu-id="f644f-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="f644f-189">Als u gebruikers vragen over deze machtiging toobe verstoren, kunt u deze verwijderen als u deze gebruikt voor Mobile Engagement alleen maar op Hallo kosten van het uitschakelen van de functie grote afbeelding.</span><span class="sxs-lookup"><span data-stu-id="f644f-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="f644f-190">Voor Hallo locatie functies, moet u machtigingen toouser met een dialoogvenster standaardbesturingssysteem aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f644f-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="f644f-191">Als de gebruiker Hallo goedkeurt, moet u tootell ``EngagementAgent`` tootake die in aanmerking in realtime (anders Hallo wijziging worden verwerkte Hallo volgende tijd Hallo gestart Hallo-Gebruikerstoepassing) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f644f-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="f644f-192">Hier volgt een voorbeeld code toouse in een activiteit van uw toorequest Toepassingsmachtigingen en voorwaarts Hallo resultaat als positief te``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="f644f-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="f644f-193">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-193">Advanced reporting</span></span>
<span data-ttu-id="f644f-194">Eventueel, als u tooreport toepassing specifieke gebeurtenissen, fouten en taken wilt, moet u toouse Hallo Engagement API via de methoden Hallo Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="f644f-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="f644f-195">Een object van deze klasse kan worden opgehaald door de aanroepende Hallo `EngagementAgent.getInstance()` statische methode.</span><span class="sxs-lookup"><span data-stu-id="f644f-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="f644f-196">Hallo Engagement API toouse kunnen alle Engagement geavanceerde mogelijkheden en wordt beschreven in Hallo hoe tooUse de Engagement-API voor Android (en van de technische documentatie Hallo Hallo `EngagementAgent` klasse).</span><span class="sxs-lookup"><span data-stu-id="f644f-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="f644f-197">Geavanceerde configuratie (in AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="f644f-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="f644f-198">Wake-vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="f644f-198">Wake locks</span></span>
<span data-ttu-id="f644f-199">Als u toobe ervoor wilt dat de statistieken worden verzonden in realtime bij gebruik van Wi-Fi of wanneer het welkomstscherm is uitgeschakeld, voegt u Hallo optionele machtiging te volgen:</span><span class="sxs-lookup"><span data-stu-id="f644f-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="f644f-200">Foutrapportage</span><span class="sxs-lookup"><span data-stu-id="f644f-200">Crash report</span></span>
<span data-ttu-id="f644f-201">Als u de foutenrapporten toodisable wilt, voeg deze toe (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="f644f-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="f644f-202">Burst drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="f644f-202">Burst threshold</span></span>
<span data-ttu-id="f644f-203">Standaard Hallo Engagement servicerapporten Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="f644f-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="f644f-204">Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd).</span><span class="sxs-lookup"><span data-stu-id="f644f-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="f644f-205">toodo dus toevoegen (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="f644f-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="f644f-206">Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken).</span><span class="sxs-lookup"><span data-stu-id="f644f-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="f644f-207">Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="f644f-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="f644f-208">Sessietime-out</span><span class="sxs-lookup"><span data-stu-id="f644f-208">Session timeout</span></span>
<span data-ttu-id="f644f-209">Een sessie is beëindigd per 10 standaard, na het Hallo-einde van de laatste activiteit (die doorgaans optreedt, door te drukken Hallo start of Back-sleutel, telefonisch instelling Hallo inactief of door te gaan naar een andere toepassing).</span><span class="sxs-lookup"><span data-stu-id="f644f-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="f644f-210">Dit is tooavoid een sessie-splitsing van elke gebruiker tijd Hallo afsluiten en toohello toepassing zeer snel terug (dit kan gebeuren wanneer hij een installatiekopie worden opgepikt controleren een melding, enz.).</span><span class="sxs-lookup"><span data-stu-id="f644f-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="f644f-211">U kunt deze parameter toomodify.</span><span class="sxs-lookup"><span data-stu-id="f644f-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="f644f-212">toodo dus toevoegen (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="f644f-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="f644f-213">Melden van logboek uitschakelen</span><span class="sxs-lookup"><span data-stu-id="f644f-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f644f-214">Met behulp van een methodeaanroep van</span><span class="sxs-lookup"><span data-stu-id="f644f-214">Using a method call</span></span>
<span data-ttu-id="f644f-215">Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:</span><span class="sxs-lookup"><span data-stu-id="f644f-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="f644f-216">Deze aanroep is permanent: een gedeelde voorkeuren-bestand wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f644f-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="f644f-217">Als bij het aanroepen van deze functie Engagement actief is, kan 1 minuut voor Hallo service toostop duren.</span><span class="sxs-lookup"><span data-stu-id="f644f-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="f644f-218">Maar deze won't start Hallo-service op alle Hallo volgende keer dat u de toepassing hello starten.</span><span class="sxs-lookup"><span data-stu-id="f644f-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="f644f-219">U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `true`.</span><span class="sxs-lookup"><span data-stu-id="f644f-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="f644f-220">Integratie in uw eigen`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="f644f-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="f644f-221">In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f644f-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="f644f-222">U kunt Engagement toouse uw voorkeuren bestand (met de gewenste modus Hallo) configureren in Hallo `AndroidManifest.xml` het bestand met `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="f644f-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="f644f-223">Hallo `engagement:agent:settings:name` sleutel is de naam van de gebruikte toodefine Hallo van Hallo gedeelde voorkeurenbestand.</span><span class="sxs-lookup"><span data-stu-id="f644f-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="f644f-224">Hallo `engagement:agent:settings:mode` sleutel gebruikte toodefine Hallo modus van Hallo gedeelde voorkeurenbestand is, moet u Hallo dezelfde modus als in uw `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f644f-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="f644f-225">Hallo-modus moet worden doorgegeven als een getal: als u een combinatie van constante vlaggen in uw code gebruikt, controleert u Hallo totale waarde.</span><span class="sxs-lookup"><span data-stu-id="f644f-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="f644f-226">Engagement altijd gebruik Hallo `engagement:key` Booleaanse sleutel binnen Hallo voorkeurenbestand voor het beheren van deze instelling.</span><span class="sxs-lookup"><span data-stu-id="f644f-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="f644f-227">Hallo volgende voorbeeld van `AndroidManifest.xml` toont Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="f644f-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="f644f-228">Vervolgens kunt u toevoegen een `CheckBoxPreference` in de indeling van uw voorkeur zoals Hallo volgt:</span><span class="sxs-lookup"><span data-stu-id="f644f-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
