---
title: aaaAzure AD B2C | Microsoft Docs
description: Hoe toobuild een .NET-Web-API met behulp van Azure Active Directory B2C, beveiligd met OAuth 2.0-toegangstokens voor verificatie.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: een .NET-web-API maken

Met Azure Active Directory (Azure AD) B2C kunt u een web-API beveiligen met OAuth 2.0-toegangstokens. Deze tokens kunnen uw client-apps tooauthenticate toohello API. Dit artikel laat zien hoe een .NET MVC-API 'takenlijst' toocreate die kunnen gebruikers van uw toepassing tooCRUD taken. Hallo-web-API is beveiligd met Azure AD B2C en alleen hun takenlijst kan toomanage geverifieerde gebruikers.

## <a name="create-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken

Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken. Een directory is een container voor alle gebruikers, apps, groepen en meer. Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.

> [!NOTE]
> Hallo-clienttoepassing en web-API moeten Hallo dezelfde Azure AD B2C-directory gebruiken.
>

## <a name="create-a-web-api"></a>Een web-API maken

Vervolgens moet u een web API-app toocreate in uw B2C-directory. Hiermee geeft u Azure AD-informatie of deze behoeften toosecurely met uw app communiceren. toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md). Zorg ervoor dat:

* Omvatten een **web-app** of **web-API** in Hallo-toepassing.
* Gebruik Hallo **omleidings-URI** `https://localhost:44332/` voor Hallo web-app. Dit is de standaardlocatie Hallo van Hallo web app-client voor dit codevoorbeeld.
* Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. U hebt deze later nodig.
* Voer een app-id **URI voor de app-id** in.
* Machtigingen via Hallo toevoegen **gepubliceerd scopes** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken

In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). U moet toocreate een toocommunicate beleid met Azure AD B2C. Het is raadzaam met behulp van Hallo gecombineerd sign-up-to-date/aanmelden beleid, zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md). Wanneer u het beleid maakt, vergeet dan niet het volgende:

* Kies een **Weergavenaam** en andere registratiekenmerken in uw beleid.
* Kiest u **Weergavenaam**- en **Object-id**-claims als toepassingsclaims voor elk beleid. U kunt ook andere claims kiezen.
* Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt. U hebt de beleidsnaam hello later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u Hallo beleid hebt gemaakt, bent u klaar toobuild uw app.

## <a name="download-hello-code"></a>Hallo code downloaden

Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). U kunt Hallo voorbeeld klonen door te voeren:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart. Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`. `TaskWebApp`is een MVC-webtoepassing die gebruiker Hallo communiceert met. `TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is. In dit artikel wordt alleen besproken Hallo `TaskService` toepassing. toolearn hoe toobuild `TaskWebApp` met behulp van Azure AD B2C, Zie [onze zelfstudie .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Hello Azure AD B2C-configuratie bijwerken

Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant. Als u toouse wilt uw eigen tenant, moet u toodo hello te volgen:

1. Open `web.config` in Hallo `TaskService` project en vervang de waarden voor Hallo
    * `ida:Tenant` door de naam van uw tenant
    * `ida:ClientId` door de id van uw web-API-toepassing
    * `ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid

2. Open `web.config` in Hallo `TaskWebApp` project en vervang de waarden voor Hallo
    * `ida:Tenant` door de naam van uw tenant
    * `ida:ClientId` door de id van uw web-app-toepassing
    * `ida:ClientSecret` door de geheime sleutel voor uw web-app
    * `ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid
    * `ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid
    * `ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid


## <a name="secure-hello-api"></a>Hallo-API beveiligen

Wanneer u een client hebt die de API aanroept, kunt u uw API (bijv. `TaskService`) beveiligen met Bearer-tokens van OAuth 2.0. Dit zorgt ervoor dat elke aanvraag tooyour API worden pas geldig als het Hallo-aanvraag heeft een bearer-token. De API kan Bearer-tokens accepteren en valideren met behulp van de Microsoft Open Web Interface voor .NET-bibliotheek (OWIN).

### <a name="install-owin"></a>OWIN installeren

Beginnen met het Hallo OWIN OAuth-verificatiepijplijn installeren met behulp van Hallo Visual Studio Package Manager-Console.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Hiermee installeert u Hallo OWIN middleware waarmee accepteert en bearer-tokens te valideren.

### <a name="add-an-owin-startup-class"></a>Een OWIN-opstartklasse toevoegen

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

### <a name="configure-oauth-20-authentication"></a>OAuth 2.0-verificatie configureren

Open Hallo bestand `App_Start\Startup.Auth.cs`, en implementeren van Hallo `ConfigureAuth(...)` methode. Bijvoorbeeld, eruit het volgende Hallo:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Hallo taakcontroller beveiligen

Zodra Hallo app geconfigureerde toouse OAuth 2.0-verificatie, kunt u uw web-API beveiligen door het toevoegen van een `[Authorize]` tag toohello taakcontroller. Dit is Hallo controller waarop alle bewerkingen van de takenlijst uitgevoerd, worden dus moet u de hele controller Hallo op Hallo klasseniveau beveiligen. U kunt ook toevoegen Hallo `[Authorize]` tag tooindividual acties voor nauwkeuriger beheer.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Gebruikersgegevens uit Hallo-token ophalen

`TasksController`slaat taken in een database waarin elke taak een gekoppelde gebruiker die 'eigenaar' hello taak heeft. Hallo eigenaar wordt geïdentificeerd met van Hallo gebruiker **object-ID**. (Dit is de reden waarom u tooadd Hallo object-ID als een toepassing nodig toepassingsclaim in al uw beleidsregels.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Hallo machtigingen in Hallo token valideren

Een algemene vereiste voor web-API's is toovalidate Hallo 'scopes' Hallo token aanwezig. Dit zorgt ervoor dat die gebruiker Hallo heeft ingestemd toohello machtigingen vereist tooaccess Hallo taak list-service.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Hallo voorbeeld-app uitvoeren

Bouw ten slotte `TaskWebApp` en `TaskService` en voer deze uit. Sommige taken in de takenlijst van de gebruiker Hallo maken en u ziet hoe ze worden doorgevoerd in Hallo API zelfs na het stoppen en het Hallo-client opnieuw te starten.

## <a name="edit-your-policies"></a>Het beleid bewerken

Nadat u een API hebt beveiligd met behulp van Azure AD B2C, kunt u experimenteren met uw Sign-in/Sign-up-to-date beleid en het Hallo-effecten weergeven (of ontbreken daarvan) op Hallo API. U kunt toepassingsclaims voor Hallo Hallo beleidsregels bewerken en Hallo gebruikersgegevens die beschikbaar is in Hallo web-API wijzigen. Claims die u toevoegt worden beschikbaar tooyour .NET MVC web-API in Hallo `ClaimsPrincipal` object, zoals eerder in dit artikel is beschreven.
