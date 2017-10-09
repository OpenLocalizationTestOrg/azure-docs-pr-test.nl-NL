---
title: Active Directory Authentication Libraries aaaAzure | Microsoft Docs
description: "Hello Azure AD Authentication Library (ADAL) kan client toepassingsontwikkelaars tooeasily toocloud gebruikers verifiëren of on-premises Active Directory (AD) en vervolgens verkrijgen toegangstokens voor het beveiligen van API-aanroepen."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Azure Active Directory-Verificatiebibliotheken
Hello Azure Active Directory Authentication Library (ADAL) kan client toepassing ontwikkelaars tooeasily toocloud gebruikers verifiëren of on-premises Active Directory (AD), en toegangstokens voor het beveiligen van API-aanroepen te verkrijgen. ADAL gemakkelijker verificatie voor ontwikkelaars via functies, zoals:
 - ondersteuning voor asynchrone methodeaanroepen
 - een configureerbare tokencache dat winkels tokens en vernieuw tokens
 - automatisch token vernieuwen wanneer een toegangstoken is verlopen en een vernieuwingstoken is beschikbaar
 - en meer
 
De meeste Hallo complexiteit kan verwerken, ADAL helpt ontwikkelaars zich richten op uw bedrijfslogica en resources, eenvoudig te beveiligen zonder een expert in de beveiliging.

ADAL is beschikbaar op verschillende platforms.

### <a name="client-libraries"></a>Clientbibliotheken

| Platform | Bibliotheek | Downloaden | Broncode | Voorbeeld | Naslaginformatie
| --- | --- | --- | --- | --- | --- |
| .NET-client, Windows Store UWP, Xamarin iOS en Android |MSAL voor .NET (preview) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Bureaublad-app](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Naslaginformatie](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| Javascript |MSAL voor JavaScript (preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [App met één pagina](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Naslaginformatie](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL voor iOS (preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS-app](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Naslaginformatie](https://azuread.github.io/docs/objc/) |
| Android |MSAL voor Android (preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android-app](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Naslaginformatie](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| .NET-client, Windows Store UWP, Xamarin iOS en Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Bureaublad-app](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Naslaginformatie](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET-client, Windows Store, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Bureaublad-app](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| Javascript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[App met één pagina](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| voor iOS, Mac OS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[iOS-app](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Naslaginformatie](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Hallo centrale opslagplaats](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Android-app](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Java-web-app](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Server-bibliotheken 

| Platform | Bibliotheek | Downloaden | Broncode | Voorbeeld | Naslaginformatie
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN voor AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[MVC-App](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN voor OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Web-app](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD-Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Web-API](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN voor WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[MVC-Web-App](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Identiteit Protocol-extensies voor .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |JWT-Handler voor .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Scenario's

Hier volgen drie gangbare scenario's waarin ADAL voor het verifiëren van een client die toegang heeft tot een externe bron kan worden gebruikt:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Gebruikers van een systeemeigen clienttoepassing uitgevoerd op een apparaat te verifiëren 

In dit scenario heeft een ontwikkelaar een clienttoepassing WPF die tooaccess een externe bron die is beveiligd door Azure AD, zoals een web-API behoeften. Hij heeft een Azure-abonnement, weet hoe tooinvoke Hallo downstream web-API en kent hello Azure AD-tenant die Hallo maakt gebruik van web-API. Hij kan als gevolg hiervan toofacilitate ADAL-verificatie met Azure AD gebruiken door volledig delegeren Hallo verificatie-ervaring tooADAL of expliciet afhandeling van gebruikersreferenties. ADAL maakt het eenvoudig tooauthenticate Hallo gebruiker, een toegangstoken en een vernieuwingstoken verkrijgen van Azure AD en gebruik vervolgens Hallo access token toomake aanvragen toohello web-API.

Zie voor een voorbeeld van code die u laat zien van dit scenario met verificatie tooAzure AD [systeemeigen clienttoepassing WPF tooWeb API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Verificatie van een vertrouwelijk clienttoepassing uitvoert op een webserver

In dit scenario heeft een ontwikkelaar een toepassing die wordt uitgevoerd op een server die tooaccess moet een externe bron die is beveiligd door Azure AD, zoals een web-API. Hij heeft een Azure-abonnement, weet hoe tooinvoke downstream service Hallo en kent hello Azure AD-tenant Hallo web-API wordt gebruikt. Hij kan als gevolg hiervan toofacilitate ADAL-verificatie gebruiken met Azure AD expliciet Hallo de referenties van toepassing kan verwerken. ADAL maakt het eenvoudig tooretrieve een token van Azure AD met behulp van de toepassing hello clientreferenties en gebruik vervolgens dat token toomake aanvragen toohello web API. ADAL ook ingangen beheren Hallo levensduur van Hallo toegangstoken door deze cache en vernieuwen van deze indien nodig. Zie voor een voorbeeld van code die u in dit scenario laat zien [Daemon console toepassing tooWeb API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Een vertrouwelijk clienttoepassing uitgevoerd op een server namens een gebruiker verifiëren 

In dit scenario heeft een ontwikkelaar een toepassing die wordt uitgevoerd op een server die tooaccess moet een externe bron die is beveiligd door Azure AD, zoals een web-API. Hallo-aanvraag moet ook toobe gedaan namens een Azure AD-gebruiker. Hij heeft een Azure-abonnement, weet hoe tooinvoke Hallo downstream web-API en kent hello Azure AD-tenant Hallo-service wordt gebruikt. Zodra gebruiker Hallo geverifieerde toohello webtoepassing, krijgen Hallo toepassing een autorisatiecode voor Hallo gebruiker van Azure AD. Vervolgens kunt Hallo webtoepassing ADAL tooobtain gebruiken een toegangstoken en een vernieuwingstoken namens een gebruiker met Hallo autorisatie code en de client de referenties die zijn gekoppeld aan de toepassing hello van Azure AD. Zodra het Hallo-webtoepassing is in bezit is van het toegangstoken Hallo, kan Hallo web-API aanroepen totdat het Hallo-token is verlopen. Wanneer Hallo-token is verlopen, kunt Hallo webtoepassing ADAL tooget een nieuw toegangstoken gebruiken met behulp van Hallo-vernieuwingstoken dat u eerder hebt ontvangen. Zie voor een voorbeeld van code die u in dit scenario laat zien [Native client tooWeb API tooWeb API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Zie ook

- [Hallo ontwikkelaarshandleiding Azure Active Directory](active-directory-developers-guide.md)
- [Verificatie-scenario's voor Azure Active directory](active-directory-authentication-scenarios.md)
- [Azure Active Directory-codevoorbeelden](active-directory-code-samples.md)
