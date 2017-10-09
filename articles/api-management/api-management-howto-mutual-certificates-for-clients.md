---
title: aaaSecure API's met behulp van verificatie van clientcertificaten in API Management - Azure API Management | Microsoft Docs
description: Meer informatie over hoe toosecure toegang krijgen tot tooAPIs met behulp van clientcertificaten
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Hoe toosecure-API's met behulp van client certificaat gebaseerde verificatie in API Management

API Management biedt Hallo mogelijkheid toosecure toegang tooAPIs (dat wil zeggen, client tooAPI Management) met behulp van clientcertificaten. U kunt op dit moment Hallo vingerafdruk van een certificaat met een waarde van de gewenste controleren. U kunt ook controleren Hallo vingerafdruk op basis van bestaande certificaten geüpload tooAPI Management.  

Zie voor meer informatie over het beveiligen van access-service toohello back-end van een API met behulp van clientcertificaten (dat wil zeggen, API Management tooback-end) [hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Hallo-vervaldatum controleren

Hieronder beleid kan geconfigureerde toocheck zijn als het Hallo-certificaat is verlopen:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Hallo verlener en onderwerp controleren

Hieronder beleid kan worden geconfigureerd toocheck Hallo verlener en onderwerp van een certificaat:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Hallo vingerafdruk controleren

Hieronder beleid kan worden geconfigureerd toocheck Hallo vingerafdruk van een certificaat:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>Controleren of een vingerafdruk tegen certificaten geüpload tooAPI Management

Hallo volgende voorbeeld laat zien hoe toocheck Hallo vingerafdruk van een clientcertificaat tegen certificaten tooAPI Management geüpload: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Volgende stap

*  [Hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Hoe tooupload certificaten](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

