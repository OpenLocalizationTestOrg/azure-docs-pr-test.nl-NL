---
title: aaaCreate actiegroepen met Resource Manager-sjablonen | Microsoft Docs
description: Meer informatie over hoe een actie toocreate groeperen met behulp van een Azure Resource Manager-sjabloon.
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>Een actiegroep met Resource Manager-sjabloon maken
Dit artikel ziet u hoe toouse een [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure Actiegroepen. Met behulp van sjablonen, kunt u automatisch actiegroepen die opnieuw kunnen worden gebruikt in bepaalde typen waarschuwingen instellen. Deze actiegroepen Zorg ervoor dat alle Hallo juiste partijen worden gewaarschuwd wanneer een waarschuwing wordt geactiveerd.

Hallo basisstappen zijn:

1. Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe toocreate Hallo actiegroep.

2. Hallo-sjabloon implementeren met [eventuele implementatiemethode](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

Eerst we beschrijven hoe toocreate Resource Manager-sjabloon voor een actie groep waar Hallo actie definities zijn hardgecodeerd in Hallo-sjabloon. Ten tweede beschrijven we hoe toocreate een sjabloon waarmee Hallo webhook-configuratiegegevens als parameters voor invoer wanneer Hallo sjabloon wordt geïmplementeerd.

## <a name="resource-manager-templates-for-an-action-group"></a>Resource Manager-sjablonen voor een actiegroep

toocreate een actiegroep met een Resource Manager-sjabloon, hebt u een resource van het type Hallo `Microsoft.Insights/actionGroups`. Vervolgens vult u alle bijbehorende eigenschappen. Hier vindt u twee voorbeeldsjablonen die een actiegroep maken.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [actiegroepen](monitoring-action-groups.md).
* Meer informatie over [waarschuwingen](monitoring-overview-alerts.md).
* Meer informatie over hoe tooadd [waarschuwingen met een Resource Manager-sjabloon](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
