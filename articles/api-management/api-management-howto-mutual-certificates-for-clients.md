---
title: Met behulp van client API's beveiligd tegen certificaatverificatie in API Management - Azure API Management | Microsoft Docs
description: Meer informatie over het beveiligen van toegang tot API's met behulp van clientcertificaten
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
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="b9e49-103">Het beveiligen van API's met behulp van client certificaatverificatie in API Management</span><span class="sxs-lookup"><span data-stu-id="b9e49-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="b9e49-104">API Management biedt de mogelijkheid om toegang tot API's (dat wil zeggen, de client naar API Management) te beveiligen met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="b9e49-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="b9e49-105">Op dit moment kunt u de vingerafdruk van een certificaat met een waarde van de gewenste controleren.</span><span class="sxs-lookup"><span data-stu-id="b9e49-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="b9e49-106">U kunt ook de vingerafdruk op basis van bestaande certificaten geüpload naar de API Management controleren.</span><span class="sxs-lookup"><span data-stu-id="b9e49-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="b9e49-107">Zie voor meer informatie over het beveiligen van toegang tot de back-end-service van een API met behulp van clientcertificaten (dat wil zeggen, API Management aan back-end) [het beveiligen van back-end-services met behulp van client verificatie via certificaat](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="b9e49-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="b9e49-108">Controleren of de vervaldatum</span><span class="sxs-lookup"><span data-stu-id="b9e49-108">Checking the expiration date</span></span>

<span data-ttu-id="b9e49-109">Onderstaande beleidsregels kunnen worden geconfigureerd om te controleren of het certificaat is verlopen:</span><span class="sxs-lookup"><span data-stu-id="b9e49-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="b9e49-110">Controle van de verlener en onderwerp</span><span class="sxs-lookup"><span data-stu-id="b9e49-110">Checking the issuer and subject</span></span>

<span data-ttu-id="b9e49-111">Onderstaande beleidsregels kunnen worden geconfigureerd om te controleren van de verlener en onderwerp van een certificaat:</span><span class="sxs-lookup"><span data-stu-id="b9e49-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="b9e49-112">Controleren of de vingerafdruk</span><span class="sxs-lookup"><span data-stu-id="b9e49-112">Checking the thumbprint</span></span>

<span data-ttu-id="b9e49-113">Onderstaande beleidsregels kunnen worden geconfigureerd om te controleren van de vingerafdruk van een certificaat:</span><span class="sxs-lookup"><span data-stu-id="b9e49-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="b9e49-114">Controleren of een vingerafdruk tegen certificaten geüpload naar de API Management</span><span class="sxs-lookup"><span data-stu-id="b9e49-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="b9e49-115">Het volgende voorbeeld ziet u hoe u controleert de vingerafdruk van een clientcertificaat tegen certificaten geüpload naar de API Management:</span><span class="sxs-lookup"><span data-stu-id="b9e49-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="b9e49-116">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="b9e49-116">Next step</span></span>

*  [<span data-ttu-id="b9e49-117">Het beveiligen van back-end-services met behulp van client verificatie via certificaat</span><span class="sxs-lookup"><span data-stu-id="b9e49-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="b9e49-118">Het uploaden van certificaten</span><span class="sxs-lookup"><span data-stu-id="b9e49-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

