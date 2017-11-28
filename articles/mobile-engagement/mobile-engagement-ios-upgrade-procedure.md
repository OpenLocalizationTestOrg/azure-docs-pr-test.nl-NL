---
title: Mobile Engagement iOS SDK Upgrade Procedure aaaAzure | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="4502d-103">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="4502d-103">Upgrade procedures</span></span>
<span data-ttu-id="4502d-104">Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="4502d-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="4502d-105">Voor elke nieuwe versie van Hallo SDK moet u eerst vervangen (verwijderen en opnieuw te importeren in xcode) Hallo EngagementSDK en EngagementReach mappen.</span><span class="sxs-lookup"><span data-stu-id="4502d-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="4502d-106">Van 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="4502d-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="4502d-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="4502d-107">XCode 8</span></span>
<span data-ttu-id="4502d-108">XCode 8 is verplicht vanaf versie 4.0.0 Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="4502d-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="4502d-109">Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="4502d-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="4502d-110">Er is een bekend probleem op Hallo reach-module van de vorige versie bij het uitvoeren op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen.</span><span class="sxs-lookup"><span data-stu-id="4502d-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="4502d-111">toofix dit hebt u tooimplement Hallo API afgeschaft `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:</span><span class="sxs-lookup"><span data-stu-id="4502d-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="4502d-112">**Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="4502d-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="4502d-113">Zo snel mogelijk moet u tooXCode 8 overschakelen.</span><span class="sxs-lookup"><span data-stu-id="4502d-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="4502d-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="4502d-114">UserNotifications framework</span></span>
<span data-ttu-id="4502d-115">U moet tooadd hello `UserNotifications` framework in uw fasen bouwen.</span><span class="sxs-lookup"><span data-stu-id="4502d-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="4502d-116">in Projectverkenner hello, opent u het deelvenster van uw project en selecteer Hallo juiste doel.</span><span class="sxs-lookup"><span data-stu-id="4502d-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="4502d-117">Open vervolgens Hallo **'Buildfasen'** tabblad en in Hallo **'Link Binary With Libraries'** menu toevoegen framework `UserNotifications.framework` -set Hallo koppelen als`Optional`</span><span class="sxs-lookup"><span data-stu-id="4502d-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="4502d-118">Toepassing push mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="4502d-118">Application push capability</span></span>
<span data-ttu-id="4502d-119">XCode 8 opnieuw kunnen instellen voor uw app push mogelijkheid, Controleer of deze klopt in Hallo `capability` tabblad van het geselecteerde doel.</span><span class="sxs-lookup"><span data-stu-id="4502d-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="4502d-120">Hallo nieuwe iOS 10 kennisgeving registratiecode toevoegen</span><span class="sxs-lookup"><span data-stu-id="4502d-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="4502d-121">Hallo oudere code codefragment tooregister Hallo app toonotifications werkt nog maar maakt gebruik van afgeschaft API's bij het uitvoeren op iOS 10.</span><span class="sxs-lookup"><span data-stu-id="4502d-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="4502d-122">Importeren Hallo `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="4502d-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="4502d-123">In uw toepassingsgemachtigde `application:didFinishLaunchingWithOptions` methode vervangen:</span><span class="sxs-lookup"><span data-stu-id="4502d-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="4502d-124">door:</span><span class="sxs-lookup"><span data-stu-id="4502d-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="4502d-125">UNUserNotificationCenter gemachtigde conflicten oplossen</span><span class="sxs-lookup"><span data-stu-id="4502d-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="4502d-126">*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*</span><span class="sxs-lookup"><span data-stu-id="4502d-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="4502d-127">Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door Hallo SDK toomonitor Hallo levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4502d-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="4502d-128">Hallo SDK heeft een eigen implementatie Hallo `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing.</span><span class="sxs-lookup"><span data-stu-id="4502d-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="4502d-129">Geen andere gedelegeerde toegevoegd toohello `UNUserNotificationCenter` object Hello Engagement een conflict veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="4502d-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="4502d-130">Als Hallo SDK uw of een andere leveranciers gemachtigde detecteert en maakt geen gebruik van een eigen implementatie toogive Hallo u een kans tooresolve conflicten.</span><span class="sxs-lookup"><span data-stu-id="4502d-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="4502d-131">Hebt u tooadd Hallo Engagement logica tooyour eigenaar gemachtigde in volgorde tooresolve Hallo conflicten.</span><span class="sxs-lookup"><span data-stu-id="4502d-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="4502d-132">Er zijn twee manieren tooachieve dit.</span><span class="sxs-lookup"><span data-stu-id="4502d-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="4502d-133">Voorstel 1, door de gemachtigde doorsturen roept toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="4502d-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="4502d-134">Of voorstel 2, door het overnemen van Hallo `AEUserNotificationHandler` klasse</span><span class="sxs-lookup"><span data-stu-id="4502d-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="4502d-135">U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst toohello Agent `isEngagementPushPayload:` klasse-methode.</span><span class="sxs-lookup"><span data-stu-id="4502d-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="4502d-136">Zorg ervoor dat Hallo `UNUserNotificationCenter` gemachtigde van het object is ingesteld tooyour gemachtigde binnen een Hallo `application:willFinishLaunchingWithOptions:` of Hallo `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.</span><span class="sxs-lookup"><span data-stu-id="4502d-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="4502d-137">Bijvoorbeeld, als u Hallo hierboven voorstel 1 geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="4502d-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="4502d-138">Van 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="4502d-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="4502d-139">Ondersteuning voor iOS verwijderd 4.X.</span><span class="sxs-lookup"><span data-stu-id="4502d-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="4502d-140">Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 6.</span><span class="sxs-lookup"><span data-stu-id="4502d-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="4502d-141">Als u van Reach in uw toepassing gebruikmaakt, moet u toevoegen `remote-notification` waarde toohello `UIBackgroundModes` matrix in uw Info.plist-bestand in de volgorde tooreceive externe meldingen.</span><span class="sxs-lookup"><span data-stu-id="4502d-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="4502d-142">Hallo methode `application:didReceiveRemoteNotification:` moet toobe vervangen door `application:didReceiveRemoteNotification:fetchCompletionHandler:` in uw toepassingsgemachtigde.</span><span class="sxs-lookup"><span data-stu-id="4502d-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="4502d-143">'AEPushDelegate.h' is afgeschaft interface en u moet tooremove alle verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="4502d-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="4502d-144">Dit omvat het verwijderen van `[[EngagementAgent shared] setPushDelegate:self]` en Hallo delegeren methoden uit uw toepassingsgemachtigde:</span><span class="sxs-lookup"><span data-stu-id="4502d-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="4502d-145">Van 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="4502d-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="4502d-146">Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4502d-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="4502d-147">Als u vanaf een eerdere versie migreert, raadpleegt u eerst Hallo Capptain website toomigrate too1.16 vervolgens toepassing hello procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="4502d-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4502d-148">Capptain en Mobile Engagement dezelfde services niet zijn Hallo en Hallo onderstaande procedure alleen illustreert hoe toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="4502d-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="4502d-149">Uw gegevens worden niet van Hallo Capptain servers toohello Mobile Engagement servers migreren Hallo SDK in Hallo-app gemigreerd</span><span class="sxs-lookup"><span data-stu-id="4502d-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="4502d-150">Agent</span><span class="sxs-lookup"><span data-stu-id="4502d-150">Agent</span></span>
<span data-ttu-id="4502d-151">Hallo methode `registerApp:` is vervangen door de nieuwe methode Hallo `init:`.</span><span class="sxs-lookup"><span data-stu-id="4502d-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="4502d-152">Uw toepassingsgemachtigde dienovereenkomstig moeten worden bijgewerkt en verbindingsreeks gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4502d-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="4502d-153">SmartAd bijhouden is verwijderd uit de SDK die u zojuist tooremove alle exemplaren van hebt `AETrackModule` klasse</span><span class="sxs-lookup"><span data-stu-id="4502d-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="4502d-154">Wijzigingen in de klasse naam</span><span class="sxs-lookup"><span data-stu-id="4502d-154">Class Name Changes</span></span>
<span data-ttu-id="4502d-155">Als onderdeel van het Hallo rebranding, zijn er enkele klasse/bestandsnamen die toobe gewijzigd moeten.</span><span class="sxs-lookup"><span data-stu-id="4502d-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="4502d-156">Alle klassen die worden voorafgegaan door 'CP' worden met het voorvoegsel 'AE' gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4502d-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="4502d-157">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4502d-157">Example:</span></span>

* <span data-ttu-id="4502d-158">`CPModule.h`de naam wordt gewijzigd te`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="4502d-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="4502d-159">Alle klassen die worden voorafgegaan door 'Capptain' worden met het voorvoegsel 'Engagement' gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4502d-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="4502d-160">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="4502d-160">Examples:</span></span>

* <span data-ttu-id="4502d-161">Hallo klasse `CapptainAgent` wordt gewijzigd te`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="4502d-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="4502d-162">Hallo klasse `CapptainTableViewController` wordt gewijzigd te`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="4502d-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="4502d-163">Hallo klasse `CapptainUtils` wordt gewijzigd te`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="4502d-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="4502d-164">Hallo klasse `CapptainViewController` wordt gewijzigd te`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="4502d-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

