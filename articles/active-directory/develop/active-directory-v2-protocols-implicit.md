---
title: "aaaSecure één pagina toepassingen met behulp van hello Azure AD v2.0 impliciete stroom | Microsoft Docs"
description: "Gebouw webtoepassingen die gebruikmaken van Azure AD v2.0-implementatie van Hallo impliciete stroom voor apps van één pagina."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# v2.0 protocollen - kuuroorden Hallo impliciete stroom met
Met Hallo v2.0-eindpunt, kunt u gebruikers zich bij uw apps op één pagina met persoonlijke en zakelijke/school accounts van Microsoft.  Wordt geleverd tooauthentication één pagina en andere JavaScript-apps die voornamelijk in een browser gezicht interessante enkele uitdagingen bij deze uitvoeren:

* Hallo-beveiligingskenmerken van deze apps zijn aanzienlijk anders dan traditionele server op basis van webtoepassingen.
* Veel autorisatieservers & id-providers bieden geen ondersteuning voor CORS-aanvragen.
* Volledige pagina browser omleidingen weg Hallo app worden met name Invasief toohello gebruikerservaring.

Voor deze toepassingen (nadenkt: AngularJS, Ember.js, React.js, enzovoort) Hallo impliciete OAuth 2.0-Grant-stroom biedt ondersteuning voor Azure AD.  Hallo impliciete stroom wordt beschreven in Hallo [OAuth 2.0-specificatie](http://tools.ietf.org/html/rfc6749#section-4.2).  Het belangrijkste voordeel is dat Hallo app tooget-tokens van Azure AD kunnen zonder dat u een back-end server referentie exchange uitvoert.  Hierdoor kunnen Hallo app toosign in Hallo gebruiker, sessie en het verkrijgen van tokens tooother web-API's allemaal binnen Hallo client JavaScript-code.  Er zijn enkele belangrijke overwegingen tootake rekening wanneer u de impliciete stroom Hallo - specifiek ongeveer [client](http://tools.ietf.org/html/rfc6749#section-10.3) en [gebruikersimitaties](http://tools.ietf.org/html/rfc6749#section-10.3).

Als u toouse Hallo impliciete stroom en Azure AD tooadd verificatie tooyour JavaScript-app wilt, raden wij aan gebruik van onze JavaScript-bibliotheek van open-source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Er zijn enkele AngularJS-zelfstudies beschikbaar [hier](active-directory-appmodel-v2-overview.md#getting-started) toohelp die u aan de slag.  

Als u liever niet toouse een bibliotheek in één pagina app en verzenden protocolberichten zelf, volgt u Hallo algemene stappen hieronder.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## Protocol-diagram
Hallo gehele impliciete aanmelden stroom ziet er ongeveer als volgt - Hallo stappen hieronder in detail worden beschreven.

![OpenId Connect banen](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Hallo aanmelden aanvraag verzenden
tooinitially aanmelding hello gebruiker in uw app, kunt u verzendt een [OpenID Connect](active-directory-v2-protocols-oidc.md) autorisatieaanvraag en get een `id_token` van Hallo v2.0-eindpunt:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Klik Hallo-koppeling hieronder tooexecute deze aanvraag. Na het aanmelden, uw browser te moet worden omgeleid`https://localhost/myapp/` met een `id_token` in de adresbalk Hallo.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassings-Id die Hallo-portal voor wachtwoordregistratie ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) toegewezen van uw app. |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden.  Het kan ook betekenen dat Hallo response_type `token`. Met behulp van `token` hier, krijgt uw app tooreceive een toegangstoken onmiddellijk uit Hallo autoriseren eindpunt zonder een tweede aanvraag toohello autoriseren toomake eindpunt.  Als u Hallo `token` response_type, Hallo `scope` parameter moet een scope die aangeeft welke resource tooissue Hallo token voor bevatten. |
| redirect_uri |Aanbevolen |Hallo redirect_uri van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app.  Deze moet exact overeenkomen met een Hallo redirect_uris die u geregistreerd in het Hallo-portal, behalve url gecodeerd moet. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Voor het OpenID Connect, het Hallo-bereik omvat `openid`, toohello 'Aanmelden u' machtiging in Hallo toestemming gebruikersinterface, wat overeenkomt.  (Optioneel) u kunt ook tooinclude hello `email` of `profile` [scopes](active-directory-v2-scopes.md) voor toegang tot tooadditional gebruikersgegevens.  U mogelijk ook andere bereiken opnemen in deze aanvraag voor het aanvragen van toestemming toovarious resources. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende token back tooyour app worden moet.  Moet `fragment` voor impliciete Hallo-stroom. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd.  Een tekenreeks van inhoud die u wenst dat kan zijn.  Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor [voorkomen van aanvraagvervalsing op meerdere sites aanvallen](http://tools.ietf.org/html/rfc6749#section-10.12).  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| nonce |Vereist |Een waarde die is opgenomen in de aanvraag hello, die worden gegenereerd door Hallo-app, die wordt opgenomen in de resulterende id_token Hallo als een claim.  Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen.  Hallo-waarde is doorgaans een willekeurige, unieke tekenreeks die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| prompt |Optioneel |Geeft Hallo type gebruikersinteractie is vereist.  alleen geldige waarden op dit moment 'aanmelding', 'none zijn' Hallo ' toestemming geven '.  `prompt=login`geforceerd wordt Hallo gebruiker tooenter hun referenties op die het negatief maken van eenmalige aanmelding op verzoek.  `prompt=none`Hallo tegengestelde - brengt dat die Hallo-gebruiker niet vragen beeïndigen krijgt is.  Als het Hallo-aanvraag kan niet worden voltooid in stille modus via eenmalige aanmelding, worden Hallo v2.0-eindpunt een fout geretourneerd.  `prompt=consent`trigger Hallo OAuth wordt dialoogvenster na Hallo gebruiker zich aanmeldt, Hallo gebruiker toogrant machtigingen toohello app gevraagd toestemming. |
| login_hint |Optioneel |Worden kunnen gebruikt toopre-opvulling Hallo gebruikersnaam, e adresveld Hallo aanmelden pagina Hallo gebruiker, als u hun gebruikersnaam tevoren weet.  Vaak apps deze parameter wordt gebruikt tijdens de hervalidatie Hallo gebruikersnaam die al worden opgehaald uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Optioneel |Een van `consumers` of `organizations`.  Als opgenomen, wordt het Hallo detectie op basis van e-mailbericht proces overslaan die gebruiker doorloopt op Hallo v2.0 aanmeldingspagina, voorloopspaties tooa iets sneller gebruikerservaring.  Vaak apps wordt met deze parameter gebruikt tijdens de hervalidatie door uit te pakken Hallo `tid` claim uit Hallo id_token.  Als hello `tid` claim waarde is `9188040d-6c67-4c5b-b112-36a304b66dad`, moet u `domain_hint=consumers`.  Gebruik anders `domain_hint=organizations`. |

Op dit moment Hallo gebruiker worden tooenter gevraagd hun referenties en volledige Hallo-verificatie.  Hallo v2.0-eindpunt zorgt er ook die gebruiker Hallo toohello machtigingen die zijn aangegeven in Hallo heeft ingestemd `scope` queryparameter.  Als gebruiker Hallo tooany van deze machtigingen niet heeft ingestemd, wordt het Hallo gebruiker tooconsent toohello vereist machtigingen gevraagd.  Details van [machtigingen, toestemming en multitenant apps vindt u hier](active-directory-v2-scopes.md).

Zodra Hallo gebruiker wordt geverifieerd en toestemming verleent, Hallo v2.0-eindpunt resulteert in een antwoord tooyour app op Hallo aangegeven `redirect_uri`, met behulp van de methode in Hallo Hallo `response_mode` parameter.

#### Geslaagde reactie
Een geslaagde reactie met `response_mode=fragment` en `response_type=id_token+token` vergelijkbaar is met de volgende hello, met regeleinden beter leesbaar:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Opgenomen als `response_type` bevat `token`. Hallo-toegangstoken dat Hallo app aangevraagd, in dit geval voor Hallo Microsoft Graph.  Hallo toegangstoken moet niet worden gedecodeerd of anders gecontroleerd, kan deze worden behandeld als één tekenreeks. |
| token_type |Opgenomen als `response_type` bevat `token`.  Altijd `Bearer`. |
| expires_in |Opgenomen als `response_type` bevat `token`.  Geeft het aantal seconden op Hallo-token ongeldig is voor cachedoeleinden Hallo. |
| Bereik |Opgenomen als `response_type` bevat `token`.  Hiermee wordt aangegeven Hallo voor een of meer bereiken voor welke Hallo access_token geldig zijn. |
| id_token |Hallo id_token die Hallo app aangevraagd. U kunt gebruiken Hallo id_token tooverify Hallo gebruikers id en beginnen met een sessie met de Hallo-gebruiker.  Meer informatie over id_tokens en de inhoud ervan is opgenomen in Hallo [v2.0-eindpunt tokenverwijzing](active-directory-v2-tokens.md). |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |

#### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat Hallo app ze op de juiste wijze kan verwerken:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

## Hallo id_token valideren
Zojuist hebt ontvangen van een id_token is niet voldoende tooauthenticate Hallo-gebruiker. u moet de Hallo id_token handtekening valideren en controleer of Hallo claims in Hallo token per vereisten van uw app.  Hallo v2.0-eindpunt maakt gebruik van [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) en openbare sleutel-cryptografie toosign tokens en controleer of ze geldig zijn.

Kunt u toovalidate hello `id_token` in de clientcode, maar een gebruikelijk is toosend hello `id_token` tooa back-endserver en er Hallo validatie uit te voeren.  Zodra u Hallo handtekening van Hallo id_token hebt gevalideerd, zijn er enkele claims, dat kunt u zich tooverify vereist.  Zie Hallo [v2.0 tokenverwijzing](active-directory-v2-tokens.md) voor meer informatie, met inbegrip van [valideren van Tokens](active-directory-v2-tokens.md#validating-tokens) en [belangrijke informatie over het ondertekenen van sleutel Rollover](active-directory-v2-tokens.md#validating-tokens).  U wordt aangeraden die gebruikmaken van een bibliotheek geparseerd en valideren van tokens: Er is ten minste één beschikbaar voor de meeste talen en platforms.
<!--TODO: Improve hello information on this-->

Mogelijk wilt u ook toovalidate extra claims afhankelijk van uw scenario.  Sommige algemene validaties zijn onder andere:

* Gezorgd Hallo organisatie-gebruiker is aangemeld voor Hallo-app.
* Ervoor zorgen dat Hallo gebruiker heeft juiste autorisatie/bevoegdheden
* Een bepaalde sterkte van verificatie gezorgd is opgetreden, zoals multi-factor authentication-server.

Zie voor meer informatie over claims in een id_token Hallo Hallo [v2.0-eindpunt tokenverwijzing](active-directory-v2-tokens.md).

Zodra u hebt Hallo id_token volledig gevalideerd, kunt u beginnen met een sessie met de Hallo gebruiker en het gebruik van Hallo claims in Hallo id_token tooobtain informatie over Hallo gebruiker in uw app.  Deze informatie kan worden gebruikt voor weergave, registreert, autorisaties, enzovoort.

## Toegangstokens ophalen
Nu dat u hebt Hallo gebruiker zich in uw app met één pagina, kunt u toegangstokens ophalen voor het aanroepen van web API's die zijn beveiligd door Azure AD, zoals Hallo [Microsoft Graph](https://graph.microsoft.io).  Zelfs als u al een token met Hallo ontvangen `token` response_type, kunt u deze methode tooacquire tokens tooadditional bronnen zonder tooredirect Hallo gebruiker toosign in opnieuw.

In de normale OpenID Connect/OAuth-flow hello, zou u dit doen door het maken van een aanvraag toohello v2.0 `/token` eindpunt.  Hallo v2.0-eindpunt biedt echter geen ondersteuning voor CORS aanvragen, zodat tooget waardoor AJAX-aanroepen en vernieuwen van tokens valt buiten het Hallo-vraag.  U kunt in plaats daarvan Hallo impliciete stroom gebruiken in een verborgen iframe tooget nieuwe tokens voor andere web-API's: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Probeer kopiëren en plakken Hallo hieronder aanvraag in een browsertabblad! (Vergeet niet tooreplace hello `domain_hint` en Hallo `login_hint` waarden Hello corrigeren van waarden voor uw gebruiker)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassings-Id die Hallo-portal voor wachtwoordregistratie ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) toegewezen van uw app. |
| response_type |Vereist |Moet bevatten `id_token` voor OpenID Connect aanmelden.  Het kan ook betekenen dat andere response_types zoals `code`. |
| redirect_uri |Aanbevolen |Hallo redirect_uri van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app.  Deze moet exact overeenkomen met een Hallo redirect_uris die u geregistreerd in het Hallo-portal, behalve url gecodeerd moet. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Voor het ophalen van tokens, omvatten alle [scopes](active-directory-v2-scopes.md) u nodig hebt voor de resource Hallo van belang. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende token back tooyour app worden moet.  Een van `query`, `form_post`, of `fragment`. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd.  Een tekenreeks van inhoud die u wenst dat kan zijn.  Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor het voorkomen van aanvraagvervalsing op meerdere sites aanvallen.  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| nonce |Vereist |Een waarde die is opgenomen in de aanvraag hello, die worden gegenereerd door Hallo-app, die wordt opgenomen in de resulterende id_token Hallo als een claim.  Hallo-app kunt vervolgens controleren of dat deze waarde toomitigate token replay-aanvallen.  Hallo-waarde is doorgaans een willekeurige, unieke tekenreeks die gebruikt tooidentify Hallo oorsprong van Hallo-aanvraag worden kan. |
| prompt |Vereist |Voor het vernieuwen van & ophalen van tokens in een verborgen iframe, moet u `prompt=none` tooensure die iframe Hallo nu niet vastloopt op Hallo v2.0-aanmeldingspagina en wordt onmiddellijk geretourneerd. |
| login_hint |Vereist |Voor het vernieuwen van & ophalen van tokens in een verborgen iframe, moet u Hallo gebruikersnaam van Hallo gebruiker opnemen in deze hint in volgorde toodistinguish tussen meerdere sessies Hallo gebruiker op een bepaald tijdstip heeft mogelijk. U kunt Hallo gebruikersnaam extraheren uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Vereist |Een van `consumers` of `organizations`.  Voor het vernieuwen van & ophalen van tokens in een verborgen iframe, moet u Hallo domain_hint opnemen in Hallo-aanvraag.  U moet Hallo uitpakken `tid` claim uit Hallo id_token van een vorige toodetermine aanmelden welke toouse waarde.  Als hello `tid` claim waarde is `9188040d-6c67-4c5b-b112-36a304b66dad`, moet u `domain_hint=consumers`.  Gebruik anders `domain_hint=organizations`. |

Hartelijk dank toohello `prompt=none` parameter, deze aanvraag ofwel slagen of mislukken onmiddellijk en tooyour toepassing retourneren.  Een geslaagde reactie tooyour app verzonden op Hallo aangegeven `redirect_uri`, met behulp van de methode in Hallo Hallo `response_mode` parameter.

#### Geslaagde reactie
Een geslaagde reactie met `response_mode=fragment` lijkt:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo-token dat Hallo app aangevraagd. |
| token_type |Altijd `Bearer`. |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| Bereik |Hallo-scopes die Hallo toegangstoken is geldig voor. |

#### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat Hallo app ze op de juiste wijze kan verwerken.  In geval van Hallo `prompt=none`, een verwachte fout is:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

Als u deze fout in Hallo iframe aanvraag ontvangt, moet Hallo gebruiker interactief aanmelden opnieuw tooretrieve een nieuw token.  U kunt toohandle in dit geval in een manier die het zinvol is voor uw toepassing.

## Vernieuwen van tokens
Beide `id_token`s en `access_token`s verloopt na een korte periode, zodat uw app moet worden voorbereid toorefresh deze regelmatig tokens.  toorefresh ofwel type token, kunt u Hallo uitvoeren dezelfde verborgen iframe aanvraag boven het Hallo `prompt=none` parameter toocontrol Azure AD-gedrag.  Als u wilt dat tooreceive een nieuwe `id_token`, worden ervoor toouse `response_type=id_token` en `scope=openid`, evenals een `nonce` parameter.

## Een afmelden aanvraag verzenden
Hallo OpenIdConnect `end_session_endpoint` kunt u uw app toosend een aanvraag toohello v2.0-eindpunt tooend de sessie en Schakel cookies van een gebruiker ingesteld door Hallo v2.0-eindpunt.  toofully Meld u aan een gebruiker uit een webtoepassing, uw app moet een eigen sessie met Hallo gebruiker beëindigen (meestal met een token cache wissen of verwijderen van cookies) en leid Hallo browser:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | Aanbevolen | Hallo-URL die gebruiker Hallo moet worden geretourneerd tooafter afmelden is voltooid. Deze waarde moet overeenkomen met een van URI's geregistreerd voor de toepassing hello Hallo-omleiding. Als er niet is opgenomen, wordt Hallo gebruiker weergegeven een algemeen bericht door Hallo v2.0-eindpunt. |
