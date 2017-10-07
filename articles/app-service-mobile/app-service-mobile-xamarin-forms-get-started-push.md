---
title: aaaAdd push notifications tooyour Xamarin.Forms-app | Microsoft Docs
description: Meer informatie over hoe toouse Azure services toosend meerdere platforms push notifications tooyour Xamarin.Forms-apps.
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Push notifications tooyour Xamarin.Forms-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overzicht
In deze zelfstudie maakt u push notifications tooall Hallo projecten die het gevolg zijn van Hallo toevoegen [Xamarin.Forms snel starten](app-service-mobile-xamarin-forms-get-started.md). Dit betekent dat een push-melding tooall platformoverschrijdende clients verzonden telkens wanneer een record wordt ingevoegd.

Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket. Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Vereisten
Voor iOS, moet u een [Apple Developer Program-lidmaatschap](https://developer.apple.com/programs/ios/) en een fysiek iOS-apparaat. Hallo [iOS-simulator biedt geen ondersteuning voor pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Een notification hub configureren
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Hallo server project toosend-pushmeldingen bijwerken
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Configureren en uitvoeren van Hallo Android-project (optioneel)
Deze sectie tooenable pushmeldingen voor Hallo Xamarin.Forms Droid-project voor Android worden voltooid.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Firebase Cloud Messaging (FCM) inschakelen
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Hallo Mobile Apps back-end toosend push aanvragen configureren met behulp van FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Push notifications toohello Android-project toevoegen
Hallo back-end geconfigureerd met het FCM, kunt u onderdelen en codes toohello client tooregister met FCM toevoegen. U kunt ook registreren voor pushmeldingen met Azure Notification Hubs via Hallo Mobile Apps terug beëindigen en meldingen ontvangen.

1. In Hallo **Droid** project, klik met de rechtermuisknop op Hallo **onderdelen** map en klik op **meer onderdelen ophalen...** . Zoek vervolgens naar Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project. Dit onderdeel biedt ondersteuning voor pushmeldingen voor een Xamarin.android-project.
2. Hallo MainActivity.cs projectbestand openen en Hallo Hallo boven aan het bestand Hallo-instructie toe:

        using Gcm.Client;
3. Hallo na code toohello toevoegen **OnCreate** te aanroep van servermethode na Hallo**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Voeg een nieuwe **CreateAndShowDialog** Help-methode, als volgt:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Hallo na code toohello toevoegen **MainActivity** klasse:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    Dit wordt de huidige Hallo **MainActivity** exemplaar, zodat kan worden uitgevoerd op Hallo belangrijkste UI-thread.
6. Hallo initialiseren `instance` variabele aan begin Hallo Hallo **OnCreate** methode als volgt.

        // Set hello current instance of MainActivity.
        instance = this;
7. Voeg een nieuwe klasse bestand toohello **Droid** project met de naam `GcmService.cs`, en zorg ervoor dat Hallo volgende **met** instructies Hallo boven aan het Hallo-bestand aanwezig zijn:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Toevoegen van de volgende machtigingsaanvragen Hallo boven aan het Hallo-bestand, na het Hallo Hallo **met** instructies en vóór Hallo **naamruimte** declaratie.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Voeg Hallo klasse definitie toohello naamruimte te volgen.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Vervang **< PROJECT_NUMBER >** met het projectnummer van uw u eerder hebt genoteerd.    
   >
   >
10. Vervang Hallo leeg **GcmService** klasse met de volgende code, die gebruikmaakt van nieuwe broadcast ontvanger Hallo Hallo:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Hallo na code toohello toevoegen **GcmService** klasse. Overschrijft dit Hallo **OnRegistered** gebeurtenis-handler en implementeert een **registreren** methode.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Deze code wordt Hallo `messageParam` parameter Hallo sjabloon registratie.
12. Toevoegen na de code die wordt geïmplementeerd Hallo **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Dit binnenkomende berichten worden verwerkt en verzendt deze toohello notification manager toobe weergegeven.
13. **GcmServiceBase** moet u ook tooimplement hello **OnUnRegistered** en **bij fout** handler-methoden, die u kunt als volgt:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Nu u gereed test pushmeldingen in Hallo app uitgevoerd op een Android-apparaat of emulator Hallo.

### <a name="test-push-notifications-in-your-android-app"></a>Pushmeldingen testen in uw Android-app
Hallo eerste twee stappen zijn vereist, alleen wanneer u op een emulator test.

1. Zorg ervoor dat u tooor foutopsporing op een virtueel apparaat met Google APIs ingesteld als doel hello implementeert, zoals hieronder wordt weergegeven in Hallo Android Virtual Device manager.
2. Een apparaat toohello Android van Google-account toevoegen door te klikken op **Apps** > **instellingen** > **account toevoegen**. Volg daarna Hallo prompts tooadd een bestaand apparaat van Google-account toohello of toocreate een nieuwe.
3. In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **Droid** project en klik op **instellen als opstartproject**.
4. Klik op **uitvoeren** toobuild Hallo project en Hallo-app op uw Android-apparaat of emulator te starten.
5. Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.
6. Controleer of dat er een melding wordt ontvangen wanneer een item wordt toegevoegd.

## <a name="configure-and-run-hello-ios-project-optional"></a>Configureren en uitvoeren van Hallo iOS-project (optioneel)
Deze sectie is voor het uitvoeren van Hallo Xamarin iOS-project voor iOS-apparaten. Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Hallo notification hub configureren voor APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Vervolgens configureert u instelling Hallo iOS-project in Xamarin Studio of Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Push notifications tooyour iOS-app toevoegen
1. In Hallo **iOS** project, opent u AppDelegate.cs en toevoegen van de volgende instructie toohello boven aan het codebestand Hallo Hallo.

        using Newtonsoft.Json.Linq;
2. In Hallo **AppDelegate** klasse, Voeg een onderdrukking voor Hallo **RegisteredForRemoteNotifications** gebeurtenis tooregister voor meldingen:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. In **AppDelegate**, ook toevoegen na onderdrukken voor Hallo Hallo **DidReceiveRemoteNotification** gebeurtenis-handler:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Deze methode verwerkt de inkomende meldingen terwijl Hallo-app wordt uitgevoerd.
4. In Hallo **AppDelegate** klasse, het toevoegen van Hallo na code toohello **FinishedLaunching** methode:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Dit biedt ondersteuning voor externe meldingen en push-registratie van aanvragen.

Uw app is nu bijgewerkte toosupport pushmeldingen.

#### <a name="test-push-notifications-in-your-ios-app"></a>Pushmeldingen testen in uw iOS-app
1. Met de rechtermuisknop op Hallo iOS-project en klik op **instellen als opstartproject**.
2. Druk op Hallo **uitvoeren** knop of **F5** in Visual Studio toobuild Hallo project en Hallo-app te starten in een iOS-apparaat. Klik vervolgens op **OK** tooaccept pushmeldingen.

   > [!NOTE]
   > U moet expliciet pushmeldingen accepteren van uw app. Deze aanvraag is alleen sprake Hallo eerste keer is dat Hallo app wordt uitgevoerd.
   >
   >
3. Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.
4. Controleer of een melding wordt ontvangen, en klik vervolgens op **OK** toodismiss Hallo melding.

## <a name="configure-and-run-windows-projects-optional"></a>Configureren en uitvoeren van Windows-projecten (optioneel)
Deze sectie is voor het uitvoeren van Hallo Xamarin.Forms WinApp en WinPhone81 projecten voor Windows-apparaten. Deze stappen bieden ook ondersteuning voor Universal Windows Platform (UWP)-projecten. Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Uw Windows-app voor pushmeldingen registreren met Windows Notification Service (WNS)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Hallo notification hub configureren voor WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Push notifications tooyour Windows-app toevoegen
1. Open in Visual Studio **App.xaml.cs** in een Windows-project en voeg Hallo instructies te volgen.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Vervang `<your_TodoItemManager_portable_class_namespace>` met de naamruimte van uw draagbare project met Hallo Hallo `TodoItemManager` klasse.
2. Voeg in App.xaml.cs Hallo volgende **InitNotificationsAsync** methode:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Deze methode Hallo push notification channel opgehaald en wordt een sjabloon tooreceive Sjabloonmeldingen van uw notification hub geregistreerd. Een sjabloon melding die ondersteuning biedt voor *messageParam* toothis client wordt geleverd.
3. Werk in App.xaml.cs hello **OnLaunched** gebeurtenis-handler methodedefinitie door toe te voegen Hallo `async` aanpassingsfunctie. Voeg vervolgens Hallo volgende regel code achter Hallo Hallo-methode toe:

        await InitNotificationsAsync();

    Dit zorgt ervoor dat de registratie voor pushberichten hello wordt gemaakt of vernieuwd telkens wanneer het Hallo-app wordt gestart. Het is belangrijk toodo deze tooguarantee die WNS push kanaal Hallo altijd actief is.  
4. Open in Solution Explorer voor Visual Studio Hallo **Package.appxmanifest** bestand en stel **Toast geschikt** te**Ja** onder **meldingen**.
5. Hallo-app bouwen en controleer of er geen fouten. Uw client-app moet nu registreren voor Hallo de Sjabloonmeldingen van Hallo dat Mobile Apps back-end. Herhaal deze sectie voor elke Windows-project in uw oplossing.

#### <a name="test-push-notifications-in-your-windows-app"></a>Pushmeldingen testen in uw Windows-app
1. Met de rechtermuisknop op een Windows-project in Visual Studio, en klik op **instellen als opstartproject**.
2. Druk op Hallo **uitvoeren** knop toobuild Hallo-project en het Hallo-app te starten.
3. Typ een naam voor een nieuwe stukje in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram tooadd deze.
4. Controleer of dat er een melding wordt ontvangen wanneer Hallo item wordt toegevoegd.

## <a name="next-steps"></a>Volgende stappen
U kunt meer informatie over pushmeldingen:

* [Push notification problemen vaststellen](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten. Dit onderwerp leest u hoe tooanalyze en uitzoeken Hallo hoofdmap push notification fouten veroorzaken.

U kunt ook doorwerken op tooone Hallo volgende zelfstudies:

* [Verificatie tooyour app toevoegen](app-service-mobile-xamarin-forms-get-started-users.md)  
  Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Meer informatie over hoe tooadd offlineondersteuning voor uw app met behulp van een mobiele Apps van back-end. Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
