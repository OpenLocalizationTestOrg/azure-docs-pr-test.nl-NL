---
title: aaaCreate een waarschuwing activiteit logboek met Resource Manager-sjabloon | Microsoft Docs
description: Op de hoogte worden gesteld wanneer uw Azure-resources zijn gemaakt.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Een activiteit logboek waarschuwing met Resource Manager-sjabloon maken
Dit artikel ziet u hoe toouse een [Azure Resource Manager-sjabloon](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activiteit logboek waarschuwingen. Met behulp van sjablonen, kunt u gemakkelijk veel waarschuwingen die worden geactiveerd op basis van specifieke activiteit logboek gebeurtenis voorwaarden als onderdeel van uw geautomatiseerde implementatie instellen.

Hallo basisstappen zijn:

1. Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe de waarschuwing voor het melden van toocreate Hallo activiteit.

2. Hallo-sjabloon implementeren met [eventuele implementatiemethode](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Resource Manager-sjabloon voor een activiteit logboek-waarschuwing
toocreate een waarschuwing activiteit logboek met een Resource Manager-sjabloon, hebt u een resource van het type Hallo `microsoft.insights/activityLogAlerts`. Vervolgens vult u alle bijbehorende eigenschappen. Hier volgt een sjabloon die u een activiteit logboek-waarschuwing maakt.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

Ga naar onze [Azure snelstartgalerie](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) voor enkele voorbeelden van waarschuwing activiteitssjablonen logboek.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [waarschuwingen](monitoring-overview-alerts.md).
- Meer informatie over hoe tooadd [actiegroepen met behulp van een Resource Manager-sjabloon](monitoring-create-action-group-with-resource-manager-template.md).
- Meer informatie over hoe te[maken van een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Meer informatie over hoe te[maken van een activiteit logboek waarschuwing toomonitor alle mislukte automatisch schalen scale-in/scale-out-bewerkingen op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
