---
title: Azure AD .NET web-app aan de slag | Microsoft Docs
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="109a7-103">ASP.NET-web-app aanmelden en afmelden met Azure AD</span><span class="sxs-lookup"><span data-stu-id="109a7-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="109a7-104">Dankzij één aanmelden en afmelden met slechts een paar regels code, kunt Azure Active Directory (Azure AD) u eenvoudig kunt uitbesteden Identiteitsbeheer voor web-app.</span><span class="sxs-lookup"><span data-stu-id="109a7-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="109a7-105">U kunt gebruikers in en uit de ASP.NET-web-apps ondertekenen met behulp van de Microsoft-implementatie van Open Web Interface voor .NET (OWIN) middleware.</span><span class="sxs-lookup"><span data-stu-id="109a7-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="109a7-106">OWIN middleware community aangestuurde is opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="109a7-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="109a7-107">In dit artikel laat zien hoe OWIN te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="109a7-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="109a7-108">Meld u aan gebruikers voor web-apps met behulp van Azure AD als de id-provider.</span><span class="sxs-lookup"><span data-stu-id="109a7-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="109a7-109">Bepaalde gebruikersgegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="109a7-109">Display some user information.</span></span>
* <span data-ttu-id="109a7-110">Meld u aan gebruikers buiten de apps.</span><span class="sxs-lookup"><span data-stu-id="109a7-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="109a7-111">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="109a7-111">Before you get started</span></span>
* <span data-ttu-id="109a7-112">Download de [basis app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) of download de [voltooide voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="109a7-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="109a7-113">U moet ook een Azure AD-tenant waarin de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="109a7-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="109a7-114">Als u geen Azure AD-tenant al hebt [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="109a7-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="109a7-115">Wanneer u klaar bent, voert u de procedures in de volgende vier secties.</span><span class="sxs-lookup"><span data-stu-id="109a7-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="109a7-116">Stap 1: De nieuwe app te registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="109a7-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="109a7-117">Voor het instellen van de app aan gebruikers worden geverifieerd, eerst registreren in de tenant door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="109a7-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="109a7-118">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="109a7-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="109a7-119">Klik op de accountnaam van uw op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="109a7-119">On the top bar, click your account name.</span></span> <span data-ttu-id="109a7-120">Onder de **Directory** , selecteert u de Active Directory-tenant waar u de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="109a7-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="109a7-121">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="109a7-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="109a7-122">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="109a7-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="109a7-123">Volg de aanwijzingen voor het maken van een nieuwe **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="109a7-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="109a7-124">**Naam** beschrijving van de app voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="109a7-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="109a7-125">**Aanmeldings-URL** is de basis-URL van de app.</span><span class="sxs-lookup"><span data-stu-id="109a7-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="109a7-126">Standaard-URL voor het basisproject is https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="109a7-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="109a7-127">Nadat u de registratie hebt voltooid, wijst Azure AD de app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="109a7-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="109a7-128">Kopieer de waarde van de pagina moet worden gebruikt in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="109a7-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="109a7-129">Van de **instellingen** -> **eigenschappen** pagina voor uw toepassing, het bijwerken van de App ID URI.</span><span class="sxs-lookup"><span data-stu-id="109a7-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="109a7-130">De **App ID URI** is de unieke id voor de app.</span><span class="sxs-lookup"><span data-stu-id="109a7-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="109a7-131">De naamgevingsconventie is `https://<tenant-domain>/<app-name>` (bijvoorbeeld `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="109a7-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="109a7-132">Stap 2: De app instellen voor de pijplijn OWIN-verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="109a7-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="109a7-133">In deze stap configureert u de OWIN-middleware voor gebruik van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="109a7-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="109a7-134">U kunt OWIN aan- en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren, ophalen van gebruikersgegevens, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="109a7-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="109a7-135">Toevoegen om te beginnen, de OWIN middleware NuGet-pakketten aan het project met de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="109a7-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="109a7-136">Een OWIN-Opstartklasse toevoegen aan het project met de naam `Startup.cs`, met de rechtermuisknop op het project, selecteer **toevoegen**, selecteer **Nieuw Item**, en zoek vervolgens naar **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="109a7-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="109a7-137">De OWIN-middleware roept de **Configuration(...)**  methode wanneer de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="109a7-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="109a7-138">Wijzig de klassendeclaratie naar `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="109a7-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="109a7-139">We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="109a7-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="109a7-140">In de **Configuration(...)**  een aanroep van methode **ConfgureAuth(...)**  verificatie voor de app instellen.</span><span class="sxs-lookup"><span data-stu-id="109a7-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="109a7-141">Open het bestand App_Start\Startup.Auth.cs en implementeer de **ConfigureAuth(...)**  methode.</span><span class="sxs-lookup"><span data-stu-id="109a7-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="109a7-142">De parameters die u opgeeft in *OpenIDConnectAuthenticationOptions* fungeren als coördinaten voor de app om te communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="109a7-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="109a7-143">U moet ook voor het instellen van de cookie-verificatie, omdat het OpenID Connect middleware gebruikmaakt van cookies op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="109a7-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="109a7-144">Open het bestand web.config in de hoofdmap van het project en voer vervolgens de configuratiewaarden in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="109a7-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="109a7-145">`ida:ClientId`: De GUID die u hebt gekopieerd uit de Azure-portal in ' stap 1: de nieuwe app te registreren met Azure AD. "</span><span class="sxs-lookup"><span data-stu-id="109a7-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="109a7-146">`ida:Tenant`: De naam van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="109a7-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="109a7-147">`ida:PostLogoutRedirectUri`: De indicator die Azure AD geeft aan waar een gebruiker wordt omgeleid nadat een afmelden aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="109a7-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="109a7-148">Stap 3: Gebruik OWIN om aan- en afmeldingsaanvragen te verzenden naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="109a7-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="109a7-149">De app is nu geconfigureerd om te communiceren met Azure AD met behulp van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="109a7-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="109a7-150">OWIN heeft afgehandeld dat alle gegevens van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies.</span><span class="sxs-lookup"><span data-stu-id="109a7-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="109a7-151">Alles wat u hoeft alleen nog uw gebruikers kunnen aanmelden en afmelden geven.</span><span class="sxs-lookup"><span data-stu-id="109a7-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="109a7-152">U kunt labels in uw domeincontrollers te vereisen dat gebruikers zich aanmelden voordat ze toegang krijgen bepaalde pagina's tot te autoriseren.</span><span class="sxs-lookup"><span data-stu-id="109a7-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="109a7-153">Om dit te doen, opent u Controllers\HomeController.cs en voeg vervolgens de `[Authorize]` label aan het Info-controller.</span><span class="sxs-lookup"><span data-stu-id="109a7-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="109a7-154">U kunt ook OWIN rechtstreeks uitgeven verificatieaanvragen van binnen uw code.</span><span class="sxs-lookup"><span data-stu-id="109a7-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="109a7-155">Open Controllers\AccountController.cs om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="109a7-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="109a7-156">Klik in de acties SignIn() en SignOut() uitgeven uitdaging OpenID Connect afmelden aanvragen.</span><span class="sxs-lookup"><span data-stu-id="109a7-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="109a7-157">Open Views\Shared\_LoginPartial.cshtml om weer te geven van de gebruiker de app aanmelden en afmelden koppelingen en de naam van de gebruiker in een weergave afdrukken.</span><span class="sxs-lookup"><span data-stu-id="109a7-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="109a7-158">Stap 4: Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="109a7-158">Step 4: Display user information</span></span>
<span data-ttu-id="109a7-159">Als deze zich gebruikers met OpenID Connect verifieert, retourneert Azure AD een id_token naar de app die 'claims' of asserties over de gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="109a7-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="109a7-160">U kunt deze claims gebruiken voor het aanpassen van de app als volgt:</span><span class="sxs-lookup"><span data-stu-id="109a7-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="109a7-161">Open het bestand Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="109a7-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="109a7-162">U hebt toegang tot claims van de gebruiker in uw domeincontrollers via de `ClaimsPrincipal.Current` SPN-object.</span><span class="sxs-lookup"><span data-stu-id="109a7-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="109a7-163">Ontwikkel en voer de app.</span><span class="sxs-lookup"><span data-stu-id="109a7-163">Build and run the app.</span></span> <span data-ttu-id="109a7-164">Als u dit nog niet hebt al een nieuwe gebruiker in uw tenant met een onmicrosoft.com-domein gemaakt, het is nu tijd om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="109a7-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="109a7-165">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="109a7-165">Here's how:</span></span>

  <span data-ttu-id="109a7-166">a.</span><span class="sxs-lookup"><span data-stu-id="109a7-166">a.</span></span> <span data-ttu-id="109a7-167">Meld u aan met die gebruiker en houd er rekening mee hoe de identiteit van de gebruiker wordt weergegeven op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="109a7-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="109a7-168">b.</span><span class="sxs-lookup"><span data-stu-id="109a7-168">b.</span></span> <span data-ttu-id="109a7-169">Meld u af en vervolgens weer aanmelden als een andere gebruiker in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="109a7-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="109a7-170">c.</span><span class="sxs-lookup"><span data-stu-id="109a7-170">c.</span></span> <span data-ttu-id="109a7-171">Als u in bijzonder ambitieuze een hebt, registreren en uitvoeren van een ander exemplaar van deze app (met een eigen clientId) en één aanmelding toe in actie bekijken.</span><span class="sxs-lookup"><span data-stu-id="109a7-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="109a7-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="109a7-172">Next steps</span></span>
<span data-ttu-id="109a7-173">Zie voor een verwijzing naar [het voltooide voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="109a7-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="109a7-174">U kunt nu verder met geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="109a7-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="109a7-175">Probeer bijvoorbeeld [beveiligen van een Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="109a7-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
