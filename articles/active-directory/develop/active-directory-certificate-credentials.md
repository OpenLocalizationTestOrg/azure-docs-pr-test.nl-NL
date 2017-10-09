---
title: aaaCertificate referenties in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven Hallo registratie en het gebruik van referenties van het computercertificaat voor de verificatie van de toepassing
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>Referenties van het computercertificaat voor de verificatie van de toepassing

Azure Active Directory biedt een toouse toepassing eigen referenties voor verificatie, bijvoorbeeld in Hallo OAuth 2.0-Client referenties Grant stroom en Hallo op namens-stroom.
Een vorm van de referentie die kan worden gebruikt is een JSON Web Token(JWT) assertion ondertekend met een toepassing hello-certificaat.

## <a name="format-of-hello-assertion"></a>Indeling van Hallo verklaring
toocompute Hallo verklaring, wilt u waarschijnlijk toouse een Hallo veel [JSON Web Token](https://jwt.io/) bibliotheken in Hallo taal van uw keuze. Hallo-informatie die door Hallo-token is:

#### <a name="header"></a>Koptekst

| Parameter |  Opmerking |
| --- | --- | --- |
| `alg` | Moet **RS256** |
| `typ` | Moet **JWT** |
| `x5t` | Hallo x.509-certificaat SHA-1-vingerafdruk moet worden |

#### <a name="claims-payload"></a>Claims (Payload)

| Parameter |  Opmerking |
| --- | --- | --- |
| `aud` | : Doelgroep  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token ** |
| `exp` | Vervaldatum: Hallo datum wanneer Hallo-token is verlopen. Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo Hallo token geldigheidsduur is verstreken.|
| `iss` | Uitgever: moet Hallo client_id (toepassings-Id van de clientservice Hallo) |
| `jti` | GUID: Hallo JWT-ID |
| `nbf` | Niet vooraf: Hallo datum voordat welke Hallo token kan niet worden gebruikt. Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo tijd Hallo token is uitgegeven. |
| `sub` | Onderwerp:-als voor `iss`, moet Hallo client_id (toepassings-Id van de clientservice Hallo) |

#### <a name="signature"></a>Handtekening
Hallo-handtekening wordt berekend Hallo certificaat toepassen, zoals beschreven in Hallo [JSON Web Token RFC7519 specificatie](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Voorbeeld van een gedecodeerde JWT-verklaring
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>Voorbeeld van een gecodeerde JWT bewering
Hallo volgende tekenreeks is een voorbeeld van gecodeerde verklaring. Als u zorgvuldig bekijkt, ziet u drie secties gescheiden door punten (.).
de eerste sectie Hallo Hallo-kop, Hallo tweede Hallo nettolading codeert en Hallo is laatste Hallo-handtekening berekend met Hallo certificaten van de inhoud van de eerste twee secties Hallo Hallo.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Uw certificaat registreren met Azure AD
tooassociate hello certificaat-referentie met de clienttoepassing Hallo in Azure AD, moet u tooedit Hallo-toepassingsmanifest.
De blokkering van een certificaat hebt, moet u toocompute:
- `$base64Thumbprint`, die is Hallo base64-codering van Hallo certificaat-Hash
- `$base64Value`, die is Hallo base64-codering van Hallo onbewerkte gegevens van certificaat

u moet ook een GUID tooidentify Hallo-sleutel in het toepassingsmanifest Hallo tooprovide (`$keyId`)

Open in Azure app-registratie voor de clienttoepassing Hallo Hallo, Hallo toepassingsmanifest en vervang Hallo *keyCredentials* eigenschap met uw nieuwe certificaatgegevens met Hallo schema te volgen:
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Hallo bewerkingen toohello toepassingsmanifest opslaan en tooAzure AD uploaden. Hallo keyCredentials eigenschap heeft meerdere waarden, zodat u meerdere certificaten voor uitgebreidere Sleutelbeheer kan uploaden.
