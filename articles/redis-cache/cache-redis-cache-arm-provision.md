---
title: aaaProvision een Redis-Cache met Azure Resource Manager | Microsoft Docs
description: Azure Resource Manager-sjabloon toodeploy een Azure Redis-Cache gebruiken.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Een Redis Cache maken op basis van een sjabloon
In dit onderwerp leert u hoe toocreate een Azure Resource Manager-sjabloon die wordt geïmplementeerd in een Azure Redis-Cache. Hallo-cache kan worden gebruikt met een bestaande opslag account tookeep diagnostische gegevens. U leert ook hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd. U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.

Op dit moment diagnostische instellingen worden gedeeld voor alle caches in Hallo dezelfde regio voor een abonnement. Bijwerken van een cache in Hallo regio is van invloed op alle andere caches in Hallo regio.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

Zie voor de volledige sjabloon hello, [Redis-Cache sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Resource Manager-sjablonen voor nieuwe Hallo [Premium-laag](cache-premium-tier-intro.md) beschikbaar zijn. 
> 
> * [Maken van een Premium Redis-Cache met clustering](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Premium Redis-Cache met gegevenspersistentie maken](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Premium Redis-Cache maken met VNet en een optionele clustering](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck voor de meest recente sjablonen hello, Zie [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) en zoek naar `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Wat u wilt implementeren
In deze sjabloon implementeert u een Azure Redis-Cache die gebruikmaakt van een bestaand opslagaccount voor diagnostische gegevens.

toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:

[![TooAzure implementeren](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd. Hallo-sjabloon bevat een sectie met de naam van de Parameters die alle Hallo parameterwaarden bevat.
U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren. Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde. De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
Hallo-locatie van Hallo Redis-Cache. Voor de beste prestaties Hallo gebruik dezelfde locatie als Hallo app toobe met Hallo cache gebruikt.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
Hallo de naam van Hallo bestaande storage account toouse voor diagnostische gegevens. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>EnableNonSslPort
Een Boolean die aangeeft of tooallow toegang krijgen tot via niet-SSL-poort.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Een waarde die aangeeft of diagnostische gegevens is ingeschakeld. Gebruik ON of OFF.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Resources toodeploy
### <a name="redis-cache"></a>Redis Cache
Hiermee maakt u hello Azure Redis-Cache.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Opdrachten toorun implementatie
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


