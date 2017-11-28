---
title: Azure Mobile Engagement iOS SDK overzicht | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="7bd64-103">iOS-SDK voor Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7bd64-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="7bd64-104">Begin hier voor alle informatie over het integreren van Azure Mobile Engagement in een iOS-App.</span><span class="sxs-lookup"><span data-stu-id="7bd64-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="7bd64-105">Als u u het eerst proberen wilt, controleert u of u doen onze [15 minuten zelfstudie](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7bd64-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="7bd64-106">Klik om te zien de [SDK-inhoud](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="7bd64-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="7bd64-107">Integratie procedures</span><span class="sxs-lookup"><span data-stu-id="7bd64-107">Integration procedures</span></span>
1. <span data-ttu-id="7bd64-108">Begin hier: [Mobile Engagement integreren in uw iOS-app](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="7bd64-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="7bd64-109">Voor meldingen: [Reach (meldingen) integreren in uw iOS-app](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="7bd64-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="7bd64-110">Tag plan implementatie: [hoe u de geavanceerde Mobile Engagement tags API in uw iOS-app](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="7bd64-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="7bd64-111">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="7bd64-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="7bd64-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="7bd64-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="7bd64-113">Vaste badges uitgeschakeld op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="7bd64-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="7bd64-114">Vaste waarschuwingen op 9 over API's niet aangeroepen in hoofdwachtrij XCode.</span><span class="sxs-lookup"><span data-stu-id="7bd64-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="7bd64-115">Een geheugenlek vast Reach polls.</span><span class="sxs-lookup"><span data-stu-id="7bd64-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="7bd64-116">Ondersteuning voor iOS verwijderd 6.X.</span><span class="sxs-lookup"><span data-stu-id="7bd64-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="7bd64-117">Vanaf deze versie van het implementatiedoel van uw toepassing moet ten minste iOS 7.</span><span class="sxs-lookup"><span data-stu-id="7bd64-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="7bd64-118">Zie voor een eerdere versie de [voltooien release-opmerkingen](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="7bd64-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="7bd64-119">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="7bd64-119">Upgrade procedures</span></span>
<span data-ttu-id="7bd64-120">Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u de volgende punten overwegen bij het upgraden van de SDK.</span><span class="sxs-lookup"><span data-stu-id="7bd64-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="7bd64-121">Wellicht hebt u verschillende procedures volgen als u verschillende versies van de SDK van de volledige Zie gemist [Procedures Upgrade](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="7bd64-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="7bd64-122">Voor elke nieuwe versie van de SDK moet u eerst vervangen (verwijderen en opnieuw te importeren in xcode) de mappen EngagementSDK en EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="7bd64-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="7bd64-123">Van 3.0.0 naar 4.0.0</span><span class="sxs-lookup"><span data-stu-id="7bd64-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="7bd64-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="7bd64-124">XCode 8</span></span>
<span data-ttu-id="7bd64-125">XCode 8 is verplicht vanaf versie 4.0.0 van de SDK.</span><span class="sxs-lookup"><span data-stu-id="7bd64-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd64-126">Als u echt afhankelijk van XCode 7 zijn en u kunt de [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="7bd64-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="7bd64-127">Er is een bekend probleem in de vorige versie van de reach-module tijdens het uitvoeren van op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen.</span><span class="sxs-lookup"><span data-stu-id="7bd64-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="7bd64-128">Om op te lossen dit er voor het implementeren van de afgeschafte API `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:</span><span class="sxs-lookup"><span data-stu-id="7bd64-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="7bd64-129">**Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="7bd64-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="7bd64-130">U moet zo snel mogelijk overschakelen naar XCode 8.</span><span class="sxs-lookup"><span data-stu-id="7bd64-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="7bd64-131">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="7bd64-131">UserNotifications framework</span></span>
<span data-ttu-id="7bd64-132">U wilt toevoegen de `UserNotifications` framework in uw fasen bouwen.</span><span class="sxs-lookup"><span data-stu-id="7bd64-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="7bd64-133">uw project openen in de Projectverkenner en selecteert u het juiste doel.</span><span class="sxs-lookup"><span data-stu-id="7bd64-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="7bd64-134">Open vervolgens de **'Buildfasen'** tabblad en in de **'Link Binary With Libraries'** menu framework toevoegen `UserNotifications.framework` -de koppeling als instellen`Optional`</span><span class="sxs-lookup"><span data-stu-id="7bd64-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="7bd64-135">Toepassing push mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="7bd64-135">Application push capability</span></span>
<span data-ttu-id="7bd64-136">XCode 8 opnieuw kunnen instellen voor uw app push mogelijkheid, Controleer of deze klopt de `capability` tabblad van het geselecteerde doel.</span><span class="sxs-lookup"><span data-stu-id="7bd64-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="7bd64-137">De nieuwe registratiecode voor iOS 10 melding toevoegen</span><span class="sxs-lookup"><span data-stu-id="7bd64-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="7bd64-138">De oudere codefragment registreren van de app kan meldingen werkt nog maar afgeschaft API's gebruikt bij het uitvoeren op iOS 10.</span><span class="sxs-lookup"><span data-stu-id="7bd64-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="7bd64-139">Importeer de `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="7bd64-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="7bd64-140">In uw toepassingsgemachtigde `application:didFinishLaunchingWithOptions` methode vervangen:</span><span class="sxs-lookup"><span data-stu-id="7bd64-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="7bd64-141">door:</span><span class="sxs-lookup"><span data-stu-id="7bd64-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="7bd64-142">UNUserNotificationCenter gemachtigde conflicten oplossen</span><span class="sxs-lookup"><span data-stu-id="7bd64-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="7bd64-143">*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*</span><span class="sxs-lookup"><span data-stu-id="7bd64-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="7bd64-144">Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door de SDK voor het bewaken van de levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="7bd64-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="7bd64-145">De SDK heeft een eigen implementatie van de `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bd64-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="7bd64-146">Geen andere gedelegeerde toegevoegd aan de `UNUserNotificationCenter` object met de Engagement een conflict veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="7bd64-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="7bd64-147">Als de SDK de of alle andere leveranciers gemachtigde detecteert wordt deze niet zijn eigen implementatie gebruiken om een waarschuwingsbericht geeft u de conflicten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="7bd64-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="7bd64-148">U moet de Engagement-logica toevoegen aan uw eigen gemachtigde om de conflicten oplossen.</span><span class="sxs-lookup"><span data-stu-id="7bd64-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="7bd64-149">Er zijn twee manieren om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="7bd64-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="7bd64-150">Voorstel 1, door de gemachtigde doorsturen aanroepen naar de SDK:</span><span class="sxs-lookup"><span data-stu-id="7bd64-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="7bd64-151">Of voorstel 2, door het overnemen van de `AEUserNotificationHandler` klasse</span><span class="sxs-lookup"><span data-stu-id="7bd64-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="7bd64-152">U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst met de Agent `isEngagementPushPayload:` klasse-methode.</span><span class="sxs-lookup"><span data-stu-id="7bd64-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="7bd64-153">Zorg ervoor dat de `UNUserNotificationCenter` gemachtigde van het object is ingesteld op uw gemachtigde binnen ofwel de `application:willFinishLaunchingWithOptions:` of de `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.</span><span class="sxs-lookup"><span data-stu-id="7bd64-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="7bd64-154">Bijvoorbeeld, als u de bovenstaande voorstel 1 geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="7bd64-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
