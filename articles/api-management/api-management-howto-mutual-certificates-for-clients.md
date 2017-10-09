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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="10b5b-103">Hoe toosecure-API's met behulp van client certificaat gebaseerde verificatie in API Management</span><span class="sxs-lookup"><span data-stu-id="10b5b-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="10b5b-104">API Management biedt Hallo mogelijkheid toosecure toegang tooAPIs (dat wil zeggen, client tooAPI Management) met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="10b5b-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="10b5b-105">U kunt op dit moment Hallo vingerafdruk van een certificaat met een waarde van de gewenste controleren.</span><span class="sxs-lookup"><span data-stu-id="10b5b-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="10b5b-106">U kunt ook controleren Hallo vingerafdruk op basis van bestaande certificaten geüpload tooAPI Management.</span><span class="sxs-lookup"><span data-stu-id="10b5b-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="10b5b-107">Zie voor meer informatie over het beveiligen van access-service toohello back-end van een API met behulp van clientcertificaten (dat wil zeggen, API Management tooback-end) [hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="10b5b-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="10b5b-108">Hallo-vervaldatum controleren</span><span class="sxs-lookup"><span data-stu-id="10b5b-108">Checking hello expiration date</span></span>

<span data-ttu-id="10b5b-109">Hieronder beleid kan geconfigureerde toocheck zijn als het Hallo-certificaat is verlopen:</span><span class="sxs-lookup"><span data-stu-id="10b5b-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="10b5b-110">Hallo verlener en onderwerp controleren</span><span class="sxs-lookup"><span data-stu-id="10b5b-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="10b5b-111">Hieronder beleid kan worden geconfigureerd toocheck Hallo verlener en onderwerp van een certificaat:</span><span class="sxs-lookup"><span data-stu-id="10b5b-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="10b5b-112">Hallo vingerafdruk controleren</span><span class="sxs-lookup"><span data-stu-id="10b5b-112">Checking hello thumbprint</span></span>

<span data-ttu-id="10b5b-113">Hieronder beleid kan worden geconfigureerd toocheck Hallo vingerafdruk van een certificaat:</span><span class="sxs-lookup"><span data-stu-id="10b5b-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="10b5b-114">Controleren of een vingerafdruk tegen certificaten geüpload tooAPI Management</span><span class="sxs-lookup"><span data-stu-id="10b5b-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="10b5b-115">Hallo volgende voorbeeld laat zien hoe toocheck Hallo vingerafdruk van een clientcertificaat tegen certificaten tooAPI Management geüpload:</span><span class="sxs-lookup"><span data-stu-id="10b5b-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="10b5b-116">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="10b5b-116">Next step</span></span>

*  [<span data-ttu-id="10b5b-117">Hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie</span><span class="sxs-lookup"><span data-stu-id="10b5b-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="10b5b-118">Hoe tooupload certificaten</span><span class="sxs-lookup"><span data-stu-id="10b5b-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

