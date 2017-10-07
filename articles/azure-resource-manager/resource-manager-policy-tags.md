---
title: bronbeleid aaaAzure voor tags | Microsoft Docs
description: Voorbeelden van bronbeleid biedt voor het beheren van tags voor bronnen
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="d7c3d-103">Resource-beleid voor tags toepassen</span><span class="sxs-lookup"><span data-stu-id="d7c3d-103">Apply resource policies for tags</span></span>

<span data-ttu-id="d7c3d-104">Dit onderwerp bevat algemene beleidsregels dat kunt u tooensure consistent gebruik van tags toepassen op bronnen.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="d7c3d-105">Een label beleid tooa resourcegroep of abonnement met bestaande bronnen toepassen geldt met terugwerkende kracht niet Hallo beleid toothose resources.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="d7c3d-106">op deze resources tooenforce Hallo-beleid activeren een update toohello bestaande bronnen.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="d7c3d-107">Dit artikel bevat een voorbeeld van PowerShell voor activering van een update.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="d7c3d-108">Zorg ervoor dat alle bronnen in een resourcegroep hebben een tagwaarde</span><span class="sxs-lookup"><span data-stu-id="d7c3d-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="d7c3d-109">Een algemene vereiste is dat alle bronnen in een resourcegroep een bepaalde tag en een waarde hebben.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="d7c3d-110">Deze vereiste is vaak nodig tootrack kosten per afdeling.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="d7c3d-111">Hallo volgende voorwaarden is voldaan:</span><span class="sxs-lookup"><span data-stu-id="d7c3d-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="d7c3d-112">Hallo vereist label en waarde toegevoegde toonew en resources die geen label Hallo bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="d7c3d-113">Hallo vereist label en de waarde kan niet worden verwijderd uit een bestaande resources.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="d7c3d-114">U uitvoeren deze vereiste door het toepassen van twee ingebouwde beleid tooa-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="d7c3d-115">Id</span><span class="sxs-lookup"><span data-stu-id="d7c3d-115">ID</span></span> | <span data-ttu-id="d7c3d-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7c3d-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="d7c3d-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="d7c3d-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="d7c3d-118">Van toepassing is een vereiste label en de standaardwaarde wanneer deze niet is opgegeven door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="d7c3d-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="d7c3d-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="d7c3d-120">Hiermee wordt het een vereiste label en de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="d7c3d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7c3d-121">PowerShell</span></span>

<span data-ttu-id="d7c3d-122">Hallo volgende PowerShell-script wordt toegewezen Hallo twee ingebouwde beleid definities tooa-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="d7c3d-123">Voordat u Hallo script uitvoert, alle vereiste tags toohello resourcegroep worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="d7c3d-124">Elke tag voor de resourcegroep Hallo is vereist voor Hallo bronnen in Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="d7c3d-125">tooassign tooall resourcegroepen in uw abonnement, bieden geen Hallo `-Name` parameter bij het ophalen van Hallo resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="d7c3d-126">Na het toewijzen van Hallo beleidsregels, kunt u een update tooall bestaande resources tooenforce Hallo tag beleidsregels die u hebt toegevoegd activeren.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="d7c3d-127">Hallo behoudt volgende script andere codes die beschikbaar op Hallo bronnen waren:</span><span class="sxs-lookup"><span data-stu-id="d7c3d-127">hello following script retains any other tags that existed on hello resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="d7c3d-128">Codes voor een resourcetype vereisen</span><span class="sxs-lookup"><span data-stu-id="d7c3d-128">Require tags for a resource type</span></span>
<span data-ttu-id="d7c3d-129">Hallo volgende voorbeeld ziet u hoe toonest logische operators toorequire een toepassing taggen voor alleen een type opgegeven resource (in dit geval storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="d7c3d-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="d7c3d-130">Tag vereisen</span><span class="sxs-lookup"><span data-stu-id="d7c3d-130">Require tag</span></span>
<span data-ttu-id="d7c3d-131">Hallo weigert volgende beleid aanvragen die niet over een label met 'costCenter' sleutel (elke waarde kan worden toegepast):</span><span class="sxs-lookup"><span data-stu-id="d7c3d-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d7c3d-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7c3d-132">Next steps</span></span>
* <span data-ttu-id="d7c3d-133">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="d7c3d-134">Hallo bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="d7c3d-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d7c3d-135">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3d-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d7c3d-136">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3d-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="d7c3d-137">Zie voor een inleiding tooresource beleidsregels, [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3d-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="d7c3d-138">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3d-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

