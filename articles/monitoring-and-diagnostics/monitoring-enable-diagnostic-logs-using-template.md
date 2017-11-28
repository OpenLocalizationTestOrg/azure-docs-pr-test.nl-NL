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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="b714e-103">Diagnostische instellingen voor automatisch inschakelen bij het maken van de resource met een Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b714e-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="b714e-104">In dit artikel laten we zien hoe u kunt een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure diagnostische instellingen op een resource als deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b714e-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="b714e-105">Hiermee kunt u tooautomatically start streaming uw diagnostische logboeken en metrische gegevens tooEvent Hubs, in een Opslagaccount wilt archiveren, of ze tooLog Analytics verzonden wanneer een bron wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b714e-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="b714e-106">Hallo-methode voor het inschakelen van diagnostische logboeken met een Resource Manager-sjabloon is afhankelijk van Hallo brontype.</span><span class="sxs-lookup"><span data-stu-id="b714e-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="b714e-107">**Niet-Compute** resources (bijvoorbeeld Netwerkbeveiligingsgroepen Logic Apps automatisering) gebruiken [diagnostische instellingen die worden beschreven in dit artikel](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="b714e-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="b714e-108">**COMPUTE** resources (af/LAD gebaseerde) gebruiken Hallo [af/LAD configuratiebestand beschreven in dit artikel](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="b714e-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="b714e-109">In dit artikel wordt beschreven hoe tooconfigure van diagnostische gegevens met een van de methoden.</span><span class="sxs-lookup"><span data-stu-id="b714e-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="b714e-110">Hallo eenvoudige stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="b714e-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="b714e-111">Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe toocreate Hallo resource en diagnostische gegevens inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b714e-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="b714e-112">[Hallo-sjabloon met een implementatiemethode implementeert](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b714e-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="b714e-113">We bieden hieronder een voorbeeld van Hallo sjabloon, moet u toogenerate voor niet-berekenings- en rekenresources JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="b714e-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="b714e-114">Niet-Compute resource-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b714e-114">Non-Compute resource template</span></span>
<span data-ttu-id="b714e-115">Voor niet-rekenresources moet u toodo twee dingen:</span><span class="sxs-lookup"><span data-stu-id="b714e-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="b714e-116">Voeg parameters toohello parameters blob voor de opslagaccountnaam hello, service bus regel-ID en/of OMS Log Analytics werkruimte-ID (waardoor archivering van diagnostische logboeken in een opslagaccount, streamen van Logboeken tooEvent Hubs en/of verzenden van Logboeken tooLog Analytics).</span><span class="sxs-lookup"><span data-stu-id="b714e-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
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
2. <span data-ttu-id="b714e-117">In Hallo resources matrix van Hallo bron waarvoor u tooenable diagnostische logboeken, voegt u een resource van het type `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="b714e-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="b714e-118">Hallo eigenschappen blob voor Hallo diagnostische instelling volgt [Hallo-indeling die wordt beschreven in dit artikel](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="b714e-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="b714e-119">Toe te voegen Hallo `metrics` eigenschap inschakelen tooalso verzenden resource metrische gegevens toothese dezelfde levert, op voorwaarde dat [Hallo-resource ondersteunt Azure Monitor metrische gegevens](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b714e-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="b714e-120">Hier volgt een voorbeeld van een volledige die een logische App maakt en Hiermee schakelt u streaming tooEvent Hubs en opslag in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b714e-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

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

## <a name="compute-resource-template"></a><span data-ttu-id="b714e-121">COMPUTE resource-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b714e-121">Compute resource template</span></span>
<span data-ttu-id="b714e-122">tooenable diagnostische gegevens op een berekeningsresource, bijvoorbeeld een virtuele Machine of Service Fabric-cluster, moet u:</span><span class="sxs-lookup"><span data-stu-id="b714e-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="b714e-123">Hello Azure Diagnostics toohello VM resource-uitbreidingsdefinitie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b714e-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="b714e-124">Geef een opslag-account en/of event hub als parameter.</span><span class="sxs-lookup"><span data-stu-id="b714e-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="b714e-125">Hallo-inhoud van uw WADCfg XML-bestand in Hallo XMLCfg eigenschap, alle XML-tekens juist aanhalingstekens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b714e-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="b714e-126">Deze laatste stap kan lastig tooget rechts zijn.</span><span class="sxs-lookup"><span data-stu-id="b714e-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="b714e-127">[Raadpleeg dit artikel](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) voor een voorbeeld dat splitsingen Diagnostics configuratieschema Hallo naar variabelen die zijn escape-teken en de juiste indeling.</span><span class="sxs-lookup"><span data-stu-id="b714e-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="b714e-128">Hallo hele proces, inclusief voorbeelden, wordt beschreven [in dit document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b714e-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b714e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b714e-129">Next Steps</span></span>
* [<span data-ttu-id="b714e-130">Meer informatie over Azure diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="b714e-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="b714e-131">Diagnostische logboeken van Azure tooEvent Hubs Stream</span><span class="sxs-lookup"><span data-stu-id="b714e-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

