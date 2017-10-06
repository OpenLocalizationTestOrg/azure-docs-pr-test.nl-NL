---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een .NET-Web-app en roept u een web api met Azure Active Directory B2C en OAuth 2.0-toegangstokens.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: Een .NET web API aanroepen vanuit een .NET-web-app

Met behulp van Azure AD B2C, kunt u krachtige identity management-functies tooyour web-apps en web-API's kunt toevoegen. Dit artikel wordt beschreven hoe toorequest toegang tot tokens en aanroepen vanuit een .NET 'takenlijst' web-app tooa .NET web-api.

Dit artikel wordt niet beschreven hoe tooimplement aanmelden, registreren en de profiel-beheer met Azure AD B2C. Dit artikel gaat over het aanroepen van web API's nadat Hallo gebruiker al is geverifieerd. Als u nog niet gedaan hebt, moet u het volgende doen:

* Aan de slag met een [.NET-web-app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Aan de slag met een [.NET web-api](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Vereiste

toobuild een webtoepassing die een web aanroept-api, moet u:

1. [Een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).
2. [Registreren van een web api](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Een web-app registreren](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Instellen van het beleid](active-directory-b2c-reference-policies.md).
5. [Verleen Hallo web app machtigingen toouse Hallo web-api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> Hallo-clienttoepassing en web-API moeten Hallo dezelfde Azure AD B2C-directory gebruiken.
>

## <a name="download-hello-code"></a>Hallo code downloaden

Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). U kunt Hallo voorbeeld klonen door te voeren:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart. Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`. `TaskWebApp`is een MVC-webtoepassing die gebruiker Hallo communiceert met. `TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is. In dit artikel omvat niet gebouw Hallo `TaskWebApp` web-app of Hallo `TaskService` web-api. toolearn hoe toobuild Hallo .NET web-app met Azure AD B2C, Zie onze [.NET web app-zelfstudie](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn hoe toobuild Hallo .NET web-API is beveiligd met Azure AD B2C, Zie onze [.NET-web-API-zelfstudie](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Hello Azure AD B2C-configuratie bijwerken

Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant. Als u toouse wilt uw eigen tenant:

1. Open `web.config` in Hallo `TaskService` project en vervang de waarden voor Hallo

    * `ida:Tenant` door de naam van uw tenant
    * `ida:ClientId`met de toepassings-ID van uw web-api
    * `ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid

2. Open `web.config` in Hallo `TaskWebApp` project en vervang de waarden voor Hallo

    * `ida:Tenant` door de naam van uw tenant
    * `ida:ClientId` door de id van uw web-app-toepassing
    * `ida:ClientSecret` door de geheime sleutel voor uw web-app
    * `ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid
    * `ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid
    * `ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid



## <a name="requesting-and-saving-an-access-token"></a>Aanvragen en het opslaan van een toegangstoken

### <a name="specify-hello-permissions"></a>Hallo machtigingen opgeven

In de volgorde toomake Hallo aanroep toohello web-API, moet u tooauthenticate Hallo gebruiker (met behulp van uw beleid sign-up-to-date/aanmelden) en [ontvangen van een toegangstoken](active-directory-b2c-access-tokens.md) van Azure AD B2C. In de volgorde tooreceive een toegangstoken, moet u eerst Hallo machtigingen die u wilt dat Hallo access token toogrant opgeven. Hallo machtigingen zijn opgegeven in Hallo `scope` parameter wanneer u Hallo aanvraag toohello `/authorize` eindpunt. Bijvoorbeeld, een toegangstoken Hello 'lezen' machtiging toohello resource-toepassing met tooacquire App ID URI van Hallo `https://contoso.onmicrosoft.com/tasks`, Hallo bereik zou worden `https://contoso.onmicrosoft.com/tasks/read`.

toospecify hello bereik in ons voorbeeld, open Hallo-bestand `App_Start\Startup.Auth.cs` en definieer Hallo `Scope` variabele in OpenIdConnectAuthenticationOptions.

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Exchange Hallo autorisatiecode voor een toegangstoken

Nadat een gebruiker is voltooid Hallo registreren of aanmelden ervaring, ontvangt de app een autorisatiecode van Azure AD B2C. Hallo OWIN OpenID Connect middleware Hallo code wordt opgeslagen, maar niet voor een toegangstoken exchange. U kunt Hallo [MSAL bibliotheek](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake Hallo exchange. In ons voorbeeld geconfigureerde een callback van querymelding in Hallo OpenID Connect middleware wanneer een autorisatiecode wordt ontvangen. In Hallo-retouraanroep we MSAL tooexchange Hallo code gebruiken voor een token en Hallo-token in Hallo cache op te slaan.

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a>Hallo-web-API aanroepen

Deze sectie wordt beschreven hoe toouse Hallo token ontvangen tijdens sign-up-to-date/aanmelden met Azure AD B2C in volgorde Hallo tooaccess web-API.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Het ophalen van Hallo opgeslagen token in Hallo-domeincontrollers

Hallo `TasksController` verantwoordelijk is voor communicatie met de Hallo web-API en voor het verzenden van HTTP-aanvragen toohello API tooread maken en verwijderen van taken. Omdat Hallo API is beveiligd door Azure AD B2C, moet u token toofirst ophalen Hallo die u hebt opgeslagen in Hallo bovenstaande stap.

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a>Lezen van de taken van Hallo web-API

Wanneer u een token hebt, kunt u koppelen het toohello HTTP `GET` aanvraag in Hallo `Authorization` header toosecurely aanroep `TaskService`:

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Maken en verwijderen van taken op Hallo web-API

Volg Hallo hetzelfde patroon bij het verzenden van `POST` en `DELETE` MSAL tooretrieve Hallo-toegangstoken uit Hallo cache toohello-web-API-aanvragen kan gebruiken.

## <a name="run-hello-sample-app"></a>Hallo voorbeeld-app uitvoeren

Ten slotte bouwen en uitvoeren van beide Hallo-apps. Aanmelden en meld u aan en maak taken voor Hallo aangemelde gebruiker. Meld u af en meld u aan als een andere gebruiker. Taken voor die gebruiker maken. U ziet hoe Hallo taken worden opgeslagen per gebruiker op Hallo API, omdat Hallo API de identiteit van de gebruiker Hallo haalt uit Hallo-token die wordt ontvangen. U kunt ook met Hallo scopes speelt. Verwijder de machtigingen voor hello te 'schrijven' en probeer het toevoegen van een taak. Zorg ervoor dat toosign uit telkens wanneer die u Hallo bereik wijzigen.

