---
title: Pushmeldingen toevoegen aan uw Xamarin.Forms-app | Microsoft Docs
description: Informatie over het gebruik van Azure-services voor meerdere platforms pushmeldingen verzendt naar uw apps voor Xamarin.Forms.
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="cbdc7-103">Pushmeldingen toevoegen aan uw Xamarin.Forms-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="cbdc7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cbdc7-104">Overview</span></span>
<span data-ttu-id="cbdc7-105">In deze zelfstudie hebt u pushmeldingen toevoegen aan de projecten die het gevolg zijn van de [Xamarin.Forms snel starten](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="cbdc7-106">Dit betekent dat een push-melding wordt verzonden naar alle clients van de platformoverschrijdende telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="cbdc7-107">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="cbdc7-108">Zie voor meer informatie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbdc7-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cbdc7-109">Prerequisites</span></span>
<span data-ttu-id="cbdc7-110">Voor iOS, moet u een [Apple Developer Program-lidmaatschap](https://developer.apple.com/programs/ios/) en een fysiek iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="cbdc7-111">De [iOS-simulator biedt geen ondersteuning voor pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="cbdc7-112"><a name="configure-hub"></a>Een notification hub configureren</span><span class="sxs-lookup"><span data-stu-id="cbdc7-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="cbdc7-113">Bijwerken van het serverproject om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="cbdc7-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="cbdc7-114">Configureren en uitvoeren van het Android-project (optioneel)</span><span class="sxs-lookup"><span data-stu-id="cbdc7-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="cbdc7-115">Deze sectie om in te schakelen pushmeldingen voor het Xamarin.Forms Droid-project voor Android worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="cbdc7-116">Firebase Cloud Messaging (FCM) inschakelen</span><span class="sxs-lookup"><span data-stu-id="cbdc7-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="cbdc7-117">De back-end voor mobiele Apps voor het verzenden van push-aanvragen via FCM configureren</span><span class="sxs-lookup"><span data-stu-id="cbdc7-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="cbdc7-118">Pushmeldingen toevoegen aan de Android-project</span><span class="sxs-lookup"><span data-stu-id="cbdc7-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="cbdc7-119">U kunt met de back-end geconfigureerd met het FCM onderdelen en codes toevoegen aan de client om te registreren bij FCM.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="cbdc7-120">U kunt ook registreren voor pushmeldingen met Azure Notification Hubs via de back-end van Mobile Apps en meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="cbdc7-121">In de **Droid** project, met de rechtermuisknop op de **onderdelen** map en klik op **meer onderdelen ophalen...** .</span><span class="sxs-lookup"><span data-stu-id="cbdc7-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="cbdc7-122">Zoek vervolgens naar de **Google Cloud Messaging-Client** onderdeel en voeg deze toe aan het project.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="cbdc7-123">Dit onderdeel biedt ondersteuning voor pushmeldingen voor een Xamarin.android-project.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="cbdc7-124">Open het projectbestand MainActivity.cs en voeg de volgende instructie toe aan de bovenkant van het bestand:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="cbdc7-125">Voeg de volgende code naar de **OnCreate** methode na het aanroepen van **LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="cbdc7-126">Voeg een nieuwe **CreateAndShowDialog** Help-methode, als volgt:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="cbdc7-127">Voeg de volgende code naar de **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="cbdc7-128">Hiermee wordt de huidige **MainActivity** exemplaar, zodat kan worden uitgevoerd op de belangrijkste UI-thread.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="cbdc7-129">Initialisatie van de `instance` variabele aan het begin van de **OnCreate** methode als volgt.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="cbdc7-130">Voeg een nieuw klassebestand naar de **Droid** project met de naam `GcmService.cs`, en zorg ervoor dat de volgende **met** instructies aan de bovenkant van het bestand aanwezig zijn:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="cbdc7-131">Voeg de volgende machtigingsaanvragen aan de bovenkant van het bestand toe na de **met** instructies en vóór de **naamruimte** declaratie.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="cbdc7-132">De volgende klassendefinitie toevoegen aan de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="cbdc7-133">Vervang **< PROJECT_NUMBER >** met het projectnummer van uw u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="cbdc7-134">Vervang de lege **GcmService** klasse met de volgende code, die de nieuwe broadcast ontvanger gebruikt:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="cbdc7-135">Voeg de volgende code naar de **GcmService** klasse.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="cbdc7-136">Overschrijft dit de **OnRegistered** gebeurtenis-handler en implementeert een **registreren** methode.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="cbdc7-137">Merk op dat deze code gebruikt de `messageParam` parameter in de registratie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="cbdc7-138">Voeg de volgende code waarmee **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="cbdc7-139">Dit binnenkomende berichten worden verwerkt en zendt deze naar de notification manager moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="cbdc7-140">**GcmServiceBase** vereist ook dat u voor het implementeren van de **OnUnRegistered** en **bij fout** handler-methoden, die u kunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="cbdc7-141">U bent nu klaar test pushmeldingen in de app uitgevoerd op een Android-apparaat of de emulator.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="cbdc7-142">Pushmeldingen testen in uw Android-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="cbdc7-143">De eerste twee stappen zijn vereist, alleen wanneer u op een emulator test.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="cbdc7-144">Zorg ervoor dat u implementeert voor of foutopsporing op een virtueel apparaat met Google APIs ingesteld als doel, zoals hieronder wordt weergegeven in de Android Virtual Device manager.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="cbdc7-145">Een Google-account toevoegen aan de Android-apparaat door te klikken op **Apps** > **instellingen** > **account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="cbdc7-146">Volg de aanwijzingen een bestaande Google-account toevoegen aan het apparaat, of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="cbdc7-147">In Visual Studio of Xamarin Studio, met de rechtermuisknop op de **Droid** project en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="cbdc7-148">Klik op **uitvoeren** bouw het project en de app op uw Android-apparaat of emulator te starten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="cbdc7-149">Typ een taak in de app en klik vervolgens op het plusteken (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="cbdc7-150">Controleer of dat er een melding wordt ontvangen wanneer een item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="cbdc7-151">Configureren en uitvoeren van het iOS-project (optioneel)</span><span class="sxs-lookup"><span data-stu-id="cbdc7-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="cbdc7-152">Deze sectie gaat over het uitvoeren van het Xamarin iOS-project voor iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="cbdc7-153">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="cbdc7-154">De notification hub configureren voor APNS</span><span class="sxs-lookup"><span data-stu-id="cbdc7-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="cbdc7-155">Vervolgens configureert u de instelling van de iOS-project in Xamarin Studio of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="cbdc7-156">Pushmeldingen toevoegen aan uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="cbdc7-157">In de **iOS** project, opent u AppDelegate.cs en de volgende instructie toe te voegen aan de bovenkant van het codebestand.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="cbdc7-158">In de **AppDelegate** klasse, Voeg een onderdrukking voor de **RegisteredForRemoteNotifications** gebeurtenis registreren voor meldingen:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="cbdc7-159">In **AppDelegate**, Voeg ook de volgende onderdrukking voor de **DidReceiveRemoteNotification** gebeurtenis-handler:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="cbdc7-160">Deze methode binnenkomende berichten worden verwerkt terwijl de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="cbdc7-161">In de **AppDelegate** klasse, het toevoegen van de volgende code naar de **FinishedLaunching** methode:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="cbdc7-162">Dit biedt ondersteuning voor externe meldingen en push-registratie van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="cbdc7-163">Uw app is nu bijgewerkt ter ondersteuning van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="cbdc7-164">Pushmeldingen testen in uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="cbdc7-165">Met de rechtermuisknop op het iOS-project en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="cbdc7-166">Druk op de **uitvoeren** knop of **F5** in Visual Studio om het project bouwen en starten van de app in een iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="cbdc7-167">Klik vervolgens op **OK** pushmeldingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbdc7-168">U moet expliciet pushmeldingen accepteren van uw app.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="cbdc7-169">Deze aanvraag treedt alleen op de eerste keer dat de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="cbdc7-170">Typ een taak in de app en klik vervolgens op het plusteken (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="cbdc7-171">Controleer of een melding wordt ontvangen, en klik vervolgens op **OK** kunnen worden verwijderd van de melding.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="cbdc7-172">Configureren en uitvoeren van Windows-projecten (optioneel)</span><span class="sxs-lookup"><span data-stu-id="cbdc7-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="cbdc7-173">Deze sectie is voor het uitvoeren van de Xamarin.Forms-WinApp en WinPhone81-projecten voor Windows-apparaten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="cbdc7-174">Deze stappen bieden ook ondersteuning voor Universal Windows Platform (UWP)-projecten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="cbdc7-175">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="cbdc7-176">Uw Windows-app voor pushmeldingen registreren met Windows Notification Service (WNS)</span><span class="sxs-lookup"><span data-stu-id="cbdc7-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="cbdc7-177">De notification hub configureren voor WNS</span><span class="sxs-lookup"><span data-stu-id="cbdc7-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="cbdc7-178">Pushmeldingen toevoegen aan uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="cbdc7-179">Open in Visual Studio **App.xaml.cs** in een Windows-project en voeg de volgende instructies toe.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="cbdc7-180">Vervang `<your_TodoItemManager_portable_class_namespace>` met de naamruimte van uw draagbare project met de `TodoItemManager` klasse.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="cbdc7-181">Voeg het volgende in App.xaml.cs **InitNotificationsAsync** methode:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="cbdc7-182">Deze methode opgehaald van het meldingskanaal push en een sjabloon voor het ontvangen van Sjabloonmeldingen van uw notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="cbdc7-183">Een sjabloon melding die ondersteuning biedt voor *messageParam* aan deze client wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="cbdc7-184">Werk in App.xaml.cs de **OnLaunched** gebeurtenis-handler methodedefinitie door toe te voegen de `async` aanpassingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="cbdc7-185">Voeg vervolgens de volgende coderegel toe aan het einde van de methode:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="cbdc7-186">Dit zorgt ervoor dat de registratie voor pushberichten wordt gemaakt of vernieuwd telkens wanneer de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="cbdc7-187">Het is belangrijk om ervoor te zorgen dat het kanaal WNS-push altijd actief is.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="cbdc7-188">Open in Solution Explorer voor Visual Studio de **Package.appxmanifest** bestand en stel **Toast geschikt** naar **Ja** onder **meldingen**.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="cbdc7-189">De app bouwen en controleer of er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="cbdc7-190">Uw client-app moet zich nu registreren voor de Sjabloonmeldingen van de back-end van Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="cbdc7-191">Herhaal deze sectie voor elke Windows-project in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="cbdc7-192">Pushmeldingen testen in uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="cbdc7-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="cbdc7-193">Met de rechtermuisknop op een Windows-project in Visual Studio, en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="cbdc7-194">Druk op de knop **Uitvoeren** om het project te bouwen en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="cbdc7-195">Typ een naam voor een nieuwe taken in de app en klik vervolgens op het plusteken (**+**) pictogram toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="cbdc7-196">Controleer of dat er een melding wordt ontvangen wanneer het item is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbdc7-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cbdc7-197">Next steps</span></span>
<span data-ttu-id="cbdc7-198">U kunt meer informatie over pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="cbdc7-199">Push notification problemen vaststellen</span><span class="sxs-lookup"><span data-stu-id="cbdc7-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="cbdc7-200">Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="cbdc7-201">Dit onderwerp leest u hoe te analyseren en te achterhalen van de hoofdoorzaken van fouten voor push-melding.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="cbdc7-202">U kunt ook door te gaan naar een van de volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="cbdc7-203">Verificatie toevoegen aan uw app </span><span class="sxs-lookup"><span data-stu-id="cbdc7-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="cbdc7-204">Ontdek hoe u gebruikers van uw app verifieert met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="cbdc7-205">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="cbdc7-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="cbdc7-206">Ontdek hoe u offlineondersteuning voor uw app toevoegt met behulp van een back-end voor Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="cbdc7-207">Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
