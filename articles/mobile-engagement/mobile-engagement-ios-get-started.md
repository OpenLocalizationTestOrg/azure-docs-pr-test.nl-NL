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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Aan de slag met Azure Mobile Engagement voor iOS-apps in Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers tooan iOS-toepassing.
In deze zelfstudie maakt u een lege iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).

Deze zelfstudie vereist de volgende Hallo:

* XCode 8, die u vanuit de Mac App Store kunt installeren.
* Hallo [Mobile Engagement iOS SDK]

Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Engagement-zelfstudies voor iOS-apps.

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started) voor meer informatie.
>
>

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement iOS SDK-integratie](mobile-engagement-ios-sdk-overview.md)

We gaan een eenvoudige app maken met XCode toodemonstrate Hallo-integratie.

### <a name="create-a-new-ios-project"></a>Een nieuw iOS-project maken
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
1. Hallo downloaden [Mobile Engagement iOS SDK].
2. Hallo extraheren..GZ-bestand tooa map op uw computer.
3. Met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Add File to**.

    ![][1]
4. Navigeer toohello map waar u Hallo SDK hebt uitgepakt, selecteer Hallo `EngagementSDK` map, klikt u op **opties** Hallo linksonder en zorg ervoor dat dit selectievakje Hallo **items kopiëren indien nodig** en Hallo selectievakje in voor uw doel zijn geselecteerd en druk vervolgens **OK**.

    ![][2]
5. Open Hallo **Build Phases** tabblad en in Hallo **Link Binary With Libraries** menu Voeg Hallo-frameworks toe, zoals hieronder wordt weergegeven:

    ![][3]
6. Ga terug toohello Azure-portal in uw app **verbindingsgegevens** pagina en kopieer Hallo-verbindingsreeks.

    ![][4]
7. Toevoegen Hallo volgende regel code in uw **AppDelegate.m** bestand.

        #import "EngagementAgent.h"
8. Plak nu Hallo-verbindingsreeks in Hallo `didFinishLaunchingWithOptions` delegeren.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`is een optionele instructie waarmee de SDK-logboeken voor u tooidentify problemen.

## <a id="monitor"></a>Realtime-bewaking inschakelen
U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.

1. Open Hallo **ViewController.h** bestand en importeer **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Vervang nu de bovenliggende klasse Hallo Hallo **ViewController** interface door `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uw app tooreceive achtergrond-Pushmeldingen inschakelen
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Hallo Reach-bibliotheek tooyour project toevoegen
1. Klik met de rechtermuisknop op het project.
2. Selecteer **Add file to**.
3. Navigeer toohello map waar u Hallo SDK hebt uitgepakt.
4. Selecteer Hallo `EngagementReach` map.
5. Klik op **Add**.

### <a name="modify-your-application-delegate"></a>Uw toepassingsgemachtigde wijzigen
1. Terug in de **AppDeletegate.m** bestand, Hallo Engagement bereiken module importeren.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Hallo binnen `application:didFinishLaunchingWithOptions` methode, maakt u een Reach-module en geef dit door bestaande initialisatieregel tooyour:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Uw app tooreceive APNS-Pushmeldingen inschakelen
1. Hallo volgende regel toohello toevoegen `application:didFinishLaunchingWithOptions` methode:

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
2. Hallo toevoegen `application:didRegisterForRemoteNotificationsWithDeviceToken` methode als volgt:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Hallo toevoegen `didFailToRegisterForRemoteNotificationsWithError` methode als volgt:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Hallo toevoegen `didReceiveRemoteNotification:fetchCompletionHandler` methode als volgt:

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
