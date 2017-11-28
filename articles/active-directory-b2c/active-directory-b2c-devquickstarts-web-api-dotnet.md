---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een .NET-Web-app en roept u een web api met Azure Active Directory B2C en OAuth 2.0-toegangstokens.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="53e84-103">Azure AD B2C: Een .NET web API aanroepen vanuit een .NET-web-app</span><span class="sxs-lookup"><span data-stu-id="53e84-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="53e84-104">Met behulp van Azure AD B2C, kunt u krachtige identity management-functies tooyour web-apps en web-API's kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="53e84-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="53e84-105">Dit artikel wordt beschreven hoe toorequest toegang tot tokens en aanroepen vanuit een .NET 'takenlijst' web-app tooa .NET web-api.</span><span class="sxs-lookup"><span data-stu-id="53e84-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="53e84-106">Dit artikel wordt niet beschreven hoe tooimplement aanmelden, registreren en de profiel-beheer met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="53e84-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="53e84-107">Dit artikel gaat over het aanroepen van web API's nadat Hallo gebruiker al is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="53e84-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="53e84-108">Als u nog niet gedaan hebt, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="53e84-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="53e84-109">Aan de slag met een [.NET-web-app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="53e84-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="53e84-110">Aan de slag met een [.NET web-api](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="53e84-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="53e84-111">Vereiste</span><span class="sxs-lookup"><span data-stu-id="53e84-111">Prerequisite</span></span>

<span data-ttu-id="53e84-112">toobuild een webtoepassing die een web aanroept-api, moet u:</span><span class="sxs-lookup"><span data-stu-id="53e84-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="53e84-113">[Een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="53e84-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="53e84-114">[Registreren van een web api](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="53e84-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="53e84-115">[Een web-app registreren](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="53e84-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="53e84-116">[Instellen van het beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="53e84-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="53e84-117">[Verleen Hallo web app machtigingen toouse Hallo web-api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="53e84-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53e84-118">Hallo-clienttoepassing en web-API moeten Hallo dezelfde Azure AD B2C-directory gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53e84-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="53e84-119">Hallo code downloaden</span><span class="sxs-lookup"><span data-stu-id="53e84-119">Download hello code</span></span>

<span data-ttu-id="53e84-120">Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="53e84-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="53e84-121">U kunt Hallo voorbeeld klonen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="53e84-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="53e84-122">Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart.</span><span class="sxs-lookup"><span data-stu-id="53e84-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="53e84-123">Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="53e84-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="53e84-124">`TaskWebApp`is een MVC-webtoepassing die gebruiker Hallo communiceert met.</span><span class="sxs-lookup"><span data-stu-id="53e84-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="53e84-125">`TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is.</span><span class="sxs-lookup"><span data-stu-id="53e84-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="53e84-126">In dit artikel omvat niet gebouw Hallo `TaskWebApp` web-app of Hallo `TaskService` web-api.</span><span class="sxs-lookup"><span data-stu-id="53e84-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="53e84-127">toolearn hoe toobuild Hallo .NET web-app met Azure AD B2C, Zie onze [.NET web app-zelfstudie](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="53e84-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="53e84-128">toolearn hoe toobuild Hallo .NET web-API is beveiligd met Azure AD B2C, Zie onze [.NET-web-API-zelfstudie](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="53e84-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="53e84-129">Hello Azure AD B2C-configuratie bijwerken</span><span class="sxs-lookup"><span data-stu-id="53e84-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="53e84-130">Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant.</span><span class="sxs-lookup"><span data-stu-id="53e84-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="53e84-131">Als u toouse wilt uw eigen tenant:</span><span class="sxs-lookup"><span data-stu-id="53e84-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="53e84-132">Open `web.config` in Hallo `TaskService` project en vervang de waarden voor Hallo</span><span class="sxs-lookup"><span data-stu-id="53e84-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="53e84-133">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="53e84-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="53e84-134">`ida:ClientId`met de toepassings-ID van uw web-api</span><span class="sxs-lookup"><span data-stu-id="53e84-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="53e84-135">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="53e84-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="53e84-136">Open `web.config` in Hallo `TaskWebApp` project en vervang de waarden voor Hallo</span><span class="sxs-lookup"><span data-stu-id="53e84-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="53e84-137">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="53e84-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="53e84-138">`ida:ClientId` door de id van uw web-app-toepassing</span><span class="sxs-lookup"><span data-stu-id="53e84-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="53e84-139">`ida:ClientSecret` door de geheime sleutel voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="53e84-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="53e84-140">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="53e84-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="53e84-141">`ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid</span><span class="sxs-lookup"><span data-stu-id="53e84-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="53e84-142">`ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid</span><span class="sxs-lookup"><span data-stu-id="53e84-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="53e84-143">Aanvragen en het opslaan van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="53e84-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="53e84-144">Hallo machtigingen opgeven</span><span class="sxs-lookup"><span data-stu-id="53e84-144">Specify hello permissions</span></span>

<span data-ttu-id="53e84-145">In de volgorde toomake Hallo aanroep toohello web-API, moet u tooauthenticate Hallo gebruiker (met behulp van uw beleid sign-up-to-date/aanmelden) en [ontvangen van een toegangstoken](active-directory-b2c-access-tokens.md) van Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="53e84-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="53e84-146">In de volgorde tooreceive een toegangstoken, moet u eerst Hallo machtigingen die u wilt dat Hallo access token toogrant opgeven.</span><span class="sxs-lookup"><span data-stu-id="53e84-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="53e84-147">Hallo machtigingen zijn opgegeven in Hallo `scope` parameter wanneer u Hallo aanvraag toohello `/authorize` eindpunt.</span><span class="sxs-lookup"><span data-stu-id="53e84-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="53e84-148">Bijvoorbeeld, een toegangstoken Hello 'lezen' machtiging toohello resource-toepassing met tooacquire App ID URI van Hallo `https://contoso.onmicrosoft.com/tasks`, Hallo bereik zou worden `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="53e84-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="53e84-149">toospecify hello bereik in ons voorbeeld, open Hallo-bestand `App_Start\Startup.Auth.cs` en definieer Hallo `Scope` variabele in OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="53e84-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="53e84-150">Exchange Hallo autorisatiecode voor een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="53e84-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="53e84-151">Nadat een gebruiker is voltooid Hallo registreren of aanmelden ervaring, ontvangt de app een autorisatiecode van Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="53e84-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="53e84-152">Hallo OWIN OpenID Connect middleware Hallo code wordt opgeslagen, maar niet voor een toegangstoken exchange.</span><span class="sxs-lookup"><span data-stu-id="53e84-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="53e84-153">U kunt Hallo [MSAL bibliotheek](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake Hallo exchange.</span><span class="sxs-lookup"><span data-stu-id="53e84-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="53e84-154">In ons voorbeeld geconfigureerde een callback van querymelding in Hallo OpenID Connect middleware wanneer een autorisatiecode wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="53e84-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="53e84-155">In Hallo-retouraanroep we MSAL tooexchange Hallo code gebruiken voor een token en Hallo-token in Hallo cache op te slaan.</span><span class="sxs-lookup"><span data-stu-id="53e84-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="53e84-156">Hallo-web-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="53e84-156">Calling hello web API</span></span>

<span data-ttu-id="53e84-157">Deze sectie wordt beschreven hoe toouse Hallo token ontvangen tijdens sign-up-to-date/aanmelden met Azure AD B2C in volgorde Hallo tooaccess web-API.</span><span class="sxs-lookup"><span data-stu-id="53e84-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="53e84-158">Het ophalen van Hallo opgeslagen token in Hallo-domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="53e84-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="53e84-159">Hallo `TasksController` verantwoordelijk is voor communicatie met de Hallo web-API en voor het verzenden van HTTP-aanvragen toohello API tooread maken en verwijderen van taken.</span><span class="sxs-lookup"><span data-stu-id="53e84-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="53e84-160">Omdat Hallo API is beveiligd door Azure AD B2C, moet u token toofirst ophalen Hallo die u hebt opgeslagen in Hallo bovenstaande stap.</span><span class="sxs-lookup"><span data-stu-id="53e84-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="53e84-161">Lezen van de taken van Hallo web-API</span><span class="sxs-lookup"><span data-stu-id="53e84-161">Read tasks from hello web API</span></span>

<span data-ttu-id="53e84-162">Wanneer u een token hebt, kunt u koppelen het toohello HTTP `GET` aanvraag in Hallo `Authorization` header toosecurely aanroep `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="53e84-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="53e84-163">Maken en verwijderen van taken op Hallo web-API</span><span class="sxs-lookup"><span data-stu-id="53e84-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="53e84-164">Volg Hallo hetzelfde patroon bij het verzenden van `POST` en `DELETE` MSAL tooretrieve Hallo-toegangstoken uit Hallo cache toohello-web-API-aanvragen kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53e84-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="53e84-165">Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="53e84-165">Run hello sample app</span></span>

<span data-ttu-id="53e84-166">Ten slotte bouwen en uitvoeren van beide Hallo-apps.</span><span class="sxs-lookup"><span data-stu-id="53e84-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="53e84-167">Aanmelden en meld u aan en maak taken voor Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="53e84-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="53e84-168">Meld u af en meld u aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="53e84-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="53e84-169">Taken voor die gebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="53e84-169">Create tasks for that user.</span></span> <span data-ttu-id="53e84-170">U ziet hoe Hallo taken worden opgeslagen per gebruiker op Hallo API, omdat Hallo API de identiteit van de gebruiker Hallo haalt uit Hallo-token die wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="53e84-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="53e84-171">U kunt ook met Hallo scopes speelt.</span><span class="sxs-lookup"><span data-stu-id="53e84-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="53e84-172">Verwijder de machtigingen voor hello te 'schrijven' en probeer het toevoegen van een taak.</span><span class="sxs-lookup"><span data-stu-id="53e84-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="53e84-173">Zorg ervoor dat toosign uit telkens wanneer die u Hallo bereik wijzigen.</span><span class="sxs-lookup"><span data-stu-id="53e84-173">Just make sure toosign out each time you change hello scope.</span></span>

