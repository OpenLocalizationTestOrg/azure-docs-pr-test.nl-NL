---
title: aaaGet gestart met Azure Mobile Engagement voor Xamarin.iOS
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Xamarin.iOS-Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Aan de slag met Azure Mobile Engagement voor Xamarin.iOS-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers in een Xamarin.iOS-toepassing.
In deze zelfstudie maakt u een lege Xamarin.iOS-app die basisgegevens verzamelt en pushmeldingen ontvangt via Apple Push Notification System (APNS).

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

Deze zelfstudie vereist de volgende Hallo:

* [Xamarin Studio](http://xamarin.com/studio). U kunt ook Visual Studio gebruiken met Xamarin, maar deze zelfstudie gebruikt Xamarin Studio. Zie [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installatie voor Visual Studio en Xamarin) voor installatie-instructies. 
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie' hello minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.

We gaan een eenvoudige app maken met Xamarin toodemonstrate Hallo integratie:

### <a name="create-a-new-xamarinios-project"></a>Een nieuw Xamarin.iOS-project maken
1. Start Xamarin Studio. Ga te**bestand** -> **nieuw** -> **oplossing** 
   
    ![][1]
2. Selecteer **Single View App**, Controleer of de taal Hallo geselecteerd **C#** en klik vervolgens op **volgende**.
   
    ![][2]
3. Vul Hallo **Appnaam** en Hallo **organisatie-id** en klik vervolgens op **volgende**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Zorg ervoor dat Hallo publiceren profiel die u uiteindelijk toodeploy die uw iOS-app is met behulp van een App-ID die overeenkomt met exact met Hallo bundel-id hier gebruiken. 
   > 
   > 
4. Update Hallo **projectnaam**, **oplossingsnaam** en **locatie** indien nodig, en klik op **maken**.
   
    ![][4]

Xamarin Studio maakt Hallo demo-app waarin we Mobile Engagement gaan integreren. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Klik met de rechtermuisknop op Hallo **pakketten** map in Hallo Solution en selecteer **pakketten toevoegen...**
   
    ![][5]
2. Zoeken naar Hallo **Microsoft Azure Mobile Engagement Xamarin SDK** en toe te voegen tooyour oplossing.  
   
    ![][6]
3. Open **AppDelegate.cs** en voeg de volgende Hallo toe met de instructie:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. In Hallo **FinishedLaunching** methode toevoegen Hallo tooinitialize Hallo verbinding met de back-end van Mobile Engagement te volgen. Zorg ervoor dat tooadd uw **ConnectionString**. Deze code wordt een dummy **NotificationIcon** toegevoegd door Mobile Engagement SDK die u kunt Hallo tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Realtime-bewaking inschakelen
U moet ten minste één scherm toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen Hallo gebruikers actief zijn.

1. Open **ViewController.cs** en voeg de volgende Hallo toe met de instructie:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Vervang Hallo klasse waarvan `ViewController` neemt over van `UIViewController` te`EngagementViewController`. 

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="modify-your-application-delegate"></a>Uw toepassingsgemachtigde wijzigen
1. Open Hallo **AppDelegate.cs** en voeg de volgende Hallo toe met de instructie:
   
        using System; 
2. Nu binnen Hallo `FinishedLaunching` methode Hallo na tooregister van pushberichten na toevoegen`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Ten slotte - bijwerken of toevoegen Hallo volgende methoden:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. In uw **Info.plist** bestand in Hallo-oplossing, bevestig dat Hallo **bundel-id** overeenkomt met de Hallo **App-ID** hebt in uw inrichtingsprofiel in Hallo Apple Dev Center. 
   
    ![][7]
5. Hallo in dezelfde **Info.plist** bestand, zorg ervoor dat u hebt gecontroleerd dat Hallo **Enable Background Modes** en **Remote Notifications**. 
   
     ![][8]
6. Hallo-app uitvoeren op Hallo-apparaat die u hebt gekoppeld aan dit publicatieprofiel. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
