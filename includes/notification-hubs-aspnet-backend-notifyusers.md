## <a name="create-hello-webapi-project"></a>Hallo WebAPI-Project maken
Een nieuwe ASP.NET WebAPI-back-end Hallo die in secties worden gemaakt en er drie hoofddoelen:

1. **Clients verifiëren**: de berichtenhandler van een worden toegevoegd hoger tooauthenticate-clientaanvragen en koppelen Hallo-gebruiker met Hallo-aanvraag.
2. **Client melding registraties**: Later kunt u een nieuwe domeincontroller toohandle-registraties voor een client apparaat tooreceive meldingen wilt toevoegen. Hallo geverifieerde gebruikersnaam wordt automatisch toegevoegd toohello registratie als een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Verzenden van meldingen tooClients**: Later kunt u ook toevoegen een controller tooprovide een manier om een gebruiker tootrigger een toodevices beveiligde push clients die zijn gekoppeld aan het Hallo-tag. 

Hallo stappen te volgen tonen hoe toocreate Hallo nieuwe ASP.NET WebAPI-back-end: 

> [!IMPORTANT]
> Als u Visual Studio 2015 of eerder, voordat u deze zelfstudie begint, zorg ervoor dat u de nieuwste versie Hallo Hallo NuGet Package Manager hebt geïnstalleerd. toocheck, start Visual Studio. Van Hallo **extra** menu, klikt u op **uitbreidingen en Updates**. Zoeken naar **NuGet Package Manager** voor uw versie van Visual Studio en zorg ervoor dat u beschikt over de nieuwste versie Hallo. Verwijder, als dat niet, en installeer daarna Hallo NuGet Package Manager.
> 
> ![][B4]
> 
> [!NOTE]
> Zorg ervoor dat u hebt geïnstalleerd Hallo Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) voor de implementatie van de website.
> 
> 

1. Start Visual Studio of Visual Studio Express. Klik op **Server Explorer** en meld u aan tooyour Azure-account. Visual Studio moet u aangemeld toocreate Hallo website resources voor uw account.
2. Klik in Visual Studio **bestand**, klikt u vervolgens op **nieuw**, klikt u vervolgens **Project**, vouw **sjablonen**, **Visual C#**, klikt u vervolgens op **Web** en **ASP.NET-webtoepassing**, Hallo typenaam **AppBackend**, en klik vervolgens op **OK**. 
   
    ![][B1]
3. In Hallo **nieuw ASP.NET-Project** dialoogvenster, klikt u op **Web API**, klikt u vervolgens op **OK**.
   
    ![][B2]
4. In Hallo **Microsoft Azure Web-App configureren** dialoogvenster, kies een abonnement en een **App Service-abonnement** u al hebt gemaakt. U kunt ook **maken van een nieuwe app service-abonnement** en een Hallo dialoogvenster maken. U hebt geen database nodig voor deze zelfstudie. Nadat u uw app service-abonnement hebt geselecteerd, klikt u op **OK** toocreate Hallo project.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Verificatie van Clients toohello WebAPI Backend
In deze sectie maakt u een nieuwe berichtklasse handler met de naam **AuthenticationTestHandler** voor Hallo nieuwe back-end. Deze klasse wordt afgeleid van [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) en toegevoegd als een berichtenhandler zodat deze kan verwerken alle aanvragen die door Hallo back-end. 

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **AppBackend** project, klikt u op **toevoegen**, klikt u vervolgens op **klasse**. Naam nieuwe klasse Hallo **AuthenticationTestHandler.cs**, en klik op **toevoegen** toogenerate Hallo-klasse. Deze klasse worden gebruikers in gebruikte tooauthenticate *basisverificatie* voor eenvoud. Uw app kan een willekeurig verificatieschema gebruiken.
2. Voeg de volgende Hallo in AuthenticationTestHandler.cs, `using` instructies:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. In AuthenticationTestHandler.cs, vervangen Hallo `AuthenticationTestHandler` definitie klasse Hello code te volgen. 
   
    Deze handler machtigen Hallo aanvraag wanneer Hallo na drie voorwaarden alle waar zijn:
   
   * Hallo-aanvraag opgenomen een *autorisatie* header. 
   * Hallo aanvraag gebruikt *basic* verificatie. 
   * Hallo tekenreeks voor de gebruiker en Hallo wachtwoordtekenreeks zijn Hallo dezelfde tekenreeks.
     
     Anders wordt Hallo-aanvraag geweigerd. Dit is geen bestaande benadering op verificatie en autorisatie. Dit is slechts een zeer eenvoudig voorbeeld voor deze zelfstudie.
     
     Als de aanvraag het Hallo-bericht is geverifieerd en gemachtigd door Hallo `AuthenticationTestHandler`, en vervolgens Hallo Basisverificatie gebruiker de huidige aanvraag gekoppelde toohello op Hallo worden [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Gebruikersgegevens in Hallo HttpContext wordt gebruikt door een andere domeincontroller (RegisterController) hoger tooadd een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello melding registratieverzoek.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Opmerking over beveiliging**: Hallo `AuthenticationTestHandler` klasse biedt geen true verificatie. Het gebruikte alleen toomimic basisverificatie is en is niet beveiligd. U moet een veilig verificatiemechanisme implementeren in uw productietoepassingen en -services.                
     > 
     > 
4. Toevoegen van de volgende code achter Hallo HALLO hallo `Register` methode in Hallo **App_Start/WebApiConfig.cs** klasse tooregister Hallo-berichtenhandler:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Sla uw wijzigingen op.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Registreren voor meldingen met Hallo WebAPI Backend
In deze sectie zullen we toevoegen dat een nieuwe domeincontroller toohello WebAPI-back-end toohandle aanvragen tooregister een gebruiker en apparaat voor meldingen via Hallo-clientbibliotheek voor notification hubs. Hallo-controller wordt een gebruiker label toevoegen voor Hallo-gebruiker die is geverifieerd en gekoppeld toohello HttpContext door Hallo `AuthenticationTestHandler`. Hallo-label heeft tekenreeksindeling hello, `"username:<actual username>"`.

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **AppBackend** project en klik vervolgens op **NuGet-pakketten beheren**.
2. Aan de linkerkant Hallo en klikt u op **Online**, en zoek naar **Microsoft.Azure.NotificationHubs** in Hallo **Search** vak.
3. Klik in de lijst met resultaten Hallo op **Microsoft Azure Notification Hubs**, en klik vervolgens op **installeren**. Hallo-installatie voltooien en vervolgens Hallo NuGet package manager venster sluiten.
   
    Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
4. We gaan nu een nieuwe klassebestand die verbinding met de notification hub gebruikt toosend meldingen Hallo vertegenwoordigt maken. Hallo Solution Explorer, met de rechtermuisknop op Hallo **modellen** map, klikt u op **toevoegen**, klikt u vervolgens op **klasse**. Naam nieuwe klasse Hallo **Notifications.cs**, klikt u vervolgens op **toevoegen** toogenerate Hallo-klasse. 
   
    ![][B6]
5. Voeg de volgende Hallo in Notifications.cs, `using` instructie Hallo boven aan het Hallo-bestand:
   
        using Microsoft.Azure.NotificationHubs;
6. Vervang Hallo `Notifications` definitie door Hallo volgende klasse en zorg ervoor dat tooreplace Hallo twee tijdelijke aanduidingen door Hallo verbindingsreeks (met volledige toegang) voor uw notification hub en hubnaam Hallo (beschikbaar op [klassieke Azure-Portal ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Vervolgens maken we een nieuwe controller met de naam **RegisterController**. Klik in Solution Explorer met de rechtermuisknop op Hallo **domeincontrollers** map, klikt u vervolgens op **toevoegen**, klikt u vervolgens op **Controller**. Klik op Hallo **Web API 2-Controller--leeg** item en klik vervolgens op **toevoegen**. Naam nieuwe klasse Hallo **RegisterController**, en klik vervolgens op **toevoegen** opnieuw toogenerate Hallo controller.
   
    ![][B7]
   
    ![][B8]
8. Voeg de volgende Hallo in RegisterController.cs, `using` instructies:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Toevoegen van de volgende code in Hallo Hallo `RegisterController` klasse definitie. Houd er rekening mee dat in de volgende code, we een gebruikerscode voor Hallo gebruiker die dit is gekoppeld toohello HttpContext toevoegen. Hallo-gebruiker is geverifieerd en gekoppeld toohello HttpContext door Hallo-berichtenfilter wordt toegevoegd, `AuthenticationTestHandler`. U kunt ook toevoegen optionele controles tooverify die Hallo gebruiker beschikt over rechten tooregister voor Hallo codes aangevraagd.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Sla uw wijzigingen op.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Verzenden van meldingen vanuit Hallo WebAPI Backend
In deze sectie voegt u een nieuwe domeincontroller waarmee een manier om de client apparaten toosend een melding op basis van Hallo gebruikersnaam tag met Azure Notification Hubs Service Management Library in Hallo ASP.NET WebAPI-back-end.

1. Maak een andere nieuwe controller met de naam **NotificationsController**. Deze Hallo maken dezelfde manier gemaakt van Hallo **RegisterController** in de vorige sectie Hallo.
2. Voeg de volgende Hallo in NotificationsController.cs, `using` instructies:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Hallo na methode toohello toevoegen **NotificationsController** klasse.
   
    Deze code verzenden van een meldingstype op basis van Hallo Platform Notification Service (PNS) `pns` parameter. waarde van Hallo `to_tag` gebruikte tooset Hallo is *gebruikersnaam* label op het Hallo-bericht. Deze tag moet overeenkomen met een gebruikersnaamtag van een actieve notification hub-registratie. Hallo-melding is opgehaald uit het Hallo-hoofdtekst van Hallo POST-aanvraag en geformatteerd voor Hallo doel PNS. 
   
    Afhankelijk van Hallo Platform Notification Service (PNS) die uw ondersteunde apparaten tooreceive meldingen gebruiken, worden andere meldingen met behulp van verschillende indelingen ondersteund. Bijvoorbeeld op Windows-apparaten kunt u een [pop-upmelding met WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) gebruiken die niet rechtstreeks wordt ondersteund door een andere PNS. U plant toosupport zodat uw back-end nodig tooformat Hallo-bericht in een ondersteunde melding voor Hallo PNS van apparaten. Gebruik vervolgens Hallo juiste verzenden API op Hallo [NotificationHubClient-klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Druk op **F5** toorun Hallo toepassings- en tooensure Hallo juistheid van uw werk tot nu toe. Hallo-app moet een webbrowser worden gestart en Hallo ASP.NET-startpagina weergeven. 

## <a name="publish-hello-new-webapi-backend"></a>Publiceren Hallo nieuwe WebAPI Backend
1. Nu we deze app tooan Azure-Website in volgorde toomake implementeren deze toegankelijk is vanaf alle apparaten. Met de rechtermuisknop op Hallo **AppBackend** project en selecteer **publiceren**.
2. Selecteer **Microsoft Azure App Service** als publicatiedoel en klik vervolgens op **Publiceren**. Hiermee opent u het dialoogvenster App Service maken hello, waardoor u alle Hallo nodig Azure-resources toorun Hallo ASP.NET-web-app maken in Azure.

    ![][B15]
3. In Hallo **Create App Service** dialoogvenster, selecteer uw Azure-account. Klik op **Type wijzigen** en selecteer **Web-app**. Hallo houden **Web-Appnaam** gegeven en selecteer Hallo **abonnement**, **resourcegroep**, en **App Service-Plan**.  Klik op **Create**.

4. Maak een notitie van Hallo **Site-URL** eigenschap in Hallo **samenvatting** sectie. Toothis URL als wordt verwezen uw *back-end-eindpunt* verderop in deze zelfstudie. Klik op **Publish**.

5. Zodra Hallo wizard is voltooid, het Hallo ASP.NET web app tooAzure publiceert en vervolgens wordt gestart in de standaardbrowser Hallo app Hallo.  Uw toepassing is zichtbaar in Azure App Services.

Hallo URL Hallo web app-naam die u eerder hebt opgegeven met Hallo indeling http://<app_name>.azurewebsites.net gebruikt.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
