---
title: 'Azure Active Directory B2C: Token verwijzing | Microsoft Docs'
description: Hallo typen tokens die zijn uitgegeven in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: Token verwijzing
Azure Active Directory B2C (Azure AD B2C) verzendt verschillende typen beveiligingstokens tijdens de verwerking van elk [authenticatiestroom](active-directory-b2c-apps.md). Dit document beschrijft Hallo-indeling, de beveiligingskenmerken en de inhoud van elk type token.

## <a name="types-of-tokens"></a>Typen tokens
Azure AD B2C ondersteunt Hallo [OAuth 2.0-protocol voor autorisatie](active-directory-b2c-reference-protocols.md), welke maakt gebruik van beide toegang tot tokens en vernieuwen van tokens. Het biedt ook ondersteuning voor verificatie en meld u via [OpenID Connect](active-directory-b2c-reference-protocols.md), die een derde type token introduceert: Hallo-id-token. Elk van deze tokens wordt weergegeven als een bearer-token.

Een bearer-token is een lichtgewicht beveiligingstoken dat verleent 'bearer' toegang tooa Hallo beveiligde resource. Hallo bearer is een partij die Hallo token kan opleveren. Azure AD een partij moet eerst worden geverifieerd voordat er een bearer-token kan ontvangen. Maar desgewenst Hallo stappen worden niet genomen toosecure Hallo-token in overdracht en opslag kan worden onderschept en gebruikt door een onbedoelde partij. Sommige beveiligingstokens hebben een ingebouwde mechanisme om te voorkomen dat onbevoegden kunnen gebruiken, maar bearer-tokens hebben geen dit mechanisme. Zij moeten worden overgebracht in een beveiligd kanaal, zoals transport layer security (HTTPS).

Als bearer-token buiten een beveiligd kanaal wordt verzonden, kunt een schadelijke party u een man-in-the-middle-aanval tooacquire Hallo-token gebruiken en deze toogain niet-geautoriseerde toegang tooa beveiligde resource. Hallo dezelfde beveiligings-principals toepassen wanneer bearer-tokens worden opgeslagen of voor later gebruik opgeslagen. Altijd voor zorgen dat uw app verzendt en bearer-tokens worden opgeslagen op een veilige manier.

Zie voor extra beveiligingsoverwegingen op bearer-tokens [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).

Veel van Hallo-tokens die problemen met Azure AD B2C worden geïmplementeerd als JSON webtokens (JWTs). Een JWT is een compacte, URL-veilige methode voor het overbrengen van gegevens tussen twee partijen. JWTs bevatten informatie die wel claims. Dit zijn asserties van informatie over Hallo bearer en onderwerp Hallo Hallo-token. Hallo-claims in JWTs zijn JSON-objecten die zijn gecodeerd en geserialiseerd voor verzending. Omdat Hallo JWTs uitgegeven door Azure AD B2C zijn ondertekend, maar niet versleuteld, kunt u eenvoudig hello inhoud van een JWT toodebug inspecteren deze. Er zijn verschillende hulpprogramma's beschikbaar die hiervoor, met inbegrip van [calebb.net](http://calebb.net). Voor meer informatie over JWTs verwijzen te[JWT-specificaties](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>ID-tokens
Een token ID is een vorm van het beveiligingstoken dat uw app van hello Azure AD B2C ontvangt `authorize` en `token` eindpunten. ID-tokens worden weergegeven als [JWTs](#types-of-tokens), en bevatten claims die u tooidentify gebruikers in uw app kunt gebruiken. Wanneer de ID-tokens zijn verkregen van Hallo `authorize` eindpunt, zijn vaak gebruikte toosign in gebruikers tooweb toepassingen. Wanneer de ID-tokens zijn verkregen van Hallo `token` eindpunt, ze kunnen worden verzonden in HTTP-aanvragen tijdens de communicatie tussen de twee onderdelen van Hallo dezelfde toepassing of service. Zoals u dat wilt, kunt u Hallo claims in een token ID. Ze zijn vaak gebruikte toodisplay account informatie of toomake wijze het toegangsbeheer in een app.  

ID-tokens zijn ondertekend, maar ze niet op dit moment zijn gecodeerd. Wanneer uw app of API ontvangt een token ID, moet deze [Hallo handtekening valideren](#token-validation) tooprove die Hallo token authentiek is. Uw app of API moet ook valideren voor een paar claims in Hallo token tooprove geldig is. Afhankelijk van de scenariovereisten Hallo Hallo claims gevalideerd door een app kunnen variëren, maar uw app moet uitvoeren sommige [algemene claim validaties](#token-validation) in elk scenario.

#### <a name="sample-id-token"></a>Voorbeeldtoken-ID
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Toegangstokens
Een toegangstoken is ook een vorm van een beveiligingstoken dat uw app van hello Azure AD B2C ontvangt `authorize` en `token` eindpunten. Toegangstokens worden ook weergegeven als [JWTs](#types-of-tokens), en bevatten claims die u tooidentify Hallo verleende machtigingen tooyour API's kunt gebruiken. Toegangstokens zijn ondertekend, maar ze niet op dit moment zijn gecodeerd. Toegangstokens moet gebruikte tooprovide toegang tooAPIs en resource-servers. Meer informatie over het te[toegangstokens gebruiken](active-directory-b2c-access-tokens.md). 

Wanneer uw API een toegangstoken ontvangt, moet deze [Hallo handtekening valideren](#token-validation) tooprove die Hallo token authentiek is. Uw API moet ook valideren voor een paar claims in Hallo token tooprove geldig is. Afhankelijk van de scenariovereisten Hallo Hallo claims gevalideerd door een app kunnen variëren, maar uw app moet uitvoeren sommige [algemene claim validaties](#token-validation) in elk scenario.

### <a name="claims-in-id-and-access-tokens"></a>Claims in tokens-ID en -toegang
Wanneer u Azure AD B2C gebruikt, hebt u fijnmazig controle over Hallo inhoud van uw tokens. U kunt configureren [beleid](active-directory-b2c-reference-policies.md) toosend bepaalde ingesteld van gebruikersgegevens in de claims die uw app is vereist voor bewerkingen. Deze claims standaardeigenschappen zoals Hallo van de gebruiker kunnen opnemen `displayName` en `emailAddress`. Ze kunnen ook [aangepaste gebruikerskenmerken](active-directory-b2c-reference-custom-attr.md) die u kunt definiëren in uw B2C-directory. Elke-ID en -toegang token die u ontvangt een bepaalde set claims die betrekking hebben op beveiliging bevat. Uw toepassingen kunnen gebruikmaken van deze claims toosecurely verifiëren van gebruikers en aanvragen.

Houd er rekening mee dat de Hallo claims in de ID-tokens niet in een bepaalde volgorde worden geretourneerd. Bovendien kunnen u nieuwe claims geïntroduceerd in de ID-tokens op elk gewenst moment. Uw app beter niet verbreken wanneer nieuwe claims binnenkomen. Hier volgen Hallo claims die u verwacht tooexist in-ID en toegang tokens die zijn uitgegeven door Azure AD B2C dat. Aanvullende claims worden bepaald door het beleid. Probeer het Hallo-claims in de ID voorbeeldtoken Hallo bekijken door te plakken in verdient het aanbeveling [calebb.net](http://calebb.net). Meer informatie vindt u in Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

| Naam | Claim | Voorbeeldwaarde | Beschrijving |
| --- | --- | --- | --- |
| Doelgroep |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Een claim doelgroep identificeert Hallo bedoeld ontvanger van Hallo-token. Voor Azure AD B2C is Hallo doelgroep van uw app-toepassings-ID als toegewezen tooyour app in de portal voor wachtwoordregistratie Hallo-app. Uw app moet deze waarde niet valideren en Hallo token afwijzen als deze niet overeenkomt. |
| certificaatverlener |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Deze claim identificeert Hallo beveiligingstokenservice (STS) die constructs en het Hallo-token retourneert. Het identificeert ook hello Azure AD-directory in welke Hallo gebruiker werd geverifieerd. Uw app moet Hallo verlener claim tooensure die Hallo token afkomstig zijn van hello Azure Active Directory v2.0-eindpunt te valideren. |
| verleend aan |`iat` |`1438535543` |Deze claim is het Hallo-tijd op welke Hallo token is uitgegeven, epoche tijd. |
| verlooptijd |`exp` |`1438539443` |Hallo is verlopen tijd claim Hallo tijd op welke Hallo token ongeldig, dat wordt vertegenwoordigd in epoche tijd wordt. Uw app moet deze claim tooverify Hallo geldigheid van de levensduur van token hello gebruiken. |
| niet voor |`nbf` |`1438535543` |Deze claim is het Hallo-tijd op welke hello token geldig, dat wordt vertegenwoordigd in epoche tijd wordt. Dit is meestal Hallo dezelfde zijn als Hallo tijd Hallo token is uitgegeven. Uw app moet deze claim tooverify Hallo geldigheid van de levensduur van token hello gebruiken. |
| Versie |`ver` |`1.0` |Dit is Hallo-versie van het Hallo-ID-token, zoals gedefinieerd door Azure AD. |
| code-hash |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Een code-hash is opgenomen in een token ID alleen wanneer Hallo token samen met een OAuth 2.0-autorisatiecode wordt uitgegeven. Een hash van de code kan worden gebruikt toovalidate Hallo echtheid van een autorisatiecode. Voor meer informatie over het tooperform deze validatie Hallo Zie [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).  |
| token hash toegang |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Een token hash van de toegang is opgenomen in een token ID alleen wanneer het Hallo-token is uitgegeven samen met een OAuth 2.0-toegangstoken. Een token hash toegang kan worden gebruikt toovalidate Hallo echtheid van een toegangstoken. Voor meer informatie over het tooperform deze validatie Zie Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)  |
| nonce |`nonce` |`12345` |Een nonce is dat een strategie gebruikt toomitigate token replay-aanvallen. Uw app een nonce kunt opgeven in een aanvraag voor verificatie met behulp van Hallo `nonce` queryparameter. Hallo-waarde die u in de aanvraag Hallo opgeeft worden gegenereerd in Hallo ongewijzigd `nonce` van een token ID alleen claim. Hierdoor kan uw app tooverify Hallo-waarde met deze op verzoek Hallo die sessie Hallo-app aan een opgegeven ID-token koppelt opgegeven Hallo-waarde. Uw app moet deze validatie tijdens Hallo ID token validatie uitvoeren. |
| Onderwerp |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Dit is Hallo principal over welke Hallo asserts token informatie, zoals Hallo gebruiker van een app. Deze waarde is onveranderbaar en kan niet worden toegewezen of opnieuw gebruikt. Kan het zijn gebruikte tooperform autorisatie controles veilig, zoals wanneer Hallo token gebruikte tooaccess een bron is. Hallo onderwerp claim wordt standaard gevuld met object-ID van gebruiker in de map Hallo HALLO hallo. toolearn meer, Zie [Azure Active Directory B2C: Token, sessie en configuratie voor één aanmelding](active-directory-b2c-token-session-sso.md). |
| Authentication context class reference |`acr` |Niet van toepassing |Momenteel niet gebruikt, behalve in geval van oudere beleidsregels Hallo. toolearn meer, Zie [Azure Active Directory B2C: Token, sessie en configuratie voor één aanmelding](active-directory-b2c-token-session-sso.md). |
| Framework vertrouwensbeleid |`tfp` |`b2c_1_sign_in` |Dit is de naam Hallo van Hallo-beleid dat gebruikt tooacquire Hallo-id-token is. |
| Verificatie-tijd |`auth_time` |`1438535543` |Deze claim is Hallo tijdstip waarop een laatste opgegeven gebruikersreferenties, epoche tijd. |

### <a name="refresh-tokens"></a>Vernieuwen van tokens
Vernieuwen van tokens zijn beveiligingstokens dat uw app kunt tooacquire nieuwe ID-tokens gebruiken en toegang tokens in een OAuth 2.0-stroom tot. Ze bieden uw app op lange termijn toegang tooresources namens gebruikers zonder tussenkomst met deze gebruikers.

een vernieuwingstoken in een token antwoord tooreceive, uw app moet aanvragen Hallo `offline_acesss` bereik. meer informatie over Hallo toolearn `offline_access` bereik, raadpleeg dan toohello [naslaginformatie over Azure AD B2C-protocol](active-directory-b2c-reference-protocols.md).

Vernieuwen van tokens, en zullen altijd zijn volledig ondoorzichtig tooyour app. Ze kunnen zijn uitgegeven door Azure AD en worden gecontroleerd en geïnterpreteerd alleen door Azure AD. Ze zijn lange levensduur hebben, maar uw app niet worden geschreven met Hallo verwachting die een vernieuwingstoken voor een bepaalde periode duurt. Vernieuwen van tokens kunnen op elk moment om een groot aantal redenen zijn ongeldig. Hallo enige manier om uw app tooknow als een vernieuwingstoken geldig tooattempt tooredeem is het door het maken van een tokenaanvraag tooAzure AD.

Wanneer u een vernieuwingstoken voor een nieuw token inwisselen (en als uw app heeft gekregen Hallo `offline_access` bereik), ontvangt u een nieuwe vernieuwingstoken Hallo token reactie. Hallo zojuist uitgegeven vernieuwingstoken op te slaan. Het moet vernieuwingstoken dat u eerder hebt gebruikt in de aanvraag Hallo Hallo vervangen. Dit helpt te garanderen dat uw vernieuwen van tokens geldig voor zo lang mogelijk blijven.

## <a name="token-validation"></a>Validatie van tokens
een token toovalidate, uw app moet controleren zowel Hallo handtekening en claims van het Hallo-token.

Veel open-source bibliotheken zijn beschikbaar voor het valideren van JWTs, afhankelijk van uw voorkeurstaal. U wordt aangeraden dat u deze opties verkennen in plaats van uw eigen validatielogica implementeren. Hallo-informatie in deze handleiding kunt u meer informatie over hoe tooproperly die bibliotheken gebruiken.

### <a name="validate-hello-signature"></a>Hallo handtekening valideren
Een JWT bevat drie segmenten, gescheiden door Hallo `.` teken. Hallo eerste segment is Hallo *header*, tweede is Hallo Hallo *hoofdtekst*, en het derde is Hallo Hallo *handtekening*. Hallo handtekening segment mag gebruikte toovalidate Hallo authenticiteit van Hallo token zodat deze kan worden vertrouwd door uw app.

Azure AD B2C-tokens zijn ondertekend met behulp van industriestandaard asymmetrische algoritmen, zoals RSA 256. Hallo-header van Hallo token bevat informatie over Hallo-sleutel en versleutelingsmethode toosign Hallo-token hebt gebruikt:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Hallo `alg` claim geeft Hallo-algoritme dat gebruikt toosign Hallo-token is. Hallo `kid` claim geeft Hallo bepaalde openbare sleutel die gebruikt toosign Hallo-token is.

Azure AD kunt een token ondertekenen met behulp van een van een bepaalde set paren van openbare en persoonlijke sleutels op een bepaald moment. Azure AD draait Hallo mogelijke set sleutels periodiek, zodat uw app toohandle deze sleutel wordt automatisch gewijzigd worden geschreven. Een redelijke frequentie toocheck voor updates toohello openbare sleutels die worden gebruikt door Azure AD wordt elke 24 uur.

Azure AD B2C heeft een eindpunt met OpenID Connect metagegevens. Hierdoor kunnen apps toofetch informatie over Azure AD B2C tijdens runtime. Deze informatie omvat eindpunten, inhoud van tokens en token-ondertekening sleutels. Uw B2C-directory bevat een JSON-metagegevens-document voor elk beleid. Bijvoorbeeld, Hallo metagegevensdocument voor Hallo `b2c_1_sign_in` beleid in `fabrikamb2c.onmicrosoft.com` bevindt zich op:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`Hallo B2C-directory gebruikt tooauthenticate Hallo gebruiker, en `b2c_1_sign_in` is Hallo beleid tooacquire Hallo-token hebt gebruikt. toodetermine welk beleid gebruikte toosign een token is (en waar toogo toofetch Hallo metagegevens), hebt u twee opties. Eerst Hallo beleidsnaam is opgenomen in Hallo `acr` claim in Hallo-token. Claims buiten het Hallo-hoofdtekst van Hallo JWT door base 64-decodering Hallo instantie kunnen worden geparseerd en voor het deserialiseren van Hallo JSON tekenreeksen die als resultaat. Hallo `acr` claim Hallo-naam van Hallo-beleid dat gebruikt tooissue Hallo token is zijn.  De andere mogelijkheid is tooencode Hallo beleid in Hallo-waarde van Hallo `state` parameter wanneer u Hallo-aanvraag en decoderen vervolgens toodetermine welk beleid is gebruikt. Beide methoden is geldig.

Hallo-metagegevensdocument is een JSON-object dat nuttig stukjes informatie bevat. Het gaat hierbij om Hallo-locatie van Hallo eindpunten vereist tooperform OpenID Connect-verificatie. Ook `jwks_uri`, waardoor Hallo locatie van de set Hallo van openbare sleutels die gebruikt toosign tokens zijn. Die locatie hier is opgegeven, maar het is aanbevolen toofetch Hallo locatie dynamisch met behulp van het metagegevensdocument hello en parseren `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

Hallo JSON-document zich bij deze URL bevat alle Hallo informatie over openbare sleutels op een bepaald moment in gebruik. Uw app kunt Hallo `kid` claim in Hallo JWT-header tooselect Hallo openbare sleutel in Hallo JSON-document dat is gebruikt toosign-token van een bepaald. Validatie van handtekening kan vervolgens met behulp van de juiste openbare sleutel Hallo en Hallo aangegeven algoritme uitvoeren.

Een beschrijving van hoe de handtekeningvalidatie tooperform buiten Hallo bereik van dit document is. Veel open-source bibliotheken zijn beschikbaar toohelp u met dit als u deze nodig hebt.

### <a name="validate-hello-claims"></a>Hallo claims valideren
Wanneer uw app of API ontvangt een token ID, moet deze ook verschillende controles op basis van claims Hallo uitvoeren in Hallo-id-token. Deze omvatten, maar zijn niet beperkt tot:

* Hallo **doelgroep** claim: Hiermee wordt gecontroleerd dat Hallo-ID-token is beoogde toobe tooyour app gegeven.
* Hallo **niet voor** en **verlooptijd** claims: deze controleren dat Hallo-ID-token niet is verlopen.
* Hallo **verlener** claim: Hiermee wordt gecontroleerd dat token Hallo tooyour app is uitgegeven door Azure AD.
* Hallo **nonce**: dit is een strategie voor tokenreplay aanval risicobeperking.

Raadpleeg voor een volledige lijst van uw app moet worden uitgevoerd validaties toohello [specificatie van het OpenID Connect](https://openid.net). Details van Hallo verwachte waarden voor deze claims worden opgenomen in de voorgaande Hallo [token sectie](#types-of-tokens).  

## <a name="token-lifetimes"></a>Levensduur van token
Hallo levensduur van token na zijn opgegeven toofurther uw medeweten. Ze kunnen u helpen bij het ontwikkelen en foutopsporing van apps. Denk eraan dat uw apps mag geen tooexpect een van deze levensduur tooremain constante geschreven. Ze kunnen en wordt gewijzigd. Lees meer over Hallo [aanpassing van de levensduur van token](active-directory-b2c-token-session-sso.md) in Azure AD B2C.

| Token | Levensduur | Beschrijving |
| --- | --- | --- |
| ID-tokens |Een uur |ID-tokens zijn doorgaans geldig voor een uur. Uw web-app kunt gebruiken deze toomaintain levensduur van een eigen sessies met gebruikers (aanbevolen). U kunt ook de levensduur van een andere sessie. Als uw app tooget een nieuw token voor de ID moet, moet het toomake een nieuwe aanmeldingsverzoek tooAzure AD. Als een gebruiker een ongeldig browsersessie met Azure AD heeft, die gebruiker mogelijk niet meer vereist tooenter referenties opnieuw. |
| Vernieuwen van tokens |Too14 dagen |Een enkele vernieuwingstoken is geldig voor een maximum van 14 dagen. Echter kan een vernieuwingstoken op elk gewenst moment voor een aantal redenen ongeldig worden. Uw app moet tootry toouse een vernieuwingstoken blijven totdat het Hallo-aanvraag is mislukt, of uw app Hallo vernieuwingstoken vervangt door een nieuwe. Een vernieuwingstoken kan ook ongeldig als 90 dagen zijn verstreken nadat de gebruiker Hallo laatste aanmeldingsgegevens hebt opgegeven. |
| Autorisatiecodes |Vijf minuten |Autorisatiecodes zijn opzettelijk tijdelijke. Ze moeten worden ingewisseld onmiddellijk voor toegangstokens, ID-tokens of vernieuwen van tokens wanneer ze worden ontvangen. |

