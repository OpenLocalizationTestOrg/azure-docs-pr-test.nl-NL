---
title: aaaGet gestart met Azure Mobile Engagement voor Xamarin.iOS
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Xamarin.iOS-Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="43493-103">Aan de slag met Azure Mobile Engagement voor Xamarin.iOS-apps</span><span class="sxs-lookup"><span data-stu-id="43493-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="43493-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers in een Xamarin.iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="43493-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="43493-105">In deze zelfstudie maakt u een lege Xamarin.iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="43493-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="43493-106">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="43493-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="43493-107">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="43493-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="43493-108">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="43493-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="43493-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="43493-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="43493-110">U kunt ook Visual Studio gebruiken met Xamarin, maar deze zelfstudie gebruikt Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="43493-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="43493-111">Zie [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installatie voor Visual Studio en Xamarin) voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="43493-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="43493-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="43493-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="43493-113">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="43493-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="43493-114">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="43493-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="43493-115">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="43493-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="43493-116"><a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="43493-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="43493-117"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="43493-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="43493-118">Deze zelfstudie toont een 'basisintegratie' hello minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="43493-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="43493-119">We gaan een eenvoudige app maken met Xamarin toodemonstrate Hallo integratie:</span><span class="sxs-lookup"><span data-stu-id="43493-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="43493-120">Een nieuw Xamarin.iOS-project maken</span><span class="sxs-lookup"><span data-stu-id="43493-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="43493-121">Start Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="43493-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="43493-122">Ga te**bestand** -> **nieuw** -> **oplossing**</span><span class="sxs-lookup"><span data-stu-id="43493-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="43493-123">Selecteer **Single View App**, Controleer of de taal Hallo geselecteerd **C#** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="43493-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="43493-124">Vul Hallo **Appnaam** en Hallo **organisatie-id** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="43493-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="43493-125">Zorg ervoor dat Hallo publiceren profiel die u uiteindelijk toodeploy die uw iOS-app is met behulp van een App-ID die overeenkomt met exact met Hallo bundel-id hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="43493-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="43493-126">Update Hallo **projectnaam**, **oplossingsnaam** en **locatie** indien nodig, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="43493-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="43493-127">Xamarin Studio maakt Hallo demo-app waarin we Mobile Engagement gaan integreren.</span><span class="sxs-lookup"><span data-stu-id="43493-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="43493-128">Verbinding maken met uw app tooMobile Engagement back-end</span><span class="sxs-lookup"><span data-stu-id="43493-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="43493-129">Klik met de rechtermuisknop op Hallo **pakketten** map in Hallo Solution en selecteer **pakketten toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="43493-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="43493-130">Zoeken naar Hallo **Microsoft Azure Mobile Engagement Xamarin SDK** en toe te voegen tooyour oplossing.</span><span class="sxs-lookup"><span data-stu-id="43493-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="43493-131">Open **AppDelegate.cs** en voeg de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="43493-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="43493-132">In Hallo **FinishedLaunching** methode toevoegen Hallo tooinitialize Hallo verbinding met de back-end van Mobile Engagement te volgen.</span><span class="sxs-lookup"><span data-stu-id="43493-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="43493-133">Zorg ervoor dat tooadd uw **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="43493-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="43493-134">Deze code wordt een dummy **NotificationIcon** toegevoegd door Mobile Engagement SDK die u kunt Hallo tooreplace.</span><span class="sxs-lookup"><span data-stu-id="43493-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="43493-135"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="43493-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="43493-136">U moet ten minste één scherm toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="43493-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="43493-137">Open **ViewController.cs** en voeg de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="43493-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="43493-138">Vervang Hallo klasse waarvan `ViewController` neemt over van `UIViewController` te`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="43493-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="43493-139"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="43493-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="43493-140"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="43493-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="43493-141">Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="43493-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="43493-142">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="43493-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="43493-143">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="43493-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="43493-144">Uw toepassingsgemachtigde wijzigen</span><span class="sxs-lookup"><span data-stu-id="43493-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="43493-145">Open Hallo **AppDelegate.cs** en voeg de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="43493-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="43493-146">Nu binnen Hallo `FinishedLaunching` methode Hallo na tooregister van pushberichten na toevoegen`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="43493-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="43493-147">Ten slotte - bijwerken of toevoegen Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="43493-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="43493-148">In uw **Info.plist** bestand in Hallo-oplossing, bevestig dat Hallo **bundel-id** overeenkomt met de Hallo **App-ID** hebt in uw inrichtingsprofiel in Hallo Apple Dev Center.</span><span class="sxs-lookup"><span data-stu-id="43493-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="43493-149">Hallo in dezelfde **Info.plist** bestand, zorg ervoor dat u hebt gecontroleerd dat Hallo **Enable Background Modes** en **Remote Notifications**.</span><span class="sxs-lookup"><span data-stu-id="43493-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="43493-150">Hallo-app uitvoeren op Hallo-apparaat die u hebt gekoppeld aan dit publicatieprofiel.</span><span class="sxs-lookup"><span data-stu-id="43493-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
