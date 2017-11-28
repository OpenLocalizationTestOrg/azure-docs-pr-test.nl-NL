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
# <a name="event-grid-event-schema"></a><span data-ttu-id="1243f-103">Gebeurtenis raster gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="1243f-103">Event Grid event schema</span></span>

<span data-ttu-id="1243f-104">Dit artikel bevat Hallo eigenschappen en het schema voor gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="1243f-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="1243f-105">Gebeurtenissen bestaan uit een set van vijf vereiste tekenreekseigenschappen en een vereiste **gegevens** object.</span><span class="sxs-lookup"><span data-stu-id="1243f-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="1243f-106">Hallo-eigenschappen zijn algemene tooall gebeurtenissen van een willekeurige uitgever.</span><span class="sxs-lookup"><span data-stu-id="1243f-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="1243f-107">Hallo **gegevens** object bevat eigenschappen die specifiek tooeach publisher zijn.</span><span class="sxs-lookup"><span data-stu-id="1243f-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="1243f-108">Deze eigenschappen zijn voor systeemonderwerpen, specifieke toohello-resourceprovider, zoals opslag- of Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1243f-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="1243f-109">Gebeurtenissen worden tooAzure gebeurtenis raster verzonden in een matrix die meerdere gebeurtenisobjecten kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="1243f-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="1243f-110">Als er slechts één gebeurtenis, heeft Hallo matrix een lengte van 1.</span><span class="sxs-lookup"><span data-stu-id="1243f-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="1243f-111">Eigenschappen van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="1243f-111">Event properties</span></span>

<span data-ttu-id="1243f-112">Alle gebeurtenissen bevat Hallo dezelfde na het hoogste niveau gegevens.</span><span class="sxs-lookup"><span data-stu-id="1243f-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="1243f-113">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1243f-113">Property</span></span> | <span data-ttu-id="1243f-114">Type</span><span class="sxs-lookup"><span data-stu-id="1243f-114">Type</span></span> | <span data-ttu-id="1243f-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1243f-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="1243f-116">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="1243f-116">topic</span></span> | <span data-ttu-id="1243f-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1243f-117">string</span></span> | <span data-ttu-id="1243f-118">Volledige resource pad toohello gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="1243f-118">Full resource path toohello event source.</span></span> <span data-ttu-id="1243f-119">Dit veld is niet beschrijfbaar.</span><span class="sxs-lookup"><span data-stu-id="1243f-119">This field is not writeable.</span></span> |
| <span data-ttu-id="1243f-120">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="1243f-120">subject</span></span> | <span data-ttu-id="1243f-121">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1243f-121">string</span></span> | <span data-ttu-id="1243f-122">Publisher gedefinieerde pad toohello gebeurtenis onderwerp.</span><span class="sxs-lookup"><span data-stu-id="1243f-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="1243f-123">EventType</span><span class="sxs-lookup"><span data-stu-id="1243f-123">eventType</span></span> | <span data-ttu-id="1243f-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1243f-124">string</span></span> | <span data-ttu-id="1243f-125">Een van de Hallo typen gebeurtenissen voor deze gebeurtenisbron geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="1243f-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="1243f-126">eventTime</span></span> | <span data-ttu-id="1243f-127">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1243f-127">string</span></span> | <span data-ttu-id="1243f-128">Hallo tijd Hallo gebeurtenis wordt gegenereerd op basis van UTC-tijd Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="1243f-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="1243f-129">id</span><span class="sxs-lookup"><span data-stu-id="1243f-129">id</span></span> | <span data-ttu-id="1243f-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1243f-130">string</span></span> | <span data-ttu-id="1243f-131">De unieke id voor Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="1243f-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="1243f-132">Gegevens</span><span class="sxs-lookup"><span data-stu-id="1243f-132">data</span></span> | <span data-ttu-id="1243f-133">object</span><span class="sxs-lookup"><span data-stu-id="1243f-133">object</span></span> | <span data-ttu-id="1243f-134">Specifieke toohello resourceprovider gebeurtenisgegevens.</span><span class="sxs-lookup"><span data-stu-id="1243f-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="1243f-135">Beschikbare gebeurtenisbronnen</span><span class="sxs-lookup"><span data-stu-id="1243f-135">Available event sources</span></span>

<span data-ttu-id="1243f-136">Hallo volgende gebeurtenisbronnen publiceren gebeurtenissen voor consumptie via gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="1243f-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="1243f-137">Resourcegroepen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="1243f-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="1243f-138">Azure-abonnementen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="1243f-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="1243f-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1243f-139">Event Hubs</span></span>
* <span data-ttu-id="1243f-140">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="1243f-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="1243f-141">Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="1243f-141">Azure Subscriptions</span></span>

<span data-ttu-id="1243f-142">Azure-abonnementen kunnen nu verzenden van gebeurtenissen van Azure Resource Manager management zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1243f-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1243f-143">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="1243f-143">Available event types</span></span>

- <span data-ttu-id="1243f-144">**Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1243f-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="1243f-145">**Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="1243f-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="1243f-146">**Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="1243f-147">**Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1243f-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="1243f-148">**Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="1243f-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="1243f-149">**Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="1243f-150">Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="1243f-151">Voorbeeld van de gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="1243f-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="1243f-152">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="1243f-152">Resource Groups</span></span>

<span data-ttu-id="1243f-153">Resourcegroepen kunnen nu verzenden management gebeurtenissen van Azure Resource Manager zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1243f-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1243f-154">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="1243f-154">Available event types</span></span>

- <span data-ttu-id="1243f-155">**Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1243f-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="1243f-156">**Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="1243f-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="1243f-157">**Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="1243f-158">**Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1243f-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="1243f-159">**Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="1243f-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="1243f-160">**Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="1243f-161">Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1243f-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="1243f-162">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="1243f-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="1243f-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1243f-163">Event Hubs</span></span>

<span data-ttu-id="1243f-164">Gebeurtenissen van Event Hubs zijn momenteel alleen verzonden wanneer een bestand met de Hallo vastleggen functie toostorage automatisch wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="1243f-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1243f-165">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="1243f-165">Available event types</span></span>

- <span data-ttu-id="1243f-166">**Microsoft.EventHub.CaptureFileCreated**: deze gebeurtenis treedt op wanneer een bestand met vastleggen wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1243f-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="1243f-167">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="1243f-167">Example event</span></span>

<span data-ttu-id="1243f-168">Deze voorbeeldgebeurtenis toont Hallo-schema van een Event Hubs-gebeurtenis die optreedt wanneer vastleggen wordt een bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1243f-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="1243f-169">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1243f-169">Azure Blob Storage</span></span>

<span data-ttu-id="1243f-170">Azure Blob Storage afgeschermd voorbeeld met registratie van integratie met gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="1243f-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1243f-171">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="1243f-171">Available event types</span></span>

- <span data-ttu-id="1243f-172">**Microsoft.Storage.BlobCreated**: deze gebeurtenis treedt op wanneer een blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1243f-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="1243f-173">**Microsoft.Storage.BlobDeleted**: deze gebeurtenis treedt op wanneer een blob wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1243f-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="1243f-174">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="1243f-174">Example event</span></span>

<span data-ttu-id="1243f-175">Deze voorbeeldgebeurtenis toont Hallo-schema van een opslag-gebeurtenis die optreedt wanneer een blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1243f-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="1243f-176">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="1243f-176">Custom Topics</span></span>

<span data-ttu-id="1243f-177">Hallo nettolading met gegevens van uw aangepaste gebeurtenissen wordt gedefinieerd door u en mag juiste indeling heeft JSON.</span><span class="sxs-lookup"><span data-stu-id="1243f-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="1243f-178">Hallo bovenste niveau gegevens moet dezelfde als standaard resource gedefinieerd gebeurtenissen velden Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="1243f-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="1243f-179">Bij het publiceren van gebeurtenissen toocustom onderwerpen kunt u overwegen modelleren Hallo onderwerp van uw tooaid gebeurtenissen in Routering en filteren.</span><span class="sxs-lookup"><span data-stu-id="1243f-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="1243f-180">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="1243f-180">Example event</span></span>

<span data-ttu-id="1243f-181">Hallo volgende voorbeeld ziet u een gebeurtenis voor een aangepaste onderwerp:</span><span class="sxs-lookup"><span data-stu-id="1243f-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="1243f-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1243f-182">Next steps</span></span>

* <span data-ttu-id="1243f-183">Zie voor een inleiding-tooEvent raster [wat gebeurtenis raster is?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="1243f-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="1243f-184">Zie toolearn over het maken van een abonnement gebeurtenis raster [gebeurtenis raster abonnement schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1243f-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
