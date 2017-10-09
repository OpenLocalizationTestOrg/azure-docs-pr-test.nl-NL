## <a name="create-hello-webapi-project"></a><span data-ttu-id="be33a-101">Hallo WebAPI-Project maken</span><span class="sxs-lookup"><span data-stu-id="be33a-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="be33a-102">Een nieuwe ASP.NET WebAPI-back-end Hallo die in secties worden gemaakt en er drie hoofddoelen:</span><span class="sxs-lookup"><span data-stu-id="be33a-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="be33a-103">**Clients verifiëren**: de berichtenhandler van een worden toegevoegd hoger tooauthenticate-clientaanvragen en koppelen Hallo-gebruiker met Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="be33a-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="be33a-104">**Client melding registraties**: Later kunt u een nieuwe domeincontroller toohandle-registraties voor een client apparaat tooreceive meldingen wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="be33a-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="be33a-105">Hallo geverifieerde gebruikersnaam wordt automatisch toegevoegd toohello registratie als een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="be33a-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="be33a-106">**Verzenden van meldingen tooClients**: Later kunt u ook toevoegen een controller tooprovide een manier om een gebruiker tootrigger een toodevices beveiligde push clients die zijn gekoppeld aan het Hallo-tag.</span><span class="sxs-lookup"><span data-stu-id="be33a-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="be33a-107">Hallo stappen te volgen tonen hoe toocreate Hallo nieuwe ASP.NET WebAPI-back-end:</span><span class="sxs-lookup"><span data-stu-id="be33a-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="be33a-108">Als u Visual Studio 2015 of eerder, voordat u deze zelfstudie begint, zorg ervoor dat u de nieuwste versie Hallo Hallo NuGet Package Manager hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="be33a-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="be33a-109">toocheck, start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be33a-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="be33a-110">Van Hallo **extra** menu, klikt u op **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="be33a-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="be33a-111">Zoeken naar **NuGet Package Manager** voor uw versie van Visual Studio en zorg ervoor dat u beschikt over de nieuwste versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="be33a-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="be33a-112">Verwijder, als dat niet, en installeer daarna Hallo NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="be33a-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="be33a-113">Zorg ervoor dat u hebt geïnstalleerd Hallo Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) voor de implementatie van de website.</span><span class="sxs-lookup"><span data-stu-id="be33a-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="be33a-114">Start Visual Studio of Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="be33a-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="be33a-115">Klik op **Server Explorer** en meld u aan tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="be33a-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="be33a-116">Visual Studio moet u aangemeld toocreate Hallo website resources voor uw account.</span><span class="sxs-lookup"><span data-stu-id="be33a-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="be33a-117">Klik in Visual Studio **bestand**, klikt u vervolgens op **nieuw**, klikt u vervolgens **Project**, vouw **sjablonen**, **Visual C#**, klikt u vervolgens op **Web** en **ASP.NET-webtoepassing**, Hallo typenaam **AppBackend**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="be33a-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="be33a-118">In Hallo **nieuw ASP.NET-Project** dialoogvenster, klikt u op **Web API**, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="be33a-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="be33a-119">In Hallo **Microsoft Azure Web-App configureren** dialoogvenster, kies een abonnement en een **App Service-abonnement** u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be33a-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="be33a-120">U kunt ook **maken van een nieuwe app service-abonnement** en een Hallo dialoogvenster maken.</span><span class="sxs-lookup"><span data-stu-id="be33a-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="be33a-121">U hebt geen database nodig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="be33a-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="be33a-122">Nadat u uw app service-abonnement hebt geselecteerd, klikt u op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="be33a-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="be33a-123">Verificatie van Clients toohello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="be33a-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="be33a-124">In deze sectie maakt u een nieuwe berichtklasse handler met de naam **AuthenticationTestHandler** voor Hallo nieuwe back-end.</span><span class="sxs-lookup"><span data-stu-id="be33a-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="be33a-125">Deze klasse wordt afgeleid van [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) en toegevoegd als een berichtenhandler zodat deze kan verwerken alle aanvragen die door Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="be33a-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="be33a-126">Klik in Solution Explorer met de rechtermuisknop op Hallo **AppBackend** project, klikt u op **toevoegen**, klikt u vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="be33a-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="be33a-127">Naam nieuwe klasse Hallo **AuthenticationTestHandler.cs**, en klik op **toevoegen** toogenerate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="be33a-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="be33a-128">Deze klasse worden gebruikers in gebruikte tooauthenticate *basisverificatie* voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="be33a-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="be33a-129">Uw app kan een willekeurig verificatieschema gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be33a-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="be33a-130">Voeg de volgende Hallo in AuthenticationTestHandler.cs, `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="be33a-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="be33a-131">In AuthenticationTestHandler.cs, vervangen Hallo `AuthenticationTestHandler` definitie klasse Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="be33a-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="be33a-132">Deze handler machtigen Hallo aanvraag wanneer Hallo na drie voorwaarden alle waar zijn:</span><span class="sxs-lookup"><span data-stu-id="be33a-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="be33a-133">Hallo-aanvraag opgenomen een *autorisatie* header.</span><span class="sxs-lookup"><span data-stu-id="be33a-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="be33a-134">Hallo aanvraag gebruikt *basic* verificatie.</span><span class="sxs-lookup"><span data-stu-id="be33a-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="be33a-135">Hallo tekenreeks voor de gebruiker en Hallo wachtwoordtekenreeks zijn Hallo dezelfde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="be33a-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="be33a-136">Anders wordt Hallo-aanvraag geweigerd.</span><span class="sxs-lookup"><span data-stu-id="be33a-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="be33a-137">Dit is geen bestaande benadering op verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="be33a-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="be33a-138">Dit is slechts een zeer eenvoudig voorbeeld voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="be33a-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="be33a-139">Als de aanvraag het Hallo-bericht is geverifieerd en gemachtigd door Hallo `AuthenticationTestHandler`, en vervolgens Hallo Basisverificatie gebruiker de huidige aanvraag gekoppelde toohello op Hallo worden [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="be33a-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="be33a-140">Gebruikersgegevens in Hallo HttpContext wordt gebruikt door een andere domeincontroller (RegisterController) hoger tooadd een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello melding registratieverzoek.</span><span class="sxs-lookup"><span data-stu-id="be33a-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="be33a-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="be33a-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="be33a-142">}</span><span class="sxs-lookup"><span data-stu-id="be33a-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="be33a-143">**Opmerking over beveiliging**: Hallo `AuthenticationTestHandler` klasse biedt geen true verificatie.</span><span class="sxs-lookup"><span data-stu-id="be33a-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="be33a-144">Het gebruikte alleen toomimic basisverificatie is en is niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="be33a-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="be33a-145">U moet een veilig verificatiemechanisme implementeren in uw productietoepassingen en -services.</span><span class="sxs-lookup"><span data-stu-id="be33a-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="be33a-146">Toevoegen van de volgende code achter Hallo HALLO hallo `Register` methode in Hallo **App_Start/WebApiConfig.cs** klasse tooregister Hallo-berichtenhandler:</span><span class="sxs-lookup"><span data-stu-id="be33a-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="be33a-147">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="be33a-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="be33a-148">Registreren voor meldingen met Hallo WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="be33a-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="be33a-149">In deze sectie zullen we toevoegen dat een nieuwe domeincontroller toohello WebAPI-back-end toohandle aanvragen tooregister een gebruiker en apparaat voor meldingen via Hallo-clientbibliotheek voor notification hubs.</span><span class="sxs-lookup"><span data-stu-id="be33a-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="be33a-150">Hallo-controller wordt een gebruiker label toevoegen voor Hallo-gebruiker die is geverifieerd en gekoppeld toohello HttpContext door Hallo `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="be33a-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="be33a-151">Hallo-label heeft tekenreeksindeling hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="be33a-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="be33a-152">Klik in Solution Explorer met de rechtermuisknop op Hallo **AppBackend** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="be33a-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="be33a-153">Aan de linkerkant Hallo en klikt u op **Online**, en zoek naar **Microsoft.Azure.NotificationHubs** in Hallo **Search** vak.</span><span class="sxs-lookup"><span data-stu-id="be33a-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="be33a-154">Klik in de lijst met resultaten Hallo op **Microsoft Azure Notification Hubs**, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="be33a-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="be33a-155">Hallo-installatie voltooien en vervolgens Hallo NuGet package manager venster sluiten.</span><span class="sxs-lookup"><span data-stu-id="be33a-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="be33a-156">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="be33a-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="be33a-157">We gaan nu een nieuwe klassebestand die verbinding met de notification hub gebruikt toosend meldingen Hallo vertegenwoordigt maken.</span><span class="sxs-lookup"><span data-stu-id="be33a-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="be33a-158">Hallo Solution Explorer, met de rechtermuisknop op Hallo **modellen** map, klikt u op **toevoegen**, klikt u vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="be33a-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="be33a-159">Naam nieuwe klasse Hallo **Notifications.cs**, klikt u vervolgens op **toevoegen** toogenerate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="be33a-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="be33a-160">Voeg de volgende Hallo in Notifications.cs, `using` instructie Hallo boven aan het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="be33a-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="be33a-161">Vervang Hallo `Notifications` definitie door Hallo volgende klasse en zorg ervoor dat tooreplace Hallo twee tijdelijke aanduidingen door Hallo verbindingsreeks (met volledige toegang) voor uw notification hub en hubnaam Hallo (beschikbaar op [klassieke Azure-Portal ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="be33a-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="be33a-162">Vervolgens maken we een nieuwe controller met de naam **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="be33a-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="be33a-163">Klik in Solution Explorer met de rechtermuisknop op Hallo **domeincontrollers** map, klikt u vervolgens op **toevoegen**, klikt u vervolgens op **Controller**.</span><span class="sxs-lookup"><span data-stu-id="be33a-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="be33a-164">Klik op Hallo **Web API 2-Controller--leeg** item en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="be33a-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="be33a-165">Naam nieuwe klasse Hallo **RegisterController**, en klik vervolgens op **toevoegen** opnieuw toogenerate Hallo controller.</span><span class="sxs-lookup"><span data-stu-id="be33a-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="be33a-166">Voeg de volgende Hallo in RegisterController.cs, `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="be33a-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="be33a-167">Toevoegen van de volgende code in Hallo Hallo `RegisterController` klasse definitie.</span><span class="sxs-lookup"><span data-stu-id="be33a-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="be33a-168">Houd er rekening mee dat in de volgende code, we een gebruikerscode voor Hallo gebruiker die dit is gekoppeld toohello HttpContext toevoegen.</span><span class="sxs-lookup"><span data-stu-id="be33a-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="be33a-169">Hallo-gebruiker is geverifieerd en gekoppeld toohello HttpContext door Hallo-berichtenfilter wordt toegevoegd, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="be33a-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="be33a-170">U kunt ook toevoegen optionele controles tooverify die Hallo gebruiker beschikt over rechten tooregister voor Hallo codes aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="be33a-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="be33a-171">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="be33a-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="be33a-172">Verzenden van meldingen vanuit Hallo WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="be33a-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="be33a-173">In deze sectie voegt u een nieuwe domeincontroller waarmee een manier om de client apparaten toosend een melding op basis van Hallo gebruikersnaam tag met Azure Notification Hubs Service Management Library in Hallo ASP.NET WebAPI-back-end.</span><span class="sxs-lookup"><span data-stu-id="be33a-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="be33a-174">Maak een andere nieuwe controller met de naam **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="be33a-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="be33a-175">Deze Hallo maken dezelfde manier gemaakt van Hallo **RegisterController** in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="be33a-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="be33a-176">Voeg de volgende Hallo in NotificationsController.cs, `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="be33a-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="be33a-177">Hallo na methode toohello toevoegen **NotificationsController** klasse.</span><span class="sxs-lookup"><span data-stu-id="be33a-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="be33a-178">Deze code verzenden van een meldingstype op basis van Hallo Platform Notification Service (PNS) `pns` parameter.</span><span class="sxs-lookup"><span data-stu-id="be33a-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="be33a-179">waarde van Hallo `to_tag` gebruikte tooset Hallo is *gebruikersnaam* label op het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="be33a-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="be33a-180">Deze tag moet overeenkomen met een gebruikersnaamtag van een actieve notification hub-registratie.</span><span class="sxs-lookup"><span data-stu-id="be33a-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="be33a-181">Hallo-melding is opgehaald uit het Hallo-hoofdtekst van Hallo POST-aanvraag en geformatteerd voor Hallo doel PNS.</span><span class="sxs-lookup"><span data-stu-id="be33a-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="be33a-182">Afhankelijk van Hallo Platform Notification Service (PNS) die uw ondersteunde apparaten tooreceive meldingen gebruiken, worden andere meldingen met behulp van verschillende indelingen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="be33a-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="be33a-183">Bijvoorbeeld op Windows-apparaten kunt u een [pop-upmelding met WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) gebruiken die niet rechtstreeks wordt ondersteund door een andere PNS.</span><span class="sxs-lookup"><span data-stu-id="be33a-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="be33a-184">U plant toosupport zodat uw back-end nodig tooformat Hallo-bericht in een ondersteunde melding voor Hallo PNS van apparaten.</span><span class="sxs-lookup"><span data-stu-id="be33a-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="be33a-185">Gebruik vervolgens Hallo juiste verzenden API op Hallo [NotificationHubClient-klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="be33a-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="be33a-186">Druk op **F5** toorun Hallo toepassings- en tooensure Hallo juistheid van uw werk tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="be33a-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="be33a-187">Hallo-app moet een webbrowser worden gestart en Hallo ASP.NET-startpagina weergeven.</span><span class="sxs-lookup"><span data-stu-id="be33a-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="be33a-188">Publiceren Hallo nieuwe WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="be33a-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="be33a-189">Nu we deze app tooan Azure-Website in volgorde toomake implementeren deze toegankelijk is vanaf alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="be33a-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="be33a-190">Met de rechtermuisknop op Hallo **AppBackend** project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="be33a-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="be33a-191">Selecteer **Microsoft Azure App Service** als publicatiedoel en klik vervolgens op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="be33a-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="be33a-192">Hiermee opent u het dialoogvenster App Service maken hello, waardoor u alle Hallo nodig Azure-resources toorun Hallo ASP.NET-web-app maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="be33a-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="be33a-193">In Hallo **Create App Service** dialoogvenster, selecteer uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="be33a-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="be33a-194">Klik op **Type wijzigen** en selecteer **Web-app**.</span><span class="sxs-lookup"><span data-stu-id="be33a-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="be33a-195">Hallo houden **Web-Appnaam** gegeven en selecteer Hallo **abonnement**, **resourcegroep**, en **App Service-Plan**.</span><span class="sxs-lookup"><span data-stu-id="be33a-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="be33a-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="be33a-196">Click **Create**.</span></span>

4. <span data-ttu-id="be33a-197">Maak een notitie van Hallo **Site-URL** eigenschap in Hallo **samenvatting** sectie.</span><span class="sxs-lookup"><span data-stu-id="be33a-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="be33a-198">Toothis URL als wordt verwezen uw *back-end-eindpunt* verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="be33a-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="be33a-199">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="be33a-199">Click **Publish**.</span></span>

5. <span data-ttu-id="be33a-200">Zodra Hallo wizard is voltooid, het Hallo ASP.NET web app tooAzure publiceert en vervolgens wordt gestart in de standaardbrowser Hallo app Hallo.</span><span class="sxs-lookup"><span data-stu-id="be33a-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="be33a-201">Uw toepassing is zichtbaar in Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="be33a-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="be33a-202">Hallo URL Hallo web app-naam die u eerder hebt opgegeven met Hallo indeling http://<app_name>.azurewebsites.net gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be33a-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
