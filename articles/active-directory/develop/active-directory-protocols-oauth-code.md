---
title: aaaUnderstand hello OAuth 2.0-autorisatiecodestroom in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse HTTP-berichten tooauthorize toegang tot tooweb toepassingen en web-API's in uw tenant met behulp van Azure Active Directory en OAuth 2.0.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Toegang tooweb toepassingen met behulp van OAuth 2.0 en Azure Active Directory autoriseren
Azure Active Directory (Azure AD) maakt gebruik van OAuth 2.0 tooenable u tooauthorize toegang tooweb toepassingen en web-API's in uw Azure AD-tenant. Deze handleiding is taalonafhankelijk en beschrijft hoe toosend en HTTP-berichten ontvangen zonder dat u een van onze open source-bibliotheken.

Hallo OAuth 2.0-autorisatiecodestroom wordt beschreven in [sectie 4.1 van Hallo OAuth 2.0-specificatie](https://tools.ietf.org/html/rfc6749#section-4.1). Het is gebruikte tooperform verificatie en autorisatie in de meeste toepassingstypen, met inbegrip van web-apps en systeemeigen apps hebben geïnstalleerd.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Stroom van OAuth 2.0-autorisatie
Op een hoog niveau ziet Hallo volledige autorisatie stroom voor een toepassing er nogal zo:

![OAuth autorisatiecode stroom](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Aanvraag een autorisatiecode
Hallo-autorisatiecodestroom begint met de Hallo client doorsturen Hallo gebruiker toohello `/authorize` eindpunt. In deze aanvraag Hallo-client geeft aan Hallo machtigingen moet tooacquire van Hallo-gebruiker. U krijgt Hallo OAuth 2.0-eindpunten van uw toepassing pagina in de klassieke Azure-Portal in Hallo **eindpunten weergeven** knop in Hallo onder lade.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn tenant-id's, bijvoorbeeld `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` of `contoso.onmicrosoft.com` of `common` voor tenant-onafhankelijke tokens |
| client_id |Vereist |Hallo toepassings-Id toegewezen tooyour app bij de registratie met Azure AD. U kunt dit vinden in hello Azure-Portal. Klik op **Active Directory**, klikt u op Hallo directory, kies de toepassing hello en klikt u op **configureren** |
| response_type |Vereist |Moet bevatten `code` voor Hallo-autorisatiecodestroom. |
| redirect_uri |Aanbevolen |Hallo redirect_uri van uw app, waarbij verificatie reacties kunnen worden verzonden en ontvangen door uw app.  Deze moet exact overeenkomen met een Hallo redirect_uris die u geregistreerd in het Hallo-portal, behalve url gecodeerd moet.  Voor mobiele en systeemeigen apps, moet u de standaardwaarde Hallo van `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |Aanbevolen |Hiermee geeft u Hallo-methode die gebruikt toosend Hallo resulterende token back tooyour app worden moet.  Kan `query` of `form_post`. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag wordt ook Hallo token antwoord geretourneerd. Een willekeurig gegenereerde unieke waarde wordt doorgaans gebruikt voor [voorkomen van aanvraagvervalsing op meerdere sites aanvallen](http://tools.ietf.org/html/rfc6749#section-10.12).  Hallo-status is bovendien gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| Resource |Optioneel |Hallo App ID URI van Hallo web-API (beveiligde resource). toofind hello App ID URI van Hallo web-API, in hello Azure-Portal klikt u op **Active Directory**, klikt u op Hallo directory, klikt u op de toepassing hello en klik vervolgens op **configureren**. |
| prompt |Optioneel |Geven Hallo type gebruikersinteractie is vereist.<p> Geldige waarden zijn: <p> *aanmelding*: Hallo gebruiker zou na vragen aan gebruiker tooreauthenticate. <p> *toestemming*: gebruiker toestemming heeft gekregen, maar moet toobe bijgewerkt. Hallo-gebruiker moet na vragen aan gebruiker tooconsent. <p> *admin_consent*: een beheerder moet na vragen aan gebruiker tooconsent namens alle gebruikers in hun organisatie |
| login_hint |Optioneel |Mag gebruikte toopre-opvulling Hallo gebruikersnaam, e adresveld van het Hallo-aanmeldingspagina voor de gebruiker hello, als u hun gebruikersnaam tevoren weet.  Vaak apps Gebruik deze parameter tijdens verificatie wordt uitgevoerd, dat al Hallo gebruikersnaam opgehaald uit een eerdere aanmelden met behulp van Hallo `preferred_username` claim. |
| domain_hint |Optioneel |Biedt een aanwijzing over Hallo tenant of het aanmeldingsdomein waarmee gebruiker Hallo toosign in gebruik. Hallo-waarde van Hallo domain_hint is een geregistreerd domein voor Hallo-tenant. Als Hallo tenant federatieve tooan on-premises adreslijst, leidt AAD toohello opgegeven tenant federation-server. |

> [!NOTE]
> Als Hallo gebruiker deel van een organisatie uitmaakt, kunt een beheerder van de organisatie Hallo toestemming geven of weigeren van de gebruiker Hallo namens of Hallo gebruiker tooconsent toestaan. Hallo gebruiker krijgt Hallo optie tooconsent alleen wanneer Hallo beheerder toestaat.
>
>

Op dit moment Hallo gebruiker tooenter gevraagd hun referenties en toestemming toohello machtigingen die zijn aangegeven in Hallo `scope` queryparameter. Zodra het Hallo-gebruiker wordt geverifieerd en toestemming verleent, Azure AD een antwoord tooyour app verzendt op Hallo `redirect_uri` adres in uw aanvraag.

### Geslaagde reactie
Een geslaagde reactie kan er als volgt uitzien:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parameter | Beschrijving |
| --- | --- |
| admin_consent |Hallo-waarde is True als een beheerder ingestemd tooa aanvraag instemmingsprompt. |
| code |Hallo autorisatie-code die de toepassing hello aangevraagd. Hallo-toepassing kan Hallo autorisatie code toorequest een toegangstoken voor de doelresource hello gebruiken. |
| session_state |Een unieke waarde die de huidige gebruikerssessie Hallo identificeert. Deze waarde is een GUID, maar moet worden behandeld als een ondoorzichtige waarde die wordt doorgegeven zonder onderzoek. |
| state |Als een parameter state is opgenomen in de aanvraag hello, hello dezelfde waarde moet worden weergegeven in het Hallo-antwoord. Het is raadzaam voor Hallo toepassing tooverify dat Hallo statuswaarden in Hallo-aanvraag en -antwoord voordat u antwoord Hallo identiek zijn. Dit helpt toodetect [Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen](https://tools.ietf.org/html/rfc6749#section-10.12) tegen Hallo-client. |

### Foutbericht
Foutberichten kunnen ook worden verzonden toohello `redirect_uri` zodat de toepassing hello ze op de juiste wijze kan verwerken.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een foutwaarde code gedefinieerd in de sectie 5.2 Hallo [OAuth 2.0 autorisatie Framework](http://tools.ietf.org/html/rfc6749). de volgende tabel Hallo Hallo worden foutcodes beschreven die Azure AD als resultaat gegeven. |
| error_description |Een gedetailleerde beschrijving van Hallo-fout. Dit bericht is niet bedoeld toobe eindgebruiker gebruiksvriendelijke. |
| state |Hallo staat een willekeurig gegenereerde niet opnieuw gebruikt getal is dat wordt verzonden in Hallo-aanvraag en geretourneerd in Hallo antwoord tooprevent aanvraagvervalsing op meerdere sites (CSRF) aanvallen. |

#### Foutcodes voor autorisatie eindpunt fouten
Hallo volgende tabel beschrijft Hallo verschillende foutcodes die kunnen worden geretourneerd in Hallo `error` parameter van het Hallo-foutmelding.

| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout voor ontwikkeling en meestal wordt onderschept tijdens de eerste test. |
| unauthorized_client |Hallo-clienttoepassing is niet toegestaan toorequest een autorisatiecode. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| ACCESS_DENIED |Resource-eigenaar toestemming geweigerd |Hallo-clienttoepassing kan melden Hallo-gebruiker die deze kan niet worden voortgezet tenzij Hallo gebruiker hiermee akkoord gaat. |
| unsupported_response_type |Hallo autorisatie server biedt geen ondersteuning voor antwoordtype Hallo Hallo-aanvraag. |Herstel en Hallo aanvraag opnieuw indienen. Dit is een fout voor ontwikkeling en meestal wordt onderschept tijdens de eerste test. |
| server_error |Hallo-server heeft een onverwachte fout aangetroffen. |Hallo aanvraag opnieuw proberen. Deze fouten kunnen worden veroorzaakt door tijdelijke omstandigheden. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke fout. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke situatie. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven met het Hallo-resource, indien aanwezig, is niet geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |

## Hallo autorisatie code toorequest een toegangstoken gebruiken
Nu dat u hebt aangeschaft een autorisatiecode en gemachtigd door de gebruiker hello, kunt u Hallo-code voor een resource van de token toohello gewenst toegang inwisselen door te sturen een POST-aanvraag toohello `/token` eindpunt:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Parameter |  | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo `{tenant}` waarde in het pad van Hallo aanvraag Hallo gebruikte toocontrol die zich in de toepassing hello aanmelden kan kan zijn.  Hallo toegestane waarden zijn tenant-id's, bijvoorbeeld `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` of `contoso.onmicrosoft.com` of `common` voor tenant-onafhankelijke tokens |
| client_id |Vereist |Hallo toepassings-Id toegewezen tooyour app bij de registratie met Azure AD. U kunt dit vinden in Hallo klassieke Azure-Portal. Klik op **Active Directory**, klikt u op Hallo directory, kies de toepassing hello en klikt u op **configureren** |
| grant_type |Vereist |Moet `authorization_code` voor Hallo-autorisatiecodestroom. |
| code |Vereist |Hallo `authorization_code` die u hebt verkregen in de vorige sectie Hallo |
| redirect_uri |Vereist |Hallo dezelfde `redirect_uri` waarde die gebruikt tooacquire hello is `authorization_code`. |
| client_secret |vereist voor web-apps |Hallo-toepassingsgeheim die u in de registratieportal Hallo-app voor uw app hebt gemaakt.  Deze mag niet worden gebruikt in een eigen app omdat client_secrets betrouwbaar kunnen niet worden opgeslagen op apparaten.  Het is vereist voor de web-apps en web-API's, waarvoor Hallo mogelijkheid toostore hello `client_secret` veilig aan de serverzijde Hallo. |
| Resource |vereist als het opgegeven in de autorisatieaanvraag, anders optioneel |Hallo App ID URI van Hallo web-API (beveiligde resource). |

toofind hello App ID URI, in hello Azure-beheerportal, klikt u op **Active Directory**, klikt u op Hallo directory, klikt u op Hallo-toepassing en klik vervolgens op **configureren**.

### Geslaagde reactie
Azure AD retourneert een toegangstoken na een geslaagde reactie. toominimize netwerk aanroepen vanuit de clienttoepassing Hallo en hun bijbehorende latentie, client-toepassing hello moet in de cache toegangstokens Hallo levensduur van token die is opgegeven in Hallo OAuth 2.0-antwoord. toodetermine hello levensduur van token, gebruiken beide Hallo `expires_in` of `expires_on` parameterwaarden.

Als een web API-resource geeft een `invalid_token` foutcode: dit kan duiden op Hallo resource heeft vastgesteld dat Hallo-token is verlopen. Als het Hallo-client en resource klok tijden zijn verschillende (bekend als een 'scheeftrekken keer'), kunt Hallo resource Hallo token toobe verlopen voordat het Hallo-token van de clientcache Hallo is uitgeschakeld. Als dit het geval is, schakelt u Hallo-token van Hallo-cache, zelfs als deze nog steeds binnen de berekende levensduur.

Een geslaagde reactie kan er als volgt uitzien:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo aangevraagde toegangstoken. Hallo-app kunt dit token tooauthenticate toohello beveiligd resource, zoals een web-API gebruiken. |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo alleen typen dat ondersteunt Azure AD Bearer is. Zie voor meer informatie over Bearer-tokens [OAuth2.0 autorisatie Framework: Bearer-Token gebruik (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| expires_on |Hallo tijd wanneer Hallo toegangstoken is verlopen. Hallo datum wordt weergegeven als het aantal seconden Hallo vanaf 1970-01-01T0:0:0Z UTC tot verlooptijd Hallo. Deze waarde is gebruikte toodetermine Hallo levensduur van tokens in de cache. |
| Resource |Hallo App ID URI van Hallo web-API (beveiligde resource). |
| Bereik |Imitatie machtigingen verleend toohello client-toepassing. Hallo standaardmachtiging `user_impersonation`. Hallo-eigenaar van beveiligde resource Hallo kunt u aanvullende waarden registreren in Azure AD. |
| refresh_token |Een OAuth 2.0-vernieuwingstoken. Hallo-app kunt dit token tooacquire extra toegangstokens gebruiken nadat Hallo huidige toegangstoken is verlopen.  Vernieuwen van tokens worden lange levensduur en gebruikte tooretain toegang tooresources voor langere tijd kan worden. |
| id_token |Een niet-ondertekende JSON Web Token (JWT). Hallo-app kan base64Url decoderen Hallo segmenten van deze informatie token toorequest over Hallo-gebruiker die zich aangemeld. Hallo-app kunt Hallo waarden in de cache en deze weer te geven, maar moet niet vertrouwen op deze beveiligingsgrenzen of autorisatie. |

### JWT-Token Claims
Hallo JWT-token in Hallo-waarde van Hallo `id_token` parameter kan worden gedecodeerd naar Hallo claims te volgen:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Zie voor meer informatie over de JSON-webtokens hello [JWT IETF conceptspecificatie](http://go.microsoft.com/fwlink/?LinkId=392344). Lees voor meer informatie over Hallo token typen of claims [ondersteund Token en claimtypen](active-directory-token-and-claims.md)

Hallo `id_token` parameter Hallo claimtypen volgende bevat:

| Claimtype | Beschrijving |
| --- | --- |
| AUD |De doelgroep van Hallo-token. Wanneer het Hallo-token is uitgegeven tooa clienttoepassing, Hallo doelgroep Hallo is `client_id` van Hallo-client. |
| EXP |Verlooptijd. Hallo-tijd waarop het Hallo-token verloopt. Voor de token toobe voor Hallo is geldig, Hallo huidige datum en tijd moet kleiner zijn dan of gelijk toohello `exp` waarde. Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo tijd Hallo token is uitgegeven. |
| family_name |Van de gebruiker achternaam of achternaam. Hallo-toepassing kunt u deze waarde weergeven. |
| given_name |De voornaam van de gebruiker. Hallo-toepassing kunt u deze waarde weergeven. |
| IAT |Op tijdstip afgegeven. Hallo tijd wanneer Hallo JWT is uitgegeven. Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo tijd Hallo token is uitgegeven. |
| ISS |Hallo token verlener identificeert |
| NBF |Niet voor de tijd. Hallo-tijd waarop token Hallo van kracht. Voor de token toobe voor Hallo is geldig moet Hallo huidige datum en tijd groter dan of gelijk toohello Nbf waarde. Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo tijd Hallo token is uitgegeven. |
| OID |Object-id (ID) van het gebruikersobject Hallo in Azure AD. |
| Sub |Token onderwerp-id. Dit is een permanente en onveranderbare id voor het Hallo-gebruiker die de token Hallo beschrijft. Gebruik deze waarde in de cache logica. |
| TID |Tenant-id (ID) van hello Azure AD-tenant die Hallo token heeft uitgegeven. |
| unique_name |Een unieke id voor dat kan worden weergegeven toohello gebruiker. Dit is meestal een UPN (user Principal name). |
| UPN |De UPN van Hallo-gebruiker. |
| ver |Versie. Hallo-versie van Hallo JWT-token, doorgaans 1.0. |

### Foutbericht
Hallo uitgifte van tokens eindpunt fouten zijn foutcodes voor HTTP, omdat het Hallo-clientaanroepen Hallo eindpunt van de uitgifte van tokens rechtstreeks. Bovendien toohello HTTP-statuscode hello Azure AD uitgifte van tokens eindpunt ook retourneert een JSON-document met objecten die Hallo fout wordt beschreven.

Een voorbeeld-foutmelding kan uitzien:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |
| error_codes |Een lijst met foutcodes STS-specifieke die bij het diagnostische gegevens helpen. |
| tijdstempel |Hallo tijd waarin Hallo-fout is opgetreden. |
| trace_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens helpen. |
| correlation_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens over de onderdelen helpen. |

#### HTTP-statuscodes
Hallo bevat volgende tabel Hallo HTTP-statuscodes die Hallo uitgifte van tokens eindpunt retourneert. In sommige gevallen Hallo foutcode voldoende toodescribe Hallo antwoord is, maar als er fouten zijn, moet u tooparse Hallo begeleidende JSON-document en bekijk de foutcode.

| HTTP-Code | Beschrijving |
| --- | --- |
| 400 |Standaardcode voor HTTP. In de meeste gevallen gebruikt en is meestal vanwege tooa onjuist gevormde aanvraag. Herstel en Hallo aanvraag opnieuw indienen. |
| 401 |Verificatie is mislukt. Hallo-aanvraag is bijvoorbeeld Hallo client_secret parameter ontbreekt. |
| 403 |Autorisatie is mislukt. Bijvoorbeeld, Hallo gebruiker geen machtiging tooaccess Hallo resource. |
| 500 |Een interne fout opgetreden bij het Hallo-service. Hallo aanvraag opnieuw proberen. |

#### Foutcodes voor token-eindpunt fouten
| Foutcode | Beschrijving | Clientactie |
| --- | --- | --- |
| invalid_request |Protocolfout, zoals een ontbrekende vereiste parameter. |Herstel en Hallo aanvraag opnieuw indienen |
| invalid_grant |Hallo autorisatiecode is ongeldig of is verlopen. |Probeer een nieuwe aanvraag toohello `/authorize` eindpunt |
| unauthorized_client |Hallo geverifieerde client is niet geautoriseerd toouse deze toestemming verlenen type. |Dit gebeurt meestal wanneer de clienttoepassing Hallo is niet geregistreerd in Azure AD of Azure AD-tenant van toohello gebruiker niet is toegevoegd. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| invalid_client |Clientverificatie is mislukt. |Hallo-clientreferenties zijn niet geldig. toofix, beheerder van de toepassing hello updates Hallo-referenties. |
| unsupported_grant_type |Hallo autorisatie server biedt geen ondersteuning voor Hallo authorization grant type. |Wijziging Hallo machtigingstype in Hallo-aanvraag. Dit type fout moet worden uitgevoerd tijdens de ontwikkeling en worden gedetecteerd tijdens de eerste test. |
| invalid_resource |Hallo doelbron is ongeldig omdat deze niet bestaat, Azure AD kan niet worden gevonden of is niet correct geconfigureerd. |Hiermee wordt aangegeven met het Hallo-resource, indien aanwezig, is niet geconfigureerd in Hallo-tenant. Hallo-toepassing kunt Hallo-gebruiker met instructies voor het Hallo-toepassing installeren en deze toe te voegen tooAzure AD gevraagd. |
| interaction_required |Hallo aanvraag vereist gebruikersinteractie. Bijvoorbeeld, is een stap extra authenticatie vereist. | In plaats van een niet-interactieve aanvraag, probeer het opnieuw met een interactieve autorisatieaanvraag voor Hallo dezelfde resource. |
| temporarily_unavailable |Hallo-server is tijdelijk bezet toohandle Hallo-aanvraag. |Hallo aanvraag opnieuw proberen. Hallo-clienttoepassing kan toohello gebruiker verklaren dat het antwoord is vertraagd vanwege tooa tijdelijke situatie. |

## Hallo access token tooaccess Hallo bron gebruiken
Nu dat u hebt gekregen een `access_token`, kunt u Hallo-token in aanvragen tooWeb API's, door deze in Hallo `Authorization` header. Hallo [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) specificatie legt uit hoe toouse bearer-tokens in HTTP-aanvragen tooaccess beveiligde bronnen.

### Voorbeeld van een aanvraag
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Foutbericht
Beveiligde bronnen en RFC 6750 probleem HTTP-statuscodes implementeren. Als het Hallo-aanvraag bevat geen referenties voor verificatie of het token, Hallo antwoord Hallo ontbreekt bevat een `WWW-Authenticate` header. Wanneer een aanvraag is mislukt, wordt Hallo resource server reageert met Hallo HTTP-statuscode en een foutcode.

Hallo Hieronder volgt een voorbeeld van een mislukte reactie wanneer clientaanvraag Hallo Hallo bearer-token niet omvat:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Foutparameters
| Parameter | Beschrijving |
| --- | --- |
| authorization_uri |Hallo-URI (fysieke eindpunt) van Hallo autorisatie-server. Deze waarde wordt ook gebruikt als een lookup key tooget meer informatie over Hallo server vanaf een detectie-eindpunt. <p><p> Hallo-client moet valideren die Hallo autorisatie-server wordt vertrouwd. Wanneer het Hallo-resource is beveiligd door Azure AD, is het voldoende tooverify die Hallo URL met https://login.microsoftonline.com begint of een andere hostnaam die ondersteuning biedt voor Azure AD. Een resource tenantspecifieke moet altijd een verificatie-URI van de tenant-specifieke retourneren. |
| error |Een foutwaarde code gedefinieerd in de sectie 5.2 Hallo [OAuth 2.0 autorisatie Framework](http://tools.ietf.org/html/rfc6749). |
| error_description |Een gedetailleerde beschrijving van Hallo-fout. Dit bericht is niet bedoeld toobe eindgebruiker gebruiksvriendelijke. |
| bron-id |Retourneert Hallo de unieke id van resource Hallo. Hallo-clienttoepassing deze id kunt gebruiken als de waarde Hallo Hallo `resource` parameter wanneer deze een token voor Hallo bron aanvraagt. <p><p> Het is belangrijk voor Hallo van client-toepassing tooverify deze waarde, anders een schadelijke service kunnen tooinduce mogelijk een **verhoging van bevoegdheden** aanval <p><p> Hallo aanbevolen strategie voor een aanval waardoor is tooverify die Hallo `resource_id` komt overeen met Hallo base van Hallo web API-URL die wordt geopend. Bijvoorbeeld, als https://service.contoso.com/data wordt geopend, Hallo `resource_id` htttps://service.contoso.com/ kan zijn. Hallo-clienttoepassing afwijzen moet een `resource_id` die begint niet met Hallo basis-URL tenzij er een betrouwbare alternatieve manier tooverify Hallo-id. |

#### Foutcodes voor Bearer-schema
Hallo RFC 6750 specificatie definieert Hallo volgende fouten voor resources die Hallo WWW-verificatie-header en Bearer-schema in het antwoord Hallo gebruikt.

| HTTP-statuscode | Foutcode | Beschrijving | Clientactie |
| --- | --- | --- | --- |
| 400 |invalid_request |Hallo-aanvraag is niet grammaticaal correct. Bijvoorbeeld: er ontbreekt een parameter of dezelfde parameter met behulp van twee keer Hallo. |Hallo fout corrigeren en Hallo aanvraag opnieuw proberen. Dit type fout moet worden uitgevoerd tijdens de ontwikkeling en tests van de eerste worden gedetecteerd. |
| 401 |invalid_token |Hallo toegangstoken ontbreekt, is ongeldig of is ingetrokken. Hallo-waarde van de Hallo error_description parameter biedt aanvullende informatie. |Een nieuw token aanvragen van Hallo autorisatie-server. Als nieuw Hallo-token is mislukt, heeft een onverwachte fout opgetreden. Verzenden van een gebruiker fout bericht toohello en opnieuw proberen na willekeurige vertraging. |
| 403 |insufficient_scope |Hallo toegangstoken bevat geen Hallo imitatie machtigingen vereist tooaccess Hallo resource. |Verzend een nieuwe autorisatie aanvraag toohello autorisatie-eindpunt. Als antwoord Hallo bereikparameter hello bevat, gebruikt u de bereikwaarde Hallo in Hallo aanvraag toohello resource. |
| 403 |insufficient_access |Hallo-onderwerp van het Hallo-token heeft geen Hallo machtigingen die vereist tooaccess Hallo resource zijn. |Vragen Hallo gebruiker toouse een ander account of toorequest machtigingen toohello van de opgegeven bron. |

## Hallo-toegangstokens vernieuwen
Toegangstokens tijdelijke zijn en moeten worden vernieuwd nadat ze toegang krijgen tot bronnen toocontinue verlopen. Kunt u Hallo vernieuwen `access_token` door het indienen van een andere `POST` aanvragen toohello `/token` eindpunt, maar dit moment bieden Hallo `refresh_token` in plaats van Hallo `code`.

Vernieuwen van tokens hebben geen opgegeven levensduur. Hallo-levensduur van het vernieuwen van tokens zijn meestal relatief lange. Echter in sommige gevallen vernieuwen van tokens verlopen, worden ingetrokken of niet over voldoende bevoegdheden voor Hallo gewenst actie. Uw toepassing moet tooexpect en ingang fouten geretourneerd door Hallo uitgifte van tokens eindpunt goed.

Wanneer u een antwoord met een token fout vernieuwen ontvangt, de huidige vernieuwingstoken Hallo negeren en vraag een nieuwe autorisatiecode of toegangstoken. In het bijzonder wanneer met behulp van een vernieuwing token in Hallo Authorization Code Grant flow, als er een antwoord Hello `interaction_required` of `invalid_grant` foutcodes Hallo vernieuwingstoken negeren en vraag een nieuwe autorisatiecode.

Een voorbeeld aanvraag toohello **tenantspecifieke** eindpunt (u kunt ook Hallo **algemene** eindpunt) tooget een nieuw toegangstoken met behulp van een vernieuwingstoken uitziet:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Geslaagde reactie
Een geslaagde reactie token, ziet er als:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parameter | Beschrijving |
| --- | --- |
| token_type |Hallo type token. Hallo alleen ondersteunde waarde is **bearer**. |
| expires_in |Hallo resterende levensduur van token Hallo in seconden. Een typische waarde is 3600 (één uur). |
| expires_on |Hallo-datum en tijd waarop Hallo-token is verlopen. Hallo datum wordt weergegeven als het aantal seconden Hallo vanaf 1970-01-01T0:0:0Z UTC tot verlooptijd Hallo. |
| Resource |Hallo identificeert resource beveiligd, kan dat toegangstoken hello worden gebruikt tooaccess. |
| Bereik |Imitatie machtigingen verleend toohello native client-toepassing. Hallo standaardmachtiging **user_impersonation**. Hallo-eigenaar van de doelbron Hallo kunt alternatieve waarden registreren in Azure AD. |
| access_token |Hallo nieuw toegangstoken die is aangevraagd. |
| refresh_token |Een nieuwe OAuth 2.0-refresh_token die nieuwe toegangstokens gebruikte toorequest worden kunnen wanneer Hallo in dit antwoord is verlopen. |

### Foutbericht
Een voorbeeld-foutmelding kan uitzien:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Parameter | Beschrijving |
| --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een verificatiefout. |
| error_codes |Een lijst met foutcodes STS-specifieke die bij het diagnostische gegevens helpen. |
| tijdstempel |Hallo tijd waarin Hallo-fout is opgetreden. |
| trace_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens helpen. |
| correlation_id |Een unieke id voor Hallo-aanvraag die bij het diagnostische gegevens over de onderdelen helpen. |

Zie voor een beschrijving van Hallo-foutcodes en de aanbevolen clientactie Hallo [foutcodes voor token-eindpunt fouten](#error-codes-for-token-endpoint-errors).
