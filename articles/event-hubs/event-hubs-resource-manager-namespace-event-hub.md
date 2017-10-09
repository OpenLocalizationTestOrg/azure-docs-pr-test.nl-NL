---
title: een Azure Event Hubs-naamruimte en de consument een groep met een sjabloon aaaCreate | Microsoft Docs
description: Een Event Hubs-naamruimte maken met een event hub en een consumergroep met behulp van Azure Resource Manager-sjablonen
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon maken

Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een naamruimte van het type Event Hubs met een event hub en een consumergroep. Hallo toont hoe artikel toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd. U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten

Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.

Zie voor de volledige sjabloon hello, Hallo [Event hub- en groep sjabloon] [ Event Hub and consumer group template] op GitHub.

> [!NOTE]
> toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Event Hubs.
> 
> 

## <a name="what-will-you-deploy"></a>Wat wilt u implementeren?
Met deze sjabloon implementeert u een Event Hubs-naamruimte met een event hub en een consumergroep.

[Event Hubs](event-hubs-what-is-event-hubs.md) is een service die wordt gebruikt tooprovide gebeurtenissen en telemetriegegevens inkomend tooAzure op grote schaal met weinig latentie en hoge betrouwbaarheid.

toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:

[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd. Hallo-sjabloon bevat een sectie met de naam `Parameters` die alle Hallo parameterwaarden bevat. Een parameter voor de waarden die variëren, op basis van Hallo-project die u implementeert of op basis van Hallo omgeving toowhich die u implementeert, moet u definiëren. Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde. Elke parameterwaarde in Hallo sjabloon definieert Hallo-resources die zijn geïmplementeerd.

Hallo sjabloon definieert Hallo volgende parameters:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
Hallo-naam van Hallo Event Hubs naamruimte toocreate.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
Hallo-naam van Hallo event hub in Hallo Event Hubs-naamruimte gemaakt.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
Hallo-naam van consumentengroep Hallo voor Hallo event hub is gemaakt.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
Hallo API-versie van Hallo-sjabloon.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Resources toodeploy
Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en een consumergroep.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Opdrachten toorun implementatie
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
