---
title: aaaAutomatically Schakel de diagnostische instellingen met een Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe een Resource Manager toouse sjabloon toocreate diagnostische instellingen waarmee u toostream uw diagnostische logboeken tooEvent Hubs of op te slaan in een opslagaccount.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Diagnostische instellingen voor automatisch inschakelen bij het maken van de resource met een Resource Manager-sjabloon
In dit artikel laten we zien hoe u kunt een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure diagnostische instellingen op een resource als deze is gemaakt. Hiermee kunt u tooautomatically start streaming uw diagnostische logboeken en metrische gegevens tooEvent Hubs, in een Opslagaccount wilt archiveren, of ze tooLog Analytics verzonden wanneer een bron wordt gemaakt.

Hallo-methode voor het inschakelen van diagnostische logboeken met een Resource Manager-sjabloon is afhankelijk van Hallo brontype.

* **Niet-Compute** resources (bijvoorbeeld Netwerkbeveiligingsgroepen Logic Apps automatisering) gebruiken [diagnostische instellingen die worden beschreven in dit artikel](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **COMPUTE** resources (af/LAD gebaseerde) gebruiken Hallo [af/LAD configuratiebestand beschreven in dit artikel](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

In dit artikel wordt beschreven hoe tooconfigure van diagnostische gegevens met een van de methoden.

Hallo eenvoudige stappen zijn als volgt:

1. Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe toocreate Hallo resource en diagnostische gegevens inschakelen.
2. [Hallo-sjabloon met een implementatiemethode implementeert](../azure-resource-manager/resource-group-template-deploy.md).

We bieden hieronder een voorbeeld van Hallo sjabloon, moet u toogenerate voor niet-berekenings- en rekenresources JSON-bestand.

## <a name="non-compute-resource-template"></a>Niet-Compute resource-sjabloon
Voor niet-rekenresources moet u toodo twee dingen:

1. Voeg parameters toohello parameters blob voor de opslagaccountnaam hello, service bus regel-ID en/of OMS Log Analytics werkruimte-ID (waardoor archivering van diagnostische logboeken in een opslagaccount, streamen van Logboeken tooEvent Hubs en/of verzenden van Logboeken tooLog Analytics).
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. In Hallo resources matrix van Hallo bron waarvoor u tooenable diagnostische logboeken, voegt u een resource van het type `[resource namespace]/providers/diagnosticSettings`.
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

Hallo eigenschappen blob voor Hallo diagnostische instelling volgt [Hallo-indeling die wordt beschreven in dit artikel](https://msdn.microsoft.com/library/azure/dn931931.aspx). Toe te voegen Hallo `metrics` eigenschap inschakelen tooalso verzenden resource metrische gegevens toothese dezelfde levert, op voorwaarde dat [Hallo-resource ondersteunt Azure Monitor metrische gegevens](monitoring-supported-metrics.md).

Hier volgt een voorbeeld van een volledige die een logische App maakt en Hiermee schakelt u streaming tooEvent Hubs en opslag in een opslagaccount.

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a>COMPUTE resource-sjabloon
tooenable diagnostische gegevens op een berekeningsresource, bijvoorbeeld een virtuele Machine of Service Fabric-cluster, moet u:

1. Hello Azure Diagnostics toohello VM resource-uitbreidingsdefinitie toevoegen.
2. Geef een opslag-account en/of event hub als parameter.
3. Hallo-inhoud van uw WADCfg XML-bestand in Hallo XMLCfg eigenschap, alle XML-tekens juist aanhalingstekens toevoegen.

> [!WARNING]
> Deze laatste stap kan lastig tooget rechts zijn. [Raadpleeg dit artikel](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) voor een voorbeeld dat splitsingen Diagnostics configuratieschema Hallo naar variabelen die zijn escape-teken en de juiste indeling.
> 
> 

Hallo hele proces, inclusief voorbeelden, wordt beschreven [in dit document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Azure diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md)
* [Diagnostische logboeken van Azure tooEvent Hubs Stream](monitoring-stream-diagnostic-logs-to-event-hubs.md)

