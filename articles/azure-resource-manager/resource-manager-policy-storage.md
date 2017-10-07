---
title: bronbeleid aaaAzure voor opslagaccounts | Microsoft Docs
description: Beschrijving van het Azure Resource Manager-beleid voor het beheren van Hallo-implementatie van de storage-accounts.
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
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>Resourceaccounts beleid toostorage toepassen
Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u tooAzure storage-accounts kunt toepassen. Deze beleidsregels consistentie voor opslagaccounts Hallo geïmplementeerd in uw organisatie. 

## <a name="define-permitted-storage-account-types"></a>Account voor toegestane opslagtypen definiëren

Hallo volgende beleid beperkt die [opslagaccounttypen](../storage/common/storage-redundancy.md) kan worden geïmplementeerd:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
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

Een beleidsregel vergelijkbaar met een parameter voor het accepteren van Hallo toegestaan SKU's is beschikbaar als een ingebouwde beleidsdefinitie. ingebouwde beleid Hallo Hallo resource-ID heeft `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Toegestane toegangslaag definiëren

Hallo volgende beleid bevat Hallo soort [toegangslaag](../storage/blobs/storage-blob-storage-tiers.md) die kan worden opgegeven voor de storage-accounts:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>Zorg ervoor dat versleuteling is ingeschakeld

Hallo volgende beleid vereist dat alle storage accounts tooenable [service opslagversleuteling](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Deze beleidsregel is ook beschikbaar als de beleidsdefinitie van een ingebouwde met de Hallo resource ID `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik. Hallo bereik mag een abonnement, resourcegroep of resource. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md). 
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

