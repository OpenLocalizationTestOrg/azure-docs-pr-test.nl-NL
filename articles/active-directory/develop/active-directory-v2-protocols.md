---
title: aaaLearn over Hallo autorisatie protocollen die worden ondersteund door Azure AD v2.0 | Microsoft Docs
description: Een handleiding tooprotocols wordt ondersteund door hello Azure AD v2.0-eindpunt.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# v2.0-protocollen - OAuth 2.0 & OpenID Connect
Hallo v2.0-eindpunt kunt Azure AD voor identity-as-a-service met de protocollen volgens de industrienorm, OpenID Connect en OAuth 2.0 gebruiken.  Hallo-service is compatibel met de standaarden, kunnen er subtiele verschillen tussen de twee implementaties van deze protocollen.  Hallo informatie hier is handig als u ervoor toowrite uw code kiezen door rechtstreeks verzenden & afhandeling van HTTP-aanvragen of gebruik een 3rd partij open source bibliotheek in plaats van met een van onze open-source bibliotheken.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

## Hallo basisbeginselen
In bijna alle OAuth & OpenID Connect stromen zijn er vier partijen betrokken bij Hallo exchange:

![OAuth 2.0-functies](../../media/active-directory-v2-flows/protocols_roles.png)

* Hallo **autorisatie Server** Hallo v2.0-eindpunt is.  Het is verantwoordelijk voor gezorgd Hallo gebruikersidentiteit, verlenen en intrekken van toegang tooresources en uitgifte van tokens.  Het is ook bekend als identiteitsprovider Hallo - iets veilig worden verwerkt toodo met Hallo van de gebruiker informatie, hun toegang en Hallo vertrouwensrelaties tussen partijen in een stroom.
* Hallo **Resource-eigenaar** is doorgaans Hallo door eindgebruikers.  Het is Hallo-partij die eigenaar is van Hallo gegevens, en heeft Hallo power tooallow derden tooaccess die gegevens of de resource.
* Hallo **OAuth Client** wordt uw app, geïdentificeerd door de toepassings-id.  Dit is meestal Hallo partij dat Hallo eindgebruikers interactie met en het tokens van Hallo autorisatie server aanvraagt.  Hallo-client moet verlenen machtiging tooaccess resource Hallo Hallo resource-eigenaar.
* Hallo **bronserver** is waarin Hallo bron of de gegevens zich bevindt.  Deze vertrouwt Hallo autorisatie Server toosecurely verifiëren en autoriseren hello OAuth-Client en maakt gebruik van Bearer access_tokens tooensure die toegang hebben tot de resource tooa kan worden verleend.

## App-registratie
Elke app die gebruikmaakt van Hallo v2.0-eindpunt moet toobe geregistreerd bij [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) voordat deze kan communiceren met OAuth of OpenID Connect.  Hallo app registratieproces wordt verzamelen & enkele waarden tooyour app toewijzen:

* Een **toepassings-Id** die wordt aangeduid uw app
* Een **omleidings-URI** of **-pakket-id** die kunnen worden gebruikt toodirect antwoorden back tooyour app
* Enkele andere scenariospecifieke waarden.

Voor meer informatie, meer informatie over hoe te[een app registreren](active-directory-v2-app-registration.md).

## Eindpunten
Na de registratie communiceert Hallo-app met Azure AD door te verzenden aanvragen toohello v2.0-eindpunt:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Waar Hallo `{tenant}` kan duren voordat een van de vier verschillende waarden:

| Waarde | Beschrijving |
| --- | --- |
| `common` |Kunnen gebruikers met persoonlijke Microsoft-accounts en werk/schoolaccounts van Azure Active Directory-toosign in Hallo-toepassing. |
| `organizations` |Kunnen alleen gebruikers met werk/schoolaccounts van Azure Active Directory-toosign in Hallo-toepassing. |
| `consumers` |Kunnen alleen gebruikers met persoonlijke Microsoft-accounts (MSA) toosign in Hallo-toepassing. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` of `contoso.onmicrosoft.com` |Kunnen alleen gebruikers met werk/schoolaccounts van een bepaald Azure Active Directory-tenant toosign in Hallo-toepassing.  Een beschrijvende domeinnaam Hallo van hello Azure AD-tenant of guid-id van Hallo tenant kan worden gebruikt. |

Voor meer informatie over het toointeract met deze eindpunten, met een bepaalde app-type onderstaande kiezen.

## Tokens
Hallo v2.0-implementatie van OAuth 2.0 en OpenID Connect maken intensief gebruik van bearer-tokens, weergegeven als JWTs bearer-tokens. Een bearer-token is een lichtgewicht beveiligingstoken dat verleent 'bearer' toegang tooa Hallo beveiligde resource. In dit opzicht is Hallo 'bearer' een partij die Hallo token kan opleveren. Hoewel een partij moet eerst worden geverifieerd bij Azure AD tooreceive hello bearer-token, als Hallo vereist stappen worden niet genomen toosecure Hallo-token in overdracht en opslag, kunt u het probleem is onderschept en gebruikt door een onbedoelde partij. Sommige beveiligingstokens beschikken over een ingebouwde mechanisme om te voorkomen dat onbevoegden kunnen gebruiken, worden de bearer-tokens hebben geen dit mechanisme en moeten worden overgebracht in een beveiligd kanaal zoals transport layer security (HTTPS). Als een bearer-token wordt verzonden in Hallo wissen, wordt een man-in Hallo middelste aanval kan worden gebruikt door een kwaadwillende tooacquire Hallo-token en gebruiken voor een resource van de beveiligde tooa onbevoegde toegang. Hallo dezelfde beveiligings-principals van toepassing wanneer caching bearer-tokens voor later gebruik of op te slaan. Altijd voor zorgen dat uw app verzendt en bearer-tokens worden opgeslagen op een veilige manier. Zie voor meer beveiligingsoverwegingen op bearer-tokens [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).

Meer informatie over de verschillende typen tokens die worden gebruikt in Hallo v2.0-eindpunt is beschikbaar in [Hallo v2.0-eindpunt tokenverwijzing](active-directory-v2-tokens.md).

## Protocollen
Als u klaar toosee voorbeelden aanvraagt bent, aan de slag met een van de Hallo hieronder zelfstudies.  Elke tooa bepaalde verificatiescenario komt overeen.  Als u hulp bij het bepalen dat de juiste stroom Hallo voor u nodig hebt, kijk dan eens [typen apps kunt u met de Hallo v2.0 Hallo](active-directory-v2-flows.md).

* [Mobiele en systeemeigen toepassing met OAuth 2.0 bouwen](active-directory-v2-protocols-oauth-code.md)
* [Maken van Web Apps met Open ID Connect](active-directory-v2-protocols-oidc.md)
* [Apps met één pagina bij het maken van Hallo OAuth 2.0 impliciete stromen](active-directory-v2-protocols-implicit.md)
* [Daemons of processen op de Server bij het maken van Hallo OAuth 2.0-Client referenties stromen](active-directory-v2-protocols-oauth-client-creds.md)
* [Ophalen van tokens in een Web-API met Hallo OAuth 2.0 namens stromen](active-directory-v2-protocols-oauth-on-behalf-of.md)
