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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Aan de slag met Azure Mobile Engagement voor iOS-apps in Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers tooan iOS-toepassing.
In deze zelfstudie maakt u een lege iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).

Deze zelfstudie vereist de volgende Hallo:

* XCode 8, die u vanuit de Mac App Store kunt installeren.
* Hallo [Mobile Engagement iOS SDK]
* Pushmeldingcertificaat (.p12), dat u kunt verkrijgen via Apple Dev Center.

> [!NOTE]
> In deze zelfstudie wordt gebruikgemaakt van Swift versie 3.0. 
> 
> 

Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Engagement-zelfstudies voor iOS-apps.

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement iOS SDK-integratie](mobile-engagement-ios-sdk-overview.md)

We gaan een eenvoudige app maken met XCode toodemonstrate Hallo integratie:

### <a name="create-a-new-ios-project"></a>Een nieuw iOS-project maken
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Hallo downloaden [Mobile Engagement iOS SDK]
2. Hallo extraheren..GZ-bestand tooa map op uw computer
3. Klik met de rechtermuisknop op Hallo-project en selecteer ' bestanden te toevoegen... "
   
    ![][1]
4. Navigeer toohello map waar u Hallo SDK en selecteer Hallo uitgepakt `EngagementSDK` map druk op OK.
   
    ![][2]
5. Open Hallo `Build Phases` tabblad en in Hallo `Link Binary With Libraries` menu toevoegen Hallo frameworks, zoals hieronder wordt weergegeven:
   
    ![][3]
6. Een Bridging header toobe kunnen toouse Hallo SDK van Objective C-API's maken door naar File > New > File > iOS > Source > Header-bestand.
   
    ![][4]
7. Hallo bridging header-bestand tooexpose Mobile Engagement Objective-C-code tooyour Swift-code bewerken, Hallo na invoer toevoegen:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. Controleer onder Build Settings of Hallo Objective-C Bridging Header bouwen instelling onder Swift Compiler - Code Generation een pad toothis koptekst heeft. Hier volgt een voorbeeld van een pad: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (afhankelijk van het Hallo-pad)**
   
   ![][6]
9. Ga terug toohello Azure-portal in uw app *verbindingsgegevens* pagina en kopieer de verbindingsreeks Hallo
   
   ![][5]
10. Plak nu Hallo-verbindingsreeks in Hallo `didFinishLaunchingWithOptions` delegeren
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Realtime-bewaking inschakelen
U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.

1. Open Hallo **ViewController.swift** -bestand en vervang de basisklasse Hallo van **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract en neem contact met uw gebruikers met Pushmeldingen en In-app-berichten in Hallo context van campagnes. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uw app tooreceive achtergrond-Pushmeldingen inschakelen
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Hallo Reach-bibliotheek tooyour project toevoegen
1. Klik met de rechtermuisknop op het project.
2. Selecteer `Add file too...`
3. Navigeer toohello map waar u Hallo SDK hebt uitgepakt.
4. Selecteer Hallo `EngagementReach` map
5. Klik op Add.
6. Hallo bridging Mobile Engagement Objective-C Reach-headers van header-bestand tooexpose bewerken en Hallo na invoer toevoegen:
   
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

### <a name="modify-your-application-delegate"></a>Uw toepassingsgemachtigde wijzigen
1. Hallo binnen `didFinishLaunchingWithOptions` - maakt een reach-module en geef dit door bestaande initialisatieregel tooyour:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Uw app tooreceive APNS-Pushmeldingen inschakelen
1. Hallo volgende regel toohello toevoegen `didFinishLaunchingWithOptions` methode:
   
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
2. Hallo toevoegen `didRegisterForRemoteNotificationsWithDeviceToken` methode als volgt:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Hallo toevoegen `didReceiveRemoteNotification:fetchCompletionHandler:` methode als volgt:
   
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
