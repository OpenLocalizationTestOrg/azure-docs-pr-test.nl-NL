---
title: aaaAzure AD service tooservice auth met OAuth2.0 conceptspecificatie op-andere gebruikers-Of-| Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse HTTP berichten tooimplement service tooservice verificatie met behulp van Hallo OAuth2.0 op namens-stroom.
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Service tooservice aanroept met behulp van gedelegeerde gebruikersidentiteit in Hallo op namens-stroom
Hallo OAuth 2.0 On-Behalf-Of stroom fungeert Hallo gebruiksvoorbeeld waar een service of web-API wordt aangeroepen in een toepassing die op zijn beurt toocall moet een andere service of web-API. Hallo idee is toopropagate Hallo gedelegeerde gebruikersidentiteit en machtigingen via Hallo aanvraagketen. Voor Hallo middelste laag service toomake geverifieerde aanvragen toohello downstream-service moet deze toosecure een toegangstoken van Azure Active Directory (Azure AD), namens de gebruiker Hallo.

## Op-andere gebruikers-Of stroomdiagram
Wordt ervan uitgegaan dat Hallo-gebruiker is geverifieerd op een toepassing met Hallo [autorisatiecodetoekenning OAuth 2.0](active-directory-protocols-oauth-code.md). Hallo-toepassing is op dit moment een toegangstoken (token A) met de claims en toestemming tooaccess Hallo middelste laag web API (A-API) van de gebruiker Hallo. Nu moet API A toomake een geverifieerde aanvraag toohello downstream web-API (API-B).

Hallo stappen volgen Hallo op namens-stroom vormen en aan de hand Hallo van Hallo volgende diagram worden uitgelegd.

![OAuth2.0 op namens-stroom](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. Hallo-clienttoepassing maakt een aanvraag tooAPI A met Hallo token A.
2. API-A verifieert toohello Azure AD uitgifte van tokens eindpunt en vraagt een token tooaccess API B.
3. Hello Azure AD uitgifte van tokens eindpunt API A van referenties met een token valideert en problemen hello toegangstoken voor de API-B (token B).
4. Hallo token B is ingesteld in Hallo autorisatie-header van Hallo aanvraag tooAPI B.
5. Gegevens uit beveiligde resource hello wordt geretourneerd door de API B.

## Hallo-toepassing en service in Azure AD registreren
Registreer zowel client-toepassing hello en Hallo middelste laag service in Azure AD.
### Hallo middelste laag service registreren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.
3. Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.
4. Klik op **App registraties** en kies **registratie van de nieuwe toepassing**.
5. Voer een beschrijvende naam voor de toepassing hello en Hallo-toepassingstype selecteren. Op basis van het toepassingstype Hallo set Hallo aanmeldings-URL of Omleidings-URL toohello basis-URL. Klik op **maken** toocreate Hallo-toepassing.
6. Tijdens het nog hello Azure-portal, kiest u uw toepassing en klik op **instellingen**. Kies in het menu instellingen Hallo **sleutels** en toevoegen van een sleutel - selecteert u een sleutel duur van 1 jaar of 2 jaar. Wanneer u deze pagina opslaat, Hallo-sleutelwaarde wordt weergegeven, kopiëren en Hallo waarde opslaan op een veilige locatie - u deze later tooconfigure Hallo toepassing registersleutelinstellingen in uw implementatie moet - waarde van deze sleutel worden niet opnieuw weergegeven en ook niet worden opgehaald door een andere manier record dus u moet deze zodra deze zichtbaar zijn vanaf hello Azure-Portal is.

### Hallo client-toepassing registreren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.
3. Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.
4. Klik op **App registraties** en kies **registratie van de nieuwe toepassing**.
5. Voer een beschrijvende naam voor de toepassing hello en Hallo-toepassingstype selecteren. Op basis van het toepassingstype Hallo set Hallo aanmeldings-URL of Omleidings-URL toohello basis-URL. Klik op **maken** toocreate Hallo-toepassing.
6. Machtigingen configureren voor uw toepassing - in menu Hallo-instellingen, kiest u Hallo **vereist machtigingen** sectie, klikt u op **toevoegen**, klikt u vervolgens **selecteert u een API**, en type Hallo naam van Hallo middelste laag service in Hallo tekstvak. Klik vervolgens op **Selecteer machtigingen** en selecteer ' toegang *servicenaam*'.

### Bekende clienttoepassingen configureren
In dit scenario heeft Hallo middelste laag service geen gebruiker interactie tooobtain Hallo van gebruiker toestemming geven tooaccess Hallo downstream-API. Daarom Hallo optie toogrant toegang toohello downstream API moet worden weergegeven als onderdeel van het Hallo toestemming stap tijdens de verificatie vooraf.
tooachieve deze, volg de stappen hieronder tooexplicitly bind Hallo client van app-registratie in Azure AD met Hallo registratie van Hallo middelste laag service, die worden samengevoegd Hallo toestemming vereist zijn voor zowel de Hallo client als de middelste laag in een dialoogvenster met één Hallo.
1. Registratie van de middelste laag service toohello navigeren en klik op **Manifest** tooopen Hallo manifest editor.
2. Zoek in het manifest van de Hallo Hallo `knownClientApplications` eigenschap matrix en Client-ID van de clienttoepassing Hallo Hallo toevoegen als een element.
3. Hallo manifest door te klikken op Hallo knop opslaan opslaan.

## Tooservice access token serviceaanvraag
toorequest een toegangstoken maken voor een HTTP POST toohello tenantspecifieke Azure AD-eindpunt Hallo parameters te volgen.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Er zijn twee gevallen, afhankelijk van of de client-toepassing hello toobe beveiligd door een gedeeld geheim of een certificaat kiest.

### Het eerste aanvraagnummer: aanvraag voor toegang tot token met een gedeeld geheim
Wanneer u een gedeeld geheim, bevat een tokenaanvraag voor service-naar-service toegang Hallo volgende parameters:

| Parameter |  | Beschrijving |
| --- | --- | --- |
| grant_type |Vereist | Hallo type token Hallo-aanvraag. Voor een aanvraag met behulp van een JWT, moet Hallo waarde **urn: ietf:params:oauth:grant-type: jwt-bearer**. |
| Verklaring |Vereist | Hallo-waarde van Hallo token dat wordt gebruikt in Hallo-aanvraag. |
| client_id |Vereist | Hallo-App-ID toegewezen toohello aanroepen service tijdens de registratie met Azure AD. toofind hello, App-ID in hello Azure-beheerportal, klikt u op **Active Directory**, klikt u op Hallo directory en klik op de naam van de toepassing hello. |
| client_secret |Vereist | Hallo-sleutel wordt geregistreerd voor Hallo service aanroepen in Azure AD. Deze waarde is moet opgemerkt op Hallo moment van inschrijving. |
| Resource |Vereist | Hallo App ID URI Hallo service (beveiligde resource) ontvangen. toofind hello App ID URI, in hello Azure-beheerportal, klikt u op **Active Directory**, klikt u op Hallo directory, klik op de naam van de toepassing hello, **alle instellingen** en klik vervolgens op **eigenschappen** . |
| requested_token_use |Vereist | Hiermee geeft u op hoe Hallo-aanvraag moet worden verwerkt. In Hallo op namens-stroom, Hallo-waarde moet **on_behalf_of**. |
| Bereik |Vereist | Een spatie gescheiden lijst met bereiken voor de tokenaanvraag Hallo. Voor het OpenID Connect, Hallo bereik **openid** moet worden opgegeven.|

#### Voorbeeld
Hallo volgende HTTP POST-aanvragen een toegangstoken voor Hallo https://graph.windows.net web-API. Hallo `client_id` Hallo service identificeert die Hallo toegangstoken aanvragen.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Tweede geval: aanvraag voor toegang tot token met een certificaat
Een service-naar-service toegang tokenaanvraag met een certificaat bevat Hallo volgende parameters:

| Parameter |  | Beschrijving |
| --- | --- | --- |
| grant_type |Vereist | Hallo type token Hallo-aanvraag. Voor een aanvraag met behulp van een JWT, moet Hallo waarde **urn: ietf:params:oauth:grant-type: jwt-bearer**. |
| Verklaring |Vereist | Hallo-waarde van Hallo token dat wordt gebruikt in Hallo-aanvraag. |
| client_id |Vereist | Hallo-App-ID toegewezen toohello aanroepen service tijdens de registratie met Azure AD. toofind hello, App-ID in hello Azure-beheerportal, klikt u op **Active Directory**, klikt u op Hallo directory en klik op de naam van de toepassing hello. |
| client_assertion_type |Vereist |Hallo-waarde moet liggen`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Vereist | Een (een JSON Web Token) bewering die u toocreate nodig hebt en ondertekenen met het Hallo-certificaat geregistreerd als de referenties voor uw toepassing.  Meer informatie over [referenties van het certificaat](active-directory-certificate-credentials.md) toolearn hoe tooregister uw certificaat en het Hallo-indeling van Hallo verklaring.|
| Resource |Vereist | Hallo App ID URI Hallo service (beveiligde resource) ontvangen. toofind hello App ID URI, in hello Azure-beheerportal, klikt u op **Active Directory**, klikt u op Hallo directory, klik op de naam van de toepassing hello, **alle instellingen** en klik vervolgens op **eigenschappen** . |
| requested_token_use |Vereist | Hiermee geeft u op hoe Hallo-aanvraag moet worden verwerkt. In Hallo op namens-stroom, Hallo-waarde moet **on_behalf_of**. |
| Bereik |Vereist | Een spatie gescheiden lijst met bereiken voor de tokenaanvraag Hallo. Voor het OpenID Connect, Hallo bereik **openid** moet worden opgegeven.|

Hallo-parameters zijn bijna Hallo dezelfde net als bij Hallo Hallo aanvraag door een gedeeld geheim, behalve dat Hallo client_secret parameter wordt vervangen door twee parameters: een client_assertion_type en client_assertion.

#### Voorbeeld
Hallo na HTTP POST-aanvragen een toegangstoken voor Hallo https://graph.windows.net web-API met een certificaat. Hallo `client_id` Hallo service identificeert die Hallo toegangstoken aanvragen.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Service tooservice access token antwoord
Een geslaagde reactie is een antwoord JSON OAuth 2.0 Hello parameters te volgen.

| Parameter | Beschrijving |
| --- | --- |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo alleen type dat ondersteunt Azure AD **Bearer**. Zie voor meer informatie over bearer-tokens Hallo [OAuth 2.0 autorisatie Framework: Bearer-Token gebruik (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| Bereik |Hallo-bereik van toegang verleend in Hallo-token. |
| expires_in |Hallo-lengte van tijd Hallo toegangstoken is ongeldig (in seconden). |
| expires_on |Hallo tijd wanneer Hallo toegangstoken is verlopen. Hallo datum wordt weergegeven als het aantal seconden Hallo vanaf 1970-01-01T0:0:0Z UTC tot verlooptijd Hallo. Deze waarde is gebruikte toodetermine Hallo levensduur van tokens in de cache. |
| Resource |Hallo App ID URI Hallo service (beveiligde resource) ontvangen. |
| access_token |Hallo aangevraagde toegangstoken. Hallo service aanroepen kunt dit token tooauthenticate toohello ontvangende service gebruiken. |
| id_token |Hallo aangevraagde id. token. Hallo aanroepen van de service kunt gebruiken deze tooverify Hallo-gebruikers-id en beginnen met een sessie met de Hallo gebruiker. |
| refresh_token |Hallo-vernieuwingstoken voor Hallo aangevraagd toegangstoken. Hallo aanroepen van de service kunt gebruiken dit token toorequest een andere toegangstoken nadat Hallo huidige toegangstoken is verlopen. |

### Geslaagd antwoord voorbeeld
Hallo volgende voorbeeld ziet u een geslaagd antwoord tooa aanvraag voor een toegangstoken voor Hallo https://graph.windows.net web-API.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Fout antwoord voorbeeld
Reactie op een fout is geretourneerd door Azure AD-tokeneindpunt wanneer u probeert een toegangstoken tooacquire voor downstream Hallo-API als Hallo downstream-API een beleid voor voorwaardelijke toegang zoals multi-factor authentication-server erop is ingesteld heeft. Hallo middelste laag service moet deze fout toohello-clienttoepassing surface zodat de clienttoepassing Hallo Hallo gebruiker interactie toosatisfy Hallo voorwaardelijk toegangsbeleid kunt bieden.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Gebruik Hallo access token tooaccess Hallo beveiligd resource
Nu Hallo middelste laag service Hallo token verkregen hierboven toomake geverifieerde aanvragen toohello downstream kunt web-API, door de instelling Hallo-token in Hallo `Authorization` header.

### Voorbeeld
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Volgende stappen
Meer informatie over Hallo OAuth 2.0-protocol en een andere manier tooperform service tooservice auth met clientreferenties.
* [Service tooservice auth met OAuth 2.0-client referenties grant in Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 in Azure AD](active-directory-protocols-oauth-code.md)
