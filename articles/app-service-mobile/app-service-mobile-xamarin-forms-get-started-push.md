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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="b15df-103">Push notifications tooyour Xamarin.Forms-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="b15df-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="b15df-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b15df-104">Overview</span></span>
<span data-ttu-id="b15df-105">In deze zelfstudie maakt u push notifications tooall Hallo projecten die het gevolg zijn van Hallo toevoegen [Xamarin.Forms snel starten](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b15df-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="b15df-106">Dit betekent dat een push-melding tooall platformoverschrijdende clients verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="b15df-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="b15df-107">Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="b15df-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="b15df-108">Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b15df-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b15df-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b15df-109">Prerequisites</span></span>
<span data-ttu-id="b15df-110">Voor iOS, moet u een [Apple Developer Program-lidmaatschap](https://developer.apple.com/programs/ios/) en een fysiek iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b15df-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="b15df-111">Hallo [iOS-simulator biedt geen ondersteuning voor pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="b15df-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="b15df-112"><a name="configure-hub"></a>Een notification hub configureren</span><span class="sxs-lookup"><span data-stu-id="b15df-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="b15df-113">Hallo server project toosend-pushmeldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="b15df-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="b15df-114">Configureren en uitvoeren van Hallo Android-project (optioneel)</span><span class="sxs-lookup"><span data-stu-id="b15df-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="b15df-115">Deze sectie tooenable pushmeldingen voor Hallo Xamarin.Forms Droid-project voor Android worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="b15df-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="b15df-116">Firebase Cloud Messaging (FCM) inschakelen</span><span class="sxs-lookup"><span data-stu-id="b15df-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="b15df-117">Hallo Mobile Apps back-end toosend push aanvragen configureren met behulp van FCM</span><span class="sxs-lookup"><span data-stu-id="b15df-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="b15df-118">Push notifications toohello Android-project toevoegen</span><span class="sxs-lookup"><span data-stu-id="b15df-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="b15df-119">Hallo back-end geconfigureerd met het FCM, kunt u onderdelen en codes toohello client tooregister met FCM toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b15df-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="b15df-120">U kunt ook registreren voor pushmeldingen met Azure Notification Hubs via Hallo Mobile Apps terug beëindigen en meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b15df-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="b15df-121">In Hallo **Droid** project, klik met de rechtermuisknop op Hallo **onderdelen** map en klik op **meer onderdelen ophalen...** . Zoek vervolgens naar Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project.</span><span class="sxs-lookup"><span data-stu-id="b15df-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="b15df-122">Dit onderdeel biedt ondersteuning voor pushmeldingen voor een Xamarin.android-project.</span><span class="sxs-lookup"><span data-stu-id="b15df-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="b15df-123">Hallo MainActivity.cs projectbestand openen en Hallo Hallo boven aan het bestand Hallo-instructie toe:</span><span class="sxs-lookup"><span data-stu-id="b15df-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="b15df-124">Hallo na code toohello toevoegen **OnCreate** te aanroep van servermethode na Hallo**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="b15df-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

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
4. <span data-ttu-id="b15df-125">Voeg een nieuwe **CreateAndShowDialog** Help-methode, als volgt:</span><span class="sxs-lookup"><span data-stu-id="b15df-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="b15df-126">Hallo na code toohello toevoegen **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="b15df-126">Add hello following code toohello **MainActivity** class:</span></span>

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

    <span data-ttu-id="b15df-127">Dit wordt de huidige Hallo **MainActivity** exemplaar, zodat kan worden uitgevoerd op Hallo belangrijkste UI-thread.</span><span class="sxs-lookup"><span data-stu-id="b15df-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="b15df-128">Hallo initialiseren `instance` variabele aan begin Hallo Hallo **OnCreate** methode als volgt.</span><span class="sxs-lookup"><span data-stu-id="b15df-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="b15df-129">Voeg een nieuwe klasse bestand toohello **Droid** project met de naam `GcmService.cs`, en zorg ervoor dat Hallo volgende **met** instructies Hallo boven aan het Hallo-bestand aanwezig zijn:</span><span class="sxs-lookup"><span data-stu-id="b15df-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="b15df-130">Toevoegen van de volgende machtigingsaanvragen Hallo boven aan het Hallo-bestand, na het Hallo Hallo **met** instructies en vóór Hallo **naamruimte** declaratie.</span><span class="sxs-lookup"><span data-stu-id="b15df-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="b15df-131">Voeg Hallo klasse definitie toohello naamruimte te volgen.</span><span class="sxs-lookup"><span data-stu-id="b15df-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="b15df-132">Vervang **< PROJECT_NUMBER >** met het projectnummer van uw u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="b15df-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="b15df-133">Vervang Hallo leeg **GcmService** klasse met de volgende code, die gebruikmaakt van nieuwe broadcast ontvanger Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="b15df-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="b15df-134">Hallo na code toohello toevoegen **GcmService** klasse.</span><span class="sxs-lookup"><span data-stu-id="b15df-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="b15df-135">Overschrijft dit Hallo **OnRegistered** gebeurtenis-handler en implementeert een **registreren** methode.</span><span class="sxs-lookup"><span data-stu-id="b15df-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="b15df-136">Deze code wordt Hallo `messageParam` parameter Hallo sjabloon registratie.</span><span class="sxs-lookup"><span data-stu-id="b15df-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="b15df-137">Toevoegen na de code die wordt geïmplementeerd Hallo **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="b15df-137">Add hello following code that implements **OnMessage**:</span></span>

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

    <span data-ttu-id="b15df-138">Dit binnenkomende berichten worden verwerkt en verzendt deze toohello notification manager toobe weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b15df-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="b15df-139">**GcmServiceBase** moet u ook tooimplement hello **OnUnRegistered** en **bij fout** handler-methoden, die u kunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="b15df-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="b15df-140">Nu u gereed test pushmeldingen in Hallo app uitgevoerd op een Android-apparaat of emulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="b15df-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="b15df-141">Pushmeldingen testen in uw Android-app</span><span class="sxs-lookup"><span data-stu-id="b15df-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="b15df-142">Hallo eerste twee stappen zijn vereist, alleen wanneer u op een emulator test.</span><span class="sxs-lookup"><span data-stu-id="b15df-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="b15df-143">Zorg ervoor dat u tooor foutopsporing op een virtueel apparaat met Google APIs ingesteld als doel hello implementeert, zoals hieronder wordt weergegeven in Hallo Android Virtual Device manager.</span><span class="sxs-lookup"><span data-stu-id="b15df-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="b15df-144">Een apparaat toohello Android van Google-account toevoegen door te klikken op **Apps** > **instellingen** > **account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b15df-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="b15df-145">Volg daarna Hallo prompts tooadd een bestaand apparaat van Google-account toohello of toocreate een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="b15df-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="b15df-146">In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **Droid** project en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="b15df-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="b15df-147">Klik op **uitvoeren** toobuild Hallo project en Hallo-app op uw Android-apparaat of emulator te starten.</span><span class="sxs-lookup"><span data-stu-id="b15df-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="b15df-148">Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="b15df-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="b15df-149">Controleer of dat er een melding wordt ontvangen wanneer een item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b15df-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="b15df-150">Configureren en uitvoeren van Hallo iOS-project (optioneel)</span><span class="sxs-lookup"><span data-stu-id="b15df-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="b15df-151">Deze sectie is voor het uitvoeren van Hallo Xamarin iOS-project voor iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b15df-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="b15df-152">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="b15df-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="b15df-153">Hallo notification hub configureren voor APNS</span><span class="sxs-lookup"><span data-stu-id="b15df-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="b15df-154">Vervolgens configureert u instelling Hallo iOS-project in Xamarin Studio of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b15df-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="b15df-155">Push notifications tooyour iOS-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="b15df-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="b15df-156">In Hallo **iOS** project, opent u AppDelegate.cs en toevoegen van de volgende instructie toohello boven aan het codebestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b15df-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="b15df-157">In Hallo **AppDelegate** klasse, Voeg een onderdrukking voor Hallo **RegisteredForRemoteNotifications** gebeurtenis tooregister voor meldingen:</span><span class="sxs-lookup"><span data-stu-id="b15df-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="b15df-158">In **AppDelegate**, ook toevoegen na onderdrukken voor Hallo Hallo **DidReceiveRemoteNotification** gebeurtenis-handler:</span><span class="sxs-lookup"><span data-stu-id="b15df-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="b15df-159">Deze methode verwerkt de inkomende meldingen terwijl Hallo-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b15df-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="b15df-160">In Hallo **AppDelegate** klasse, het toevoegen van Hallo na code toohello **FinishedLaunching** methode:</span><span class="sxs-lookup"><span data-stu-id="b15df-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="b15df-161">Dit biedt ondersteuning voor externe meldingen en push-registratie van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b15df-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="b15df-162">Uw app is nu bijgewerkte toosupport pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b15df-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="b15df-163">Pushmeldingen testen in uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="b15df-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="b15df-164">Met de rechtermuisknop op Hallo iOS-project en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="b15df-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="b15df-165">Druk op Hallo **uitvoeren** knop of **F5** in Visual Studio toobuild Hallo project en Hallo-app te starten in een iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b15df-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="b15df-166">Klik vervolgens op **OK** tooaccept pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b15df-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b15df-167">U moet expliciet pushmeldingen accepteren van uw app.</span><span class="sxs-lookup"><span data-stu-id="b15df-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="b15df-168">Deze aanvraag is alleen sprake Hallo eerste keer is dat Hallo app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b15df-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="b15df-169">Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="b15df-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="b15df-170">Controleer of een melding wordt ontvangen, en klik vervolgens op **OK** toodismiss Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="b15df-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="b15df-171">Configureren en uitvoeren van Windows-projecten (optioneel)</span><span class="sxs-lookup"><span data-stu-id="b15df-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="b15df-172">Deze sectie is voor het uitvoeren van Hallo Xamarin.Forms WinApp en WinPhone81 projecten voor Windows-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b15df-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="b15df-173">Deze stappen bieden ook ondersteuning voor Universal Windows Platform (UWP)-projecten.</span><span class="sxs-lookup"><span data-stu-id="b15df-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="b15df-174">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="b15df-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="b15df-175">Uw Windows-app voor pushmeldingen registreren met Windows Notification Service (WNS)</span><span class="sxs-lookup"><span data-stu-id="b15df-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="b15df-176">Hallo notification hub configureren voor WNS</span><span class="sxs-lookup"><span data-stu-id="b15df-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="b15df-177">Push notifications tooyour Windows-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="b15df-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="b15df-178">Open in Visual Studio **App.xaml.cs** in een Windows-project en voeg Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="b15df-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="b15df-179">Vervang `<your_TodoItemManager_portable_class_namespace>` met de naamruimte van uw draagbare project met Hallo Hallo `TodoItemManager` klasse.</span><span class="sxs-lookup"><span data-stu-id="b15df-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="b15df-180">Voeg in App.xaml.cs Hallo volgende **InitNotificationsAsync** methode:</span><span class="sxs-lookup"><span data-stu-id="b15df-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="b15df-181">Deze methode Hallo push notification channel opgehaald en wordt een sjabloon tooreceive Sjabloonmeldingen van uw notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="b15df-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="b15df-182">Een sjabloon melding die ondersteuning biedt voor *messageParam* toothis client wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="b15df-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="b15df-183">Werk in App.xaml.cs hello **OnLaunched** gebeurtenis-handler methodedefinitie door toe te voegen Hallo `async` aanpassingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="b15df-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="b15df-184">Voeg vervolgens Hallo volgende regel code achter Hallo Hallo-methode toe:</span><span class="sxs-lookup"><span data-stu-id="b15df-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="b15df-185">Dit zorgt ervoor dat de registratie voor pushberichten hello wordt gemaakt of vernieuwd telkens wanneer het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b15df-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="b15df-186">Het is belangrijk toodo deze tooguarantee die WNS push kanaal Hallo altijd actief is.</span><span class="sxs-lookup"><span data-stu-id="b15df-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="b15df-187">Open in Solution Explorer voor Visual Studio Hallo **Package.appxmanifest** bestand en stel **Toast geschikt** te**Ja** onder **meldingen**.</span><span class="sxs-lookup"><span data-stu-id="b15df-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="b15df-188">Hallo-app bouwen en controleer of er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="b15df-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="b15df-189">Uw client-app moet nu registreren voor Hallo de Sjabloonmeldingen van Hallo dat Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="b15df-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="b15df-190">Herhaal deze sectie voor elke Windows-project in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="b15df-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="b15df-191">Pushmeldingen testen in uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="b15df-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="b15df-192">Met de rechtermuisknop op een Windows-project in Visual Studio, en klik op **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="b15df-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="b15df-193">Druk op Hallo **uitvoeren** knop toobuild Hallo-project en het Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="b15df-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="b15df-194">Typ een naam voor een nieuwe stukje in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram tooadd deze.</span><span class="sxs-lookup"><span data-stu-id="b15df-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="b15df-195">Controleer of dat er een melding wordt ontvangen wanneer Hallo item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b15df-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b15df-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b15df-196">Next steps</span></span>
<span data-ttu-id="b15df-197">U kunt meer informatie over pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="b15df-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="b15df-198">Push notification problemen vaststellen</span><span class="sxs-lookup"><span data-stu-id="b15df-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="b15df-199">Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="b15df-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="b15df-200">Dit onderwerp leest u hoe tooanalyze en uitzoeken Hallo hoofdmap push notification fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="b15df-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="b15df-201">U kunt ook doorwerken op tooone Hallo volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="b15df-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="b15df-202">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="b15df-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="b15df-203">Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="b15df-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="b15df-204">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="b15df-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="b15df-205">Meer informatie over hoe tooadd offlineondersteuning voor uw app met behulp van een mobiele Apps van back-end.</span><span class="sxs-lookup"><span data-stu-id="b15df-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="b15df-206">Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="b15df-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
