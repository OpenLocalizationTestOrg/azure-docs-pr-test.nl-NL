---
title: 'Azure Active Directory B2C: Single-page-apps met behulp van de impliciete stroom | Microsoft Docs'
description: "Meer informatie over hoe toobuild één pagina apps rechtstreeks met behulp van OAuth 2.0 impliciete stromen met Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C: Single-page-app aanmelden met behulp van de impliciete OAuth 2.0-stroom

> [!NOTE]
> Deze functie is in preview.
> 

Veel moderne apps hebben een front-end app met één pagina die voornamelijk in JavaScript is geschreven. Hallo-app is vaak geschreven met behulp van een framework zoals AngularJS, Ember.js of Durandal. Apps van één pagina en andere JavaScript-apps die worden uitgevoerd in een browser voornamelijk hebt enkele aanvullende uitdagingen voor verificatie:

* Hallo-beveiligingskenmerken van deze apps zijn aanzienlijk anders dan traditionele webtoepassingen op basis van een server.
* Veel autorisatieservers en id-providers bieden geen ondersteuning voor cross-origin-resources (CORS) aanvragen om te delen.
* Volledige pagina browser omleidingen weg Hallo app kunnen aanzienlijk Invasief toohello gebruikerservaring zijn.

toosupport deze toepassingen, Azure Active Directory B2C (Azure AD B2C) impliciete Hallo OAuth 2.0-stroom wordt gebruikt. Hallo OAuth 2.0 autorisatie impliciete grant stroom wordt beschreven in [sectie 4.2 van Hallo OAuth 2.0-specificatie](http://tools.ietf.org/html/rfc6749). In impliciete stroom Hallo app-tokens rechtstreeks van ontvangen hello Azure Active Directory (Azure AD) autoriseren eindpunt, zonder eventuele exchange server-naar-server. Alle verificatielogica en sessie afhandeling van vindt volledig in Hallo JavaScript client zonder aanvullende paginaomleidingen plaatsen.

Azure AD B2C breidt Hallo standaard OAuth 2.0 impliciete stroom toomore dan eenvoudige verificatie en autorisatie. Azure AD B2C introduceert Hallo [Beleidsparameter](active-directory-b2c-reference-policies.md). Met de parameter van het beleid hello, kunt u OAuth 2.0 tooadd gebruiker merkt dat tooyour app, zoals aanmelding, aanmelding en Profielbeheer. In dit artikel zien we u hoe toouse Hallo impliciete stroom en Azure AD tooimplement, elk van deze ervaringen in uw toepassingen met één pagina. toohelp die u aan de slag, Bekijk onze [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) en [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) voorbeelden.

In voorbeeld HTTP-aanvragen Hallo in dit artikel, gebruiken we onze voorbeeld Azure AD B2C-directory **fabrikamb2c.onmicrosoft.com**. We gebruiken ook onze eigen voorbeeldtoepassing en het beleid. U kunt aanvragen Hallo zelf met behulp van deze waarden, of kunt u deze vervangen door uw eigen waarden.
Meer informatie over hoe te[ophalen van uw eigen Azure AD B2C-directory, toepassingen en beleidsregels](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Protocol-diagram

impliciete Hallo aanmelden stroom lijkt op Hallo volgende afbeelding. Elke stap wordt beschreven in artikel Hallo in detail.

![OpenID Connect banen](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Verificatieaanvragen verzenden
Wanneer uw web-app moet tooauthenticate Hallo gebruiker en uitvoeren van een beleid, stuurt het Hallo gebruiker toohello `/authorize` eindpunt. Dit is Hallo interactieve gedeelte van de stroom Hallo, waar Hallo gebruiker optreden, afhankelijk van Hallo beleid plaatsvindt. Hallo gebruiker ontvangt een ID-token van hello Azure AD-eindpunt.

In deze aanvraag Hallo-client geeft aan in Hallo `scope` parameter Hallo machtigingen dat het moet tooacquire van Hallo-gebruiker. In Hallo `p` parameter, betekent dit Hallo beleid tooexecute. Hallo gebruik volgende drie voorbeelden (met regeleinden voor leesbaarheid) elk een ander beleid. tooget een idee voor hoe elke aanvraag werkt, probeer plakken Hallo aanvraag in een browser en het uitvoeren.

### <a name="use-a-sign-in-policy"></a>Een beleid voor aanmelden gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Een registratiebeleid gebruiken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Gebruik van een beleid voor het profiel bewerken
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassings-ID toegewezen tooyour-app in Hallo [Azure-portal](https://portal.azure.com). |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden. Kan het ook Hallo antwoordtype bevatten `token`. Als u `token`, uw app kunt onmiddellijk een toegangstoken van Hallo ontvangen autoriseren eindpunt, zonder dat een tweede aanvraag toohello eindpunt autoriseren.  Als u Hallo `token` antwoordtype, Hallo `scope` parameter moet een scope die aangeeft welke resource tooissue Hallo token voor bevatten. |
| redirect_uri |Aanbevolen |Hallo omleidings-URI van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app. Deze moet exact overeenkomen met een van Hallo omleidings-URI's die u hebt geregistreerd in Hallo-portal, behalve dat het URL-codering moet worden. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo methode toouse toosend Hallo resulterende token back tooyour app.  Gebruik voor impliciete stromen `fragment`. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken. De waarde één scope geeft tooAzure AD beide Hallo machtigingen die worden aangevraagd. Hallo `openid` bereik geeft aan dat een machtiging toosign in Hallo gebruiker en get-gegevens over Hallo-gebruiker in de vorm Hallo van ID-tokens. (Bespreken we dit later in Hallo artikel.) Hallo `offline_access` bereik is optioneel voor web-apps. Hiermee wordt aangegeven dat uw app een vernieuwingstoken voor de lange levensduur hebben toegang tot tooresources moet. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in Hallo token antwoord wordt geretourneerd. Een tekenreeks van alle inhoud die u wilt dat toouse kan zijn. Normaal gesproken een willekeurig gegenereerde unieke waarde wordt gebruikt, tooprevent aanvraagvervalsing op meerdere sites aanvallen. Hallo status wordt ook gebruikt tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals Hallo pagina ze waren op. |
| nonce |Vereist |Een waarde die is opgenomen in het Hallo-aanvraag (gegenereerd door Hallo app) die is opgenomen in het resulterende ID token Hallo als een claim. Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen. Hallo-waarde is meestal een willekeurige, unieke tekenreeks die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| P |Vereist |Hallo beleid tooexecute. De Hallo naam van een beleid dat is gemaakt in uw Azure AD B2C-tenant. Hallo-beleidswaarde naam moet beginnen met **b2c\_1\_**. Zie voor meer informatie [ingebouwde beleid van Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Optioneel |Hallo type gebruikersinteractie die vereist zijn. De enige geldige waarde Hallo is momenteel `login`. Dit zorgt ervoor dat Hallo gebruiker tooenter hun referenties voor deze aanvraag. Eenmalige aanmelding wordt pas van kracht. |

Op dit moment hello wordt u gevraagd toocomplete Hallo beleid werkstroom. Dit kan erbij betrekken Hallo gebruikers voeren hun gebruikersnaam en wachtwoord, aanmelden met een sociale identiteit aanmelden voor Hallo directory of een andere aantal stappen. Acties van de gebruiker is afhankelijk van hoe Hallo beleid is gedefinieerd.

Nadat het Hallo gebruiker voltooit Hallo-beleid, Azure AD retourneert een antwoord tooyour app op Hallo-waarde die u gebruikt voor `redirect_uri`. Hierbij Hallo methode in Hallo `response_mode` parameter. Hallo-antwoord is precies dezelfde Hallo voor elk Hallo actie gebruikersscenario, onafhankelijk van het Hallo-beleid dat is uitgevoerd.

### <a name="successful-response"></a>Geslaagde reactie
Een geslaagde reactie die gebruikmaakt van `response_mode=fragment` en `response_type=id_token+token` vergelijkbaar is met de volgende hello, met regeleinden beter leesbaar:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo-toegangstoken dat Hallo app aangevraagd.  Hallo toegangstoken moet niet worden gedecodeerd of anders geïnspecteerd. Het kan worden behandeld als één tekenreeks. |
| token_type |Hallo type token waarde. Hallo alleen typen dat ondersteunt Azure AD Bearer is. |
| expires_in |Hallo tijdsduur die Hallo toegangstoken is ongeldig (in seconden). |
| Bereik |Hallo-scopes die Hallo token is geldig voor. U kunt ook scopes toocache tokens gebruiken voor later gebruik. |
| id_token |Hallo ID-token dat Hallo app aangevraagd. U kunt gebruiken Hallo ID token tooverify Hallo gebruikers id en beginnen met een sessie met de Hallo-gebruiker. Zie voor meer informatie over het ID-tokens en de inhoud ervan Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). |
| state |Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |

### <a name="error-response"></a>Foutbericht
Foutberichten kunnen ook worden verzonden toohello omleidings-URI zodat hello app ze op de juiste wijze verwerken kan:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een code fouttekenreeks gebruikt tooclassify typen fouten die optreden. U kunt ook foutcode hello gebruiken voor foutafhandeling. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |
| state |Volledige beschrijving van de Hallo in de voorgaande tabel Hallo bekijken. Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn.|

## <a name="validate-hello-id-token"></a>Hallo-id-token valideren
Ontvangen van een token ID is niet voldoende tooauthenticate Hallo-gebruiker. U moet Hallo-ID van het token handtekening valideren en controleren Hallo claims in Hallo token per vereisten van uw app. Maakt gebruik van Azure AD B2C [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) en openbare sleutel-cryptografie toosign tokens en controleer of ze geldig zijn.

Veel open source-bibliotheken zijn beschikbaar voor het valideren van JWTs, afhankelijk van de taal Hallo gewenste toouse. U kunt verkennen beschikbaar open source-bibliotheken in plaats van uw eigen validatielogica implementeren. Hallo informatie kunt u in de toohelp van dit artikel leert u hoe tooproperly die bibliotheken gebruiken.

Azure AD B2C heeft een eindpunt met OpenID Connect metagegevens. Een app kan Hallo eindpunt toofetch informatie over Azure AD B2C in runtime gebruiken. Deze informatie omvat eindpunten, inhoud van tokens en token-ondertekening sleutels. Er is een JSON-metagegevens-document voor elk beleid in uw Azure AD B2C-tenant. Bijvoorbeeld, bevindt Hallo metagegevensdocument voor Hallo b2c_1_sign_in beleid in Hallo fabrikamb2c.onmicrosoft.com tenant zich op:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Een van de Hallo eigenschappen van dit document configuratie Hallo is `jwks_uri`. Hallo-waarde voor de Hallo hetzelfde beleid zijn:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine welk beleid gebruikte toosign een token ID is (en waar toofetch metagegevens uit Hallo), hebt u twee opties. Eerst Hallo beleidsnaam is opgenomen in Hallo `acr` claim in `id_token`. Zie voor informatie over hoe tooparse Hallo claims van een token ID Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md). De andere mogelijkheid is tooencode Hallo beleid in Hallo-waarde van Hallo `state` parameter wanneer u Hallo aanvraag verzendt. Vervolgens decoderen Hallo `state` parameter toodetermine welk beleid is gebruikt. Beide methoden is geldig.

Nadat u Hallo metagegevensdocument van metagegevens-eindpunt met OpenID Connect Hallo hebt aangeschaft, kunt u Hallo RSA-256 openbare sleutels (dat zich op dit eindpunt) toovalidate Hallo handtekening van Hallo-ID-token. Er is mogelijk meerdere sleutels die worden vermeld op dit eindpunt op elk moment kunt herkennen aan een `kid`. Hallo-koptekst van `id_token` bevat ook een `kid` claim. Hiermee wordt aangegeven welke van deze sleutels gebruikte toosign Hallo-id-token is. Voor meer informatie, waaronder informatie over [valideren van tokens](active-directory-b2c-reference-tokens.md#token-validation), Zie Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Nadat u Hallo handtekening van Hallo ID token valideert, vereisen meerdere claims verificatie. Bijvoorbeeld:

* Hallo valideren `nonce` claim tooprevent token replay-aanvallen. De waarde moet Hallo aanmeldingsverzoek wat u hebt opgegeven.
* Hallo valideren `aud` claim tooensure die Hallo-id-token is uitgegeven voor uw app. De waarde moet Hallo toepassings-ID van uw app.
* Hallo valideren `iat` en `exp` claims tooensure die Hallo token ID niet is verlopen.

Verschillende meer validaties die moeten worden uitgevoerd zijn beschreven in Hallo [OpenID Connect Core Spec](http://openid.net/specs/openid-connect-core-1_0.html). U kunt ook aanvullende claims toovalidate, afhankelijk van uw scenario. Sommige algemene validaties zijn onder andere:

* Ervoor te zorgen dat Hallo gebruiker of organisatie heeft aangemeld voor Hallo-app.
* Ervoor te zorgen dat Hallo gebruiker heeft de juiste autorisatie en bevoegdheden.
* Ervoor te zorgen dat een bepaalde sterkte van verificatie heeft plaatsgevonden, zoals zoals met behulp van Azure multi-factor Authentication.

Zie voor meer informatie over claims in een token ID Hallo Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).

Nadat u hebt Hallo ID token volledig gevalideerd, kunt u een sessie beginnen met Hallo-gebruiker. Gebruik in uw app Hallo claims in Hallo ID token tooobtain informatie over Hallo gebruiker. Deze informatie kan worden gebruikt voor weergave, registreert en autorisatie.

## <a name="get-access-tokens"></a>Toegangstokens ophalen
Als het beleid worden Hallo enige dat uw web-apps behoeften toodo is uitgevoerd, kunt u overslaan Hallo van de volgende secties. Hallo-informatie in de volgende secties Hallo zijn van toepassing alleen tooweb apps die moeten toomake geverifieerde aanroepen tooa web-API en die worden beveiligd door Azure AD B2C.

Nu dat u hebt zich Hallo-gebruiker in tooyour één pagina app, kunt u toegangstokens ophalen voor het aanroepen van web API's die zijn beveiligd door Azure AD. Zelfs als u al een token hebt ontvangen met behulp van Hallo `token` antwoordtype, kunt u deze methode tooacquire tokens voor aanvullende bronnen zonder het omleiden van Hallo gebruiker toosign in opnieuw.

In een typische web-app-stroom u doet dit door het maken van een aanvraag toohello `/token` eindpunt.  Hallo-eindpunt biedt echter geen ondersteuning voor CORS aanvragen, zodat tooget waardoor AJAX-aanroepen en vernieuwen van tokens kan niet worden gebruikt. U kunt in plaats daarvan Hallo impliciete stroom gebruiken in een verborgen HTML iframe-element tooget nieuwe tokens voor andere web-API's. Hier volgt een voorbeeld: met regeleinden beter leesbaar:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassings-ID toegewezen tooyour-app in Hallo [Azure-portal](https://portal.azure.com). |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden.  Het kan ook betekenen dat Hallo antwoordtype `token`. Als u `token` hier uw app kunt onmiddellijk een toegangstoken van ontvangen Hallo autoriseren eindpunt, zonder dat een tweede aanvraag toohello eindpunt autoriseren. Als u Hallo `token` antwoordtype, Hallo `scope` parameter moet een scope die aangeeft welke resource tooissue Hallo token voor bevatten. |
| redirect_uri |Aanbevolen |Hallo omleidings-URI van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app. Deze moet exact overeenkomen met een van Hallo omleidings-URI's die u in Hallo-portal hebt geregistreerd, behalve dat het URL-codering moet worden. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Omvatten alle scopes die u nodig voor de resource Hallo bedoeld hebt voor het ophalen van tokens. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die is gebruikt toosend Hallo resulterende token back tooyour-app.  Kan `query`, `form_post`, of `fragment`. |
| state |Aanbevolen |Een waarde die is opgenomen in het Hallo-aanvraag die wordt geretourneerd als antwoord van Hallo-token.  Een tekenreeks van alle inhoud die u wilt dat toouse kan zijn.  Normaal gesproken een willekeurig gegenereerde unieke waarde wordt gebruikt, tooprevent aanvraagvervalsing op meerdere sites aanvallen.  Hallo-status is ook gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat het Hallo-verificatieaanvraag is opgetreden. Hallo pagina of weergave Hallo gebruiker is bijvoorbeeld op. |
| nonce |Vereist |Een waarde die is opgenomen in de aanvraag hello, die worden gegenereerd door Hallo-app die is opgenomen in het resulterende ID token Hallo als een claim.  Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen. Hallo-waarde is meestal een willekeurige, unieke tekenreeks die Hallo oorsprong van Hallo-aanvraag aanduidt. |
| prompt |Vereist |toorefresh en get-tokens in een verborgen iframe gebruiken `prompt=none` tooensure die iframe Hallo komt niet op de aanmeldingspagina Hallo hangen en wordt onmiddellijk geretourneerd. |
| login_hint |Vereist |gebruikersnaam van de gebruiker Hallo Hallo opnemen toorefresh en get-tokens in een verborgen iframe in deze hint toodistinguish tussen meerdere sessies Hallo gebruiker heeft mogelijk op een bepaald moment. U kunt Hallo gebruikersnaam extraheren uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Vereist |Kan `consumers` of `organizations`.  Vernieuwen en ophalen van tokens in een verborgen iframe, moet u opnemen Hallo `domain_hint` waarde in Hallo-aanvraag.  Hallo extraheren `tid` claim uit Hallo-ID-token van een eerder aanmelden toodetermine welke toouse waarde.  Als hello `tid` claim waarde is `9188040d-6c67-4c5b-b112-36a304b66dad`, gebruik `domain_hint=consumers`.  Gebruik anders `domain_hint=organizations`. |

Door de instelling Hallo `prompt=none` parameter, deze aanvraag ofwel slaagt of mislukt onmiddellijk en retourneert tooyour toepassing.  Een geslaagde reactie wordt verzonden tooyour app op Hallo aangegeven omleidings-URI, met behulp van de methode in Hallo Hallo `response_mode` parameter.

### <a name="successful-response"></a>Geslaagde reactie
Een geslaagde reactie met behulp van `response_mode=fragment` ziet er als volgt:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo-token dat Hallo app aangevraagd. |
| token_type |Hallo tokentype worden altijd Bearer. |
| state |Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat Hallo `state` waarden in Hallo-aanvraag en -antwoord identiek zijn. |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| Bereik |Hallo-scopes die Hallo toegangstoken is geldig voor. |

### <a name="error-response"></a>Foutbericht
Foutberichten kunnen ook worden verzonden toohello omleidings-URI zodat hello app kan ze op juiste manier verwerken.  Voor `prompt=none`, een verwachte fout ziet er als volgt:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die kan worden gebruikt tooclassify typen fouten die optreden. U kunt ook Hallo tekenreeks tooreact tooerrors gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |

Als u deze fout in Hallo iframe aanvraag ontvangt, moet Hallo gebruiker interactief aanmelden opnieuw tooretrieve een nieuw token. U kunt dit op een manier die zinvol is voor uw toepassing verwerkt.

## <a name="refresh-tokens"></a>Vernieuwen van tokens
ID-tokens en toegangstokens verlopen na een korte periode. Uw app moet deze regelmatig tokens toorefresh worden voorbereid.  toorefresh beide typen token, voeren dezelfde verborgen iframe-aanvraag wordt gebruikt in een eerdere bijvoorbeeld met behulp van Hallo Hallo `prompt=none` parameter toocontrol Azure AD stappen.  tooreceive een nieuwe `id_token` waarde, kunnen ervoor toouse `response_type=id_token` en `scope=openid`, en een `nonce` parameter.

## <a name="send-a-sign-out-request"></a>Afmelden aanvraag verzenden
Als u wilt dat toosign Hallo gebruiker buiten de app Hallo omleiden Hallo gebruiker tooAzure AD toosign uit. Als u dit doet, is het Hallo gebruiker mogelijk kunnen tooreauthenticate tooyour app zonder hun referenties opnieuw invoeren. Dit komt doordat er een geldige eenmalige aanmelding sessie met Azure AD.

U kunt eenvoudig hello gebruiker toohello omleiden `end_session_endpoint` is opgenomen in Hallo hetzelfde OpenID Connect metagegevensdocument wordt beschreven in [valideren Hallo ID token](#validate-the-id-token). Bijvoorbeeld:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parameter | Vereist? | Beschrijving |
| --- | --- | --- |
| P |Vereist |Hallo beleid toouse toosign Hallo gebruiker buiten uw toepassing. |
| post_logout_redirect_uri |Aanbevolen |Hallo-URL die gebruiker Hallo moet omgeleide tooafter geslaagde afmelding plaatsvindt. Als dit niet opgenomen is, wordt een algemeen bericht toohello gebruiker weergegeven in Azure AD B2C. |

> [!NOTE]
> Hallo gebruiker toohello doorsturen `end_session_endpoint` aantal Hallo status van gebruiker eenmalige aanmelding met Azure AD B2C wordt gewist. Echter ondertekenen niet het Hallo-gebruiker buiten Hallo sociale identiteit provider gebruikerssessie. Als Hallo gebruiker selecteert Hallo dezelfde provider identificeren tijdens een volgende aanmelden, Hallo gebruiker is geverifieerd, zonder dat hun referenties invoeren. Als een gebruiker wil toosign buiten uw Azure AD B2C-toepassing, betekent het niet noodzakelijkerwijs dat ze bijvoorbeeld toocompletely Meld u af bij hun account Facebook willen. Echter, voor lokale accounts Hallo gebruikerssessie wordt beëindigd goed.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Gebruik uw eigen Azure AD B2C-tenant
Deze aanvragen zelf voltooien tootry Hallo drie stappen te volgen. Vervang de voorbeeldwaarden hello we in dit artikel met uw eigen waarden gebruiken:

1. [Een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md). Hallo-naam van uw tenant gebruiken in Hallo aanvragen.
2. [Maken van een toepassing](active-directory-b2c-app-registration.md) tooobtain een toepassings-ID en een `redirect_uri` waarde. Een web-app of web-API opnemen in uw app. U kunt desgewenst een toepassingsgeheim maken.
3. [Maken van uw beleid](active-directory-b2c-reference-policies.md) tooobtain de beleidsnamen van uw.

## <a name="samples"></a>Voorbeelden

* [Een app één pagina maken met behulp van Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Een app één pagina maken met behulp van .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

