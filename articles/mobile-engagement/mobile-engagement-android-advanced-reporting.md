---
title: Geavanceerde opties voor de rapportage voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven hoe u doen geavanceerde rapport om vast te leggen analytics voor Azure Mobile Engagement Android SDK
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
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="93d90-103">Geavanceerde Reporting met Engagement voor Android</span><span class="sxs-lookup"><span data-stu-id="93d90-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93d90-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="93d90-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="93d90-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="93d90-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="93d90-106">iOS</span><span class="sxs-lookup"><span data-stu-id="93d90-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="93d90-107">Android</span><span class="sxs-lookup"><span data-stu-id="93d90-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="93d90-108">Dit onderwerp beschrijft aanvullende scenario's voor rapportage in uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="93d90-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="93d90-109">U kunt deze opties toepassen op de app gemaakt in de [aan de slag](mobile-engagement-android-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="93d90-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d90-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="93d90-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="93d90-111">De zelfstudie u voltooid is opzettelijk direct en eenvoudig, maar er zijn geavanceerde opties die u kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="93d90-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="93d90-112">Wijzigen van uw `Activity` klassen</span><span class="sxs-lookup"><span data-stu-id="93d90-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="93d90-113">In de [zelfstudie aan de slag](mobile-engagement-android-get-started.md), alle moest u is om uw `*Activity` subklassen overnemen van de bijbehorende `Engagement*Activity` klassen.</span><span class="sxs-lookup"><span data-stu-id="93d90-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="93d90-114">Bijvoorbeeld, als uw verouderde activiteit uitgebreid `ListActivity`, brengt u deze uitbreiden `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="93d90-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93d90-115">Wanneer u `EngagementListActivity` of `EngagementExpandableListActivity`, moet u ervoor zorgen dat een aanroep naar `requestWindowFeature(...);` wordt uitgevoerd vóór de aanroep van `super.onCreate(...);`, anders een crash plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="93d90-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="93d90-116">U vindt deze klassen in de `src` map, en kunt kopiëren naar uw project.</span><span class="sxs-lookup"><span data-stu-id="93d90-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="93d90-117">De klassen zich ook in de **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="93d90-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="93d90-118">Alternatieve methode: call `startActivity()` en `endActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="93d90-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="93d90-119">Als u niet kunt of niet wilt overbelasten uw `Activity` klassen, u kunt in plaats daarvan starten en beëindigen van uw activiteiten door het aanroepen van de `EngagementAgent`van methoden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="93d90-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93d90-120">De Android-SDK wordt nooit aangeroepen door de `endActivity()` methode, zelfs wanneer de toepassing wordt afgesloten (voor Android toepassingen zijn nooit gesloten).</span><span class="sxs-lookup"><span data-stu-id="93d90-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="93d90-121">Het is dus *maximaal* aanbevolen om aan te roepen de `startActivity()` methode in de `onResume` retouraanroep van *alle* uw activiteiten, en de `endActivity()` methode in de `onPause()` retouraanroep van *Alle* uw activiteiten.</span><span class="sxs-lookup"><span data-stu-id="93d90-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="93d90-122">Dit is de enige manier om ervoor te zorgen dat sessies niet gelekt.</span><span class="sxs-lookup"><span data-stu-id="93d90-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="93d90-123">Als een sessie is gelekt, wordt de service Engagement nooit ontkoppelt van de back-end Engagement (omdat de service verbonden blijft als een sessie in behandeling is).</span><span class="sxs-lookup"><span data-stu-id="93d90-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="93d90-124">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="93d90-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="93d90-125">In dit voorbeeld is vergelijkbaar met de `EngagementActivity` klasse en varianten, waarvan de broncode wordt verstrekt in de `src` map.</span><span class="sxs-lookup"><span data-stu-id="93d90-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="93d90-126">Met behulp van Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="93d90-126">Using Application.onCreate()</span></span>
<span data-ttu-id="93d90-127">Alle code die u in plaatsen `Application.onCreate()` en in andere toepassingen retouraanroepen voor de processen van uw toepassing, inclusief de Engagement-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="93d90-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="93d90-128">Er kunnen ongewenste neveneffecten hebben, zoals overbodige geheugentoewijzingen en threads in de Engagement-proces of dubbele broadcast ontvangers of services.</span><span class="sxs-lookup"><span data-stu-id="93d90-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="93d90-129">Als u negeren `Application.onCreate()`, wordt aangeraden het volgende codefragment toe te voegen aan het begin van uw `Application.onCreate()` functie:</span><span class="sxs-lookup"><span data-stu-id="93d90-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="93d90-130">U kunt hetzelfde doen voor `Application.onTerminate()`, `Application.onLowMemory()`, en `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="93d90-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="93d90-131">U kunt ook uitbreiden `EngagementApplication` in plaats van het uitbreiden van `Application`: de callback `Application.onCreate()` heeft de controle van het proces en aanroepen `Application.onApplicationProcessCreate()` alleen als het huidige proces niet degene die als host fungeert voor de Engagement-service is, dezelfde regels voor de andere gelden retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="93d90-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="93d90-132">Labels in het bestand AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="93d90-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="93d90-133">In de service-code in het bestand AndroidManifest.xml de `android:label` kenmerk kunt u de naam van de service Engagement kiezen, zoals deze wordt weergegeven aan eindgebruikers in het scherm 'Services uitgevoerd' van hun telefoon.</span><span class="sxs-lookup"><span data-stu-id="93d90-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="93d90-134">Het is raadzaam als dit kenmerk instelt op `"<Your application name>Service"` (bijvoorbeeld `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="93d90-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="93d90-135">Geven de `android:process` kenmerk zorgt ervoor dat de Engagement-service wordt uitgevoerd in een eigen proces (Engagement uitgevoerd in hetzelfde proces als uw toepassing de main/UI-thread mogelijk minder goed maakt).</span><span class="sxs-lookup"><span data-stu-id="93d90-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="93d90-136">Bouwen met ProGuard</span><span class="sxs-lookup"><span data-stu-id="93d90-136">Building with ProGuard</span></span>
<span data-ttu-id="93d90-137">Als u uw toepassingspakket met ProGuard bouwt, moet u bepaalde klassen houden.</span><span class="sxs-lookup"><span data-stu-id="93d90-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="93d90-138">U kunt de volgende configuratie-fragment:</span><span class="sxs-lookup"><span data-stu-id="93d90-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
