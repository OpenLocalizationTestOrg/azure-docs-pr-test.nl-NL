---
title: aaaGet gestart met Azure Mobile Engagement voor iOS in Swift | Microsoft Docs
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor iOS-Apps.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="d8e37-103">Aan de slag met Azure Mobile Engagement voor iOS-apps in Swift</span><span class="sxs-lookup"><span data-stu-id="d8e37-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d8e37-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers tooan iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8e37-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="d8e37-105">In deze zelfstudie maakt u een lege iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="d8e37-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="d8e37-106">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d8e37-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="d8e37-107">XCode 8, die u vanuit de Mac App Store kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="d8e37-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="d8e37-108">Hallo [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="d8e37-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="d8e37-109">Pushmeldingcertificaat (.p12), dat u kunt verkrijgen via Apple Dev Center.</span><span class="sxs-lookup"><span data-stu-id="d8e37-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="d8e37-110">In deze zelfstudie wordt gebruikgemaakt van Swift versie 3.0.</span><span class="sxs-lookup"><span data-stu-id="d8e37-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="d8e37-111">Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Engagement-zelfstudies voor iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="d8e37-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="d8e37-112">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="d8e37-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d8e37-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="d8e37-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d8e37-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d8e37-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="d8e37-115"><a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="d8e37-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d8e37-116"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="d8e37-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d8e37-117">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="d8e37-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="d8e37-118">de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement iOS SDK-integratie](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d8e37-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="d8e37-119">We gaan een eenvoudige app maken met XCode toodemonstrate Hallo integratie:</span><span class="sxs-lookup"><span data-stu-id="d8e37-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="d8e37-120">Een nieuw iOS-project maken</span><span class="sxs-lookup"><span data-stu-id="d8e37-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="d8e37-121">Verbinding maken met uw app tooMobile Engagement back-end</span><span class="sxs-lookup"><span data-stu-id="d8e37-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="d8e37-122">Hallo downloaden [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="d8e37-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="d8e37-123">Hallo extraheren..GZ-bestand tooa map op uw computer</span><span class="sxs-lookup"><span data-stu-id="d8e37-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="d8e37-124">Klik met de rechtermuisknop op Hallo-project en selecteer ' bestanden te toevoegen... "</span><span class="sxs-lookup"><span data-stu-id="d8e37-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="d8e37-125">Navigeer toohello map waar u Hallo SDK en selecteer Hallo uitgepakt `EngagementSDK` map druk op OK.</span><span class="sxs-lookup"><span data-stu-id="d8e37-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="d8e37-126">Open Hallo `Build Phases` tabblad en in Hallo `Link Binary With Libraries` menu toevoegen Hallo frameworks, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d8e37-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="d8e37-127">Een Bridging header toobe kunnen toouse Hallo SDK van Objective C-API's maken door naar File > New > File > iOS > Source > Header-bestand.</span><span class="sxs-lookup"><span data-stu-id="d8e37-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="d8e37-128">Hallo bridging header-bestand tooexpose Mobile Engagement Objective-C-code tooyour Swift-code bewerken, Hallo na invoer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d8e37-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="d8e37-129">Controleer onder Build Settings of Hallo Objective-C Bridging Header bouwen instelling onder Swift Compiler - Code Generation een pad toothis koptekst heeft.</span><span class="sxs-lookup"><span data-stu-id="d8e37-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="d8e37-130">Hier volgt een voorbeeld van een pad: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (afhankelijk van het Hallo-pad)**</span><span class="sxs-lookup"><span data-stu-id="d8e37-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="d8e37-131">Ga terug toohello Azure-portal in uw app *verbindingsgegevens* pagina en kopieer de verbindingsreeks Hallo</span><span class="sxs-lookup"><span data-stu-id="d8e37-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="d8e37-132">Plak nu Hallo-verbindingsreeks in Hallo `didFinishLaunchingWithOptions` delegeren</span><span class="sxs-lookup"><span data-stu-id="d8e37-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="d8e37-133"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="d8e37-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="d8e37-134">U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="d8e37-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d8e37-135">Open Hallo **ViewController.swift** -bestand en vervang de basisklasse Hallo van **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="d8e37-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="d8e37-136"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="d8e37-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d8e37-137"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="d8e37-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="d8e37-138">Mobile Engagement kunt u toointeract en neem contact met uw gebruikers met Pushmeldingen en In-app-berichten in Hallo context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="d8e37-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="d8e37-139">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="d8e37-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d8e37-140">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="d8e37-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="d8e37-141">Uw app tooreceive achtergrond-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="d8e37-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="d8e37-142">Hallo Reach-bibliotheek tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="d8e37-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="d8e37-143">Klik met de rechtermuisknop op het project.</span><span class="sxs-lookup"><span data-stu-id="d8e37-143">Right click your project</span></span>
2. <span data-ttu-id="d8e37-144">Selecteer `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="d8e37-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="d8e37-145">Navigeer toohello map waar u Hallo SDK hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="d8e37-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="d8e37-146">Selecteer Hallo `EngagementReach` map</span><span class="sxs-lookup"><span data-stu-id="d8e37-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="d8e37-147">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="d8e37-147">Click Add</span></span>
6. <span data-ttu-id="d8e37-148">Hallo bridging Mobile Engagement Objective-C Reach-headers van header-bestand tooexpose bewerken en Hallo na invoer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d8e37-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="d8e37-149">Uw toepassingsgemachtigde wijzigen</span><span class="sxs-lookup"><span data-stu-id="d8e37-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="d8e37-150">Hallo binnen `didFinishLaunchingWithOptions` - maakt een reach-module en geef dit door bestaande initialisatieregel tooyour:</span><span class="sxs-lookup"><span data-stu-id="d8e37-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="d8e37-151">Uw app tooreceive APNS-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="d8e37-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="d8e37-152">Hallo volgende regel toohello toevoegen `didFinishLaunchingWithOptions` methode:</span><span class="sxs-lookup"><span data-stu-id="d8e37-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="d8e37-153">Hallo toevoegen `didRegisterForRemoteNotificationsWithDeviceToken` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="d8e37-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="d8e37-154">Hallo toevoegen `didReceiveRemoteNotification:fetchCompletionHandler:` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="d8e37-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
