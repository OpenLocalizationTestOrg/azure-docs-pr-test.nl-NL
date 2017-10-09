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
# <a name="assign-and-manage-resource-policies"></a>Toewijzen en beheren van bronbeleid

tooimplement een beleid, moet u deze stappen uitvoeren:

1. Controleer beleid definities (inclusief ingebouwde beleid verstrekt door Azure) toosee als er al een bestaat in uw abonnement die voldoet aan uw vereisten.
2. Als dit bestaat, krijgen de naam ervan.
3. Als deze niet bestaat, Hallo beleidsregel JSON definiëren en toevoegen als de beleidsdefinitie van een in uw abonnement. Deze stap maakt beleid Hallo beschikbaar voor toewijzing maar Hallo regels tooyour abonnement is niet van toepassing.
4. Voor beide gevallen toewijzen Hallo beleid tooa bereik (zoals een abonnement of de resource-groep). Hallo-regels van het Hallo-beleid worden nu afgedwongen.

Dit artikel is gericht op Hallo stappen toocreate een beleidsdefinitie en toewijzen dat bereik definitie tooa via REST API, PowerShell of Azure CLI. Als u liever toouse Hallo portal tooassign beleidsregels, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). In dit artikel is niet gericht op Hallo-syntaxis voor het maken van de beleidsdefinitie Hallo. Zie voor meer informatie over de syntaxis van het beleid [Resource overzicht](resource-manager-policy.md).

## <a name="rest-api"></a>REST API

### <a name="create-policy-definition"></a>Beleidsdefinitie maken

U kunt een beleid maken met de Hallo [REST-API voor beleidsdefinities](/rest/api/resources/policydefinitions). Hallo REST-API kunt u toocreate beleidsdefinities verwijderen en informatie over bestaande definities.

een beleidsdefinitie toocreate uitvoeren:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Een aanvraag hoofdtekst vergelijkbare toohello volgt zijn:

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

### <a name="assign-policy"></a>Toewijzen van beleid

U kunt de beleidsdefinitie Hallo bij Hallo gewenst bereik via Hallo toepassen [REST-API voor beleidstoewijzingen](/rest/api/resources/policyassignments). Hallo REST-API kunt u toocreate beleidstoewijzingen verwijderen en informatie over bestaande toewijzingen.

een beleidstoewijzing toocreate uitvoeren:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Hallo {beleidstoewijzing} is Hallo-naam van de beleidstoewijzing Hallo.

Een aanvraag hoofdtekst vergelijkbare toohello volgt zijn:

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

### <a name="view-policy"></a>Weergave-beleid
een beleid tooget gebruiken Hallo [ophalen van de beleidsdefinitie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) bewerking.

### <a name="get-aliases"></a>Aliassen ophalen
U kunt aliassen via Hallo REST-API ophalen:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Hallo volgende voorbeeld ziet u een definitie van een alias. Zoals u ziet, definieert een alias paden in verschillende API-versies, zelfs wanneer er een wijziging van de eigenschap. 

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

## <a name="powershell"></a>PowerShell

Controleer of u hebt voordat u doorgaat met de PowerShell-voorbeelden Hallo [Hallo meest recente versie hebt geïnstalleerd](/powershell/azure/install-azurerm-ps) van Azure PowerShell. Beleidsparameters zijn toegevoegd in versie 3.6.0. Als er een eerdere versie, retourneren Hallo voorbeelden dat een fout die duiden Hallo-parameter kan niet worden gevonden.

### <a name="view-policy-definitions"></a>Definities van beleid weergeven
toosee alle beleidsdefinities in uw abonnement, gebruik Hallo volgende opdracht:

```powershell
Get-AzureRmPolicyDefinition
```

Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid. Elk beleid wordt geretourneerd als Hallo volgende indeling:

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

Bekijk voordat u doorgaat toocreate een beleidsdefinitie, Hallo ingebouwde beleid. Als u een ingebouwde beleid dat van toepassing is Hallo-limieten die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan. In plaats daarvan toewijzen Hallo ingebouwde beleid toohello gewenst bereik.

### <a name="create-policy-definition"></a>Beleidsdefinitie maken
U kunt de beleidsdefinitie van een met behulp van Hallo maken `New-AzureRmPolicyDefinition` cmdlet.

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

Hallo-uitvoer wordt opgeslagen in een `$definition` -object, dat wordt gebruikt tijdens de toewijzing van configuratiebeleid. 

U kunt in plaats van Hallo JSON geven als parameter, Hallo pad tooa .json-bestand met beleidsregel Hallo opgeven.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Hallo wordt volgende voorbeeld de beleidsdefinitie van een met parameters:

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

### <a name="assign-policy"></a>Toewijzen van beleid

U beleid voor het Hallo Hallo gewenst bereik toepassen via Hallo `New-AzureRmPolicyAssignment` cmdlet. Hallo volgt toegewezen Hallo beleid tooa resourcegroep.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign een beleid dat parameters vereist zijn, maken en deze waarden van objecten. Hallo volgende voorbeeld wordt een ingebouwde beleid opgehaald en wordt doorgegeven in parameterwaarden:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>De toewijzing van beleid weergeven

de toewijzing van een specifiek beleid tooget gebruiken:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

tooview hello beleidsregel voor de beleidsdefinitie van een, gebruiken:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Beleidstoewijzing verwijderen 

een beleidstoewijzing tooremove gebruiken:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Azure CLI

### <a name="view-policy-definitions"></a>Definities van beleid weergeven
toosee alle beleidsdefinities in uw abonnement, gebruik Hallo volgende opdracht:

```azurecli
az policy definition list
```

Retourneert alle beschikbare door beleidsdefinities, met inbegrip van ingebouwde beleid. Elk beleid wordt geretourneerd als Hallo volgende indeling:

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

Bekijk voordat u doorgaat toocreate een beleidsdefinitie, Hallo ingebouwde beleid. Als u een ingebouwde beleid dat van toepassing is Hallo-limieten die u nodig hebt gevonden, kunt u het maken van een beleidsdefinitie overslaan. In plaats daarvan toewijzen Hallo ingebouwde beleid toohello gewenst bereik.

### <a name="create-policy-definition"></a>Beleidsdefinitie maken

U kunt de beleidsdefinitie van een met Azure CLI met Hallo beleid definitie opdracht maken.

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

### <a name="assign-policy"></a>Toewijzen van beleid

U kunt Hallo beleid toohello gewenst bereik toepassen met behulp van Hallo beleid toewijzing opdracht. Hallo volgende voorbeeld wordt een resourcegroep van beleid tooa toegewezen.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>De toewijzing van beleid weergeven

een beleidstoewijzing tooview bieden Hallo beleidstoewijzingsnaam en Hallo bereik:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Beleidstoewijzing verwijderen 

een beleidstoewijzing tooremove gebruiken:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Volgende stappen
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

