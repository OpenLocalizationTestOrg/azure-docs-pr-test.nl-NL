---
title: aaaAssign en beheren van Azure-resource beleid | Microsoft Docs
description: Hierin wordt beschreven hoe tooapply Azure beleid toosubscriptions en resource-resourcegroepen, en hoe tooview bronbeleid.
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="79d57-103">Toewijzen en beheren van bronbeleid</span><span class="sxs-lookup"><span data-stu-id="79d57-103">Assign and manage resource policies</span></span>

<span data-ttu-id="79d57-104">tooimplement een beleid, moet u deze stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="79d57-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="79d57-105">Controleer beleid definities (inclusief ingebouwde beleid verstrekt door Azure) toosee als er al een bestaat in uw abonnement die voldoet aan uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="79d57-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="79d57-106">Als dit bestaat, krijgen de naam ervan.</span><span class="sxs-lookup"><span data-stu-id="79d57-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="79d57-107">Als deze niet bestaat, Hallo beleidsregel JSON definiëren en toevoegen als de beleidsdefinitie van een in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="79d57-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="79d57-108">Deze stap maakt beleid Hallo beschikbaar voor toewijzing maar Hallo regels tooyour abonnement is niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="79d57-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="79d57-109">Voor beide gevallen toewijzen Hallo beleid tooa bereik (zoals een abonnement of de resource-groep).</span><span class="sxs-lookup"><span data-stu-id="79d57-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="79d57-110">Hallo-regels van het Hallo-beleid worden nu afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="79d57-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="79d57-111">Dit artikel is gericht op Hallo stappen toocreate een beleidsdefinitie en toewijzen dat bereik definitie tooa via REST API, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="79d57-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="79d57-112">Als u liever toouse Hallo portal tooassign beleidsregels, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="79d57-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="79d57-113">In dit artikel is niet gericht op Hallo-syntaxis voor het maken van de beleidsdefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="79d57-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="79d57-114">Zie voor meer informatie over de syntaxis van het beleid [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="79d57-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="79d57-115">REST API</span><span class="sxs-lookup"><span data-stu-id="79d57-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="79d57-116">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="79d57-116">Create policy definition</span></span>

<span data-ttu-id="79d57-117">U kunt een beleid maken met de Hallo [REST-API voor beleidsdefinities](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="79d57-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="79d57-118">Hallo REST-API kunt u toocreate beleidsdefinities verwijderen en informatie over bestaande definities.</span><span class="sxs-lookup"><span data-stu-id="79d57-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="79d57-119">een beleidsdefinitie toocreate uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="79d57-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="79d57-120">Een aanvraag hoofdtekst vergelijkbare toohello volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="79d57-120">Include a request body similar toohello following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a><span data-ttu-id="79d57-121">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="79d57-121">Assign policy</span></span>

<span data-ttu-id="79d57-122">U kunt de beleidsdefinitie Hallo bij Hallo gewenst bereik via Hallo toepassen [REST-API voor beleidstoewijzingen](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="79d57-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="79d57-123">Hallo REST-API kunt u toocreate beleidstoewijzingen verwijderen en informatie over bestaande toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="79d57-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="79d57-124">een beleidstoewijzing toocreate uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="79d57-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="79d57-125">Hallo {beleidstoewijzing} is Hallo-naam van de beleidstoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="79d57-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="79d57-126">Een aanvraag hoofdtekst vergelijkbare toohello volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="79d57-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="79d57-127">Weergave-beleid</span><span class="sxs-lookup"><span data-stu-id="79d57-127">View policy</span></span>
<span data-ttu-id="79d57-128">een beleid tooget gebruiken Hallo [ophalen van de beleidsdefinitie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="79d57-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="79d57-129">Aliassen ophalen</span><span class="sxs-lookup"><span data-stu-id="79d57-129">Get aliases</span></span>
<span data-ttu-id="79d57-130">U kunt aliassen via Hallo REST-API ophalen:</span><span class="sxs-lookup"><span data-stu-id="79d57-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="79d57-131">Hallo volgende voorbeeld ziet u een definitie van een alias.</span><span class="sxs-lookup"><span data-stu-id="79d57-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="79d57-132">Zoals u ziet, definieert een alias paden in verschillende API-versies, zelfs wanneer er een wijziging van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="79d57-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="79d57-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79d57-133">PowerShell</span></span>

<span data-ttu-id="79d57-134">Controleer of u hebt voordat u doorgaat met de PowerShell-voorbeelden Hallo [Hallo meest recente versie hebt geïnstalleerd](/powershell/azure/install-azurerm-ps) van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79d57-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="79d57-135">Beleidsparameters zijn toegevoegd in versie 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="79d57-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="79d57-136">Als er een eerdere versie, retourneren Hallo voorbeelden dat een fout die duiden Hallo-parameter kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="79d57-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="79d57-137">Definities van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="79d57-137">View policy definitions</span></span>
<span data-ttu-id="79d57-138">toosee alle beleidsdefinities in uw abonnement, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="79d57-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="79d57-139">Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="79d57-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="79d57-140">Elk beleid wordt geretourneerd als Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="79d57-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="79d57-141">Bekijk voordat u doorgaat toocreate een beleidsdefinitie, Hallo ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="79d57-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="79d57-142">Als u een ingebouwde beleid dat van toepassing is Hallo-limieten die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan.</span><span class="sxs-lookup"><span data-stu-id="79d57-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="79d57-143">In plaats daarvan toewijzen Hallo ingebouwde beleid toohello gewenst bereik.</span><span class="sxs-lookup"><span data-stu-id="79d57-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="79d57-144">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="79d57-144">Create policy definition</span></span>
<span data-ttu-id="79d57-145">U kunt de beleidsdefinitie van een met behulp van Hallo maken `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79d57-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
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
}'
```            

<span data-ttu-id="79d57-146">Hallo-uitvoer wordt opgeslagen in een `$definition` -object, dat wordt gebruikt tijdens de toewijzing van configuratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="79d57-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="79d57-147">U kunt in plaats van Hallo JSON geven als parameter, Hallo pad tooa .json-bestand met beleidsregel Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="79d57-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="79d57-148">Hallo wordt volgende voorbeeld de beleidsdefinitie van een met parameters:</span><span class="sxs-lookup"><span data-stu-id="79d57-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="79d57-149">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="79d57-149">Assign policy</span></span>

<span data-ttu-id="79d57-150">U beleid voor het Hallo Hallo gewenst bereik toepassen via Hallo `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79d57-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="79d57-151">Hallo volgt toegewezen Hallo beleid tooa resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="79d57-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="79d57-152">tooassign een beleid dat parameters vereist zijn, maken en deze waarden van objecten.</span><span class="sxs-lookup"><span data-stu-id="79d57-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="79d57-153">Hallo volgende voorbeeld wordt een ingebouwde beleid opgehaald en wordt doorgegeven in parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="79d57-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="79d57-154">De toewijzing van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="79d57-154">View policy assignment</span></span>

<span data-ttu-id="79d57-155">de toewijzing van een specifiek beleid tooget gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79d57-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="79d57-156">tooview hello beleidsregel voor de beleidsdefinitie van een, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79d57-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="79d57-157">Beleidstoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="79d57-157">Remove policy assignment</span></span> 

<span data-ttu-id="79d57-158">een beleidstoewijzing tooremove gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79d57-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="79d57-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79d57-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="79d57-160">Definities van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="79d57-160">View policy definitions</span></span>
<span data-ttu-id="79d57-161">toosee alle beleidsdefinities in uw abonnement, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="79d57-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="79d57-162">Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="79d57-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="79d57-163">Elk beleid wordt geretourneerd als Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="79d57-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="79d57-164">Bekijk voordat u doorgaat toocreate een beleidsdefinitie, Hallo ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="79d57-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="79d57-165">Als u een ingebouwde beleid dat van toepassing is Hallo-limieten die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan.</span><span class="sxs-lookup"><span data-stu-id="79d57-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="79d57-166">In plaats daarvan toewijzen Hallo ingebouwde beleid toohello gewenst bereik.</span><span class="sxs-lookup"><span data-stu-id="79d57-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="79d57-167">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="79d57-167">Create policy definition</span></span>

<span data-ttu-id="79d57-168">U kunt de beleidsdefinitie van een met Azure CLI met Hallo beleid definitie opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="79d57-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
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
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="79d57-169">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="79d57-169">Assign policy</span></span>

<span data-ttu-id="79d57-170">U kunt Hallo beleid toohello gewenst bereik toepassen met behulp van Hallo beleid toewijzing opdracht.</span><span class="sxs-lookup"><span data-stu-id="79d57-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="79d57-171">Hallo volgende voorbeeld wordt een resourcegroep van beleid tooa toegewezen.</span><span class="sxs-lookup"><span data-stu-id="79d57-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="79d57-172">De toewijzing van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="79d57-172">View policy assignment</span></span>

<span data-ttu-id="79d57-173">een beleidstoewijzing tooview bieden Hallo beleidstoewijzingsnaam en Hallo bereik:</span><span class="sxs-lookup"><span data-stu-id="79d57-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="79d57-174">Beleidstoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="79d57-174">Remove policy assignment</span></span> 

<span data-ttu-id="79d57-175">een beleidstoewijzing tooremove gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79d57-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="79d57-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79d57-176">Next steps</span></span>
* <span data-ttu-id="79d57-177">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="79d57-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

