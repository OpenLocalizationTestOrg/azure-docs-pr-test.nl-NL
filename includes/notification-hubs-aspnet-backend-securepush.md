## <a name="webapi-project"></a><span data-ttu-id="1764c-101">WebAPI-Project</span><span class="sxs-lookup"><span data-stu-id="1764c-101">WebAPI Project</span></span>
1. <span data-ttu-id="1764c-102">Open in Visual Studio Hallo **AppBackend** project dat u hebt gemaakt in Hallo **gebruikers waarschuwen** zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1764c-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="1764c-103">In Notifications.cs, vervangen Hallo hele **meldingen** klasse Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="1764c-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="1764c-104">Worden ervoor tooreplace Hallo tijdelijke aanduidingen door uw verbindingsreeks (met volledige toegang) voor uw notification hub en het Hallo-hubnaam op.</span><span class="sxs-lookup"><span data-stu-id="1764c-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="1764c-105">U kunt deze waarden ophalen Hallo [klassieke Azure-Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1764c-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="1764c-106">Deze module vertegenwoordigt nu Hallo verschillende beveiligde berichten die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="1764c-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="1764c-107">Op een volledige implementatie worden Hallo meldingen opgeslagen in een database. voor het gemak opslaan in dit geval wordt deze in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="1764c-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="1764c-108">Vervang in NotificationsController.cs, Hallo-code binnen Hallo **NotificationsController** definitie klasse Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="1764c-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="1764c-109">Dit onderdeel een manier voor Hallo apparaat tooretrieve Hallo melding veilig geïmplementeerd, en biedt een manier (voor Hallo doel van deze zelfstudie) tootrigger ook een beveiligde push tooyour-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1764c-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="1764c-110">Houd er rekening mee dat bij het verzenden van Hallo melding toohello notification hub we alleen een onbewerkte kennisgeving verzenden met de Hallo-ID van Hallo melding (en geen daadwerkelijke bericht):</span><span class="sxs-lookup"><span data-stu-id="1764c-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="1764c-111">Houd er rekening mee dat Hallo `Post` methode verzendt nu geen toast-melding.</span><span class="sxs-lookup"><span data-stu-id="1764c-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="1764c-112">Deze stuurt een onbewerkte melding dat alleen Hallo-bericht-ID en geen gevoelige inhoud bevat.</span><span class="sxs-lookup"><span data-stu-id="1764c-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="1764c-113">Zorg ervoor dat toocomment Hallo verzendbewerking voor Hallo-platforms die u geen referenties zijn geconfigureerd op uw notification hub hebt als ze in fouten resulteren.</span><span class="sxs-lookup"><span data-stu-id="1764c-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="1764c-114">Nu we deze app tooan Azure-Website in volgorde toomake opnieuw implementeren deze toegankelijk is vanaf alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="1764c-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="1764c-115">Met de rechtermuisknop op Hallo **AppBackend** project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="1764c-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="1764c-116">Selecteer de Azure-Website als uw doel publiceren.</span><span class="sxs-lookup"><span data-stu-id="1764c-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="1764c-117">Meld u aan met uw Azure-account en selecteer een bestaande of nieuwe Website en noteer Hallo **doel-URL** eigenschap in Hallo **verbinding** tabblad. Toothis URL als wordt verwezen uw *back-end-eindpunt* verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1764c-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="1764c-118">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="1764c-118">Click **Publish**.</span></span>

