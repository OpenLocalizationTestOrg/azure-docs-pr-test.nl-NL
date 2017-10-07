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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="9fc25-103">Een activiteit logboek waarschuwing met Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="9fc25-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="9fc25-104">Dit artikel ziet u hoe toouse een [Azure Resource Manager-sjabloon](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activiteit logboek waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9fc25-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="9fc25-105">Met behulp van sjablonen, kunt u gemakkelijk veel waarschuwingen die worden geactiveerd op basis van specifieke activiteit logboek gebeurtenis voorwaarden als onderdeel van uw geautomatiseerde implementatie instellen.</span><span class="sxs-lookup"><span data-stu-id="9fc25-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="9fc25-106">Hallo basisstappen zijn:</span><span class="sxs-lookup"><span data-stu-id="9fc25-106">hello basic steps are:</span></span>

1. <span data-ttu-id="9fc25-107">Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe de waarschuwing voor het melden van toocreate Hallo activiteit.</span><span class="sxs-lookup"><span data-stu-id="9fc25-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="9fc25-108">Hallo-sjabloon implementeren met [eventuele implementatiemethode](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="9fc25-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="9fc25-109">Resource Manager-sjabloon voor een activiteit logboek-waarschuwing</span><span class="sxs-lookup"><span data-stu-id="9fc25-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="9fc25-110">toocreate een waarschuwing activiteit logboek met een Resource Manager-sjabloon, hebt u een resource van het type Hallo `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="9fc25-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="9fc25-111">Vervolgens vult u alle bijbehorende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="9fc25-111">Then you fill in all related properties.</span></span> <span data-ttu-id="9fc25-112">Hier volgt een sjabloon die u een activiteit logboek-waarschuwing maakt.</span><span class="sxs-lookup"><span data-stu-id="9fc25-112">Here's a template that creates an activity log alert.</span></span>

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

<span data-ttu-id="9fc25-113">Ga naar onze [Azure snelstartgalerie](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) voor enkele voorbeelden van waarschuwing activiteitssjablonen logboek.</span><span class="sxs-lookup"><span data-stu-id="9fc25-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fc25-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9fc25-114">Next steps</span></span>
- <span data-ttu-id="9fc25-115">Meer informatie over [waarschuwingen](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9fc25-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="9fc25-116">Meer informatie over hoe tooadd [actiegroepen met behulp van een Resource Manager-sjabloon](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="9fc25-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="9fc25-117">Meer informatie over hoe te[maken van een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="9fc25-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="9fc25-118">Meer informatie over hoe te[maken van een activiteit logboek waarschuwing toomonitor alle mislukte automatisch schalen scale-in/scale-out-bewerkingen op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="9fc25-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
