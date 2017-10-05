---
title: Toewijzen en beheren van Azure bronbeleid | Microsoft Docs
description: Beschrijft hoe Azure-resource beleid toepast op abonnementen en resourcegroepen en het bronbeleid weergeven.
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="600b9-103">Toewijzen en beheren van bronbeleid</span><span class="sxs-lookup"><span data-stu-id="600b9-103">Assign and manage resource policies</span></span>

<span data-ttu-id="600b9-104">Als u wilt een beleid implementeren, moet u deze stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="600b9-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="600b9-105">Controleer de beleidsdefinities (inclusief ingebouwde beleid verstrekt door Azure) om te zien als er al een bestaat in uw abonnement die voldoet aan uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="600b9-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="600b9-106">Als dit bestaat, krijgen de naam ervan.</span><span class="sxs-lookup"><span data-stu-id="600b9-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="600b9-107">Als deze niet bestaat, de beleidsregel met JSON definiëren en toevoegen als de beleidsdefinitie van een in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="600b9-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="600b9-108">Deze stap maakt het beleid beschikbaar voor toewijzing, maar niet de regels van toepassing op uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="600b9-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="600b9-109">Voor beide gevallen wijst u het beleid toe aan een bereik (zoals een abonnement of de resource-groep).</span><span class="sxs-lookup"><span data-stu-id="600b9-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="600b9-110">De regels van het beleid worden nu afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="600b9-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="600b9-111">Dit artikel is gericht op de stappen voor het maken van de beleidsdefinitie van een en die definitie toewijzen aan een scope via REST API, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="600b9-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="600b9-112">Als u liever de portal gebruiken voor het toewijzen van beleid, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="600b9-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="600b9-113">In dit artikel is niet gericht op de syntaxis voor het maken van de beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="600b9-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="600b9-114">Zie voor meer informatie over de syntaxis van het beleid [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="600b9-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="600b9-115">REST API</span><span class="sxs-lookup"><span data-stu-id="600b9-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="600b9-116">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="600b9-116">Create policy definition</span></span>

<span data-ttu-id="600b9-117">Kunt u een beleid met de [REST-API voor beleidsdefinities](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="600b9-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="600b9-118">De REST-API kunt u maken en verwijderen van beleidsdefinities en informatie over bestaande definities.</span><span class="sxs-lookup"><span data-stu-id="600b9-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="600b9-119">Voor het maken van een beleidsdefinitie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="600b9-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="600b9-120">Vergelijkbaar met het volgende voorbeeld wordt een aanvraagtekst omvatten:</span><span class="sxs-lookup"><span data-stu-id="600b9-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="600b9-121">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="600b9-121">Assign policy</span></span>

<span data-ttu-id="600b9-122">U kunt toepassen op het gewenste bereik via beleidsdefinitie de [REST-API voor beleidstoewijzingen](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="600b9-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="600b9-123">De REST-API kunt u maken en verwijderen van beleidstoewijzingen en informatie over bestaande toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="600b9-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="600b9-124">Voor het maken van een beleidstoewijzing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="600b9-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="600b9-125">De {-beleidstoewijzing} is de naam van de beleidstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="600b9-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="600b9-126">Vergelijkbaar met het volgende voorbeeld wordt een aanvraagtekst omvatten:</span><span class="sxs-lookup"><span data-stu-id="600b9-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="600b9-127">Weergave-beleid</span><span class="sxs-lookup"><span data-stu-id="600b9-127">View policy</span></span>
<span data-ttu-id="600b9-128">Als u een beleid, gebruikt de [ophalen van de beleidsdefinitie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="600b9-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="600b9-129">Aliassen ophalen</span><span class="sxs-lookup"><span data-stu-id="600b9-129">Get aliases</span></span>
<span data-ttu-id="600b9-130">U kunt aliassen via de REST-API ophalen:</span><span class="sxs-lookup"><span data-stu-id="600b9-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="600b9-131">Het volgende voorbeeld ziet een definitie van een alias.</span><span class="sxs-lookup"><span data-stu-id="600b9-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="600b9-132">Zoals u ziet, definieert een alias paden in verschillende API-versies, zelfs wanneer er een wijziging van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="600b9-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="600b9-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="600b9-133">PowerShell</span></span>

<span data-ttu-id="600b9-134">Controleer of u hebt voordat u doorgaat met de PowerShell-voorbeelden [de nieuwste versie geïnstalleerd](/powershell/azure/install-azurerm-ps) van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="600b9-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="600b9-135">Beleidsparameters zijn toegevoegd in versie 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="600b9-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="600b9-136">Als er een eerdere versie, retourneren in de voorbeelden foutmelding dat de parameter kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="600b9-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="600b9-137">Definities van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="600b9-137">View policy definitions</span></span>
<span data-ttu-id="600b9-138">Als alle beleidsdefinities in uw abonnement wilt weergeven, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="600b9-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="600b9-139">Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="600b9-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="600b9-140">Elk beleid wordt geretourneerd in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="600b9-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="600b9-141">Voordat u doorgaat een beleidsdefinitie maken, bekijkt u de ingebouwde beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="600b9-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="600b9-142">Als u een ingebouwde beleid dat van toepassing is de grenzen die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan.</span><span class="sxs-lookup"><span data-stu-id="600b9-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="600b9-143">In plaats daarvan de ingebouwde beleid toewijzen aan het gewenste bereik.</span><span class="sxs-lookup"><span data-stu-id="600b9-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="600b9-144">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="600b9-144">Create policy definition</span></span>
<span data-ttu-id="600b9-145">U kunt een beleid maakt definitie met de `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="600b9-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="600b9-146">De uitvoer wordt opgeslagen in een `$definition` -object, dat wordt gebruikt tijdens de toewijzing van configuratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="600b9-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="600b9-147">In plaats van de JSON geven als parameter, kunt u het pad naar een .json-bestand met de beleidsregel opgeven.</span><span class="sxs-lookup"><span data-stu-id="600b9-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="600b9-148">Het volgende voorbeeld wordt de beleidsdefinitie van een met parameters:</span><span class="sxs-lookup"><span data-stu-id="600b9-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="600b9-149">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="600b9-149">Assign policy</span></span>

<span data-ttu-id="600b9-150">U het beleid op het gewenste bereik toepassen met behulp van de `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="600b9-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="600b9-151">Het volgende voorbeeld wordt het beleid aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="600b9-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="600b9-152">Als u een beleid dat parameters vereist toewijzen, maken en deze waarden van objecten.</span><span class="sxs-lookup"><span data-stu-id="600b9-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="600b9-153">Het volgende voorbeeld wordt een ingebouwde beleid opgehaald en wordt doorgegeven in parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="600b9-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="600b9-154">De toewijzing van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="600b9-154">View policy assignment</span></span>

<span data-ttu-id="600b9-155">Als u de toewijzing van een specifiek beleid, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="600b9-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="600b9-156">Als u wilt de beleidsregel voor de beleidsdefinitie van een weergeven, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="600b9-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="600b9-157">Beleidstoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="600b9-157">Remove policy assignment</span></span> 

<span data-ttu-id="600b9-158">Als u wilt een beleidstoewijzing verwijderen, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="600b9-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="600b9-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="600b9-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="600b9-160">Definities van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="600b9-160">View policy definitions</span></span>
<span data-ttu-id="600b9-161">Als alle beleidsdefinities in uw abonnement wilt weergeven, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="600b9-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="600b9-162">Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="600b9-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="600b9-163">Elk beleid wordt geretourneerd in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="600b9-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="600b9-164">Voordat u doorgaat een beleidsdefinitie maken, bekijkt u de ingebouwde beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="600b9-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="600b9-165">Als u een ingebouwde beleid dat van toepassing is de grenzen die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan.</span><span class="sxs-lookup"><span data-stu-id="600b9-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="600b9-166">In plaats daarvan de ingebouwde beleid toewijzen aan het gewenste bereik.</span><span class="sxs-lookup"><span data-stu-id="600b9-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="600b9-167">Beleidsdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="600b9-167">Create policy definition</span></span>

<span data-ttu-id="600b9-168">U kunt een definitie voor Azure CLI gebruiken met de opdracht van de definitie beleid maken.</span><span class="sxs-lookup"><span data-stu-id="600b9-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="600b9-169">Toewijzen van beleid</span><span class="sxs-lookup"><span data-stu-id="600b9-169">Assign policy</span></span>

<span data-ttu-id="600b9-170">U kunt het beleid toepassen op het gewenste bereik met de opdracht van de toewijzing van beleid.</span><span class="sxs-lookup"><span data-stu-id="600b9-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="600b9-171">Het volgende voorbeeld wordt een beleid aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="600b9-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="600b9-172">De toewijzing van beleid weergeven</span><span class="sxs-lookup"><span data-stu-id="600b9-172">View policy assignment</span></span>

<span data-ttu-id="600b9-173">Als u wilt weergeven van de beleidstoewijzing van een, bieden de beleidstoewijzingsnaam en het bereik:</span><span class="sxs-lookup"><span data-stu-id="600b9-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="600b9-174">Beleidstoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="600b9-174">Remove policy assignment</span></span> 

<span data-ttu-id="600b9-175">Als u wilt een beleidstoewijzing verwijderen, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="600b9-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="600b9-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="600b9-176">Next steps</span></span>
* <span data-ttu-id="600b9-177">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="600b9-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

