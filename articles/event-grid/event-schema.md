---
title: Azure Event raster gebeurtenis schema
description: Beschrijft de eigenschappen die beschikbaar zijn voor gebeurtenissen met Azure Event raster.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="8905e-103">Gebeurtenis raster gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="8905e-103">Event Grid event schema</span></span>

<span data-ttu-id="8905e-104">Dit artikel bevat de eigenschappen en het schema voor gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8905e-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="8905e-105">Gebeurtenissen bestaan uit een set van vijf vereiste tekenreekseigenschappen en een vereiste **gegevens** object.</span><span class="sxs-lookup"><span data-stu-id="8905e-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="8905e-106">De eigenschappen gelden voor alle gebeurtenissen vanaf een willekeurige uitgever.</span><span class="sxs-lookup"><span data-stu-id="8905e-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="8905e-107">De **gegevens** object bevat eigenschappen die specifiek voor elke uitgever zijn.</span><span class="sxs-lookup"><span data-stu-id="8905e-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="8905e-108">Deze eigenschappen zijn specifiek voor de resourceprovider, zoals opslag of Event Hubs voor systeemonderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8905e-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="8905e-109">Gebeurtenissen worden verzonden naar Azure gebeurtenis raster in een matrix die meerdere gebeurtenisobjecten kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="8905e-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="8905e-110">Als er slechts één gebeurtenis, heeft de matrix een lengte van 1.</span><span class="sxs-lookup"><span data-stu-id="8905e-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="8905e-111">Eigenschappen van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8905e-111">Event properties</span></span>

<span data-ttu-id="8905e-112">Alle gebeurtenissen bevat dezelfde volgende bovenste niveau gegevens.</span><span class="sxs-lookup"><span data-stu-id="8905e-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="8905e-113">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8905e-113">Property</span></span> | <span data-ttu-id="8905e-114">Type</span><span class="sxs-lookup"><span data-stu-id="8905e-114">Type</span></span> | <span data-ttu-id="8905e-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8905e-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="8905e-116">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="8905e-116">topic</span></span> | <span data-ttu-id="8905e-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8905e-117">string</span></span> | <span data-ttu-id="8905e-118">Volledige resource-pad naar de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="8905e-118">Full resource path to the event source.</span></span> <span data-ttu-id="8905e-119">Dit veld is niet beschrijfbaar.</span><span class="sxs-lookup"><span data-stu-id="8905e-119">This field is not writeable.</span></span> |
| <span data-ttu-id="8905e-120">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="8905e-120">subject</span></span> | <span data-ttu-id="8905e-121">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8905e-121">string</span></span> | <span data-ttu-id="8905e-122">Publisher gedefinieerde pad naar het onderwerp van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8905e-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="8905e-123">EventType</span><span class="sxs-lookup"><span data-stu-id="8905e-123">eventType</span></span> | <span data-ttu-id="8905e-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8905e-124">string</span></span> | <span data-ttu-id="8905e-125">Een van de typen van de geregistreerde gebeurtenis van de bron van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8905e-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="8905e-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="8905e-126">eventTime</span></span> | <span data-ttu-id="8905e-127">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8905e-127">string</span></span> | <span data-ttu-id="8905e-128">De tijd dat de gebeurtenis wordt gegenereerd, gebaseerd op de UTC-tijd van de provider.</span><span class="sxs-lookup"><span data-stu-id="8905e-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="8905e-129">id</span><span class="sxs-lookup"><span data-stu-id="8905e-129">id</span></span> | <span data-ttu-id="8905e-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8905e-130">string</span></span> | <span data-ttu-id="8905e-131">De unieke id voor de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8905e-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="8905e-132">Gegevens</span><span class="sxs-lookup"><span data-stu-id="8905e-132">data</span></span> | <span data-ttu-id="8905e-133">object</span><span class="sxs-lookup"><span data-stu-id="8905e-133">object</span></span> | <span data-ttu-id="8905e-134">Gebeurtenisgegevens die specifiek zijn voor de resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="8905e-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="8905e-135">Beschikbare gebeurtenisbronnen</span><span class="sxs-lookup"><span data-stu-id="8905e-135">Available event sources</span></span>

<span data-ttu-id="8905e-136">De volgende bronnen van gebeurtenissen publiceren gebeurtenissen voor consumptie via gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="8905e-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="8905e-137">Resourcegroepen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="8905e-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="8905e-138">Azure-abonnementen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="8905e-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="8905e-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8905e-139">Event Hubs</span></span>
* <span data-ttu-id="8905e-140">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="8905e-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="8905e-141">Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="8905e-141">Azure Subscriptions</span></span>

<span data-ttu-id="8905e-142">Azure-abonnementen kunnen nu verzenden van gebeurtenissen van Azure Resource Manager management zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8905e-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="8905e-143">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8905e-143">Available event types</span></span>

- <span data-ttu-id="8905e-144">**Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8905e-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="8905e-145">**Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8905e-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="8905e-146">**Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="8905e-147">**Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8905e-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="8905e-148">**Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8905e-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="8905e-149">**Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="8905e-150">Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="8905e-151">Voorbeeld van de gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="8905e-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="8905e-152">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="8905e-152">Resource Groups</span></span>

<span data-ttu-id="8905e-153">Resourcegroepen kunnen nu verzenden management gebeurtenissen van Azure Resource Manager zoals wanneer een virtuele machine wordt gemaakt of een opslagaccount is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8905e-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="8905e-154">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8905e-154">Available event types</span></span>

- <span data-ttu-id="8905e-155">**Microsoft.Resources.ResourceWriteSuccess**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8905e-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="8905e-156">**Microsoft.Resources.ResourceWriteFailure**: deze gebeurtenis treedt op wanneer een resource maken of update-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8905e-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="8905e-157">**Microsoft.Resources.ResourceWriteCancel**: deze gebeurtenis treedt op wanneer een resource maken of bijwerken van de bewerking is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="8905e-158">**Microsoft.Resources.ResourceDeleteSuccess**: deze gebeurtenis treedt op als een resource verwijderingsbewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8905e-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="8905e-159">**Microsoft.Resources.ResourceDeleteFailure**: deze gebeurtenis treedt op wanneer een resource-delete-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8905e-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="8905e-160">**Microsoft.Resources.ResourceDeleteCancel**: 'Deze gebeurtenis treedt op wanneer het verwijderen van een resource wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="8905e-161">Dit gebeurt wanneer de sjabloonimplementatie is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8905e-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="8905e-162">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8905e-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="8905e-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8905e-163">Event Hubs</span></span>

<span data-ttu-id="8905e-164">Gebeurtenissen van Event Hubs zijn momenteel alleen verzonden wanneer een bestand wordt automatisch verzonden naar de opslag met de functie vastleggen.</span><span class="sxs-lookup"><span data-stu-id="8905e-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="8905e-165">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8905e-165">Available event types</span></span>

- <span data-ttu-id="8905e-166">**Microsoft.EventHub.CaptureFileCreated**: deze gebeurtenis treedt op wanneer een bestand met vastleggen wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8905e-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="8905e-167">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8905e-167">Example event</span></span>

<span data-ttu-id="8905e-168">Deze voorbeeldgebeurtenis ziet u het schema van een Event Hubs-gebeurtenis die optreedt wanneer vastleggen wordt een bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8905e-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="8905e-169">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="8905e-169">Azure Blob Storage</span></span>

<span data-ttu-id="8905e-170">Azure Blob Storage afgeschermd voorbeeld met registratie van integratie met gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="8905e-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="8905e-171">Typen beschikbare gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8905e-171">Available event types</span></span>

- <span data-ttu-id="8905e-172">**Microsoft.Storage.BlobCreated**: deze gebeurtenis treedt op wanneer een blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8905e-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="8905e-173">**Microsoft.Storage.BlobDeleted**: deze gebeurtenis treedt op wanneer een blob wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8905e-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="8905e-174">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8905e-174">Example event</span></span>

<span data-ttu-id="8905e-175">Deze voorbeeldgebeurtenis ziet u het schema van een opslag-gebeurtenis die optreedt wanneer een blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8905e-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="8905e-176">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="8905e-176">Custom Topics</span></span>

<span data-ttu-id="8905e-177">De nettolading van de gegevens van uw aangepaste gebeurtenissen wordt gedefinieerd door u en mag juiste indeling heeft JSON.</span><span class="sxs-lookup"><span data-stu-id="8905e-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="8905e-178">De gegevens van het hoogste niveau moet dezelfde velden als standaard resource gedefinieerd gebeurtenissen bevatten.</span><span class="sxs-lookup"><span data-stu-id="8905e-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="8905e-179">Bij het publiceren van gebeurtenissen naar aangepaste onderwerpen kunt u overwegen modelleren van de houder van uw gebeurtenissen voor Routering en filteren.</span><span class="sxs-lookup"><span data-stu-id="8905e-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="8905e-180">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8905e-180">Example event</span></span>

<span data-ttu-id="8905e-181">Het volgende voorbeeld ziet u een gebeurtenis voor een aangepaste onderwerp:</span><span class="sxs-lookup"><span data-stu-id="8905e-181">The following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8905e-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8905e-182">Next steps</span></span>

* <span data-ttu-id="8905e-183">Zie voor een inleiding tot gebeurtenis raster, [wat gebeurtenis raster is?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="8905e-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="8905e-184">Zie voor meer informatie over het maken van een gebeurtenis raster-abonnement, [gebeurtenis raster abonnement schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="8905e-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
