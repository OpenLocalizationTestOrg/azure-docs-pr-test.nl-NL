---
title: aaaAdvanced rapportageopties voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven hoe toodo reporting toocapture analytics geavanceerde voor Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="140ec-103">Geavanceerde Reporting met Engagement voor Android</span><span class="sxs-lookup"><span data-stu-id="140ec-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="140ec-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="140ec-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="140ec-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="140ec-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="140ec-106">iOS</span><span class="sxs-lookup"><span data-stu-id="140ec-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="140ec-107">Android</span><span class="sxs-lookup"><span data-stu-id="140ec-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="140ec-108">Dit onderwerp beschrijft aanvullende scenario's voor rapportage in uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="140ec-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="140ec-109">U kunt deze opties toohello app gemaakt in Hallo toepassen [aan de slag](mobile-engagement-android-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="140ec-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="140ec-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="140ec-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="140ec-111">Hallo-zelfstudie u voltooid is opzettelijk direct en eenvoudig, maar er zijn geavanceerde opties die u kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="140ec-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="140ec-112">Wijzigen van uw `Activity` klassen</span><span class="sxs-lookup"><span data-stu-id="140ec-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="140ec-113">In Hallo [zelfstudie aan de slag](mobile-engagement-android-get-started.md), alle moest u toodo toomake is uw `*Activity` subklassen overnemen van Hallo overeenkomt `Engagement*Activity` klassen.</span><span class="sxs-lookup"><span data-stu-id="140ec-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="140ec-114">Bijvoorbeeld, als uw verouderde activiteit uitgebreid `ListActivity`, brengt u deze uitbreiden `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="140ec-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="140ec-115">Wanneer u `EngagementListActivity` of `EngagementExpandableListActivity`, zorg ervoor dat alle aanroepen te`requestWindowFeature(...);` voor Hallo-aanroep is uitgevoerd, te`super.onCreate(...);`, anders een crash plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="140ec-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="140ec-116">U vindt deze klassen in Hallo `src` map, en kunt kopiëren naar uw project.</span><span class="sxs-lookup"><span data-stu-id="140ec-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="140ec-117">Hallo klassen bevinden zich ook in Hallo **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="140ec-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="140ec-118">Alternatieve methode: call `startActivity()` en `endActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="140ec-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="140ec-119">Als u niet kunt of toooverload niet wilt dat uw `Activity` klassen, u kunt in plaats daarvan beginnen en eindigen uw activiteiten door het aanroepen van Hallo `EngagementAgent`van methoden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="140ec-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="140ec-120">Hallo Android SDK wordt nooit aangeroepen door Hallo `endActivity()` methode, zelfs als de toepassing hello is gesloten (voor Android toepassingen zijn nooit gesloten).</span><span class="sxs-lookup"><span data-stu-id="140ec-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="140ec-121">Het is dus *maximaal* toocall Hallo aanbevolen `startActivity()` methode in Hallo `onResume` retouraanroep van *alle* uw activiteiten en Hallo `endActivity()` methode in Hallo `onPause()` retouraanroep van *alle* uw activiteiten.</span><span class="sxs-lookup"><span data-stu-id="140ec-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="140ec-122">Dit is Hallo alleen manier toobe ervoor dat sessies niet gelekt.</span><span class="sxs-lookup"><span data-stu-id="140ec-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="140ec-123">Als een sessie is gelekt, verbreekt Hallo Engagement service back-end Hallo Engagement nooit (omdat Hallo service verbonden blijft als een sessie in behandeling is).</span><span class="sxs-lookup"><span data-stu-id="140ec-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="140ec-124">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="140ec-124">Here is an example:</span></span>

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

<span data-ttu-id="140ec-125">In dit voorbeeld is vergelijkbaar toohello `EngagementActivity` klasse en varianten, waarvan de broncode wordt verstrekt in Hallo `src` map.</span><span class="sxs-lookup"><span data-stu-id="140ec-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="140ec-126">Met behulp van Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="140ec-126">Using Application.onCreate()</span></span>
<span data-ttu-id="140ec-127">Alle code die u in plaatsen `Application.onCreate()` en in andere toepassingen retouraanroepen voor de processen van uw toepassing, met inbegrip van Hallo Engagement service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="140ec-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="140ec-128">Deze mogelijk ongewenste neveneffecten hebben, zoals overbodige geheugentoewijzingen en threads in Hallo Engagement proces, of dubbel broadcast ontvangers of services.</span><span class="sxs-lookup"><span data-stu-id="140ec-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="140ec-129">Als u negeren `Application.onCreate()`, het is raadzaam toe te voegen Hallo volgende codefragment aan Hallo begin van uw `Application.onCreate()` functie:</span><span class="sxs-lookup"><span data-stu-id="140ec-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="140ec-130">U kunt doen Hallo hetzelfde geldt voor `Application.onTerminate()`, `Application.onLowMemory()`, en `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="140ec-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="140ec-131">U kunt ook uitbreiden `EngagementApplication` in plaats van het uitbreiden van `Application`: Hallo callback `Application.onCreate()` Hallo proces controleren en aanroepen `Application.onApplicationProcessCreate()` alleen als het huidige proces Hallo niet Hallo één hosting Hallo Engagement service, hello gelden dezelfde regels voor Hallo andere retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="140ec-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="140ec-132">Labels in Hallo AndroidManifest.xml bestand</span><span class="sxs-lookup"><span data-stu-id="140ec-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="140ec-133">Hallo in Hallo servicetag in Hallo AndroidManifest.xml bestand `android:label` kenmerk kunt u toochoose Hallo naam Hallo Engagement service wanneer deze tooend gebruikers in 'Services wordt uitgevoerd' welkomstscherm van hun telefoonnummer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="140ec-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="140ec-134">Het is raadzaam te dit kenmerk instelt`"<Your application name>Service"` (bijvoorbeeld `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="140ec-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="140ec-135">Geven Hallo `android:process` kenmerk zorgt ervoor dat Hallo Engagement service wordt uitgevoerd in een eigen proces (Engagement in Hallo dezelfde verwerken wanneer uw toepassing uw main/UI-thread mogelijk minder goed wordt uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="140ec-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="140ec-136">Bouwen met ProGuard</span><span class="sxs-lookup"><span data-stu-id="140ec-136">Building with ProGuard</span></span>
<span data-ttu-id="140ec-137">Als u uw toepassingspakket met ProGuard bouwt, moet u tookeep sommige klassen.</span><span class="sxs-lookup"><span data-stu-id="140ec-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="140ec-138">U kunt na configuratie codefragment hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="140ec-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
