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
## <a name="set-up-your-project"></a><span data-ttu-id="fc7fa-103">Instellen van uw project</span><span class="sxs-lookup"><span data-stu-id="fc7fa-103">Set up your project</span></span>

<span data-ttu-id="fc7fa-104">Deze sectie toont Hallo stappen tooinstall en Hallo-verificatiepijplijn via OWIN middleware configureren op een ASP.NET-project met OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="fc7fa-105">Voorkeur toodownload dit voorbeeld Visual Studio-project in plaats daarvan?</span><span class="sxs-lookup"><span data-stu-id="fc7fa-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="fc7fa-106">[Downloaden van een project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="fc7fa-107">Uw ASP.NET-project maken</span><span class="sxs-lookup"><span data-stu-id="fc7fa-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="fc7fa-108">In Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="fc7fa-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="fc7fa-109">Onder *Visual C# \Web*, selecteer `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="fc7fa-110">Naam van uw toepassing en klik op *OK*</span><span class="sxs-lookup"><span data-stu-id="fc7fa-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="fc7fa-111">Selecteer `Empty` en selecteer Hallo selectievakje tooadd `MVC` verwijzingen</span><span class="sxs-lookup"><span data-stu-id="fc7fa-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="fc7fa-112">Verificatieonderdelen toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc7fa-112">Add authentication components</span></span>

1. <span data-ttu-id="fc7fa-113">In Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="fc7fa-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="fc7fa-114">Voeg *OWIN middleware NuGet-pakketten* door Hallo volgende te typen in Hallo venster Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="fc7fa-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="fc7fa-115">Over deze bibliotheken</span><span class="sxs-lookup"><span data-stu-id="fc7fa-115">About these libraries</span></span>

><span data-ttu-id="fc7fa-116">Hallo bibliotheken bovenstaande Schakel eenmalige aanmelding (SSO) met OpenID Connect via authenticatie op basis van een cookie.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="fc7fa-117">Nadat de verificatie is voltooid en Hallo token die Hallo tooyour toepassing wordt verzonden, maakt OWIN middleware een sessiecookie.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="fc7fa-118">Hallo browser vervolgens gebruikt deze cookie op de volgende aanvragen zodat Hallo gebruiker niet tooretype hoeft hun wachtwoord en geen aanvullende verificatie nodig is.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="fc7fa-119">Hallo-verificatiepijplijn configureren</span><span class="sxs-lookup"><span data-stu-id="fc7fa-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="fc7fa-120">Hallo onderstaande stappen zijn gebruikte toocreate een OWIN-middleware Opstartklasse tooconfigure OpenID Connect-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="fc7fa-121">Deze klasse wordt automatisch uitgevoerd wanneer uw IIS-proces wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="fc7fa-122">Als uw project beschikt niet over een `Startup.cs` bestand in de hoofdmap Hallo:</span><span class="sxs-lookup"><span data-stu-id="fc7fa-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="fc7fa-123">Klik met de rechtermuisknop op de hoofdmap van het project Hallo: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="fc7fa-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="fc7fa-124">Geef deze de naam`Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="fc7fa-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="fc7fa-125">Zorg ervoor dat het Hallo-klasse die geselecteerd is een OWIN-Opstartklasse en niet een standaard C#-klasse.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="fc7fa-126">Dit controleren door te controleren of er `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` hierboven Hallo-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="fc7fa-127">Voeg *OWIN* en *Microsoft.IdentityModel* verwijst naar te`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="fc7fa-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="fc7fa-128">Vervang Opstartklasse met Hallo-code hieronder:</span><span class="sxs-lookup"><span data-stu-id="fc7fa-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="fc7fa-129">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="fc7fa-129">More Information</span></span>

> <span data-ttu-id="fc7fa-130">parameters die u opgeeft in Hallo *OpenIDConnectAuthenticationOptions* fungeren als coördinaten voor Hallo toepassing toocommunicate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="fc7fa-131">Omdat Hallo OpenID Connect middleware gebruikmaakt van cookies op de achtergrond hello, moet u ook tooset van Cookieverificatie als Hallo code hierboven wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="fc7fa-132">Hallo *ValidateIssuer* waarde vertelt OpenIdConnect toonot toegang tooone specifieke organisatie beperken.</span><span class="sxs-lookup"><span data-stu-id="fc7fa-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

