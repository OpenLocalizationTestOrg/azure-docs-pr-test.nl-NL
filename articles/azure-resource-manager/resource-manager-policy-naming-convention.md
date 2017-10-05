---
title: Azure-resource-beleid voor naamconventies | Microsoft Docs
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
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="6dea2-103">Resource-beleid toepassen op namen en tekst</span><span class="sxs-lookup"><span data-stu-id="6dea2-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="6dea2-104">Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u kunt toepassen om vast te stellen conventies naming en tekst.</span><span class="sxs-lookup"><span data-stu-id="6dea2-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="6dea2-105">Deze beleidsregels consistentie voor resourcenamen en labelwaarden.</span><span class="sxs-lookup"><span data-stu-id="6dea2-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="6dea2-106">Stel naamconventie met jokerteken</span><span class="sxs-lookup"><span data-stu-id="6dea2-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="6dea2-107">Het volgende voorbeeld ziet u het gebruik van jokertekens, die wordt ondersteund door de **zoals** voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="6dea2-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="6dea2-108">De voorwaarde aangeeft dat als de naam komt overeen met de genoemde patroon (namePrefix\*nameSuffix) klikt u vervolgens de aanvraag weigeren:</span><span class="sxs-lookup"><span data-stu-id="6dea2-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="6dea2-109">Stel de naamgevingsconventie met patroon</span><span class="sxs-lookup"><span data-stu-id="6dea2-109">Set naming convention with pattern</span></span>

<span data-ttu-id="6dea2-110">Resourcenamen overeenkomen met een patroon gebruikt u de voorwaarde van de overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="6dea2-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="6dea2-111">Het volgende voorbeeld vereist namen beginnen met `contoso` en zes aanvullende letters bevatten:</span><span class="sxs-lookup"><span data-stu-id="6dea2-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="6dea2-112">Patroon voor de labelwaarde datum instellen</span><span class="sxs-lookup"><span data-stu-id="6dea2-112">Set date pattern for tag value</span></span>

<span data-ttu-id="6dea2-113">Als u wilt een patroon van de datum van het gebruik van twee cijfers, streepjes, drie letters, streepjes en vier cijfers vereisen:</span><span class="sxs-lookup"><span data-stu-id="6dea2-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6dea2-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6dea2-114">Next steps</span></span>
* <span data-ttu-id="6dea2-115">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden), moet u de beleidsdefinitie maken en toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="6dea2-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="6dea2-116">Het bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="6dea2-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="6dea2-117">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6dea2-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6dea2-118">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6dea2-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="6dea2-119">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6dea2-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

