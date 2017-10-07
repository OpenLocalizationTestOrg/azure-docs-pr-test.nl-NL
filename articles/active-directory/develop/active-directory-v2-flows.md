---
title: aaaApp typen voor hello Azure Active Directory v2.0-eindpunt | Microsoft Docs
description: Hallo typen apps en scenario's ondersteund door hello Azure Active Directory v2.0-eindpunt.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>App-typen voor hello Azure Active Directory v2.0-eindpunt
Hello Azure Active Directory (Azure AD) v2.0-eindpunt ondersteunt verificatie voor diverse moderne app-architecturen allemaal op basis van industriestandaard-protocollen [OAuth 2.0- of OpenID Connect](active-directory-v2-protocols.md). Dit artikel wordt beschreven Hallo typen apps die u maken kunt met behulp van Azure AD v2.0, ongeacht uw voorkeurstaal of platform. Hallo informatie in dit artikel is ontworpen toohelp u inzicht in geavanceerde scenario's voordat u [beginnen met werken met Hallo code](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen. toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>Hallo-basisbeginselen
U moet elke app die gebruikmaakt van Hallo v2.0-eindpunt in Hallo registreren [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com). Hallo app registratieproces verzamelt en wijst deze waarden voor uw app:

* Een **toepassings-ID** die wordt aangeduid uw app
* Een **omleidings-URI** waarmee u toodirect antwoorden back tooyour app kunt
* Enkele andere scenariospecifieke waarden

Voor meer informatie, meer informatie over hoe te[een app registreren](active-directory-v2-app-registration.md).

Nadat het Hallo-app is geregistreerd, communiceert de Hallo-app met Azure AD door te verzenden aanvragen toohello Azure AD v2.0-eindpunt. We bieden open source frameworks en bibliotheken waarmee Hallo details van deze aanvragen worden verwerkt. U hebt ook Hallo optie tooimplement Hallo verificatielogica zelf aanvragen toothese eindpunten maken:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Web-apps
Voor web-apps (.NET, PHP, Java, Ruby, Python, knooppunt) die gebruiker toegang krijgt via een browser hello, kunt u [OpenID Connect](active-directory-v2-protocols.md) voor gebruikersaanmelding. In het OpenID Connect ontvangt Hallo web-app een token ID. Een token ID is een beveiligingstoken dat Hallo gebruikersidentiteit controleert en bevat informatie over het Hallo-gebruiker in de vorm van claims Hallo:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

U kunt meer informatie over alle Hallo typen tokens en claims die beschikbaar tooan-app in Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md).

In de web server-apps duurt het Hallo-in authenticatiestroom deze stappen op hoog niveau:

![Authenticatiestroom voor web-app](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

U kunt controleren of Hallo gebruikersidentiteit door het Hallo-id-token te valideren met een openbare ondertekeningssleutel die is ontvangen van Hallo v2.0-eindpunt. Een sessiecookie is ingesteld, wat kan gebruikte tooidentify Hallo gebruiker op de volgende pagina-aanvragen zijn.

toosee dit scenario werkt, probeer een van de Hallo web-app aanmelden code-voorbeelden in onze v2.0 [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.

Bovendien toosimple aanmelden moet een webserver-app mogelijk tooaccess een andere webservice, zoals een REST-API. In dit geval Hallo webserver-app alleen mogelijk in een gecombineerde OpenID Connect en OAuth 2.0-stroom met behulp van Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols.md). Lees voor meer informatie over dit scenario over [aan de slag met web-apps en Web-API's](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>Web-API's
U kunt Hallo v2.0-eindpunt toosecure webservices, zoals de RESTful Web-API van uw app kunt gebruiken. In plaats van de ID-tokens en sessiecookies een Web-API maakt gebruik van een token toosecure voor OAuth 2.0-toegang tot de gegevens en tooauthenticate binnenkomende aanvragen. Hallo aanroeper van een Web-API voegt een toegangstoken in Hallo autorisatie-header van een HTTP-verzoek als volgt:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hallo-Web-API gebruikt Hallo access token tooverify Hallo API aanroeper identiteits- en tooextract informatie over de aanroeper van claims die zijn gecodeerd in toegangstoken Hallo Hallo. toolearn over alle Hallo typen tokens en claims die beschikbaar tooan app, Zie Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md).

Een Web-API kunt geeft gebruikers Hallo power tooopt in of specifieke functionaliteit of gegevens afmelden bij het blootstellen van machtigingen, ook wel bekend als [scopes](active-directory-v2-scopes.md). Voor een aanroepen app tooacquire machtiging tooa scope, Hallo gebruiker toestemming moet geven toohello bereik tijdens een stroom. Hallo v2.0-eindpunt Hallo-gebruiker om toestemming wordt gevraagd en vervolgens registreert machtigingen in alle toegangstokens die Hallo die web API ontvangt. Hallo-Web-API valideert Hallo toegangstokens dit op elke aanroep ontvangt en autorisatie controles uitgevoerd.

Een Web-API kan toegangstokens ontvangen van alle typen apps, met inbegrip van server-web-apps, bureaublad en mobiele apps, apps van één pagina, daemons aan serverzijde en zelfs andere Web-API's. Hallo op hoog niveau stroom voor een Web-API ziet er als volgt:

![Web-API-authenticatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn hoe toosecure een Web-API met OAuth2-toegangstokens, uitchecken Hallo Web API-code-voorbeelden in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.

Web-API's in veel gevallen moet ook toomake uitgaande aanvragen tooother downstream web-API's die zijn beveiligd door Azure Active Directory.  toodo dus web-API's kan profiteren van Azure AD **op namens** stroom, waardoor Hallo web-API tooexchange een binnenkomende toegangstoken voor een andere access token toobe gebruikt in uitgaande aanvragen.  Hallo v2.0-eindpunt namens stroom wordt beschreven in [details hier](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Mobiele en systeemeigen apps
Apparaat geïnstalleerd apps, zoals mobiele en bureaublad-apps, moeten vaak tooaccess back-endservices of Web-API's die gegevens opslaan en uitvoeren van functies namens een gebruiker. Deze apps aanmelden en autorisatie tooback-end-services kunnen toevoegen met behulp van Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols-oauth-code.md).

In deze stroom ontvangt Hallo app een autorisatiecode Hallo v2.0-eindpunt wanneer Hallo gebruiker zich aanmeldt. Hallo autorisatie code vertegenwoordigt Hallo van app machtiging toocall back-end-services namens Hallo-gebruiker die is aangemeld. Hallo-app kan de autorisatiecode Hallo op de achtergrond Hallo voor een toegangstoken OAuth 2.0 en een vernieuwingstoken uitwisselen. Hallo-app kunt gebruiken Hallo access token tooauthenticate tooWeb API's in HTTP-aanvragen en Hallo vernieuwen token tooget nieuwe toegangstokens gebruiken wanneer oudere toegangstokens verlopen.

![Systeemeigen app verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Apps met één pagina (JavaScript)
Veel moderne apps hebben een front-end app met één pagina die voornamelijk in JavaScript is geschreven. Vaak wordt geschreven met behulp van een framework zoals AngularJS, Ember.js of Durandal.js. Hello Azure AD v2.0-eindpunt ondersteunt deze apps via Hallo [impliciete OAuth 2.0-stroom](active-directory-v2-protocols-implicit.md).

In deze stroom Hallo app-tokens rechtstreeks van ontvangen Hallo v2.0 autoriseren eindpunt, zonder eventuele uitwisselingen server-naar-server. Alle verificatielogica en sessie afhandeling van vindt volledig in Hallo JavaScript-client, zonder extra paginaomleidingen plaatsen.

![Impliciete verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee dit scenario werkt, probeer een van de Hallo één pagina app-codevoorbeelden in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.

## <a name="daemons-and-server-side-apps"></a>Daemons en serverzijde apps
Apps die langlopende processen hebben of die werken zonder interactie met een gebruiker moeten ook een manier tooaccess bronnen, zoals Web-API's beveiligde. Deze apps kunnen verifiëren en tokens verkrijgen met de identiteit van de app Hallo in plaats van een gebruiker overgedragen identiteit met clientreferentiestroom Hallo OAuth 2.0.

In deze stroom Hallo app communiceert rechtstreeks met de Hallo `/token` eindpunt tooobtain eindpunten:

![Verificatiestroom daemon-app](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

een app daemon toobuild Zie Hallo client referenties documentatie in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie of probeer een [voorbeeld-app voor .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
