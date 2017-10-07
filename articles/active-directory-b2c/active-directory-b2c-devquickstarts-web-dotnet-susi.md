---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een webtoepassing met sign-up-to-date/aanmelden, bewerken en wachtwoord opnieuw instellen met behulp van Azure Active Directory B2C profiel.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Een ASP.NET-web-app maken met Azure Active Directory B2C registreren, aanmelden, profiel bewerken en wachtwoord opnieuw instellen

In deze handleiding ontdekt u hoe u:

> [!div class="checklist"]
> * Azure AD B2C identiteit functies tooyour web-app toevoegen
> * Registreren van uw web-app in uw Azure AD B2C-directory
> * Maak een gebruiker sign-up-to-date/aanmelden, profiel bewerken, en beleid voor uw web-app-wachtwoord opnieuw instellen

## <a name="prerequisites"></a>Vereisten

- U moet uw B2C-Tenant tooan Azure-account. U kunt een gratis Azure-account maken [hier](https://azure.microsoft.com/en-us/).
- U moet [Microsoft Visual Studio](https://www.visualstudio.com/) of een vergelijkbare tooview programma en voorbeeldcode Hallo wijzigen.

## <a name="create-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken

Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken. Een directory is een container voor alle gebruikers, apps en groepen. Als u niet een al hebt, maakt u een B2C-directory voordat u in deze handleiding doorgaat.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> U moet tooconnect Hallo B2C-Tenant tooyour Azure-abonnement. Na het selecteren van **maken**, selecteer Hallo **koppeling een bestaande Azure AD B2C-Tenant toomy Azure-abonnement** optie en klik vervolgens in Hallo **Azure AD B2C-Tenant** vervolgkeuzelijst, selecteer Hallo tenant gewenste tooassociate.

## <a name="create-and-register-an-application"></a>Het maken en een toepassing registreren

Vervolgens moet toocreate en Hallo app registreren in uw B2C-directory. Hierdoor krijgt u informatie dat Azure AD B2C toosecurely moet communiceren met uw app. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Wanneer u klaar bent, hebt u zowel een API en een systeemeigen toepassing in de instellingen van de toepassing.

## <a name="create-policies-on-your-b2c-tenant"></a>Beleid op uw B2C-tenant maken

In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Dit codevoorbeeld bevat drie identiteitservaringen: **aanmelding & aanmelden**, **profiel bewerken**, en **wachtwoordherstel**.  U moet toocreate één beleid voor elk type, zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md). Voor elk beleid worden ervoor tooselect Hallo weergave naamkenmerk of claim en toocopy omlaag Hallo-naam van uw beleid voor later gebruik.

### <a name="add-your-identity-providers"></a>Id-providers toevoegen

Selecteer in de instellingen voor **identiteitsproviders** en kiest u registratie van de gebruikersnaam of e-aanmelding.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Maak een beleid voor aanmelden en aanmelden

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Maken van een profiel te bewerken van beleid

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Maak een beleid voor wachtwoord opnieuw instellen

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.

## <a name="download-hello-sample-code"></a>Hallo voorbeeldcode downloaden

Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). U kunt Hallo voorbeeld klonen door te voeren:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart. Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`. `TaskWebApp`is Hallo MVC-webtoepassing die gebruiker Hallo communiceert met. `TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is. In dit artikel wordt alleen besproken Hallo `TaskWebApp` toepassing. toolearn hoe toobuild `TaskService` met behulp van Azure AD B2C, Zie [onze .NET web api-zelfstudie](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Bijwerken van code toouse uw tenant en -beleid

Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant. tooconnect het eigen tooyour-tenant, moet u tooopen `web.config` in Hallo `TaskWebApp` project en vervang Hallo volgende waarden:

* `ida:Tenant` door de naam van uw tenant
* `ida:ClientId` door de id van uw web-app-toepassing
* `ida:ClientSecret` door de geheime sleutel voor uw web-app
* `ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid
* `ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid
* `ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid

## <a name="launch-hello-app"></a>Hallo-app starten
Start vanaf Hallo-app in Visual Studio. Navigeer toohello takenlijst tabblad en de opmerking Hallo-URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Zich registreren voor Hallo-app met behulp van de naam van uw e-mailadres of de gebruiker. Afmelden, en vervolgens opnieuw aan te melden en Hallo profiel bewerken of Hallo wachtwoord opnieuw instellen. Meld u af en meld u aan als een andere gebruiker. 

## <a name="add-social-idps"></a>Sociale IDPs toevoegen

Hallo app ondersteunt momenteel alleen de gebruiker zich kunnen registreren en aanmelden met behulp van **lokale accounts**; accounts opgeslagen in uw B2C-directory die gebruikmaken van een gebruikersnaam en wachtwoord. U kunt ondersteuning voor andere toevoegen met behulp van Azure AD B2C **identiteitsproviders** (IDPs) zonder uw code.

tooadd sociale IDPs tooyour app volg eerst Hallo gedetailleerde instructies in deze artikelen. Voor elke IDP gewenste toosupport, u moet een toepassing tooregister in dat systeem en verkrijgen van een client-ID.

* [Facebook ingesteld als een IDP](active-directory-b2c-setup-fb-app.md)
* [Google ingesteld als een IDP](active-directory-b2c-setup-goog-app.md)
* [Amazon ingesteld als een IDP](active-directory-b2c-setup-amzn-app.md)
* [LinkedIn instellen als een IDP](active-directory-b2c-setup-li-app.md)

Nadat u hebt toegevoegd Hallo identiteit providers tooyour B2C-directory, bewerken van uw drie beleidsregels tooinclude nieuwe IDPs Hallo zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md). Nadat u uw beleid opslaat, Voer u Hallo app opnieuw.  U ziet Hallo die nieuwe IDPs als opties voor aanmelden en registreren in elk van uw identiteitservaringen toegevoegd.

U kunt experimenteren met het beleid en observeren Hallo effect op uw voorbeeld-app. Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen. Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en OWIN met elkaar verbinden.

## <a name="sample-code-walkthrough"></a>Voorbeeld code-overzicht
Hallo volgende secties ziet u hoe de voorbeeldcode toepassing hello is geconfigureerd. U kunt dit als richtlijn bij het ontwikkelen van toekomstige app.

### <a name="add-authentication-support"></a>Toevoegen van ondersteuning voor verificatie

U kunt nu uw app toouse Azure AD B2C configureren. Uw app communiceert met Azure AD B2C door te sturen verificatieaanvragen OpenID Connect. Hallo aanvragen dicteren Hallo gebruikerservaring uw app wil tooexecute door te geven Hallo-beleid. U kunt gebruiken van Microsoft OWIN-bibliotheek toosend deze aanvragen, beleid uitvoeren, beheren van gebruikerssessies en meer.

#### <a name="install-owin"></a>OWIN installeren

toobegin, Hallo OWIN middleware NuGet-pakketten toohello project toevoegen met behulp van Hallo Visual Studio Package Manager-Console.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Een OWIN-opstartklasse toevoegen

Voeg een OWIN starten van de klasse toohello API aangeroepen `Startup.cs`.  Met de rechtermuisknop op het Hallo-project, selecteer **toevoegen** en **Nieuw Item**, en zoek naar OWIN. Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.

In ons voorbeeld wijzigen we Hallo klassendeclaratie te`public partial class Startup` en geïmplementeerd met andere onderdelen van de klasse in Hallo Hallo `App_Start\Startup.Auth.cs`. Hallo binnen `Configuration` methode, hebben we een gesprek te toegevoegd`ConfigureAuth`, die is gedefinieerd in `Startup.Auth.cs`. Na het Hallo-wijzigingen `Startup.cs` Hallo volgende lijkt:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Hallo verificatiemiddleware configureren

Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(...)` methode. parameters die u opgeeft in Hallo `OpenIdConnectAuthenticationOptions` fungeren als coördinaten voor de toocommunicate van uw app met Azure AD B2C. Als u bepaalde parameters niet opgeeft, wordt de standaardwaarde Hallo gebruikt. Bijvoorbeeld: we geen Hallo opgeeft `ResponseType` in voorbeeld Hallo Hallo dus standaardwaarde `code id_token` in elke uitgaande aanvraag tooAzure AD B2C wordt gebruikt.

U moet ook tooset van Cookieverificatie. Hallo OpenID Connect middleware maakt gebruik van cookies toomaintain gebruikerssessies, onder andere.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

In `OpenIdConnectAuthenticationOptions` , definiëren we een set callback-functies voor specifieke meldingen die worden ontvangen door Hallo OpenID Connect middleware. Deze problemen zijn gedefinieerd met behulp van een `OpenIdConnectAuthenticationNotifications` object en opgeslagen in Hallo `Notifications` variabele. In ons voorbeeld definiëren we drie verschillende retouraanroepen afhankelijk van het Hallo-gebeurtenis.

### <a name="using-different-policies"></a>Met behulp van verschillende beleidsregels

Hallo `RedirectToIdentityProvider` melding wordt geactiveerd wanneer een aanvraag wordt gedaan tooAzure AD B2C. In de callback-functie Hallo `OnRedirectToIdentityProvider`, we in Hallo uitgaande oproep als we toouse wilt controleren of een ander beleid. In volgorde toodo een wachtwoord opnieuw instellen of een profiel te bewerken, moet u toouse Hallo corresponderende beleid zoals Hallo wachtwoord opnieuw instellen van beleid in plaats van Hallo "Registreren of aanmelden" standaardbeleid.

In ons voorbeeld wanneer een gebruiker wil tooreset Hallo wachtwoord of Hallo-profiel te bewerken we Hallo beleid toevoegen we toouse liever naar Hallo OWIN context. Dat kan worden gedaan door Hallo volgende te doen:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

En u kunt de callback-functie Hallo implementeren `OnRedirectToIdentityProvider` door Hallo volgende te doen:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Afhandeling van autorisatiecodes

Hallo `AuthorizationCodeReceived` melding wordt geactiveerd wanneer een autorisatiecode wordt ontvangen. Hallo OpenID Connect middleware biedt geen ondersteuning voor uitwisselen codes voor toegangstokens. U kunt handmatig uitwisselen Hallo-code voor het Hallo-token in een callback-functie. Raadpleeg voor meer informatie Hallo [documentatie](active-directory-b2c-devquickstarts-web-api-dotnet.md) waarin wordt uitgelegd hoe.

### <a name="handling-errors"></a>Foutafhandeling

Hallo `AuthenticationFailed` melding wordt geactiveerd wanneer de verificatie is mislukt. In de callback-methode kunt u fouten Hallo verwerken als u wilt. U moet echter een controle voor de foutcode Hallo toevoegen `AADB2C90118`. Bij het uitvoeren van Hallo "Registreren of aanmelden" beleid Hallo Hallo gebruiker Hallo kans tooselect heeft een **wachtwoord vergeten?** koppeling. In dit geval stuurt Azure AD B2C uw app die fout die aangeeft dat uw app moet worden gebruikt voor het aanbrengen van een aanvraag met beleid voor wachtwoordherstel Hallo in plaats daarvan.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Verificatie aanvragen tooAzure AD verzenden

Uw app is nu correct geconfigureerde toocommunicate met Azure AD B2C via Hallo OpenID Connect-verificatieprotocol. OWIN beheert Hallo details van verificatieberichten, het valideren van tokens van Azure AD B2C en het onderhoud van de gebruikerssessie. Alles wat blijft is tooinitiate van elke gebruiker stroom.

Wanneer een gebruiker selecteert **Sign up/aanmelden**, **profiel bewerken**, of **wachtwoord opnieuw instellen** in Hallo web-app, die zijn gekoppeld Hallo actie wordt aangeroepen in de `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

U kunt ook OWIN toosign uit Hallo gebruiker uit Hallo app gebruiken. In `Controllers\AccountController.cs` we hebben:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

In aanvulling tooexplicitly aanroepen van een beleid, kunt u een `[Authorize]` code in uw domeincontrollers die een beleid wordt uitgevoerd als Hallo gebruiker niet is aangemeld. Open `Controllers\HomeController.cs` en voeg Hallo `[Authorize]` tag toohello claims controller.  OWIN selecteert Hallo laatste beleid geconfigureerd wanneer hello `[Authorize]` tag is bereikt.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Gebruikersgegevens weergeven

Wanneer u gebruikers verifiëren met behulp van OpenID Connect, Azure AD B2C retourneert een ID token toohello app met **claims**. Dit zijn asserties over Hallo-gebruiker. Uw app kunt u claims toopersonalize gebruiken.

Open Hallo `Controllers\HomeController.cs` bestand. U hebt toegang tot gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

U hebt toegang tot een claim dat uw toepassing in Hallo dezelfde ontvangt manier.  Een lijst van alle Hallo claims Hallo app ontvangt is beschikbaar voor u op Hallo **Claims** pagina.
