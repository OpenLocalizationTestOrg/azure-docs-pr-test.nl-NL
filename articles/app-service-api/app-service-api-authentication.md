---
title: Verificatie en autorisatie voor API-Apps in Azure App Service | Microsoft Docs
description: Meer informatie over de verificatie en autorisatie services met Azure App Service voor API-Apps.
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
ms.openlocfilehash: f9fd533dfbd54517232f9dae5000ed4779baebd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Verificatie en autorisatie voor API-Apps in Azure App Service
## <a name="overview"></a>Overzicht
> [!NOTE]
> In dit onderwerp worden gemigreerd naar een geconsolideerde [App Service-verificatie / autorisatie](../app-service/app-service-authentication-overview.md) onderwerp bevat informatie over mobiele-, Web- en API-Apps.
> 
> 

Azure App Service biedt ingebouwde verificatie en autorisatie die services [OAuth 2.0](#oauth) en [OpenID Connect](#oauth). Dit artikel worden de services en de opties die beschikbaar voor de API-Apps in Azure App Service zijn.

Het volgende diagram ziet u enkele belangrijke kenmerken van App Service-verificatie:

* Het verwerkt binnenkomende API-aanvragen, wat betekent dat dit proces werkt met elke taal of elk framework ondersteund door App Service.
* Dit biedt u verschillende opties voor werkt hoeveel verificatie u wilt uitvoeren in uw eigen code.
* De Tool werkt voor zowel eindgebruikers als de verificatie van de service-account. 
* Deze ondersteuning biedt voor vijf identiteitsproviders: Azure Active Directory, Facebook, Google, Twitter en Microsoft-Account.
* Dit werkt hetzelfde voor API Apps, Web-Apps en mobiele Apps.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Networkdirect taal
Verwerking van App Service-verificatie wordt uitgevoerd voordat aanvragen uw API-app, wat betekent dat de verificatiefuncties werken voor API-apps die zijn geschreven in elke taal of elk framework bereiken.  Uw API kan worden gebaseerd op ASP.NET, Java, Node.js of elk framework die ondersteuning biedt voor App Service.

Geeft App-Service op de JSON web token (JWT) in de autorisatie-header van een HTTP-aanvraag en code die is geschreven in elke taal of elk framework kan de benodigde gegevens ophalen uit het token. Bovendien biedt App Service u eenvoudiger toegang tot de meest gebruikte claims door in te stellen sommige speciale kopteksten, zoals de volgende:

* X-MS-CLIENT-PRINCIPAL-NAAM
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

In een .NET-API kunt u de `Authorize` kenmerk en code op basis van claims voor fijnmazig autorisatie kunt u eenvoudig schrijven omdat informatie over claims in .NET-klassen voor u is ingevuld.

## <a name="multiple-protection-options"></a>Meerdere beveiligingsopties
App Service kunt voorkomen dat anonieme HTTP-aanvragen uw API-app is bereikt, kan doorgeven bij alle aanvragen en valideren van tokens voor aanvragen die ze bevatten of kunnen via alle aanvragen zonder verholpen op deze:

1. Alleen geverifieerde aanvragen tot uw API-app toestaan.
   
    Als een anonieme aanvraag wordt ontvangen via een browser, wordt App-Service omleidt naar een aanmeldingspagina voor de verificatieprovider (Azure AD, Google en Twitter, enzovoort) die u kiest. 
   
    U hoeft niet te helemaal een verificatiecode te schrijven in uw app met deze optie en autorisatiecode wordt vereenvoudigd, omdat de belangrijkste claims u in de HTTP-headers vindt.
2. Toestaan dat alle aanvragen voor het bereiken van uw API-app, maar geverifieerde aanvragen valideren en doorgegeven verificatiegegevens in de HTTP-headers.
   
    Deze optie biedt meer flexibiliteit in anonieme aanvragen voor de verwerking, maar u code schrijven als u wilt voorkomen dat anonieme gebruikers met behulp van uw API. Aangezien de meest populaire claims worden doorgegeven in de headers van HTTP-aanvragen, is autorisatiecode relatief eenvoudig.
3. Toestaan dat alle aanvragen naar uw API bereikt, geen actie onderneemt op verificatiegegevens in de aanvragen.
   
    Deze optie worden de taken voor verificatie en autorisatie geheel afhankelijk van uw toepassingscode.

In de [Azure-portal](https://portal.azure.com/), selecteert u de optie die u wilt dat op de **verificatie / autorisatie** blade.

![](./media/app-service-api-authentication/authblade.png)

Inschakelen voor opties 1 en 2, **verificatie van App Service**, en in de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst kiezen **aanmelden** of **aanvraag toestaan (geen actie)**.  Als u ervoor kiest **aanmelden**, u moet een verificatieprovider kiest en dat de provider configureren.

![](./media/app-service-api-authentication/actiontotake.png)

Zie voor gedetailleerde informatie over het configureren van verificatie [het configureren van uw App Service-toepassing voor het gebruik van Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Het artikel is van toepassing op API-apps, evenals een mobiele apps en deze koppelingen naar andere artikelen voor de authenticatieproviders.

## <a id="internal"></a>Verificatie van de service-account
App Service-verificatie werkt ook voor interne scenario's zoals voor het aanroepen van een API-app in een andere API-app. In dit scenario kunt u een token ophalen met behulp van referenties voor een serviceaccount in plaats van de referenties van de eindgebruiker. Een service-account wordt ook wel een *service-principal* in Azure Active Directory en verificatie met behulp van zo'n account wordt ook wel bekend als een service-naar-service-scenario. 

Voor scenario's voor service-naar-service, de opgeroepen API-app beveiligen met behulp van Azure Active Directory en een verificatietoken AAD-service principal bieden bij het aanroepen van de API-app. U ophalen een token met de client-ID en een client geheim van de AAD-toepassing. Er is geen speciale Azure alleen-lezen-code is vereist, zoals die worden gebruikt voor het verwerken van het token Mobile Services Zumo waar. Een voorbeeld van dit scenario met ASP.NET-API-apps wordt gedekt door de zelfstudie [principal verificatie van de Service voor API-Apps](app-service-api-dotnet-service-principal-auth.md).

Als u een scenario voor service-naar-service verwerken wilt zonder het App Service-verificatie gebruikt, kunt u clientcertificaten of basisverificatie. Zie voor informatie over clientcertificaten in Azure, [hoe te configureren TLS wederzijdse verificatie voor Web-Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Zie voor meer informatie over basisverificatie in ASP.NET [verificatie-Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

Verificatie van een logische app van App Service-account in een API-app service is een speciaal geval die wordt beschreven in [uw aangepaste API gebruiken die worden gehost op App Service met Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Mobiele clientverificatie
Zie voor meer informatie over het afhandelen van verificatie van mobiele clients de [documentatie over verificatie voor mobiele apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md). App Service-verificatie werkt op dezelfde manier voor mobiele apps en API apps.

## <a name="more-information"></a>Meer informatie
Zie de volgende bronnen voor meer informatie over verificatie en autorisatie in Azure App Service:

* [Uitbreidbare App Service-verificatie / autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Het configureren van uw App Service-toepassing voor het gebruik van Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (inclusief koppelingen voor andere verificatieproviders boven aan de pagina.) 

Zie de volgende bronnen voor meer informatie over het OAuth 2.0, OpenID Connect en JSON Web Tokens (JWT).

* [Aan de slag met OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "aan de slag met OAuth 2.0") 
* [Inleiding tot OAuth2, OpenID Connect en JSON Web Tokens (JWT) - Pluralsight loop](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Opbouwen en een RESTful-API voor meerdere Clients in ASP.NET - Pluralsight loop beveiligen](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Zie de volgende bronnen voor meer informatie over Azure Active Directory.

* [Azure AD-scenario 's](http://aka.ms/aadscenarios)
* [Azure AD ontwikkelaarshandleiding](http://aka.ms/aaddev)
* [Azure AD-voorbeelden](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Volgende stappen
In dit artikel is beschreven functies voor verificatie en autorisatie van App-Service die u voor API-apps gebruiken kunt. De volgende zelfstudie in de ophalen gestart reeks ziet u hoe implementeren [verificatie van gebruikers in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).

