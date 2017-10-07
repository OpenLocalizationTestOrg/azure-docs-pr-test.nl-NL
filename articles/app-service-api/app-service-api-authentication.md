---
title: aaaAuthentication en autorisatie voor API-Apps in Azure App Service | Microsoft Docs
description: Meer informatie over Hallo verificatie en autorisatie services met Azure App Service voor API-Apps.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Verificatie en autorisatie voor API-Apps in Azure App Service
## <a name="overview"></a>Overzicht
> [!NOTE]
> In dit onderwerp worden de gemigreerde tooa geconsolideerd [App Service-verificatie / autorisatie](../app-service/app-service-authentication-overview.md) onderwerp bevat informatie over mobiele-, Web- en API-Apps.
> 
> 

Azure App Service biedt ingebouwde verificatie en autorisatie die services [OAuth 2.0](#oauth) en [OpenID Connect](#oauth). Dit artikel wordt beschreven Hallo services en de opties die beschikbaar voor de API-Apps in Azure App Service zijn.

Hallo volgende diagram ziet u enkele belangrijke kenmerken van App Service-verificatie:

* Het verwerkt binnenkomende API-aanvragen, wat betekent dat dit proces werkt met elke taal of elk framework ondersteund door App Service.
* Dit biedt u verschillende opties voor werkt hoeveel verificatie u wilt toodo in uw eigen code.
* De Tool werkt voor zowel eindgebruikers als de verificatie van de service-account. 
* Deze ondersteuning biedt voor vijf identiteitsproviders: Azure Active Directory, Facebook, Google, Twitter en Microsoft-Account.
* Dit werkt hetzelfde Hallo voor API-Apps, Web-Apps en mobiele Apps.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Networkdirect taal
Verwerking van App Service-verificatie wordt uitgevoerd voordat aanvragen uw API-app, wat betekent dat Hallo verificatiefuncties werken voor API-apps die zijn geschreven in elke taal of elk framework bereiken.  Uw API kan worden gebaseerd op ASP.NET, Java, Node.js of elk framework die ondersteuning biedt voor App Service.

App Service doorgegeven op Hallo JSON web token (JWT) in Hallo autorisatie-header van een HTTP-aanvraag en code die is geschreven in elke taal of elk framework kunt ophalen Hallo informatie die nodig is van Hallo token. Bovendien hebt App Service u eenvoudiger toegang toohello meest gebruikte claims door in te stellen sommige speciale kopteksten, zoals Hallo volgende:

* X-MS-CLIENT-PRINCIPAL-NAAM
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

In een .NET-API kunt u Hallo `Authorize` kenmerk en code op basis van claims voor fijnmazig autorisatie kunt u eenvoudig schrijven omdat informatie over claims in .NET-klassen voor u is ingevuld.

## <a name="multiple-protection-options"></a>Meerdere beveiligingsopties
App Service kunt voorkomen dat anonieme HTTP-aanvragen uw API-app is bereikt, kan doorgeven bij alle aanvragen en valideren van tokens voor aanvragen die ze bevatten of kunnen via alle aanvragen zonder verholpen op deze:

1. Toestaan dat alleen geverifieerde aanvragen tooreach uw API-app.
   
    Als een anonieme aanvraag wordt ontvangen via een browser, App-Service omleidt tooa aanmeldingspagina voor Hallo verificatieprovider (Azure AD, Google en Twitter, enzovoort) die u kiest. 
   
    U hoeft niet toowrite een verificatiecode op te geven op alle in uw app met deze optie en autorisatiecode wordt vereenvoudigd, omdat de belangrijkste claims Hallo u in Hallo HTTP-headers vindt.
2. Alle aanvragen tooreach uw API-app toestaan maar geverifieerde aanvragen valideren en verificatiegegevens in Hallo HTTP-headers doorgegeven.
   
    Deze optie biedt meer flexibiliteit in anonieme aanvragen voor de verwerking, maar er toowrite code als u tooprevent anonieme gebruikers wilt van uw API gebruiken. Sinds de meest populaire claims Hallo in Hallo-headers van HTTP-aanvragen worden doorgegeven, is autorisatiecode relatief eenvoudig.
3. Alle aanvragen tooreach toestaan uw API, geen actie onderneemt op verificatiegegevens in Hallo aanvragen.
   
    Deze optie blijven Hallo taken van verificatie en autorisatie volledig up tooyour toepassingscode.

In Hallo [Azure-portal](https://portal.azure.com/), optie Hallo op Hallo gewenste **verificatie / autorisatie** blade.

![](./media/app-service-api-authentication/authblade.png)

Inschakelen voor opties 1 en 2, **verificatie van App Service**, en in Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst kiezen **aanmelden** of **Aanvraag toestaan (geen actie)**.  Als u ervoor kiest **aanmelden**, u hebt toochoose een verificatieprovider en dat de provider configureren.

![](./media/app-service-api-authentication/actiontotake.png)

Voor gedetailleerde informatie over het tooconfigure verificatie, Zie [hoe tooconfigure uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Hallo-artikel geldt tooAPI apps, evenals een mobiele apps en andere verificatieproviders tooother artikelen voor Hallo gekoppeld.

## <a id="internal"></a>Verificatie van de service-account
App Service-verificatie werkt ook voor interne scenario's zoals voor het aanroepen van een API-app tooanother API-app. In dit scenario kunt u een token ophalen met behulp van referenties voor een serviceaccount in plaats van de referenties van de eindgebruiker. Een service-account wordt ook wel een *service-principal* in Azure Active Directory en verificatie met behulp van zo'n account wordt ook wel bekend als een service-naar-service-scenario. 

Voor service to service-scenario's beveiligen Hallo aangeroepen API-app met behulp van Azure Active Directory en een verificatietoken AAD-service principal bieden bij het aanroepen van Hallo API-app. U ophalen een token met Hallo client-ID en een client geheim Hallo AAD-toepassing. Er is geen speciale Azure alleen-lezen-code is vereist, zoals gebruikte toobe true voor het verwerken van Hallo Mobile Services Zumo token. Een voorbeeld van dit scenario met ASP.NET-API-apps wordt gedekt door Hallo zelfstudie [principal verificatie van de Service voor API-Apps](app-service-api-dotnet-service-principal-auth.md).

Als u een service-naar-serviceconnector scenario toohandle wilt zonder verificatie van App Service, kunt u clientcertificaten of basisverificatie. Zie voor informatie over clientcertificaten in Azure, [hoe tooConfigure TLS wederzijdse verificatie voor Web-Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Zie voor meer informatie over basisverificatie in ASP.NET [verificatie-Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

Verificatie van de service-account van een App Service logic app tooan API-app is een speciaal geval die wordt beschreven in [uw aangepaste API gebruiken die worden gehost op App Service met Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Mobiele clientverificatie
Voor informatie over het toohandle verificatie van mobiele clients, Zie Hallo [documentatie over verificatie voor mobiele apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md). App Service-verificatie werkt Hallo dezelfde manier voor mobiele apps en API apps.

## <a name="more-information"></a>Meer informatie
Zie voor meer informatie over verificatie en autorisatie in Azure App Service Hallo resources te volgen:

* [Uitbreidbare App Service-verificatie / autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Hoe tooconfigure uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (inclusief koppelingen voor andere verificatieproviders bovenaan Hallo Hallo pagina). 

Zie voor meer informatie over het OAuth 2.0, OpenID Connect en JSON Web Tokens (JWT) Hallo resources te volgen.

* [Aan de slag met OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "aan de slag met OAuth 2.0") 
* [Inleiding tooOAuth2, OpenID Connect en JSON Web Tokens (JWT) - Pluralsight loop](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Opbouwen en een RESTful-API voor meerdere Clients in ASP.NET - Pluralsight loop beveiligen](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Zie voor meer informatie over Azure Active Directory Hallo resources te volgen.

* [Azure AD-scenario 's](http://aka.ms/aadscenarios)
* [Azure AD ontwikkelaarshandleiding](http://aka.ms/aaddev)
* [Azure AD-voorbeelden](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Volgende stappen
In dit artikel is beschreven functies voor verificatie en autorisatie van App-Service die u voor API-apps gebruiken kunt. de volgende zelfstudie Hallo bij het ophalen van Hallo gestart reeks toont hoe tooimplement [verificatie van gebruikers in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).

