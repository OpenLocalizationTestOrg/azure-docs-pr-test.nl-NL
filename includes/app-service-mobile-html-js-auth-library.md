### <span data-ttu-id="a068b-101"><a name="server-auth"></a>Procedure: Verifiëren bij een provider (Server Flow)</span><span class="sxs-lookup"><span data-stu-id="a068b-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="a068b-102">toohave Mobile Apps beheren Hallo verificatieproces in uw app, moet u uw app registreren met de id-provider.</span><span class="sxs-lookup"><span data-stu-id="a068b-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="a068b-103">In Azure App Service moet u tooconfigure Hallo toepassings-ID en geheim geleverd door uw provider.</span><span class="sxs-lookup"><span data-stu-id="a068b-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="a068b-104">Zie voor meer informatie, Hallo zelfstudie [toevoegen verificatie tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="a068b-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="a068b-105">Wanneer u de id-provider hebt geregistreerd, aanroepen Hallo `.login()` methode met de naam van uw provider Hallo.</span><span class="sxs-lookup"><span data-stu-id="a068b-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="a068b-106">Bijvoorbeeld: toologin met Facebook Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a068b-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="a068b-107">geldige waarden voor de provider Hallo Hallo zijn 'aad', 'facebook', 'google', 'microsoftaccount' en 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="a068b-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="a068b-108">Verificatie via Google werkt momenteel niet via Server Flow.</span><span class="sxs-lookup"><span data-stu-id="a068b-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="a068b-109">tooauthenticate met Google, moet u een [client-flow-methode](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="a068b-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="a068b-110">In dit geval beheert Azure App Service Hallo OAuth 2.0-verificatiestroom.</span><span class="sxs-lookup"><span data-stu-id="a068b-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="a068b-111">Het Hallo-aanmeldingspagina van de geselecteerde provider hello wordt weergegeven en genereert een App Service-verificatietoken na geslaagde aanmelding met Hallo id-provider.</span><span class="sxs-lookup"><span data-stu-id="a068b-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="a068b-112">Hallo aanmelding functie, retourneert als u klaar een JSON-object dat toegang biedt tot zowel de Hallo gebruikers-ID en de App Service-verificatietoken in Hallo userId authenticationToken velden en respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="a068b-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="a068b-113">Dit token kan worden opgeslagen in de cache en opnieuw worden gebruikt totdat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="a068b-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="a068b-114"><a name="client-auth"></a>Procedure: Verifiëren bij een provider (Client Flow)</span><span class="sxs-lookup"><span data-stu-id="a068b-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="a068b-115">Uw app kan ook afzonderlijk Neem contact op met de identiteitsprovider Hallo en geef vervolgens Hallo geretourneerd token tooyour App Service voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a068b-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="a068b-116">Deze stroom client kunt u een één-aanmeldingservaring aanpast voor gebruikers of tooretrieve extra gebruikersgegevens van de identiteitsprovider Hallo tooprovide.</span><span class="sxs-lookup"><span data-stu-id="a068b-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="a068b-117">Eenvoudig voorbeeld van sociale verificatie</span><span class="sxs-lookup"><span data-stu-id="a068b-117">Social Authentication basic example</span></span>

<span data-ttu-id="a068b-118">In dit voorbeeld wordt de client-SDK van Facebook gebruikt voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="a068b-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="a068b-119">In dit voorbeeld wordt ervan uitgegaan dat Hallo-token opgegeven door de respectieve provider Hallo SDK wordt opgeslagen in token Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="a068b-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="a068b-120">Voorbeeld van Microsoft-account</span><span class="sxs-lookup"><span data-stu-id="a068b-120">Microsoft Account example</span></span>

<span data-ttu-id="a068b-121">Hallo wordt na Hallo Live SDK, die ondersteuning biedt voor één aanmelding voor Windows Store-apps met behulp van Microsoft-Account:</span><span class="sxs-lookup"><span data-stu-id="a068b-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="a068b-122">In dit voorbeeld krijgt een token van Live verbinding maken, die is opgegeven tooyour App Service door het Hallo-aanmelding functie aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a068b-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="a068b-123"><a name="auth-getinfo"></a>Hoe: ophalen van informatie over Hallo geverifieerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="a068b-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="a068b-124">Hallo verificatie-informatie kan worden opgehaald uit Hallo `/.auth/me` -eindpunt met een HTTP-aanroepen met eventuele AJAX-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="a068b-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="a068b-125">Zorg ervoor dat u Hallo ingesteld `X-ZUMO-AUTH` header tooyour verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="a068b-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="a068b-126">Hallo-verificatietoken opgeslagen in `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="a068b-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="a068b-127">Bijvoorbeeld: toouse Hallo ophalen API:</span><span class="sxs-lookup"><span data-stu-id="a068b-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="a068b-128">Ophalen is beschikbaar als [npm-pakket](https://www.npmjs.com/package/whatwg-fetch), maar kan ook met een browser worden gedownload van [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="a068b-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="a068b-129">U kunt ook jQuery of een andere AJAX-API toofetch Hallo-informatie.</span><span class="sxs-lookup"><span data-stu-id="a068b-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="a068b-130">Gegevens worden ontvangen als JSON-object.</span><span class="sxs-lookup"><span data-stu-id="a068b-130">Data is received as a JSON object.</span></span>
