---
title: aaaAzure AD B2C | Microsoft Docs
description: Hallo typen toepassingen die u kunt ontwikkelen in Azure Active Directory B2C Hallo.
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: Typen toepassingen
Azure Active Directory (Azure AD) B2C ondersteunt verificatie voor diverse moderne app-architecturen. Deze zijn gebaseerd op Hallo standaardprotocollen [OAuth 2.0](active-directory-b2c-reference-protocols.md) of [OpenID Connect](active-directory-b2c-reference-protocols.md). Dit document wordt kort beschreven Hallo typen apps die u kunt maken, onafhankelijk van Hallo taal of platform u liever. Bovendien leert u Hallo geavanceerde scenario's voordat u [toepassingen gaat ontwikkelen](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>Hallo-basisbeginselen
Elke app die gebruikmaakt van Azure AD B2C moet zijn geregistreerd in uw [B2C-directory](active-directory-b2c-get-started.md) via Hallo [Azure Portal](https://portal.azure.com/). Hallo app registratieproces verzameld en enkele waarden tooyour app toegewezen:

* Een **toepassings-id** die de app op unieke wijze identificeert.
* Een **omleidings-URI** die kunnen worden gebruikt toodirect antwoorden back tooyour app.
* Alle andere scenariospecifieke waarden. Voor meer informatie, meer informatie over hoe te[een app registreren](active-directory-b2c-app-registration.md).

Nadat het Hallo-app is geregistreerd, wordt deze door te verzenden aanvragen toohello Azure AD v2.0-eindpunt communiceert met Azure AD:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Elke aanvraag die tooAzure AD B2C wordt verzonden Hiermee geeft u een **beleid**. Een beleid regelt Hallo gedrag van Azure AD. U kunt ook deze eindpunten toocreate een uiterst aanpasbare verzameling gebruikerservaringen gebruiken. Algemene beleidsregels zijn beleidsregels voor registratie, aanmelding en het bewerken van profielen. Als u niet bekend met beleidsregels bent, lees dan over hello Azure AD B2C [uitbreidbaar beleidsframework](active-directory-b2c-reference-policies.md) voordat u doorgaat.

Hallo interactie van elke app met een v2.0-eindpunt volgt eenzelfde globaal patroon:

1. Hallo app leidt Hallo gebruiker toohello v2.0-eindpunt tooexecute een [beleid](active-directory-b2c-reference-policies.md).
2. Hallo gebruiker voltooit Hallo-beleid op basis van de beleidsdefinitie toohello.
3. Hallo app ontvangt een soort beveiligingstoken van Hallo v2.0-eindpunt.
4. Hallo app hello security token tooaccess beveiligd informatie of een beveiligde bron gebruikt.
5. Hallo resource-server valideert hello security token tooverify die toegang kan worden verleend.
6. Hallo-app worden regelmatig vernieuwd Hallo-beveiligingstoken.

<!-- TODO: Need a page for libraries toolink too-->
Deze stappen kunnen verschillen enigszins verschillen op basis van Hallo type app dat u maakt. Open-source bibliotheken kunnen Hallo adresgegevens voor u.

## <a name="web-apps"></a>Web-apps
Voor web-apps (zoals .NET, PHP, Java, Ruby, Python en Node.js) die worden gehost op een server en worden geopend via een browser, ondersteunt Azure AD B2C [OpenID Connect](active-directory-b2c-reference-protocols.md) voor alle gebruikerservaringen. Hiertoe behoren aanmelden, registreren en profielbeheer. In hello Azure AD B2C-implementatie van OpenID Connect initieert uw web-app deze gebruikerservaringen door uitgifte van verificatie aanvragen tooAzure AD. Hallo-resultaat van het Hallo-aanvraag is een `id_token`. Dit beveiligingstoken vertegenwoordigt de identiteit van de gebruiker Hallo. Het bevat ook informatie over de gebruiker Hallo Hallo vorm van claims:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Meer informatie over de typen tokens en claims die beschikbaar tooan in app Hallo Hallo [B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).

In een web-app bestaat de uitvoering van een [beleid](active-directory-b2c-reference-policies.md) uit de volgende globale stappen:

![Afbeelding van web-app-banen](./media/active-directory-b2c-apps/webapp.png)

Validatie van Hallo `id_token` met behulp van een openbare ondertekeningssleutel die is ontvangen van Azure AD is voldoende tooverify Hallo-identiteit van Hallo-gebruiker. Hiermee stelt u een sessiecookie die gebruikt tooidentify Hallo gebruiker op de volgende pagina-aanvragen worden kan.

toosee dit scenario werkt, probeer een van de Hallo web-app aanmelden codevoorbeelden in onze [aan de slag sectie](active-directory-b2c-overview.md#get-started).

In de toevoeging toofacilitating eenvoudig aanmelden moet een webserver-app mogelijk ook tooaccess een back-end-webservice. In dit geval Hallo web-app kunt uitvoeren een iets andere [OpenID Connect-stroom](active-directory-b2c-reference-oidc.md) en tokens verkrijgen met behulp van autorisatiecodes en vernieuwingstokens. Dit scenario wordt beschreven in de volgende Hallo [Web-API's sectie](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Web-API's
U kunt Azure AD B2C toosecure webservices zoals uw app RESTful-web-API gebruiken. Web-API's kan OAuth 2.0 toosecure hun gegevens gebruiken door verificatie van binnenkomende HTTP-aanvragen via tokens. Hallo aanroeper van een web-API voegt een token in autorisatie-header Hallo van een HTTP-aanvraag:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hallo-web-API kan Hallo token tooverify Hallo API aanroeper identiteits- en tooextract informatie over Hallo aanroeper van claims die zijn gecodeerd in Hallo-token vervolgens gebruiken. Meer informatie over de typen tokens en claims die beschikbaar tooan in app Hallo Hallo [Azure AD B2C tokenverwijzing](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Op dit moment ondersteunt Azure AD B2C alleen web-API's die worden gebruikt door hun eigen bekende clients. Zo zou uw volledige app bijvoorbeeld een iOS-app, een Android-app en een back-end web-API kunnen bevatten. Deze architectuur wordt volledig ondersteund. Een partner-client, zoals een andere iOS-app, waardoor Hallo tooaccess hetzelfde web die API wordt momenteel niet ondersteund. Alle onderdelen van de voltooide app Hallo moet een enkele toepassing-id delen.
>
>

Een web-API kan tokens ontvangen van tal van clients, waaronder web-apps, bureaublad- en mobiele apps, apps van één pagina, daemons aan serverzijde en andere web-API's. Hier volgt een voorbeeld van de volledige stroom Hallo voor een web-app die een web-API aanroept:

![Afbeelding van web-API van web-app-banen](./media/active-directory-b2c-apps/webapi.png)

toolearn meer informatie over autorisatiecodes, vernieuwingstokens en Hallo stappen voor het ophalen van tokens, lezen over Hallo [OAuth 2.0-protocol](active-directory-b2c-reference-oauth-code.md).

toolearn hoe toosecure een web-API met behulp van Azure AD B2C, uitchecken Hallo web-API-zelfstudies in onze [aan de slag sectie](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Mobiele en systeemeigen apps
Apps die zijn geïnstalleerd op apparaten, zoals mobiele en bureaublad-apps, moeten vaak tooaccess back-endservices of web-API's namens gebruikers. U kunt aangepaste identity management ervaringen tooyour systeemeigen apps toevoegen en veilig back-endservices aanroepen met behulp van Azure AD B2C en Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-b2c-reference-oauth-code.md).  

In deze stroom Hallo-app wordt uitgevoerd [beleid](active-directory-b2c-reference-policies.md) en ontvangt een `authorization_code` van Azure AD wanneer de gebruiker Hallo Hallo beleid is voltooid. Hallo `authorization_code` vertegenwoordigt Hallo van app machtiging toocall back-end-services namens Hallo-gebruiker die momenteel is aangemeld. Hallo-app kan vervolgens Hallo uitwisselen `authorization_code` op de achtergrond Hallo voor een `id_token` en een `refresh_token`.  Hallo-app kunt Hallo `id_token` tooauthenticate tooa back-end web-API in HTTP-aanvragen. Kan ook gebruikmaken van Hallo `refresh_token` tooget een nieuwe `id_token` wanneer oudere zijn verlopen.

> [!NOTE]
> Azure AD B2C ondersteunt alleen tokens die gebruikt tooaccess zijn momenteel een back-end web van app service. Zo zou uw volledige app bijvoorbeeld een iOS-app, een Android-app en een back-end web-API kunnen bevatten. Deze architectuur wordt volledig ondersteund. Een partner-web-API van uw iOS-app tooaccess toe met behulp van OAuth 2.0-toegangstokens is momenteel niet ondersteund. Alle onderdelen van de voltooide app Hallo moet een enkele toepassing-id delen.
>
>

![Afbeelding van banen voor systeemeigen web-app](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Huidige beperkingen
Azure AD B2C ondersteunt momenteel geen Hallo typen apps te volgen, maar ze zijn op Hallo roadmap. 

### <a name="daemonsserver-side-apps"></a>Daemons/apps aan serverzijde
Apps die langlopende processen bevatten of die werken zonder Hallo aanwezigheid van een gebruiker moeten ook een manier tooaccess bronnen zoals web-API's beveiligde. Deze apps kunnen verifiëren en tokens verkrijgen met behulp van de app Hallo identiteit (in plaats van een gedelegeerde gebruikersidentiteit) en met behulp van OAuth 2.0 Hallo clientreferentiestroom.

Deze stroom wordt momenteel niet ondersteund door Azure AD B2C. Deze apps kunnen pas tokens verkrijgen nadat een interactieve gebruikersstroom is voorgekomen.

### <a name="web-api-chains-on-behalf-of-flow"></a>Web-API-ketens (namens-stroom)
Veel architecturen bevatten een web-API die toocall moet een andere downstream web-API, waarbij beide zijn beveiligd door Azure AD B2C. Dit scenario is gemeenschappelijk in systeemeigen clients met een web-API-back-end. Dit roept vervolgens een Microsoft online services zoals hello Azure AD Graph API.

Dit scenario keten web-API kan worden ondersteund met behulp van Hallo OAuth 2.0 JWT bearer-referentietoekenning, ook wel bekend als Hallo op namens-stroom.  Echter, Hallo op namens-stroom is momenteel niet geïmplementeerd in hello Azure AD B2C.
