---
title: 'Azure Active Directory B2C: Verificatieprotocollen | Microsoft Docs'
description: Hoe toobuild apps rechtstreeks met behulp van protocollen die worden ondersteund door Azure Active Directory B2C Hallo
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C: Verificatieprotocollen
Azure Active Directory B2C (Azure AD B2C) biedt identiteit als een service voor uw apps door de ondersteuning van twee standaardprotocollen: OpenID Connect en OAuth 2.0. Hallo-service is compatibel met standaarden, maar de twee implementaties van deze protocollen subtiele verschillen kunnen hebben. 

Hallo-informatie in deze handleiding is handig als u uw code schrijven door rechtstreeks verzenden en HTTP-aanvragen voor de verwerking, in plaats van via een open-source-bibliotheek. Het is raadzaam dat u deze pagina te lezen voordat u Duik in de details van elk protocol dat specifieke Hallo. Maar als u al bekend met Azure AD B2C bent, gaat u meteen te[protocol verwijzing handleidingen Hallo](#protocols).

<!-- TODO: Need link toolibraries above -->

## Hallo-basisbeginselen
Elke app die gebruikmaakt van Azure AD B2C moet toobe geregistreerd in uw B2C-directory in Hallo [Azure-portal](https://portal.azure.com). Hallo app registratieproces verzameld en enkele waarden tooyour app toegewezen:

* Een **toepassings-id** die de app op unieke wijze identificeert.
* Een **omleidings-URI** of **pakket-id** die kunnen worden gebruikt toodirect antwoorden back tooyour app.
* Enkele andere scenariospecifieke waarden. Informatie voor meer informatie over [hoe tooregister uw toepassing](active-directory-b2c-app-registration.md).

Nadat u uw app registreert, wordt deze door te verzenden aanvragen toohello eindpunt communiceert met Azure Active Directory (Azure AD):

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Vier partijen zijn in bijna alle OAuth en OpenID Connect stromen, die zijn betrokken bij Hallo exchange:

![OAuth 2.0-functies](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Hallo **autorisatie server** hello Azure AD-eindpunt. Veilig worden verwerkt alles gerelateerde toouser informatie en toegang. Hallo-vertrouwensrelaties tussen Hallo partijen in een stroom ook verwerkt. Het is verantwoordelijk voor het verifiëren van de identiteit van de gebruiker hello, verlenen en tooresources toegang intrekken en uitgeven van tokens. Het is ook bekend als Hallo id-provider.

* Hallo **resource-eigenaar** is doorgaans Hallo eindgebruiker. Hallo partij die eigenaar is van de gegevens Hallo is en er Hallo power tooallow derden tooaccess die gegevens of de resource.

* Hallo **OAuth client** wordt uw app. Die wordt geïdentificeerd door de toepassing-ID. Meestal is het Hallo-partij die eindgebruikers interactie met hebben. Het ook aanvraagt tokens van Hallo autorisatie server. Hallo resource-eigenaar moet verlenen Hallo client machtiging tooaccess Hallo resource.

* Hallo **bronserver** is waarin Hallo bron of de gegevens zich bevindt. Hallo autorisatie vertrouwde server toosecurely verifiëren en autoriseren hello OAuth-client. Ook wordt gebruikt bearer-toegang tokens tooensure die toegang hebben tot de resource tooa kan worden verleend.

## Beleidsregels
Azure AD B2C-beleidsregels zijn weliswaar, Hallo belangrijkste functies van Hallo-service. Azure AD B2C wordt Hallo standaard OAuth 2.0 en OpenID Connect-protocollen uitgebreid door de introductie van beleid. Azure AD B2C tooperform kunt veel meer dan een eenvoudige verificatie en autorisatie. 

Beleid beschrijven consumer identiteitservaringen, met inbegrip van registreren, aanmelden, volledig en profiel bewerken. Beleidsregels kunnen worden gedefinieerd in een administratieve gebruikersinterface. Ze kunnen worden uitgevoerd met behulp van een speciale queryparameter in HTTP-aanvragen voor verificatie. 

Beleidsregels kunnen niet standaardfuncties van OAuth 2.0 en OpenID Connect, dus u rekening met Hallo tijd toounderstand houden moet ze. Zie voor meer informatie, Hallo [Naslaggids voor Azure AD B2C beleid](active-directory-b2c-reference-policies.md).

## Tokens
Hello Azure AD B2C-implementatie van OAuth 2.0 en OpenID Connect wordt uitgebreid gebruikgemaakt van bearer-tokens, bearer-tokens die worden weergegeven als JSON webtokens (JWTs). Een bearer-token is een lichtgewicht beveiligingstoken dat verleent 'bearer' toegang tooa Hallo beveiligde resource.

Hallo bearer is een partij die Hallo token kan opleveren. Azure AD een partij moet eerst worden geverifieerd voordat er een bearer-token kan ontvangen. Maar desgewenst Hallo stappen worden niet genomen toosecure Hallo-token in overdracht en opslag kan worden onderschept en gebruikt door een onbedoelde partij.

Sommige beveiligingstokens ingebouwde mechanismen die voorkomen dat onbevoegden gebruiken ze hebben, maar bearer-tokens hebben geen dit mechanisme. Zij moeten worden overgebracht in een beveiligd kanaal, zoals een transport layer security (HTTPS). 

Als bearer-token buiten een beveiligd kanaal wordt verzonden, kunt een schadelijke party u een man-in-the-middle-aanval tooacquire Hallo-token gebruiken en deze toogain niet-geautoriseerde toegang tooa beveiligde resource. Hallo dezelfde beveiligings-principals toepassen wanneer bearer-tokens worden opgeslagen of voor later gebruik opgeslagen. Altijd voor zorgen dat uw app verzendt en bearer-tokens worden opgeslagen op een veilige manier.

Zie voor aanvullende bearer-token beveiligingsoverwegingen [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).

Meer informatie over de verschillende soorten tokens die worden gebruikt in Azure AD B2C Hallo zijn beschikbaar in [hello Azure AD-tokenverwijzing](active-directory-b2c-reference-tokens.md).

## Protocollen
Wanneer u klaar bent tooreview een aantal voorbeelden van aanvragen, kunt u met een van de volgende zelfstudies Hallo beginnen. Elke overeen tooa bepaalde verificatiescenario. Als u hulp bij het bepalen welke stroom geschikt is voor u nodig hebt, kijk dan eens [typen apps die u maken kunt met behulp van Azure AD B2C Hallo](active-directory-b2c-apps.md).

* [Mobiele en systeemeigen toepassingen bouwen met behulp van OAuth 2.0](active-directory-b2c-reference-oauth-code.md)
* [Web-apps bouwen met behulp van OpenID Connect](active-directory-b2c-reference-oidc.md)
* [Apps van één pagina met impliciete Hallo OAuth 2.0-stroom maken](active-directory-b2c-reference-spa.md)

