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
# <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Voor elke nieuwe versie van Hallo SDK moet u eerst vervangen (verwijderen en opnieuw te importeren in xcode) Hallo EngagementSDK en EngagementReach mappen.

## <a name="from-300-too400"></a>Van 3.0.0 too4.0.0
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

### <a name="usernotifications-framework"></a>UserNotifications framework
U moet tooadd hello `UserNotifications` framework in uw fasen bouwen.

in Projectverkenner hello, opent u het deelvenster van uw project en selecteer Hallo juiste doel. Open vervolgens Hallo **'Buildfasen'** tabblad en in Hallo **'Link Binary With Libraries'** menu toevoegen framework `UserNotifications.framework` -set Hallo koppelen als`Optional`

### <a name="application-push-capability"></a>Toepassing push mogelijkheid
XCode 8 opnieuw kunnen instellen voor uw app push mogelijkheid, Controleer of deze klopt in Hallo `capability` tabblad van het geselecteerde doel.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Hallo nieuwe iOS 10 kennisgeving registratiecode toevoegen
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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter gemachtigde conflicten oplossen

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

## <a name="from-200-too300"></a>Van 2.0.0 too3.0.0
Ondersteuning voor iOS verwijderd 4.X. Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 6.

Als u van Reach in uw toepassing gebruikmaakt, moet u toevoegen `remote-notification` waarde toohello `UIBackgroundModes` matrix in uw Info.plist-bestand in de volgorde tooreceive externe meldingen.

Hallo methode `application:didReceiveRemoteNotification:` moet toobe vervangen door `application:didReceiveRemoteNotification:fetchCompletionHandler:` in uw toepassingsgemachtigde.

'AEPushDelegate.h' is afgeschaft interface en u moet tooremove alle verwijzingen. Dit omvat het verwijderen van `[[EngagementAgent shared] setPushDelegate:self]` en Hallo delegeren methoden uit uw toepassingsgemachtigde:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>Van 1.16.0 too2.0.0
Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement.
Als u vanaf een eerdere versie migreert, raadpleegt u eerst Hallo Capptain website toomigrate too1.16 vervolgens toepassing hello procedure te volgen.

> [!IMPORTANT]
> Capptain en Mobile Engagement dezelfde services niet zijn Hallo en Hallo onderstaande procedure alleen illustreert hoe toomigrate Hallo client-app. Uw gegevens worden niet van Hallo Capptain servers toohello Mobile Engagement servers migreren Hallo SDK in Hallo-app gemigreerd
> 
> 

### <a name="agent"></a>Agent
Hallo methode `registerApp:` is vervangen door de nieuwe methode Hallo `init:`. Uw toepassingsgemachtigde dienovereenkomstig moeten worden bijgewerkt en verbindingsreeks gebruiken:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

SmartAd bijhouden is verwijderd uit de SDK die u zojuist tooremove alle exemplaren van hebt `AETrackModule` klasse

### <a name="class-name-changes"></a>Wijzigingen in de klasse naam
Als onderdeel van het Hallo rebranding, zijn er enkele klasse/bestandsnamen die toobe gewijzigd moeten.

Alle klassen die worden voorafgegaan door 'CP' worden met het voorvoegsel 'AE' gewijzigd.

Voorbeeld:

* `CPModule.h`de naam wordt gewijzigd te`AEModule.h`.

Alle klassen die worden voorafgegaan door 'Capptain' worden met het voorvoegsel 'Engagement' gewijzigd.

Voorbeelden:

* Hallo klasse `CapptainAgent` wordt gewijzigd te`EngagementAgent`.
* Hallo klasse `CapptainTableViewController` wordt gewijzigd te`EngagementTableViewController`.
* Hallo klasse `CapptainUtils` wordt gewijzigd te`EngagementUtils`.
* Hallo klasse `CapptainViewController` wordt gewijzigd te`EngagementViewController`.

