---
title: aaaChanges toohello Azure AD v2.0-eindpunt | Microsoft Docs
description: Een beschrijving van wijzigingen die toohello app model v2.0 openbare preview-protocollen worden uitgevoerd.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>Belangrijke Updates toohello v2.0 verificatieprotocollen
Ontwikkelaars aandacht! Via Hallo brengen volgende twee weken, we een aantal updates tooour v2.0-verificatieprotocollen die u kunnen betekenen dat de wijzigingen voor alle apps die u hebt geschreven in onze preview-periode op te splitsen.  

## <a name="who-does-this-affect"></a>Wie heeft dit invloed op?
Alle apps die zijn geschreven toouse Hallo v2.0 geconvergeerde eindpunt voor authenticatie

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Meer informatie over het v2.0-eindpunt Hallo vindt [hier](active-directory-appmodel-v2-overview.md).

Als u een app met Hallo v2.0-eindpunt door rechtstreeks toohello v2.0 protocol coderen hebt gebouwd met een van onze middlewares OpenID Connect of OAuth web of andere 3e partij bibliotheken tooperform verificatie gebruikt, u moet voorbereid tootest projecten en maken wijzigingen indien nodig.

## <a name="who-doesnt-this-affect"></a>Wie heeft niet dit invloed op?
Alle apps die zijn geschreven voor Hallo productie Azure AD authentication eindpunt

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Dit protocol is ingesteld in steen en worden geen wijzigingen in de problemen.

Bovendien als uw app **alleen** onze ADAL-bibliotheek tooperform verificatie, gebruikt u hebt geen toochange alles.  ADAL, is uw app uit Hallo wijzigingen afgeschermd.  

## <a name="what-are-hello-changes"></a>Wat zijn Hallo wijzigingen?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Hallo x5t waarde verwijderen uit een JWT-headers
Hallo v2.0-eindpunt maakt gebruik van JWT-tokens uitgebreid, die een gedeelte van de parameters header met relevante metagegevens over Hallo token bevatten.  Als u Hallo-header van een van onze huidige JWTs decoderen, zou u ongeveer vinden:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Waar de eigenschappen van beide Hallo 'x5t' en 'kind' hello openbare sleutel identificeren die moet gebruikte toovalidate Hallo token handtekening, zoals het ophalen van metagegevens-eindpunt met OpenID Connect Hallo.

Hallo wijziging we hier maken is tooremove Hallo 'x5t'-eigenschap.  U kunt doorgaan toouse Hallo dezelfde mechanismen toovalidate tokens, maar verstandig alleen op Hallo 'kind' eigenschap tooretrieve Hallo juiste openbare sleutel, als de opgegeven in de Hallo OpenID Connect-protocol. 

> [!IMPORTANT]
> **Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo Hallo x5t waarde bestaan.**
> 
> 

### <a name="removing-profileinfo"></a>Profile_info verwijderen
Voorheen Hallo v2.0-eindpunt is is een base64-gecodeerd JSON-object in retourneren token antwoorden aangeroepen `profile_info`.  Bij het aanvragen van een toegangstoken van Hallo v2.0-eindpunt met het verzenden van een aanvraag naar:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

antwoord Hallo eruit als Hallo JSON-object te volgen:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hallo `profile_info` waarde bevat informatie over Hallo-gebruiker die zich aangemeld op Hallo app - hun weergavenaam, de voornaam, achternaam, e-mailadres, id, enzovoort.  Hallo voornamelijk om `profile_info` is gebruikt voor het opslaan van token en op het scherm.

Hallo worden nu verwijderd `profile_info` waarde – maar maak je geen zorgen, bieden we nog steeds deze toodevelopers informatie op een iets andere plaats.  In plaats van `profile_info`, Hallo v2.0-eindpunt resulteert nu een `id_token` in elk token antwoord:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

U kunt decoderen en parseren Hallo id_token tooretrieve Hallo dezelfde informatie die u hebt ontvangen van profile_info.  Hallo id_token is een JSON Web Token (JWT), met inhoud zoals opgegeven door het OpenID Connect.  Hallo code Hiertoe moet vergelijkbaar: u hoeft alleen tooextract Hallo midden segment (tekst hello) van Hallo id_token en base64 dit tooaccess Hallo JSON-object binnen decoderen.

Via Hallo volgende twee weken, u moet de code van uw app tooretrieve Hallo gebruikersgegevens uit beide Hallo `id_token` of `profile_info`; afhankelijk van wat aanwezig is.  Op die manier wanneer Hallo wijziging wordt aangebracht uw app aankan naadloos Hallo overgang van `profile_info` te`id_token` zonder onderbreking.

> [!IMPORTANT]
> **Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo bestaan Hallo `profile_info` waarde.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Id_token_expires_in verwijderen
Vergelijkbare te`profile_info`, worden ook verwijderd Hallo `id_token_expires_in` parameter van antwoorden.  Voorheen Hallo v2.0-eindpunt zou waarde retourneren voor `id_token_expires_in` samen met elke id_token antwoord, bijvoorbeeld in een antwoord autoriseren:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Of in een token antwoord:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hallo `id_token_expires_in` waarde duidt dit op het aantal seconden Hallo id_token blijft geldig voor Hallo.  Nu we Hallo verwijdert `id_token_expires_in` volledig waarde.  In plaats daarvan kunt u Hallo OpenID Connect standaard `nbf` en `exp` tooexamine Hallo geldigheid van een id_token claims.  Zie Hallo [v2.0 tokenverwijzing](active-directory-v2-tokens.md) voor meer informatie over deze claims.

> [!IMPORTANT]
> **Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo bestaan Hallo `id_token_expires_in` waarde.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Hallo claims geretourneerd door een bereik wijzigen openid =
Deze wijziging wordt de meest significante – Hallo in feite, heeft dit gevolgen voor vrijwel elke app die gebruikmaakt van Hallo v2.0-eindpunt.  Veel toepassingen verzenden aanvragen toohello v2.0-eindpunt met Hallo `openid` bereik, zoals:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Vandaag, wanneer Hallo gebruiker toestemming voor Hallo verleent `openid` bereik, uw app ontvangt een schat aan informatie over Hallo gebruiker in de resulterende id_token Hallo.  Deze claims kunnen opnemen hun naam, voorkeur gebruikersnaam, e-mailadres, object-ID en meer.

In deze update we wijzigt Hallo informatie die Hallo `openid` bereik kan uw apptoegang tot, toobetter comform Hello OpenID Connect-specificatie.  Hallo `openid` bereik wordt alleen toestaan van uw app toosign Hallo gebruiker in en ontvangt een app-specifiek-id voor de gebruiker Hallo in Hallo `sub` van Hallo id_token claim.  claims in een id_token Hallo alleen hello `openid` bereik verleend worden persoonlijke gegevens.  Voorbeeld id_token claims zijn:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Als u tooobtain persoonsgegevens (PII) over Hallo gebruiker in uw app wilt, moet uw app toorequest extra machtigingen van Hallo-gebruiker.  We introduceert ondersteuning voor twee nieuwe scopes uit Hallo OpenID Connect spec – hello `email` en `profile` scopes – waarmee u toodo dus.

* Hallo `email` bereik is zeer eenvoudig: het primaire e-mailadres van uw app toegang toohello gebruiker via Hallo kunt `email` in Hallo id_token claim.  Houd er rekening mee dat Hallo `email` claim altijd worden niet aanwezig in id_tokens – het alleen worden opgenomen als beschikbaar in Hallo gebruikersprofiel.
* Hallo `profile` bereik kan uw app toegang tooall andere basisinformatie over Hallo gebruiker – de naam, de voorkeur username, object-ID, enzovoort.

Hiermee kunt u toocode uw app op een wijze minimale openbaarmaking – vraagt u Hallo gebruiker voor NET Hallo reeks gegevens dat uw app toodo de taak vereist.  Als u ophalen van de volledige set Hallo gebruikersgegevens die uw app momenteel ontvangt toocontinue wilt, moet u alle drie bereiken opnemen in uw autorisatieaanvragen:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Uw app kunt beginnen met het verzenden van Hallo `email` en `profile` onmiddellijk bereiken en Hallo v2.0-eindpunt accepteert deze twee scopes en beginnen met het aanvragen van de machtigingen van gebruikers indien nodig.  Echter Hallo wijzigen in Hallo interpretatie van Hallo `openid` bereik wordt pas van kracht een paar weken.

> [!IMPORTANT]
> **Uw job: Hallo toevoegen `profile` en `email` scopes als uw app informatie over Hallo gebruiker vereist.**  Houd er rekening mee dat ADAL beide machtigingen in aanvragen standaard bevatten zal. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Hallo verlener afsluitende slash te verwijderen.
Voorheen duurde Hallo verlener waarde die wordt weergegeven in de tokens van Hallo v2.0-eindpunt Hallo formulier

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Hallo-guid is waar Hallo tenantId van hello Azure AD-tenant die Hallo token heeft afgegeven.  Met deze wijzigingen wordt Hallo verlener waarde

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

in beide tokens en Hallo OpenID Connect discovery-document.

> [!IMPORTANT]
> **Uw job: Zorg ervoor dat uw app Hallo verlener waarde zowel met als zonder een afsluitende slash tijdens het valideren van certificaatverlener accepteert.**
> 
> 

## <a name="why-change"></a>Waarom wijzigen?
Hallo primaire reden voor het introduceren van deze wijzigingen is toobe compatibel zijn met de Hallo standaard specificatie OpenID Connect.  We hopen toominimize verschillen tussen integreren met Microsoft identity services en met andere services identiteit in de industrie Hallo door OpenID Connect compatibel.  We willen hun favoriete open-source-verificatiebibliotheken tooenable ontwikkelaars toouse zonder tooalter Hallo bibliotheken tooaccommodate Microsoft verschillen.

## <a name="what-can-you-do"></a>Wat kunt u doen?
Vanaf vandaag, kunt u beginnen met het maken van alle Hallo wijzigingen die hierboven worden beschreven.  U moet onmiddellijk het volgende doen:

1. **Verwijder de afhankelijkheden van Hallo `x5t` headerparameter.**
2. **Hallo overgang van de juiste manier verwerken `profile_info` te`id_token` in antwoorden van een token.**
3. **Verwijder de afhankelijkheden van Hallo `id_token_expires_in` antwoord-parameter.**
4. **Hallo toevoegen `profile` en `email` scopes tooyour app als uw app basisgebruiker informatie nodig heeft.**
5. **Waarden van de verlener in tokens zowel met als zonder een afsluitende slash accepteren.**

Onze [protocoldocumentatie v2.0](active-directory-v2-protocols.md) is al bijgewerkt tooreflect deze wijzigingen, zodat u deze als referentie gebruiken kunt bij het bijwerken van uw code.

Als u meer vragen op Hallo bereik van Hallo wijzigingen hebt, kunt u gratis tooreach out toous op Twitter op @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Hoe vaak wijzigingen protocol plaatsvindt?
We voorziet niet alle verder op te splitsen verificatieprotocollen toohello wordt gewijzigd.  We bundelt deze wijzigingen in een versie die u geen toogo via dit soort updateproces snel opnieuw elk gewenst moment hebt opzettelijk.  Natuurlijk, zullen wij tooadd functies toohello geconvergeerde v2.0 authentication-service die u van profiteren kunt, maar deze wijzigingen moet additief zijn en niet-bestaande code einde.

Willen we graag ten slotte toosay Hartelijk dank voor dingen tijdens de evaluatieperiode Hallo uitprobeert.  Hallo insights en ervaringen van onze vroege gebruikers zijn waardevol zijn tot nu toe, en we hopen dat u hebt tooshare uw mening en ideeën.

Gelukkig coderen!

Hallo Microsoft Identity deling

