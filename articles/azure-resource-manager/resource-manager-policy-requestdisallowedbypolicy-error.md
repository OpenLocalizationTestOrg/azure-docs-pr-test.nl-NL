---
title: Fout bij het bronbeleid Azure aaaRequestDisallowedByPolicy | Microsoft Docs
description: Hallo oorzaak Hallo RequestDisallowedByPolicy fout beschrijft.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="e8536-103">Fout bij het bronbeleid Azure RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="e8536-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="e8536-104">Dit artikel wordt beschreven Hallo oorzaak van Hallo RequestDisallowedByPolicy fout, het bevat ook oplossing voor deze fout.</span><span class="sxs-lookup"><span data-stu-id="e8536-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="e8536-105">Symptoom</span><span class="sxs-lookup"><span data-stu-id="e8536-105">Symptom</span></span>

<span data-ttu-id="e8536-106">Wanneer u een actie tijdens de implementatie van toodo probeert, verschijnt er een **RequestDisallowedByPolicy** fout waardoor het Hallo-actie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8536-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="e8536-107">Hallo volgt een voorbeeld van Hallo-fout:</span><span class="sxs-lookup"><span data-stu-id="e8536-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="e8536-108">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e8536-108">Troubleshooting</span></span>

<span data-ttu-id="e8536-109">tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd Hallo na een Hallo methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e8536-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="e8536-110">Methode 1</span><span class="sxs-lookup"><span data-stu-id="e8536-110">Method 1</span></span>

<span data-ttu-id="e8536-111">In PowerShell bieden die beleids-id als Hallo **Id** parameter tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e8536-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="e8536-112">Methode 2</span><span class="sxs-lookup"><span data-stu-id="e8536-112">Method 2</span></span> 

<span data-ttu-id="e8536-113">Geef in de Azure CLI 2.0, Hallo-naam van de beleidsdefinitie Hallo:</span><span class="sxs-lookup"><span data-stu-id="e8536-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="e8536-114">Oplossing</span><span class="sxs-lookup"><span data-stu-id="e8536-114">Solution</span></span>

<span data-ttu-id="e8536-115">Voor beveiliging of naleving uw IT-afdeling kan resource beleid afdwingen dat verbiedt het openbare IP-adressen, Netwerkbeveiligingsgroepen, door de gebruiker gedefinieerde Routes of routetabellen maken.</span><span class="sxs-lookup"><span data-stu-id="e8536-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="e8536-116">In voorbeeld van Hallo foutbericht dat wordt beschreven in de sectie 'Symptomen' Hallo HALLO hallo-beleid heet **regionPolicyDefinition**, maar het zou kunnen verschillen.</span><span class="sxs-lookup"><span data-stu-id="e8536-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="e8536-117">tooresolve dit probleem werken met uw IT-afdeling tooreview Hallo bronbeleid en bepalen hoe tooperform Hallo aangevraagd in overeenstemming met deze beleidsregels in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="e8536-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="e8536-118">Zie voor meer informatie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8536-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="e8536-119">Overzicht van de resource-beleid</span><span class="sxs-lookup"><span data-stu-id="e8536-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="e8536-120">Algemene implementatie fouten RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="e8536-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


