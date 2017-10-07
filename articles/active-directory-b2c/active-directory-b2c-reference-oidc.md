---
title: Web-aanmelden met OpenID Connect - Azure AD B2C | Microsoft Docs
description: Web-toepassingen maken met behulp van hello Azure Active Directory-implementatie van OpenID Connect-verificatieprotocol van Hallo
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: Web aanmelden met OpenID Connect
OpenID Connect is een protocol voor verificatie, OAuth 2.0, die gebruikers van de gebruikte toosecurely aanmelden in tooweb toepassingen kunnen zijn ingebouwd. Met behulp van hello Azure Active Directory B2C (Azure AD B2C) implementatie van OpenID Connect, u kunt uitbesteden registreren, aanmelden en andere identiteitsbeheer in uw web-toepassingen tooAzure Active Directory (Azure AD). Deze handleiding ontdekt u hoe toodo geval op een manier taalonafhankelijk. Hierin wordt beschreven hoe toosend en HTTP-berichten ontvangen zonder dat u een van onze open source-bibliotheken.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) breidt Hallo OAuth 2.0 *autorisatie* protocol voor gebruik als een *verificatie* protocol. Hiermee kunt u eenmalige aanmelding tooperform met behulp van OAuth. Het concept van Hallo introduceert een *token ID*, dit is een beveiligingstoken waarmee Hallo client tooverify identiteit van de gebruiker Hallo Hallo en basisprofiel informatie verkrijgen over Hallo-gebruiker.

Omdat het OAuth 2.0 uitbreidt, kunt u eveneens apps toosecurely verkrijgen *toegang tot tokens*. U kunt access_tokens tooaccess resources die zijn beveiligd met een [autorisatie server](active-directory-b2c-reference-protocols.md#the-basics). Het is raadzaam OpenID Connect als u een webtoepassing die wordt gehost op een server en is toegankelijk via een browser maakt. Als u tooadd identity management tooyour mobiele of bureaubladtoepassingen toepassingen wilt met behulp van Azure AD B2C, moet u [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) in plaats van het OpenID Connect.

Azure AD B2C breidt Hallo standaard OpenID Connect protocol toodo meer dan eenvoudige verificatie en autorisatie. Hierdoor Hallo [parameter van het beleid](active-directory-b2c-reference-policies.md), waarmee u toouse OpenID Connect tooadd gebruikerservaringen--zoals aanmelding, aanmelding en Profielbeheer--tooyour app. Hier wordt uitgelegd hoe u dat toouse OpenID Connect en beleidsregels tooimplement elk van deze in uw webtoepassingen functionaliteit. Ook ziet u hoe tooget toegangstokens voor toegang tot web-API's.

Hallo voorbeeld HTTP-aanvragen in de volgende sectie hello gebruiken onze voorbeeld B2C-directory, fabrikamb2c.onmicrosoft.com, evenals onze voorbeeldtoepassing https://aadb2cplayground.azurewebsites.net en beleidsregels. U kunt gratis tootry uit Hallo verzoeken zelf met behulp van deze waarden, of kunt u deze vervangen door uw eigen.
Meer informatie over hoe te[ophalen van uw eigen B2C-tenant-, toepassings- en beleid](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Verificatieaanvragen verzenden
Wanneer uw web-app moet tooauthenticate Hallo gebruiker en uitvoeren van een beleid, Hallo gebruiker toohello kan worden doorgestuurd `/authorize` eindpunt. Dit is Hallo interactieve gedeelte van de stroom Hallo, waar Hallo gebruiker optreden, afhankelijk van Hallo beleid plaatsvindt.

In deze aanvraag Hallo-client geeft aan dat het moet tooacquire van gebruiker in Hallo HALLO hallo-machtigingen `scope` parameter en Hallo beleid tooexecute in Hallo `p` parameter. Drie voorbeelden vindt u in Hallo uit te voeren (met regeleinden voor leesbaarheid), elk met een ander beleid. tooget een idee voor hoe elke aanvraag werkt, probeer plakken Hallo aanvraag in een browser en het uitvoeren.

#### <a name="use-a-sign-in-policy"></a>Een beleid voor aanmelden gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Een registratiebeleid gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Gebruik van een beleid voor het profiel bewerken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassing-ID die Hallo [Azure-portal](https://portal.azure.com/) tooyour app toegewezen. |
| response_type |Vereist |Hallo antwoordtype, die een token ID voor het OpenID Connect moet bevatten. Als uw web-app ook tokens moet voor het aanroepen van een web-API, kunt u `code+id_token`, zoals we hier hebt gedaan. |
| redirect_uri |Aanbevolen |Hallo `redirect_uri` parameter van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app. Deze moet exact overeenkomen met een Hallo `redirect_uri` parameters die u hebt geregistreerd in Hallo-portal, behalve dat het moet een URL zijn gecodeerd. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide machtigingen die worden aangevraagd. Hallo `openid` bereik geeft aan dat een machtiging toosign in Hallo gebruiker en get-gegevens over Hallo-gebruiker in de vorm Hallo van ID-tokens (meer toocome op deze later in Hallo artikel). Hallo `offline_access` bereik is optioneel voor web-apps. Hiermee wordt aangegeven dat uw app moet een *vernieuwingstoken* voor lange levensduur hebben toegang tot tooresources. |
| response_mode |Aanbevolen |Hallo-methode die gebruikt toosend Hallo resulterende autorisatie code back tooyour app worden moet. Het kan zijn `query`, `form_post`, of `fragment`.  Hallo `form_post` antwoord-modus wordt aanbevolen voor de beste beveiliging. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag wordt ook Hallo token antwoord geretourneerd. Een tekenreeks van inhoud die u wilt dat kan zijn. Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor het voorkomen van aanvraagvervalsing op meerdere sites aanvallen. Hallo-status is ook gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina op. |
| nonce |Vereist |Een waarde die is opgenomen in het Hallo-aanvraag (gegenereerd door Hallo app) die worden opgenomen in het resulterende ID token Hallo als een claim. Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen. Hallo-waarde is meestal een willekeurige unieke tekenreeks die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| P |Vereist |Hallo-beleid dat wordt uitgevoerd. Het is Hallo-naam van een beleid dat is gemaakt in uw B2C-tenant. Hallo-beleidswaarde naam moet beginnen met `b2c\_1\_`. Meer informatie over beleidsregels en Hallo [uitbreidbaar beleidsframework](active-directory-b2c-reference-policies.md). |
| prompt |Optioneel |Hallo-type van de interactie van de gebruiker die is vereist. Hallo enige geldige waarde op dit moment is `login`, dit dwingt Hallo gebruiker tooenter hun referenties voor deze aanvraag. Eenmalige aanmelding wordt pas van kracht. |

Op dit moment hello wordt u gevraagd toocomplete Hallo beleid werkstroom. Dit kan erbij betrekken Hallo gebruikers voeren hun gebruikersnaam en wachtwoord, aanmelden met een sociale identiteit aanmelden voor Hallo directory of een andere aantal stappen, afhankelijk van hoe Hallo beleid is gedefinieerd.

Nadat het Hallo gebruiker voltooit Hallo-beleid, Azure AD retourneert een antwoord tooyour app op Hallo aangegeven `redirect_uri` parameter met Hallo-methode die is opgegeven in Hallo `response_mode` parameter. Hallo-antwoord is Hallo dezelfde voor elk Hallo voorgaande gevallen, onafhankelijk van het Hallo-beleid dat wordt uitgevoerd.

Een geslaagde reactie met `response_mode=fragment` eruit als:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parameter | Beschrijving |
| --- | --- |
| id_token |Hallo ID-token dat Hallo app aangevraagd. U kunt gebruiken Hallo ID token tooverify Hallo gebruikers id en beginnen met een sessie met de Hallo-gebruiker. Meer informatie over het ID-tokens en de inhoud ervan zijn opgenomen in Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). |
| code |Hallo autorisatie code die Hallo app aangevraagd, als u hebt gebruikt `response_type=code+id_token`. Hallo-app kunt Hallo autorisatie code toorequest een toegangstoken gebruiken voor een doelbron. Autorisatiecodes zijn zeer tijdelijke. Normaal gesproken verlopen ze na ongeveer 10 minuten. |
| state |Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |

Foutberichten kunnen ook worden verzonden toohello `redirect_uri` parameter zodat die app Hallo ze op de juiste wijze kan verwerken:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks foutcode die kan worden gebruikt tooclassify typen fouten die optreden en die kan worden gebruikt tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |
| state |Zie Hallo volledige beschrijving van de eerste tabel Hallo in deze sectie. Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |

## <a name="validate-hello-id-token"></a>Hallo-id-token valideren
Zojuist hebt ontvangen van een token ID is niet voldoende tooauthenticate Hallo-gebruiker. U moet Hallo-ID van het token handtekening valideren en controleer of Hallo claims in Hallo token per vereisten van uw app. Maakt gebruik van Azure AD B2C [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) en openbare sleutel-cryptografie toosign tokens en controleer of ze geldig zijn.

Er zijn veel open source-bibliotheken die beschikbaar zijn voor het valideren van JWTs, afhankelijk van de taal van voorkeur. U wordt aangeraden deze opties verkennen in plaats van uw eigen validatielogica implementeren. Hallo informatie hier erg nuttig zijn in uitzoeken hoe tooproperly die bibliotheken gebruiken.

Azure AD B2C heeft een eindpunt OpenID Connect metagegevens waarmee een app toofetch informatie over Azure AD B2C tijdens runtime. Deze informatie omvat eindpunten, inhoud van tokens en token-ondertekening sleutels. Er is een JSON-metagegevens-document voor elk beleid in uw B2C-tenant. Bijvoorbeeld, Hallo metagegevensdocument voor Hallo `b2c_1_sign_in` beleid in `fabrikamb2c.onmicrosoft.com` bevindt zich op:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Een van de Hallo eigenschappen van dit document configuratie `jwks_uri`, waarvan de waarde voor Hallo hetzelfde beleid zijn:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine welk beleid is gebruikt in een ID-token-ondertekening (en vanuit waar toofetch Hallo metagegevens), hebt u twee opties. Eerst Hallo beleidsnaam is opgenomen in Hallo `acr` claim in Hallo-id-token. Zie voor informatie over hoe tooparse Hallo claims van een token ID Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). De andere mogelijkheid is tooencode Hallo beleid in Hallo-waarde van Hallo `state` parameter wanneer u Hallo-aanvraag en decoderen vervolgens toodetermine welk beleid is gebruikt. Beide methoden is geldig.

Nadat u Hallo metagegevensdocument van metagegevens-eindpunt met OpenID Connect Hallo hebt aangeschaft, kunt u Hallo RSA 256 openbare sleutels (die zich op dit eindpunt) toovalidate Hallo handtekening van Hallo-ID-token. Er is mogelijk meerdere sleutels die aan dit eindpunt op elk gewenst moment worden vermeld in de tijd die u kunt herkennen door een `kid` claim. Hallo-header van het Hallo-id-token bevat ook een `kid` claim, waarmee wordt aangegeven welke van deze sleutels gebruikte toosign Hallo-id-token is. Zie voor meer informatie, Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md) (sectie op Hallo [valideren van tokens](active-directory-b2c-reference-tokens.md#token-validation), met name).
<!--TODO: Improve hello information on this-->

Nadat u Hallo handtekening van Hallo-ID-token hebt geverifieerd, zijn er verschillende claims, moet u tooverify. Bijvoorbeeld:

* U moet valideren Hallo `nonce` claim tooprevent token replay-aanvallen. De waarde moet Hallo aanmeldingsverzoek wat u hebt opgegeven.
* U moet valideren Hallo `aud` claim tooensure die Hallo-id-token is uitgegeven voor uw app. De waarde moet Hallo toepassings-ID van uw app.
* U moet valideren Hallo `iat` en `exp` claims tooensure die Hallo token ID niet is verlopen.

Er zijn ook enkele meer validaties die moeten worden uitgevoerd. Deze worden beschreven in Hallo [OpenID Connect Core Spec](http://openid.net/specs/openid-connect-core-1_0.html).  U kunt ook aanvullende claims toovalidate, afhankelijk van uw scenario. Sommige algemene validaties zijn onder andere:

* Ervoor te zorgen dat de organisatie van de gebruiker/Hallo heeft aangemeld voor Hallo-app.
* Ervoor te zorgen dat gebruiker Hallo juiste autorisatie/bevoegdheden heeft.
* Ervoor zorgen dat een bepaalde sterkte van verificatie heeft plaatsgevonden, zoals Azure multi-factor Authentication.

Zie voor meer informatie over claims in een token ID Hallo Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).

Nadat u Hallo-id-token hebt gevalideerd, kunt u een sessie beginnen met Hallo-gebruiker. Kunt u Hallo claims in Hallo ID token tooobtain informatie over Hallo gebruiker in uw app. Gebruikt voor deze gegevens omvatten weergeven, records en autorisatie.

## <a name="get-a-token"></a>Een token ophalen
Als u moet uw web-app tooonly beleid uitvoeren, kunt u overslaan Hallo van de volgende secties. Deze secties zijn van toepassing alleen tooweb-apps die u moeten toomake geverifieerde aanroepen tooa web-API en zijn ook beveiligd door Azure AD B2C.

U kunt de autorisatiecode Hallo die u hebt verkregen inwisselen (met behulp van `response_type=code+id_token`) voor een token toohello gewenst resource door te sturen een `POST` toohello aanvragen `/token` eindpunt. Hallo is alleen resource die u kunt een token voor aanvragen momenteel uw web-API van de back-end in de app. Hallo-conventie voor het aanvragen van een token tooyourself is toouse van uw app-client-ID als Hallo bereik:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| P |Vereist |beleid dat gebruikt tooacquire Hallo autorisatie is Hallo code. U kunt een ander beleid niet gebruiken in deze aanvraag. U deze parameter toohello queryreeks, niet toohello toevoegen `POST` hoofdtekst. |
| client_id |Vereist |Hallo toepassing-ID die Hallo [Azure-portal](https://portal.azure.com/) tooyour app toegewezen. |
| grant_type |Vereist |type grant moet Hallo `authorization_code` voor Hallo-autorisatiecodestroom. |
| Bereik |Aanbevolen |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide machtigingen die worden aangevraagd. Hallo `openid` bereik geeft aan dat een machtiging toosign in Hallo gebruiker en get-gegevens over de gebruiker Hallo Hallo vorm van id_token parameters. Het gebruikte tooget tokens tooyour van app back-end-web-API, die wordt vertegenwoordigd door Hallo kan ook dezelfde toepassings-ID als Hallo-client. Hallo `offline_access` bereik geeft aan dat uw app een vernieuwingstoken voor lange levensduur hebben toegang tot tooresources nodig. |
| code |Vereist |Hallo autorisatie-code die u hebt verkregen in de eerste arm Hallo van Hallo stroom. |
| redirect_uri |Vereist |Hallo `redirect_uri` parameter van Hallo toepassing waar u de autorisatiecode Hallo ontvangen. |
| client_secret |Vereist |Hallo-toepassingsgeheim die u hebt gegenereerd in Hallo [Azure-portal](https://portal.azure.com/). Deze toepassing geheime sleutel is een belangrijke beveiligingsupdate artefact. U moet het veilig opslaan op uw server. U moet ook deze clientgeheim periodiek draaien. |

Een geslaagde reactie token ziet eruit als:

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
| token_type |Hallo type token waarde. Hallo alleen type dat ondersteunt Azure AD `Bearer`. |
| access_token |Hallo ondertekend JWT-token dat u hebt aangevraagd. |
| Bereik |Hallo scopes voor welke Hallo-token ongeldig is. Deze kunnen worden gebruikt voor het opslaan van tokens voor later gebruik. |
| expires_in |Hallo tijdsduur die Hallo toegangstoken is ongeldig (in seconden). |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo-app kunt dit token tooacquire extra tokens gebruiken nadat Hallo huidige token is verlopen. Vernieuwen van tokens worden lange levensduur en gebruikte tooretain toegang tooresources voor langere tijd kan worden. Raadpleeg voor meer informatie, toohello [B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). U moet hebben gebruikt Hallo bereik `offline_access` in Hallo autorisatie en -token aanvragen in volgorde tooreceive een vernieuwingstoken. |

Foutberichten ziet er als:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks foutcode die kan worden gebruikt tooclassify typen fouten die optreden en die kan worden gebruikt tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

## <a name="use-hello-token"></a>Hallo-token gebruiken
Nu dat u hebt een toegangstoken is verkregen, kunt u Hallo-token in aanvragen tooyour back-end web-API's door deze in Hallo `Authorization` header:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Hallo-token te vernieuwen
ID-tokens zijn tijdelijke. Nadat ze zijn verlopen toocontinue kunnen tooaccess resources wordt, moet u deze vernieuwen. U kunt dit doen door het indienen van een andere `POST` toohello aanvragen `/token` eindpunt. Deze tijd bieden Hallo `refresh_token` parameter in plaats van Hallo `code` parameter:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Parameter | Vereist | Beschrijving |
| --- | --- | --- |
| P |Vereist |Hallo-beleid dat gebruikt tooacquire Hallo oorspronkelijke vernieuwingstoken is. U kunt een ander beleid niet gebruiken in deze aanvraag. Houd er rekening mee dat u deze parameter toohello queryreeks, niet toohello POST hoofdtekst toevoegt. |
| client_id |Vereist |Hallo toepassing-ID die Hallo [Azure-portal](https://portal.azure.com/) tooyour app toegewezen. |
| grant_type |Vereist |Verleen dit een vernieuwingstoken voor deze fase van de autorisatiecodestroom Hallo moet Hallo type. |
| Bereik |Aanbevolen |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide machtigingen die worden aangevraagd. Hallo `openid` bereik geeft aan dat een machtiging toosign in Hallo gebruiker en get-gegevens over Hallo-gebruiker in de vorm Hallo van ID-tokens. Het gebruikte tooget tokens tooyour van app back-end-web-API, die wordt vertegenwoordigd door Hallo kan ook dezelfde toepassings-ID als Hallo-client. Hallo `offline_access` bereik geeft aan dat uw app een vernieuwingstoken voor lange levensduur hebben toegang tot tooresources nodig. |
| redirect_uri |Aanbevolen |Hallo `redirect_uri` parameter van Hallo toepassing waar u de autorisatiecode Hallo ontvangen. |
| refresh_token |Vereist |Hallo oorspronkelijke vernieuwingstoken die u hebt verkregen in de tweede arm Hallo van Hallo stroom. U moet hebben gebruikt Hallo bereik `offline_access` in Hallo autorisatie en -token aanvragen in volgorde tooreceive een vernieuwingstoken. |
| client_secret |Vereist |Hallo-toepassingsgeheim die u hebt gegenereerd in Hallo [Azure-portal](https://portal.azure.com/). Deze toepassing geheime sleutel is een belangrijke beveiligingsupdate artefact. U moet het veilig opslaan op uw server. U moet ook deze clientgeheim periodiek draaien. |

Een geslaagde reactie token ziet eruit als:

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
| token_type |Hallo type token waarde. Hallo alleen type dat ondersteunt Azure AD `Bearer`. |
| access_token |Hallo ondertekend JWT-token dat u hebt aangevraagd. |
| Bereik |Hallo-bereik dat Hallo token is geldig voor, die kan worden gebruikt voor het opslaan van tokens voor later gebruik. |
| expires_in |Hallo tijdsduur die Hallo toegangstoken is ongeldig (in seconden). |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo-app kunt dit token tooacquire extra tokens gebruiken nadat Hallo huidige token is verlopen.  Vernieuwen van tokens worden lange levensduur en gebruikte tooretain toegang tooresources voor langere tijd kan worden. Raadpleeg voor meer details toohello [B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). |

Foutberichten ziet er als:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks foutcode die kan worden gebruikt tooclassify typen fouten die optreden en die kan worden gebruikt tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

## <a name="send-a-sign-out-request"></a>Afmelden aanvraag verzenden
Als u wilt dat toosign Hallo gebruiker buiten het Hallo-app, is niet voldoende tooclear cookies van uw app of anders Hallo-sessie met Hallo gebruiker beëindigen. U moet ook omleiden Hallo gebruiker tooAzure AD toosign uit. Als u toodo zo niet, mogelijk Hallo gebruiker kunnen tooreauthenticate tooyour app zonder hun referenties opnieuw invoeren. Dit komt doordat er een geldige eenmalige aanmelding sessie met Azure AD.

U kunt eenvoudig hello gebruiker toohello omleiden `end_session` eindpunt dat wordt weergegeven in het document met OpenID Connect Hallo metagegevens die eerder in Hallo sectie 'Hello ID token valideren' worden beschreven:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| P |Vereist |Hallo-beleid dat u wilt dat toouse toosign Hallo gebruiker buiten uw toepassing. |
| post_logout_redirect_uri |Aanbevolen |Hallo-URL die gebruiker Hallo moet omgeleide tooafter geslaagde afmelding plaatsvindt. Als dit niet opgenomen is, geeft Azure AD B2C Hallo gebruiker een algemeen foutbericht. |

> [!NOTE]
> Hoewel doorsturen Hallo gebruiker toohello `end_session` eindpunt aantal Hallo status van gebruiker eenmalige aanmelding met Azure AD B2C wordt gewist, ondertekent geen Hallo gebruiker buiten hun sessie sociale identity-provider (IDP). Als Hallo gebruiker selecteert Hallo van dezelfde IDP tijdens een volgende aanmelden, ze zal worden geverifieerd, zonder dat hun referenties invoeren. Als een gebruiker wil toosign buiten uw B2C-toepassing, betekent het niet noodzakelijkerwijs dat hij of zij wil toosign buiten hun Facebook-account. Echter, in geval van lokale accounts Hallo Hallo gebruikerssessie wordt beëindigd goed.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Gebruik uw eigen B2C-tenant
Als u deze aanvragen tootry voor uzelf wilt, moet u eerst deze drie stappen uitvoeren en vervolgens vervangen Hallo voorbeelden van waarden die eerder zijn beschreven door uw eigen:

1. [Maken van een B2C-tenant](active-directory-b2c-get-started.md), en Hallo-naam van uw tenant gebruiken in Hallo aanvragen.
2. [Maken van een toepassing](active-directory-b2c-app-registration.md) tooobtain een toepassings-ID. Een web-app of web-API opnemen in uw app. Maak eventueel een toepassingsgeheim.
3. [Maken van uw beleid](active-directory-b2c-reference-policies.md) tooobtain de beleidsnamen van uw.

