---
title: aaaAzure AD .NET web-app aan de slag | Microsoft Docs
description: Maken van een .NET MVC-web-app die met Azure AD voor aanmelden integreert.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="c1de8-103">ASP.NET-web-app aanmelden en afmelden met Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1de8-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c1de8-104">Dankzij één aanmelden en afmelden met slechts een paar regels code, kunt Azure Active Directory (Azure AD) u eenvoudig voor u toooutsource web-app identiteitsbeheer.</span><span class="sxs-lookup"><span data-stu-id="c1de8-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="c1de8-105">U kunt gebruikers in en uit de ASP.NET-web-apps ondertekenen met behulp van Microsoft-implementatie Hallo van Open Web Interface voor .NET (OWIN) middleware.</span><span class="sxs-lookup"><span data-stu-id="c1de8-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="c1de8-106">OWIN middleware community aangestuurde is opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c1de8-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="c1de8-107">Dit artikel laat zien hoe toouse OWIN naar:</span><span class="sxs-lookup"><span data-stu-id="c1de8-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="c1de8-108">Meld u aan gebruikers in tooweb apps met behulp van Azure AD als Hallo id-provider.</span><span class="sxs-lookup"><span data-stu-id="c1de8-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="c1de8-109">Bepaalde gebruikersgegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="c1de8-109">Display some user information.</span></span>
* <span data-ttu-id="c1de8-110">Meld u aan gebruikers buiten het Hallo-apps.</span><span class="sxs-lookup"><span data-stu-id="c1de8-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="c1de8-111">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="c1de8-111">Before you get started</span></span>
* <span data-ttu-id="c1de8-112">Hallo downloaden [basis app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c1de8-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="c1de8-113">U moet ook een Azure AD-tenant in welke tooregister Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="c1de8-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="c1de8-114">Als u geen Azure AD-tenant al hebt [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c1de8-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="c1de8-115">Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende vier secties.</span><span class="sxs-lookup"><span data-stu-id="c1de8-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="c1de8-116">Stap 1: Hallo nieuwe app te registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1de8-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="c1de8-117">tooset van Hallo app tooauthenticate gebruikers eerst registreren in de tenant door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="c1de8-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="c1de8-118">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1de8-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1de8-119">Op de bovenste balk hello, klikt u op de accountnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="c1de8-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="c1de8-120">Onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.</span><span class="sxs-lookup"><span data-stu-id="c1de8-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="c1de8-121">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1de8-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c1de8-122">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c1de8-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c1de8-123">Ga als volgt Hallo vraagt toocreate een nieuwe **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="c1de8-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="c1de8-124">**Naam** Hallo app toousers beschrijft.</span><span class="sxs-lookup"><span data-stu-id="c1de8-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="c1de8-125">**Aanmeldings-URL** Hallo basis-URL van de app Hallo is.</span><span class="sxs-lookup"><span data-stu-id="c1de8-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="c1de8-126">Hallo geraamte van standaard-URL is https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="c1de8-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="c1de8-127">Nadat u Hallo-registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="c1de8-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="c1de8-128">Hallo-waarde van Hallo app pagina toouse in de volgende secties Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c1de8-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="c1de8-129">Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c1de8-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="c1de8-130">Hallo **App ID URI** is de unieke id voor Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="c1de8-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="c1de8-131">Hallo naamgevingsconventie is `https://<tenant-domain>/<app-name>` (bijvoorbeeld `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="c1de8-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="c1de8-132">Stap 2: Hallo app toouse hello OWIN-verificatiepijplijn instellen</span><span class="sxs-lookup"><span data-stu-id="c1de8-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="c1de8-133">In deze stap configureert u Hallo OWIN middleware toouse hello OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="c1de8-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c1de8-134">U gebruikt OWIN tooissue aanmelden en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren, ophalen van gebruikersgegevens, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c1de8-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="c1de8-135">toobegin, Hallo OWIN middleware NuGet-pakketten toohello project toevoegen met behulp van Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="c1de8-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="c1de8-136">een OWIN klasse toohello opstartproject aangeroepen tooadd `Startup.cs`, met de rechtermuisknop op het Hallo-project, selecteer **toevoegen**, selecteer **Nieuw Item**, en zoek vervolgens naar **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="c1de8-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="c1de8-137">Hallo OWIN middleware roept Hallo **Configuration(...)**  methode wanneer Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c1de8-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="c1de8-138">Hallo klassendeclaratie ook wijzigen`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="c1de8-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="c1de8-139">We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="c1de8-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="c1de8-140">In Hallo **Configuration(...)**  methode te maken van een aanroep van**ConfgureAuth(...)**  tooset van verificatie voor Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="c1de8-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="c1de8-141">Hallo App_Start\Startup.Auth.cs bestand openen en vervolgens implementeren Hallo **ConfigureAuth(...)**  methode.</span><span class="sxs-lookup"><span data-stu-id="c1de8-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="c1de8-142">parameters die u opgeeft in Hallo *OpenIDConnectAuthenticationOptions* fungeren als coördinaten voor Hallo app toocommunicate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1de8-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="c1de8-143">Tooset van Cookieverificatie, moet u ook omdat Hallo OpenID Connect middleware gebruikmaakt van cookies op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="c1de8-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="c1de8-144">Hallo web.config-bestand openen in de hoofdmap Hallo van Hallo-project en Voer Hallo configuratiewaarden in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="c1de8-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="c1de8-145">`ida:ClientId`: Hallo GUID die u hebt gekopieerd uit hello Azure-portal in ' stap 1: registreren Hallo nieuwe app met Azure AD. "</span><span class="sxs-lookup"><span data-stu-id="c1de8-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="c1de8-146">`ida:Tenant`: Hallo-naam van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c1de8-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="c1de8-147">`ida:PostLogoutRedirectUri`: Hallo-indicator die Azure AD geeft aan waar een gebruiker wordt omgeleid nadat een afmelden aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c1de8-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="c1de8-148">Stap 3: Gebruik OWIN tooissue aan- en afmeldingsaanvragen tooAzure AD-aanvragen</span><span class="sxs-lookup"><span data-stu-id="c1de8-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="c1de8-149">Hallo-app is nu correct geconfigureerde toocommunicate met Azure AD via Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="c1de8-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c1de8-150">OWIN heeft afgehandeld alle details op Hallo van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies.</span><span class="sxs-lookup"><span data-stu-id="c1de8-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="c1de8-151">Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u af.</span><span class="sxs-lookup"><span data-stu-id="c1de8-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="c1de8-152">U kunt labels in uw domeincontrollers toorequire gebruikers toosign in autoriseren voordat ze toegang krijgen bepaalde pagina's tot.</span><span class="sxs-lookup"><span data-stu-id="c1de8-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="c1de8-153">toodo dus Controllers\HomeController.cs openen en voeg vervolgens Hallo `[Authorize]` tag toohello over controller.</span><span class="sxs-lookup"><span data-stu-id="c1de8-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="c1de8-154">U kunt ook OWIN toodirectly probleem verificatieaanvragen van binnen uw code.</span><span class="sxs-lookup"><span data-stu-id="c1de8-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="c1de8-155">Hiertoe opent u toodo Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="c1de8-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="c1de8-156">Vervolgens in het vak Hallo SignIn() en SignOut() acties uitgeven OpenID Connect uitdaging afmelden aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c1de8-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="c1de8-157">Open Views\Shared\_LoginPartial.cshtml tooshow Hallo gebruiker Hallo app aanmelden en afmelden koppelingen en tooprint uit Hallo gebruikersnaam in een weergave.</span><span class="sxs-lookup"><span data-stu-id="c1de8-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="c1de8-158">Stap 4: Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="c1de8-158">Step 4: Display user information</span></span>
<span data-ttu-id="c1de8-159">Wanneer gebruikers met OpenID Connect geverifieerd, retourneert Azure AD een id_token toohello app dat 'claims' of asserties over Hallo gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="c1de8-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="c1de8-160">U kunt deze app claims toopersonalize hello gebruiken door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="c1de8-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="c1de8-161">Hallo Controllers\HomeController.cs bestand openen.</span><span class="sxs-lookup"><span data-stu-id="c1de8-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="c1de8-162">U hebt toegang tot Hallo gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.</span><span class="sxs-lookup"><span data-stu-id="c1de8-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="c1de8-163">Ontwikkel en Voer Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="c1de8-163">Build and run hello app.</span></span> <span data-ttu-id="c1de8-164">Als u dit nog niet hebt al een nieuwe gebruiker in uw tenant met een onmicrosoft.com-domein gemaakt, is nu Hallo tijd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="c1de8-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="c1de8-165">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="c1de8-165">Here's how:</span></span>

  <span data-ttu-id="c1de8-166">a.</span><span class="sxs-lookup"><span data-stu-id="c1de8-166">a.</span></span> <span data-ttu-id="c1de8-167">Meld u aan met die gebruiker en houd er rekening mee hoe Hallo gebruikersidentiteit is doorgevoerd op de bovenste balk Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1de8-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="c1de8-168">b.</span><span class="sxs-lookup"><span data-stu-id="c1de8-168">b.</span></span> <span data-ttu-id="c1de8-169">Meld u af en vervolgens weer aanmelden als een andere gebruiker in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="c1de8-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="c1de8-170">c.</span><span class="sxs-lookup"><span data-stu-id="c1de8-170">c.</span></span> <span data-ttu-id="c1de8-171">Als u in bijzonder ambitieuze een hebt, registreren en uitvoeren van een ander exemplaar van deze app (met een eigen clientId) en één aanmelding toe in actie bekijken.</span><span class="sxs-lookup"><span data-stu-id="c1de8-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1de8-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1de8-172">Next steps</span></span>
<span data-ttu-id="c1de8-173">Zie voor een verwijzing naar [Hallo voltooid voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="c1de8-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="c1de8-174">U kunt nu op toomore geavanceerde onderwerpen verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c1de8-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="c1de8-175">Probeer bijvoorbeeld [beveiligen van een Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c1de8-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
