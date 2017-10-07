---
title: aaaDeploy een web-app die is gekoppeld tooa GitHub-opslagplaats | Microsoft Docs
description: Gebruik een Azure Resource Manager-sjabloon toodeploy een web-app met een project van een GitHub-opslagplaats.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Een web-app gekoppelde tooa GitHub-opslagplaats implementeren
In dit onderwerp leert u hoe toocreate een Azure Resource Manager-sjabloon die u implementeert een web-app die is gekoppeld tooa-project in een GitHub-opslagplaats. U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd. U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

Zie voor de volledige sjabloon hello, [Web App gekoppelde tooGitHub sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Wat u wilt implementeren
Met deze sjabloon implementeert u een web-app met Hallo-code van een project in GitHub.

toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:

[![TooAzure implementeren](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Hallo-URL voor de GitHub-opslagplaats die Hallo project toodeploy bevat. Deze parameter bevat een standaardwaarde, maar deze waarde is alleen bedoeld tooshow u hoe tooprovide URL Hallo voor opslagplaats. U kunt deze waarde gebruiken bij het testen Hallo-sjabloon, maar u zult tooprovide Hallo URL uw eigen opslagplaats bij het werken met Hallo-sjabloon.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Filialen
Hallo-vertakking van Hallo opslagplaats toouse bij het implementeren van Hallo-toepassing. de standaardwaarde Hallo master is, maar u Hallo-naam van elke vertakking in Hallo opslagplaats kunt opgeven dat u wenst dat toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Resources toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Web-app
Hiermee maakt u Hallo web-app die is gekoppeld toohello-project in GitHub. 

U Hallo-naam van de web-app via Hallo Hallo **siteName** parameter en locatie van web-app via Hallo HALLO hallo **siteLocation** parameter. In Hallo **dependsOn** element Hallo sjabloon definieert Hallo web-app als afhankelijk van Hallo-service die als host fungeert voor plan. Omdat dit afhankelijk van Hallo plan hosten is, is niet Hallo web-app gemaakt tot Hallo die als host fungeert voor plan is voltooid, wordt gemaakt. Hallo **dependsOn** element wordt alleen gebruikt toospecify implementatievolgorde. Als u web-app als afhankelijk hosting plan Hallo Hallo niet inschakelt, probeert Azure Resource Doorberekeningsfuncties toocreate beide resources op Hallo dezelfde tijd en u een foutbericht ontvangen als Hallo web-app is gemaakt voordat Hallo hosting-plan.

Hallo-web-app heeft ook een onderliggende resource die is gedefinieerd in **resources** hieronder. Deze onderliggende resource definieert broncodebeheer voor Hallo-project met Hallo web-app wordt geïmplementeerd. In deze sjabloon is Hallo broncodebeheer gekoppelde tooa bepaalde GitHub-opslagplaats. Hallo GitHub-opslagplaats is gedefinieerd door code Hallo **'RepoUrl': 'https://github.com/davidebbo-test/Mvc52Application.git'** u URL van de opslagplaats vastleggen Hallo mogelijk als u wilt dat toocreate een sjabloon die herhaaldelijk implementeert een één project tijdens het minimum aantal parameters Hallo vereisen.
In plaats van hard-coding van Hallo URL opslagplaats, kunt u een parameter voor de URL van de opslagplaats Hallo toevoegen en gebruiken van die waarde voor Hallo **RepoUrl** eigenschap.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Opdrachten toorun implementatie
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Zie voor de inhoud van Hallo parameters JSON-bestand, [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

