---
title: aaaAzure Active Directory-codevoorbeelden | Microsoft Docs
description: Een index van Azure Active Directory-codevoorbeelden, onderverdeeld op basis van scenario.
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Azure Active Directory-codevoorbeelden
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

U kunt gebruiken van Microsoft Azure Active Directory (Azure AD) tooadd verificatie en autorisatie tooyour webtoepassingen en web-API's. Deze sectie koppelt u toosamples waarin u kunt zien hoe deze wordt uitgevoerd en codefragmenten die u in uw toepassingen gebruiken kunt. Op Hallo code voorbeeldpagina vindt u gedetailleerde lezen-mij onderwerpen die u bij de vereisten, installatie en configuratie helpen. En Hallo code opmerkingen toohelp u essentiële secties Hallo begrijpen is.

toounderstand hello basisscenario voor elk Voorbeeldtype Zie verificatie scenario's voor Azure AD.

Bijdragen tooour voorbeelden op GitHub: [Microsoft Azure Active Directory-voorbeelden en documentatie](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Web Browser tooWeb toepassing
Deze voorbeelden laten zien hoe een webtoepassing waarin wordt verwezen toowrite van gebruiker browser toosign Hallo ze in tooAzure AD.

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| C# / .NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Gebruik OpenID Connect (middleware ASP.Net OpenID Connect OWIN) tooauthenticate gebruikers van een Azure AD-tenant. |
| C# / .NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Een multitenant .NET MVC-webtoepassing die gebruikmaakt van OpenID Connect (middleware ASP.Net OpenID Connect OWIN) tooauthenticate gebruikers van meerdere Azure AD-tenants. |
| C# / .NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Gebruik van WS-Federation (middleware ASP.Net WS-Federation OWIN) tooauthenticate gebruikers van een Azure AD-tenant. |

## <a name="single-page-application-spa"></a>Toepassing van één pagina (SPA)
Dit voorbeeld ziet u hoe toowrite een toepassing met één pagina beveiligd met Azure AD.  

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| JavaScript, C# / .NET |[SinglePageApp DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Gebruikmaken van ADAL voor JavaScript en Azure AD toosecure een AngularJS op basis van één pagina app geïmplementeerd met een ASP.NET-web-API back-end. |

## <a name="native-application-tooweb-api"></a>Systeemeigen toepassing tooWeb API
Deze codevoorbeelden laten zien hoe toobuild systeemeigen clienttoepassingen die aanroepen van web-API's die zijn beveiligd door Azure AD. Ze gebruiken [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) en [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| Javascript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Hallo ADAL-invoegtoepassing voor Apache Cordova-toobuild een Apache Cordova-app die een web-API aanroept en Azure AD gebruikt voor verificatie gebruiken. |
| C# / .NET |[NativeClient DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Een .NET WPF-toepassing die een web-API-die aanroepen is beveiligd met Azure AD. |
| C# / .NET |[NativeClient WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Een Windows Store-toepassing die een web-API-die aanroepen is beveiligd met Azure AD. |
| C# / .NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Een Windows Store-toepassing voor het aanroepen van een multitenant-web-API die is beveiligd met Azure AD. |
| C# / .NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Een native client-toepassing die een web-API aanroept die een token tooact namens de oorspronkelijke gebruiker Hallo ontvangt, en gebruikt vervolgens Hallo token toocall een andere web-API. |
| C# / .NET |[NativeClient WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Een Windows Store-toepassing voor Windows Phone 8.1 die een web-API-die aanroepen wordt beveiligd door Azure AD. |
| ObjC |[NativeClient iOS](https://github.com/Azure-Samples/active-directory-ios) |Een iOS-toepassing die een web-API-die aanroepen vereist Azure AD voor verificatie. |
| C# / .NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Een systeemeigen clienttoepassing waarin logica tooprocess JWT-token in een web-API, in plaats van OWIN middleware. |
| C# / Xamarin |[NativeClient Xamarin.android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Een Xamarin binding toohello systeemeigen Azure AD Authentication Library (ADAL) voor Hallo Android-bibliotheek. |
| C# / Xamarin |[IOS-Xamarin-NativeClient](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Een Xamarin binding toohello systeemeigen Azure AD Authentication Library (ADAL) voor iOS. |
| C# / Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Een Xamarin-project dat gericht is op vijf platforms en een web-API-aanroepen die wordt beveiligd door Azure AD. |
| C# / .NET |[NativeClient Headless DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Een systeemeigen toepassing die niet-interactieve verificatie uitvoert en een web-API-aanroepen die wordt beveiligd door Azure AD. |

## <a name="web-application-tooweb-api"></a>Web Application tooWeb API
Deze codevoorbeelden tonen hoe gebruiken [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild webtoepassingen die aanroepen van web-API's die zijn beveiligd door Azure AD.

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| C# / .NET |[WebApp WebAPI-OpenIDConnect DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Een web-API met Hallo aangemelde gebruikersmachtigingen aanroepen. |
| C# / .NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Een web-API met Hallo Toepassingsmachtigingen aanroepen. |
| C# / .NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Toevoegen van de autorisatie met [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan bestaande webtoepassing zodat een web-API kan aanroepen. |
| Javascript |[WebAPI Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Instellen van een REST-API-service die geïntegreerd met Azure AD voor API-beveiliging. Bevat een Node.js-server met een Web-API. |
| C# / .NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Een multitenant MVC-webtoepassing die gebruikmaakt van OpenID Connect (middleware ASP.Net OpenID Connect OWIN) tooauthenticate gebruikers van een Azure AD-tenant. Maakt gebruik van een vergunning code tooinvoke Hallo Graph API. |

## <a name="server-or-daemon-application-tooweb-api"></a>Server of toepassing Daemon tooWeb API
Deze codevoorbeelden ziet u hoe een daemon toobuild of servertoepassing die resources van een web-API met behulp van krijgt [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) en [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| C# / .NET |[Daemon DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Een consoletoepassing aanroept een web-API. Hallo-clientreferenties is een wachtwoord. |
| C# / .NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Een consoletoepassing die een web-API aanroept. Hallo-clientreferenties is een certificaat. |

## <a name="calling-azure-ad-graph-api"></a>Azure AD Graph API aanroepen
Deze voorbeeldcode ziet u hoe toobuild toepassingen die aanroepen hello Azure AD Graph API tooread en write directorygegevens.

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| Java |[GraphAPI-Java-Web-App](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Een webtoepassing die gebruikmaakt van Hallo Graph API tooaccess Azure AD-directory-gegevens. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Een webtoepassing die gebruikmaakt van Hallo Graph API tooaccess Azure AD-directory-gegevens. |
| C# / .NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Een webtoepassing die gebruikmaakt van Hallo Graph API tooaccess Azure AD-directory-gegevens. |
| C# / .NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Deze console-app toont de algemene lezen en schrijven aanroepen-toohello Graph API en ziet u hoe de gebruiker tooexecute licentie-toewijzing en bijwerken van een gebruiker een foto van miniatuurformaat en koppelingen. |
| C# / .NET |[ConsoleApp GraphAPI-DiffQuery DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Een consoletoepassing die gebruikmaakt van Hallo differentiële query in Hallo Graph API tooget periodieke wijzigingen toouser objecten in een Azure AD-tenant. |
| C# / .NET |[WebApp GraphAPI-DirectoryExtensions DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Graph API-query's toogenerate een organigram eenvoudige bedrijf maakt gebruik van een MVC-toepassing. |
| PHP |[WebApp GraphAPI-DirectoryExtensions PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Een PHP-toepassing hello Graph API tooregister roept een uitbreiding en vervolgens lezen, bijwerken en verwijderen van waarden in het Hallo-extensie-kenmerk. |

## <a name="authorization"></a>Autorisatie
Deze voorbeelden tonen hoe code toouse Azure AD voor autorisatie.

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| C# / .NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Uitvoeren op rollen gebaseerd-toegangsbeheer (RBAC) met behulp van Azure Active Directory-groepclaims in een toepassing die is geïntegreerd met Azure AD. |
| C# / .NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Uitvoeren op rollen gebaseerd toegangsbeheer (RBAC) op met behulp van de rollen van de Azure Active Directory-toepassing in een toepassing die is geïntegreerd met Azure AD. |

## <a name="legacy-walkthroughs"></a>Verouderde scenario 's
Deze scenario's enigszins oudere technologie gebruiken, maar nog steeds mogelijk van belang.

| Taal/Platform | Voorbeeld | Beschrijving |
| --- | --- | --- |
| C# / .NET |[Op basis van rollen en op basis van ACL-verificatie in een Microsoft Azure AD-toepassing](http://go.microsoft.com/fwlink/?LinkId=331694) |Op basis van rollen autorisatie (RBAC) en op basis van ACL uitvoeren in een toepassing die is geïntegreerd met Azure AD. |
| C# / .NET |[AAL - service voor Windows Store-app tooREST - verificatie](http://go.microsoft.com/fwlink/?LinkId=330605) |Gebruik [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) (voorheen AAL) voor Windows Store Beta tooadd gebruiker authentication mogelijkheden tooa Windows Store-app. |
| C# / .NET |[ADAL - systeemeigen App tooREST service - verificatie met AAD via het bladerdialoogvenster](http://go.microsoft.com/fwlink/?LinkId=259814) |Gebruik [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) tooadd gebruiker authentication mogelijkheden tooa WPF-client. |
| C# / .NET |[ADAL - systeemeigen App tooREST service - verificatie met ACS via het bladerdialoogvenster](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Gebruik [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) en [Access Control Service 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd gebruiker authentication mogelijkheden tooa WPF-client. |
| C# / .NET |[ADAL - Server tooServer verificatie](http://go.microsoft.com/fwlink/?LinkId=259816) |Gebruik [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) toosecure serviceaanroepen vanuit een server side proces tooan MVC4 Web API REST-service. |
| C# / .NET |[Toevoegen van aanmelding tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configureer een .NET-toepassing tooperform web eenmalige aanmelding op basis van uw Azure AD-directory enterprise. |
| C# / .NET |[Ontwikkeling van Multitenant-webtoepassingen met Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Gebruik Azure AD tooadd toohello eenmalige aanmelding en directory toegangsmogelijkheden van één toowork voor .NET-toepassing in meerdere organisaties. |
| JAVA |[Java-voorbeeld-App voor Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkId=263969) |Gebruik Hallo tooaccess directory Graph API-gegevens van Azure AD. |
| PHP |[PHP-voorbeeld-App voor Azure AD Graph API](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Gebruik Hallo tooaccess directory Graph API-gegevens van Azure AD. |
| C# / .NET |[Voorbeeld-App voor Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkID=262648) |Gebruik Hallo tooaccess directory Graph API-gegevens van Azure AD. |
| C# / .NET |[Voorbeeld-App voor Azure AD Graph differentiële Query](http://go.microsoft.com/fwlink/?LinkId=275398) |Gebruik de differentiële query Hallo Hallo Graph API tooget periodieke wijzigingen toouser objecten in een Azure AD-tenant. |
| C# / .NET |[Voorbeeld-App voor het integreren van Multitenant Cloudtoepassing voor Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Een toepassing met meerdere tenants integreren met Azure AD. |
| C# / .NET |[Beveiligen van een Windows Store-toepassing en de REST-webservice met behulp van Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Maak een eenvoudige web-API-resource en een Windows Store-clienttoepassing die gebruikmaken van Azure AD en Hallo [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md). |
| C# / .NET |[Met behulp van Hallo Graph API tooQuery Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configureer een Microsoft .NET-toepassing toouse hello Azure AD Graph API tooaccess gegevens uit een Azure AD-directory-tenant. |

## <a name="see-also"></a>Zie ook
##### <a name="other-resources"></a>Meer informatie
[Ontwikkelaarshandleiding Azure Active Directory](active-directory-developers-guide.md)

[Azure AD Graph API conceptuele en verwijzingen](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Azure AD Graph API Hulpbibliotheek](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
