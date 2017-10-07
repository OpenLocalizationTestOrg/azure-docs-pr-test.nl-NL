---
title: aaaLearn over verschillende token Hallo en claimtypen die worden ondersteund door Azure AD | Microsoft Docs
description: Een handleiding voor meer informatie over en evalueren Hallo claims in Hallo SAML 2.0 en JSON Web Tokens (JWT)-tokens die zijn uitgegeven door Azure Active Directory (AAD)
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Azure AD-tokenverwijzing
Azure Active Directory (Azure AD) verzendt de beveiligingstokens in Hallo verwerking van elke authenticatiestroom verschillende typen. Dit document beschrijft Hallo-indeling, de beveiligingskenmerken en de inhoud van elk type token.

## <a name="types-of-tokens"></a>Typen tokens
Azure AD ondersteunt Hallo [OAuth 2.0-protocol voor autorisatie](active-directory-protocols-oauth-code.md), welke maakt gebruik van zowel access_tokens als refresh_tokens.  Het biedt ook ondersteuning voor verificatie en meld u via [OpenID Connect](active-directory-protocols-openid-connect-code.md), die een derde type token, Hallo id_token introduceert.  Elk van deze tokens wordt weergegeven als 'bearer-token'.

Een bearer-token is een lichtgewicht beveiligingstoken dat verleent 'bearer' toegang tooa Hallo beveiligde resource. In dit opzicht is Hallo 'bearer' een partij die Hallo token kan opleveren. Hoewel verificatie met Azure AD is vereist op volgorde tooreceive bearer-token, moeten maatregelen worden getroffen toosecure Hallo token, tooprevent onderschept door een onbedoelde partij. Omdat bearer-tokens niet over een ingebouwde mechanisme tooprevent niet-geautoriseerde partijen kunnen gebruiken, moeten zij worden overgebracht in een beveiligd kanaal zoals transport layer security (HTTPS). Als een bearer-token wordt verzonden in Hallo wissen, een man-in Hallo middelste aanval worden gebruikt tooacquire Hallo token en krijgen van toegang door onbevoegden tooa beveiligde resource. Hallo dezelfde beveiligings-principals van toepassing wanneer caching bearer-tokens voor later gebruik of op te slaan. Altijd voor zorgen dat uw app verzendt en bearer-tokens worden opgeslagen op een veilige manier. Zie voor meer beveiligingsoverwegingen op bearer-tokens [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).

Veel van Hallo-tokens die zijn uitgegeven door Azure AD worden geïmplementeerd als JSON Web Tokens of JWTs.  Een JWT is een compacte, URL-veilige methode voor het overbrengen van gegevens tussen twee partijen.  Hallo-gegevens in JWTs worden aangeduid als 'claims' of asserties van informatie over Hallo bearer en het onderwerp van het Hallo-token.  Hallo-claims in JWTs zijn JSON-objecten gecodeerd en geserialiseerd voor verzending.  Aangezien Hallo JWTs uitgegeven door Azure AD zijn ondertekend, maar niet versleuteld, controleert u eenvoudig hello inhoud van een JWT voor foutopsporing.  Er zijn verschillende hulpprogramma's beschikbaar om te doen, zoals [jwt.calebb.net](http://jwt.calebb.net). Voor meer informatie over JWTs, raadpleegt u toohello [JWT-specificatie](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Id_tokens
Id_tokens zijn een vorm van aanmelden beveiligingstoken dat uw app ontvangt bij het uitvoeren van verificatie met behulp van [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Ze worden weergegeven als [JWTs](#types-of-tokens), en bevatten claims die u gebruiken kunt voor het ondertekenen van Hallo gebruiker in uw app.  U kunt gebruiken Hallo claims in een id_token naar eigen inzicht: vaak ze worden gebruikt voor het weergeven van accountgegevens of beslissingen toegang besturingselement in een app.

Id_tokens zijn ondertekend, maar niet op dit moment worden versleuteld.  Wanneer uw app een id_token ontvangt, moet deze [Hallo handtekening valideren](#validating-tokens) tooprove Hallo echtheid van het token en enkele claims in het token tooprove Hallo de geldigheid te valideren.  Hallo claims gevalideerd door een app variëren afhankelijk van de scenariovereisten voor, maar er zijn een aantal [algemene claim validaties](#validating-tokens) die uw app moet worden uitgevoerd in elk scenario.

Zie volgende sectie voor meer informatie op id_tokens claims, evenals een id_token voorbeeld Hallo.  Houd er rekening mee dat de Hallo claims in id_tokens niet in een bepaalde volgorde worden geretourneerd.  Bovendien, nieuwe claims kunnen worden opgenomen in id_tokens op elk punt in tijd: uw app beter niet verbreken wanneer nieuwe claims binnenkomen.  Hallo bevat volgende lijst Hallo claims die uw app kan op betrouwbare wijze op moment van schrijven van dit Hallo interpreteren.  Indien nodig, nog meer details u in Hallo vinden kunt [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Voorbeeld id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Probeer het Hallo-claims in Hallo voorbeeld id_token bekijken door te plakken in verdient het aanbeveling [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Claims in id_tokens
> [!div class="mx-codeBreakAll"]
| JWT Claim | Naam | Beschrijving |
| --- | --- | --- |
| `appid` |Toepassings-id |Hallo-toepassing die van Hallo token tooaccess een bron gebruikmaakt te identificeren. Hallo-toepassing kan fungeren als zelf of namens een gebruiker. Hallo toepassings-ID vertegenwoordigt doorgaans een application-object, maar het kan ook een service-principal-object vertegenwoordigen in Azure AD. <br><br> **Voorbeeldwaarde JWT**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Doelgroep |Hallo bedoeld ontvanger van Hallo-token. Hallo-toepassing die de token Hallo ontvangt moet verifiëren dat Hallo doelgroep waarde juist is en tot tokens die zijn bedoeld voor een andere doelgroep negeren. <br><br> **Voorbeeldwaarde SAML**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Voorbeeldwaarde JWT**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Application Authentication Context Class Reference |Hiermee wordt aangegeven hoe Hallo-client is geverifieerd. Hallo-waarde is voor een openbare client 0. Als de client-ID en clientgeheim zijn gebruikt, is Hallo waarde 1. <br><br> **Voorbeeldwaarde JWT**: <br> `"appidacr": "0"` |
| `acr` |Authentication Context Class Reference |Hiermee wordt aangegeven hoe Hallo onderwerp is geverifieerd als tegengestelde toohello client in Hallo Application Authentication Context Class Reference claim. De waarde '0' geeft aan Hallo eindgebruiker verificatie niet voldeed aan Hallo vereisten van de ISO/IEC 29115. <br><br> **Voorbeeldwaarde JWT**: <br> `"acr": "0"` |
| Verificatie Instant |Registreert Hallo datum en tijd waarop de verificatie heeft plaatsgevonden. <br><br> **Voorbeeldwaarde SAML**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Verificatiemethode |Geeft aan hoe Hallo onderwerp van Hallo-token is geverifieerd. <br><br> **Voorbeeldwaarde SAML**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Voorbeeldwaarde JWT**:`“amr”: ["pwd"]` |
| `given_name` |Voornaam |Biedt Hallo eerst of 'gegeven"naam van de gebruiker hello, zoals ingesteld op het gebruikersobject hello Azure AD. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"given_name": "Frank"` |
| `groups` |Groepen |Biedt de object-id's die de groepslidmaatschappen van de certificaathouder Hallo vertegenwoordigen. Deze waarden zijn uniek (Zie de Object-ID) en veilig kunnen worden gebruikt voor het beheren van toegang tot, zoals het afdwingen van de autorisatie tooaccess een resource. Hallo-groepen die zijn opgenomen in Hallo groepen claim zijn geconfigureerd op basis van per toepassing, via Hallo 'groupMembershipClaims'-eigenschap van het Hallo-toepassingsmanifest. Een waarde van null alle groepen uitsluit, een waarde van 'Beveiligingsgroep' bevat alleen uitgevoerd voor Active Directory-beveiligingsgroep lidmaatschappen en een waarde 'Alle' wordt beveiligingsgroepen en distributielijsten van Office 365. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Id-provider |Registreert Hallo identiteitsprovider die geverifieerd Hallo onderwerp van Hallo-token. Deze waarde is identiek toohello waarde Hallo verlener claim tenzij Hallo gebruikersaccount bevindt zich in een andere tenant dan Hallo verlener. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Slaat Hallo tijd op welke Hallo token is uitgegeven. Het is vaak gebruikte toomeasure token versheid. <br><br> **Voorbeeldwaarde SAML**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Voorbeeldwaarde JWT**: <br> `"iat": 1390234181` |
| `iss` |certificaatverlener |Identificeert Hallo beveiligingstokenservice (STS) die constructs en het Hallo-token retourneert. In Hallo tokens die Azure AD retourneert, is het Hallo verlener sts.windows.net. Hallo is GUID in Hallo verlener claimwaarde Hallo tenant-ID van hello Azure AD-directory. Hallo tenant-ID is een niet-wijzigbaar en betrouwbare id van Hallo directory. <br><br> **Voorbeeldwaarde SAML**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Voorbeeldwaarde JWT**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Achternaam |Hallo-achternaam, achternaam of familienaam van Hallo gebruiker biedt zoals gedefinieerd in hello Azure AD-gebruikersobject. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"family_name": "Miller"` |
| `unique_name` |Naam |Biedt een menselijke leesbare waarde die Hallo onderwerp van Hallo-token aangeeft. Deze waarde kan niet worden gegarandeerd toobe uniek zijn binnen een tenant en is ontworpen toobe alleen ter informatie weergegeven. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |object-ID |Bevat een unieke id van een object in Azure AD. Deze waarde is onveranderbaar en kan niet worden toegewezen of opnieuw gebruikt. Hallo-object-ID tooidentify een object in query's tooAzure AD gebruiken. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Rollen |Geeft alle rollen van de toepassing die houder Hallo heeft gekregen zowel direct als indirect via een groepslidmaatschap en gebruikte tooenforce op basis van rollen kunnen worden toegangsbeheer. Toepassingsrollen zijn gedefinieerd op basis van per toepassing, via Hallo `appRoles` eigenschap van het Hallo-toepassingsmanifest. Hallo `value` eigenschap van de toepassingsrol van elke hello-waarde die wordt weergegeven in Hallo rollen claim is. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Bereik |Hiermee wordt aangegeven Hallo imitatie machtigingen verleend toohello client-toepassing. Hallo standaardmachtiging `user_impersonation`. Hallo-eigenaar van beveiligde resource Hallo kunt u aanvullende waarden registreren in Azure AD. <br><br> **Voorbeeldwaarde JWT**: <br> `"scp": "user_impersonation"` |
| `sub` |Onderwerp |Hallo-principal over welke Hallo token informatie, zoals een gebruiker van een toepassing hello asserts identificeert. Deze waarde is onveranderbaar en kan niet opnieuw worden toegewezen of opnieuw worden gebruikt, zodat deze kan worden gebruikt tooperform autorisatie controles veilig. Omdat Hallo onderwerp altijd aanwezig is in Hallo tokens hello Azure AD-problemen, raden we u deze waarde in een algemeen autorisatie-systeem. <br> `SubjectConfirmation`is niet een claim. Hierin wordt beschreven hoe Hallo onderwerp van Hallo-token is gecontroleerd. `Bearer`Hiermee wordt aangegeven dat onderwerp hello wordt bevestigd door hun bezit van Hallo-token. <br><br> **Voorbeeldwaarde SAML**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Voorbeeldwaarde JWT**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |Tenant-id |Een niet-wijzigbaar, herbruikbare id die Hallo directory-tenant die token Hallo uitgegeven identificeert. U kunt deze waarde tooaccess tenantspecifieke directoryresources gebruiken in een multitenant-toepassing. Bijvoorbeeld, kunt u deze waarde tooidentify hello tenant in een aanroep toohello Graph API. <br><br> **Voorbeeldwaarde SAML**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Voorbeeldwaarde JWT**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Levensduur van token |Hiermee definieert u Hallo tijdsinterval waarbinnen een token geldig is. Hallo-service die Hallo token valideert dient te verifiëren dat Hallo huidige datum valt binnen Hallo levensduur van token, anders die het Hallo-token moet afwijzen. Hallo service mogelijk voor up toofive minuten buiten Hallo levensduur van token bereik tooaccount voor eventuele verschillen in kloktijd ('tijd tijdverschil') tussen Azure AD en Hallo-service. <br><br> **Voorbeeldwaarde SAML**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Voorbeeldwaarde JWT**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Principalnaam van gebruiker |Winkels Hallo gebruikersnaam van Hallo gebruiker principal.<br><br> **Voorbeeldwaarde JWT**: <br> `"upn": frankm@contoso.com` |
| `ver` |Versie |Slaat Hallo-versienummer van het Hallo-token. <br><br> **Voorbeeldwaarde JWT**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Toegangstokens
Heeft geverifieerd wordt Azure AD een toegangstoken die gebruikt tooaccess beveiligde bronnen worden kan. Hallo toegangstoken is een base 64 gecodeerde JSON Web Token (JWT) en de inhoud ervan kunnen worden gecontroleerd via een decoder worden uitgevoerd.

Als uw app alleen *gebruikt* toegang tokens tooget toegang tooAPIs, u kunt (en moeten) behandelen toegangstokens als volledig ondoorzichtig - ze zijn alleen tekenreeksen die uw app tooresources in HTTP-aanvragen doorgeven kunt.

Wanneer u een toegangstoken aanvraagt, wordt ook bepaalde metagegevens over Hallo toegangstoken voor het gebruiken van uw app in Azure AD geretourneerd.  Deze informatie omvat het verlooptijdstip Hallo van Hallo-toegangstoken en Hallo scopes waarvoor geldig is.  Hiermee kunt uw app tooperform intelligent caching van toegangstokens zonder tooparse Hallo toegangstoken zelf te openen.

Als uw app een API die is beveiligd met Azure AD dat toegangstokens in HTTP-aanvragen is verwacht, moet u uitvoeren validatie en de controle van Hallo-tokens die u ontvangt. Validatie van het toegangstoken Hallo voordat u deze tooaccess resources moet worden uitgevoerd in uw app. Zie voor meer informatie over validatie [valideren van Tokens](#validating-tokens).  
Voor meer informatie over hoe toodo met .NET, Zie [beveiligen van een Web-API met behulp van Azure AD-Bearer-tokens](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Vernieuwen van tokens

Vernieuwen van tokens zijn beveiligingstokens die uw app kunt gebruiken tooacquire nieuw access tokens in een OAuth 2.0-stroom.  Kunt u uw app tooachieve op lange termijn toegang tooresources namens een gebruiker zonder tussenkomst door Hallo-gebruiker.

Vernieuwen van tokens zijn meerdere resource.  Dat is toosay die een vernieuwingstoken ontvangen tijdens een tokenaanvraag voor één resource kan worden ingewisseld voor toegang tot andere resource tooa tokens. toodo deze, Hallo set `resource` parameter in Hallo aanvraag toohello gericht resource.

Vernieuwen van tokens volledig ondoorzichtig zijn tooyour app. Ze zijn lange levensduur hebben, maar uw app niet worden geschreven tooexpect die een vernieuwingstoken voor een periode duurt.  Vernieuwen van tokens kunnen op elk moment in de tijd om een groot aantal redenen zijn ongeldig.  Hallo enige manier om uw app tooknow als een vernieuwingstoken geldig tooattempt tooredeem is het door het maken van een tokenaanvraag tooAzure AD token-eindpunt.

Wanneer u een vernieuwingstoken voor een nieuw toegangstoken inwisselen, ontvangt u een nieuwe vernieuwingstoken Hallo token reactie.  Op te slaan Hallo zojuist uitgegeven vernieuwingstoken vervangen Hallo u die wordt gebruikt bij het Hallo-aanvraag.  Dit wordt gegarandeerd dat het vernieuwen van tokens geldig voor zo lang mogelijk blijven.

## <a name="validating-tokens"></a>Valideren van tokens

In de volgorde toovalidate een id_token of een access_token, moet uw app beide Hallo-token handtekening en Hallo claims valideren. In de volgorde toovalidate toegangstokens, moet uw app ook valideren Hallo verlener, Hallo doelgroep en Hallo ondertekenen van tokens. Deze moeten toobe gevalideerd met het Hallo-waarden in Hallo OpenID discovery-document. Bijvoorbeeld, Hallo tenant onafhankelijke versie van Hallo-document bevindt zich op [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Azure AD-middleware beschikt over ingebouwde mogelijkheden voor het valideren van de toegangstokens en vindt u op onze [voorbeelden](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind in Hallo taal van uw keuze. Zie voor meer informatie over hoe tooexplicitly valideren voor een JWT-token, Hallo [handmatige JWT Validatievoorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Wij bibliotheken en codevoorbeelden die laten zien hoe de validatie van tokens - voor het verwerken van tooeasily Hallo onderstaande informatie gewoon beschikbaar voor degenen die wilt toounderstand Hallo onderliggende proces.  Er zijn ook enkele van derden open-source bibliotheken beschikbaar voor de validatie van JWT - er is ten minste één optie voor bijna elk platform en er taal. Zie voor meer informatie over Azure AD-verificatiebibliotheken en codevoorbeelden [Azure AD-verificatiebibliotheken](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Hallo handtekening valideren

Een JWT bevat drie segmenten die worden gescheiden door Hallo `.` teken.  het eerste segment Hallo Hallo wordt ook wel **header**, Hallo seconde als Hallo **hoofdtekst**, en Hallo derde als Hallo **handtekening**.  Hallo handtekening segment mag gebruikte toovalidate Hallo authenticiteit van Hallo token zodat deze kan worden vertrouwd door uw app.

Tokens die zijn uitgegeven door Azure AD bent aangemeld met behulp van de branche standaard versleuteling voor asymmetrische algoritmen, zoals RSA 256. Hallo-kop Hallo JWT bevat informatie over het Hallo-sleutel en versleutelingsmethode toosign Hallo-token hebt gebruikt:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Hallo `alg` claim geeft Hallo-algoritme dat gebruikt toosign Hallo token tijdens het Hallo is `x5t` claim geeft Hallo bepaalde openbare sleutel die gebruikt toosign Hallo-token is.

Op elk gewenst moment in de tijd, Azure AD Meld u aan een id_token met een van een bepaalde set paren van openbare en persoonlijke sleutels. Azure AD draait Hallo mogelijke set sleutels op periodieke basis, zodat uw app toohandle deze sleutel wordt automatisch gewijzigd worden geschreven.  Een redelijke frequentie toocheck voor updates toohello openbare sleutels die worden gebruikt door Azure AD wordt elke 24 uur.

U kunt verkrijgen Hallo sleutelgegevens nodig toovalidate Hallo handtekening ondertekenen met behulp van Hallo OpenID Connect metagegevensdocument zich bevindt op:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Probeer deze URL in een browser.
> 
> 

Dit metagegevensdocument is een nuttig stukjes informatie, zoals locatie Hallo Hallo verschillende eindpunten vereist voor het uitvoeren van OpenID Connect verificatie met JSON-object.  

Dit omvat ook een `jwks_uri`, toosign tokens waardoor Hallo-locatie van de set Hallo van openbare sleutels worden gebruikt.  Hallo JSON-document vinden op het Hallo `jwks_uri` bevat alle Hallo openbare sleutelinformatie in gebruik op dat moment bepaald.  Uw app kunt Hallo `kid` claim in Hallo JWT-header tooselect welke openbare sleutel in dit document gebruikte toosign is-token van een bepaald.  Validatie van handtekening met behulp van de juiste openbare sleutel Hallo en Hallo aangegeven algoritme kan vervolgens uitvoeren.

Het valideren van de handtekening is buiten Hallo bereik van dit document - er zijn veel open-source bibliotheken beschikbaar voor u doen indien nodig te helpen.

#### <a name="validating-hello-claims"></a>Hallo claims valideren

Wanneer uw app een token (een id_token bij het aanmelden van gebruiker of een toegangstoken als een bearer-token in Hallo HTTP-aanvraag ontvangt) moet ook uitvoeren enkele controles tegen Hallo claims in Hallo-token.  Deze omvatten, maar zijn niet beperkt tot:

* Hallo **doelgroep** claim - tooverify die Hallo token is beoogde toobe tooyour app gegeven.
* Hallo **niet voor** en **verlooptijd** claims - tooverify die Hallo token niet is verlopen.
* Hallo **verlener** claim - tooverify die Hallo token inderdaad tooyour app is uitgegeven door Azure AD.
* Hallo **Nonce** -toomitigate een token replay-aanval.
* en nog veel meer...

Raadpleeg voor een volledige lijst van uw app moet worden uitgevoerd voor de ID-Tokens claim-validaties toohello [specificatie van het OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Details van Hallo verwachte waarden voor deze claims worden opgenomen in de voorgaande Hallo [id_token sectie](#id-tokens) sectie.

## <a name="sample-tokens"></a>Voorbeeld-Tokens

Deze sectie vindt voorbeelden van SAML- en JWT-tokens die Azure AD als resultaat geeft. Deze voorbeelden kunnen u zien Hallo claims in de context.

### <a name="saml-token"></a>SAML-Token

Dit is een voorbeeld van een typische SAML-token.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>JWT-Token - Gebruikersimitaties
Dit is een voorbeeld van een typische JSON web token (JWT) gebruikt in een grant-autorisatiecodestroom.
In toevoeging tooclaims, Hallo token bevat een versienummer in **ver** en **appidacr**, Hallo authentication context class-verwijzing, waarmee wordt aangegeven hoe Hallo-client is geverifieerd. Hallo-waarde is voor een openbare client 0. Als een client-ID of een clientgeheim gebruikt, is Hallo waarde 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Gerelateerde inhoud
* Zie hello Azure AD Graph [beleid operations](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) en Hallo [beleid entiteit](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn meer over het beheren van de levensduur van token beleid via hello Azure AD Graph API.
* Zie voor meer informatie over en voorbeelden voor het beheren van beleid via PowerShell-cmdlets, inclusief voorbeelden, [configureerbare token levensduur in Azure AD](../active-directory-configurable-token-lifetimes.md). 
