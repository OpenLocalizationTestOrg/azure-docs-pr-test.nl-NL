---
title: Een web-app die is gekoppeld aan een GitHub-opslagplaats implementeren | Microsoft Docs
description: Gebruik een Azure Resource Manager-sjabloon voor het implementeren van een web-app met een project van een GitHub-opslagplaats.
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a>Een web-app die is gekoppeld aan een GitHub-opslagplaats implementeren
In dit onderwerp leert u het maken van een Azure Resource Manager-sjabloon die u implementeert een web-app die is gekoppeld aan een project in een GitHub-opslagplaats. U leert hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd. U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

Zie voor de volledige sjabloon [Web App gekoppeld aan de sjabloon GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Wat u wilt implementeren
Met deze sjabloon implementeert u een web-app met de code van een project in GitHub.

Klik op de volgende knop om de implementatie automatisch uit te voeren:

[![Implementeren in Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
De URL van de GitHub-opslagplaats met het project te implementeren. Deze parameter bevat een standaardwaarde, maar deze waarde is alleen bedoeld voor hoe u de URL opgeven voor de opslagplaats. U kunt deze waarde gebruiken bij het testen van de sjabloon, maar u wilt en geef de URL van uw eigen opslagplaats bij het werken met de sjabloon.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Filialen
De branche van de opslagplaats gebruiken bij het implementeren van de toepassing. De standaardwaarde is master, maar u kunt opgeven dat de naam van elke vertakking in de opslagplaats die u wilt implementeren.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a>Resources om te implementeren
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Web-app
Maakt de web-app die is gekoppeld aan het project in GitHub. 

U de naam van de web-app via de **siteName** parameter en de locatie van de web-app via de **siteLocation** parameter. In de **dependsOn** element, de sjabloon definieert de web-app als afhankelijk van de service die als host fungeert voor plan. Omdat dit afhankelijk van het hosting plan is, wordt de web-app niet gemaakt totdat het hosting plan is voltooid, wordt gemaakt. De **dependsOn** element wordt alleen gebruikt om op te geven van de implementatievolgorde. Als u de web-app als afhankelijk van de hosting-planning niet inschakelt, Azure Resource Doorberekeningsfuncties zal proberen te maken van beide resources op hetzelfde moment en u kunt een fout kan optreden als de web-app is gemaakt voordat het hosting plan.

De web-app heeft ook een onderliggende resource die is gedefinieerd in **resources** hieronder. Deze onderliggende resource definieert bron voor het project met de web-app wordt geïmplementeerd. In deze sjabloon is broncodebeheer gekoppeld aan een bepaalde GitHub-opslagplaats. De GitHub-opslagplaats is gedefinieerd met de code **'RepoUrl': 'https://github.com/davidebbo-test/Mvc52Application.git'** u mogelijk harde code de URL van de opslagplaats wanneer u maken van een sjabloon die herhaaldelijk een project implementeert wilt terwijl slechts het minimum aantal parameters.
In plaats van hard-coding van de URL van de opslagplaats, kunt u een parameter voor de URL van de opslagplaats toevoegen en gebruiken van die waarde voor de **RepoUrl** eigenschap.

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

## <a name="commands-to-run-deployment"></a>Opdrachten om implementatie uit te voeren
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Zie voor de inhoud van de parameters-JSON-bestand, [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

