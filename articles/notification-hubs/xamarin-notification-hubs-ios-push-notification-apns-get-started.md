---
title: aaaiOS Pushmeldingen met Notification Hubs voor Xamarin-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin iOS-toepassing.
services: notification-hubs
keywords: ios-pushmeldingen,pushberichten,pushmeldingen,pushbericht
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>iOS-pushmeldingen met Notification Hubs voor Xamarin-apps
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
> [!IMPORTANT]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started) voor meer informatie.
> 
> 

Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing.
Maakt u een lege Xamarin.iOS-app die pushmeldingen ontvangt via Hallo [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd. Hallo voltooide code is beschikbaar in Hallo [NotificationHubs-app] [ GitHub] voorbeeld.

Deze zelfstudie wordt Hallo eenvoudige push bericht scenario uitzenden met Notification Hubs.

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* [Xcode 6.0][Install Xcode]
* Een apparaat dat compatibel is met iOS 7.0 (of een hogere versie)
* iOS Developer Program-lidmaatschap
* [Xamarin Studio]
  
  > [!NOTE]
  > Vanwege configuratievereisten voor iOS-pushmeldingen, moet u implementeren en testen van de voorbeeldtoepassing Hallo op een fysiek iOS-apparaat (iPhone of iPad) in plaats van in Hallo simulator.
  > 
  > 

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin iOS-apps.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Uw Notification Hub configureren
Deze sectie leidt u door een nieuwe notification hub maken en configureren van verificatie met APNS met Hallo **.p12** pushcertificaat dat u hebt gemaakt. Als u toouse een notification hub die u al hebt gemaakt wilt, kunt u toostep 5 overslaan.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Als we tooconfigure hello APNS-verbinding in Azure Portal hello wilt open uw Notification Hub-instellingen, en klik op <b>Notification Services</b>, en klik vervolgens op Hallo <b>Apple (APNS)</b> item in de lijst Hallo. Hierna klikt u op <b>certificaat uploaden</b> en selecteer Hallo <b>.p12</b> certificaat dat u eerder, evenals het Hallo-wachtwoord voor Hallo certificaat hebt geëxporteerd.</p>

<p>Zorg ervoor dat tooselect <b>Sandbox</b> modus, aangezien u pushmeldingen verzenden van berichten in een ontwikkelomgeving. Gebruik alleen Hallo <b>productie</b> instelling als u wilt dat toosend push notifications toousers die al in uw app uit de store Hallo bezit.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Uw notification hub is nu geconfigureerd toowork met APNS en u hebt Hallo verbinding tekenreeksen tooregister uw app en om pushmeldingen te verzenden.

## <a name="connect-your-app-toohello-notification-hub"></a>Verbinding maken met uw app toohello notification hub
#### <a name="create-a-new-project"></a>Een nieuw project maken
1. In Xamarin Studio een nieuw iOS-project maken en selecteer Hallo **Unified API** > **enkele toepassingsweergave** sjabloon.
   
     ![Xamarin Studio - Toepassingstype selecteren][31]
2. Voeg een verwijzing toohello Azure Messaging-onderdeel. Hallo weergave oplossing, met de rechtermuisknop op Hallo **onderdelen** map voor uw project en kies **meer onderdelen ophalen**. Zoeken naar Hallo **Azure Messaging** onderdeel en Hallo onderdeel tooyour project toevoegen.
3. In **AppDelegate.cs**, voeg de volgende Hallo met de instructie:
   
        using WindowsAzure.Messaging;
4. Declareer een exemplaar van **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Maak een **Constants.cs** klasse Hello variabelen te volgen:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. In **AppDelegate.cs**, bijwerken **FinishedLaunching()** toomatch Hallo volgende:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Hallo overschrijven **RegisteredForRemoteNotifications()** methode in **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Hallo overschrijven **ReceivedRemoteNotification()** methode in **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Maak de volgende Hallo **ProcessNotification()** methode in **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > U kunt toooverride **FailedToRegisterForRemoteNotifications()** toohandle situaties zoals geen netwerkverbinding. Dit is vooral belangrijk waar Hallo gebruiker uw toepassing bijvoorbeeld starten in de offlinemodus bevindt (bijvoorbeeld in een vliegtuig) en u wilt dat toohandle pushberichten-scenario's voor specifieke tooyour app.
   > 
   > 
10. Hallo-app uitvoeren op uw apparaat.

## <a name="sending-push-notifications"></a>Pushmeldingen verzenden
U kunt testen ontvangen van pushmeldingen in uw app door meldingen te verzenden in Hallo [Azure Portal] via Hallo **Test verzenden** mogelijkheden in Hallo **probleemoplossing** hulpmiddelenset, rechts op Hallo notification hub pagina, zoals weergegeven in onderstaande welkomstscherm.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Pushmeldingen worden gewoonlijk met een compatibele bibliotheek verzonden via een back-endservice zoals Mobile Services of ASP.NET. U kunt ook Hallo REST-API gebruiken direct push toosend berichten als een bibliotheek niet beschikbaar in uw scenario is. 

In deze zelfstudie wordt Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden. We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie. Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:

* **REST-Interface**: U kunt push-melding ondersteunen op elk back-end-platform met Hallo [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).

**Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een back-end voor een Azure App Service Mobile Apps die geïntegreerd met Notification Hubs toosend Zie [Add push notifications tooyour mobiele app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: Zie voor een voorbeeld van hoe toosend pushmeldingen met behulp van REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(Optioneel) Pushmeldingen verzenden vanuit een .NET-console-app
In deze sectie worden pushmeldingen verzonden met een eenvoudige .NET-console-app. Ter Hallo van dit voorbeeld wordt overgeschakeld tooa Windows-ontwikkelomgeving waarin Visual Studio al is geïnstalleerd.

1. Maak in Visual Studio een nieuwe Visual C#-consoletoepassing:
   
       ![Visual Studio - Create a new console application][213]
2. Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.
   
    Hallo package manager-console moet worden weergegeven onder gedokte toohello van uw Visual Studio-werkruimte.
3. In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Open Hallo `Program.cs` -bestand en voeg de volgende Hallo `using` instructie, waarbij u ervoor zorgt dat we Azure-klassen en functies binnen uw hoofdklasse kunnen gebruiken:
   
        using Microsoft.Azure.NotificationHubs;
5. In uw `Program` klasse, Hallo volgende methode toe te voegen (Vergeet niet tooreplace hello **verbindingsreeks** en **hubnaam**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Toevoegen van de volgende regels in Hallo uw `Main` methode:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Druk op Hallo F5 sleutel toorun Hallo app. Binnen enkele seconden wordt een pushmelding op uw apparaat weergegeven. Of u Wi-Fi of een mobiel dataverkeer netwerk gebruikt, zorg ervoor dat er een actieve internetverbinding op Hallo-apparaat.

U vindt alle mogelijke nettoladingen van Hallo in Hallo Apple [Local and Push Notification Programming Guide].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(Optioneel) Meldingen verzenden vanuit een mobiele service
In deze sectie worden pushmeldingen verzonden met een mobiele service via een knooppuntscript.

een melding met behulp van een mobiele service toosend Volg [aan de slag met Mobile Services], en vervolgens:

1. Meld u aan toohello [klassieke Azure-Portal], en selecteer uw mobiele service.
2. Selecteer Hallo **Scheduler** tabblad Hallo bovenaan.
   
       ![Azure Classic Portal - Scheduler][215]
3. Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.
   
       ![Azure Classic Portal - Create new job][216]
4. Wanneer het Hallo-taak is gemaakt, klikt u op Hallo taaknaam. Klik vervolgens op Hallo **Script** tabblad op Hallo bovenste balk.
5. Hallo volgende script in de plannerfunctie invoegen. Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen. Klik op **Opslaan**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Klik op **eenmaal uitvoeren** op de balk onderaan Hallo. U ontvangt een waarschuwing op uw apparaat.

## <a name="next-steps"></a>Volgende stappen
In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw iOS-apparaten. In order tootarget specifieke gebruikers, raadpleegt u de zelfstudie toohello [Notification Hubs gebruiken toopush meldingen toousers]. Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws]. Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs] en in Hallo [Notification Hubs hoe-toofor iOS].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios
[klassieke Azure-Portal]: https://manage.windowsazure.com/
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs hoe-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Notification Hubs gebruiken toopush meldingen toousers]: /manage/services/notification-hubs/notify-users-aspnet
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-dotnet

[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
