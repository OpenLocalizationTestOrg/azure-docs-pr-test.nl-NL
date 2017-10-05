---
title: Azure Mobile Engagement iOS SDK Upgrade Procedure | Microsoft Docs
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="81d3e-103">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="81d3e-103">Upgrade procedures</span></span>
<span data-ttu-id="81d3e-104">Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u de volgende punten overwegen bij het upgraden van de SDK.</span><span class="sxs-lookup"><span data-stu-id="81d3e-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="81d3e-105">Voor elke nieuwe versie van de SDK moet u eerst vervangen (verwijderen en opnieuw te importeren in xcode) de mappen EngagementSDK en EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="81d3e-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="81d3e-106">Van 3.0.0 naar 4.0.0</span><span class="sxs-lookup"><span data-stu-id="81d3e-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="81d3e-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="81d3e-107">XCode 8</span></span>
<span data-ttu-id="81d3e-108">XCode 8 is verplicht vanaf versie 4.0.0 van de SDK.</span><span class="sxs-lookup"><span data-stu-id="81d3e-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="81d3e-109">Als u echt afhankelijk van XCode 7 zijn en u kunt de [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="81d3e-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="81d3e-110">Er is een bekend probleem in de vorige versie van de reach-module tijdens het uitvoeren van op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="81d3e-111">Om op te lossen dit er voor het implementeren van de afgeschafte API `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:</span><span class="sxs-lookup"><span data-stu-id="81d3e-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="81d3e-112">**Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="81d3e-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="81d3e-113">U moet zo snel mogelijk overschakelen naar XCode 8.</span><span class="sxs-lookup"><span data-stu-id="81d3e-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="81d3e-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="81d3e-114">UserNotifications framework</span></span>
<span data-ttu-id="81d3e-115">U wilt toevoegen de `UserNotifications` framework in uw fasen bouwen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="81d3e-116">uw project openen in de Projectverkenner en selecteert u het juiste doel.</span><span class="sxs-lookup"><span data-stu-id="81d3e-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="81d3e-117">Open vervolgens de **'Buildfasen'** tabblad en in de **'Link Binary With Libraries'** menu framework toevoegen `UserNotifications.framework` -de koppeling als instellen`Optional`</span><span class="sxs-lookup"><span data-stu-id="81d3e-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="81d3e-118">Toepassing push mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="81d3e-118">Application push capability</span></span>
<span data-ttu-id="81d3e-119">XCode 8 opnieuw kunnen instellen voor uw app push mogelijkheid, Controleer of deze klopt de `capability` tabblad van het geselecteerde doel.</span><span class="sxs-lookup"><span data-stu-id="81d3e-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="81d3e-120">De nieuwe registratiecode voor iOS 10 melding toevoegen</span><span class="sxs-lookup"><span data-stu-id="81d3e-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="81d3e-121">De oudere codefragment registreren van de app kan meldingen werkt nog maar afgeschaft API's gebruikt bij het uitvoeren op iOS 10.</span><span class="sxs-lookup"><span data-stu-id="81d3e-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="81d3e-122">Importeer de `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="81d3e-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="81d3e-123">In uw toepassingsgemachtigde `application:didFinishLaunchingWithOptions` methode vervangen:</span><span class="sxs-lookup"><span data-stu-id="81d3e-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="81d3e-124">door:</span><span class="sxs-lookup"><span data-stu-id="81d3e-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="81d3e-125">UNUserNotificationCenter gemachtigde conflicten oplossen</span><span class="sxs-lookup"><span data-stu-id="81d3e-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="81d3e-126">*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*</span><span class="sxs-lookup"><span data-stu-id="81d3e-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="81d3e-127">Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door de SDK voor het bewaken van de levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="81d3e-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="81d3e-128">De SDK heeft een eigen implementatie van de `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing.</span><span class="sxs-lookup"><span data-stu-id="81d3e-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="81d3e-129">Geen andere gedelegeerde toegevoegd aan de `UNUserNotificationCenter` object met de Engagement een conflict veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="81d3e-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="81d3e-130">Als de SDK de of alle andere leveranciers gemachtigde detecteert wordt deze niet zijn eigen implementatie gebruiken om een waarschuwingsbericht geeft u de conflicten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="81d3e-131">U moet de Engagement-logica toevoegen aan uw eigen gemachtigde om de conflicten oplossen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="81d3e-132">Er zijn twee manieren om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="81d3e-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="81d3e-133">Voorstel 1, door de gemachtigde doorsturen aanroepen naar de SDK:</span><span class="sxs-lookup"><span data-stu-id="81d3e-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="81d3e-134">Of voorstel 2, door het overnemen van de `AEUserNotificationHandler` klasse</span><span class="sxs-lookup"><span data-stu-id="81d3e-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="81d3e-135">U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst met de Agent `isEngagementPushPayload:` klasse-methode.</span><span class="sxs-lookup"><span data-stu-id="81d3e-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="81d3e-136">Zorg ervoor dat de `UNUserNotificationCenter` gemachtigde van het object is ingesteld op uw gemachtigde binnen ofwel de `application:willFinishLaunchingWithOptions:` of de `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.</span><span class="sxs-lookup"><span data-stu-id="81d3e-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="81d3e-137">Bijvoorbeeld, als u de bovenstaande voorstel 1 geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="81d3e-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="81d3e-138">Van 2.0.0 naar 3.0.0</span><span class="sxs-lookup"><span data-stu-id="81d3e-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="81d3e-139">Ondersteuning voor iOS verwijderd 4.X.</span><span class="sxs-lookup"><span data-stu-id="81d3e-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="81d3e-140">Vanaf deze versie van het implementatiedoel van uw toepassing moet ten minste iOS 6.</span><span class="sxs-lookup"><span data-stu-id="81d3e-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="81d3e-141">Als u van Reach in uw toepassing gebruikmaakt, moet u toevoegen `remote-notification` van waarde naar de `UIBackgroundModes` matrix in uw Info.plist-bestand om te kunnen externe meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="81d3e-142">De methode `application:didReceiveRemoteNotification:` moet worden vervangen door `application:didReceiveRemoteNotification:fetchCompletionHandler:` in uw toepassingsgemachtigde.</span><span class="sxs-lookup"><span data-stu-id="81d3e-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="81d3e-143">'AEPushDelegate.h' is afgeschaft interface en u moet alle verwijzingen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="81d3e-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="81d3e-144">Dit omvat het verwijderen van `[[EngagementAgent shared] setPushDelegate:self]` en de methoden van de gemachtigde van uw toepassingsgemachtigde:</span><span class="sxs-lookup"><span data-stu-id="81d3e-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="81d3e-145">Van 1.16.0 naar 2.0.0</span><span class="sxs-lookup"><span data-stu-id="81d3e-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="81d3e-146">De volgende beschrijft het migreren van een SDK-integratie van de service van Capptain SAS Capptain in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="81d3e-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="81d3e-147">Als u vanaf een eerdere versie migreert, raadpleegt u de Capptain-website om te migreren naar 1.16 eerst vervolgens toepassen van de volgende procedure.</span><span class="sxs-lookup"><span data-stu-id="81d3e-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81d3e-148">Capptain en Mobile Engagement zijn niet dezelfde services en de procedure die hieronder wordt alleen uitgelegd hoe u voor het migreren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="81d3e-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="81d3e-149">Migreren van de SDK in de app wordt niet uw gegevens migreren van de servers Capptain naar de Mobile Engagement-servers</span><span class="sxs-lookup"><span data-stu-id="81d3e-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="81d3e-150">Agent</span><span class="sxs-lookup"><span data-stu-id="81d3e-150">Agent</span></span>
<span data-ttu-id="81d3e-151">De methode `registerApp:` is vervangen door de nieuwe methode `init:`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="81d3e-152">Uw toepassingsgemachtigde dienovereenkomstig moeten worden bijgewerkt en verbindingsreeks gebruiken:</span><span class="sxs-lookup"><span data-stu-id="81d3e-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="81d3e-153">SmartAd bijhouden is verwijderd uit de SDK die u hoeft te verwijderen van alle exemplaren van `AETrackModule` klasse</span><span class="sxs-lookup"><span data-stu-id="81d3e-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="81d3e-154">Wijzigingen in de klasse naam</span><span class="sxs-lookup"><span data-stu-id="81d3e-154">Class Name Changes</span></span>
<span data-ttu-id="81d3e-155">Als onderdeel van de rebranding zijn er enkele klasse/bestandsnamen die moeten worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="81d3e-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="81d3e-156">Alle klassen die worden voorafgegaan door 'CP' worden met het voorvoegsel 'AE' gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="81d3e-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="81d3e-157">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81d3e-157">Example:</span></span>

* <span data-ttu-id="81d3e-158">`CPModule.h`is gewijzigd in `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="81d3e-159">Alle klassen die worden voorafgegaan door 'Capptain' worden met het voorvoegsel 'Engagement' gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="81d3e-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="81d3e-160">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="81d3e-160">Examples:</span></span>

* <span data-ttu-id="81d3e-161">De klasse `CapptainAgent` is gewijzigd in `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="81d3e-162">De klasse `CapptainTableViewController` is gewijzigd in `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="81d3e-163">De klasse `CapptainUtils` is gewijzigd in `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="81d3e-164">De klasse `CapptainViewController` is gewijzigd in `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="81d3e-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

