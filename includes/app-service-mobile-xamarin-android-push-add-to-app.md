1. <span data-ttu-id="70dcb-101">Maak een nieuwe klasse in het project met de naam `ToDoBroadcastReceiver`.</span><span class="sxs-lookup"><span data-stu-id="70dcb-101">Create a new class in the project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="70dcb-102">Voeg de volgende using-instructies naar **ToDoBroadcastReceiver** klasse:</span><span class="sxs-lookup"><span data-stu-id="70dcb-102">Add the following using statements to **ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="70dcb-103">Voeg de volgende machtigingsaanvragen tussen de **met** instructies en de **naamruimte** declaratie:</span><span class="sxs-lookup"><span data-stu-id="70dcb-103">Add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="70dcb-104">Vervang de bestaande **ToDoBroadcastReceiver** klasse definitie door het volgende:</span><span class="sxs-lookup"><span data-stu-id="70dcb-104">Replace the existing **ToDoBroadcastReceiver** class definition with the following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set the Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="70dcb-105">U moet in de bovenstaande code vervangen  *`<PROJECT_NUMBER>`*  met het projectnummer dat wordt toegewezen door Google wanneer u uw app in de Google-portal voor ontwikkelaars ingericht.</span><span class="sxs-lookup"><span data-stu-id="70dcb-105">In the above code, you must replace *`<PROJECT_NUMBER>`* with the project number assigned by Google when you provisioned your app in the Google developer portal.</span></span> 
5. <span data-ttu-id="70dcb-106">Voeg de volgende code waarmee wordt gedefinieerd in het projectbestand ToDoBroadcastReceiver.cs de **PushHandlerService** klasse:</span><span class="sxs-lookup"><span data-stu-id="70dcb-106">In the ToDoBroadcastReceiver.cs project file, add the following code that defines the **PushHandlerService** class:</span></span>
   
        // The ServiceAttribute must be applied to the class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="70dcb-107">Merk op dat deze klasse is afgeleid van **GcmServiceBase** en dat de **Service** kenmerk moet worden toegepast op deze klasse.</span><span class="sxs-lookup"><span data-stu-id="70dcb-107">Note that this class derives from **GcmServiceBase** and that the **Service** attribute must be applied to this class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="70dcb-108">De **GcmServiceBase** klasse implementeert de **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** en  **OnError()** methoden.</span><span class="sxs-lookup"><span data-stu-id="70dcb-108">The **GcmServiceBase** class implements the **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="70dcb-109">U moet deze methoden overschrijven de **PushHandlerService** klasse.</span><span class="sxs-lookup"><span data-stu-id="70dcb-109">You must override these methods in the **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="70dcb-110">Voeg de volgende code naar de **PushHandlerService** klasse die de **OnRegistered** gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="70dcb-110">Add the following code to the **PushHandlerService** class that overrides the **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("The device has been registered with GCM.", "Success!");
   
            // Get the MobileServiceClient from the current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define the template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run the registration on the same thread as the activity, 
                // to avoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register the template with Notification Hubs.
                    async () => await push.RegisterAsync(registrationId, templates));
   
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Push Installation Id", push.InstallationId.ToString()));
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Error with Azure push registration: {0}", ex.Message));
            }
        }
   
    <span data-ttu-id="70dcb-111">Deze methode maakt gebruik van de geretourneerde GCM-registratie-ID registreren bij Azure voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="70dcb-111">This method uses the returned GCM registration ID to register with Azure for push notifications.</span></span> <span data-ttu-id="70dcb-112">Labels kunnen alleen worden toegevoegd aan de registratie nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70dcb-112">Tags can only be added to the registration after it is created.</span></span> <span data-ttu-id="70dcb-113">Zie voor meer informatie [hoe: labels toevoegen aan de installatie van een apparaat om in te schakelen push aan labels](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span><span class="sxs-lookup"><span data-stu-id="70dcb-113">For more information, see [How to: Add tags to a device installation to enable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="70dcb-114">Overschrijf de **OnMessage** methode in **PushHandlerService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="70dcb-114">Override the **OnMessage** method in **PushHandlerService** with the following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract the push notification message from the intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager to send the notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent to show the notification in the UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create the notification using the builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display the notification in the Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="70dcb-115">Overschrijf de **OnUnRegistered()** en **OnError()** methoden met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="70dcb-115">Override the **OnUnRegistered()** and **OnError()** methods with the following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in the notification: {0}.", errorId));
       }

