---
title: aaaUse Azure AD v2.0 tooaccess resources zonder gebruikersinteractie beveiligen | Microsoft Docs
description: Webtoepassingen bouwen met behulp van hello Azure AD-implementatie van Hallo OAuth 2.0-protocol voor verificatie.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 en Hallo OAuth 2.0 clientreferenties stromen
Kunt u Hallo [OAuth 2.0-clientreferenties verlenen](http://tools.ietf.org/html/rfc6749#section-4.4), soms ook wel *tweearmige OAuth*, tooaccess web gehoste bronnen met behulp van de identiteit van een toepassing hello. Dit type grant vaak wordt gebruikt voor de server naar server interacties dat moeten worden uitgevoerd op de achtergrond hello, zonder directe interactie met een gebruiker. Deze typen toepassingen worden vaak waarnaar wordt verwezen tooas *daemons* of *-serviceaccounts*.

> [!NOTE]
> Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen. toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

In Hallo vaker voorkomende *OAuth driearmige*, een clienttoepassing toegekende machtiging tooaccess een bron is namens een specifieke gebruiker. Hallo-machtiging is overgedragen Hallo gebruiker toohello tijdens van toepassing, meestal Hallo [toestemming](active-directory-v2-scopes.md) proces. Echter, in de clientreferentiestroom hello, machtigingen worden verleend rechtstreeks toohello toepassing zelf. Wanneer Hallo app een token tooa resource geeft, Hallo resource wordt afgedwongen dat Hallo app zelf autorisatie tooperform een actie heeft en niet die Hallo de gebruiker toestemming heeft.

## Protocol-diagram
Hallo gehele clientreferentiestroom lijkt vergelijkbare toohello volgende diagram. Hallo stappen verderop in dit artikel worden beschreven.

![Clientreferentiestroom](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Directe autorisatie ophalen
Een app ontvangt doorgaans direct autorisatie tooaccess een resource op twee manieren: via een toegangsbeheerlijst (ACL) op Hallo resource of machtingstoewijzing toepassing in Azure Active Directory (Azure AD). Deze twee methoden zijn Hallo meest voorkomende in Azure AD en het is raadzaam deze voor clients en bronnen die Hallo clientreferentiestroom uitvoeren. Een resource kunt tooauthorize de clients op andere manieren echter. Elke resource-server kunt Hallo-methode die zinvol Hallo meeste voor de toepassing.

### Toegangsbeheerlijsten
Een resourceprovider mogelijk een autorisatie-controle op basis van een lijst met toepassings-id's die deze kent en een specifiek niveau van toegang tot verleent afdwingen. Wanneer Hallo resource een token uit Hallo v2.0-eindpunt ontvangt, kan het decoderen Hallo token en Hallo-client toepassings-ID ophalen uit het Hallo `appid` en `iss` claims. Vergelijkt vervolgens de toepassing hello tegen een ACL die wordt bijgehouden. Hallo granulatie van de ACL's en de methode kan aanzienlijk variëren tussen resources.

Een algemene gebruiksvoorbeeld is toouse een ACL-toorun voor een webtoepassing of voor een Web-API test. Hallo-Web-API kan alleen een subset van de volledige machtigingen tooa specifieke client verlenen. een testclient die u verkrijgt tokens van Hallo v2.0-eindpunt en verzendt deze API toohello maken toorun end-to-end tests op Hallo-API Hallo API vervolgens controles Hallo ACL voor Hallo test de toepassings-ID van de client voor volledige toegang tot de volledige functionaliteit van toohello-API's. Als u dit soort ACL gebruikt, moet u niet alleen Hallo aanroeper toovalidate `appid` waarde. Ook valideren dat Hallo `iss` waarde Hallo-token wordt vertrouwd.

Dit type verificatie is gebruikelijk daemons en serviceaccounts voor groepen die tooaccess gegevens die eigendom zijn van de consument gebruikers met persoonlijke Microsoft-account nodig. Voor gegevens die eigendom zijn van organisaties, is het raadzaam dat u nodig autorisatie Hallo via Toepassingsmachtigingen voor de krijgt.

### Toepassingsmachtigingen
U kunt in plaats van ACL's, API's tooexpose een reeks Toepassingsmachtigingen. Een toepassing toestemming tooan toepassing is verleend door een beheerder en kunt gebruikte alleen tooaccess gegevens eigendom zijn van die organisatie en werknemers. Bijvoorbeeld: Microsoft Graph beschrijft de verschillende toepassing machtigingen toodo Hallo volgende:

* E-mail in alle postvakken lezen
* E-mail in alle postvakken lezen en schrijven
* E-mail met elke willekeurige gebruiker als afzender verzenden
* Active directory-gegevens lezen

Voor meer informatie over de machtigingen van een toepassing, gaat u te[Microsoft Graph](https://graph.microsoft.io).

Toepassingsmachtigingen toouse in uw app stappen bespreken we in de volgende secties Hallo Hallo.

#### Hallo machtigingen in Hallo-portal voor registratie van app
1. Ga tooyour toepassing in Hallo [toepassing-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of [maken van een app](active-directory-v2-app-registration.md), als u dat nog niet gedaan hebt. U moet toouse ten minste één Toepassingsgeheim bij het maken van uw app.
2. Zoek Hallo **Direct Toepassingsmachtigingen** sectie en voeg vervolgens Hallo machtigingen die vereist dat uw app.
3. **Sla** Hallo van app-registratie.

#### Aanbevolen: Meld u Hallo gebruiker in tooyour app
Normaal gesproken als u een toepassing die gebruikmaakt van machtigingen voor een toepassing bouwen, Hallo app vereist dat een pagina of weergave op welke Hallo beheerder keurt deze goed Hallo-app-machtigingen. Deze pagina kan deel uitmaken van Hallo-app aanmelden flow, onderdeel van de Hallo-app-instellingen of deze kan worden toegewezen 'verbinding' stroom. In veel gevallen kan zinvol het voor Hallo app tooshow dit "verbinding maken' weergave alleen nadat een gebruiker is aangemeld met een werk- of school Microsoft-account.

Als u zich Hallo-gebruiker in de app tooyour aanmeldt, kunt u identificeren Hallo organisatie toowhich Hallo gebruiker behoort Toepassingsmachtigingen Hallo Hallo gebruiker tooapprove vergeet. Hoewel niet strikt noodzakelijk is, kunt u u bij het maken van een intuïtieve ervaring voor uw gebruikers. toosign hello gebruiker in Volg ons [v2.0 protocol zelfstudies](active-directory-v2-protocols.md).

#### Hallo-machtigingen voor aanvragen van een directory-beheerder
Wanneer u klaar toorequest machtigingen van de organisatie Hallo beheerder bent, kunt u Hallo gebruiker toohello v2.0 omleiden *toestemming beheereindpunt*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parameter | Voorwaarde | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo directory-tenant die u wilt dat de machtiging toorequest van. Dit kan zijn in de beschrijvende naam van de indeling of GUID. Als u niet weet welke tenant Hallo-gebruiker behoort tooand die u wilt dat ze met een tenant, gebruik aanmelden toolet `common`. |
| client_id |Vereist |Hallo toepassing-ID die Hallo [toepassing Registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour app toegewezen. |
| redirect_uri |Vereist |Hallo omleidings-URI waar u Hallo antwoord toobe voor uw app toohandle verzonden. Deze moet exact overeenkomen met een van Hallo omleidings-URI's die u hebt geregistreerd in Hallo-portal, behalve dat het URL-codering moet en aanvullende padsegmenten kan hebben. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in Hallo token antwoord wordt geretourneerd. Een tekenreeks van inhoud die u wilt dat kan zijn. Hallo-status is gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |

Azure AD wordt op dit punt wordt afgedwongen of alleen een tenantbeheerder toocomplete Hallo aanvraag kunt aanmelden. Hallo beheerder wordt tooapprove die alle rechtstreekse Toepassingsmachtigingen die u hebt aangevraagd voor uw app in app-registratieportal Hallo Hallo gevraagd.

##### Geslaagde reactie
Hallo beheerder machtigingen voor uw toepassing hello goedkeurt, Hallo geslaagd antwoord ziet er uit als volgt:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parameter | Beschrijving |
| --- | --- | --- |
| Tenant |Hallo directory-tenant die uw toepassing hello worden machtigingen verleend die deze aangevraagd, in GUID-indeling. |
| state |Een waarde die is opgenomen in Hallo-aanvraag die ook in Hallo token antwoord wordt geretourneerd. Een tekenreeks van inhoud die u wilt dat kan zijn. Hallo-status is gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| admin_consent |Stel te**true**. |

##### Foutbericht
Als Hallo beheerder machtigingen voor uw toepassing hello niet goedkeurt, mislukt de Hallo antwoord ziet er als volgt:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parameter | Beschrijving |
| --- | --- | --- |
| error |Een code fouttekenreeks waarmee u tooclassify typen kunt van fouten en waarmee u tooreact tooerrors kunt gebruiken. |
| error_description |Een specifiek foutbericht waarmee u kunt identificeren Hallo hoofdoorzaak van een fout. |

Nadat u een geslaagde reactie van Hallo app inrichting eindpunt ontvangen hebt, is uw app Hallo direct Toepassingsmachtigingen aangevraagde ervaring. U kunt nu een token voor Hallo-bron die u wilt aanvragen.

## Een token ophalen
Nadat u Hallo benodigde machtiging hebt voor uw toepassing hebt verkregen, kunt u doorgaan met het ophalen van de toegangstokens voor API's. een token met behulp van Hallo client referenties grant tooget verzenden een POST-aanvraag toohello `/token` v2.0-eindpunt:

### Het eerste aanvraagnummer: aanvraag voor toegang tot token met een gedeeld geheim

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parameter | Voorwaarde | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassing-ID die Hallo [toepassing Registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour app toegewezen. |
| Bereik |Vereist |Hallo-waarde doorgegeven voor Hallo `scope` parameter in deze aanvraag moet Hallo resource identifier (URI van aanvraag-ID) van het Hallo-bron die u wilt dat, aangebracht Hello `.default` achtervoegsel. Hallo Microsoft Graph Hallo-waarde is bijvoorbeeld `https://graph.microsoft.com/.default`. Deze waarde informeert Hallo v2.0-eindpunt dat alle Hallo rechtstreekse toepassing machtiging die u voor uw app hebt geconfigureerd, deze moet uitgeven van een token voor Hallo die zijn gekoppeld aan het Hallo-bron die u wilt dat toouse. |
| client_secret |Vereist |Hello Toepassingsgeheim die u voor uw app in de portal voor wachtwoordregistratie Hallo-app hebt gegenereerd. |
| grant_type |Vereist |Moet `client_credentials`. |

### Tweede geval: aanvraag voor toegang tot token met een certificaat

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parameter | Voorwaarde | Beschrijving |
| --- | --- | --- |
| client_id |Vereist |Hallo toepassing-ID die Hallo [toepassing Registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour app toegewezen. |
| Bereik |Vereist |Hallo-waarde doorgegeven voor Hallo `scope` parameter in deze aanvraag moet Hallo resource identifier (URI van aanvraag-ID) van het Hallo-bron die u wilt dat, aangebracht Hello `.default` achtervoegsel. Hallo Microsoft Graph Hallo-waarde is bijvoorbeeld `https://graph.microsoft.com/.default`. Deze waarde informeert Hallo v2.0-eindpunt dat alle Hallo rechtstreekse toepassing machtiging die u voor uw app hebt geconfigureerd, deze moet uitgeven van een token voor Hallo die zijn gekoppeld aan het Hallo-bron die u wilt dat toouse. |
| client_assertion_type |Vereist |Hallo-waarde moet liggen`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Vereist | Een (een JSON Web Token) bewering die u toocreate nodig hebt en ondertekenen met het Hallo-certificaat geregistreerd als de referenties voor uw toepassing. Meer informatie over [referenties van het certificaat](active-directory-certificate-credentials.md) toolearn hoe tooregister uw certificaat en het Hallo-indeling van Hallo verklaring.|
| grant_type |Vereist |Moet `client_credentials`. |

Hallo-parameters zijn bijna Hallo dezelfde net als bij Hallo Hallo aanvraag door een gedeeld geheim, behalve dat Hallo client_secret parameter wordt vervangen door twee parameters: een client_assertion_type en client_assertion.

### Geslaagde reactie
Een geslaagde reactie ziet er als volgt:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo aangevraagde toegangstoken. Hallo-app kunt dit token tooauthenticate toohello beveiligd resource, zoals tooa Web-API gebruiken. |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo alleen type dat ondersteunt Azure AD `bearer`. |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |

### Foutbericht
Een foutmelding ziet er als volgt:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die u tooclassify typen fouten die optreden en tooreact tooerrors kunt gebruiken. |
| error_description |Een specifiek foutbericht die u kan helpen identificeren Hallo hoofdoorzaak van een verificatiefout. |
| error_codes |Een lijst met foutcodes STS-specifieke die met diagnostische gegevens helpen kunnen. |
| tijdstempel |Hallo tijd waarin Hallo-fout is opgetreden. |
| trace_id |Een unieke id voor Hallo-aanvraag die u met diagnostische gegevens helpen kan. |
| correlation_id |Een unieke id voor Hallo-aanvraag die u met diagnostische gegevens over de onderdelen helpen kan. |

## Gebruik een token
Nu u een token hebt aangeschaft, gebruiken Hallo token toomake aanvragen toohello resource. Wanneer het Hallo-token is verlopen, herhaalt u Hallo aanvraag toohello `/token` eindpunt tooacquire een nieuw toegangstoken.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Codevoorbeeld
een voorbeeld van een toepassing dat implements client referenties grant Hallo via Hallo beheerder toestemming eindpunt toosee Zie onze [v2.0-daemon-codevoorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
