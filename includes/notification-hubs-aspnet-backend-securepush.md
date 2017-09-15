## <a name="webapi-project"></a><span data-ttu-id="40be3-101">WebAPI-Project</span><span class="sxs-lookup"><span data-stu-id="40be3-101">WebAPI Project</span></span>
1. <span data-ttu-id="40be3-102">Open in Visual Studio de **AppBackend** project dat u hebt gemaakt in de **gebruikers waarschuwen** zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="40be3-102">In Visual Studio, open the **AppBackend** project that you created in the **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="40be3-103">Vervang in Notifications.cs, het gehele **meldingen** klasse met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="40be3-103">In Notifications.cs, replace the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="40be3-104">Zorg ervoor dat de tijdelijke aanduidingen vervangt door uw verbindingsreeks (met volledige toegang) voor uw notification hub en de naam van de hub.</span><span class="sxs-lookup"><span data-stu-id="40be3-104">Be sure to replace the placeholders with your connection string (with full access) for your notification hub, and the hub name.</span></span> <span data-ttu-id="40be3-105">U vindt deze waarden uit de [klassieke Azure-Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="40be3-105">You can obtain these values from the [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="40be3-106">Deze module vertegenwoordigt nu de verschillende beveiligde meldingen die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="40be3-106">This module now represents the different secure notifications that will be sent.</span></span> <span data-ttu-id="40be3-107">Op een volledige implementatie worden de meldingen opgeslagen in een database. voor het gemak opslaan in dit geval wordt deze in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="40be3-107">In a complete implementation, the notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="40be3-108">In NotificationsController.cs, vervang de code in de **NotificationsController** klasse-definitie maken met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="40be3-108">In NotificationsController.cs, replace the code inside the **NotificationsController** class definition with the following code.</span></span> <span data-ttu-id="40be3-109">Dit onderdeel een manier voor het apparaat voor het ophalen van de melding veilig geïmplementeerd, en biedt ook een manier (voor de doeleinden van deze zelfstudie) om te activeren van een beveiligde push op uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="40be3-109">This component implements a way for the device to retrieve the notification securely, and also provides a way (for the purposes of this tutorial) to trigger a secure push to your devices.</span></span> <span data-ttu-id="40be3-110">Houd er rekening mee dat wanneer u de melding verzendt met de notification hub, wordt alleen de een onbewerkte melding met de ID van de melding (en geen daadwerkelijke bericht) verzenden:</span><span class="sxs-lookup"><span data-stu-id="40be3-110">Note that when sending the notification to the notification hub, we only send a raw notification with the ID of the notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="40be3-111">Houd er rekening mee dat de `Post` methode verzendt nu geen toast-melding.</span><span class="sxs-lookup"><span data-stu-id="40be3-111">Note that the `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="40be3-112">Een onbewerkte melding met de ID van de melding en geen gevoelige inhoud wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="40be3-112">It sends a raw notification that contains only the notification ID, and not any sensitive content.</span></span> <span data-ttu-id="40be3-113">Controleer ook of de verzendbewerking voor de platforms die u geen referenties zijn geconfigureerd op uw notification hub hebt als ze in fouten resulteren opmerkingen te maken.</span><span class="sxs-lookup"><span data-stu-id="40be3-113">Also, make sure to comment the send operation for the platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="40be3-114">Er wordt nu opnieuw deze app wordt een Azure-Website zodat deze toegankelijk is vanaf alle apparaten implementeren.</span><span class="sxs-lookup"><span data-stu-id="40be3-114">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="40be3-115">Klik met de rechtermuisknop op het project **AppBackend** en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="40be3-115">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="40be3-116">Selecteer de Azure-Website als uw doel publiceren.</span><span class="sxs-lookup"><span data-stu-id="40be3-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="40be3-117">Meld u aan met uw Azure-account en selecteer een bestaande of nieuwe Website en noteer de **doel-URL** eigenschap in de **verbinding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="40be3-117">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="40be3-118">Naar deze URL wordt verderop in deze zelfstudie verwezen als uw *back-endeindpunt*.</span><span class="sxs-lookup"><span data-stu-id="40be3-118">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="40be3-119">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="40be3-119">Click **Publish**.</span></span>

