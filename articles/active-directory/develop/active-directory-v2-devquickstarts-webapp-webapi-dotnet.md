---
title: aaaAzure AD v2.0 .NET web-app aanroepen API aan de slag | Microsoft Docs
description: Hoe toobuild een Web-App voor .NET MVC-aanroepen van web-services met behulp van persoonlijke Microsoft-accounts en werk- of schoolaccounts voor aanmelden.
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
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="37c14-103">Een web-API aanroept vanuit een .NET-web-app</span><span class="sxs-lookup"><span data-stu-id="37c14-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="37c14-104">Met Hallo v2.0-eindpunt, kunt u snel toevoegen verificatie tooyour web-apps en web-API's met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccounts.</span><span class="sxs-lookup"><span data-stu-id="37c14-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="37c14-105">Wij je hier een MVC-web-app die gebruikers in het gebruik van het OpenID Connect, met hulp van Microsoft OWIN middleware ondertekent bouwen.</span><span class="sxs-lookup"><span data-stu-id="37c14-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="37c14-106">Hallo-web-app wordt OAuth 2.0-toegangstokens ophalen voor een web api is beveiligd met OAuth 2.0 waarmee maken, lezen en verwijderen op een bepaalde gebruiker 'takenlijst'.</span><span class="sxs-lookup"><span data-stu-id="37c14-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="37c14-107">Deze zelfstudie wordt voornamelijk over het gebruik van MSAL tooacquire richten en toegangstokens gebruiken in een web-app beschreven in de volledige [hier](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="37c14-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="37c14-108">Als de vereisten, wilt u wellicht toofirst meer informatie over hoe te[basic aanmelden tooa web-app toevoegen](active-directory-v2-devquickstarts-dotnet-web.md) of hoe te[een web-API goed is beveiligd](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="37c14-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37c14-109">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="37c14-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="37c14-110">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="37c14-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="37c14-111">Voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="37c14-111">Download sample code</span></span>
<span data-ttu-id="37c14-112">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="37c14-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="37c14-113">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="37c14-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="37c14-114">U kunt ook [Hallo voltooid app als een zip downloaden](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) of kloon voltooid Hallo app:</span><span class="sxs-lookup"><span data-stu-id="37c14-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="37c14-115">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="37c14-115">Register an app</span></span>
<span data-ttu-id="37c14-116">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="37c14-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="37c14-117">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="37c14-117">Make sure to:</span></span>

* <span data-ttu-id="37c14-118">Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="37c14-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="37c14-119">Maak een **App geheim** Hallo **wachtwoord** type en noteer de waarde voor later</span><span class="sxs-lookup"><span data-stu-id="37c14-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="37c14-120">Hallo toevoegen **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="37c14-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="37c14-121">Voer de juiste Hallo **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="37c14-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="37c14-122">Hallo omleidings-uri geeft tooAzure AD waarbij verificatie antwoorden moeten worden omgeleid - Hallo standaardwaarde voor deze zelfstudie is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="37c14-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="37c14-123">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="37c14-123">Install OWIN</span></span>
<span data-ttu-id="37c14-124">Hallo OWIN middleware NuGet-pakketten toohello toevoegen `TodoList-WebApp` project met Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="37c14-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="37c14-125">Hallo OWIN middleware gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.</span><span class="sxs-lookup"><span data-stu-id="37c14-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="37c14-126">Meld u Hallo gebruiker in</span><span class="sxs-lookup"><span data-stu-id="37c14-126">Sign hello user in</span></span>
<span data-ttu-id="37c14-127">Nu configureren Hallo OWIN middleware toouse hello [OpenID Connect-verificatieprotocol](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="37c14-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="37c14-128">Open Hallo `web.config` bestand in de hoofdmap Hallo Hallo `TodoList-WebApp` project en voer waarden in uw app-configuratie in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="37c14-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="37c14-129">Hallo `ida:ClientId` Hallo is **toepassings-Id** tooyour-app in de portal voor registratie van Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="37c14-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="37c14-130">Hallo `ida:ClientSecret` Hallo is **App geheim** u hebt gemaakt in het Hallo-portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="37c14-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="37c14-131">Hallo `ida:RedirectUri` Hallo is **omleidings-Uri** u hebt ingevoerd in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="37c14-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="37c14-132">Open Hallo `web.config` bestand in de hoofdmap Hallo Hallo `TodoList-Service` project en vervang Hallo `ida:Audience` Hallo met dezelfde **toepassings-Id** zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="37c14-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="37c14-133">Open Hallo bestand `App_Start\Startup.Auth.cs` en voeg `using` -instructies voor het Hallo-bibliotheken van hierboven.</span><span class="sxs-lookup"><span data-stu-id="37c14-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="37c14-134">In hetzelfde bestand Hallo, Hallo implementeren `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="37c14-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="37c14-135">parameters die u opgeeft in Hallo `OpenIDConnectAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37c14-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="37c14-136">Toegangstokens voor MSAL tooget gebruiken</span><span class="sxs-lookup"><span data-stu-id="37c14-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="37c14-137">In Hallo `AuthorizationCodeReceived` melding, willen we toouse [OAuth 2.0 in combinatie met OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code voor een access token toohello taak List-Service.</span><span class="sxs-lookup"><span data-stu-id="37c14-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="37c14-138">MSAL kan dit proces toegankelijk maken voor u:</span><span class="sxs-lookup"><span data-stu-id="37c14-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="37c14-139">Installeer eerst Hallo preview-versie van MSAL:</span><span class="sxs-lookup"><span data-stu-id="37c14-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="37c14-140">En voeg een andere `using` instructie toohello `App_Start\Startup.Auth.cs` -bestand voor MSAL.</span><span class="sxs-lookup"><span data-stu-id="37c14-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="37c14-141">Nu een nieuwe methode toevoegen, hello `OnAuthorizationCodeReceived` gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="37c14-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="37c14-142">Deze handler MSAL tooacquire een access token toohello taak lijst API wordt gebruikt en Hallo token opgeslagen in de MSAL tokencache voor later:</span><span class="sxs-lookup"><span data-stu-id="37c14-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="37c14-143">MSAL heeft in web-apps, een uitbreidbaar tokencache die gebruikt toostore tokens worden kan.</span><span class="sxs-lookup"><span data-stu-id="37c14-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="37c14-144">Dit voorbeeld implementeert Hallo `NaiveSessionCache` waarvoor HTTP-sessie opslag toocache tokens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37c14-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="37c14-145">Hallo-Web-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="37c14-145">Call hello Web API</span></span>
<span data-ttu-id="37c14-146">Nu is het tijd tooactually hello access_token die u hebt verkregen in stap 3 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37c14-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="37c14-147">Open Hallo van web-app `Controllers\TodoListController.cs` bestand, waardoor alle Hallo CRUD toohello taak lijst API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="37c14-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="37c14-148">U kunt MSAL opnieuw hier toofetch access_tokens van MSAL cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="37c14-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="37c14-149">Voeg eerst een `using` -instructie voor MSAL toothis bestand.</span><span class="sxs-lookup"><span data-stu-id="37c14-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="37c14-150">In Hallo `Index` van de actie, gebruik MSAL `AcquireTokenSilentAsync` methode tooget een access_token die gebruikt tooread gegevens van Hallo takenlijst-service worden kunnen:</span><span class="sxs-lookup"><span data-stu-id="37c14-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="37c14-151">Hallo voorbeeld vervolgens toegevoegd Hallo resulterende token toohello HTTP GET-aanvraag als Hallo `Authorization` -kop, welke service van de takenlijst Hallo tooauthenticate Hallo aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37c14-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="37c14-152">Als Hallo takenlijst-service retourneert een `401 Unauthorized` antwoord Hallo access_tokens in MSAL niet meer geldig voor een bepaalde reden.</span><span class="sxs-lookup"><span data-stu-id="37c14-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="37c14-153">In dit geval moet u eventuele access_tokens niet verwijderen uit de Hallo MSAL cache en Hallo-gebruiker een bericht dat toosign moeten in, die wordt opnieuw gestart Hallo token overname stroom weergeven.</span><span class="sxs-lookup"><span data-stu-id="37c14-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="37c14-154">Op dezelfde manier als MSAL niet kan tooreturn een access_token om welke reden, moet u opdracht geven Hallo gebruiker toosign in opnieuw.</span><span class="sxs-lookup"><span data-stu-id="37c14-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="37c14-155">Dit is net zo eenvoudig als het afvangen van een `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="37c14-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="37c14-156">Hallo exact dezelfde `AcquireTokenSilentAsync` aanroep is implementd in Hallo `Create` en `Delete` acties.</span><span class="sxs-lookup"><span data-stu-id="37c14-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="37c14-157">In de web-apps, kunt u deze MSAL methode tooget access_tokens wanneer u nodig hebt in uw app.</span><span class="sxs-lookup"><span data-stu-id="37c14-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="37c14-158">MSAL zorgt voor het ophalen, opslaan in cache en vernieuwen van tokens voor u.</span><span class="sxs-lookup"><span data-stu-id="37c14-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="37c14-159">Ten slotte bouwen en uitvoeren van uw app!</span><span class="sxs-lookup"><span data-stu-id="37c14-159">Finally, build and run your app!</span></span>  <span data-ttu-id="37c14-160">Meld u aan met een Microsoft-Account of een Azure AD-Account en zien hoe de identiteit van de gebruiker hello wordt weergegeven in de bovenste navigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="37c14-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="37c14-161">Voeg toe en verwijder enkele items uit de takenlijst van de gebruiker Hallo toosee Hallo die OAuth 2.0 beveiligd API-in actie aanroepen.</span><span class="sxs-lookup"><span data-stu-id="37c14-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="37c14-162">U hebt nu een web-app & web-API beide beveiligd via standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="37c14-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="37c14-163">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [vindt u hier](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="37c14-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="37c14-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37c14-164">Next Steps</span></span>
<span data-ttu-id="37c14-165">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="37c14-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="37c14-166">Hallo v2.0 ontwikkelaarshandleiding >></span><span class="sxs-lookup"><span data-stu-id="37c14-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="37c14-167">StackOverflow 'azure active directory'-tag >></span><span class="sxs-lookup"><span data-stu-id="37c14-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="37c14-168">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="37c14-168">Get security updates for our products</span></span>
<span data-ttu-id="37c14-169">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="37c14-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

