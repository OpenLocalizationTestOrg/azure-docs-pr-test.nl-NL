---
title: AD-Service tooService Auth aaaAzure met OAuth2.0 | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse HTTP-berichten tooimplement tooservice-verificatie met behulp van Hallo OAuth2.0 grant clientreferentiestroom service.
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Service tooservice aanroepen met clientreferenties (gedeelde geheim of certificaat)
Hallo OAuth 2.0-Client referenties Grant stromen is toegestaan voor een webservice (*vertrouwelijke client*) toouse zijn eigen referenties in plaats van het imiteren van een gebruiker, tooauthenticate bij het aanroepen van een andere web-service. In dit scenario is Hallo-client meestal een middelste laag webservice, een daemon-service of de website. Voor een hoger niveau van zekerheid kan Azure AD ook Hallo service toouse het aanroepen van een certificaat (in plaats van een gedeeld geheim) als referentie.

## Clientreferenties verlenen stroomdiagram
Hallo volgende diagram wordt uitgelegd hoe de clientreferenties Hallo verlenen stroom werkt in Azure Active Directory (Azure AD).

![OAuth2.0 Grant Clientreferentiestroom](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. Hallo-clienttoepassing verifieert toohello Azure AD uitgifte van tokens eindpunt en een toegangstoken aanvragen.
2. Hello Azure AD uitgifte van tokens endpoint problemen Hallo toegangstoken.
3. Hallo toegangstoken is gebruikte tooauthenticate toohello beveiligde resource.
4. Gegevens uit beveiligde resource Hallo geretourneerd toohello-webtoepassing.

## Hallo-Services in Azure AD registreren
Zowel Hallo service aanroepen en Hallo ontvangst van de service in Azure Active Directory (Azure AD) registreren. Zie voor gedetailleerde instructies [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).

## Aanvragen van een toegangstoken
een toegangstoken toorequest gebruiken een HTTP POST toohello tenantspecifieke Azure AD-eindpunt.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Service-naar-service toegang tokenaanvraag
Er zijn twee gevallen, afhankelijk van of de client-toepassing hello toobe beveiligd door een gedeeld geheim of een certificaat kiest.

### Het eerste aanvraagnummer: aanvraag voor toegang tot token met een gedeeld geheim
Wanneer u een gedeeld geheim, bevat een tokenaanvraag voor service-naar-service toegang Hallo volgende parameters:

| Parameter |  | Beschrijving |
| --- | --- | --- |
| grant_type |Vereist |Hiermee geeft u op Hallo aangevraagd type verlenen. In een stroom Client referenties Grant Hallo-waarde moet **client_credentials**. |
| client_id |Vereist |Hiermee geeft u hello Azure AD-client-id Hallo webservice aanroepen. toofind hello aanroepen van de client-ID van de toepassing, in Hallo [Azure-portal](https://portal.azure.com), klikt u op **Active Directory**, directory overschakelen, klikt u op Hallo-toepassing. Hallo client_id is Hallo *toepassings-ID* |
| client_secret |Vereist |Geef een sleutel die is geregistreerd voor Hallo aanroepen van web service of -daemon-toepassing in Azure AD. toocreate een sleutel in hello Azure-portal, klikt u op **Active Directory**, directory overschakelen, klikt u op de toepassing hello, klik op **instellingen**, klikt u op **sleutels**, en een sleutel toevoegen.|
| Resource |Vereist |Voer Hallo App ID URI Hallo web-service ontvangen. toofind hello App ID URI, in hello Azure-portal, klikt u op **Active Directory**, directory overschakelen, klikt u op Hallo-servicetoepassing en klik vervolgens op **instellingen** en **eigenschappen** |

#### Voorbeeld
Hallo volgende HTTP POST-aanvragen een toegangstoken voor Hallo https://service.contoso.com/-webservice. Hallo `client_id` Hallo webservice identificeert die Hallo toegangstoken aanvragen.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Tweede geval: aanvraag voor toegang tot token met een certificaat
Een service-naar-service toegang tokenaanvraag met een certificaat bevat Hallo volgende parameters:

| Parameter |  | Beschrijving |
| --- | --- | --- |
| grant_type |Vereist |Hiermee geeft u op Hallo antwoordtype aangevraagd. In een stroom Client referenties Grant Hallo-waarde moet **client_credentials**. |
| client_id |Vereist |Hiermee geeft u hello Azure AD-client-id Hallo webservice aanroepen. toofind hello aanroepen van de client-ID van de toepassing, in Hallo [Azure-portal](https://portal.azure.com), klikt u op **Active Directory**, directory overschakelen, klikt u op Hallo-toepassing. Hallo client_id is Hallo *toepassings-ID* |
| client_assertion_type |Vereist |Hallo-waarde moet liggen`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Vereist | Een (een JSON Web Token) bewering die u toocreate nodig hebt en ondertekenen met het Hallo-certificaat geregistreerd als de referenties voor uw toepassing. Meer informatie over [referenties van het certificaat](active-directory-certificate-credentials.md) toolearn hoe tooregister uw certificaat en het Hallo-indeling van Hallo verklaring.|
| Resource | Vereist |Voer Hallo App ID URI Hallo web-service ontvangen. toofind hello App ID URI, in hello Azure-portal, klikt u op **Active Directory**, klikt u op Hallo directory, klikt u op Hallo-toepassing en klik vervolgens op **configureren**. |

Hallo-parameters zijn bijna Hallo dezelfde net als bij Hallo Hallo aanvraag door een gedeeld geheim, behalve dat Hallo client_secret parameter wordt vervangen door twee parameters: een client_assertion_type en client_assertion.

#### Voorbeeld
Hallo na HTTP POST-aanvragen een toegangstoken voor Hallo https://service.contoso.com/ webservice met een certificaat. Hallo `client_id` Hallo webservice identificeert die Hallo toegangstoken aanvragen.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Service-naar-Service toegang Token antwoord

Een geslaagde reactie bevat een JSON OAuth 2.0-antwoord Hello volgende parameters:

| Parameter | Beschrijving |
| --- | --- |
| access_token |Hallo aangevraagde toegangstoken. Hallo webservice aanroepen kunt dit token tooauthenticate toohello web-service ontvangen. |
| token_type |Hiermee wordt aangegeven Hallo type token waarde. Hallo alleen type dat ondersteunt Azure AD **Bearer**. Zie voor meer informatie over bearer-tokens Hallo [OAuth 2.0 autorisatie Framework: Bearer-Token gebruik (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Hoe lang Hallo toegangstoken is ongeldig (in seconden). |
| expires_on |Hallo tijd wanneer Hallo toegangstoken is verlopen. Hallo datum wordt weergegeven als het aantal seconden Hallo vanaf 1970-01-01T0:0:0Z UTC tot verlooptijd Hallo. Deze waarde is gebruikte toodetermine Hallo levensduur van tokens in de cache. |
| not_before |Hallo-tijd van welke Hallo toegangstoken gebruikt wordt. Hallo datum wordt weergegeven als het aantal seconden Hallo vanaf 1970-01-01T0:0:0Z UTC totdat de tijd van geldigheid voor Hallo-token.|
| Resource |Hallo App ID URI Hallo web-service ontvangen. |

#### Voorbeeld van antwoord
Hallo volgende voorbeeld ziet u een geslaagd antwoord tooa aanvraag voor een access token tooa-webservice.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Zie ook
* [OAuth 2.0 in Azure AD](active-directory-protocols-oauth-code.md)
* [Voorbeeld in C# van Hallo service tooservice aanroep met een gedeeld geheim](https://github.com/Azure-Samples/active-directory-dotnet-daemon) en [voorbeeld in C# van Hallo service tooservice aanroep met een certificaat](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
