---
title: een logische app met een sjabloon in Azure aaaCreate | Microsoft Docs
description: "Gebruik een Azure Resource Manager-sjabloon toodeploy een logische app om werkstromen te definiëren."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Een logische app maken met een sjabloon
Sjablonen bieden een snelle manier toouse verschillende connectors in een logische app. Logische apps bevat Azure Resource Manager-sjablonen voor toocreate een logische app die gebruikt toodefine zakelijke werkstromen kan worden. U kunt definiëren welke bronnen worden geïmplementeerd, en hoe toodefine parameters wanneer u uw logische app implementeert. U kunt deze sjabloon voor uw eigen zakelijke scenario's gebruiken of aanpassen toomeet uw vereisten.

Zie voor meer informatie over Hallo Logic app-eigenschappen [Logic App werkstroom Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Zie voor voorbeelden van Hallo definitie zelf [auteur Logic App-definities](logic-apps-author-definitions.md). 

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

Zie voor de volledige sjabloon hello, [sjabloon voor logische Apps](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Wat u implementeert
Met deze sjabloon kunt u een logische app implementeren.

toorun Hallo implementatie selecteert automatisch Hallo volgende knop:  

[![TooAzure implementeren](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Resources toodeploy
### <a name="logic-app"></a>Logische app
Hallo logische app maakt.

Hallo sjablonen maakt gebruik van een parameterwaarde voor Hallo logic app-naam. Hallo-locatie van Hallo logic app toohello Hiermee dezelfde locatie als Hallo resourcegroep. 

Deze definitie voor bepaalde eens per uur wordt uitgevoerd en pings Hallo opgegeven locatie in Hallo **testUri** parameter. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
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
      }
    }


## <a name="commands-toorun-deployment"></a>Opdrachten toorun implementatie
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



