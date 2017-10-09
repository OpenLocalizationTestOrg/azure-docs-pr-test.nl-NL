---
title: aaaAzure AD v2.0 .NET web-app aanroepen API aan de slag | Microsoft Docs
description: Hoe toobuild een Web-App voor .NET MVC-aanroepen van web-services met behulp van persoonlijke Microsoft-accounts en werk- of schoolaccounts voor aanmelden.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a>Een web-API aanroept vanuit een .NET-web-app
Met Hallo v2.0-eindpunt, kunt u snel toevoegen verificatie tooyour web-apps en web-API's met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccounts.  Wij je hier een MVC-web-app die gebruikers in het gebruik van het OpenID Connect, met hulp van Microsoft OWIN middleware ondertekent bouwen.  Hallo-web-app wordt OAuth 2.0-toegangstokens ophalen voor een web api is beveiligd met OAuth 2.0 waarmee maken, lezen en verwijderen op een bepaalde gebruiker 'takenlijst'.

Deze zelfstudie wordt voornamelijk over het gebruik van MSAL tooacquire richten en toegangstokens gebruiken in een web-app beschreven in de volledige [hier](active-directory-v2-flows.md#web-apps).  Als de vereisten, wilt u wellicht toofirst meer informatie over hoe te[basic aanmelden tooa web-app toevoegen](active-directory-v2-devquickstarts-dotnet-web.md) of hoe te[een web-API goed is beveiligd](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Voorbeeldcode downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

U kunt ook [Hallo voltooid app als een zip downloaden](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) of kloon voltooid Hallo app:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Een app registreren
Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.
* Maak een **App geheim** Hallo **wachtwoord** type en noteer de waarde voor later
* Hallo toevoegen **Web** platform voor uw app.
* Voer de juiste Hallo **omleidings-URI**. Hallo omleidings-uri geeft tooAzure AD waarbij verificatie antwoorden moeten worden omgeleid - Hallo standaardwaarde voor deze zelfstudie is `https://localhost:44326/`.

## <a name="install-owin"></a>OWIN installeren
Hallo OWIN middleware NuGet-pakketten toohello toevoegen `TodoList-WebApp` project met Hallo Package Manager-Console.  Hallo OWIN middleware gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Meld u Hallo gebruiker in
Nu configureren Hallo OWIN middleware toouse hello [OpenID Connect-verificatieprotocol](active-directory-v2-protocols.md).  

* Open Hallo `web.config` bestand in de hoofdmap Hallo Hallo `TodoList-WebApp` project en voer waarden in uw app-configuratie in Hallo `<appSettings>` sectie.
  * Hallo `ida:ClientId` Hallo is **toepassings-Id** tooyour-app in de portal voor registratie van Hallo toegewezen.
  * Hallo `ida:ClientSecret` Hallo is **App geheim** u hebt gemaakt in het Hallo-portal voor wachtwoordregistratie.
  * Hallo `ida:RedirectUri` Hallo is **omleidings-Uri** u hebt ingevoerd in het Hallo-portal.
* Open Hallo `web.config` bestand in de hoofdmap Hallo Hallo `TodoList-Service` project en vervang Hallo `ida:Audience` Hallo met dezelfde **toepassings-Id** zoals hierboven.
* Open Hallo bestand `App_Start\Startup.Auth.cs` en voeg `using` -instructies voor het Hallo-bibliotheken van hierboven.
* In hetzelfde bestand Hallo, Hallo implementeren `ConfigureAuth(...)` methode.  parameters die u opgeeft in Hallo `OpenIDConnectAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a>Toegangstokens voor MSAL tooget gebruiken
In Hallo `AuthorizationCodeReceived` melding, willen we toouse [OAuth 2.0 in combinatie met OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code voor een access token toohello taak List-Service.  MSAL kan dit proces toegankelijk maken voor u:

* Installeer eerst Hallo preview-versie van MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* En voeg een andere `using` instructie toohello `App_Start\Startup.Auth.cs` -bestand voor MSAL.
* Nu een nieuwe methode toevoegen, hello `OnAuthorizationCodeReceived` gebeurtenis-handler.  Deze handler MSAL tooacquire een access token toohello taak lijst API wordt gebruikt en Hallo token opgeslagen in de MSAL tokencache voor later:

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* MSAL heeft in web-apps, een uitbreidbaar tokencache die gebruikt toostore tokens worden kan.  Dit voorbeeld implementeert Hallo `NaiveSessionCache` waarvoor HTTP-sessie opslag toocache tokens worden gebruikt.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Hallo-Web-API aanroepen
Nu is het tijd tooactually hello access_token die u hebt verkregen in stap 3 gebruiken.  Open Hallo van web-app `Controllers\TodoListController.cs` bestand, waardoor alle Hallo CRUD toohello taak lijst API-aanvragen.

* U kunt MSAL opnieuw hier toofetch access_tokens van MSAL cache Hallo.  Voeg eerst een `using` -instructie voor MSAL toothis bestand.
  
    `using Microsoft.Identity.Client;`
* In Hallo `Index` van de actie, gebruik MSAL `AcquireTokenSilentAsync` methode tooget een access_token die gebruikt tooread gegevens van Hallo takenlijst-service worden kunnen:

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* Hallo voorbeeld vervolgens toegevoegd Hallo resulterende token toohello HTTP GET-aanvraag als Hallo `Authorization` -kop, welke service van de takenlijst Hallo tooauthenticate Hallo aanvraag gebruikt.
* Als Hallo takenlijst-service retourneert een `401 Unauthorized` antwoord Hallo access_tokens in MSAL niet meer geldig voor een bepaalde reden.  In dit geval moet u eventuele access_tokens niet verwijderen uit de Hallo MSAL cache en Hallo-gebruiker een bericht dat toosign moeten in, die wordt opnieuw gestart Hallo token overname stroom weergeven.

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* Op dezelfde manier als MSAL niet kan tooreturn een access_token om welke reden, moet u opdracht geven Hallo gebruiker toosign in opnieuw.  Dit is net zo eenvoudig als het afvangen van een `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Hallo exact dezelfde `AcquireTokenSilentAsync` aanroep is implementd in Hallo `Create` en `Delete` acties.  In de web-apps, kunt u deze MSAL methode tooget access_tokens wanneer u nodig hebt in uw app.  MSAL zorgt voor het ophalen, opslaan in cache en vernieuwen van tokens voor u.

Ten slotte bouwen en uitvoeren van uw app!  Meld u aan met een Microsoft-Account of een Azure AD-Account en zien hoe de identiteit van de gebruiker hello wordt weergegeven in de bovenste navigatiebalk Hallo.  Voeg toe en verwijder enkele items uit de takenlijst van de gebruiker Hallo toosee Hallo die OAuth 2.0 beveiligd API-in actie aanroepen.  U hebt nu een web-app & web-API beide beveiligd via standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [vindt u hier](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Volgende stappen
Voor aanvullende bronnen voor uitchecken:

* [Hallo v2.0 ontwikkelaarshandleiding >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow 'azure active directory'-tag >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

