---
title: Referenties van het certificaat in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven voor de registratie en het gebruik van referenties van het computercertificaat voor de verificatie van de toepassing
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="2a79a-103">Referenties van het computercertificaat voor de verificatie van de toepassing</span><span class="sxs-lookup"><span data-stu-id="2a79a-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="2a79a-104">Azure Active Directory kunt een toepassing een eigen referenties gebruiken voor verificatie, bijvoorbeeld in de OAuth 2.0-Client referenties Grant-stroom en de On-namens-stroom.</span><span class="sxs-lookup"><span data-stu-id="2a79a-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="2a79a-105">Een vorm van de referentie die kan worden gebruikt is een JSON Web Token(JWT) assertion ondertekend met een certificaat waartoe de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2a79a-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="2a79a-106">Indeling van de verklaring</span><span class="sxs-lookup"><span data-stu-id="2a79a-106">Format of the assertion</span></span>
<span data-ttu-id="2a79a-107">Als u wilt de verklaring compute, wilt u waarschijnlijk een van de vele [JSON Web Token](https://jwt.io/) bibliotheken in de taal van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="2a79a-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="2a79a-108">De informatie die door het token is:</span><span class="sxs-lookup"><span data-stu-id="2a79a-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="2a79a-109">Koptekst</span><span class="sxs-lookup"><span data-stu-id="2a79a-109">Header</span></span>

| <span data-ttu-id="2a79a-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="2a79a-110">Parameter</span></span> |  <span data-ttu-id="2a79a-111">Opmerking</span><span class="sxs-lookup"><span data-stu-id="2a79a-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="2a79a-112">Moet **RS256**</span><span class="sxs-lookup"><span data-stu-id="2a79a-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="2a79a-113">Moet **JWT**</span><span class="sxs-lookup"><span data-stu-id="2a79a-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="2a79a-114">Moet de vingerafdruk van het x.509-certificaat SHA-1</span><span class="sxs-lookup"><span data-stu-id="2a79a-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="2a79a-115">Claims (Payload)</span><span class="sxs-lookup"><span data-stu-id="2a79a-115">Claims (Payload)</span></span>

| <span data-ttu-id="2a79a-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="2a79a-116">Parameter</span></span> |  <span data-ttu-id="2a79a-117">Opmerking</span><span class="sxs-lookup"><span data-stu-id="2a79a-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="2a79a-118">: Doelgroep  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token **</span><span class="sxs-lookup"><span data-stu-id="2a79a-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="2a79a-119">Vervaldatum: de datum waarop het token verloopt.</span><span class="sxs-lookup"><span data-stu-id="2a79a-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="2a79a-120">De tijd wordt weergegeven als het aantal seconden vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat de geldigheid van het token is verlopen.</span><span class="sxs-lookup"><span data-stu-id="2a79a-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="2a79a-121">Uitgever: moet de client_id (toepassings-Id van de client-service)</span><span class="sxs-lookup"><span data-stu-id="2a79a-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="2a79a-122">GUID: de JWT-ID</span><span class="sxs-lookup"><span data-stu-id="2a79a-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="2a79a-123">Niet vooraf: de datum voor het token kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2a79a-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="2a79a-124">De tijd wordt weergegeven als het aantal seconden vanaf 1 januari 1970 (1970-01-01T0:0:0Z) UTC totdat de tijd die het token is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="2a79a-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="2a79a-125">Onderwerp:-als voor `iss`, moet de client_id (toepassings-Id van de client-service)</span><span class="sxs-lookup"><span data-stu-id="2a79a-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="2a79a-126">Handtekening</span><span class="sxs-lookup"><span data-stu-id="2a79a-126">Signature</span></span>
<span data-ttu-id="2a79a-127">De handtekening wordt berekend met het toepassen van het certificaat, zoals beschreven in de [JSON Web Token RFC7519 specificatie](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="2a79a-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="2a79a-128">Voorbeeld van een gedecodeerde JWT-verklaring</span><span class="sxs-lookup"><span data-stu-id="2a79a-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="2a79a-129">Voorbeeld van een gecodeerde JWT bewering</span><span class="sxs-lookup"><span data-stu-id="2a79a-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="2a79a-130">De volgende tekenreeks is een voorbeeld van gecodeerde verklaring.</span><span class="sxs-lookup"><span data-stu-id="2a79a-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="2a79a-131">Als u zorgvuldig bekijkt, ziet u drie secties gescheiden door punten (.).</span><span class="sxs-lookup"><span data-stu-id="2a79a-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="2a79a-132">De eerste sectie codeert de kop van de tweede de nettolading en de laatste is de handtekening berekend met de certificaten van de inhoud van de eerste twee secties.</span><span class="sxs-lookup"><span data-stu-id="2a79a-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="2a79a-133">Uw certificaat registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a79a-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="2a79a-134">De referentie certificaat koppelt u de clienttoepassing in Azure AD, moet u het toepassingsmanifest te bewerken.</span><span class="sxs-lookup"><span data-stu-id="2a79a-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="2a79a-135">De blokkering van een certificaat hebt, moet u berekenen:</span><span class="sxs-lookup"><span data-stu-id="2a79a-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="2a79a-136">`$base64Thumbprint`, namelijk het base64-codering van het certificaat-Hash</span><span class="sxs-lookup"><span data-stu-id="2a79a-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="2a79a-137">`$base64Value`, namelijk het base64-codering van de onbewerkte gegevens van certificaat</span><span class="sxs-lookup"><span data-stu-id="2a79a-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="2a79a-138">u moet ook een GUID voor het identificeren van de sleutel in het toepassingsmanifest bieden (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="2a79a-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="2a79a-139">In de Azure-app-registratie voor de clienttoepassing, open het toepassingsmanifest en vervang de *keyCredentials* eigenschap met de nieuwe certificaatinformatie van een met het volgende schema:</span><span class="sxs-lookup"><span data-stu-id="2a79a-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="2a79a-140">De wijzigingen opslaan in het toepassingsmanifest en uploaden naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a79a-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="2a79a-141">De eigenschap keyCredentials heeft meerdere waarden, zodat u meerdere certificaten voor uitgebreidere Sleutelbeheer kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="2a79a-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
