---
title: aaaGet gestart met Azure Mobile Engagement voor iOS in Objective C | Microsoft Docs
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor iOS-apps.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="29952-103">Aan de slag met Azure Mobile Engagement voor iOS-apps in Objective C</span><span class="sxs-lookup"><span data-stu-id="29952-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="29952-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers tooan iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="29952-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="29952-105">In deze zelfstudie maakt u een lege iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="29952-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="29952-106">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="29952-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="29952-107">XCode 8, die u vanuit de Mac App Store kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="29952-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="29952-108">Hallo [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="29952-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="29952-109">Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Engagement-zelfstudies voor iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="29952-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="29952-110">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="29952-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="29952-111">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="29952-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="29952-112">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="29952-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="29952-113"><a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="29952-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="29952-114"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="29952-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="29952-115">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="29952-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="29952-116">de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement iOS SDK-integratie](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="29952-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="29952-117">We gaan een eenvoudige app maken met XCode toodemonstrate Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="29952-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="29952-118">Een nieuw iOS-project maken</span><span class="sxs-lookup"><span data-stu-id="29952-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="29952-119">Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="29952-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="29952-120">Hallo downloaden [Mobile Engagement iOS SDK].</span><span class="sxs-lookup"><span data-stu-id="29952-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="29952-121">Hallo extraheren..GZ-bestand tooa map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="29952-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="29952-122">Met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Add File to**.</span><span class="sxs-lookup"><span data-stu-id="29952-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="29952-123">Navigeer toohello map waar u Hallo SDK hebt uitgepakt, selecteer Hallo `EngagementSDK` map, klikt u op **opties** Hallo linksonder en zorg ervoor dat dit selectievakje Hallo **items kopiëren indien nodig** en Hallo selectievakje in voor uw doel zijn geselecteerd en druk vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="29952-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="29952-124">Open Hallo **Build Phases** tabblad en in Hallo **Link Binary With Libraries** menu Voeg Hallo-frameworks toe, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="29952-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="29952-125">Ga terug toohello Azure-portal in uw app **verbindingsgegevens** pagina en kopieer Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="29952-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="29952-126">Toevoegen Hallo volgende regel code in uw **AppDelegate.m** bestand.</span><span class="sxs-lookup"><span data-stu-id="29952-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="29952-127">Plak nu Hallo-verbindingsreeks in Hallo `didFinishLaunchingWithOptions` delegeren.</span><span class="sxs-lookup"><span data-stu-id="29952-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="29952-128">`setTestLogEnabled`is een optionele instructie waarmee de SDK-logboeken voor u tooidentify problemen.</span><span class="sxs-lookup"><span data-stu-id="29952-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="29952-129"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="29952-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="29952-130">U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="29952-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="29952-131">Open Hallo **ViewController.h** bestand en importeer **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="29952-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="29952-132">Vervang nu de bovenliggende klasse Hallo Hallo **ViewController** interface door `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="29952-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="29952-133"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="29952-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="29952-134"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="29952-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="29952-135">Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="29952-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="29952-136">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="29952-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="29952-137">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="29952-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="29952-138">Uw app tooreceive achtergrond-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="29952-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="29952-139">Hallo Reach-bibliotheek tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="29952-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="29952-140">Klik met de rechtermuisknop op het project.</span><span class="sxs-lookup"><span data-stu-id="29952-140">Right-click your project.</span></span>
2. <span data-ttu-id="29952-141">Selecteer **Add file to**.</span><span class="sxs-lookup"><span data-stu-id="29952-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="29952-142">Navigeer toohello map waar u Hallo SDK hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="29952-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="29952-143">Selecteer Hallo `EngagementReach` map.</span><span class="sxs-lookup"><span data-stu-id="29952-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="29952-144">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="29952-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="29952-145">Uw toepassingsgemachtigde wijzigen</span><span class="sxs-lookup"><span data-stu-id="29952-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="29952-146">Terug in de **AppDeletegate.m** bestand, Hallo Engagement bereiken module importeren.</span><span class="sxs-lookup"><span data-stu-id="29952-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="29952-147">Hallo binnen `application:didFinishLaunchingWithOptions` methode, maakt u een Reach-module en geef dit door bestaande initialisatieregel tooyour:</span><span class="sxs-lookup"><span data-stu-id="29952-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="29952-148">Uw app tooreceive APNS-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="29952-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="29952-149">Hallo volgende regel toohello toevoegen `application:didFinishLaunchingWithOptions` methode:</span><span class="sxs-lookup"><span data-stu-id="29952-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="29952-150">Hallo toevoegen `application:didRegisterForRemoteNotificationsWithDeviceToken` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="29952-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="29952-151">Hallo toevoegen `didFailToRegisterForRemoteNotificationsWithError` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="29952-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="29952-152">Hallo toevoegen `didReceiveRemoteNotification:fetchCompletionHandler` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="29952-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
