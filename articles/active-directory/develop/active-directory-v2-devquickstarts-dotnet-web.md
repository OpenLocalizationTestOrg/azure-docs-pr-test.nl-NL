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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Aanmelden tooan .NET MVC-webtoepassing toevoegen
Met Hallo v2.0-eindpunt, kunt u snel verificatie tooyour web-apps met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccount toevoegen.  In ASP.NET-web-apps, kunt u dit doen met behulp van Microsoft OWIN middleware is opgenomen in .NET Framework 4.5.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

 Hier gaan we gaat verder met een web-app die gebruikmaakt van OWIN toosign Hallo gebruiker in de weergave enige informatie over het Hallo-gebruiker en aanmelding gebruiker buiten de app Hallo Hallo.

## <a name="download"></a>Downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

Hallo voltooid app wordt op Hallo einde van deze zelfstudie ook aangeboden.

## <a name="register-an-app"></a>Een app registreren
Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.
* Hallo toevoegen **Web** platform voor uw app.
* Voer de juiste Hallo **omleidings-URI**. Hallo omleidings-uri geeft tooAzure AD waarbij verificatie antwoorden moeten worden omgeleid - Hallo standaardwaarde voor deze zelfstudie is `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Installeren en OWIN-verificatie configureren
Hier geconfigureerd Hallo OWIN middleware toouse hello OpenID Connect-verificatieprotocol.  OWIN gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.

1. toobegin, open Hallo `web.config` bestand in de hoofdmap Hallo van Hallo-project en voer de configuratiewaarden van uw app in Hallo `<appSettings>` sectie.

  * Hallo `ida:ClientId` Hallo is **toepassings-Id** tooyour-app in de portal voor registratie van Hallo toegewezen.
  * Hallo `ida:RedirectUri` Hallo is **omleidings-Uri** u hebt ingevoerd in het Hallo-portal.

2. Voeg vervolgens Hallo OWIN middleware NuGet-pakketten toohello-project via een Hallo Package Manager-Console.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Een 'OWIN-Opstartklasse' toohello project genoemd toevoegen `Startup.cs` rechts Klik op Hallo project--> **toevoegen** --> **Nieuw Item** --> Zoek naar 'OWIN'.  Hallo OWIN middleware Hallo worden ingeroepen `Configuration(...)` methode als uw app wordt gestart.
4. Hallo klassendeclaratie ook wijzigen`public partial class Startup` -we hebben u al deel uit van deze klasse geïmplementeerd in een ander bestand.  In Hallo `Configuration(...)` methode, een aanroep van tooConfigureAuth(...) tooset van verificatie voor uw web-app maken  

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

5. Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(...)` methode.  parameters die u opgeeft in Hallo `OpenIdConnectAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.  U moet ook tooset van verificatie van de Cookie - Hallo OpenID Connect middleware maakt gebruik van cookies onder Hallo behandelt.

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

## <a name="send-authentication-requests"></a>Verificatieaanvragen verzenden
Uw app is nu correct geconfigureerde toocommunicate met Hallo v2.0-eindpunt met Hallo OpenID Connect-verificatieprotocol.  OWIN heeft gezorgd voor alle Hallo lelijke details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van de gebruikerssessie.  Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u af.

- U kunt tags autoriseren in uw domeincontrollers toorequire die gebruiker zich aanmeldt voor de toegang tot een bepaalde pagina.  Open `Controllers\HomeController.cs`, en voeg Hallo `[Authorize]` tag toohello over controller.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- U kunt ook OWIN toodirectly probleem verificatieaanvragen van binnen uw code.  Open `Controllers\AccountController.cs`.  In Hallo SignIn() en SignOut() acties uitgeven OpenID Connect uitdaging afmelden aanvragen, respectievelijk.

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

- Open nu `Views\Shared\_LoginPartial.cshtml`.  Dit is waar u Hallo gebruiker koppelingen voor het aanmelden en afmelden van uw app weergeven en afdrukken Hallo gebruikersnaam in een weergave.

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

## <a name="display-user-information"></a>Gebruikersgegevens weergeven
Bij het verifiëren van gebruikers met OpenID Connect retourneert Hallo v2.0-eindpunt een id_token toohello app dat claims of asserties over Hallo gebruiker bevat.  U kunt deze claims toopersonalize uw app:

- Open Hallo `Controllers\HomeController.cs` bestand.  U hebt toegang tot Hallo gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.

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

## <a name="run"></a>Voer
Ten slotte bouwen en uitvoeren van uw app!   Meld u aan met een persoonlijk Microsoft-Account of een account voor werk of school en zien hoe de identiteit van de gebruiker hello wordt weergegeven in de bovenste navigatiebalk Hallo.  U hebt nu een web-app die is beveiligd met standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Volgende stappen
U kunt nu verplaatsen naar geavanceerdere onderwerpen.  U kunt tootry:

[Beveiligen van een Web-API met Hallo Hallo v2.0-eindpunt >>](active-directory-devquickstarts-webapi-dotnet.md)

Voor aanvullende bronnen voor uitchecken:

* [Hallo v2.0 ontwikkelaarshandleiding >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow 'azure active directory'-tag >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.
