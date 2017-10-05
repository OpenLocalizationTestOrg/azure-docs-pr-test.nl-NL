---
title: Azure AD v2.0 .NET web-app aanroepen API aan de slag | Microsoft Docs
description: Het bouwen van een .NET MVC-Web-App dat aanroepen web services met behulp van persoonlijke Microsoft-accounts en werk of schoolaccounts voor aanmelden.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="a4c7d-103">Een web-API aanroept vanuit een .NET-web-app</span><span class="sxs-lookup"><span data-stu-id="a4c7d-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="a4c7d-104">U kunt snel verificatie toevoegen aan uw web-apps en web-API's met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccounts met het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a4c7d-105">Wij je hier een MVC-web-app die gebruikers in het gebruik van het OpenID Connect, met hulp van Microsoft OWIN middleware ondertekent bouwen.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="a4c7d-106">De web-app wordt OAuth 2.0-toegangstokens ophalen voor een web api is beveiligd met OAuth 2.0 waarmee maken, lezen en verwijderen op een bepaalde gebruiker 'takenlijst'.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="a4c7d-107">Deze zelfstudie wordt de nadruk gelegd voornamelijk over het gebruik van MSAL verkrijgen en toegangstokens gebruiken in een web-app beschreven in de volledige [hier](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="a4c7d-108">Als de vereisten, wilt u mogelijk eerst meer informatie over hoe [basic aanmelden toevoegen aan een web-app](active-directory-v2-devquickstarts-dotnet-web.md) of hoe [een web-API goed is beveiligd](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a4c7d-109">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a4c7d-110">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="a4c7d-111">Voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="a4c7d-111">Download sample code</span></span>
<span data-ttu-id="a4c7d-112">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="a4c7d-113">Als u wilt volgen, kunt u [basis van de app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="a4c7d-114">U kunt ook [downloaden van de voltooide app als een ZIP](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) of te klonen van de voltooide app:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="a4c7d-115">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="a4c7d-115">Register an app</span></span>
<span data-ttu-id="a4c7d-116">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a4c7d-117">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-117">Make sure to:</span></span>

* <span data-ttu-id="a4c7d-118">Noteer de **toepassings-Id** toegewezen aan uw app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="a4c7d-119">Maak een **App geheim** van de **wachtwoord** type en noteer de waarde voor later</span><span class="sxs-lookup"><span data-stu-id="a4c7d-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="a4c7d-120">Voeg de **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="a4c7d-121">Voer de juiste **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="a4c7d-122">De omleidings-uri geeft u aan Azure AD waarbij verificatie antwoorden moeten worden omgeleid: de standaardwaarde voor deze zelfstudie is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="a4c7d-123">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="a4c7d-123">Install OWIN</span></span>
<span data-ttu-id="a4c7d-124">Voeg de OWIN middleware NuGet-pakketten naar de `TodoList-WebApp` project met de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="a4c7d-125">De OWIN-middleware wordt aan- en afmeldingsaanvragen te verzenden, sessie van de gebruiker beheren en informatie over de gebruiker, onder andere gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="a4c7d-126">Meld u aan de gebruiker</span><span class="sxs-lookup"><span data-stu-id="a4c7d-126">Sign the user in</span></span>
<span data-ttu-id="a4c7d-127">Nu configureren de OWIN-middleware gebruiken de [OpenID Connect-verificatieprotocol](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="a4c7d-128">Open de `web.config` bestand in de hoofdmap van de `TodoList-WebApp` project en voer de configuratiewaarden van uw app in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="a4c7d-129">De `ida:ClientId` is de **toepassings-Id** toegewezen aan uw app in de portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="a4c7d-130">De `ida:ClientSecret` is de **App geheim** u hebt gemaakt in de portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="a4c7d-131">De `ida:RedirectUri` is de **omleidings-Uri** u hebt ingevoerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="a4c7d-132">Open de `web.config` bestand in de hoofdmap van de `TodoList-Service` project en vervang de `ida:Audience` met dezelfde **toepassings-Id** zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="a4c7d-133">Open het bestand `App_Start\Startup.Auth.cs` en voeg `using` -instructies voor de bibliotheken van hierboven.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="a4c7d-134">Implementeren in hetzelfde bestand de `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="a4c7d-135">De parameters die u opgeeft in `OpenIDConnectAuthenticationOptions` fungeert als coördinaten voor uw app om te communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="a4c7d-136">Gebruik MSAL toegangstokens ophalen</span><span class="sxs-lookup"><span data-stu-id="a4c7d-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="a4c7d-137">In de `AuthorizationCodeReceived` melding, die we willen gebruiken [OAuth 2.0 in combinatie met OpenID Connect](active-directory-v2-protocols.md) om in te wisselen van de authorization_code voor een toegangstoken uit aan de taak Service.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="a4c7d-138">MSAL kan dit proces toegankelijk maken voor u:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="a4c7d-139">Installeer eerst de evaluatieversie van MSAL:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="a4c7d-140">En voeg een andere `using` instructie voor de `App_Start\Startup.Auth.cs` -bestand voor MSAL.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="a4c7d-141">Voeg nu een nieuwe methode de `OnAuthorizationCodeReceived` gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="a4c7d-142">Deze handler MSAL gebruikt om te verkrijgen van een toegangstoken voor de API van de lijst met taken en het token opgeslagen in de MSAL tokencache voor later:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="a4c7d-143">MSAL heeft in de web-apps, een uitbreidbaar tokencache die kan worden gebruikt voor het opslaan van tokens.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="a4c7d-144">Dit voorbeeld implementeert de `NaiveSessionCache` die gebruikmaakt van HTTP-sessie opslag voor cache-tokens.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="a4c7d-145">De Web-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="a4c7d-145">Call the Web API</span></span>
<span data-ttu-id="a4c7d-146">Nu is het tijd om daadwerkelijk gebruiken de access_token die u hebt verkregen in stap 3.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="a4c7d-147">Open de web-app `Controllers\TodoListController.cs` bestand, waardoor alle CRUD-aanvragen naar de API van de lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="a4c7d-148">U kunt MSAL opnieuw gebruiken hier access_tokens ophalen uit de cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="a4c7d-149">Voeg eerst een `using` -instructie voor MSAL tot dit bestand.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="a4c7d-150">In de `Index` van de actie, gebruik MSAL `AcquireTokenSilentAsync` methode voor het ophalen van een access_token die kunnen worden gebruikt om gegevens te lezen van de takenlijst-service:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="a4c7d-151">Het resulterende token in het voorbeeld vervolgens worden toegevoegd aan de HTTP GET-aanvraag als de `Authorization` koptekst, die de takenlijst-service gebruikt voor het verifiëren van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="a4c7d-152">Als de takenlijst-service retourneert een `401 Unauthorized` antwoord wordt de access_tokens in MSAL niet meer geldig voor een bepaalde reden.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="a4c7d-153">In dit geval moet u eventuele access_tokens niet verwijderen uit de cache MSAL en weergeven van de gebruiker een bericht dat ze aanmelden moeten mogelijk, die wordt opnieuw gestart de stroom token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="a4c7d-154">Op dezelfde manier als MSAL kan een access_token retourneren voor een of andere reden is, moet u opdracht geven de gebruiker zich opnieuw aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="a4c7d-155">Dit is net zo eenvoudig als het afvangen van een `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="a4c7d-156">De exacte dezelfde `AcquireTokenSilentAsync` aanroep is implementd in de `Create` en `Delete` acties.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="a4c7d-157">In de web-apps, kunt u deze methode MSAL access_tokens ophalen wanneer u nodig hebt in uw app.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="a4c7d-158">MSAL zorgt voor het ophalen, opslaan in cache en vernieuwen van tokens voor u.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="a4c7d-159">Ten slotte bouwen en uitvoeren van uw app!</span><span class="sxs-lookup"><span data-stu-id="a4c7d-159">Finally, build and run your app!</span></span>  <span data-ttu-id="a4c7d-160">Meld u aan met een Microsoft-Account of een Azure AD-Account en zien hoe de identiteit van de gebruiker wordt weergegeven in de bovenste navigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="a4c7d-161">Toevoegen en verwijderen van enkele items uit de takenlijst van de gebruiker om te zien van dat de OAuth 2.0 API-aanroepen in actie beveiligd.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="a4c7d-162">U hebt nu een web-app & web-API beide beveiligd via standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="a4c7d-163">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) [vindt u hier](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a4c7d-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a4c7d-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4c7d-164">Next Steps</span></span>
<span data-ttu-id="a4c7d-165">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="a4c7d-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="a4c7d-166">De ontwikkelaarshandleiding v2.0 >></span><span class="sxs-lookup"><span data-stu-id="a4c7d-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a4c7d-167">StackOverflow 'azure active directory'-tag >></span><span class="sxs-lookup"><span data-stu-id="a4c7d-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a4c7d-168">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="a4c7d-168">Get security updates for our products</span></span>
<span data-ttu-id="a4c7d-169">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="a4c7d-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

