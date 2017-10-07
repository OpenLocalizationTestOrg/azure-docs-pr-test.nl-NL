---
title: aaaAzure AD v2.0 .NET web-app aanmelden aan de slag | Microsoft Docs
description: Hoe toobuild een .NET MVC-Web-App die zich aanmeldt gebruikers met beide persoonlijke Microsoft-Account en werk- of schoolaccount accounts.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="b0f7f-103">Aanmelden tooan .NET MVC-webtoepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0f7f-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="b0f7f-104">Met Hallo v2.0-eindpunt, kunt u snel verificatie tooyour web-apps met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="b0f7f-105">In ASP.NET-web-apps, kunt u dit doen met behulp van Microsoft OWIN middleware is opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="b0f7f-106">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="b0f7f-107">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b0f7f-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="b0f7f-108">Hier gaan we gaat verder met een web-app die gebruikmaakt van OWIN toosign Hallo gebruiker in de weergave enige informatie over het Hallo-gebruiker en aanmelding gebruiker buiten de app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="b0f7f-109">Downloaden</span><span class="sxs-lookup"><span data-stu-id="b0f7f-109">Download</span></span>
<span data-ttu-id="b0f7f-110">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="b0f7f-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="b0f7f-111">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="b0f7f-112">Hallo voltooid app wordt op Hallo einde van deze zelfstudie ook aangeboden.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="b0f7f-113">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="b0f7f-113">Register an app</span></span>
<span data-ttu-id="b0f7f-114">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b0f7f-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="b0f7f-115">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-115">Make sure to:</span></span>

* <span data-ttu-id="b0f7f-116">Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="b0f7f-117">Hallo toevoegen **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="b0f7f-118">Voer de juiste Hallo **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="b0f7f-119">Hallo omleidings-uri geeft tooAzure AD waarbij verificatie antwoorden moeten worden omgeleid - Hallo standaardwaarde voor deze zelfstudie is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="b0f7f-120">Installeren en OWIN-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="b0f7f-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="b0f7f-121">Hier geconfigureerd Hallo OWIN middleware toouse hello OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b0f7f-122">OWIN gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="b0f7f-123">toobegin, open Hallo `web.config` bestand in de hoofdmap Hallo van Hallo-project en voer de configuratiewaarden van uw app in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="b0f7f-124">Hallo `ida:ClientId` Hallo is **toepassings-Id** tooyour-app in de portal voor registratie van Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="b0f7f-125">Hallo `ida:RedirectUri` Hallo is **omleidings-Uri** u hebt ingevoerd in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="b0f7f-126">Voeg vervolgens Hallo OWIN middleware NuGet-pakketten toohello-project via een Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="b0f7f-127">Een 'OWIN-Opstartklasse' toohello project genoemd toevoegen `Startup.cs` rechts Klik op Hallo project--> **toevoegen** --> **Nieuw Item** --> Zoek naar 'OWIN'.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="b0f7f-128">Hallo OWIN middleware Hallo worden ingeroepen `Configuration(...)` methode als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="b0f7f-129">Hallo klassendeclaratie ook wijzigen`public partial class Startup` -we hebben u al deel uit van deze klasse geïmplementeerd in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="b0f7f-130">In Hallo `Configuration(...)` methode, een aanroep van tooConfigureAuth(...) tooset van verificatie voor uw web-app maken</span><span class="sxs-lookup"><span data-stu-id="b0f7f-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="b0f7f-131">Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="b0f7f-132">parameters die u opgeeft in Hallo `OpenIdConnectAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="b0f7f-133">U moet ook tooset van verificatie van de Cookie - Hallo OpenID Connect middleware maakt gebruik van cookies onder Hallo behandelt.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="b0f7f-134">Verificatieaanvragen verzenden</span><span class="sxs-lookup"><span data-stu-id="b0f7f-134">Send authentication requests</span></span>
<span data-ttu-id="b0f7f-135">Uw app is nu correct geconfigureerde toocommunicate met Hallo v2.0-eindpunt met Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b0f7f-136">OWIN heeft gezorgd voor alle Hallo lelijke details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="b0f7f-137">Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u af.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="b0f7f-138">U kunt tags autoriseren in uw domeincontrollers toorequire die gebruiker zich aanmeldt voor de toegang tot een bepaalde pagina.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="b0f7f-139">Open `Controllers\HomeController.cs`, en voeg Hallo `[Authorize]` tag toohello over controller.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="b0f7f-140">U kunt ook OWIN toodirectly probleem verificatieaanvragen van binnen uw code.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="b0f7f-141">Open `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="b0f7f-142">In Hallo SignIn() en SignOut() acties uitgeven OpenID Connect uitdaging afmelden aanvragen, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="b0f7f-143">Open nu `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="b0f7f-144">Dit is waar u Hallo gebruiker koppelingen voor het aanmelden en afmelden van uw app weergeven en afdrukken Hallo gebruikersnaam in een weergave.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a><span data-ttu-id="b0f7f-145">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="b0f7f-145">Display user information</span></span>
<span data-ttu-id="b0f7f-146">Bij het verifiëren van gebruikers met OpenID Connect retourneert Hallo v2.0-eindpunt een id_token toohello app dat claims of asserties over Hallo gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="b0f7f-147">U kunt deze claims toopersonalize uw app:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="b0f7f-148">Open Hallo `Controllers\HomeController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="b0f7f-149">U hebt toegang tot Hallo gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="b0f7f-150">Voer</span><span class="sxs-lookup"><span data-stu-id="b0f7f-150">Run</span></span>
<span data-ttu-id="b0f7f-151">Ten slotte bouwen en uitvoeren van uw app!</span><span class="sxs-lookup"><span data-stu-id="b0f7f-151">Finally, build and run your app!</span></span>   <span data-ttu-id="b0f7f-152">Meld u aan met een persoonlijk Microsoft-Account of een account voor werk of school en zien hoe de identiteit van de gebruiker hello wordt weergegeven in de bovenste navigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="b0f7f-153">U hebt nu een web-app die is beveiligd met standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="b0f7f-154">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="b0f7f-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0f7f-155">Next steps</span></span>
<span data-ttu-id="b0f7f-156">U kunt nu verplaatsen naar geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="b0f7f-157">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-157">You may want tootry:</span></span>

[<span data-ttu-id="b0f7f-158">Beveiligen van een Web-API met Hallo Hallo v2.0-eindpunt >></span><span class="sxs-lookup"><span data-stu-id="b0f7f-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="b0f7f-159">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="b0f7f-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="b0f7f-160">Hallo v2.0 ontwikkelaarshandleiding >></span><span class="sxs-lookup"><span data-stu-id="b0f7f-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b0f7f-161">StackOverflow 'azure active directory'-tag >></span><span class="sxs-lookup"><span data-stu-id="b0f7f-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b0f7f-162">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="b0f7f-162">Get security updates for our products</span></span>
<span data-ttu-id="b0f7f-163">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="b0f7f-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
