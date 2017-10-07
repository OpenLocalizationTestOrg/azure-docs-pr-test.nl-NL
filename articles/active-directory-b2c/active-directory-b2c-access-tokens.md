---
title: 'Azure Active Directory B2C: Toegangstokens voor aanvragen | Microsoft Docs'
description: In dit artikel wordt uitgelegd hoe u een clienttoepassing toosetup en verkrijgen van een toegangstoken.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: Toegangstokens voor aanvragen

Een toegangstoken (aangeduid als **toegang\_token** in Hallo-antwoorden van Azure AD B2C) is een vorm van een beveiligingstoken dat een client kan tooaccess bronnen gebruiken die zijn beveiligd met een [autorisatie server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), zoals een web-API. Toegangstokens worden weergegeven als [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) en informatie over de beoogde bronserver Hallo en Hallo verleende machtigingen toohello server bevatten. Bij het aanroepen van de bronserver Hallo moet Hallo toegangstoken aanwezig zijn in Hallo HTTP-aanvraag.

Dit artikel wordt beschreven hoe bestellen tooobtain tooconfigure een clienttoepassing en web-API in een **toegang\_token**.

> [!NOTE]
> **Web-API-ketens (op-andere gebruikers-Of) wordt niet ondersteund door Azure AD B2C.**
>
> Veel architecturen bevatten een web-API die toocall moet een andere downstream web-API, beide beveiligd door Azure AD B2C. Dit scenario is gemeenschappelijk in systeemeigen clients waarvoor een web-API back-end die op zijn beurt een Microsoft online services zoals hello Azure AD Graph API aanroept.
>
> Dit scenario keten web-API kan worden ondersteund met behulp van OAuth 2.0 JWT Bearer Credential toekennen, anders Hallo Hallo op namens-stroom genoemd. Echter, Hallo op namens-stroom is momenteel niet geïmplementeerd in Azure AD B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Registreren van een web-API en machtigingen publiceren

Voordat u een toegangstoken, u eerst moet tooregister een web-API en machtigingen (scopes genoemd) die kunnen worden verleend als de clienttoepassing toohello publiceren.

### <a name="register-a-web-api"></a>Een web-API registreren

1. Klik op de blade Hallo B2C-functies op Hallo Azure-portal, **toepassingen**.
1. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
1. Voer een **naam** voor Hallo-toepassing die uw toepassing tooconsumers wordt beschreven. U kunt bijvoorbeeld 'Contoso-API invoeren.
1. Wisselknop Hallo **omvatten web-app / web-API** te schakelen**Ja**.
1. Geef een willekeurige waarde voor Hallo **antwoord-URL's**. Geef bijvoorbeeld `https://localhost:44316/` op. Hallo-waarde niet van belang omdat een API niet daarom Hallo token rechtstreeks vanuit Azure AD B2C.
1. Voer een waarde in voor **URI voor de app-id**. Dit is Hallo-id die wordt gebruikt voor uw web-API. Bijvoorbeeld 'notities' in hello vak invoeren. Hallo **App ID URI** worden dan `https://{tenantName}.onmicrosoft.com/notes`.
1. Klik op **maken** tooregister uw toepassing.
1. Klik op Hallo-toepassing die u zojuist hebt gemaakt en noteert u Hallo globaal unieke **toepassing de Client-ID** u later in uw code.

### <a name="publishing-permissions"></a>Publishing machtigingen

Scopes die vergelijkbaar toopermissions, zijn nodig als uw app een API aanroept. Enkele voorbeelden van bereiken zijn 'lezen' of 'schrijven'. Stel dat u wilt dat uw web- of systeemeigen te 'lezen' van een API-app. Uw app in Azure AD B2C roepen en een token die aanvraag geeft toohello toegangsbereik 'lezen'. Hallo-app moet in volgorde voor Azure AD B2C tooemit een toegangstoken toobe machtiging te 'lezen' van de specifieke API Hallo verleend. toodo dit door uw API moet eerst toopublish Hallo 'lezen' bereik.

1. Binnen hello Azure AD B2C **toepassingen** blade open Hallo web API-toepassing ('Contoso-API).
1. Klik op **Gepubliceerd bereiken**. Dit is waar u Hallo machtigingen (scopes genoemd) die kunnen worden verleend tooother toepassingen definiëren.
1. Voeg **waarden voor het bereik** zo nodig (bijvoorbeeld ' lezen'). Standaard worden Hallo 'user_impersonation' bereik gedefinieerd. U kunt deze negeren als u wenst. Voer een beschrijving van Hallo scope in Hallo **scopenaam** kolom.
1. Klik op **Opslaan**.

> [!IMPORTANT]
> Hallo **scopenaam** is Hallo beschrijving van Hallo **bereikwaarde**. Wanneer u Hallo bereik, dient u ervoor dat toouse hello **bereikwaarde**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Een systeemeigen verlenen of web-app-machtigingen tooa web-API

Zodra een API geconfigureerd toopublish bereiken is, moet de clienttoepassing Hallo toobe verleend deze bereiken via hello Azure-portal.

1. Navigeer toohello **toepassingen** menu in Hallo B2C-functiesblade.
1. Registreren van een clienttoepassing ([web-app](active-directory-b2c-app-registration.md#register-a-web-app) of [native client](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) als u nog niet hebt. Als u deze handleiding als startpunt volgt, moet u een clienttoepassing tooregister.
1. Klik op **API-toegang**.
1. Klik op **Toevoegen**.
1. Selecteer uw web-API en Hallo scopes (machtigingen) u wilt dat toogrant.
1. Klik op **OK**.

> [!NOTE]
> Azure AD B2C wordt niet gevraagd uw client toepassingsgebruikers om hun toestemming. In plaats daarvan wordt alle toestemming verstrekt door Hallo beheerder, op basis van Hallo machtigingen geconfigureerd tussen Hallo-toepassingen die hierboven worden beschreven. Als een machtiging verlenen voor een toepassing is ingetrokken, alle gebruikers die eerder wel tooacquire zijn deze machtiging wordt niet meer kunnen toodo dus worden.

## <a name="requesting-a-token"></a>Aanvragen van een token

Bij het aanvragen van een toegangstoken Hallo clienttoepassing toospecify Hallo gewenste machtigingen in Hallo moet **bereik** parameter van het Hallo-aanvraag. Bijvoorbeeld toospecify hello **bereikwaarde** 'lezen' voor Hallo API met Hallo **App ID URI** van `https://contoso.onmicrosoft.com/notes`, Hallo bereik zou worden `https://contoso.onmicrosoft.com/notes/read`. Hieronder volgt een voorbeeld van een vergunning code aanvraag toohello `/authorize` eindpunt.

> [!NOTE]
> Aangepaste domeinen worden momenteel niet ondersteund samen met toegangstokens. U moet uw domein tenantName.onmicrosoft.com in Hallo aanvraag-URL.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire meerdere machtigingen in Hallo dezelfde aanvragen, kunt u meerdere vermeldingen toevoegen in één Hallo **bereik** parameter, gescheiden door spaties. Bijvoorbeeld:

URL gedecodeerd:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

URL-gecodeerd:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

U kunt meer scopes (machtigingen) aanvragen voor een resource dan wat voor de clienttoepassing wordt verleend. Wanneer dit Hallo geval, slaagt Hallo aanroep, als ten minste één machtiging is verleend. Hallo resulterende **toegang\_token** heeft de claim 'scp' is gevuld met alleen Hallo machtigingen is.

> [!NOTE] 
> Wij ondersteunen geen aanvragende machtigingen op basis van twee verschillende webbronnen in Hallo dezelfde aanvraag. Dit soort aanvraag zal mislukken.

### <a name="special-cases"></a>Bijzondere gevallen

Hallo OpenID Connect standaard verschillende speciale 'bereik'-waarden zijn opgegeven. Hallo speciale scopes vertegenwoordigen Hallo machtiging te volgen 'hello gebruikersprofiel toegang':

* **openid**: dit vraagt een token ID
* **offline\_toegang**: dit vraagt een vernieuwingstoken (met behulp van [autorisatiecode loopt](active-directory-b2c-reference-oauth-code.md)).

Als hello `response_type` parameter in een `/authorize` aanvraag bevat `token`, Hallo `scope` parameter moet ten minste één bron bereik bevatten (anders dan `openid` en `offline_access`) die wordt verleend. Anders Hallo `/authorize` -aanvraag wordt beëindigd met een fout.

## <a name="hello-returned-token"></a>Hallo heeft een token geretourneerd

In een succes geslagen **toegang\_token** (van beide Hallo `/authorize` of `/token` eindpunt), Hallo volgende claims aanwezig zijn:

| Naam | Claim | Beschrijving |
| --- | --- | --- |
|Doelgroep |`aud` |Hallo **toepassings-ID** van één resource Hallo dat token Hallo verleent toegang tot. |
|Bereik |`scp` |Hallo machtigingen verleend toohello resource. Meerdere verleende machtigingen worden gescheiden door een spatie. |
|Geautoriseerde partij |`azp` |Hallo **toepassings-ID** van Hallo-clienttoepassing die Hallo aanvraag gestart. |

Wanneer uw API Hallo ontvangt **toegang\_token**, moet deze [valideren Hallo token](active-directory-b2c-reference-tokens.md) tooprove die Hallo token authentiek is en juist claims Hallo heeft.

We zijn altijd open toofeedback en suggesties! Als u problemen met dit onderwerp ondervindt, boek bij Stack Overflow met behulp van de tag Hallo ['azure ad b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Volgende stappen

* Maakt een API met [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Maakt een API met [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
