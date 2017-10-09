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
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="5424d-103">Referenties van het computercertificaat voor de verificatie van de toepassing</span><span class="sxs-lookup"><span data-stu-id="5424d-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="5424d-104">Azure Active Directory biedt een toouse toepassing eigen referenties voor verificatie, bijvoorbeeld in Hallo OAuth 2.0-Client referenties Grant stroom en Hallo op namens-stroom.</span><span class="sxs-lookup"><span data-stu-id="5424d-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="5424d-105">Een vorm van de referentie die kan worden gebruikt is een JSON Web Token(JWT) assertion ondertekend met een toepassing hello-certificaat.</span><span class="sxs-lookup"><span data-stu-id="5424d-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="5424d-106">Indeling van Hallo verklaring</span><span class="sxs-lookup"><span data-stu-id="5424d-106">Format of hello assertion</span></span>
<span data-ttu-id="5424d-107">toocompute Hallo verklaring, wilt u waarschijnlijk toouse een Hallo veel [JSON Web Token](https://jwt.io/) bibliotheken in Hallo taal van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="5424d-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="5424d-108">Hallo-informatie die door Hallo-token is:</span><span class="sxs-lookup"><span data-stu-id="5424d-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="5424d-109">Koptekst</span><span class="sxs-lookup"><span data-stu-id="5424d-109">Header</span></span>

| <span data-ttu-id="5424d-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="5424d-110">Parameter</span></span> |  <span data-ttu-id="5424d-111">Opmerking</span><span class="sxs-lookup"><span data-stu-id="5424d-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="5424d-112">Moet **RS256**</span><span class="sxs-lookup"><span data-stu-id="5424d-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="5424d-113">Moet **JWT**</span><span class="sxs-lookup"><span data-stu-id="5424d-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="5424d-114">Hallo x.509-certificaat SHA-1-vingerafdruk moet worden</span><span class="sxs-lookup"><span data-stu-id="5424d-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="5424d-115">Claims (Payload)</span><span class="sxs-lookup"><span data-stu-id="5424d-115">Claims (Payload)</span></span>

| <span data-ttu-id="5424d-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="5424d-116">Parameter</span></span> |  <span data-ttu-id="5424d-117">Opmerking</span><span class="sxs-lookup"><span data-stu-id="5424d-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="5424d-118">: Doelgroep  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token **</span><span class="sxs-lookup"><span data-stu-id="5424d-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="5424d-119">Vervaldatum: Hallo datum wanneer Hallo-token is verlopen.</span><span class="sxs-lookup"><span data-stu-id="5424d-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="5424d-120">Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo Hallo token geldigheidsduur is verstreken.</span><span class="sxs-lookup"><span data-stu-id="5424d-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="5424d-121">Uitgever: moet Hallo client_id (toepassings-Id van de clientservice Hallo)</span><span class="sxs-lookup"><span data-stu-id="5424d-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="5424d-122">GUID: Hallo JWT-ID</span><span class="sxs-lookup"><span data-stu-id="5424d-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="5424d-123">Niet vooraf: Hallo datum voordat welke Hallo token kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5424d-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="5424d-124">Hallo tijd wordt weergegeven als het aantal seconden Hallo vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat Hallo tijd Hallo token is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="5424d-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="5424d-125">Onderwerp:-als voor `iss`, moet Hallo client_id (toepassings-Id van de clientservice Hallo)</span><span class="sxs-lookup"><span data-stu-id="5424d-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="5424d-126">Handtekening</span><span class="sxs-lookup"><span data-stu-id="5424d-126">Signature</span></span>
<span data-ttu-id="5424d-127">Hallo-handtekening wordt berekend Hallo certificaat toepassen, zoals beschreven in Hallo [JSON Web Token RFC7519 specificatie](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="5424d-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="5424d-128">Voorbeeld van een gedecodeerde JWT-verklaring</span><span class="sxs-lookup"><span data-stu-id="5424d-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="5424d-129">Voorbeeld van een gecodeerde JWT bewering</span><span class="sxs-lookup"><span data-stu-id="5424d-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="5424d-130">Hallo volgende tekenreeks is een voorbeeld van gecodeerde verklaring.</span><span class="sxs-lookup"><span data-stu-id="5424d-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="5424d-131">Als u zorgvuldig bekijkt, ziet u drie secties gescheiden door punten (.).</span><span class="sxs-lookup"><span data-stu-id="5424d-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="5424d-132">de eerste sectie Hallo Hallo-kop, Hallo tweede Hallo nettolading codeert en Hallo is laatste Hallo-handtekening berekend met Hallo certificaten van de inhoud van de eerste twee secties Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5424d-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="5424d-133">Uw certificaat registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="5424d-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="5424d-134">tooassociate hello certificaat-referentie met de clienttoepassing Hallo in Azure AD, moet u tooedit Hallo-toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="5424d-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="5424d-135">De blokkering van een certificaat hebt, moet u toocompute:</span><span class="sxs-lookup"><span data-stu-id="5424d-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="5424d-136">`$base64Thumbprint`, die is Hallo base64-codering van Hallo certificaat-Hash</span><span class="sxs-lookup"><span data-stu-id="5424d-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="5424d-137">`$base64Value`, die is Hallo base64-codering van Hallo onbewerkte gegevens van certificaat</span><span class="sxs-lookup"><span data-stu-id="5424d-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="5424d-138">u moet ook een GUID tooidentify Hallo-sleutel in het toepassingsmanifest Hallo tooprovide (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="5424d-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="5424d-139">Open in Azure app-registratie voor de clienttoepassing Hallo Hallo, Hallo toepassingsmanifest en vervang Hallo *keyCredentials* eigenschap met uw nieuwe certificaatgegevens met Hallo schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="5424d-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="5424d-140">Hallo bewerkingen toohello toepassingsmanifest opslaan en tooAzure AD uploaden.</span><span class="sxs-lookup"><span data-stu-id="5424d-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="5424d-141">Hallo keyCredentials eigenschap heeft meerdere waarden, zodat u meerdere certificaten voor uitgebreidere Sleutelbeheer kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="5424d-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
