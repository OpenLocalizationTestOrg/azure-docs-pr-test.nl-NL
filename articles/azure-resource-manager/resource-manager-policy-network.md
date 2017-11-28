---
title: Azure-resource beleidsregels voor netwerkbronnen | Microsoft Docs
description: Beschrijving van het Azure Resource Manager-beleid voor het beheren van de implementatie van netwerkbronnen.
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="4bc02-103">Resource-beleid toepassen op netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="4bc02-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="4bc02-104">In dit artikel ziet u een voorbeeld [bronbeleid](resource-manager-policy.md) u kunt toepassen op virtuele Azure-netwerkgateways.</span><span class="sxs-lookup"><span data-stu-id="4bc02-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="4bc02-105">Dit beleid zorgt ervoor dat de consistentie van gateways geïmplementeerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="4bc02-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="4bc02-106">Toegestane virtuele netwerkgateway SKU definiëren</span><span class="sxs-lookup"><span data-stu-id="4bc02-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="4bc02-107">Het volgende beleid beperkt welke SKU's voor virtuele netwerkgateways kunnen worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="4bc02-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="4bc02-108">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4bc02-108">Next steps</span></span>
* <span data-ttu-id="4bc02-109">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden), moet u de beleidsdefinitie maken en toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="4bc02-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="4bc02-110">Het bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="4bc02-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4bc02-111">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4bc02-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="4bc02-112">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="4bc02-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="4bc02-113">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4bc02-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

