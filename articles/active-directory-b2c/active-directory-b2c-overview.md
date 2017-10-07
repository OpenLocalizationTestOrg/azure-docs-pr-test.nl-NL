---
title: Overzicht - Azure AD B2C | Microsoft Docs
description: Consumententoepassingen ontwikkelen met Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C: u kunt u op uw app richten, dan letten wij op de registratie en aanmelding

Azure AD B2C is een oplossing voor identiteitsbeheer in de cloud voor uw web- en mobiele toepassingen. Het is een maximaal beschikbare wereldwijde service toohundreds miljoenen identiteiten. Azure AD B2C is ontwikkeld op een hoogwaardig, veilig platform en is bedoeld om uw toepassingen, uw bedrijf en uw klanten te beveiligen.

Met een minimale configuratie kunt Azure AD B2C in uw toepassing tooauthenticate:

* **Sociale accounts** (zoals Facebook, Google en LinkedIn)
* **Bedrijfsaccounts** (met behulp van open-standaardprotocollen, OpenID Connect of SAML)
* **Lokale accounts** (e-mailadres en wachtwoord of gebruikersnaam en wachtwoord)

## <a name="get-started"></a>Aan de slag

Haal eerst uw eigen tenant met behulp van Hallo stappen die worden beschreven in [een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).

Kies het scenario voor het ontwikkelen van uw toepassing:

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Mobiele en bureaubladapps](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />Mobiele en bureaubladapps</center> | [Overzicht](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Overzicht](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.js](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Apps met één pagina](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Apps met één pagina</center> | [Overzicht](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![Web-API's](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />Web-API's</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [Een .NET-web-API aanroepen](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Nieuwe functies

Kijk vaak toolearn over toekomstige wijzigingen toohello Azure Active Directory B2C. We tweeten ook over eventuele updates via @AzureAD.

* Bovendien te 'ingebouwde beleid (algemeen beschikbaar is),' Hallo ['Aangepaste beleidsregels'](active-directory-b2c-overview-custom.md) functie is nu beschikbaar in public preview.  Aangepaste beleidsregels zijn voor identity-professionals die controle over Hallo samenstelling van hun ervaring identiteit nodig.
* Hallo [Access Token](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) functie is nu beschikbaar in public preview.
* [Algemene beschikbaarheid van in Europa gebaseerde Azure AD B2C](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/)-directory's is aangekondigd.
* Bekijk onze groeiende bibliotheek met [codevoorbeelden op GitHub](https://github.com/Azure-Samples?q=b2c).

## <a name="how-tooarticles"></a>Hoe tooarticles

Meer informatie over hoe toouse specifieke Azure Active Directory B2C-functies:

* Configureer accounts van [Facebook](active-directory-b2c-setup-fb-app.md), [Google +](active-directory-b2c-setup-goog-app.md), [Microsoft](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) en [LinkedIn](active-directory-b2c-setup-li-app.md) voor gebruik in uw consumententoepassingen.
* [Gebruik aangepaste kenmerken toocollect informatie over uw consumenten](active-directory-b2c-reference-custom-attr.md).
* [Schakel Azure Multi-Factor Authentication in uw consumententoepassingen in](active-directory-b2c-reference-mfa.md).
* [Stel selfservice wachtwoordherstel in voor uw consumenten](active-directory-b2c-reference-sspr.md).
* [Hallo uiterlijk aan van de registratie aanpassen, meld u aan in en andere consumentenpagina's](active-directory-b2c-reference-ui-customization.md) die door Azure Active Directory B2C worden behandeld.
* [Gebruik hello Azure Active Directory Graph API tooprogrammatically maken, lezen, bijwerken en verwijderen van consumenten](active-directory-b2c-devquickstarts-graph-dotnet.md) in uw Azure Active Directory B2C-tenant.

## <a name="next-steps"></a>Volgende stappen

Deze koppelingen zijn handig voor het verkennen van Hallo service gedetailleerd besproken:

* Zie Hallo [prijsinformatie voor Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Bekijk onze [codevoorbeelden](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) voor Azure Active Directory B2C. 
* Hulp bij Stack Overflow met behulp van Hallo [azure-ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) label.
* Geef ons uw mening via [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), willen we toohear ze!
* Bekijk Hallo [naslaginformatie over Azure AD B2C-Protocol](active-directory-b2c-reference-protocols.md).
* Bekijk Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).
* Lees Hallo [Azure Active Directory B2C Veelgestelde vragen over](active-directory-b2c-faqs.md).
* [Aanvragen voor bestandsondersteuning voor Azure Active Directory B2C](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden

We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

