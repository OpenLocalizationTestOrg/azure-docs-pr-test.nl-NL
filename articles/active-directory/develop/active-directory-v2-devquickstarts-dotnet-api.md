---
title: aaaAdd aanmelden tooa .NET MVC-web-API met behulp van Azure AD v2.0-eindpunt Hallo | Microsoft Docs
description: Hoe toobuild een .NET MVC Web-Api die tokens van beide persoonlijke Microsoft-Account en werk-of schoolaccounts accepteert.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Een MVC-web-API beveiligen
U kunt met Azure Active Directory Hallo v2.0-eindpunt beveiligen een Web-API met [OAuth 2.0](active-directory-v2-protocols.md) toegangstokens, waardoor gebruikers met beide persoonlijke Microsoft-account en werk- of schoolaccount accounts toosecurely toegang tot uw Web-API.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

In ASP.NET web-API's, kunt u dit doen met behulp van Microsoft OWIN middleware is opgenomen in .NET Framework 4.5.  We gebruiken hier OWIN toobuild een 'tooDo lijst' MVC Web-API waarmee clients toocreate weergeven en lezen taken van de takenlijst van de gebruiker.  Hallo-web-API valideert dat inkomende aanvragen een ongeldig toegangstoken bevatten en alle aanvragen die niet zijn gevalideerd op een beveiligde route afwijzen.  Dit voorbeeld is gebouwd met behulp van Visual Studio 2015.

## <a name="download"></a>Downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

Hallo geraamte app omvat alle Hallo standaardcode voor een eenvoudige API, maar alle Hallo identity-gerelateerde onderdelen ontbreken. Als u toofollow langs niet wilt, kunt u in plaats daarvan klonen of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Een app registreren
Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.

Deze visual studio-oplossing bevat ook een 'TodoListClient', dit een eenvoudige WPF-app is.  Hallo TodoListClient gebruikte toodemonstrate hoe een gebruiker zich aanmeldt is en hoe u een client kan verlenen tooyour Web API-aanvragen.  In dit geval Hallo TodoListClient zowel Hallo TodoListService worden vertegenwoordigd door Hallo dezelfde app.  tooconfigure Hallo TodoListClient, moet u ook:

* Hallo toevoegen **Mobile** platform voor uw app.

## <a name="install-owin"></a>OWIN installeren
Nu u een app hebt geregistreerd, moet u tooset van uw app toocommunicate met Hallo v2.0-eindpunt in de volgorde toovalidate inkomende aanvragen & tokens.

* toobegin, open Hallo oplossing en Hallo OWIN middleware NuGet-pakketten toohello TodoListService-project toevoegen met behulp van Hallo Package Manager-Console.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>OAuth-verificatie configureren
* Voeg een OWIN klasse toohello TodoListService opstartproject aangeroepen `Startup.cs`.  Rechtermuisknop te klikken op op Hallo project--> **toevoegen** --> **Nieuw Item** --> Zoek naar 'OWIN'.  Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.
* Hallo klassendeclaratie ook wijzigen`public partial class Startup` -we hebben u al deel uit van deze klasse geïmplementeerd in een ander bestand.  In Hallo `Configuration(…)` methode, een aanroep van tooConfgureAuth(...) tooset van verificatie voor uw web-app maken.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(…)` methode die Hallo Web API tooaccept tokens van Hallo v2.0-eindpunt wordt ingesteld.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Nu kunt u `[Authorize]` tooprotect kenmerken uw domeincontrollers en de acties met OAuth 2.0-bearer-verificatie.  Hallo opmaken `Controllers\TodoListController.cs` klasse met een tag autoriseren.  Hierdoor moeten Hallo gebruiker toosign in voor de toegang tot deze pagina.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Wanneer een geautoriseerde beller is roept een Hallo `TodoListController` API's, Hallo actie mogelijk moet toegang tot tooinformation over Hallo aanroeper.  OWIN toegang toohello claims binnen Hallo bearer-token via Hallo levert `ClaimsPrincpal` object.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Tot slot opent Hallo `web.config` bestand in de hoofdmap Hallo van Hallo TodoListService project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.
  * Uw `ida:Audience` Hallo is **toepassings-Id** van Hallo-app die u hebt ingevoerd in Hallo-portal.

## <a name="configure-hello-client-app"></a>Hallo client-app configureren
Voordat u Hallo Todo List-Service in actie zien kunt, moet u tooconfigure Hallo Todo lijst Client, zodat het kan tokens van Hallo v2.0-eindpunt verkrijgen en aanroepen toohello service maken.

* Open in Hallo TodoListClient project `App.config` en voer de configuratiewaarden van uw in Hallo `<appSettings>` sectie.
  * Uw `ida:ClientId` toepassings-Id die u hebt gekopieerd uit Hallo-portal.

Ten slotte wilt opschonen, bouwen en uitvoeren van elk project!  U hebt nu een .NET MVC Web-API die tokens van beide persoonlijke Microsoft-accounts en werk-of schoolaccounts accepteert.  Meld u aan bij Hallo TodoListClient en roept u de takenlijst web api tooadd taken toohello van uw gebruikers.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Volgende stappen
U kunt nu verplaatsen naar andere onderwerpen.  U kunt tootry:

[Een Web-API aanroept vanuit een Web-App >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Voor aanvullende bronnen voor uitchecken:

* [Hallo v2.0 ontwikkelaarshandleiding >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow 'azure active directory'-tag >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.
