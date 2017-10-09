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
# <a name="apply-resource-policies-toonetwork-resources"></a>Resource beleid toonetwork resources toepassen
In dit artikel ziet u een voorbeeld [bronbeleid](resource-manager-policy.md) kunt u de virtuele netwerkgateways tooAzure toepassen. Dit beleid zorgt ervoor dat de consistentie van gateways geïmplementeerd in uw organisatie. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>Toegestane virtuele netwerkgateway SKU definiëren

Hallo na beleid beperkt welke SKU's voor virtuele netwerkgateways kunnen worden geïmplementeerd:

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

## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik. Hallo bereik mag een abonnement, resourcegroep of resource. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md). 
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

