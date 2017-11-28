## <a name="create-the-webapi-project"></a><span data-ttu-id="13cfb-101">Het WebAPI-project maken</span><span class="sxs-lookup"><span data-stu-id="13cfb-101">Create the WebAPI Project</span></span>
<span data-ttu-id="13cfb-102">In de volgende secties wordt een nieuwe ASP.NET WebAPI-back-end gemaakt. Dit heeft drie hoofddoelen:</span><span class="sxs-lookup"><span data-stu-id="13cfb-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="13cfb-103">**Clients verifiëren**: later wordt een berichtenhandler toegevoegd voor het verifiëren van aanvragen van clients en het koppelen van de gebruiker aan de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="13cfb-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="13cfb-104">**Registraties van clientmeldingen**: later voegt u een controller toe voor het afhandelen van nieuwe registraties voor een clientapparaat voor het ontvangen van meldingen.</span><span class="sxs-lookup"><span data-stu-id="13cfb-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="13cfb-105">De naam van de geverifieerde gebruiker wordt automatisch aan de registratie toegevoegd als een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="13cfb-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="13cfb-106">**Meldingen verzenden naar clients**: later voegt u ook een controller toe om gebruikers een manier te bieden voor het activeren van een beveiligde push naar apparaten en clients die zijn gekoppeld aan de tag.</span><span class="sxs-lookup"><span data-stu-id="13cfb-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="13cfb-107">In de volgende stappen ziet u hoe u de nieuwe ASP.NET WebAPI-back-end maakt:</span><span class="sxs-lookup"><span data-stu-id="13cfb-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="13cfb-108">Als u Visual Studio 2015 of eerder gebruikt, moet u voordat u deze zelfstudie begint controleren of u de meest recente versie van NuGet Package Manager hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="13cfb-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="13cfb-109">Start Visual Studio om dit te controleren.</span><span class="sxs-lookup"><span data-stu-id="13cfb-109">To check, start Visual Studio.</span></span> <span data-ttu-id="13cfb-110">Klik vanuit het menu **Tools** op **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="13cfb-111">Zoek naar **NuGet Package Manager** voor uw versie van Visual Studio en controleer of u de meest recente versie hebt.</span><span class="sxs-lookup"><span data-stu-id="13cfb-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="13cfb-112">Als dit niet het geval is, verwijder dan NuGet Package Manager en installeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="13cfb-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="13cfb-113">Controleer of u de Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) voor website-implementatie hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="13cfb-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="13cfb-114">Start Visual Studio of Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="13cfb-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="13cfb-115">Klik op **Server Explorer** en meld u aan bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="13cfb-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="13cfb-116">Voor Visual Studio moet u aangemeld zijn om de website-resources voor uw account te maken.</span><span class="sxs-lookup"><span data-stu-id="13cfb-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="13cfb-117">Klik in Visual Studio op **Bestand**, klik vervolgens op **Nieuw** en daarna op **Project**, vouw **Sjablonen**, **Visual C#** uit en klik op **Web** en **ASP.NET-webtoepassing**, typ de naam **AppBackend** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="13cfb-118">Klik in het dialoogvenster **Nieuw ASP.NET-project** op **Web-API** en daarna op **OK**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="13cfb-119">Kies in het dialoogvenster **Microsoft Azure-web-app configureren** een abonnement en een **App Service-abonnement** dat u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="13cfb-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="13cfb-120">U kunt ook **Nieuw App Service-plan opstellen** kiezen en er een via het dialoogvenster maken.</span><span class="sxs-lookup"><span data-stu-id="13cfb-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="13cfb-121">U hebt geen database nodig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="13cfb-122">Nadat u uw App Service-plan hebt geselecteerd, klikt u op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="13cfb-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="13cfb-123">Clients verifiëren bij de WebAPI-back-end</span><span class="sxs-lookup"><span data-stu-id="13cfb-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="13cfb-124">In deze sectie maakt u een nieuwe berichtenhandlerklasse met de naam **AuthenticationTestHandler** voor de nieuwe back-end.</span><span class="sxs-lookup"><span data-stu-id="13cfb-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="13cfb-125">Deze klasse wordt afgeleid van [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) en toegevoegd als een berichtenhandler zodat deze alle aanvragen die de back-end ontvangt, kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="13cfb-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="13cfb-126">Klik in Solution Explorer met de rechtermuisknop op het project **AppBackend**, klik op **Toevoegen** en klik vervolgens op **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="13cfb-127">Geef de nieuwe klasse de naam **AuthenticationTestHandler.cs**, en klik op **Toevoegen** om de klasse te genereren.</span><span class="sxs-lookup"><span data-stu-id="13cfb-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="13cfb-128">Deze klasse wordt gebruikt voor verificatie van gebruikers met behulp van *Basisverificatie* om het eenvoudig te houden.</span><span class="sxs-lookup"><span data-stu-id="13cfb-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="13cfb-129">Uw app kan een willekeurig verificatieschema gebruiken.</span><span class="sxs-lookup"><span data-stu-id="13cfb-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="13cfb-130">Voeg in AuthenticationTestHandler.cs de volgende `using`-instructies toe:</span><span class="sxs-lookup"><span data-stu-id="13cfb-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="13cfb-131">Vervang in AuthenticationTestHandler.cs de `AuthenticationTestHandler`-klassedefinitie door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="13cfb-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="13cfb-132">Deze handler verifieert de aanvraag wanneer de volgende drie voorwaarden alle waar zijn:</span><span class="sxs-lookup"><span data-stu-id="13cfb-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="13cfb-133">De aanvraag bevatte een *Autorisatie*header.</span><span class="sxs-lookup"><span data-stu-id="13cfb-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="13cfb-134">De aanvraag maakt gebruik van *basis*verificatie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="13cfb-135">De gebruikersnaamtekenreeks en de wachtwoordtekenreeks zijn dezelfde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="13cfb-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="13cfb-136">Anders wordt de aanvraag geweigerd.</span><span class="sxs-lookup"><span data-stu-id="13cfb-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="13cfb-137">Dit is geen bestaande benadering op verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="13cfb-138">Dit is slechts een zeer eenvoudig voorbeeld voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="13cfb-139">Als het aanvraagbericht is geverifieerd en geautoriseerd door de `AuthenticationTestHandler`, wordt de basisverificatiegebruiker toegevoegd aan de huidige aanvraag in de [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="13cfb-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="13cfb-140">Gebruikersgegevens in de HttpContext worden later gebruikt door een andere controller (RegisterController) om een [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toe te voegen aan de aanvraag voor meldingen van registraties.</span><span class="sxs-lookup"><span data-stu-id="13cfb-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="13cfb-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="13cfb-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach the new principal object to the current HttpContext object
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
       <span data-ttu-id="13cfb-142">}</span><span class="sxs-lookup"><span data-stu-id="13cfb-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="13cfb-143">**Opmerking over beveiliging**: de `AuthenticationTestHandler`-klasse biedt geen echte verificatie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="13cfb-144">Het wordt alleen gebruikt om basisverificatie na te bootsen en is niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="13cfb-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="13cfb-145">U moet een veilig verificatiemechanisme implementeren in uw productietoepassingen en -services.</span><span class="sxs-lookup"><span data-stu-id="13cfb-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="13cfb-146">Voeg de volgende code toe aan het einde van de `Register`-methode in de klasse **App_Start/WebApiConfig.cs** om de berichtenhandler te registreren:</span><span class="sxs-lookup"><span data-stu-id="13cfb-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="13cfb-147">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="13cfb-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="13cfb-148">Registreren voor meldingen met behulp van de WebAPI-back-end</span><span class="sxs-lookup"><span data-stu-id="13cfb-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="13cfb-149">In deze sectie voegen we een nieuwe controller toe aan de WebAPI-back-end om aanvragen voor het registreren van een gebruiker en apparaat voor meldingen af te handelen met behulp van de clientbibliotheek voor notification hubs.</span><span class="sxs-lookup"><span data-stu-id="13cfb-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="13cfb-150">De controller voegt een gebruikerstag toe voor de gebruiker die door de `AuthenticationTestHandler` is geverifieerd en gekoppeld aan de HttpContext.</span><span class="sxs-lookup"><span data-stu-id="13cfb-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="13cfb-151">De tag heeft de indeling van de tekenreeks, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="13cfb-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="13cfb-152">Klik in Solution Explorer met de rechtermuisknop op het project **AppBackend** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="13cfb-153">Klik aan de linkerkant op **Online** en zoek naar **Microsoft.Azure.NotificationHubs** in het vak **Zoeken**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="13cfb-154">Klik in de lijst met resultaten op **Microsoft Azure Notification Hubs**, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="13cfb-155">Voltooi de installatie en sluit vervolgens het venster Nuget Package Manager.</span><span class="sxs-lookup"><span data-stu-id="13cfb-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="13cfb-156">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="13cfb-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="13cfb-157">We gaan nu een nieuw klassebestand maken waarmee de verbinding met de notification hub wordt gebruikt voor het verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="13cfb-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="13cfb-158">Klik in Solution Explorer met de rechtermuisknop op de map **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="13cfb-159">Noem de nieuwe klasse **Notifications.cs** en klik vervolgens op **Toevoegen** om de klasse te genereren.</span><span class="sxs-lookup"><span data-stu-id="13cfb-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="13cfb-160">Voeg in Notifications.cs de volgende `using`-instructie toe aan het begin van het bestand:</span><span class="sxs-lookup"><span data-stu-id="13cfb-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="13cfb-161">Vervang de `Notifications`-klassedefinitie maken met het volgende en zorg ervoor dat u de twee tijdelijke aanduidingen vervangt door de verbindingsreeks (met volledige toegang) voor uw notification hub en de naam van de hub (beschikbaar in de [klassieke Azure-portal](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="13cfb-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="13cfb-162">Vervolgens maken we een nieuwe controller met de naam **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="13cfb-163">Klik in Solution Explorer met de rechtermuisknop op de map **Controllers** en klik achtereenvolgens op **Toevoegen** en **Controller**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="13cfb-164">Klik op het item **Web API 2-controller - leeg** item en klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="13cfb-165">Noem de nieuwe klasse **RegisterController** en klik vervolgens opnieuw op **Toevoegen** om de controller te genereren.</span><span class="sxs-lookup"><span data-stu-id="13cfb-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="13cfb-166">Voeg in RegisterController.cs de volgende `using`-instructies toe:</span><span class="sxs-lookup"><span data-stu-id="13cfb-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="13cfb-167">Voeg de volgende code in de `RegisterController`-klassedefinitie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="13cfb-168">In deze code voegen we een gebruikerstag toe voor de gebruiker die is gekoppeld aan de HttpContext.</span><span class="sxs-lookup"><span data-stu-id="13cfb-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="13cfb-169">De gebruiker is geverifieerd en gekoppeld aan de HttpContext door het berichtenfilter dat we hebben toegevoegd, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="13cfb-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="13cfb-170">U kunt ook optionele controles toevoegen om te controleren of de gebruiker rechten heeft voor het registreren voor de aangevraagde tags.</span><span class="sxs-lookup"><span data-stu-id="13cfb-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at the specified id
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
   
            // add check if user is allowed to add these tags
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
10. <span data-ttu-id="13cfb-171">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="13cfb-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="13cfb-172">Meldingen verzenden vanuit de WebAPI-back-end</span><span class="sxs-lookup"><span data-stu-id="13cfb-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="13cfb-173">In deze sectie voegt u een nieuwe controller toe die een manier biedt voor clientapparaten om een melding te verzenden op basis van de gebruikersnaamtag met behulp van de Azure Notification Hubs Service Management-bibliotheek in de ASP.NET WebAPI-back-end.</span><span class="sxs-lookup"><span data-stu-id="13cfb-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="13cfb-174">Maak een andere nieuwe controller met de naam **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="13cfb-175">Maak deze op dezelfde manier als waarop u **RegisterController** in de vorige sectie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="13cfb-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="13cfb-176">Voeg in NotificationsController.cs de volgende `using`-instructies toe:</span><span class="sxs-lookup"><span data-stu-id="13cfb-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="13cfb-177">Voeg de volgende methode toe aan de klasse **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="13cfb-178">Met deze code wordt een meldingstype verzonden op basis van de `pns`-parameter (Platform Notification Service, PNS).</span><span class="sxs-lookup"><span data-stu-id="13cfb-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="13cfb-179">De waarde van `to_tag` wordt gebruikt om de tag *gebruikersnaam* in te stellen in het bericht.</span><span class="sxs-lookup"><span data-stu-id="13cfb-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="13cfb-180">Deze tag moet overeenkomen met een gebruikersnaamtag van een actieve notification hub-registratie.</span><span class="sxs-lookup"><span data-stu-id="13cfb-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="13cfb-181">Het meldingsbericht wordt opgehaald uit de hoofdtekst van de POST-aanvraag en geformatteerd voor de doel-PNS.</span><span class="sxs-lookup"><span data-stu-id="13cfb-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="13cfb-182">Afhankelijk van de PNS (Platform Notification Service) die uw ondersteunde apparaten gebruiken om meldingen te ontvangen, worden andere meldingen met verschillende indelingen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="13cfb-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="13cfb-183">Bijvoorbeeld op Windows-apparaten kunt u een [pop-upmelding met WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) gebruiken die niet rechtstreeks wordt ondersteund door een andere PNS.</span><span class="sxs-lookup"><span data-stu-id="13cfb-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="13cfb-184">Uw back-end moet de melding dus in een ondersteunde melding indelen voor de PNS van apparaten die u wilt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="13cfb-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="13cfb-185">Gebruik vervolgens de juiste API voor verzending in de [NotificationHubClient-klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="13cfb-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="13cfb-186">Druk op **F5** om de toepassing uit te voeren en om de juistheid van uw werk tot nu toe te controleren.</span><span class="sxs-lookup"><span data-stu-id="13cfb-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="13cfb-187">De app moet een webbrowser starten en de ASP.NET-startpagina weergeven.</span><span class="sxs-lookup"><span data-stu-id="13cfb-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="13cfb-188">De nieuwe WebAPI-back-end publiceren</span><span class="sxs-lookup"><span data-stu-id="13cfb-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="13cfb-189">We gaan nu deze app implementeren op een Azure-website zodat deze toegankelijk is vanaf alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="13cfb-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="13cfb-190">Klik met de rechtermuisknop op het project **AppBackend** en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="13cfb-191">Selecteer **Microsoft Azure App Service** als publicatiedoel en klik vervolgens op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="13cfb-192">Hiermee opent u het dialoogvenster App Service maken, waarmee u alle Azure-resources kunt maken die nodig zijn voor het uitvoeren van uw ASP.NET-web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="13cfb-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="13cfb-193">Selecteer uw Azure-account in het dialoogvenster **App Service maken**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="13cfb-194">Klik op **Type wijzigen** en selecteer **Web-app**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="13cfb-195">Houd de gegeven **Web-appnaam** en selecteer het **Abonnement**, de **Resourcegroep** en het **App Service-plan**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="13cfb-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-196">Click **Create**.</span></span>

4. <span data-ttu-id="13cfb-197">Noteer de **Site-URL**-eigenschap in de sectie **Samenvatting**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="13cfb-198">Naar deze URL wordt verderop in deze zelfstudie verwezen als uw *back-endeindpunt*.</span><span class="sxs-lookup"><span data-stu-id="13cfb-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="13cfb-199">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="13cfb-199">Click **Publish**.</span></span>

5. <span data-ttu-id="13cfb-200">Zodra de wizard is voltooid, wordt de ASP.NET-web-app naar Azure gepubliceerd. Daarna wordt de app gestart in de standaardbrowser.</span><span class="sxs-lookup"><span data-stu-id="13cfb-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="13cfb-201">Uw toepassing is zichtbaar in Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="13cfb-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="13cfb-202">De URL maakt gebruik van de web-appnaam die u eerder hebt opgegeven, met de notatie http://<app_naam>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="13cfb-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
