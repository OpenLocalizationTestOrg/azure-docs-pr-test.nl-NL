---
title: aaaGet gestart met Azure Mobile Engagement voor Xamarin.Android
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Xamarin.Android-Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="895e2-103">Aan de slag met Azure Mobile Engagement voor Xamarin.Android-apps</span><span class="sxs-lookup"><span data-stu-id="895e2-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="895e2-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Xamarin.Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="895e2-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="895e2-105">Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="895e2-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="895e2-106">U maakt een lege Xamarin.Android-app die basisgegevens verzamelt en pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="895e2-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="895e2-107">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="895e2-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="895e2-108">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="895e2-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="895e2-109">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="895e2-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="895e2-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="895e2-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="895e2-111">U kunt ook Visual Studio gebruiken met Xamarin, maar deze zelfstudie gebruikt Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="895e2-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="895e2-112">Zie [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installatie voor Visual Studio en Xamarin) voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="895e2-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="895e2-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="895e2-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="895e2-114">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="895e2-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="895e2-115">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="895e2-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="895e2-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="895e2-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="895e2-117"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app</span><span class="sxs-lookup"><span data-stu-id="895e2-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="895e2-118"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="895e2-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="895e2-119">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="895e2-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="895e2-120">We gaan een eenvoudige app maken met Xamarin Studio toodemonstrate Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="895e2-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="895e2-121">Een nieuw Xamarin.Android-project maken</span><span class="sxs-lookup"><span data-stu-id="895e2-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="895e2-122">Start **Xamarin Studio** te gaan**bestand** -> **nieuw** -> **oplossing**</span><span class="sxs-lookup"><span data-stu-id="895e2-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="895e2-123">Selecteer **Android-App** zorgt u ervoor Hallo geselecteerde taal **C#** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="895e2-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="895e2-124">Vul Hallo **Appnaam** en Hallo **organisatie-id**.</span><span class="sxs-lookup"><span data-stu-id="895e2-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="895e2-125">Zorg ervoor dat toocheckmark **Google Play Services** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="895e2-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="895e2-126">Update Hallo **projectnaam**, **oplossingsnaam** en **locatie** indien nodig, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="895e2-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="895e2-127">Xamarin Studio maakt Hallo-app waarin we Mobile Engagement gaan integreren.</span><span class="sxs-lookup"><span data-stu-id="895e2-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="895e2-128">Verbinding maken met uw app tooMobile Engagement back-end</span><span class="sxs-lookup"><span data-stu-id="895e2-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="895e2-129">Klik met de rechtermuisknop op Hallo **pakketten** map in Hallo Solution en selecteer **pakketten toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="895e2-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="895e2-130">Zoeken naar Hallo **Microsoft Azure Mobile Engagement Xamarin SDK** en toe te voegen tooyour oplossing.</span><span class="sxs-lookup"><span data-stu-id="895e2-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="895e2-131">Open **MainActivity.cs** en voeg de volgende Hallo using-instructies:</span><span class="sxs-lookup"><span data-stu-id="895e2-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="895e2-132">In Hallo `OnCreate` methode toevoegen Hallo tooinitialize Hallo verbinding met de back-end van Mobile Engagement te volgen.</span><span class="sxs-lookup"><span data-stu-id="895e2-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="895e2-133">Zorg ervoor dat tooadd uw **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="895e2-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="895e2-134">Machtigingen en een servicedeclaratie toevoegen</span><span class="sxs-lookup"><span data-stu-id="895e2-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="895e2-135">Open Hallo **Manifest.xml** bestand in map Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="895e2-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="895e2-136">Selecteer het tabblad Source zodat u Hallo XML-bron direct kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="895e2-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="895e2-137">Toevoegen van deze machtigingen toohello Manifest.xml (dat zich bevindt onder Hallo **eigenschappen** map) van uw project direct vóór of na Hallo `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="895e2-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="895e2-138">Voeg de volgende Hallo tussen Hallo `<application>` en `</application>` tags toodeclare Hallo agent-service:</span><span class="sxs-lookup"><span data-stu-id="895e2-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="895e2-139">In de code Hallo u zojuist hebt geplakt, vervangt u `"<Your application name>"` in Hallo label.</span><span class="sxs-lookup"><span data-stu-id="895e2-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="895e2-140">Dit wordt weergegeven in Hallo **instellingen** menu waar gebruikers de services die worden uitgevoerd op Hallo apparaat kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="895e2-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="895e2-141">U kunt bijvoorbeeld Hallo woord 'Service' aan dat label toevoegen.</span><span class="sxs-lookup"><span data-stu-id="895e2-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="895e2-142">Een scherm tooMobile Engagement verzenden</span><span class="sxs-lookup"><span data-stu-id="895e2-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="895e2-143">U moet ten minste één scherm toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="895e2-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="895e2-144">Om dit te doen-Zorg ervoor dat Hallo `MainActivity` neemt over van `EngagementActivity` in plaats van `Activity`.</span><span class="sxs-lookup"><span data-stu-id="895e2-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="895e2-145">Als u niet kunt overnemen van `EngagementActivity`, moet u vervolgens de methode `.StartActivity` en `.EndActivity` toevoegen in respectievelijk `OnResume` en `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="895e2-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="895e2-146"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="895e2-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="895e2-147"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="895e2-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="895e2-148">Mobile Engagement kunt u toointeract met en uw gebruikers met pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="895e2-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="895e2-149">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="895e2-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="895e2-150">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="895e2-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
