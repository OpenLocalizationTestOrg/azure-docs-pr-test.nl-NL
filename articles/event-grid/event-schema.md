---
title: aaaAzure gebeurtenis raster gebeurtenis schema
description: Hallo-eigenschappen die beschikbaar zijn voor gebeurtenissen met Azure Event raster beschrijft.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a>Gebeurtenis raster gebeurtenis schema

Dit artikel bevat Hallo eigenschappen en het schema voor gebeurtenissen. Gebeurtenissen bestaan uit een set van vijf vereiste tekenreekseigenschappen en een vereiste **gegevens** object. Hallo-eigenschappen zijn algemene tooall gebeurtenissen van een willekeurige uitgever. Hallo **gegevens** object bevat eigenschappen die specifiek tooeach publisher zijn. Deze eigenschappen zijn voor systeemonderwerpen, specifieke toohello-resourceprovider, zoals opslag- of Event Hubs.

Gebeurtenissen worden tooAzure gebeurtenis raster verzonden in een matrix die meerdere gebeurtenisobjecten kan bevatten. Als er slechts één gebeurtenis, heeft Hallo matrix een lengte van 1. 
 
## <a name="event-properties"></a>Eigenschappen van gebeurtenis

Alle gebeurtenissen bevat Hallo dezelfde na het hoogste niveau gegevens.

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| Onderwerp | Tekenreeks | Volledige resource pad toohello gebeurtenisbron. Dit veld is niet beschrijfbaar. |
| Onderwerp | Tekenreeks | Publisher gedefinieerde pad toohello gebeurtenis onderwerp. |
| EventType | Tekenreeks | Een van de Hallo typen gebeurtenissen voor deze gebeurtenisbron geregistreerd. |
| eventTime | Tekenreeks | Hallo tijd Hallo gebeurtenis wordt gegenereerd op basis van UTC-tijd Hallo-provider. |
| id | Tekenreeks | De unieke id voor Hallo-gebeurtenis. |
| Gegevens | object | Specifieke toohello resourceprovider gebeurtenisgegevens. |

## <a name="available-event-sources"></a>Beschikbare gebeurtenisbronnen

Hallo volgende gebeurtenisbronnen publiceren gebeurtenissen voor consumptie via gebeurtenis raster:

* Resourcegroepen (beheerbewerkingen)
* Azure-abonnementen (beheerbewerkingen)
* Event Hubs
* Aangepaste-onderwerpen

## <a name="azure-subscriptions"></a>Azure-abonnementen

Azure-abonnementen kunnen nu verzenden van gebeurtenissen van Azure Resource Manager management zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.

### <a name="available-event-types"></a>Typen beschikbare gebeurtenissen

- **Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.  
- **Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.  
- **Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.  
- **Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.  
- **Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.  
- **Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd. Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.

### <a name="example-event-schema"></a>Voorbeeld van de gebeurtenis schema

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a>Resourcegroepen

Resourcegroepen kunnen nu verzenden management gebeurtenissen van Azure Resource Manager zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.

### <a name="available-event-types"></a>Typen beschikbare gebeurtenissen

- **Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.  
- **Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.  
- **Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.  
- **Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.  
- **Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.  
- **Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd. Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.

### <a name="example-event"></a>Voorbeeld van de gebeurtenis

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a>Event Hubs

Gebeurtenissen van Event Hubs zijn momenteel alleen verzonden wanneer een bestand met de Hallo vastleggen functie toostorage automatisch wordt verzonden.

### <a name="available-event-types"></a>Typen beschikbare gebeurtenissen

- **Microsoft.EventHub.CaptureFileCreated**: deze gebeurtenis treedt op wanneer een bestand met vastleggen wordt gemaakt.

### <a name="example-event"></a>Voorbeeld van de gebeurtenis

Deze voorbeeldgebeurtenis toont Hallo-schema van een Event Hubs-gebeurtenis die optreedt wanneer vastleggen wordt een bestand opgeslagen. 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a>Azure Blob Storage

Azure Blob Storage afgeschermd voorbeeld met registratie van integratie met gebeurtenis raster.

### <a name="available-event-types"></a>Typen beschikbare gebeurtenissen

- **Microsoft.Storage.BlobCreated**: deze gebeurtenis treedt op wanneer een blob is gemaakt.
- **Microsoft.Storage.BlobDeleted**: deze gebeurtenis treedt op wanneer een blob wordt verwijderd.

### <a name="example-event"></a>Voorbeeld van de gebeurtenis

Deze voorbeeldgebeurtenis toont Hallo-schema van een opslag-gebeurtenis die optreedt wanneer een blob is gemaakt. 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a>Aangepaste-onderwerpen

Hallo nettolading met gegevens van uw aangepaste gebeurtenissen wordt gedefinieerd door u en mag juiste indeling heeft JSON. Hallo bovenste niveau gegevens moet dezelfde als standaard resource gedefinieerd gebeurtenissen velden Hallo bevatten. Bij het publiceren van gebeurtenissen toocustom onderwerpen kunt u overwegen modelleren Hallo onderwerp van uw tooaid gebeurtenissen in Routering en filteren.

### <a name="example-event"></a>Voorbeeld van de gebeurtenis

Hallo volgende voorbeeld ziet u een gebeurtenis voor een aangepaste onderwerp:
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding-tooEvent raster [wat gebeurtenis raster is?](overview.md)
* Zie toolearn over het maken van een abonnement gebeurtenis raster [gebeurtenis raster abonnement schema](subscription-creation-schema.md).
