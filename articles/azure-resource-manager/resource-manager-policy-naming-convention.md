---
title: bronbeleid aaaAzure voor naamconventies | Microsoft Docs
description: Beschrijving van het Azure Resource Manager-beleid voor de naamgeving van de resource.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="55ddc-103">Resource-beleid toepassen op namen en tekst</span><span class="sxs-lookup"><span data-stu-id="55ddc-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="55ddc-104">Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u tooestablish naming en tekst conventies kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="55ddc-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="55ddc-105">Deze beleidsregels consistentie voor resourcenamen en labelwaarden.</span><span class="sxs-lookup"><span data-stu-id="55ddc-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="55ddc-106">Stel naamconventie met jokerteken</span><span class="sxs-lookup"><span data-stu-id="55ddc-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="55ddc-107">Hallo volgende voorbeeld ziet u Hallo gebruik van jokertekens, die wordt ondersteund door Hallo **zoals** voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="55ddc-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="55ddc-108">Hallo voorwaarde aangegeven dat als hello naam komt overeen met de genoemde patroon hello (namePrefix\*nameSuffix) vervolgens weigeren Hallo-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="55ddc-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="55ddc-109">Stel de naamgevingsconventie met patroon</span><span class="sxs-lookup"><span data-stu-id="55ddc-109">Set naming convention with pattern</span></span>

<span data-ttu-id="55ddc-110">toospecify of resourcenamen overeenkomen met een patroon, gebruik Hallo overeenkomen met de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="55ddc-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="55ddc-111">Hallo volgende voorbeeld vereist dat namen toostart met `contoso` en zes aanvullende letters bevatten:</span><span class="sxs-lookup"><span data-stu-id="55ddc-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="55ddc-112">Patroon voor de labelwaarde datum instellen</span><span class="sxs-lookup"><span data-stu-id="55ddc-112">Set date pattern for tag value</span></span>

<span data-ttu-id="55ddc-113">een datum-patroon van twee cijfers, streepjes, drie letters, streepjes en vier cijfers gebruik toorequire:</span><span class="sxs-lookup"><span data-stu-id="55ddc-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="55ddc-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55ddc-114">Next steps</span></span>
* <span data-ttu-id="55ddc-115">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="55ddc-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="55ddc-116">Hallo bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="55ddc-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="55ddc-117">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55ddc-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="55ddc-118">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="55ddc-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="55ddc-119">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="55ddc-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

