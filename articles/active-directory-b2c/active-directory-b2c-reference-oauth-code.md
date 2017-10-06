---
title: Autorisatiecodestroom - Azure AD B2C | Microsoft Docs
description: Meer informatie over hoe toobuild web-apps met behulp van Azure AD B2C en OpenID Connect-verificatieprotocol.
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: OAuth 2.0-autorisatiecodestroom
U kunt Hallo OAuth 2.0 autorisatie code grant in apps die zijn geïnstalleerd op een apparaat toogain toegang tooprotected resources, zoals web-API's gebruiken. U kunt toevoegen, registreren, aanmelden met behulp van hello Azure Active Directory B2C (Azure AD B2C) implementatie van OAuth 2.0 en andere identiteitsbeheer taken tooyour mobiele en bureaublad-apps. In dit artikel is taalonafhankelijk. In Hallo artikel wordt beschreven hoe toosend en HTTP-berichten ontvangen zonder gebruik van een open source-bibliotheken.

<!-- TODO: Need link toolibraries -->

Hallo OAuth 2.0-autorisatiecodestroom wordt beschreven in [sectie 4.1 van Hallo OAuth 2.0-specificatie](http://tools.ietf.org/html/rfc6749). U kunt deze gebruiken voor verificatie en autorisatie in de meeste typen van de app, inclusief [web-apps](active-directory-b2c-apps.md#web-apps) en [systeemeigen geïnstalleerde apps](active-directory-b2c-apps.md#mobile-and-native-apps). Kunt u OAuth 2.0 autorisatie code stroom toosecurely verkrijgen Hallo *toegang tot tokens* voor uw apps, wat kan zijn gebruikte tooaccess resources die zijn beveiligd met een [autorisatie server](active-directory-b2c-reference-protocols.md#the-basics).

In dit artikel is gericht op Hallo **openbare clients** OAuth 2.0-autorisatiecodestroom. Een openbare-client is elke clienttoepassing die niet kan worden vertrouwd toosecurely Hallo integriteit van een geheime vraag te behouden. Dit omvat mobiele apps, bureaublad-apps en in wezen elke toepassing die wordt uitgevoerd op een apparaat en moet tooget toegangstokens. 

> [!NOTE]
> tooadd identity management tooa web-app met behulp van Azure AD B2C, gebruik [OpenID Connect](active-directory-b2c-reference-oidc.md) in plaats van OAuth 2.0.

Azure AD B2C breidt Hallo standaard die OAuth 2.0 loopt toodo meer dan een eenvoudige verificatie en autorisatie. Hierdoor Hallo [Beleidsparameter](active-directory-b2c-reference-policies.md). Met ingebouwde beleidsregels, kunt u OAuth 2.0 tooadd gebruiker merkt dat tooyour app, zoals aanmelding, aanmelding en Profielbeheer. In dit artikel wordt uitgelegd hoe u dat toouse OAuth 2.0 en beleidsregels tooimplement elk van deze in uw eigen toepassingen functionaliteit. We ook ziet u hoe tooget toegangstokens voor toegang tot web-API's.

In voorbeeld HTTP-aanvragen Hallo in dit artikel, gebruiken we onze voorbeeld Azure AD B2C-directory **fabrikamb2c.onmicrosoft.com**. We gebruiken ook onze voorbeeldtoepassing en beleidsregels. U kunt aanvragen Hallo zelf met behulp van deze waarden, of kunt u deze vervangen door uw eigen waarden.
Meer informatie over hoe te[ophalen van uw eigen Azure AD B2C-directory, toepassingen en beleidsregels](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Een autorisatiecode ophalen
Hallo-autorisatiecodestroom begint met de Hallo client doorsturen Hallo gebruiker toohello `/authorize` eindpunt. Dit is Hallo interactieve onderdeel van Hallo-stroom waar Hallo gebruiker actie plaatsvindt. In deze aanvraag Hallo-client geeft aan in Hallo `scope` parameter Hallo machtigingen dat het moet tooacquire van Hallo-gebruiker. In Hallo `p` parameter, betekent dit Hallo beleid tooexecute. Hallo gebruik volgende drie voorbeelden (met regeleinden voor leesbaarheid) elk een ander beleid.

### <a name="use-a-sign-in-policy"></a>Een beleid voor aanmelden gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Een registratiebeleid gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Gebruik van een beleid voor het profiel bewerken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassings-ID toegewezen tooyour-app in Hallo [Azure-portal](https://portal.azure.com). |
| response_type |Vereist |Hallo antwoordtype, waaronder moet `code` voor Hallo-autorisatiecodestroom. |
| redirect_uri |Vereist |Hallo omleidings-URI van uw app, waarbij verificatie antwoorden zijn verzonden en ontvangen door uw app. Deze moet exact overeenkomen met een van Hallo omleidings-URI's die u hebt geregistreerd in Hallo-portal, behalve dat het URL-codering moet worden. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure Active Directory (Azure AD) beide Hallo machtigingen die worden aangevraagd. Met behulp van Hallo client ID zoals Hallo bereik geeft aan dat uw app moet een toegangstoken die kan worden gebruikt op basis van uw eigen service of web-API, vertegenwoordigd door Hallo dezelfde client-ID.  Hallo `offline_access` bereik geeft aan dat uw app een vernieuwingstoken voor de lange levensduur hebben toegang tot tooresources moet. Ook kunt u Hallo `openid` bereik toorequest een token ID van Azure AD B2C. |
| response_mode |Aanbevolen |Hallo-methode is dat u toosend Hallo resulterende autorisatie code back tooyour app gebruiken. Kan `query`, `form_post`, of `fragment`. |
| state |Aanbevolen |Een waarde die is opgenomen in het Hallo-aanvraag die wordt geretourneerd als antwoord van Hallo-token. Een tekenreeks van alle inhoud die u wilt dat toouse kan zijn. Normaal gesproken een willekeurig gegenereerde unieke waarde wordt gebruikt, tooprevent aanvraagvervalsing op meerdere sites aanvallen. Hallo-status is ook gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat het Hallo-verificatieaanvraag is opgetreden. Bijvoorbeeld, Hallo pagina Hallo gebruiker is aan of Hallo beleid dat werd uitgevoerd. |
| P |Vereist |Hallo-beleid dat wordt uitgevoerd. De Hallo naam van een beleid dat is gemaakt in uw Azure AD B2C-directory. Hallo-beleidswaarde naam moet beginnen met **b2c\_1\_**. toolearn meer informatie over beleidsregels, Zie [ingebouwde beleid van Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Optioneel |Hallo-type van de interactie van de gebruiker die is vereist. De enige geldige waarde Hallo is momenteel `login`, dit dwingt Hallo gebruiker tooenter hun referenties op die aanvraag. Eenmalige aanmelding wordt pas van kracht. |

Op dit moment hello wordt u gevraagd toocomplete Hallo beleid werkstroom. Dit kan erbij betrekken Hallo gebruikers voeren hun gebruikersnaam en wachtwoord, aanmelden met een sociale identiteit aanmelden voor Hallo directory of een andere aantal stappen. Acties van de gebruiker is afhankelijk van hoe Hallo beleid is gedefinieerd.

Nadat het Hallo gebruiker voltooit Hallo-beleid, Azure AD retourneert een antwoord tooyour app op Hallo-waarde die u gebruikt voor `redirect_uri`. Hierbij Hallo methode in Hallo `response_mode` parameter. Hallo-antwoord is precies dezelfde Hallo voor elk Hallo actie gebruikersscenario, onafhankelijk van het Hallo-beleid dat is uitgevoerd.

Een geslaagde reactie die gebruikmaakt van `response_mode=query` ziet er als volgt:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parameter | Beschrijving |
| --- | --- |
| code |Hallo autorisatiecode die Hallo app aangevraagd. Hallo-app kunt Hallo autorisatie code toorequest een toegangstoken gebruiken voor een doelbron. Autorisatiecodes zijn zeer tijdelijke. Normaal gesproken verlopen ze na ongeveer 10 minuten. |
| state |Volledige beschrijving van de Hallo in de tabel in de voorgaande sectie Hallo Hallo bekijken. Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |

Foutberichten kunnen ook worden verzonden toohello omleidings-URI zodat hello app ze op de juiste wijze verwerken kan:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u kunt tooclassify Hallo typen fouten die optreden. U kunt ook Hallo tekenreeks tooreact tooerrors gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |
| state |Volledige beschrijving van de Hallo in de voorgaande tabel Hallo bekijken. Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |

## <a name="2-get-a-token"></a>2. Een token ophalen
Nu dat u een autorisatiecode hebt aangeschaft, kunt u gebruikmaken van Hallo `code` voor een token toohello resource bedoeld door het verzenden van een POST-aanvraag toohello `/token` eindpunt. In Azure AD B2C is hello alleen resource die u kunt een token voor aanvragen het uw web-API van de back-end in de app. Hallo-conventie die wordt gebruikt voor het aanvragen van een token tooyourself is toouse van uw app-client-ID als Hallo bereik:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| P |Vereist |beleid dat gebruikt tooacquire Hallo autorisatie is Hallo code. U kunt een ander beleid niet gebruiken in deze aanvraag. U deze parameter toohello toevoegen *querytekenreeks*, niet in Hallo POST-instantie. |
| client_id |Vereist |Hallo toepassings-ID toegewezen tooyour-app in Hallo [Azure-portal](https://portal.azure.com). |
| grant_type |Vereist |Hallo type verlenen. Voor het Hallo-autorisatiecodestroom, Hallo grant type moet `authorization_code`. |
| Bereik |Aanbevolen |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide Hallo machtigingen die worden aangevraagd. Met behulp van Hallo client ID zoals Hallo bereik geeft aan dat uw app moet een toegangstoken die kan worden gebruikt op basis van uw eigen service of web-API, vertegenwoordigd door Hallo dezelfde client-ID.  Hallo `offline_access` bereik geeft aan dat uw app een vernieuwingstoken voor de lange levensduur hebben toegang tot tooresources moet.  Ook kunt u Hallo `openid` bereik toorequest een token ID van Azure AD B2C. |
| code |Vereist |Hallo autorisatie-code die u hebt verkregen in de eerste arm Hallo van Hallo stroom. |
| redirect_uri |Vereist |Hallo omleidings-URI van Hallo toepassing waar u de autorisatiecode Hallo ontvangen. |

Een geslaagde reactie token ziet er als volgt:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parameter | Beschrijving |
| --- | --- |
| not_before |Hallo tijd op welke Hallo token wordt beschouwd als geldige epoche tijdstip. |
| token_type |Hallo type token waarde. Hallo alleen typen dat ondersteunt Azure AD Bearer is. |
| access_token |Hallo ondertekend JSON Web Token (JWT) die u hebt aangevraagd. |
| Bereik |Hallo-scopes die Hallo token is geldig voor. U kunt ook scopes toocache tokens gebruiken voor later gebruik. |
| expires_in |Hallo tijdsduur die Hallo token is ongeldig (in seconden). |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo-app kunt dit token tooacquire extra tokens gebruiken nadat Hallo huidige token is verlopen. Vernieuwen van tokens zijn lange levensduur hebben. U kunt ze tooretain toegang tooresources voor langere tijd. Zie voor meer informatie, Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). |

-Foutberichten moeten uitzien:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u kunt tooclassify Hallo typen fouten die optreden. U kunt ook Hallo tekenreeks tooreact tooerrors gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |

## <a name="3-use-hello-token"></a>3. Hallo-token gebruiken
Nu dat u hebt een toegangstoken is verkregen, kunt u Hallo-token in aanvragen tooyour back-end web-API's door deze in Hallo `Authorization` header:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Hallo-token te vernieuwen
Toegangstokens en ID-tokens zijn tijdelijke. Nadat ze zijn verlopen, moet u ze toocontinue tooaccess resources vernieuwen. toodo dit door een andere toohello voor POST-aanvraag indienen `/token` eindpunt. Deze tijd bieden Hallo `refresh_token` in plaats van Hallo `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| P |Vereist |Hallo-beleid dat gebruikt tooacquire Hallo oorspronkelijke vernieuwingstoken is. U kunt een ander beleid niet gebruiken in deze aanvraag. U deze parameter toohello toevoegen *querytekenreeks*, niet in Hallo POST-instantie. |
| client_id |Aanbevolen |Hallo toepassings-ID toegewezen tooyour-app in Hallo [Azure-portal](https://portal.azure.com). |
| grant_type |Vereist |Hallo type verlenen. Voor deze fase van de autorisatiecodestroom hello, Hallo grant type moet `refresh_token`. |
| Bereik |Aanbevolen |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide Hallo machtigingen die worden aangevraagd. Met behulp van Hallo client ID zoals Hallo bereik geeft aan dat uw app moet een toegangstoken die kan worden gebruikt op basis van uw eigen service of web-API, vertegenwoordigd door Hallo dezelfde client-ID.  Hallo `offline_access` bereik geeft aan dat uw app een vernieuwingstoken voor lange levensduur hebben toegang tot tooresources nodig.  Ook kunt u Hallo `openid` bereik toorequest een token ID van Azure AD B2C. |
| redirect_uri |Optioneel |Hallo omleidings-URI van Hallo toepassing waar u de autorisatiecode Hallo ontvangen. |
| refresh_token |Vereist |Hallo oorspronkelijke vernieuwingstoken die u hebt verkregen in de tweede arm Hallo van Hallo stroom. |

Een geslaagde reactie token ziet er als volgt:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parameter | Beschrijving |
| --- | --- |
| not_before |Hallo tijd op welke Hallo token wordt beschouwd als geldige epoche tijdstip. |
| token_type |Hallo type token waarde. Hallo alleen typen dat ondersteunt Azure AD Bearer is. |
| access_token |Hallo ondertekend JWT die u hebt aangevraagd. |
| Bereik |Hallo-scopes die Hallo token is geldig voor. U kunt ook Hallo scopes toocache tokens gebruiken voor later gebruik. |
| expires_in |Hallo tijdsduur die Hallo token is ongeldig (in seconden). |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo-app kunt dit token tooacquire extra tokens gebruiken nadat Hallo huidige token is verlopen. Vernieuwen van tokens worden lange levensduur en gebruikte tooretain toegang tooresources voor langere tijd kan worden. Zie voor meer informatie, Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). |

-Foutberichten moeten uitzien:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u kunt tooclassify typen fouten die optreden. U kunt ook Hallo tekenreeks tooreact tooerrors gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Uw eigen Azure AD B2C-directory gebruiken
tootry deze aanvragen zelf voltooid hello te volgen stappen. Vervang Hallo voorbeeldwaarden die wordt gebruikt in dit artikel met uw eigen waarden.

1. [Een Azure AD B2C-directory maken](active-directory-b2c-get-started.md). Hallo-naam van uw directory in Hallo aanvragen gebruiken.
2. [Maken van een toepassing](active-directory-b2c-app-registration.md) tooobtain een toepassings-ID en een omleidings-URI. Een systeemeigen client opnemen in uw app.
3. [Maken van uw beleid](active-directory-b2c-reference-policies.md) tooobtain de beleidsnamen van uw.

