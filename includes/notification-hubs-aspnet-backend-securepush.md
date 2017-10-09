## <a name="webapi-project"></a>WebAPI-Project
1. Open in Visual Studio Hallo **AppBackend** project dat u hebt gemaakt in Hallo **gebruikers waarschuwen** zelfstudie.
2. In Notifications.cs, vervangen Hallo hele **meldingen** klasse Hello code te volgen. Worden ervoor tooreplace Hallo tijdelijke aanduidingen door uw verbindingsreeks (met volledige toegang) voor uw notification hub en het Hallo-hubnaam op. U kunt deze waarden ophalen Hallo [klassieke Azure-Portal](http://manage.windowsazure.com). Deze module vertegenwoordigt nu Hallo verschillende beveiligde berichten die worden verzonden. Op een volledige implementatie worden Hallo meldingen opgeslagen in een database. voor het gemak opslaan in dit geval wordt deze in het geheugen.
   
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

1. Vervang in NotificationsController.cs, Hallo-code binnen Hallo **NotificationsController** definitie klasse Hello code te volgen. Dit onderdeel een manier voor Hallo apparaat tooretrieve Hallo melding veilig geïmplementeerd, en biedt een manier (voor Hallo doel van deze zelfstudie) tootrigger ook een beveiligde push tooyour-apparaten. Houd er rekening mee dat bij het verzenden van Hallo melding toohello notification hub we alleen een onbewerkte kennisgeving verzenden met de Hallo-ID van Hallo melding (en geen daadwerkelijke bericht):
   
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


Houd er rekening mee dat Hallo `Post` methode verzendt nu geen toast-melding. Deze stuurt een onbewerkte melding dat alleen Hallo-bericht-ID en geen gevoelige inhoud bevat. Zorg ervoor dat toocomment Hallo verzendbewerking voor Hallo-platforms die u geen referenties zijn geconfigureerd op uw notification hub hebt als ze in fouten resulteren.

1. Nu we deze app tooan Azure-Website in volgorde toomake opnieuw implementeren deze toegankelijk is vanaf alle apparaten. Met de rechtermuisknop op Hallo **AppBackend** project en selecteer **publiceren**.
2. Selecteer de Azure-Website als uw doel publiceren. Meld u aan met uw Azure-account en selecteer een bestaande of nieuwe Website en noteer Hallo **doel-URL** eigenschap in Hallo **verbinding** tabblad. Toothis URL als wordt verwezen uw *back-end-eindpunt* verderop in deze zelfstudie. Klik op **Publish**.

