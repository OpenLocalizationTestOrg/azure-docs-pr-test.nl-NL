### <span data-ttu-id="b4ab4-101"><a name="server-auth"></a>Procedure: Verifiëren bij een provider (Server Flow)</span><span class="sxs-lookup"><span data-stu-id="b4ab4-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="b4ab4-102">Als u het verificatieproces in uw app door Mobile Apps wilt laten beheren, moet u uw app registreren bij uw id-provider.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="b4ab4-103">Daarna moet u in uw Azure App Service de door uw provider verstrekte toepassings-id en geheim configureren.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="b4ab4-104">Zie de zelfstudie [Verificatie toevoegen aan uw app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="b4ab4-105">Wanneer u de id-provider hebt geregistreerd, roept u de methode `.login()` aan met de naam van uw provider.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="b4ab4-106">Meld u bijvoorbeeld aan bij Facebook met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="b4ab4-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="b4ab4-107">De geldige waarden voor de provider zijn 'aad', 'facebook', 'google', 'microsoftaccount' en 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ab4-108">Verificatie via Google werkt momenteel niet via Server Flow.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="b4ab4-109">Voor verificatie via Google moet u een [client-flowmethode](#client-auth) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="b4ab4-110">In dit geval beheert Azure App Service de OAuth 2.0-verificatiestroom.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="b4ab4-111">Deze geeft de aanmeldingspagina van de geselecteerde provider weer en genereert een App Service-verificatietoken na geslaagde aanmelding bij de id-provider.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="b4ab4-112">De aanmeldingsfunctie retourneert na voltooiing een JSON-object dat zowel de gebruikers-id als het App Service-verificatietoken respectievelijk in de velden userId en authenticationToken weergeeft.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="b4ab4-113">Dit token kan worden opgeslagen in de cache en opnieuw worden gebruikt totdat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="b4ab4-114"><a name="client-auth"></a>Procedure: Verifiëren bij een provider (Client Flow)</span><span class="sxs-lookup"><span data-stu-id="b4ab4-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="b4ab4-115">Uw app kan ook afzonderlijk contact opnemen met de id-provider en het geretourneerde token vervolgens aan uw App Service verstrekken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="b4ab4-116">Met deze clientstroom kunt u een eenmalige aanmelding bieden voor gebruikers of aanvullende gebruikersgegevens ophalen van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="b4ab4-117">Eenvoudig voorbeeld van sociale verificatie</span><span class="sxs-lookup"><span data-stu-id="b4ab4-117">Social Authentication basic example</span></span>

<span data-ttu-id="b4ab4-118">In dit voorbeeld wordt de client-SDK van Facebook gebruikt voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="b4ab4-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="b4ab4-119">In dit voorbeeld wordt ervan uitgegaan dat het token dat is opgegeven door de betreffende SDK-provider, is opgeslagen in de tokenvariabele.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="b4ab4-120">Voorbeeld van Microsoft-account</span><span class="sxs-lookup"><span data-stu-id="b4ab4-120">Microsoft Account example</span></span>

<span data-ttu-id="b4ab4-121">In het volgende voorbeeld wordt de Live SDK gebruikt, die eenmalige aanmelding ondersteunt voor Windows Store-apps met behulp van een Microsoft-account:</span><span class="sxs-lookup"><span data-stu-id="b4ab4-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="b4ab4-122">In dit voorbeeld wordt een token opgehaald van Live Connect, dat wordt doorgegeven aan uw App Service door de aanmeldingsfunctie aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="b4ab4-123"><a name="auth-getinfo"></a>Procedure: Informatie verzamelen over de geverifieerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="b4ab4-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="b4ab4-124">De verificatiegegevens kunnen worden opgehaald uit het `/.auth/me`-eindpunt met een HTTP aanroep aan een willekeurige AJAX-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="b4ab4-125">Zorg ervoor dat u de `X-ZUMO-AUTH`-header in uw verificatietoken instelt.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="b4ab4-126">Het verificatietoken wordt opgeslagen in `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="b4ab4-127">Als u bijvoorbeeld de API 'Ophalen' gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b4ab4-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="b4ab4-128">Ophalen is beschikbaar als [npm-pakket](https://www.npmjs.com/package/whatwg-fetch), maar kan ook met een browser worden gedownload van [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="b4ab4-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="b4ab4-129">U kunt ook jQuery of een andere AJAX-API gebruiken voor het ophalen van de informatie.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="b4ab4-130">Gegevens worden ontvangen als JSON-object.</span><span class="sxs-lookup"><span data-stu-id="b4ab4-130">Data is received as a JSON object.</span></span>
