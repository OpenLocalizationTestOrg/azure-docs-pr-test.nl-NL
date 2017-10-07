---
title: Active Directory-v2.0 aaaAzure tokens verwijzing | Microsoft Docs
description: Hallo typen tokens en claims die worden verzonden door hello Azure AD v2.0-eindpunt
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Overzicht van Azure Active Directory v2.0-tokens
Hello Azure Active Directory (Azure AD) v2.0-eindpunt verzendt verschillende typen beveiligingstokens in elk [authenticatiestroom](active-directory-v2-flows.md). Deze verwijzing beschrijft Hallo-indeling, de beveiligingskenmerken en de inhoud van elk type token.

> [!NOTE]
> Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen. toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Typen tokens
Hallo v2.0-eindpunt ondersteunt Hallo [OAuth 2.0-protocol voor autorisatie](active-directory-v2-protocols.md), welke maakt gebruik van tokens en vernieuw tokens. Hallo v2.0-eindpunt biedt ook ondersteuning voor verificatie en meld u via [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect introduceert een derde type token, Hallo-id-token. Elk van deze tokens wordt weergegeven als een *bearer* token.

Een bearer-token is een lichtgewicht beveiligingstoken dat verleent bearer toegang tooa Hallo beveiligde resource. Hallo bearer is een partij die Hallo token kan opleveren. Hoewel een partij moet worden geverifieerd bij Azure AD tooreceive hello bearer-token, als deze stappen zijn toosecure Hallo token niet gebruikt tijdens de overdracht en opslag, kunt u het probleem is onderschept en gebruikt door een onbedoelde partij. Sommige beveiligingstokens hebben een ingebouwde mechanisme tooprevent niet-geautoriseerde partijen niet, maar bearer-tokens wilt gebruiken. Bearer-tokens moeten in een beveiligd kanaal zoals transport layer security (HTTPS) worden getransporteerd. Als een bearer-token wordt verzonden zonder dat dit type beveiliging, een schadelijke party een token 'man-in-the-middle-aanval' tooacquire hello te gebruiken en gebruiken voor toegang door onbevoegden tooa beveiligde resource. Hallo dezelfde beveiligings-principals van toepassing wanneer caching bearer-tokens voor later gebruik of op te slaan. Altijd voor zorgen dat uw app veilig worden verzonden en bearer-tokens slaat. Zie voor meer beveiligingsoverwegingen voor bearer-tokens, [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).

Veel van Hallo-tokens die zijn uitgegeven door Hallo v2.0-eindpunt worden geïmplementeerd als JSON Web Tokens (JWTs). Een JWT is een compact, URL-veilige manier tootransfer informatie tussen twee partijen. Hallo-informatie in een JWT wordt aangeroepen een *claim*. Het is een bewering van informatie over Hallo bearer en het onderwerp van het Hallo-token. Hallo-claims in een JWT zijn JSON JavaScript Object Notation ()-objecten die zijn gecodeerd en geserialiseerd voor verzending. Omdat de Hallo JWTs uitgegeven door Hallo v2.0-eindpunt zijn ondertekend, maar niet versleuteld, controleert u eenvoudig hello inhoud van een JWT voor foutopsporing. Zie voor meer informatie over JWTs hello [JWT-specificatie](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>ID-tokens
Een token ID is een vorm van aanmelden beveiligingstoken dat uw app ontvangt wanneer wordt verificatie uitgevoerd via [OpenID Connect](active-directory-v2-protocols.md). ID-tokens worden weergegeven als [JWTs](#types-of-tokens), en bevatten claims die u toosign Hallo gebruiker in tooyour app kunt gebruiken. U kunt Hallo claims kunt gebruiken in een token ID op verschillende manieren. Normaal gesproken gebruik admins ID tokens toodisplay accountgegevens of toomake wijze het toegangsbeheer in een app. Hallo v2.0-eindpunt problemen die slechts één type token ID, waarvoor een consistente set claims, ongeacht het Hallo-type van de gebruiker die is aangemeld. Hallo-indeling en inhoud van de ID-tokens worden Hallo dezelfde voor persoonlijke Microsoft-accountgebruikers en werk-of schoolaccounts.

ID-tokens worden op dit moment is ondertekend, maar niet versleuteld. Wanneer uw app een token ID ontvangt, moet deze [Hallo handtekening valideren](#validating-tokens) tooprove Hallo echtheid van het token en enkele claims in het token tooprove Hallo de geldigheid te valideren. Hallo claims gevalideerd door een app variëren afhankelijk van de scenariovereisten voor, maar uw app moet uitvoeren sommige [algemene claim validaties](#validating-tokens) in elk scenario.

We bieden u volledige informatie over claims in de ID-tokens in Hallo Hallo volgende secties bovendien tooa ID voorbeeldtoken. Houd er rekening mee dat de claims in de ID-tokens niet in een bepaalde volgorde worden geretourneerd. Nieuwe claims kunnen ook worden opgenomen in de ID-tokens op elk gewenst moment. Uw app beter niet verbreken wanneer nieuwe claims zijn geïntroduceerd. Hallo volgende lijst bevat Hallo claims die uw app momenteel betrouwbaar herkent. U vindt meer informatie in Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Voorbeeldtoken-ID
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Oefening tooinspect hello voorbeeldtoken-ID in Hallo-claims in Hallo-voorbeeldtoken ID plakken [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Claims in de ID-tokens
| Naam | Claim | Voorbeeldwaarde | Beschrijving |
| --- | --- | --- | --- |
| doelgroep |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identificeert Hallo bedoeld ontvanger van Hallo-token. Hallo doelgroep is in de ID-tokens van uw app toepassings-ID, tooyour-app in de Portal voor registratie van Microsoft-toepassing hello toegewezen. Uw app moet deze waarde niet valideren en Hallo token afwijzen als Hallo waarde komt niet overeen met. |
| certificaatverlener |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identificeert Hallo beveiligingstokenservice (STS) die wordt gemaakt en retourneert Hallo-token en hello Azure AD-tenant in welke Hallo gebruiker werd geverifieerd. Uw app moet Hallo verlener claim tooensure die Hallo token afkomstig zijn van Hallo v2.0-eindpunt te valideren. Het moet ook Hallo GUID-gedeelte van Hallo toorestrict Hallo claimset van tenants die zich toohello app aanmelden kunt gebruiken. Hallo GUID die die gebruiker Hallo aangeeft is een consumer gebruiker uit een Microsoft-account is `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| verleend aan |`iat` |`1452285331` |Hallo tijd op welke Hallo token is uitgegeven, epoche tijd. |
| verlooptijd |`exp` |`1452289231` |Hallo tijd op welke Hallo token is ongeldig, weergegeven in de epoche tijd. Uw app moet deze claim tooverify Hallo geldigheid van de levensduur van token hello gebruiken. |
| niet voor |`nbf` |`1452285331` |Hallo-tijd op welke Hallo token geldig is, wordt weergegeven in de epoche tijd. Dit is dezelfde meestal Hallo Hallo uitgifte tijd. Uw app moet deze claim tooverify Hallo geldigheid van de levensduur van token hello gebruiken. |
| Versie |`ver` |`2.0` |Hallo-versie van Hallo ID token, zoals gedefinieerd door Azure AD. Hallo-waarde voor het Hallo-v2.0-eindpunt heeft `2.0`. |
| Tenant-ID |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Een GUID die hello Azure AD-tenant die gebruiker Hallo vertegenwoordigt is afkomstig uit. Voor werk- en schoolaccounts-accounts is Hallo GUID Hallo onveranderbare tenant-ID van Hallo organisatie die Hallo gebruiker behoort. Hallo-waarde voor persoonlijke accounts heeft `9188040d-6c67-4c5b-b112-36a304b66dad`. Hallo `profile` bereik is vereist in volgorde tooreceive deze claim. |
| code-hash |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Hallo code hash is opgenomen in de ID-tokens, alleen wanneer het Hallo-id-token is uitgegeven door een OAuth 2.0-autorisatie-code. Het kan gebruikte toovalidate Hallo echtheid van een autorisatiecode zijn. Zie voor meer informatie over het uitvoeren van deze validatie Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html). |
| token hash toegang |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Hallo access token hash is opgenomen in de ID-tokens, alleen wanneer het Hallo-id-token is uitgegeven met een OAuth 2.0-toegangstoken. Het kan gebruikte toovalidate Hallo echtheid van een toegangstoken zijn. Zie voor meer informatie over het uitvoeren van deze validatie Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html). |
| nonce |`nonce` |`12345` |Hallo nonce is een strategie voor het oplossen van token replay-aanvallen. Uw app een nonce kunt opgeven in een aanvraag voor verificatie met behulp van Hallo `nonce` queryparameter. Hallo-waarde die u in Hallo-aanvraag opgeeft is verzonden in Hallo-ID van het token `nonce` claim, ongewijzigd. Uw app kunt controleren of de waarde van de Hallo ten opzichte van het opgegeven op Hallo-aanvraag die sessie Hallo-app aan een specifieke ID token koppelt Hallo-waarde. Uw app moet deze validatie tijdens Hallo ID token validatie uitvoeren. |
| naam |`name` |`Babe Ruth` |Hallo-naamclaim biedt een leesbare waarde die Hallo onderwerp van Hallo-token aangeeft. Hallo-waarde kan niet worden gegarandeerd toobe unieke veranderlijke is en is ontworpen toobe alleen ter informatie weergegeven. Hallo `profile` bereik is vereist in volgorde tooreceive deze claim. |
| E-mail |`email` |`thegreatbambino@nyy.onmicrosoft.com` |Hallo primaire e-mailadres is gekoppeld aan de gebruikersaccount hello, indien aanwezig. De waarde ervan is veranderlijke en na verloop van tijd kan wijzigen. Hallo `email` bereik is vereist in volgorde tooreceive deze claim. |
| voorkeur gebruikersnaam |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Primaire gebruikersnaam Hallo die staat voor de gebruiker Hallo in Hallo v2.0-eindpunt. Het is mogelijk een e-mailadres, telefoonnummer of een algemene gebruikersnaam zonder een specifieke indeling. De waarde ervan is veranderlijke en na verloop van tijd kan wijzigen. Hallo `profile` bereik is vereist in volgorde tooreceive deze claim. |
| Onderwerp |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | Hallo-principal over welke Hallo asserts token informatie, zoals Hallo gebruiker van een app. Deze waarde is onveranderbaar en kan niet worden toegewezen of opnieuw gebruikt. Kan het zijn gebruikte tooperform autorisatie controles veilig, zoals wanneer Hallo token gebruikte tooaccess is een resource en kan worden gebruikt als een sleutel in databasetabellen. Omdat Hallo onderwerp altijd aanwezig is in Hallo tokens die Azure AD geeft, wordt u aangeraden deze waarde in een algemeen autorisatiesysteem. Hallo-onderwerp is echter een pairwise id - het is uniek tooa bepaalde toepassing-ID.  Daarom als één gebruiker zich bij twee verschillende apps met behulp van twee andere client-ID aanmeldt, ontvangt deze apps twee verschillende waarden voor Hallo onderwerp claim.  Dit kan of kan niet worden gewenst afhankelijk van uw architectuur en privacy-vereisten. |
| object-ID |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Hallo onveranderbare id voor een object in Hallo Microsoft identity-systeem, in dit geval wordt een gebruikersaccount.  Het kan ook gebruikte tooperform autorisatie controles zijn veilig en als de sleutel in databasetabellen. Deze ID is uniek voor Hallo gebruiker alle toepassingen - twee verschillende toepassingen Hallo dezelfde gebruiker ontvangt aanmelden Hallo dezelfde waarde in Hallo `oid` claim.  Dit betekent dat deze kan worden gebruikt bij het maken van query's tooMicrosoft online services, zoals Hallo Microsoft Graph.  Hallo Microsoft Graph retourneert deze ID als Hallo `id` eigenschap voor een bepaald gebruikersaccount.  Omdat Hallo `oid` kunnen meerdere apps toocorrelate gebruikers, hello `profile` bereik is vereist in volgorde tooreceive deze claim. Houd er rekening mee dat als een enkele gebruiker in meerdere tenants bestaat, Hallo gebruiker een ander object-ID in elke tenant bevat-deze worden beschouwd als andere accounts, zelfs als de gebruiker zich aanmeldt Hallo in elke rekening met de Hallo dezelfde referenties. |

### <a name="access-tokens"></a>Toegangstokens
Toegangstokens die zijn uitgegeven door Hallo v2.0-eindpunt kunnen op dit moment wordt alleen door Microsoft-Services worden verbruikt. Uw apps nodig niet tooperform validatie of inspectie van toegangstokens voor scenario's Hallo momenteel niet ondersteund. U kunt toegangstokens behandelen als een mat. Ze zijn alleen tekenreeksen die uw app tooMicrosoft HTTP-aanvragen doorgeven kunt.

In Hallo bij toekomstige, Hallo v2.0 vindt eindpunt Hallo mogelijkheid voor uw app tooreceive toegangstokens van andere clients. Hallo-informatie in dit naslagonderwerp wordt op dat moment wordt bijgewerkt met Hallo-informatie die u nodig hebt voor uw app tooperform token validatie van servertoegang op en andere vergelijkbare taken.

Wanneer u het Hallo v2.0-eindpunt van een toegangstoken aanvraagt, retourneert Hallo v2.0-eindpunt ook metagegevens over Hallo toegangstoken voor uw app toouse. Deze informatie omvat het verlooptijdstip Hallo van Hallo-toegangstoken en Hallo scopes waarvoor geldig is. Uw app gebruikmaakt van deze metagegevens tooperform Intelligente caching van toegangstokens zonder tooparse open Hallo toegangstoken zelf.

### <a name="refresh-tokens"></a>Vernieuwen van tokens
Vernieuwen van tokens zijn beveiligingstokens die uw app tooget nieuwe gebruiken kunt toegang tokens in een OAuth 2.0-stroom. Uw app kunt vernieuwen van tokens tooachieve op lange termijn toegang tooresources namens een gebruiker zonder interactie met Hallo-gebruiker gebruiken.

Vernieuwen van tokens zijn meerdere resource. Een vernieuwingstoken dat is ontvangen tijdens een tokenaanvraag voor één resource kan worden ingewisseld voor toegang tot tokens tooa andere resource.

tooreceive vernieuwen in een token antwoord, uw app moet aanvragen en Hallo worden verleend `offline_acesss` bereik. meer informatie over Hallo toolearn `offline_access` bereik, Zie Hallo [toestemming en scopes](active-directory-v2-scopes.md) artikel.

Vernieuwen van tokens, en altijd zullen zijn, een mat tooyour app. Ze kunnen zijn uitgegeven door hello Azure AD v2.0-eindpunt en alleen worden gecontroleerd en geïnterpreteerd door Hallo v2.0-eindpunt. Ze zijn lange levensduur hebben, maar uw app niet worden geschreven tooexpect die een vernieuwingstoken voor een periode duurt. Vernieuwen van tokens kunnen op elk moment om verschillende redenen zijn ongeldig. Hallo enige manier om uw app tooknow als een vernieuwingstoken geldig tooattempt tooredeem is het door het maken van een tokenaanvraag toohello v2.0-eindpunt.

Wanneer u een vernieuwingstoken voor een nieuw toegangstoken inwisselen (en als uw app had gekregen Hallo `offline_access` bereik), ontvangt u een nieuwe vernieuwingstoken in token antwoord Hallo. Hallo zojuist uitgegeven vernieuwen token, tooreplace Hallo u gebruikt in Hallo aanvraag opslaan. Dit zorgt ervoor dat het vernieuwen van tokens geldig voor zo lang mogelijk blijven.

## <a name="validating-tokens"></a>Valideren van tokens
Op dit moment alleen token validatie van uw apps hoeft Hallo tooperform ID-tokens wordt gevalideerd. een token ID toovalidate, uw app moet beide Hallo-ID van het token van handtekening en Hallo claims in de ID-token Hallo valideren.

<!-- TODO: Link -->
Microsoft biedt bibliotheken en codevoorbeelden die u laten zien hoe de validatie van tokens voor het verwerken van tooeasily. In de volgende secties hello beschrijven we Hallo onderliggende proces. Er zijn verschillende van derden open source-bibliotheken beschikbaar voor de validatie van JWT. Er is ten minste één tapewisselaar optie voor bijna elk platform- en taalinstellingen.

### <a name="validate-hello-signature"></a>Hallo handtekening valideren
Een JWT bevat drie segmenten die worden gescheiden door Hallo `.` teken. Hallo eerste segment wordt ook wel Hallo *header*, tweede Hallo-segment is Hallo *hoofdtekst*, en de derde segment Hallo Hallo *handtekening*. Hallo handtekening segment kan gebruikte toovalidate Hallo authenticiteit van Hallo-id-token zijn, zodat deze kan worden vertrouwd door uw app.

ID-tokens zijn ondertekend met behulp van industriestandaard asymmetrische algoritmen, zoals RSA 256. Hallo-header van het Hallo-id-token heeft informatie over het Hallo-sleutel en versleutelingsmethode toosign Hallo-token hebt gebruikt. Bijvoorbeeld:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Hallo `alg` claim geeft Hallo-algoritme dat gebruikt toosign Hallo-token is. Hallo `kid` claim geeft Hallo openbare sleutel die gebruikt toosign Hallo-token is.

Op elk gewenst moment kan Hallo v2.0-eindpunt een token ID ondertekenen met behulp van een van een specifieke set paren van openbare en persoonlijke sleutels. Hallo v2.0-eindpunt draait periodiek Hallo mogelijke set van sleutels, zodat uw app toohandle deze sleutel wordt automatisch gewijzigd worden geschreven. Een redelijke frequentie toocheck voor updates toohello openbare sleutels die worden gebruikt door Hallo v2.0-eindpunt is elke 24 uur.

U kunt ondertekenen van belangrijke gegevens die u nodig hebt toovalidate Hallo handtekening met behulp van Hallo OpenID Connect metagegevensdocument zich bevindt op Hallo verkrijgen:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Probeer Hallo-URL in een browser.
>
>

Dit metagegevensdocument is een JSON-object dat is nuttig stukjes informatie, zoals locatie Hallo Hallo verschillende eindpunten voor OpenID Connect-verificatie vereist.  Hallo-document bevat ook een *jwks_uri*, toosign tokens waardoor Hallo-locatie van de set Hallo van openbare sleutels worden gebruikt. Hallo JSON-document vinden op het Hallo jwks_uri heeft alle Hallo openbare sleutelinformatie die momenteel in gebruik is. Uw app kunt Hallo `kid` claim in Hallo JWT-header tooselect welke openbare sleutel in dit document gebruikte toosign is een token. Vervolgens voert deze validatie van handtekening met behulp van de juiste openbare sleutel Hallo en Hallo aangegeven algoritme.

Het valideren van de handtekening is buiten Hallo-bereik van dit document. Veel open source-bibliotheken zijn beschikbaar toohelp u dit.

### <a name="validate-hello-claims"></a>Hallo claims valideren
Wanneer uw app een token ID van de gebruiker zich aanmelden ontvangt, moet deze ook een aantal controles op basis van claims Hallo uitvoeren in Hallo-id-token. Deze omvatten, maar zijn niet beperkt tot:

* **doelgroep** claim, tooverify die de token ID Hallo beoogde toobe gegeven tooyour app is
* **niet voor** en **verlooptijd** claims, tooverify die Hallo token ID niet is verlopen
* **certificaatverlener** claim, tooverify die Hallo token tooyour app is uitgegeven door Hallo v2.0-eindpunt
* **nonce**, als een token replay-aanvallen risicobeperking

Zie voor een volledige lijst van claim validaties die moet worden uitgevoerd in uw app Hallo [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Details van de Hallo verwachte waarden voor deze claims worden opgenomen in Hallo [ID-tokens](# ID tokens) sectie.

## <a name="token-lifetimes"></a>Levensduur van token
We bieden Hallo na token levensduur uitsluitend ter informatie. Hallo informatie kan u helpen bij het ontwikkelen en foutopsporing van apps. Uw apps mag geen tooexpect een van deze levensduur tooremain constante geschreven. Token kan levensduur en op elk gewenst moment wordt gewijzigd.

| Token | Levensduur | Beschrijving |
| --- | --- | --- |
| ID-tokens (werk of school-accounts) |1 uur |ID-tokens zijn meestal geldig 1 uur. Uw web-app kunt gebruiken deze dezelfde levensduur toomaintain een eigen sessie met Hallo gebruiker (aanbevolen), of u ervoor de levensduur van een andere sessie kiezen kunt. Als uw app een nieuwe ID token tooget moet, moet deze toomake een nieuwe aanmelden aanvraag toohello v2.0 autoriseren eindpunt. Als Hallo gebruiker een ongeldig browsersessie met Hallo v2.0-eindpunt heeft, Hallo-gebruiker kan niet worden vereist tooenter hun referenties opnieuw. |
| ID-tokens (persoonlijke accounts) |24 uur |ID-tokens voor persoonlijke accounts zijn meestal geldig 24 uur. Uw web-app kunt gebruiken deze dezelfde levensduur toomaintain een eigen sessie met Hallo gebruiker (aanbevolen), of u ervoor de levensduur van een andere sessie kiezen kunt. Als uw app een nieuwe ID token tooget moet, moet deze toomake een nieuwe aanmelden aanvraag toohello v2.0 autoriseren eindpunt. Als Hallo gebruiker een ongeldig browsersessie met Hallo v2.0-eindpunt heeft, Hallo-gebruiker kan niet worden vereist tooenter hun referenties opnieuw. |
| Toegangstokens (werk of school-accounts) |1 uur |In token antwoorden aangeduid als onderdeel van het token Hallo-metagegevens. |
| Toegangstokens (persoonlijke accounts) |1 uur |In token antwoorden aangeduid als onderdeel van het token Hallo-metagegevens. Toegangstokens die zijn uitgegeven namens persoonlijke accounts kunnen worden geconfigureerd voor de levensduur van een andere, maar 1 uur is standaard. |
| Vernieuwen van tokens (werk of school-account) |Too14 dagen |Een enkele vernieuwingstoken is geldig voor een maximum van 14 dagen. Hallo-vernieuwingstoken mogelijk worden in op elk gewenst moment om verschillende redenen ongeldig zodat uw app tootry toouse een vernieuwingstoken moet blijven totdat deze is mislukt, of tot uw app wordt vervangen door een nieuw vernieuwingstoken. Er wordt een vernieuwingstoken ongeldig als het al 90 dagen geleden Hallo gebruiker hun referenties heeft ingevoerd. |
| Vernieuwen van tokens (persoonlijke accounts) |Too1 jaar |Een enkele vernieuwingstoken is geldig voor een maximum van 1 jaar. Echter Hallo vernieuwingstoken ongeldig worden op elk gewenst moment om verschillende redenen, zodat uw app moet blijven tootry toouse een vernieuwingstoken totdat het mislukt. |
| Autorisatiecodes (werk of school-accounts) |10 minuten |Autorisatiecodes zijn opzettelijk tijdelijke en onmiddellijk moeten worden ingewisseld voor toegangstokens en vernieuwen van tokens wanneer Hallo tokens worden ontvangen. |
| Autorisatiecodes (persoonlijke accounts) |5 minuten |Autorisatiecodes zijn opzettelijk tijdelijke en onmiddellijk moeten worden ingewisseld voor toegangstokens en vernieuwen van tokens wanneer Hallo tokens worden ontvangen. Er zijn autorisatiecodes die namens persoonlijke accounts worden verleend voor eenmalig gebruik. |
