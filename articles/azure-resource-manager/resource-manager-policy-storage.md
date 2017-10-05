---
title: Azure-resource beleidsregels voor opslagaccounts | Microsoft Docs
description: Beschrijving van het Azure Resource Manager-beleid voor het beheren van de implementatie van de storage-accounts.
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="9225e-103">Resource-beleid toepassen op de storage-accounts</span><span class="sxs-lookup"><span data-stu-id="9225e-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="9225e-104">Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u kunt toepassen op Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="9225e-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="9225e-105">Deze beleidsregels consistentie voor de opslagaccounts die zijn geïmplementeerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="9225e-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="9225e-106">Account voor toegestane opslagtypen definiëren</span><span class="sxs-lookup"><span data-stu-id="9225e-106">Define permitted storage account types</span></span>

<span data-ttu-id="9225e-107">Het volgende beleid beperkt die [opslagaccounttypen](../storage/common/storage-redundancy.md) kan worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="9225e-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="9225e-108">Een beleidsregel vergelijkbaar met een parameter voor het accepteren van de toegestane SKU's is beschikbaar als een ingebouwde beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="9225e-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="9225e-109">Het ingebouwde beleid heeft de bron-ID van `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="9225e-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="9225e-110">Toegestane toegangslaag definiëren</span><span class="sxs-lookup"><span data-stu-id="9225e-110">Define permitted access tier</span></span>

<span data-ttu-id="9225e-111">Het volgende beleid geeft het type [toegangslaag](../storage/blobs/storage-blob-storage-tiers.md) die kan worden opgegeven voor de storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="9225e-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="9225e-112">Zorg ervoor dat versleuteling is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9225e-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="9225e-113">Het volgende beleid vereist dat alle opslagaccounts om in te schakelen [service opslagversleuteling](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="9225e-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="9225e-114">Deze beleidsregel is ook beschikbaar als de beleidsdefinitie van een ingebouwde aan de bron-ID van `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="9225e-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9225e-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9225e-115">Next steps</span></span>
* <span data-ttu-id="9225e-116">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden), moet u de beleidsdefinitie maken en toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="9225e-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="9225e-117">Het bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="9225e-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="9225e-118">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9225e-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="9225e-119">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="9225e-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="9225e-120">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9225e-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

