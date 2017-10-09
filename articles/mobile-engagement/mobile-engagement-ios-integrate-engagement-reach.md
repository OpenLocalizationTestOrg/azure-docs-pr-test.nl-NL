---
title: Mobile Engagement iOS SDK-integratie bereiken aaaAzure | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="e31d3-103">Hoe tooIntegrate Engagement bereiken op iOS</span><span class="sxs-lookup"><span data-stu-id="e31d3-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="e31d3-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo [hoe tooIntegrate Engagement voor iOS-document](mobile-engagement-ios-integrate-engagement.md) voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="e31d3-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="e31d3-105">Deze documentatie vereist XCode 8.</span><span class="sxs-lookup"><span data-stu-id="e31d3-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="e31d3-106">Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="e31d3-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="e31d3-107">Er is een bekend probleem in de vorige versie bij het uitvoeren op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="e31d3-108">toofix dit hebt u tooimplement Hallo API afgeschaft `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:</span><span class="sxs-lookup"><span data-stu-id="e31d3-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="e31d3-109">**Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="e31d3-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="e31d3-110">Zo snel mogelijk moet u tooXCode 8 overschakelen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="e31d3-111">Uw app tooreceive achtergrond-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="e31d3-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="e31d3-112">Stappen voor integratie</span><span class="sxs-lookup"><span data-stu-id="e31d3-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="e31d3-113">Hallo Engagement bereiken SDK in uw iOS-project insluiten</span><span class="sxs-lookup"><span data-stu-id="e31d3-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="e31d3-114">Hallo Reach-sdk toevoegen aan uw Xcode-project.</span><span class="sxs-lookup"><span data-stu-id="e31d3-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="e31d3-115">Ga te in Xcode**Project \> toevoegen tooproject** en kies Hallo `EngagementReach` map.</span><span class="sxs-lookup"><span data-stu-id="e31d3-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e31d3-116">Uw toepassingsgemachtigde wijzigen</span><span class="sxs-lookup"><span data-stu-id="e31d3-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="e31d3-117">Hallo bovenaan uw implementatiebestand in Hallo Engagement bereiken module te importeren:</span><span class="sxs-lookup"><span data-stu-id="e31d3-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="e31d3-118">In de methode `applicationDidFinishLaunching:` of `application:didFinishLaunchingWithOptions:`, maakt u een reach-module en geef dit door bestaande initialisatieregel tooyour:</span><span class="sxs-lookup"><span data-stu-id="e31d3-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="e31d3-119">Wijzig **'icon.png'** tekenreeks met de naam van de installatiekopie Hallo u wilt gebruiken als uw meldingspictogram.</span><span class="sxs-lookup"><span data-stu-id="e31d3-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="e31d3-120">Als u wilt dat toouse Hallo optie *Update badge waarde* in Reach-campagnes of als u wilt dat de native pushberichten toouse \<SaaS/Reach API/campagne indeling Native Push\> campagnes, moet u laten Hallo Reach-module beheren Hallo badge pictogram zelf (deze wordt automatisch gewist Hallo toepassing badge en ook opnieuw instellen Engagement opgeslagen telkens wanneer de toepassing hello gestart of foregrounded is Hallo-waarde).</span><span class="sxs-lookup"><span data-stu-id="e31d3-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="e31d3-121">Dit wordt gedaan door Hallo volgt regel na de initialisatie van de Reach-module toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="e31d3-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="e31d3-122">Als u toohandle Reach gegevens-push wilt, moet u uw toepassingsgemachtigde toohello voldoen laten `AEReachDataPushDelegate` protocol.</span><span class="sxs-lookup"><span data-stu-id="e31d3-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="e31d3-123">Hallo volgt regel na de initialisatie van de Reach-module toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e31d3-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="e31d3-124">Vervolgens kunt u methoden Hallo implementeren `onDataPushStringReceived:` en `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in uw toepassingsgemachtigde:</span><span class="sxs-lookup"><span data-stu-id="e31d3-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="e31d3-125">Category</span><span class="sxs-lookup"><span data-stu-id="e31d3-125">Category</span></span>
<span data-ttu-id="e31d3-126">Hallo categorieparameter is optioneel bij het maken van een campagne Push-gegevens en kunt dat u gegevens toofilter pushes.</span><span class="sxs-lookup"><span data-stu-id="e31d3-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="e31d3-127">Dit is handig als u wilt dat de verschillende typen toopush van `Base64` gegevens en wilt tooidentify hun type voordat ze worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="e31d3-128">**Uw toepassing is nu gereed tooreceive en weergave inhoud bereiken!**</span><span class="sxs-lookup"><span data-stu-id="e31d3-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="e31d3-129">Hoe tooreceive aankondigingen en polls op elk gewenst moment</span><span class="sxs-lookup"><span data-stu-id="e31d3-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="e31d3-130">Engagement kunt Reach meldingen verzenden tooyour eindgebruikers op elk gewenst moment via Hallo Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="e31d3-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="e31d3-131">tooenable deze functionaliteit u tooprepare hebben uw aanvraag voor Apple pushmeldingen en uw toepassingsgemachtigde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="e31d3-132">Uw aanvraag voor Apple pushmeldingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="e31d3-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="e31d3-133">Volg Hallo guide: [hoe tooPrepare uw aanvraag voor Apple Pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="e31d3-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="e31d3-134">Hallo nodig clientcode toevoegen</span><span class="sxs-lookup"><span data-stu-id="e31d3-134">Add hello necessary client code</span></span>
<span data-ttu-id="e31d3-135">*Uw toepassing hebt op dit moment een geregistreerde Apple push-certificaat in Hallo Engagement frontend.*</span><span class="sxs-lookup"><span data-stu-id="e31d3-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="e31d3-136">Als deze niet al gebeurt, moet u tooregister uw toepassing tooreceive-pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="e31d3-137">Importeren Hallo `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="e31d3-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="e31d3-138">Toevoegen van Hallo volgt regel wanneer uw toepassing wordt gestart (meestal in `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="e31d3-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="e31d3-139">Vervolgens moet u tooprovide tooEngagement hello apparaattoken geretourneerd door de servers van Apple.</span><span class="sxs-lookup"><span data-stu-id="e31d3-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="e31d3-140">Dit doet u in het Hallo-methode met de naam `application:didRegisterForRemoteNotificationsWithDeviceToken:` in uw toepassingsgemachtigde:</span><span class="sxs-lookup"><span data-stu-id="e31d3-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="e31d3-141">U hebt ten slotte tooinform Hallo Engagement SDK wanneer uw toepassing een externe melding ontvangt.</span><span class="sxs-lookup"><span data-stu-id="e31d3-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="e31d3-142">toodo die aanroepen Hallo methode `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in uw toepassingsgemachtigde:</span><span class="sxs-lookup"><span data-stu-id="e31d3-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="e31d3-143">Standaard controleert de Hallo completionHandler Engagement bereiken.</span><span class="sxs-lookup"><span data-stu-id="e31d3-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="e31d3-144">Als u wilt dat toomanually reageren toohello `handler` blokkeren in uw code, kunt u nil voor Hallo doorgeven `handler` argument en beheer Hallo voltooiing blokkeren zelf.</span><span class="sxs-lookup"><span data-stu-id="e31d3-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="e31d3-145">Zie Hallo `UIBackgroundFetchResult` type voor een lijst van mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="e31d3-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="e31d3-146">Compleet voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e31d3-146">Full example</span></span>
<span data-ttu-id="e31d3-147">Hier volgt een voorbeeld van een volledige integratie:</span><span class="sxs-lookup"><span data-stu-id="e31d3-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="e31d3-148">UNUserNotificationCenter gemachtigde conflicten oplossen</span><span class="sxs-lookup"><span data-stu-id="e31d3-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="e31d3-149">*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*</span><span class="sxs-lookup"><span data-stu-id="e31d3-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="e31d3-150">Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door Hallo SDK toomonitor Hallo levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e31d3-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="e31d3-151">Hallo SDK heeft een eigen implementatie Hallo `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing.</span><span class="sxs-lookup"><span data-stu-id="e31d3-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="e31d3-152">Geen andere gedelegeerde toegevoegd toohello `UNUserNotificationCenter` object Hello Engagement een conflict veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="e31d3-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="e31d3-153">Als Hallo SDK uw of een andere leveranciers gemachtigde detecteert en maakt geen gebruik van een eigen implementatie toogive Hallo u een kans tooresolve conflicten.</span><span class="sxs-lookup"><span data-stu-id="e31d3-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="e31d3-154">Hebt u tooadd Hallo Engagement logica tooyour eigenaar gemachtigde in volgorde tooresolve Hallo conflicten.</span><span class="sxs-lookup"><span data-stu-id="e31d3-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="e31d3-155">Er zijn twee manieren tooachieve dit.</span><span class="sxs-lookup"><span data-stu-id="e31d3-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="e31d3-156">Voorstel 1, door de gemachtigde doorsturen roept toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="e31d3-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="e31d3-157">Of voorstel 2, door het overnemen van Hallo `AEUserNotificationHandler` klasse</span><span class="sxs-lookup"><span data-stu-id="e31d3-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="e31d3-158">U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst toohello Agent `isEngagementPushPayload:` klasse-methode.</span><span class="sxs-lookup"><span data-stu-id="e31d3-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="e31d3-159">Zorg ervoor dat Hallo `UNUserNotificationCenter` gemachtigde van het object is ingesteld tooyour gemachtigde binnen een Hallo `application:willFinishLaunchingWithOptions:` of Hallo `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.</span><span class="sxs-lookup"><span data-stu-id="e31d3-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="e31d3-160">Bijvoorbeeld, als u Hallo hierboven voorstel 1 geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="e31d3-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="e31d3-161">Hoe toocustomize campagnes</span><span class="sxs-lookup"><span data-stu-id="e31d3-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="e31d3-162">Meldingen</span><span class="sxs-lookup"><span data-stu-id="e31d3-162">Notifications</span></span>
<span data-ttu-id="e31d3-163">Er zijn twee typen meldingen: systeem en in-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="e31d3-164">Systeemmeldingen worden afgehandeld door iOS en kunnen niet worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="e31d3-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="e31d3-165">In-app-meldingen zijn gemaakt van een weergave die de huidige toepassingsvenster toohello wordt dynamisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="e31d3-166">Dit is een melding overlay genoemd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-166">This is called a notification overlay.</span></span> <span data-ttu-id="e31d3-167">Melding overlays zijn ideaal voor een snelle integratie omdat ze geen vereist toomodify u elke weergave in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e31d3-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="e31d3-168">Lay-out</span><span class="sxs-lookup"><span data-stu-id="e31d3-168">Layout</span></span>
<span data-ttu-id="e31d3-169">toomodify hello uiterlijk van uw in-app-meldingen, kunt u eenvoudig hello bestand wijzigen `AENotificationView.xib` tooyour moet, zolang u Hallo labelwaarden en typen van de bestaande subweergaven Hallo houden.</span><span class="sxs-lookup"><span data-stu-id="e31d3-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="e31d3-170">Standaard worden in-app-meldingen weergegeven onder Hallo van welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="e31d3-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="e31d3-171">Als u liever toodisplay opgegeven ze Hallo boven aan het scherm bewerken Hallo `AENotificationView.xib` en wijzig Hallo `AutoSizing` eigenschap van hoofdweergave Hallo zodat het Hallo boven aan de superview kan worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="e31d3-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="e31d3-172">Categorieën</span><span class="sxs-lookup"><span data-stu-id="e31d3-172">Categories</span></span>
<span data-ttu-id="e31d3-173">Als u Hallo opgegeven lay-out wijzigt, wijzigt u Hallo uiterlijk van al uw meldingen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="e31d3-174">Categorieën kunnen toodefine u die verschillende gericht lijkt (mogelijk gedrag) voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="e31d3-175">Een categorie kan worden opgegeven wanneer u een Reach-campagne maken.</span><span class="sxs-lookup"><span data-stu-id="e31d3-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="e31d3-176">Houd er rekening mee dat categorieën ook kunnen u aanpassen aankondigingen en polls, die verderop in dit document wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="e31d3-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="e31d3-177">tooregister een categorie-handler voor uw meldingen, moet u tooadd een aanroep van zodra Hallo reach-module is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="e31d3-178">`myNotifier`moet een exemplaar van een object dat toohello protocol voldoet `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="e31d3-179">U kunt Hallo protocolmethoden implementeren door uzelf of u kunt bestaande klasse van tooreimplement hello `AEDefaultNotifier` al uitvoert, wordt de meeste Hallo werk.</span><span class="sxs-lookup"><span data-stu-id="e31d3-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="e31d3-180">Bijvoorbeeld, als u de weergave van meldingen Hallo tooredefine voor een specifieke categorie wilt, kunt u dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e31d3-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="e31d3-181">Dit eenvoudige voorbeeld van de categorie wordt ervan uitgegaan dat u hebt een bestand met de naam `MyNotificationView.xib` in de bundel hoofdtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e31d3-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="e31d3-182">Als het Hallo-methode is niet kunnen toofind een overeenkomstige `.xib`, Hallo-melding worden niet weergegeven en Engagement wordt een bericht in de console Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e31d3-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="e31d3-183">Hallo opgegeven kroontjespen bestand moet inachtneming van Hallo volgens de regels voor:</span><span class="sxs-lookup"><span data-stu-id="e31d3-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="e31d3-184">Het moet slechts één weergave bevatten.</span><span class="sxs-lookup"><span data-stu-id="e31d3-184">It should only contain one view.</span></span>
* <span data-ttu-id="e31d3-185">Subweergaven moet van dezelfde zoals Hallo zijn binnen de opgegeven Hallo kroontjespen bestand met de naam typen Hallo`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="e31d3-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="e31d3-186">Subweergaven moeten Hallo dezelfde labels als Hallo zijn binnen de opgegeven Hallo kroontjespen bestand met de naam hebben`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="e31d3-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="e31d3-187">Alleen opgegeven Hallo kroontjespen bestand kopiëren, met de naam `AENotificationView.xib`, en beginnen met werken vanaf daar.</span><span class="sxs-lookup"><span data-stu-id="e31d3-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="e31d3-188">Maar wees voorzichtig, Hallo weergeven binnen dit kroontjespen-bestand is gekoppeld aan de klasse toohello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="e31d3-189">Deze klasse gedefinieerd Hallo methode `layoutSubViews` toomove en het formaat ervan subweergaven volgens toocontext.</span><span class="sxs-lookup"><span data-stu-id="e31d3-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="e31d3-190">U kunt tooreplace deze met een `UIView` of u aangepaste weergave-klasse.</span><span class="sxs-lookup"><span data-stu-id="e31d3-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="e31d3-191">Als u diepere aanpassing van uw meldingen (als u wilt bijvoorbeeld tooload uw weergave rechtstreeks vanuit Hallo code), het verdient aanbeveling tootake bekijkt hello code en klasse documentatie bij de gegevensbron van opgegeven `Protocol ReferencesDefaultNotifier` en `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="e31d3-192">Let op: u kunt dezelfde melder voor verschillende categorieën Hallo.</span><span class="sxs-lookup"><span data-stu-id="e31d3-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="e31d3-193">U kunt ook opnieuw gedefinieerde Hallo standaard melder als volgt:</span><span class="sxs-lookup"><span data-stu-id="e31d3-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="e31d3-194">Afhandeling van melding</span><span class="sxs-lookup"><span data-stu-id="e31d3-194">Notification handling</span></span>
<span data-ttu-id="e31d3-195">Wanneer u de standaardcategorie hello, een aantal methoden levenscyclus worden aangeroepen op Hallo `AEReachContent` tooreport statistieken en update Hallo campagne status object:</span><span class="sxs-lookup"><span data-stu-id="e31d3-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="e31d3-196">Wanneer Hallo melding wordt weergegeven in de toepassing, Hallo `displayNotification` methode (die statistieken) wordt aangeroepen door `AEReachModule` als `handleNotification:` retourneert `YES`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="e31d3-197">Als het Hallo-melding wordt gesloten, Hallo `exitNotification` methode wordt aangeroepen, statistiek wordt gerapporteerd en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e31d3-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="e31d3-198">Als u Hallo melding klikt, `actionNotification` is aangeroepen, statistiek is gerapporteerd en Hallo gekoppeld actie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="e31d3-199">Als uw implementatie van `AENotifier` omleidingen Hallo standaardgedrag, hebt u toocall deze methoden van de levenscyclus van de door u zelf.</span><span class="sxs-lookup"><span data-stu-id="e31d3-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="e31d3-200">Hallo volgen voorbeelden illustreren bepaalde gevallen waarbij Hallo standaardgedrag wordt overgeslagen:</span><span class="sxs-lookup"><span data-stu-id="e31d3-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="e31d3-201">U kunt niet uitbreiden `AEDefaultNotifier`, zoals u categorie verwerking helemaal geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e31d3-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="e31d3-202">U overrode `prepareNotificationView:forContent:`, moet u ervoor dat toomap ten minste `onNotificationActioned` of `onNotificationExited` tooone uw U.I-besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="e31d3-203">Als `handleNotification:` er wordt een uitzondering, Hallo inhoud is verwijderd en `drop` is aangeroepen, dit wordt gemeld in statistieken en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e31d3-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="e31d3-204">Melding als onderdeel van een bestaande weergave opnemen</span><span class="sxs-lookup"><span data-stu-id="e31d3-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="e31d3-205">Overlays zijn ideaal voor een snelle integratie, maar kunnen worden soms niet handig of ongewenste neveneffecten hebben.</span><span class="sxs-lookup"><span data-stu-id="e31d3-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="e31d3-206">Als u niet tevreden met Hallo overlay systeem in een aantal weergaven bent, kunt u deze kunt aanpassen voor deze weergaven.</span><span class="sxs-lookup"><span data-stu-id="e31d3-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="e31d3-207">U kunt tooinclude onze lay-out voor de melding in uw bestaande weergaven.</span><span class="sxs-lookup"><span data-stu-id="e31d3-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="e31d3-208">toodo twee implementatie stijlen dus er is:</span><span class="sxs-lookup"><span data-stu-id="e31d3-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="e31d3-209">Weergave van meldingen Hallo met interface builder toevoegen</span><span class="sxs-lookup"><span data-stu-id="e31d3-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="e31d3-210">Open *Builder Interface*</span><span class="sxs-lookup"><span data-stu-id="e31d3-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="e31d3-211">Een 320 x 60 (of als u op iPad 768 x 60) plaatst `UIView` waar u Hallo melding tooappear</span><span class="sxs-lookup"><span data-stu-id="e31d3-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="e31d3-212">Hallo tagwaarde voor deze weergave te stellen: **36822491**</span><span class="sxs-lookup"><span data-stu-id="e31d3-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="e31d3-213">Weergave van meldingen Hallo programmatisch toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e31d3-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="e31d3-214">Hallo code volgen wanneer de weergave is geïnitialiseerd alleen toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="e31d3-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="e31d3-215">`NOTIFICATION_AREA_VIEW_TAG`macro vindt u in `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="e31d3-216">Standaard-melder Hallo detecteert automatisch die Hallo notification-indeling is opgenomen in deze weergave en wordt een overlay niet toevoegen voor.</span><span class="sxs-lookup"><span data-stu-id="e31d3-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="e31d3-217">Aankondigingen en polls</span><span class="sxs-lookup"><span data-stu-id="e31d3-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="e31d3-218">Indelingen</span><span class="sxs-lookup"><span data-stu-id="e31d3-218">Layouts</span></span>
<span data-ttu-id="e31d3-219">U kunt bestanden Hallo wijzigen `AEDefaultAnnouncementView.xib` en `AEDefaultPollView.xib` , zolang u Hallo labelwaarden en typen van de bestaande subweergaven Hallo houden.</span><span class="sxs-lookup"><span data-stu-id="e31d3-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="e31d3-220">Categorieën</span><span class="sxs-lookup"><span data-stu-id="e31d3-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="e31d3-221">Alternatieve indelingen</span><span class="sxs-lookup"><span data-stu-id="e31d3-221">Alternate layouts</span></span>
<span data-ttu-id="e31d3-222">Zoals meldingen, kan de categorie van de campagne Hallo gebruikte toohave alternatieve indelingen voor uw aankondigingen en polls zijn.</span><span class="sxs-lookup"><span data-stu-id="e31d3-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="e31d3-223">een categorie voor een aankondiging toocreate, moet u uitbreiden **AEAnnouncementViewController** en registreer deze zodra Hallo reach-module is geïnitialiseerd:</span><span class="sxs-lookup"><span data-stu-id="e31d3-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="e31d3-224">Telkens wanneer een gebruiker wordt klikt u op een melding naar een aankondiging met Hallo categorie "Mijn\_categorie ', uw geregistreerde weergavebesturing (in dat geval `MyCustomAnnouncementViewController`) wordt geïnitialiseerd door het Hallo-methode aanroepen `initWithAnnouncement:` en Hallo weergave toegevoegde toohello huidige toepassingsvenster.</span><span class="sxs-lookup"><span data-stu-id="e31d3-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="e31d3-225">Bij de implementatie van Hallo `AEAnnouncementViewController` klasse hebt u tooread Hallo eigenschap `announcement` tooinitialize uw subweergaven.</span><span class="sxs-lookup"><span data-stu-id="e31d3-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="e31d3-226">Overweeg het Hallo-voorbeeld hieronder, waarbij twee labels zijn geïnitialiseerd met behulp van `title` en `body` eigenschappen van Hallo `AEReachAnnouncement` klasse:</span><span class="sxs-lookup"><span data-stu-id="e31d3-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="e31d3-227">Als u niet wilt dat tooload uw weergaven door uzelf, maar u alleen tooreuse Hallo aankondiging weergave standaardindeling wilt, kunt u gewoon de aangepaste weergave-controller Hallo opgegeven klasse uitbreidt `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="e31d3-228">In dat geval dubbele Hallo kroontjespen bestand `AEDefaultAnnouncementView.xib` en wijzig deze zodat deze kan worden geladen door de aangepaste weergave-controller (voor een domeincontroller met de naam `CustomAnnouncementViewController`, moet u het bestand kroontjespen aanroepen `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="e31d3-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="e31d3-229">tooreplace hello standaardcategorie van aankondigingen, registreren gewoon de besturing van de aangepaste weergave voor Hallo categorie gedefinieerd in `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="e31d3-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="e31d3-230">Polls kunnen worden aangepast Hallo dezelfde manier:</span><span class="sxs-lookup"><span data-stu-id="e31d3-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="e31d3-231">Deze tijd, Hallo opgegeven `MyCustomPollViewController` moet uitbreiden `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="e31d3-232">Of u kunt tooextend van Hallo standaard domeincontroller: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="e31d3-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e31d3-233">Vergeet niet toocall ofwel `action` (`submitAnswers:` voor aangepaste poll weergave domeincontrollers) of `exit` methode voordat de weergavebesturing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="e31d3-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="e31d3-234">Anders statistieken niet verzonden (d.w.z. geen analytics op Hallo campagne) en meer belangrijker nog volgende campagnes wordt niet gewaarschuwd als het toepassingsproces Hallo opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="e31d3-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="e31d3-235">Voorbeeldimplementatie</span><span class="sxs-lookup"><span data-stu-id="e31d3-235">Implementation example</span></span>
<span data-ttu-id="e31d3-236">In deze implementatie is Hallo aangepaste aankondiging weergave geladen uit een externe xib-bestand.</span><span class="sxs-lookup"><span data-stu-id="e31d3-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="e31d3-237">Net als voor geavanceerde melding aanpassing, wordt aangeraden toolook op Hallo broncode van de standaardimplementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e31d3-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
