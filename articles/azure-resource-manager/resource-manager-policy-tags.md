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
# <a name="apply-resource-policies-for-tags"></a>Resource-beleid voor tags toepassen

Dit onderwerp bevat algemene beleidsregels dat kunt u tooensure consistent gebruik van tags toepassen op bronnen.

Een label beleid tooa resourcegroep of abonnement met bestaande bronnen toepassen geldt met terugwerkende kracht niet Hallo beleid toothose resources. op deze resources tooenforce Hallo-beleid activeren een update toohello bestaande bronnen. Dit artikel bevat een voorbeeld van PowerShell voor activering van een update.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Zorg ervoor dat alle bronnen in een resourcegroep hebben een tagwaarde

Een algemene vereiste is dat alle bronnen in een resourcegroep een bepaalde tag en een waarde hebben. Deze vereiste is vaak nodig tootrack kosten per afdeling. Hallo volgende voorwaarden is voldaan:

* Hallo vereist label en waarde toegevoegde toonew en resources die geen label Hallo bijgewerkt.
* Hallo vereist label en de waarde kan niet worden verwijderd uit een bestaande resources.

U uitvoeren deze vereiste door het toepassen van twee ingebouwde beleid tooa-resourcegroep.

| Id | Beschrijving |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Van toepassing is een vereiste label en de standaardwaarde wanneer deze niet is opgegeven door de gebruiker Hallo. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Hiermee wordt het een vereiste label en de waarde ervan. |

### <a name="powershell"></a>PowerShell

Hallo volgende PowerShell-script wordt toegewezen Hallo twee ingebouwde beleid definities tooa-resourcegroep. Voordat u Hallo script uitvoert, alle vereiste tags toohello resourcegroep worden toegewezen. Elke tag voor de resourcegroep Hallo is vereist voor Hallo bronnen in Hallo-groep. tooassign tooall resourcegroepen in uw abonnement, bieden geen Hallo `-Name` parameter bij het ophalen van Hallo resourcegroepen.

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

Na het toewijzen van Hallo beleidsregels, kunt u een update tooall bestaande resources tooenforce Hallo tag beleidsregels die u hebt toegevoegd activeren. Hallo behoudt volgende script andere codes die beschikbaar op Hallo bronnen waren:

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

## <a name="require-tags-for-a-resource-type"></a>Codes voor een resourcetype vereisen
Hallo volgende voorbeeld ziet u hoe toonest logische operators toorequire een toepassing taggen voor alleen een type opgegeven resource (in dit geval storage-accounts).

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

## <a name="require-tag"></a>Tag vereisen
Hallo weigert volgende beleid aanvragen die niet over een label met 'costCenter' sleutel (elke waarde kan worden toegepast):

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

## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik. Hallo bereik mag een abonnement, resourcegroep of resource. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).
* Zie voor een inleiding tooresource beleidsregels, [Resource overzicht](resource-manager-policy.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

