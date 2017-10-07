---
title: aaaAzure Active Directory v2.0-verificatiebibliotheken | Microsoft Docs
description: Compatibel clientbibliotheken en server middleware bibliotheken en -gerelateerde bibliotheek, bron en voorbeelden koppelingen voor hello Azure Active Directory v2.0-eindpunt.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Azure Active Directory-verificatiebibliotheken voor v2.0
Hello Azure Active Directory (Azure AD) v2.0-eindpunt ondersteunt Hallo industriestandaard OAuth 2.0 als OpenID Connect 1.0-protocol. U kunt verschillende bibliotheken van Microsoft en andere organisaties met Hallo v2.0-eindpunt.

Wanneer u een toepassing die gebruikmaakt van Hallo v2.0-eindpunt maakt, wordt aangeraden dat u bibliotheken die zijn geschreven door protocol domein experts die een methodologie Security Development Lifecycle (SDL) zoals volgen [Hallo een gevolgd door Microsoft] [Microsoft-SDL]. Als u toohand code ondersteuning voor Hallo protocollen besluit, wordt aangeraden SDL methodologie volgen en aandacht besteedt toohello beveiligingsoverwegingen in Hallo standaarden specificaties voor elk protocol.

## <a name="types-of-libraries"></a>Typen bibliotheken
Azure AD v2.0 werkt met twee soorten bibliotheken:

* **Clientbibliotheken**. Systeemeigen clients en servers gebruiken client bibliotheken tooget toegangstokens voor het aanroepen van een resource, zoals Microsoft Graph.
* **Server middleware bibliotheken**. Web-apps gebruiken server middleware bibliotheken voor gebruikersaanmelding. Web-API's gebruiken server middleware bibliotheken toovalidate tokens die zijn verzonden door de systeemeigen clients of andere servers.

## <a name="library-support"></a>Bibliotheek-ondersteuning
Omdat u kunt alle standaarden compatibele bibliotheek kiezen kunt wanneer u Hallo v2.0-eindpunt, is het belangrijk tooknow waar toogo voor ondersteuning. Neem contact op met Hallo bibliotheek eigenaar voor problemen en functie-aanvragen in de bibliotheek-code. Neem contact op met Microsoft voor problemen en functieaanvragen in Hallo aan servicezijde protocolimplementatie.

Bibliotheken zijn twee categorieën van ondersteuning:

* **Microsoft ondersteunde**. Microsoft biedt oplossingen voor deze bibliotheken en SDL heeft gedaan innen op deze bibliotheken.
* **Compatibel**. Microsoft heeft getest deze bibliotheken in basisscenario's en bevestigd dat ze met Hallo v2.0-eindpunt werken. Microsoft biedt geen oplossingen voor deze bibliotheken en een overzicht van deze bibliotheken niet uitgevoerd. Problemen en functie-aanvragen moeten gerichte toohello-bibliotheek open source-project.

Zie voor een lijst met bibliotheken die met het v2.0-eindpunt Hallo werken Hallo volgende secties in dit artikel.


## <a name="microsoft-supported-client-libraries"></a>Microsoft ondersteunde clientbibliotheken

> [!IMPORTANT]
> Hallo MSAL preview bibliotheken zijn geschikt voor gebruik in een productieomgeving. We bieden dezelfde productie-ondersteuning voor deze bibliotheken Hallo zoals wij onze huidige productie-bibliotheken (ADAL doen). Tijdens de preview Hallo mogelijk maken we wijzigingen toohello MSAL API, indeling van de interne cache, en andere mechanismen van deze bibliotheken zonder voorafgaande kennisgeving, wat u zult nodig tootake samen met oplossingen voor problemen of verbeterde functies. Dit mogelijk invloed op uw toepassing. Bijvoorbeeld, kan een wijziging toohello cache-indeling van uw gebruikers, zoals het vereisen dat ze toosign in opnieuw invloed. Een wijziging in de API kan tooupdate u uw code nodig. Wanneer wij algemene beschikbaarheid release is verplicht tooupdate toohello algemene beschikbaarheid versie binnen zes maanden hello bieden, als toepassingen die zijn geschreven met behulp van een preview werkt-versie van de bibliotheek niet meer.

| Platform | Bibliotheek | Downloaden | Broncode | Voorbeeld | Naslaginformatie
| --- | --- | --- | --- | --- | --- |
| .NET-client, Windows Store UWP, Xamarin iOS en Android | MSAL .NET (Preview) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Bureaublad-App](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| Javascript | MSAL.js (Preview) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [App met één pagina](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| voor iOS, Mac OS | MSAL (Preview) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS-App](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (Preview) | [Hallo centrale opslagplaats](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android-App](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Microsoft ondersteund server middleware bibliotheken

| Platform | Bibliotheek | Downloaden | Broncode | Voorbeeld | Naslaginformatie
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | OWIN OpenID Connect middleware |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[MVC-App](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | OWIN OAuth Bearer-middleware voor AzureAD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | JWT-Handler voor .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | ASP.NET-middleware OpenID Connect |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[ASP.NET-beveiliging (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[MVC-app](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | OAuth-Bearer-middleware voor ASP.NET |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[ASP.NET-beveiliging (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | JWT-Handler voor .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD-Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Web-app](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Compatibel clientbibliotheken
| Platform | Bibliotheeknaam | Geteste versie | Broncode | Voorbeeld |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Voorbeeld van de systeemeigen app](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Voorbeeld van de systeemeigen app](active-directory-v2-devquickstarts-ios.md) |
| Javascript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Compatibele server middleware bibliotheken
| Platform | Bibliotheeknaam | Geteste versie | Broncode | Voorbeeld |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Notulist Java scribejava](https://github.com/scribejava/scribejava) | [Versie 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Hallo PHP League oauth2-client](https://github.com/thephpleague/oauth2-client) | [1.4.2 versie](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python Flask |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |[Web-app](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Gerelateerde inhoud
Zie voor meer informatie over hello Azure AD v2.0-eindpunt Hallo [overzicht van Azure AD app model v2.0][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
