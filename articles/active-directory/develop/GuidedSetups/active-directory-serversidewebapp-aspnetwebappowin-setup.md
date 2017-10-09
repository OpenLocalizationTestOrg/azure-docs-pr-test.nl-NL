---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - instellingen | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Instellen van uw project

Deze sectie toont Hallo stappen tooinstall en Hallo-verificatiepijplijn via OWIN middleware configureren op een ASP.NET-project met OpenID Connect. 

> Voorkeur toodownload dit voorbeeld Visual Studio-project in plaats daarvan? [Downloaden van een project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Uw ASP.NET-project maken

> 1. In Visual Studio:`File` > `New` > `Project`<br/>
> 2. Onder *Visual C# \Web*, selecteer `ASP.NET Web Application (.NET Framework)`.
> 3. Naam van uw toepassing en klik op *OK*
> 4. Selecteer `Empty` en selecteer Hallo selectievakje tooadd `MVC` verwijzingen
<!--end-collapse-->

## <a name="add-authentication-components"></a>Verificatieonderdelen toevoegen

1. In Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Voeg *OWIN middleware NuGet-pakketten* door Hallo volgende te typen in Hallo venster Package Manager Console:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Over deze bibliotheken

>Hallo bibliotheken bovenstaande Schakel eenmalige aanmelding (SSO) met OpenID Connect via authenticatie op basis van een cookie. Nadat de verificatie is voltooid en Hallo token die Hallo tooyour toepassing wordt verzonden, maakt OWIN middleware een sessiecookie. Hallo browser vervolgens gebruikt deze cookie op de volgende aanvragen zodat Hallo gebruiker niet tooretype hoeft hun wachtwoord en geen aanvullende verificatie nodig is.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Hallo-verificatiepijplijn configureren
Hallo onderstaande stappen zijn gebruikte toocreate een OWIN-middleware Opstartklasse tooconfigure OpenID Connect-authenticatie. Deze klasse wordt automatisch uitgevoerd wanneer uw IIS-proces wordt gestart.

> Als uw project beschikt niet over een `Startup.cs` bestand in de hoofdmap Hallo:<br/>
> 1. Klik met de rechtermuisknop op de hoofdmap van het project Hallo: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Geef deze de naam`Startup.cs`

> Zorg ervoor dat het Hallo-klasse die geselecteerd is een OWIN-Opstartklasse en niet een standaard C#-klasse. Dit controleren door te controleren of er `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` hierboven Hallo-naamruimte.


1. Voeg *OWIN* en *Microsoft.IdentityModel* verwijst naar te`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Vervang Opstartklasse met Hallo-code hieronder:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Meer informatie

> parameters die u opgeeft in Hallo *OpenIDConnectAuthenticationOptions* fungeren als coördinaten voor Hallo toepassing toocommunicate met Azure AD. Omdat Hallo OpenID Connect middleware gebruikmaakt van cookies op de achtergrond hello, moet u ook tooset van Cookieverificatie als Hallo code hierboven wordt weergegeven. Hallo *ValidateIssuer* waarde vertelt OpenIdConnect toonot toegang tooone specifieke organisatie beperken.
<!--end-collapse-->

