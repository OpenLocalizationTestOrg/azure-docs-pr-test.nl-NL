---
title: bronbeleid aaaAzure voor netwerkbronnen | Microsoft Docs
description: Beschrijving van het beleid voor het beheren van de implementatie van netwerkbronnen hello Azure Resource Manager.
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
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="57d7e-103">Resource beleid toonetwork resources toepassen</span><span class="sxs-lookup"><span data-stu-id="57d7e-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="57d7e-104">In dit artikel ziet u een voorbeeld [bronbeleid](resource-manager-policy.md) kunt u de virtuele netwerkgateways tooAzure toepassen.</span><span class="sxs-lookup"><span data-stu-id="57d7e-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="57d7e-105">Dit beleid zorgt ervoor dat de consistentie van gateways geïmplementeerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="57d7e-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="57d7e-106">Toegestane virtuele netwerkgateway SKU definiëren</span><span class="sxs-lookup"><span data-stu-id="57d7e-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="57d7e-107">Hallo na beleid beperkt welke SKU's voor virtuele netwerkgateways kunnen worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="57d7e-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="57d7e-108">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57d7e-108">Next steps</span></span>
* <span data-ttu-id="57d7e-109">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="57d7e-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="57d7e-110">Hallo bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="57d7e-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="57d7e-111">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57d7e-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="57d7e-112">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="57d7e-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="57d7e-113">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="57d7e-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

