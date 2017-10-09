---
title: aaaAzure Active Directory v2.0 en Hallo OpenID Connect-protocol | Microsoft Docs
description: Webtoepassingen bouwen met behulp van hello Azure AD v2.0-implementatie van Hallo OpenID Connect-verificatieprotocol.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 en Hallo OpenID Connect-protocol
OpenID Connect, is een authenticatieprotocol die is gebaseerd op OAuth 2.0 die u in een webtoepassing voor gebruiker tooa toosecurely aanmelding kunt gebruiken. Wanneer u Hallo v2.0-eindpunt van implementatie van OpenID Connect gebruikt, kunt u aanmelden en API toegang tooyour web gebaseerde apps kunt toevoegen. In dit artikel wordt uitgelegd hoe u dat dit taalonafhankelijke toodo. We beschrijven hoe toosend en HTTP-berichten ontvangen zonder gebruik van alle Microsoft open source-bibliotheken.

> [!NOTE]
> Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen. toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) breidt Hallo OAuth 2.0 *autorisatie* protocol toouse als een *verificatie* protocol, zodat u één uitvoeren kunt aanmelding met OAuth. Hallo-concept van OpenID Connect introduceert een *token ID*, dit is een beveiligingstoken waarmee Hallo client tooverify Hallo identiteit van Hallo-gebruiker. Hallo-id-token wordt ook informatie over Hallo gebruiker basisprofiel. Omdat OpenID Connect OAuth 2.0 breidt, apps veilig kunnen verkrijgen *toegang tot tokens*, wat kan zijn gebruikte tooaccess resources die zijn beveiligd met een [autorisatie server](active-directory-v2-protocols.md#the-basics). Het is raadzaam dat u OpenID Connect als u een [webtoepassing](active-directory-v2-flows.md#web-apps) die wordt gehost op een server en geopend via een browser.

## Protocol diagram: aanmelden
Hallo heeft meest eenvoudige aanmelding-stroom Hallo stappen in het volgende diagram Hallo. Elke stap in detail in dit artikel worden beschreven.

![Protocol OpenID Connect: aanmelden](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Hallo OpenID Connect metagegevensdocument ophalen
Beschrijving van een document met metagegevens die de meeste van Hallo vereiste informatie voor een app tooperform aanmelden bevat OpenID Connect. Dit omvat gegevens zoals Hallo URL's toouse en Hallo-locatie van de openbare handtekeningsleutels Hallo-service. Dit is Hallo OpenID Connect metagegevensdocument die moet u voor Hallo-v2.0-eindpunt:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Hallo `{tenant}` kan duren voordat een van de vier waarden:

| Waarde | Beschrijving |
| --- | --- |
| `common` |Gebruikers met een persoonlijk Microsoft-account en een account voor werk of school van Azure Active Directory (Azure AD) kunnen toohello toepassing aanmelden. |
| `organizations` |Alleen gebruikers met een werk- of schoolaccounts van Azure AD toohello toepassing kunnen aanmelden. |
| `consumers` |Alleen gebruikers met een persoonlijk Microsoft-account kunnen toohello toepassing aanmelden. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` of `contoso.onmicrosoft.com` |Alleen gebruikers met een werk- of schoolaccount van een specifieke Azure AD tenant toohello toepassing kunt aanmelden. Een beschrijvende domeinnaam Hallo van hello Azure AD-tenant of GUID-id van Hallo tenant kan worden gebruikt. |

Hallo metagegevens is een eenvoudige JSON JavaScript Object Notation ()-document. Zie Hallo codefragment voor een voorbeeld te volgen. Hallo inhoud van het codefragment worden volledig beschreven in Hallo [specificatie van het OpenID Connect](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Doorgaans wilt u deze metagegevens document tooconfigure OpenID Connect-bibliotheek of SDK; Hallo-bibliotheek zou Hallo metagegevens toodo het werk gebruiken. Als u een vooraf build OpenID Connect-bibliotheek niet gebruikt, kunt u stappen echter Hallo Hallo rest van dit artikel tooperform aanmelden in een web-app met behulp van Hallo v2.0-eindpunt.

## Hallo aanmelden aanvraag verzenden
Als uw web-app tooauthenticate Hallo gebruiker moet, Hallo gebruiker toohello kan worden doorgestuurd `/authorize` eindpunt. Deze aanvraag is vergelijkbaar toohello eerste arm van Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols-oauth-code.md), met deze belangrijke verschillen:

* Hallo aanvraag vergezeld gaan van Hallo `openid` bereik in Hallo `scope` parameter.
* Hallo `response_type` vergezeld gaan van de parameter `id_token`.
* Hallo aanvraag vergezeld gaan van Hallo `nonce` parameter.

Bijvoorbeeld:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Klik op Hallo koppeling tooexecute na deze aanvraag. Nadat u zich aanmeldt, worden uw browser omgeleide toohttps://localhost/myapp/, met een token ID in de adresbalk Hallo. Let op: maakt gebruik van deze aanvraag `response_mode=query` (voor demonstratiedoeleinden alleen). Het is raadzaam dat u `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parameter | Voorwaarde | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |U kunt Hallo `{tenant}` waarde in het Hallo-pad van Hallo aanvraag toocontrol die toohello toepassing kunt aanmelden. Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's. Zie voor meer informatie [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassing-ID die Hallo [toepassing Registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour app toegewezen. |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden. Het kan ook betekenen dat andere `response_types` waarden, zoals `code`. |
| redirect_uri |Aanbevolen |Hallo omleidings-URI van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app. Deze moet exact overeenkomen met een Hallo redirect URI's u geregistreerd in het Hallo-portal, behalve dat deze URL moet worden gecodeerd. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken. Voor het OpenID Connect, het Hallo-bereik omvat `openid`, toohello 'Aanmelden u' machtiging in Hallo toestemming gebruikersinterface, wat overeenkomt. U kunt ook andere bereiken opnemen in deze aanvraag voor toestemming wordt gevraagd. |
| nonce |Vereist |Een waarde die is opgenomen in de aanvraag hello, die worden gegenereerd door Hallo-app, die wordt opgenomen in het resulterende id_token waarde Hallo als een claim. Hallo-app kunt controleren of dat deze waarde toomitigate token replay-aanvallen. Hallo-waarde is meestal een willekeurige, unieke tekenreeks die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende autorisatie code back tooyour app worden moet. Een van `query`, `form_post`, of `fragment`. Voor webtoepassingen, wordt u aangeraden `response_mode=form_post`, tooensure Hallo meest veilige overdracht van tokens tooyour toepassing. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd. Een tekenreeks van alle inhoud die u wilt dat kan zijn. Een willekeurig gegenereerde unieke waarde wordt meestal gebruikt te[aanvraagvervalsing op meerdere sites aanvallen te voorkomen](http://tools.ietf.org/html/rfc6749#section-10.12). Hallo staat ook is gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals Hallo pagina of weergave Hallo gebruiker is op. |
| prompt |Optioneel |Geeft Hallo type gebruikersinteractie is vereist. Hallo op dit moment alleen geldige waarden zijn `login`, `none`, en `consent`. Hallo `prompt=login` claim dwingt Hallo gebruiker tooenter hun referenties op die aanvraag dat eenmalige aanmelding wordt genegeerd. Hallo `prompt=none` claim Hallo tegengestelde is. Deze claim zorgt ervoor dat die Hallo-gebruiker niet vragen beeïndigen krijgt. Als het Hallo-aanvraag kan niet worden voltooid in stille modus via eenmalige aanmelding, Hallo v2.0-eindpunt een fout geretourneerd. Hallo `prompt=consent` claim triggers Hallo OAuth toestemming dialoogvenster nadat Hallo gebruiker zich aanmeldt. Hallo-dialoogvenster wordt u gevraagd Hallo gebruiker toogrant machtigingen toohello app. |
| login_hint |Optioneel |Als u de gebruikersnaam Hallo tevoren weet, kunt u deze parameter toopre opvulling Hallo gebruikersnaam en het e-mailbericht adresveld van de aanmeldingspagina Hallo voor Hallo-gebruiker. Vaak apps deze parameter gebruiken tijdens de hervalidatie nadat u hebt al Hallo gebruikersnaam uitgepakt vanuit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Optioneel |Deze waarde kan zijn `consumers` of `organizations`. Als opgenomen, slaat het Hallo op basis van e-mail detectieproces die gebruiker Hallo doorloopt op Hallo v2.0-aanmeldingspagina, voor een iets meer gestroomlijnde gebruikerservaring. Vaak apps Gebruik deze parameter tijdens het opnieuw verifiëren door te extraheren Hallo `tid` claim uit Hallo-ID-token. Als hello `tid` claim waarde is `9188040d-6c67-4c5b-b112-36a304b66dad`, gebruik `domain_hint=consumers`. Gebruik anders `domain_hint=organizations`. |

Op dit moment Hallo gebruiker is na vragen aan gebruiker tooenter hun referenties en volledige Hallo-verificatie. Hallo v2.0-eindpunt controleert die gebruiker Hallo toohello machtigingen die zijn aangegeven in Hallo heeft ingestemd `scope` queryparameter. Als gebruiker Hallo tooany van deze machtigingen niet heeft ingestemd, vraagt Hallo v2.0-eindpunt tooconsent Hallo-toohello vereist gebruikersmachtigingen. U kunt meer lezen over [machtigingen, toestemming en multitenant apps](active-directory-v2-scopes.md).

Nadat het Hallo-gebruiker wordt geverifieerd en toestemming verleent, Hallo v2.0-eindpunt retourneert een antwoord tooyour app op Hallo aangegeven omleidings-URI met behulp van de methode in Hallo Hallo `response_mode` parameter.

### Geslaagde reactie
Een geslaagde reactie wanneer u `response_mode=form_post` ziet er als volgt:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| id_token |Hallo ID-token dat Hallo app aangevraagd. U kunt Hallo `id_token` parameter tooverify Hallo gebruikers id en wilt beginnen met een sessie met de Hallo-gebruiker. Zie voor meer informatie over het ID-tokens en de inhoud ervan Hallo [v2.0-eindpunt tokens verwijzing](active-directory-v2-tokens.md). |
| state |Als een `state` parameter is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |

### Foutbericht
Foutberichten kunnen ook worden verzonden toohello omleidings-URI zodat hello app kan deze te verwerken. Een foutmelding ziet er als volgt:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u tooclassify typen fouten die optreden en tooreact tooerrors kunt gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |

### Foutcodes voor autorisatie eindpunt fouten
Hallo volgende tabel worden foutcodes beschreven die kunnen worden geretourneerd in Hallo `error` parameter van het Hallo-foutbericht:

| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout ontwikkeling dat meestal wordt onderschept tijdens de eerste test. |
| unauthorized_client |Hallo-clienttoepassing kan niet een autorisatiecode aanvragen. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies tooinstall Hallo toepassing gevraagd en voeg deze tooAzure AD. |
| ACCESS_DENIED |de resource-eigenaar Hallo toestemming geweigerd. |Hallo-clienttoepassing kan melden Hallo-gebruiker die deze kan niet worden voortgezet tenzij Hallo gebruiker hiermee akkoord gaat. |
| unsupported_response_type |Hallo autorisatie server biedt geen ondersteuning voor antwoordtype Hallo Hallo-aanvraag. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout ontwikkeling dat meestal wordt onderschept tijdens de eerste test. |
| server_error |Hallo-server heeft een onverwachte fout aangetroffen. |Hallo aanvraag opnieuw proberen. Deze fouten kunnen worden veroorzaakt door tijdelijke omstandigheden. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke fout. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke situatie. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven dat Hallo resource, indien aanwezig, niet is geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het installeren van de toepassing hello en deze toe te voegen tooAzure AD vragen. |

## Hallo-id-token valideren
Ontvangen van een token ID is niet voldoende tooauthenticate Hallo gebruiker. U moet ook Hallo-ID van het token handtekening valideren en controleren van claims Hallo Hallo token per vereisten van uw app. Hallo v2.0-eindpunt maakt gebruik van [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) en openbare sleutel-cryptografie toosign tokens en controleer of ze geldig zijn.

Kunt u toovalidate Hallo-id-token in de clientcode, maar een gangbare optie toosend Hallo ID token tooa back-end-server is en er Hallo validatie uitvoert. Nadat u hebt geverifieerd Hallo handtekening van Hallo-ID-token, moet u tooverify enkele claims. Voor meer informatie, met inbegrip van informatie over [valideren van tokens](active-directory-v2-tokens.md#validating-tokens) en [belangrijke informatie over het ondertekenen van sleutelrollover](active-directory-v2-tokens.md#validating-tokens), Zie Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md). We raden het gebruik van een bibliotheek tooparse en valideren van tokens. Er is ten minste één van deze bibliotheken beschikbaar zijn voor de meeste talen en platforms.
<!--TODO: Improve hello information on this-->

Ook kunt u aanvullende claims toovalidate, afhankelijk van uw scenario. Sommige algemene validaties zijn onder andere:

* Zorg ervoor dat Hallo gebruiker of organisatie heeft aangemeld voor Hallo-app.
* Zorg ervoor dat die gebruiker Hallo autorisatie of de bevoegdheden is vereist.
* Zorg ervoor dat een bepaalde sterkte van verificatie heeft plaatsgevonden, zoals multi-factor authentication-server.

Zie voor meer informatie over claims in een token ID Hallo Hallo [v2.0-eindpunt tokens verwijzing](active-directory-v2-tokens.md).

Nadat u hebt Hallo ID token volledig gevalideerd, kunt u een sessie beginnen met Hallo-gebruiker. Hallo-claims in Hallo ID token tooget informatie over Hallo-gebruiker in uw app gebruiken. U kunt deze informatie gebruiken voor de weergave, registreert en autorisaties.

## Afmelden aanvraag verzenden
Wanneer u toosign uit Hallo gebruiker wilt van uw app, is niet voldoende tooclear cookies van uw app of anders Hallo gebruikerssessie beëindigen. U moet ook omleiden Hallo gebruiker toohello v2.0-eindpunt toosign uit. Als u dit doet, Hallo gebruiker tooyour app opnieuw zonder hun referenties opnieuw invoeren geverifieerd omdat er een geldige één aanmeldingssessie met Hallo v2.0-eindpunt.

U kunt omleiden Hallo gebruiker toohello `end_session_endpoint` vermeld in het Hallo-document OpenID Connect metagegevens:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Parameter | Voorwaarde | Beschrijving |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Aanbevolen | Hallo-URL die Hallo gebruiker is omgeleid tooafter is afmelden. Als het Hallo-parameter niet is opgenomen, weergegeven Hallo gebruiker een algemeen bericht dat wordt gegenereerd door Hallo v2.0-eindpunt. Deze URL moet overeenkomen met een van de Hallo redirect die URI 's geregistreerd voor uw toepassing in de portal voor wachtwoordregistratie Hallo-app.  |

## Eenmalige afmelding
Wanneer u Hallo gebruiker toohello omleiden `end_session_endpoint`, Hallo v2.0-eindpunt Hallo gebruikerssessie vanuit Hallo browser worden gewist. Hallo-gebruiker kan echter nog steeds zijn ondertekend in tooother toepassingen die Microsoft-accounts voor verificatie gebruiken. tooenable die toepassingen toosign Hallo gebruiker tegelijk, Hallo v2.0-eindpunt verzendt een aanvraag HTTP GET toohello geregistreerd `LogoutUrl` van alle Hallo-toepassingen die gebruiker Hallo is momenteel aangemeld bij. Toepassingen toothis aanvraag moeten reageren door het selectievakje van elke sessie die Hallo gebruiker en het retourneren van identificeert een `200` antwoord.  Als u eenmalige aanmelding toosupport af in uw toepassing wenst, moet u deze implementeren een `LogoutUrl` in de code van uw toepassing.  U kunt instellen Hallo `LogoutUrl` van Hallo app-portal voor wachtwoordregistratie.

## Protocol diagram: Token verkrijgen
Veel web-apps moeten toonot enige teken Hallo gebruiker in, maar ook een webservice namens de gebruiker Hallo tooaccess met behulp van OAuth. Dit scenario combineert OpenID Connect voor de verificatie bij het ophalen van een vergunning tegelijkertijd code waarmee u tooget toegang kunt als u van Hallo OAuth-autorisatiecodestroom gebruikmaakt tokens.

Hallo volledige OpenID Connect aanmelden en token overname stroom lijkt vergelijkbare toohello volgende diagram. Elke stap in de volgende secties Hallo van Hallo artikel in detail worden beschreven.

![Protocol OpenID Connect: Token verkrijgen](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Toegangstokens ophalen
tooacquire toegangstokens, wijzigen Hallo aanmeldingsverzoek:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Klik op Hallo koppeling tooexecute na deze aanvraag. Nadat u zich aanmeldt, is uw browser omgeleide toohttps://localhost/myapp/, met een token ID en een code in de adresbalk Hallo. Let op: maakt gebruik van deze aanvraag `response_mode=query` (voor demonstratiedoeleinden alleen). Het is raadzaam dat u `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

Door machtigingsbereiken in Hallo-aanvraag en met behulp van `response_type=id_token code`, Hallo v2.0-eindpunt zorgt ervoor dat die gebruiker Hallo toohello machtigingen die zijn aangegeven in Hallo heeft ingestemd `scope` queryparameter. Het resultaat een autorisatie code tooyour app tooexchange voor een toegangstoken.

### Geslaagde reactie
Een geslaagde reactie van het gebruik van `response_mode=form_post` ziet er als volgt:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| id_token |Hallo ID-token dat Hallo app aangevraagd. U kunt gebruiken Hallo ID token tooverify Hallo gebruikers id en beginnen met een sessie met de Hallo-gebruiker. U vindt meer informatie over het ID-tokens en de inhoud ervan in Hallo [v2.0-eindpunt tokens verwijzing](active-directory-v2-tokens.md). |
| code |Hallo autorisatiecode die Hallo app aangevraagd. Hallo-app kunt Hallo autorisatie code toorequest een toegangstoken voor de doelresource hello gebruiken. Er is een autorisatiecode zeer tijdelijke. Normaal gesproken verloopt een autorisatiecode over ongeveer tien minuten. |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |

### Foutbericht
Foutberichten kunnen ook worden verzonden toohello omleidings-URI zodat hello app kan ze op juiste manier verwerken. Een foutmelding ziet er als volgt:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u tooclassify typen fouten die optreden en tooreact tooerrors kunt gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een verificatiefout. |

Zie voor een beschrijving van mogelijke foutcodes en aanbevolen clientantwoorden [foutcodes voor autorisatie eindpunt fouten](#error-codes-for-authorization-endpoint-errors).

Wanneer u een autorisatiecode en een token ID hebt, kunt u Hallo gebruiker aanmelden en toegangstokens ophalen in hun naam. toosign hello gebruiker in, moet u Hallo ID token valideren [precies zoals beschreven](#validate-the-id-token). tooget toegangstokens, volg de stappen Hallo in onze [OAuth-protocoldocumentatie](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
