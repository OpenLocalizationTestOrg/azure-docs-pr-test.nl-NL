---
title: aaaAzure AD v2.0 OAuth-autorisatie Code stromen | Microsoft Docs
description: Gebouw webtoepassingen die gebruikmaken van Azure AD-implementatie van Hallo OAuth 2.0-protocol voor verificatie.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Protocollen v2.0 - OAuth 2.0-Autorisatiecodestroom
Hallo OAuth 2.0 autorisatie code grant kan worden gebruikt in apps die zijn geïnstalleerd op een apparaat toogain toegang tooprotected resources, zoals web-API's.  Hallo app model v2.0 van implementatie van OAuth 2.0 gebruikt, kunt u aanmelden en API tooyour mobiele en bureaublad-apps toevoegen.  Deze handleiding is taalonafhankelijk en beschrijft hoe toosend en HTTP-berichten ontvangen zonder dat u een van onze open source-bibliotheken.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

Hallo OAuth 2.0-autorisatiecodestroom wordt beschreven in in [sectie 4.1 van Hallo OAuth 2.0-specificatie](http://tools.ietf.org/html/rfc6749).  Het gebruikte tooperform verificatie en autorisatie in de meeste Hallo van app-typen, inclusief is [web-apps](active-directory-v2-flows.md#web-apps) en [systeemeigen geïnstalleerde apps](active-directory-v2-flows.md#mobile-and-native-apps).  Hiermee kunt apps toosecurely verkrijgen access_tokens die kunnen worden gebruikt tooaccess resources die zijn beveiligd met Hallo v2.0-eindpunt.  

## Protocol-diagram
Op een hoog niveau weergegeven Hallo volledige authenticatiestroom voor een native/mobile-applicatie iets als volgt:

![OAuth autorisatiecode stroom](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Aanvraag een autorisatiecode
Hallo-autorisatiecodestroom begint met de Hallo client doorsturen Hallo gebruiker toohello `/authorize` eindpunt.  In deze aanvraag Hallo-client geeft aan Hallo machtigingen moet tooacquire van Hallo gebruiker:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Klik Hallo-koppeling hieronder tooexecute deze aanvraag. Na het aanmelden, uw browser te moet worden omgeleid`https://localhost/myapp/` met een `code` in de adresbalk Hallo.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassings-Id die Hallo-portal voor wachtwoordregistratie ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) toegewezen van uw app. |
| response_type |Vereist |Moet bevatten `code` voor Hallo-autorisatiecodestroom. |
| redirect_uri |Aanbevolen |Hallo redirect_uri van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app.  Deze moet exact overeenkomen met een Hallo redirect_uris die u geregistreerd in het Hallo-portal, behalve url gecodeerd moet.  Voor mobiele en systeemeigen apps, moet u de standaardwaarde Hallo van `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| Bereik |Vereist |Een door spaties gescheiden lijst met [scopes](active-directory-v2-scopes.md) dat u wilt dat Hallo gebruiker tooconsent aan. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende token back tooyour app worden moet.  Kan `query` of `form_post`. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd.  Een tekenreeks van inhoud die u wenst dat kan zijn.  Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor [voorkomen van aanvraagvervalsing op meerdere sites aanvallen](http://tools.ietf.org/html/rfc6749#section-10.12).  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| prompt |Optioneel |Geeft Hallo type gebruikersinteractie is vereist.  alleen geldige waarden op dit moment 'aanmelding', 'none zijn' Hallo ' toestemming geven '.  `prompt=login`geforceerd wordt Hallo gebruiker tooenter hun referenties op die het negatief maken van eenmalige aanmelding op verzoek.  `prompt=none`Hallo tegengestelde - brengt dat die Hallo-gebruiker niet vragen beeïndigen krijgt is.  Als het Hallo-aanvraag kan niet worden voltooid in stille modus via eenmalige aanmelding, worden Hallo v2.0-eindpunt een fout geretourneerd.  `prompt=consent`trigger Hallo OAuth wordt dialoogvenster na Hallo gebruiker zich aanmeldt, Hallo gebruiker toogrant machtigingen toohello app gevraagd toestemming. |
| login_hint |Optioneel |Worden kunnen gebruikt toopre-opvulling Hallo gebruikersnaam, e adresveld Hallo aanmelden pagina Hallo gebruiker, als u hun gebruikersnaam tevoren weet.  Vaak apps deze parameter wordt gebruikt tijdens de hervalidatie Hallo gebruikersnaam die al worden opgehaald uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Optioneel |Een van `consumers` of `organizations`.  Als opgenomen, wordt het Hallo detectie op basis van e-mailbericht proces overslaan die gebruiker doorloopt op Hallo v2.0 aanmeldingspagina, voorloopspaties tooa iets sneller gebruikerservaring.  Vaak apps wordt met deze parameter gebruikt tijdens de hervalidatie door uit te pakken Hallo `tid` van een vorige aanmelden.  Als hello `tid` claim waarde is `9188040d-6c67-4c5b-b112-36a304b66dad`, moet u `domain_hint=consumers`.  Gebruik anders `domain_hint=organizations`. |

Op dit moment Hallo gebruiker worden tooenter gevraagd hun referenties en volledige Hallo-verificatie.  Hallo v2.0-eindpunt zorgt er ook die gebruiker Hallo toohello machtigingen die zijn aangegeven in Hallo heeft ingestemd `scope` queryparameter.  Als gebruiker Hallo tooany van deze machtigingen niet heeft ingestemd, wordt het Hallo gebruiker tooconsent toohello vereist machtigingen gevraagd.  Details van [machtigingen, toestemming en multitenant apps vindt u hier](active-directory-v2-scopes.md).

Zodra Hallo gebruiker wordt geverifieerd en toestemming verleent, Hallo v2.0-eindpunt resulteert in een antwoord tooyour app op Hallo aangegeven `redirect_uri`, met behulp van de methode in Hallo Hallo `response_mode` parameter.

#### Geslaagde reactie
Een geslaagde reactie met `response_mode=query` lijkt:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parameter | Beschrijving |
| --- | --- |
| code |Hallo authorization_code die Hallo app aangevraagd. Hallo-app kunt Hallo autorisatie code toorequest een toegangstoken voor de doelresource hello gebruiken.  Authorization_codes zijn zeer korte levensduur, doorgaans ze verlopen na ongeveer 10 minuten. |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Hallo app dient te verifiëren dat de statuswaarden Hallo in Hallo-aanvraag en -antwoord identiek zijn. |

#### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat Hallo app ze op de juiste wijze kan verwerken:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |

#### Foutcodes voor autorisatie eindpunt fouten
Hallo volgende tabel beschrijft Hallo verschillende foutcodes die kunnen worden geretourneerd in Hallo `error` parameter van het Hallo-foutmelding.

| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een ontwikkeling fout wordt meestal onderschept tijdens de eerste test. |
| unauthorized_client |Hallo-clienttoepassing is niet toegestaan toorequest een autorisatiecode. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| ACCESS_DENIED |Resource-eigenaar toestemming geweigerd |Hallo-clienttoepassing kan melden Hallo-gebruiker die deze kan niet worden voortgezet tenzij Hallo gebruiker hiermee akkoord gaat. |
| unsupported_response_type |Hallo autorisatie server biedt geen ondersteuning voor antwoordtype Hallo Hallo-aanvraag. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een ontwikkeling fout wordt meestal onderschept tijdens de eerste test. |
| server_error |Hallo-server heeft een onverwachte fout aangetroffen. |Hallo aanvraag opnieuw proberen. Deze fouten kunnen worden veroorzaakt door tijdelijke omstandigheden. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege een tijdelijke fout. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege een tijdelijk probleem. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven met het Hallo-resource, indien aanwezig, is niet geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |

## Aanvragen van een toegangstoken
Nu dat u een authorization_code hebt aangeschaft en gemachtigd door de gebruiker hello, kunt u gebruikmaken van Hallo `code` voor een `access_token` toohello gewenst resource, door te sturen een `POST` toohello aanvragen `/token` eindpunt:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Probeer deze aanvraag uit te voeren in Postman! (Vergeet niet tooreplace hello `code`) [ ![uitvoeren in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassings-Id die Hallo-portal voor wachtwoordregistratie ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) toegewezen van uw app. |
| grant_type |Vereist |Moet `authorization_code` voor Hallo-autorisatiecodestroom. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Hallo scopes aangevraagd in deze fase moet worden gelijkwaardige tooor een subset van Hallo scopes aangevraagd in de eerste arm Hallo.  Als Hallo-bereiken die zijn opgegeven in deze aanvraag span meerdere resource-servers, worden een token voor Hallo resource is opgegeven in de eerste bereik Hallo geretourneerd op Hallo v2.0-eindpunt.  Raadpleeg te voor een meer gedetailleerde uitleg van bereiken[machtigingen, toestemming en -scopes](active-directory-v2-scopes.md). |
| code |Vereist |Hallo authorization_code die u tijdens de eerste arm Hallo van Hallo stroom opgehaald. |
| redirect_uri |Vereist |Hallo dezelfde redirect_uri-waarde die gebruikt tooacquire hello authorization_code is. |
| client_secret |vereist voor web-apps |Hallo-toepassingsgeheim die u in de registratieportal Hallo-app voor uw app hebt gemaakt.  Deze mag niet worden gebruikt in een eigen app omdat client_secrets betrouwbaar kunnen niet worden opgeslagen op apparaten.  Het is vereist voor de web-apps en web-API's die veilig Hallo mogelijkheid toostore hello client_secret op Hallo serverzijde hebben. |

#### Geslaagde reactie
Een geslaagde reactie token, ziet er als:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo aangevraagde toegangstoken. Hallo-app kunt dit token tooauthenticate toohello beveiligd resource, zoals een web-API gebruiken. |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo is alleen type die ondersteuning biedt voor Azure AD Bearer |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| Bereik |Hallo-scopes die Hallo access_token is geldig voor. |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo app kunt gebruiken dit token aanvullende toegangstokens verkrijgen nadat Hallo huidige toegangstoken is verlopen.  Refresh_tokens zijn lange levensduur en gebruikte tooretain toegang tooresources voor langere tijd kan worden.  Raadpleeg voor meer details toohello [v2.0 tokenverwijzing](active-directory-v2-tokens.md). |
| id_token |Een niet-ondertekende JSON Web Token (JWT). Hallo-app kan base64Url decoderen Hallo segmenten van deze informatie token toorequest over Hallo-gebruiker die zich aangemeld. Hallo-app kunt Hallo waarden in de cache en deze weer te geven, maar moet niet vertrouwen op deze beveiligingsgrenzen of autorisatie.  Zie voor meer informatie over id_tokens hello [v2.0-eindpunt tokenverwijzing](active-directory-v2-tokens.md). |

#### Foutbericht
Foutberichten ziet er als volgt:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |
| error_codes |Een lijst van STS specifieke foutcodes die bij het diagnostische gegevens helpen. |
| tijdstempel |Hallo tijd waarin Hallo-fout is opgetreden. |
| trace_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens helpen. |
| correlation_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens over de onderdelen helpen. |

#### Foutcodes voor token-eindpunt fouten
| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen |
| invalid_grant |Hallo autorisatiecode is ongeldig of is verlopen. |Probeer een nieuwe aanvraag toohello `/authorize` eindpunt |
| unauthorized_client |Hallo geverifieerde client is niet geautoriseerd toouse deze toestemming verlenen type. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| invalid_client |Clientverificatie is mislukt. |Hallo-clientreferenties zijn niet geldig. toofix, beheerder van de toepassing hello updates Hallo-referenties. |
| unsupported_grant_type |Hallo autorisatie server biedt geen ondersteuning voor Hallo authorization grant type. |Wijziging Hallo machtigingstype in Hallo-aanvraag. Dit type fout moet worden uitgevoerd tijdens de ontwikkeling en worden gedetecteerd tijdens de eerste test. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven met het Hallo-resource, indien aanwezig, is niet geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| interaction_required |Hallo aanvraag vereist gebruikersinteractie. Bijvoorbeeld, is een stap extra authenticatie vereist. |Hallo-aanvraag met Hallo opnieuw proberen dezelfde resource. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege een tijdelijk probleem. |

## Hallo toegangstoken gebruiken
Nu dat u hebt gekregen een `access_token`, kunt u Hallo-token in aanvragen tooWeb API's door deze in Hallo `Authorization` header:

> [!TIP]
> Het uitvoeren van deze aanvraag in Postman! (Hallo vervangen `Authorization` header eerste) [ ![uitvoeren in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Hallo toegangstoken vernieuwen
Access_tokens korte worden gehouden en moet u deze vernieuwen nadat ze toegang krijgen tot bronnen toocontinue verlopen.  U kunt dit doen door het indienen van een andere `POST` aanvragen toohello `/token` eindpunt, ditmaal Hallo bieden `refresh_token` in plaats van Hallo `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Probeer deze aanvraag uit te voeren in Postman! (Vergeet niet tooreplace hello `refresh_token`) [ ![uitvoeren in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn `common`, `organizations`, `consumers`, en het tenant-id's.  Zie voor meer details [protocol basisbeginselen](active-directory-v2-protocols.md#endpoints). |
| client_id |Vereist |Hallo toepassings-Id die Hallo-portal voor wachtwoordregistratie ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) toegewezen van uw app. |
| grant_type |Vereist |Moet `refresh_token` voor deze fase van de Hallo-autorisatiecodestroom. |
| Bereik |Vereist |Een door spaties gescheiden lijst met bereiken.  Hallo scopes aangevraagd in deze fase moet worden gelijkwaardige tooor een subset van Hallo scopes aangevraagd in Hallo oorspronkelijke authorization_code aanvraag arm.  Als Hallo-bereiken die zijn opgegeven in deze aanvraag span meerdere resource-servers, worden een token voor Hallo resource is opgegeven in de eerste bereik Hallo geretourneerd op Hallo v2.0-eindpunt.  Raadpleeg te voor een meer gedetailleerde uitleg van bereiken[machtigingen, toestemming en -scopes](active-directory-v2-scopes.md). |
| refresh_token |Vereist |Hallo refresh_token die u hebt verkregen in de tweede arm Hallo van Hallo stroom. |
| redirect_uri |Vereist |Hallo dezelfde redirect_uri-waarde die gebruikt tooacquire hello authorization_code is. |
| client_secret |vereist voor web-apps |Hallo-toepassingsgeheim die u in de registratieportal Hallo-app voor uw app hebt gemaakt.  Deze mag niet worden gebruikt in een eigen app omdat client_secrets betrouwbaar kunnen niet worden opgeslagen op apparaten.  Het is vereist voor de web-apps en web-API's die veilig Hallo mogelijkheid toostore hello client_secret op Hallo serverzijde hebben. |

#### Geslaagde reactie
Een geslaagde reactie token, ziet er als:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo aangevraagde toegangstoken. Hallo-app kunt dit token tooauthenticate toohello beveiligd resource, zoals een web-API gebruiken. |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo is alleen type die ondersteuning biedt voor Azure AD Bearer |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| Bereik |Hallo-scopes die Hallo access_token is geldig voor. |
| refresh_token |Een nieuwe OAuth 2.0-vernieuwingstoken. U moet de oude vernieuwen Hallo vervangen token met dit token tooensure recent overgenomen vernieuwen blijven geldig zo lang mogelijk voor het vernieuwen van tokens. |
| id_token |Een niet-ondertekende JSON Web Token (JWT). Hallo-app kan base64Url decoderen Hallo segmenten van deze informatie token toorequest over Hallo-gebruiker die zich aangemeld. Hallo-app kunt Hallo waarden in de cache en deze weer te geven, maar moet niet vertrouwen op deze beveiligingsgrenzen of autorisatie.  Zie voor meer informatie over id_tokens hello [v2.0-eindpunt tokenverwijzing](active-directory-v2-tokens.md). |

#### Foutbericht
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |
| error_codes |Een lijst van STS specifieke foutcodes die bij het diagnostische gegevens helpen. |
| tijdstempel |Hallo tijd waarin Hallo-fout is opgetreden. |
| trace_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens helpen. |
| correlation_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens over de onderdelen helpen. |

Zie voor een beschrijving van het Hallo-foutcodes en Hallo aanbevolen clientactie, [foutcodes voor token-eindpunt fouten](#error-codes-for-token-endpoint-errors).

