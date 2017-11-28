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
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="79edf-103">Resourceaccounts beleid toostorage toepassen</span><span class="sxs-lookup"><span data-stu-id="79edf-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="79edf-104">Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u tooAzure storage-accounts kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="79edf-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="79edf-105">Deze beleidsregels consistentie voor opslagaccounts Hallo geïmplementeerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="79edf-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="79edf-106">Account voor toegestane opslagtypen definiëren</span><span class="sxs-lookup"><span data-stu-id="79edf-106">Define permitted storage account types</span></span>

<span data-ttu-id="79edf-107">Hallo volgende beleid beperkt die [opslagaccounttypen](../storage/common/storage-redundancy.md) kan worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="79edf-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="79edf-108">Een beleidsregel vergelijkbaar met een parameter voor het accepteren van Hallo toegestaan SKU's is beschikbaar als een ingebouwde beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="79edf-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="79edf-109">ingebouwde beleid Hallo Hallo resource-ID heeft `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="79edf-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="79edf-110">Toegestane toegangslaag definiëren</span><span class="sxs-lookup"><span data-stu-id="79edf-110">Define permitted access tier</span></span>

<span data-ttu-id="79edf-111">Hallo volgende beleid bevat Hallo soort [toegangslaag](../storage/blobs/storage-blob-storage-tiers.md) die kan worden opgegeven voor de storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="79edf-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="79edf-112">Zorg ervoor dat versleuteling is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="79edf-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="79edf-113">Hallo volgende beleid vereist dat alle storage accounts tooenable [service opslagversleuteling](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="79edf-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="79edf-114">Deze beleidsregel is ook beschikbaar als de beleidsdefinitie van een ingebouwde met de Hallo resource ID `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="79edf-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79edf-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79edf-115">Next steps</span></span>
* <span data-ttu-id="79edf-116">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="79edf-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="79edf-117">Hallo bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="79edf-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="79edf-118">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="79edf-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="79edf-119">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="79edf-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="79edf-120">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="79edf-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

