---
title: aaaUnderstand hello OpenID Connect code authenticatiestroom in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse HTTP-berichten tooauthorize toegang tot tooweb toepassingen en web-API's in uw tenant met behulp van Azure Active Directory en OpenID Connect.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Toegang tooweb toepassingen met OpenID Connect en Azure Active Directory autoriseren
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) is een eenvoudige identiteitlaag gebouwd op Hallo OAuth 2.0-protocol. OAuth 2.0 definieert mechanismen tooobtain en gebruik **toegang tot tokens** tooaccess beveiligde bronnen, maar ze standaardmethoden tooprovide identiteitsgegevens niet bepalen. OpenID Connect implementeert verificatie als een uitbreiding toohello autorisatieproces OAuth 2.0. Biedt informatie over de eindgebruiker Hallo Hallo vorm van een `id_token` die Hallo identiteit van Hallo gebruiker wordt geverifieerd en bevat informatie over Hallo gebruiker basisprofiel.

Onze aanbeveling OpenID Connect worden is als u een webtoepassing die wordt gehost op een server en is toegankelijk via een browser bouwt.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Verificatiestroom met OpenID Connect
Hallo meest eenvoudige aanmelden stroom bevat stappen te volgen Hallo - elk van deze hieronder in detail wordt beschreven.

![OpenId Connect Verificatiestroom](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Metagegevensdocument OpenID Connect

Beschrijving van een document met metagegevens die de meeste van Hallo vereiste informatie voor een app tooperform aanmelden bevat OpenID Connect. Dit omvat gegevens zoals Hallo URL's toouse en Hallo-locatie van de openbare handtekeningsleutels Hallo-service. Hallo OpenID Connect metagegevensdocument kan worden gevonden op:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
Hallo metagegevens is een eenvoudige JSON JavaScript Object Notation ()-document. Zie Hallo codefragment voor een voorbeeld te volgen. Hallo inhoud van het codefragment worden volledig beschreven in Hallo [specificatie van het OpenID Connect](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Hallo aanmelden aanvraag verzenden
Wanneer uw webtoepassing tooauthenticate Hallo gebruiker moet, moet het Hallo gebruiker toohello directe `/authorize` eindpunt. Deze aanvraag is vergelijkbaar toohello eerste arm van Hallo [OAuth 2.0 autorisatie Code stromen](active-directory-protocols-oauth-code.md), met enkele belangrijke verschillen:

* Hallo aanvraag vergezeld gaan van Hallo bereik `openid` in Hallo `scope` parameter.
* Hallo `response_type` vergezeld gaan van de parameter `id_token`.
* Hallo aanvraag vergezeld gaan van Hallo `nonce` parameter.

Dus eruit als volgt een voorbeeld van een aanvraag:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn tenant-id's, bijvoorbeeld `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` of `contoso.onmicrosoft.com` of `common` voor tenant-onafhankelijke tokens |
| client_id |Vereist |Hallo toepassings-Id toegewezen tooyour app bij de registratie met Azure AD. U kunt dit vinden in hello Azure-Portal. Klik op **Azure Active Directory**, klikt u op **App registraties**, kies de toepassing hello en Hallo toepassings-Id op de pagina van de toepassing hello vinden. |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden.  Het kan ook betekenen dat andere response_types zoals `code`. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Voor het OpenID Connect, het Hallo-bereik omvat `openid`, toohello 'Aanmelden u' machtiging in Hallo toestemming gebruikersinterface, wat overeenkomt.  U mogelijk ook andere bereiken opnemen in deze aanvraag voor het aanvragen van toestemming. |
| nonce |Vereist |Een waarde die is opgenomen in de aanvraag hello, die worden gegenereerd door Hallo-app die is opgenomen in de resulterende Hallo `id_token` als een claim.  Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen.  Hallo-waarde is meestal een unieke tekenreeks van willekeurige of GUID die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| redirect_uri |Aanbevolen |Hallo redirect_uri van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app.  Deze moet exact overeenkomen met een Hallo redirect_uris die u geregistreerd in het Hallo-portal, behalve url gecodeerd moet. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende authorization_code back tooyour app worden moet.  Ondersteunde waarden zijn `form_post` voor *HTTP Formulierbericht* of `fragment` voor *URL-fragment*.  Voor webtoepassingen, wordt u aangeraden `response_mode=form_post` tooensure Hallo meest veilige overdracht van tokens tooyour toepassing. |
| state |Aanbevolen |Een waarde die is opgenomen in het Hallo-aanvraag die wordt geretourneerd als antwoord van Hallo-token.  Een tekenreeks van inhoud die u wenst dat kan zijn.  Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor [voorkomen van aanvraagvervalsing op meerdere sites aanvallen](http://tools.ietf.org/html/rfc6749#section-10.12).  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| prompt |Optioneel |Geeft Hallo type gebruikersinteractie is vereist.  Op dit moment Hallo alleen geldige waarden zijn 'aanmelding', 'none', ' toestemming geven '.  `prompt=login`dwingt Hallo gebruiker tooenter hun referenties op die aanvraag, het negatief maken van eenmalige aanmelding.  `prompt=none`is tegengestelde Hallo - die Hallo-gebruiker is niet opgenomen met een interactieve prompt helemaal te garanderen.  Als het Hallo-aanvraag kan niet worden voltooid in stille modus via eenmalige aanmelding, Hallo eindpunt een fout geretourneerd.  `prompt=consent`Hallo OAuth toestemming dialoogvenster na Hallo gebruiker zich aanmeldt, waarin wordt gevraagd Hallo gebruiker toogrant machtigingen toohello app wordt geactiveerd. |
| login_hint |Optioneel |Mag gebruikte toopre-opvulling Hallo gebruikersnaam, e adresveld van het Hallo-aanmeldingspagina voor de gebruiker hello, als u hun gebruikersnaam tevoren weet.  Vaak apps Gebruik deze parameter tijdens verificatie wordt uitgevoerd, dat al Hallo gebruikersnaam opgehaald uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |

Op dit moment Hallo gebruiker wordt gevraagd tooenter hun referenties en volledige Hallo-verificatie.

### Voorbeeldreactie
Een voorbeeldantwoord kan nadat Hallo gebruiker is geverifieerd, uitzien:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| id_token |Hallo `id_token` die Hallo app aangevraagd. U kunt Hallo `id_token` tooverify Hallo gebruikers id en wilt beginnen met een sessie met de Hallo-gebruiker. |
| state |Een waarde die is opgenomen in Hallo-aanvraag wordt ook Hallo token antwoord geretourneerd. Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor [voorkomen van aanvraagvervalsing op meerdere sites aanvallen](http://tools.ietf.org/html/rfc6749#section-10.12).  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |

### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat Hallo app ze op de juiste wijze kan verwerken:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

#### Foutcodes voor autorisatie eindpunt fouten
Hallo volgende tabel beschrijft Hallo verschillende foutcodes die kunnen worden geretourneerd in Hallo `error` parameter van het Hallo-foutmelding.

| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout voor ontwikkeling en meestal wordt onderschept tijdens de eerste test. |
| unauthorized_client |Hallo-clienttoepassing is niet toegestaan toorequest een autorisatiecode. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| ACCESS_DENIED |Resource-eigenaar toestemming geweigerd |Hallo-clienttoepassing kan melden Hallo-gebruiker die deze kan niet worden voortgezet tenzij Hallo gebruiker hiermee akkoord gaat. |
| unsupported_response_type |Hallo autorisatie server biedt geen ondersteuning voor antwoordtype Hallo Hallo-aanvraag. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout voor ontwikkeling en meestal wordt onderschept tijdens de eerste test. |
| server_error |Hallo-server heeft een onverwachte fout aangetroffen. |Hallo aanvraag opnieuw proberen. Deze fouten kunnen worden veroorzaakt door tijdelijke omstandigheden. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke fout. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke situatie. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven met het Hallo-resource, indien aanwezig, is niet geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |

## Hallo id_token valideren
Zojuist hebt ontvangen van een `id_token` is niet voldoende tooauthenticate Hallo gebruiker; u moet Hallo handtekening valideren en controleren van de claims in Hallo Hallo `id_token` per vereisten van uw app. Hello Azure AD-eindpunt maakt gebruik van JSON Web Tokens (JWTs) en openbare-sleutelcryptografie toosign tokens en controleer of ze geldig zijn.

Kunt u toovalidate hello `id_token` in de clientcode, maar een gebruikelijk is toosend hello `id_token` tooa back-endserver en er Hallo validatie uit te voeren. Zodra u hebt gevalideerd Hallo handtekening Hallo `id_token`, er zijn enkele claims bent u vereiste tooverify.

Mogelijk wilt u ook toovalidate extra claims afhankelijk van uw scenario. Sommige algemene validaties zijn onder andere:

* Gezorgd Hallo organisatie-gebruiker is aangemeld voor Hallo-app.
* Ervoor zorgen dat Hallo gebruiker heeft juiste autorisatie/bevoegdheden
* Een bepaalde sterkte van verificatie gezorgd is opgetreden, zoals multi-factor authentication-server.

Zodra u hebt gevalideerd Hallo `id_token`, kunt u beginnen met een sessie met de Hallo gebruiker en claims hello gebruiken in Hallo `id_token` tooobtain informatie over Hallo-gebruiker in uw app. Deze informatie kan worden gebruikt voor weergave, registreert, autorisaties, enzovoort. Lees voor meer informatie over Hallo token typen of claims [ondersteund Token en claimtypen](active-directory-token-and-claims.md).

## Afmelden aanvraag verzenden
Wanneer u wenst toosign Hallo gebruiker buiten het Hallo-app, is niet voldoende tooclear cookies van uw app of anders Hallo-sessie met Hallo gebruiker beëindigen.  U moet ook Hallo gebruiker toohello omleiden `end_session_endpoint` voor afmelden.  Als u toodo zo niet, Hallo gebruiker worden opgegeven kunnen tooreauthenticate tooyour app zonder hun referenties opnieuw invoeren omdat er een geldige eenmalige aanmelding sessie met hello Azure AD-eindpunt.

U kunt eenvoudig hello gebruiker toohello omleiden `end_session_endpoint` vermeld in het Hallo-document OpenID Connect metagegevens:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| post_logout_redirect_uri |Aanbevolen |Hallo-URL die gebruiker Hallo moet omgeleide tooafter geslaagde afmelden.  Als u niet worden opgenomen, Hallo gebruiker een algemeen bericht weergegeven. |

## Eenmalige afmelding
Wanneer u Hallo gebruiker toohello omleiden `end_session_endpoint`, Azure AD Hallo gebruikerssessie vanuit Hallo browser worden gewist. Hallo-gebruiker kan echter nog steeds zijn ondertekend in tooother-toepassingen die Azure AD voor verificatie gebruiken. tooenable die toepassingen toosign gebruiker tegelijkertijd Hallo, Azure AD verzendt een aanvraag HTTP GET toohello geregistreerd `LogoutUrl` van alle Hallo-toepassingen die gebruiker Hallo is momenteel aangemeld bij. Toepassingen toothis aanvraag moeten reageren door het selectievakje van elke sessie die Hallo gebruiker en het retourneren van identificeert een `200` antwoord.  Als u eenmalige aanmelding toosupport af in uw toepassing wenst, moet u deze implementeren een `LogoutUrl` in de code van uw toepassing.  U kunt instellen Hallo `LogoutUrl` van hello Azure-portal:

1. Navigeer toohello [Azure Portal](https://portal.azure.com).
2. Kies uw Active Directory door te klikken op uw account in Hallo rechtsboven Hallo pagina.
3. Kies in het navigatievenster aan Hallo linkerkant **Azure Active Directory**, en kies vervolgens **App registraties** en selecteer uw toepassing.
4. Klik op **eigenschappen** en Hallo zoeken **afmelding URL** in het tekstvak. 

## Token verkrijgen
Veel web-apps nodig toonot enige teken Hallo gebruiker in, maar ook toegang tot een webservice namens een gebruiker met OAuth. Dit scenario combineert OpenID Connect voor de verificatie bij het ophalen van tegelijkertijd een `authorization_code` die kunnen worden gebruikt tooget `access_tokens` met behulp van Hallo OAuth-autorisatie Code stromen.

## Toegangstokens ophalen
tooacquire toegangstokens, moet u toomodify Hallo aanmeldingsverzoek van boven:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Door machtigingsbereiken inclusief in Hallo-aanvraag en `response_type=code+id_token`, Hallo `authorize` eindpunt zorgt ervoor dat die gebruiker Hallo toohello machtigingen die zijn aangegeven in Hallo heeft ingestemd `scope` queryparameter en uw app een autorisatiecode retourneren tooexchange voor een toegangstoken.

### Geslaagde reactie
Een geslaagde reactie met `response_mode=form_post` lijkt:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| id_token |Hallo `id_token` die Hallo app aangevraagd. U kunt Hallo `id_token` tooverify Hallo gebruikers id en wilt beginnen met een sessie met de Hallo-gebruiker. |
| code |Hallo authorization_code die Hallo app aangevraagd. Hallo-app kunt Hallo autorisatie code toorequest een toegangstoken voor de doelresource hello gebruiken. Authorization_codes korte worden gehouden en normaal verlopen na ongeveer 10 minuten. |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |

### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat Hallo app ze op de juiste wijze kan verwerken:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

Zie voor een beschrijving van de mogelijke foutcodes Hallo en hun aanbevolen clientactie [foutcodes voor autorisatie eindpunt fouten](#error-codes-for-authorization-endpoint-errors).

Als u toegang hebt verkregen van een vergunning `code` en een `id_token`, kunt u Hallo gebruiker aanmelden en toegangstokens ophalen in hun naam.  toosign hello gebruiker in, moet u Hallo valideren `id_token` precies zoals hierboven is beschreven. tooget toegangstokens, kunt u stappen Hallo beschreven in 'Hello autorisatie code toorequest een toegangstoken gebruiken' Hallo-sectie van onze [OAuth-protocoldocumentatie](active-directory-protocols-oauth-code.md).
