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
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>ASP.NET-web-app aanmelden en afmelden met Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Dankzij één aanmelden en afmelden met slechts een paar regels code, kunt Azure Active Directory (Azure AD) u eenvoudig voor u toooutsource web-app identiteitsbeheer. U kunt gebruikers in en uit de ASP.NET-web-apps ondertekenen met behulp van Microsoft-implementatie Hallo van Open Web Interface voor .NET (OWIN) middleware. OWIN middleware community aangestuurde is opgenomen in .NET Framework 4.5. Dit artikel laat zien hoe toouse OWIN naar:

* Meld u aan gebruikers in tooweb apps met behulp van Azure AD als Hallo id-provider.
* Bepaalde gebruikersgegevens weergeven.
* Meld u aan gebruikers buiten het Hallo-apps.

## <a name="before-you-get-started"></a>Voordat u aan de slag gaat
* Hallo downloaden [basis app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* U moet ook een Azure AD-tenant in welke tooregister Hallo-app. Als u geen Azure AD-tenant al hebt [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende vier secties.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Stap 1: Hallo nieuwe app te registreren met Azure AD
tooset van Hallo app tooauthenticate gebruikers eerst registreren in de tenant door Hallo volgende te doen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op de accountnaam van uw. Onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Ga als volgt Hallo vraagt toocreate een nieuwe **webtoepassing en/of WebAPI**.
  * **Naam** Hallo app toousers beschrijft.
  * **Aanmeldings-URL** Hallo basis-URL van de app Hallo is. Hallo geraamte van standaard-URL is https://localhost:44320 /.
6. Nadat u Hallo-registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID. Hallo-waarde van Hallo app pagina toouse in de volgende secties Hallo kopiëren.
7. Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken. Hallo **App ID URI** is de unieke id voor Hallo-app. Hallo naamgevingsconventie is `https://<tenant-domain>/<app-name>` (bijvoorbeeld `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Stap 2: Hallo app toouse hello OWIN-verificatiepijplijn instellen
In deze stap configureert u Hallo OWIN middleware toouse hello OpenID Connect-verificatieprotocol. U gebruikt OWIN tooissue aanmelden en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren, ophalen van gebruikersgegevens, enzovoort.

1. toobegin, Hallo OWIN middleware NuGet-pakketten toohello project toevoegen met behulp van Hallo Package Manager-Console.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. een OWIN klasse toohello opstartproject aangeroepen tooadd `Startup.cs`, met de rechtermuisknop op het Hallo-project, selecteer **toevoegen**, selecteer **Nieuw Item**, en zoek vervolgens naar **OWIN**. Hallo OWIN middleware roept Hallo **Configuration(...)**  methode wanneer Hallo-app wordt gestart.
3. Hallo klassendeclaratie ook wijzigen`public partial class Startup`. We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand. In Hallo **Configuration(...)**  methode te maken van een aanroep van**ConfgureAuth(...)**  tooset van verificatie voor Hallo-app.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Hallo App_Start\Startup.Auth.cs bestand openen en vervolgens implementeren Hallo **ConfigureAuth(...)**  methode. parameters die u opgeeft in Hallo *OpenIDConnectAuthenticationOptions* fungeren als coördinaten voor Hallo app toocommunicate met Azure AD. Tooset van Cookieverificatie, moet u ook omdat Hallo OpenID Connect middleware gebruikmaakt van cookies op Hallo achtergrond.

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

5. Hallo web.config-bestand openen in de hoofdmap Hallo van Hallo-project en Voer Hallo configuratiewaarden in Hallo `<appSettings>` sectie.
  * `ida:ClientId`: Hallo GUID die u hebt gekopieerd uit hello Azure-portal in ' stap 1: registreren Hallo nieuwe app met Azure AD. "
  * `ida:Tenant`: Hallo-naam van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: Hallo-indicator die Azure AD geeft aan waar een gebruiker wordt omgeleid nadat een afmelden aanvraag is voltooid.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Stap 3: Gebruik OWIN tooissue aan- en afmeldingsaanvragen tooAzure AD-aanvragen
Hallo-app is nu correct geconfigureerde toocommunicate met Azure AD via Hallo OpenID Connect-verificatieprotocol. OWIN heeft afgehandeld alle details op Hallo van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies. Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u af.

1. U kunt labels in uw domeincontrollers toorequire gebruikers toosign in autoriseren voordat ze toegang krijgen bepaalde pagina's tot. toodo dus Controllers\HomeController.cs openen en voeg vervolgens Hallo `[Authorize]` tag toohello over controller.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. U kunt ook OWIN toodirectly probleem verificatieaanvragen van binnen uw code. Hiertoe opent u toodo Controllers\AccountController.cs. Vervolgens in het vak Hallo SignIn() en SignOut() acties uitgeven OpenID Connect uitdaging afmelden aanvragen.

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

3. Open Views\Shared\_LoginPartial.cshtml tooshow Hallo gebruiker Hallo app aanmelden en afmelden koppelingen en tooprint uit Hallo gebruikersnaam in een weergave.

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

## <a name="step-4-display-user-information"></a>Stap 4: Gebruikersgegevens weergeven
Wanneer gebruikers met OpenID Connect geverifieerd, retourneert Azure AD een id_token toohello app dat 'claims' of asserties over Hallo gebruiker bevat. U kunt deze app claims toopersonalize hello gebruiken door Hallo volgende te doen:

1. Hallo Controllers\HomeController.cs bestand openen. U hebt toegang tot Hallo gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.

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

2. Ontwikkel en Voer Hallo-app. Als u dit nog niet hebt al een nieuwe gebruiker in uw tenant met een onmicrosoft.com-domein gemaakt, is nu Hallo tijd toodo dus. Dit doet u al volgt:

  a. Meld u aan met die gebruiker en houd er rekening mee hoe Hallo gebruikersidentiteit is doorgevoerd op de bovenste balk Hallo.

  b. Meld u af en vervolgens weer aanmelden als een andere gebruiker in uw tenant.

  c. Als u in bijzonder ambitieuze een hebt, registreren en uitvoeren van een ander exemplaar van deze app (met een eigen clientId) en één aanmelding toe in actie bekijken.

## <a name="next-steps"></a>Volgende stappen
Zie voor een verwijzing naar [Hallo voltooid voorbeeld](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).

U kunt nu op toomore geavanceerde onderwerpen verplaatsen. Probeer bijvoorbeeld [beveiligen van een Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
