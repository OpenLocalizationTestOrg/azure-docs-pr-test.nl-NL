---
title: aaaGet slag met Notification Hubs voor Xamarin.Android-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin.android-toepassing.
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Aan de slag met Notification Hubs met Xamarin voor Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin.Android-toepassing.
U maakt een lege Xamarin.Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM). Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd. Hallo voltooide code is beschikbaar in Hallo [NotificationHubs-app] [ GitHub] voorbeeld.

Deze zelfstudie wordt Hallo eenvoudige scenario uitzenden met Notification hubs beschreven.

## <a name="before-you-begin"></a>Voordat u begint
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* Visual Studio met Xamarin in Windows of Xamarin Studio in Mac OS X. U vindt de volledige installatie-instructies in [Instellen en installeren voor Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Actief Google-account
* [Azure Messaging-onderdeel]
* [Google Cloud Messaging-clientonderdeel]

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin.Android-apps.

> [!IMPORTANT]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F) voor meer informatie.
> 
> 

## <a name="enable-google-cloud-messaging"></a>Google Cloud Messaging inschakelen
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Uw Notification Hub configureren
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Klik op Hallo <b>configureren</b> tabblad Hallo bovenaan, Voer Hallo <b>API-sleutel</b> waarde als u hebt verkregen in de vorige sectie Hallo en klik vervolgens op <b>opslaan</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Uw notification hub is nu geconfigureerd toowork bij GCM en u Hallo verbinding tekenreeksen tooboth uw app tooreceive meldingen en toosend pushmeldingen registreren hebt.

## <a name="connect-your-app-toohello-notification-hub"></a>Verbinding maken met uw app toohello notification hub
### <a name="create-a-new-project"></a>Een nieuw project maken
1. Klik in Xamarin Studio op **Nieuwe oplossing**, klik op **Android-app** en klik op **Volgende**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Voer uw **appnaam** en **id** in. Klik op Hallo **doelplatforms** u toosupport wilt en klik vervolgens op **volgende** en **maken**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Hierop wordt een nieuw Android-project gemaakt.

1. Hallo Projecteigenschappen openen met de rechtermuisknop op het nieuwe project in Hallo weergave oplossing kiezen **opties**. Selecteer Hallo **Android-toepassing** item in Hallo **bouwen** sectie.
   
    Zorg ervoor dat Hallo eerste letter van uw **pakketnaam** in kleine letters.
   
   > [!IMPORTANT]
   > de eerste letter Hallo van Hallo pakketnaam moet een kleine letter. Als dit niet zo is, worden er toepassingsmanifestfouten weergegeven wanneer u hieronder uw **BroadcastReceiver** en **IntentFilter** voor pushmeldingen registreert.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Eventueel set Hallo **minimumversie van android** tooanother API-niveau.
3. Eventueel set Hallo **doelversie van android** toohello een andere API-versie die u wilt dat tootarget (moet API-niveau 8 of hoger).

Klik op **OK** en sluiten Hallo Projectopties dialoogvenster.

### <a name="add-hello-required-components-tooyour-project"></a>Hallo vereiste onderdelen tooyour project toevoegen
Hallo Google Cloud Messaging-Client beschikbaar is op Hallo Xamarin Component Store vereenvoudigt Hallo ondersteunen van pushmeldingen in Xamarin.Android.

1. Met de rechtermuisknop op de map voor Hallo-onderdelen in de Xamarin.Android-app en kies **meer onderdelen ophalen**.
2. Zoeken naar Hallo **Azure Messaging** onderdeel en toe te voegen toohello project.
3. Zoeken naar Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project.

### <a name="set-up-notification-hubs-in-your-project"></a>Notification Hubs in uw project instellen
1. Verzamel de volgende informatie voor uw Android-app en notification hub Hallo:
   
   * **GoogleProjectNumber**: dit Project Number-waarde niet ophalen uit Hallo overzicht van uw app op Hallo Google Developer-Portal. U hebt aangebracht een notitie van deze waarde genoteerd toen u Hallo-app op Hallo portal gemaakt.
   * **Verbindingsreeks voor luisteren**: op Hallo dashboard in Hallo [klassieke Azure-Portal], klikt u op **verbindingsreeksen weergeven**. Kopiëren Hallo *DefaultListenSharedAccessSignature* verbindingsreeks voor deze waarde.
   * **Hubnaam**: dit is de naam Hallo van uw hub uit Hallo [klassieke Azure-Portal]. Bijvoorbeeld *mynotificationhub2*.
     
     Maak een **Constants.cs** klasse voor uw Xamarin-project en definieer Hallo constante waarden in de klasse hello te volgen. Vervang Hallo tijdelijke aanduidingen door uw waarden.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Voeg de volgende Hallo using-instructies te**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Toevoegen van een variabele toohello exemplaar `MainActivity` klasse die gebruikt tooshow een waarschuwingsvenster worden wanneer Hallo-app wordt uitgevoerd:
   
        public static MainActivity instance;
4. Maken van de volgende methode in Hallo Hallo **MainActivity** klasse:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. In Hallo `OnCreate` methode van **MainActivity.cs**, initialiseren Hallo `instance` variabele en voeg een aanroep te`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Maak een nieuwe klasse, **MyBroadcastReceiver**.
   
   > [!NOTE]
   > U wordt hieronder begeleid bij het maken van een geheel nieuwe klasse **BroadcastReceiver**. Echter, het maken van een snelle alternatieve toomanually **MyBroadcastReceiver.cs** toorefer toohello is **GcmService.cs** bestand vinden in het Hallo Xamarin.Android-voorbeeldproject opgenomen Hello [NotificationHubs-voorbeelden][GitHub]. Het dupliceren van **GcmService.cs** en wijzigen van klassenamen kan ook een goede plaats-toostart.
   > 
   > 
7. Voeg de volgende Hallo using-instructies te**MyBroadcastReceiver.cs** (verwijst toohello onderdeel en de assembly die u eerder hebt toegevoegd):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. In **MyBroadcastReceiver.cs**, toevoegen van de volgende machtigingsaanvragen tussen Hallo Hallo **met** -instructies en Hallo **naamruimte** declaratie:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. In **MyBroadcastReceiver.cs**, Hallo wijzigen **MyBroadcastReceiver** toomatch Hallo volgende klasse:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Voeg een andere klasse in **MyBroadcastReceiver.cs** toe met de naam **PushHandlerService** die is afgeleid van **GcmServiceBase**. Zorg ervoor dat tooapply hello **Service** toohello kenmerkklasse:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. Met **GcmServiceBase** worden de volgende methoden geïmplementeerd: **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** en **OnError()**. Onze **PushHandlerService** implementatieklasse moet deze methoden overschrijven en deze methoden antwoord toointeracting bij Hallo notification hub wordt geactiveerd.
12. Hallo overschrijven **OnRegistered()** methode in **PushHandlerService** met behulp van de volgende code Hallo:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > In Hallo **OnRegistered()** code hierboven, let u Hallo mogelijkheid toospecify labels tooregister voor specifieke berichtenkanalen.
    > 
    > 
13. Hallo overschrijven **OnMessage** methode in **PushHandlerService** met behulp van de volgende code Hallo:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Voeg de volgende Hallo **createNotification** en **dialogNotify** methoden te**PushHandlerService** om gebruikers te informeren wanneer een melding wordt ontvangen.
    
    > [!NOTE]
    > Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies. Als u dit op Android 5.0 of hoger testen moet Hallo app toobe tooreceive Hallo melding uitgevoerd. Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Overschrijf abstracte leden **OnUnRegistered()**, **OnRecoverableError()** en **OnError()** zodat uw code wordt gecompileerd:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Uitvoeren van uw app in Hallo-emulator
Als u deze app in Hallo-emulator uitvoert, zorg ervoor dat u een Android Virtual Device (AVD) die ondersteuning biedt voor Google APIs gebruikt.

> [!IMPORTANT]
> In de volgorde tooreceive pushmeldingen, moet u een Google-account instellen op uw Android Virtual Device. (In Hallo-emulator te navigeren**instellingen** en klik op **Account toevoegen**.) Zorg ook dat Hallo-emulator is verbonden toohello Internet.
> 
> [!NOTE]
> Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies. Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.
> 
> 

1. Klik in **Extra** op **Android Emulator Manager openen**, selecteer uw apparaat en klik vervolgens op **Bewerken**.
   
      ![][18]
2. Selecteer **Google API's** in **Doel** en klik vervolgens op **OK**.
   
      ![][19]
3. Op de bovenste werkbalk Hallo **uitvoeren**, en selecteer vervolgens uw app. Hiermee start Hallo-emulator en Hallo app uitvoert.
   
   Hallo app haalt Hallo *registrationId* van GCM en wordt geregistreerd bij Hallo notification hub.

## <a name="send-notifications-from-your-backend"></a>Meldingen verzenden vanuit uw back-end
U kunt testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [klassieke Azure-Portal] via Hallo debug tabblad op Hallo notification hub, zoals wordt weergegeven in onderstaande welkomstscherm.

![][30]

Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek. U kunt ook Hallo REST-API gebruiken direct toosend worden meldingsberichten als een bibliotheek niet beschikbaar voor uw back-end is.

Hier volgt een lijst met andere zelfstudies mogelijk wilt u tooreview voor verzenden van meldingen:

* ASP.NET: Zie [Notification Hubs gebruiken toopush meldingen toousers].
* Azure Notification Hubs Java SDK: Zie [hoe toouse Notification Hubs vanuit Java](notification-hubs-java-push-notification-tutorial.md) voor het verzenden van meldingen vanuit Java. Dit is getest in Eclipse voor Android-ontwikkeling.
* PHP: Zie [hoe toouse Notification Hubs vanuit PHP](notification-hubs-php-push-notification-tutorial.md).

In de volgende subsecties Hallo Hallo zelfstudie verzendt u meldingen met behulp van een .NET-consoletoepassing en met behulp van een mobiele service via een knooppuntscript.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Optioneel) Meldingen verzenden met een .NET-app
In deze sectie worden meldingen verzonden met een .NET-console-app.

1. Maak een nieuwe Visual C#-consoletoepassing:
   
      ![][20]
2. Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.
   
    Hiermee geeft Hallo Package Manager-Console in Visual Studio.
3. In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Open het bestand Program.cs hello en voeg de volgende Hallo `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
5. In uw `Program` klasse, Hallo volgende methode toe te voegen. Bijwerken van Hallo tijdelijke aanduiding voor tekst met uw *DefaultFullSharedAccessSignature* verbindingsreeks en hubnaam verbindingsnaam van Hallo [klassieke Azure-Portal].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Toevoegen van de volgende regels in Hallo uw **Main** methode:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Druk op Hallo F5 sleutel toorun Hallo app. U ontvangt een melding in Hallo-app.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Optioneel) Meldingen verzenden met een mobiele service
1. Volg [Aan de slag met Mobile Services].
2. Meld u aan toohello [klassieke Azure-Portal], en selecteer uw mobiele service.
3. Selecteer Hallo **Scheduler** tabblad Hallo bovenaan.
   
      ![][22]
4. Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.
   
      ![][23]
5. Wanneer het Hallo-taak is gemaakt, klikt u op Hallo taaknaam. Klik vervolgens op Hallo **Script** tabblad op Hallo bovenste balk.
6. Hallo volgende script in de plannerfunctie invoegen. Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen. Klik op **Opslaan**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Klik op **eenmaal uitvoeren** op de balk onderaan Hallo. U ontvangt een pop-upmelding.

## <a name="next-steps"></a>Volgende stappen
In dit eenvoudige voorbeeld hebt u uitgezonden meldingen tooall uw Android-apparaten. In order tootarget specifieke gebruikers, raadpleegt u de zelfstudie toohello [Notification Hubs gebruiken toopush meldingen toousers]. Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws]. Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs] en in Hallo [Notification Hubs hoe toofor Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[klassieke Azure-Portal]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs hoe toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Notification Hubs gebruiken toopush meldingen toousers]: /manage/services/notification-hubs/notify-users-aspnet
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging-clientonderdeel]: http://components.xamarin.com/view/GCMClient/
[Azure Messaging-onderdeel]: http://components.xamarin.com/view/azure-messaging
