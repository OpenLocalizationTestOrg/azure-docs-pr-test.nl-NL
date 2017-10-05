---
title: Maken van een activiteit logboek waarschuwing met Resource Manager-sjabloon | Microsoft Docs
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
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="4cbe4-103">Een activiteit logboek waarschuwing met Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="4cbe4-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="4cbe4-104">Dit artikel laat zien hoe u een [Azure Resource Manager-sjabloon](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) activiteit logboek waarschuwingen configureren.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="4cbe4-105">Met behulp van sjablonen, kunt u gemakkelijk veel waarschuwingen die worden geactiveerd op basis van specifieke activiteit logboek gebeurtenis voorwaarden als onderdeel van uw geautomatiseerde implementatie instellen.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="4cbe4-106">De eenvoudige stappen zijn:</span><span class="sxs-lookup"><span data-stu-id="4cbe4-106">The basic steps are:</span></span>

1. <span data-ttu-id="4cbe4-107">Een sjabloon maken als een JSON-bestand dat wordt beschreven hoe u de activiteit logboek-waarschuwing wilt maken.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="4cbe4-108">De sjabloon implementeren met behulp van [eventuele implementatiemethode](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="4cbe4-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="4cbe4-109">Resource Manager-sjabloon voor een activiteit logboek-waarschuwing</span><span class="sxs-lookup"><span data-stu-id="4cbe4-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="4cbe4-110">Activiteit logboek waarschuwingen met een Resource Manager-sjabloon maken, die u maakt een resource van het type `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="4cbe4-111">Vervolgens vult u alle bijbehorende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-111">Then you fill in all related properties.</span></span> <span data-ttu-id="4cbe4-112">Hier volgt een sjabloon die u een activiteit logboek-waarschuwing maakt.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
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

<span data-ttu-id="4cbe4-113">Ga naar onze [Azure snelstartgalerie](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) voor enkele voorbeelden van waarschuwing activiteitssjablonen logboek.</span><span class="sxs-lookup"><span data-stu-id="4cbe4-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cbe4-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4cbe4-114">Next steps</span></span>
- <span data-ttu-id="4cbe4-115">Meer informatie over [waarschuwingen](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4cbe4-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="4cbe4-116">Meer informatie over het toevoegen van [actiegroepen met behulp van een Resource Manager-sjabloon](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="4cbe4-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="4cbe4-117">Meer informatie over hoe [maken van een activiteit logboek-waarschuwing voor het bewaken van alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="4cbe4-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="4cbe4-118">Meer informatie over hoe [maken van een activiteit logboek-waarschuwing voor het bewaken van alle mislukte automatisch schalen scale-in/scale-out-bewerkingen op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="4cbe4-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
