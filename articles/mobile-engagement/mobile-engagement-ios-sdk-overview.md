---
title: aaaAzure Mobile Engagement iOS SDK overzicht | Microsoft Docs
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
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>iOS-SDK voor Azure Mobile Engagement
Begin hier tooget alle Hallo details over het Azure Mobile Engagement toointegrate in een iOS-App. Als u toogive dat wilt deze een try Controleer eerst of u doen onze [15 minuten zelfstudie](mobile-engagement-ios-get-started.md).

Klik op toosee hello [SDK-inhoud](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Integratie procedures
1. Begin hier: [hoe toointegrate Mobile Engagement in uw iOS-app](mobile-engagement-ios-integrate-engagement.md)
2. Voor meldingen: [hoe toointegrate Reach (meldingen) in uw iOS-app](mobile-engagement-ios-integrate-engagement-reach.md)
3. Tag plan implementatie: [hoe toouse Hallo Geavanceerd Mobile Engagement tags API in uw iOS-app](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Releaseopmerkingen
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Vaste badges uitgeschakeld op de achtergrond.
* Vaste waarschuwingen op 9 over API's niet aangeroepen in hoofdwachtrij XCode.
* Een geheugenlek vast Reach polls.
* Ondersteuning voor iOS verwijderd 6.X. Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 7.

Zie voor een eerdere versie Hallo [voltooien release-opmerkingen](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Wellicht hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK Zie gemist Hallo voltooid [Procedures Upgrade](mobile-engagement-ios-upgrade-procedure.md).

Voor elke nieuwe versie van Hallo SDK moet u eerst vervangen (verwijderen en opnieuw te importeren in xcode) Hallo EngagementSDK en EngagementReach mappen.

### <a name="from-300-too400"></a>Van 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 is verplicht vanaf versie 4.0.0 Hallo SDK.

> [!NOTE]
> Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Er is een bekend probleem op Hallo reach-module van de vorige versie bij het uitvoeren op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen. toofix dit hebt u tooimplement Hallo API afgeschaft `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft. Zo snel mogelijk moet u tooXCode 8 overschakelen.
>
>

#### <a name="usernotifications-framework"></a>UserNotifications framework
U moet tooadd hello `UserNotifications` framework in uw fasen bouwen.

in Projectverkenner hello, opent u het deelvenster van uw project en selecteer Hallo juiste doel. Open vervolgens Hallo **'Buildfasen'** tabblad en in Hallo **'Link Binary With Libraries'** menu toevoegen framework `UserNotifications.framework` -set Hallo koppelen als`Optional`

#### <a name="application-push-capability"></a>Toepassing push mogelijkheid
XCode 8 opnieuw kunnen instellen voor uw app push mogelijkheid, Controleer of deze klopt in Hallo `capability` tabblad van het geselecteerde doel.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Hallo nieuwe iOS 10 kennisgeving registratiecode toevoegen
Hallo oudere code codefragment tooregister Hallo app toonotifications werkt nog maar maakt gebruik van afgeschaft API's bij het uitvoeren op iOS 10.

Importeren Hallo `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>

In uw toepassingsgemachtigde `application:didFinishLaunchingWithOptions` methode vervangen:

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

door:

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter gemachtigde conflicten oplossen

*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*

Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door Hallo SDK toomonitor Hallo levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger. Hallo SDK heeft een eigen implementatie Hallo `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing. Geen andere gedelegeerde toegevoegd toohello `UNUserNotificationCenter` object Hello Engagement een conflict veroorzaken. Als Hallo SDK uw of een andere leveranciers gemachtigde detecteert en maakt geen gebruik van een eigen implementatie toogive Hallo u een kans tooresolve conflicten. Hebt u tooadd Hallo Engagement logica tooyour eigenaar gemachtigde in volgorde tooresolve Hallo conflicten.

Er zijn twee manieren tooachieve dit.

Voorstel 1, door de gemachtigde doorsturen roept toohello SDK:

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

Of voorstel 2, door het overnemen van Hallo `AEUserNotificationHandler` klasse

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
> U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst toohello Agent `isEngagementPushPayload:` klasse-methode.

Zorg ervoor dat Hallo `UNUserNotificationCenter` gemachtigde van het object is ingesteld tooyour gemachtigde binnen een Hallo `application:willFinishLaunchingWithOptions:` of Hallo `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.
Bijvoorbeeld, als u Hallo hierboven voorstel 1 geïmplementeerd:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
