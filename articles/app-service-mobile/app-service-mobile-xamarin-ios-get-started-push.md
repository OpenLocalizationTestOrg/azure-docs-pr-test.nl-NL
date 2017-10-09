---
title: aaaAdd push notifications tooyour Xamarin.iOS-app met Azure App Service
description: Meer informatie over hoe Azure App Service-toosend toouse push-meldingen tooyour Xamarin.iOS-app
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Push notifications tooyour Xamarin.iOS-App toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overzicht
In deze zelfstudie maakt u een push notifications toohello toevoegen [Xamarin.iOS snel starten](app-service-mobile-xamarin-ios-get-started.md) project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.

Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket. Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.

## <a name="prerequisites"></a>Vereisten
* Volledige Hallo [Xamarin.iOS Quick Start](app-service-mobile-xamarin-ios-get-started.md) zelfstudie.
* Een fysiek iOS-apparaat. Pushmeldingen worden niet ondersteund door Hallo iOS-simulator.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Hallo-app voor pushmeldingen op Apple developer-portal te registreren
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Uw mobiele App toosend-pushmeldingen configureren
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Hallo server project toosend-pushmeldingen bijwerken
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Configureer uw Xamarin.iOS-project
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Push notifications tooyour app toevoegen
1. In **QSTodoService**, Hallo na eigenschap toevoegen zodat **AppDelegate** Hallo mobiele clients kunt verkrijgen:
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo **AppDelegate.cs** bestand.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. In **AppDelegate**, overschrijven Hallo **FinishedLaunching** gebeurtenis:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. In hetzelfde bestand Hallo, overschrijven Hallo **RegisteredForRemoteNotifications** gebeurtenis. In deze code registreert u voor een eenvoudige sjabloon melding die door Hallo-server worden verzonden voor alle ondersteunde platforms.
   
    Zie voor meer informatie over sjablonen met Notification Hubs [sjablonen](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. Vervolgens overschrijven Hallo **DidReceivedRemoteNotification** gebeurtenis:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

Uw app is nu bijgewerkte toosupport pushmeldingen.

## <a name="test"></a>Pushmeldingen testen in uw app
1. Druk op Hallo **uitvoeren** toobuild Hallo project knop Hallo-app te starten in een compatibele iOS-apparaat, en klikt u op **OK** tooaccept pushmeldingen.
   
   > [!NOTE]
   > U moet expliciet pushmeldingen accepteren van uw app. Deze aanvraag is alleen sprake Hallo eerste keer is dat Hallo app wordt uitgevoerd.
   > 
   > 
2. Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.
3. Controleer of een melding wordt ontvangen en klik op **OK** toodismiss Hallo melding.
4. Herhaal stap 2 en onmiddellijk sluiten Hallo app en controleer of er een melding wordt weergegeven.

Deze zelfstudie hebt voltooid.

<!-- Images. -->

<!-- URLs. -->



