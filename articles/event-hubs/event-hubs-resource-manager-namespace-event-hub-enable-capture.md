---
title: een Azure Event Hubs-naamruimte en schakel vastleggen met behulp van een sjabloon aaaCreate | Microsoft Docs
description: Een Azure Event Hubs-naamruimte met een gebeurtenishub maken en Capture inschakelen met behulp van een Azure Resource Manager-sjabloon
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Een Event Hubs-naamruimte met een gebeurtenishub maken en Capture inschakelen met behulp van een Azure Resource Manager-sjabloon

Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een naamruimte Event Hubs met een event hub-instantie en schakelt Hallo [vastleggen functie](event-hubs-capture-overview.md) voor Hallo event hub. Hallo artikel wordt beschreven hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd. U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.

Dit artikel laat zien hoe toospecify dat gebeurtenissen worden vastgelegd in Azure Storage-Blobs of een Azure Data Lake Store is gebaseerd op Hallo bestemming die u kiest.

Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.

Zie [Naming Conventions][Azure Resources naming conventions] (Naamgevingsconventies) voor meer informatie over de patronen en procedures voor naamgevingsconventies van Azure Resources.

Hallo voltooid sjablonen, klikt u op Hallo GitHub-koppelingen te volgen:

- [Event hub en schakel vastleggen tooStorage sjabloon][Event Hub and enable Capture tooStorage template] 
- [Event hub en schakel vastleggen tooAzure Data Lake Store-sjabloon][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Event Hubs.
> 
> 

## <a name="what-will-you-deploy"></a>Wat wilt u implementeren?

Met deze sjabloon implementeert u een Event Hubs-naamruimte met een gebeurtenishub en schakelt u tevens [Event Hubs Cinapture](event-hubs-capture-overview.md) in.

[Event Hubs](event-hubs-what-is-event-hubs.md) is een service die wordt gebruikt tooprovide gebeurtenissen en telemetriegegevens inkomend tooAzure op grote schaal met weinig latentie en hoge betrouwbaarheid. Event Hubs vastleggen schakelt u tooautomatically leveren Hallo streaming-gegevens in Event Hubs tooAzure Blob storage of Azure Data Lake Store binnen een opgegeven periode of het interval van de grootte van uw keuze.

Klik op Hallo knop tooenable Event Hubs vastleggen in Azure Storage te volgen:

[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Klik op Hallo knop tooenable Event Hubs vastleggen in Azure Data Lake Store te volgen:

[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters

Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd. Hallo-sjabloon bevat een sectie met de naam `Parameters` die alle Hallo parameterwaarden bevat. U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren. Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde. De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.

Hallo sjabloon definieert Hallo parameters te volgen.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

Hallo-naam van Hallo [Event Hubs naamruimte](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

naam van Hallo event hub is gemaakt in Hallo Hallo [Event Hubs naamruimte](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

Hallo aantal dagen tooretain Hallo-berichten in Hallo event hub. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

Hallo aantal partities toocreate in Hallo event hub.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Schakel vastleggen op Hallo event hub.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

Hallo-coderingsindeling u tooserialize Hallo gebeurtenisgegevens opgeven.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

Hallo tijdsinterval waarin Event Hubs vastleggen begint het vastleggen van Hallo gegevens.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
Hallo grootte interval waarop vastleggen begint het vastleggen van Hallo gegevens.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

Hallo-naamnotatie gebruikt door het vastleggen van Event Hubs toowrite hello Avro bestanden. De indeling voor Capture moet de velden `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` en `{Second}` bevatten. Deze velden kunnen in willekeurige volgorde worden gerangschikt, met of zonder scheidingstekens.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

Hallo API-versie van Hallo-sjabloon.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Gebruik Hallo parameters te volgen als u Azure Storage als de bestemming.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Vastleggen vereist een Azure Storage-account resource-ID tooenable tooyour vastleggen gewenst Storage-account.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Hallo blob-container in welke toocapture de gebeurtenisgegevens.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Gebruik Hallo parameters te volgen als u Azure Data Lake Store als de bestemming. U moet machtigingen instellen op uw Data Lake Store-pad, waarin u wilt dat tooCapture Hallo gebeurtenis. tooset machtigingen, Zie [in dit artikel](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

Abonnement-ID voor Hallo Event Hubs-naamruimte en de Azure Data Lake Store. Beide deze resources moeten onder Hallo dezelfde abonnements-ID.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

naam van de Hello Azure Data Lake Store voor Hallo gebeurtenissen vastgelegd.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

Hallo pad naar de doelmap voor Hallo gebeurtenissen vastgelegd.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy resources voor Azure Storage als bestemming toocaptured gebeurtenissen

Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en schakelt vastleggen tooAzure Blob Storage.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy resources voor Azure Data Lake Store als bestemming

Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en schakelt vastleggen tooAzure Data Lake Store.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Opdrachten toorun implementatie

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Uw sjabloon tooenable Event Hubs vastleggen implementeren in Azure Storage:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Uw sjabloon tooenable Event Hubs vastleggen implementeren in Azure Data Lake Store:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI

Azure Blob Storage kiezen als doel:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Azure Data Lake Store kiezen als doel:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Volgende stappen

U kunt ook configureren Event Hubs vastleggen via Hallo [Azure-portal](https://portal.azure.com). Zie voor meer informatie [Azure-portal met behulp van inschakelen van Event Hubs vastleggen Hallo](event-hubs-capture-enable-through-portal.md).

U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
