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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="35443-103">Een Event Hubs-naamruimte met een gebeurtenishub maken en Capture inschakelen met behulp van een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="35443-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="35443-104">Dit artikel laat zien hoe toouse een Azure Resource Manager-sjabloon die wordt gemaakt een naamruimte Event Hubs met een event hub-instantie en schakelt Hallo [vastleggen functie](event-hubs-capture-overview.md) voor Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="35443-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="35443-105">Hallo artikel wordt beschreven hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35443-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="35443-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="35443-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="35443-107">Dit artikel laat zien hoe toospecify dat gebeurtenissen worden vastgelegd in Azure Storage-Blobs of een Azure Data Lake Store is gebaseerd op Hallo bestemming die u kiest.</span><span class="sxs-lookup"><span data-stu-id="35443-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="35443-108">Zie [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates] voor meer informatie over het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="35443-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="35443-109">Zie [Naming Conventions][Azure Resources naming conventions] (Naamgevingsconventies) voor meer informatie over de patronen en procedures voor naamgevingsconventies van Azure Resources.</span><span class="sxs-lookup"><span data-stu-id="35443-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="35443-110">Hallo voltooid sjablonen, klikt u op Hallo GitHub-koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35443-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="35443-111">[Event hub en schakel vastleggen tooStorage sjabloon][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="35443-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="35443-112">[Event hub en schakel vastleggen tooAzure Data Lake Store-sjabloon][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="35443-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="35443-113">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="35443-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="35443-114">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="35443-114">What will you deploy?</span></span>

<span data-ttu-id="35443-115">Met deze sjabloon implementeert u een Event Hubs-naamruimte met een gebeurtenishub en schakelt u tevens [Event Hubs Cinapture](event-hubs-capture-overview.md) in.</span><span class="sxs-lookup"><span data-stu-id="35443-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="35443-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is een service die wordt gebruikt tooprovide gebeurtenissen en telemetriegegevens inkomend tooAzure op grote schaal met weinig latentie en hoge betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="35443-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="35443-117">Event Hubs vastleggen schakelt u tooautomatically leveren Hallo streaming-gegevens in Event Hubs tooAzure Blob storage of Azure Data Lake Store binnen een opgegeven periode of het interval van de grootte van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="35443-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="35443-118">Klik op Hallo knop tooenable Event Hubs vastleggen in Azure Storage te volgen:</span><span class="sxs-lookup"><span data-stu-id="35443-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="35443-119">[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="35443-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="35443-120">Klik op Hallo knop tooenable Event Hubs vastleggen in Azure Data Lake Store te volgen:</span><span class="sxs-lookup"><span data-stu-id="35443-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="35443-121">[![TooAzure implementeren](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="35443-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="35443-122">Parameters</span><span class="sxs-lookup"><span data-stu-id="35443-122">Parameters</span></span>

<span data-ttu-id="35443-123">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="35443-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="35443-124">Hallo-sjabloon bevat een sectie met de naam `Parameters` die alle Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="35443-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="35443-125">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="35443-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="35443-126">Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="35443-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="35443-127">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="35443-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="35443-128">Hallo sjabloon definieert Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="35443-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="35443-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="35443-129">eventHubNamespaceName</span></span>

<span data-ttu-id="35443-130">Hallo-naam van Hallo [Event Hubs naamruimte](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="35443-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="35443-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="35443-131">eventHubName</span></span>

<span data-ttu-id="35443-132">naam van Hallo event hub is gemaakt in Hallo Hallo [Event Hubs naamruimte](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="35443-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="35443-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="35443-133">messageRetentionInDays</span></span>

<span data-ttu-id="35443-134">Hallo aantal dagen tooretain Hallo-berichten in Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="35443-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

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

### <a name="partitioncount"></a><span data-ttu-id="35443-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="35443-135">partitionCount</span></span>

<span data-ttu-id="35443-136">Hallo aantal partities toocreate in Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="35443-136">hello number of partitions toocreate in hello event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="35443-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="35443-137">captureEnabled</span></span>

<span data-ttu-id="35443-138">Schakel vastleggen op Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="35443-138">Enable Capture on hello event hub.</span></span>

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
### <a name="captureencodingformat"></a><span data-ttu-id="35443-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="35443-139">captureEncodingFormat</span></span>

<span data-ttu-id="35443-140">Hallo-coderingsindeling u tooserialize Hallo gebeurtenisgegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="35443-140">hello encoding format you specify tooserialize hello event data.</span></span>

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

### <a name="capturetime"></a><span data-ttu-id="35443-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="35443-141">captureTime</span></span>

<span data-ttu-id="35443-142">Hallo tijdsinterval waarin Event Hubs vastleggen begint het vastleggen van Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="35443-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

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

### <a name="capturesize"></a><span data-ttu-id="35443-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="35443-143">captureSize</span></span>
<span data-ttu-id="35443-144">Hallo grootte interval waarop vastleggen begint het vastleggen van Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="35443-144">hello size interval at which Capture starts capturing hello data.</span></span>

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

###<a name="capturenameformat"></a><span data-ttu-id="35443-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="35443-145">captureNameFormat</span></span>

<span data-ttu-id="35443-146">Hallo-naamnotatie gebruikt door het vastleggen van Event Hubs toowrite hello Avro bestanden.</span><span class="sxs-lookup"><span data-stu-id="35443-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="35443-147">De indeling voor Capture moet de velden `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` en `{Second}` bevatten.</span><span class="sxs-lookup"><span data-stu-id="35443-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="35443-148">Deze velden kunnen in willekeurige volgorde worden gerangschikt, met of zonder scheidingstekens.</span><span class="sxs-lookup"><span data-stu-id="35443-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="35443-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="35443-149">apiVersion</span></span>

<span data-ttu-id="35443-150">Hallo API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="35443-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="35443-151">Gebruik Hallo parameters te volgen als u Azure Storage als de bestemming.</span><span class="sxs-lookup"><span data-stu-id="35443-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="35443-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="35443-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="35443-153">Vastleggen vereist een Azure Storage-account resource-ID tooenable tooyour vastleggen gewenst Storage-account.</span><span class="sxs-lookup"><span data-stu-id="35443-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="35443-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="35443-154">blobContainerName</span></span>

<span data-ttu-id="35443-155">Hallo blob-container in welke toocapture de gebeurtenisgegevens.</span><span class="sxs-lookup"><span data-stu-id="35443-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="35443-156">Gebruik Hallo parameters te volgen als u Azure Data Lake Store als de bestemming.</span><span class="sxs-lookup"><span data-stu-id="35443-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="35443-157">U moet machtigingen instellen op uw Data Lake Store-pad, waarin u wilt dat tooCapture Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="35443-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="35443-158">tooset machtigingen, Zie [in dit artikel](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="35443-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="35443-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="35443-159">subscriptionId</span></span>

<span data-ttu-id="35443-160">Abonnement-ID voor Hallo Event Hubs-naamruimte en de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35443-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="35443-161">Beide deze resources moeten onder Hallo dezelfde abonnements-ID.</span><span class="sxs-lookup"><span data-stu-id="35443-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="35443-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="35443-162">dataLakeAccountName</span></span>

<span data-ttu-id="35443-163">naam van de Hello Azure Data Lake Store voor Hallo gebeurtenissen vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="35443-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="35443-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="35443-164">dataLakeFolderPath</span></span>

<span data-ttu-id="35443-165">Hallo pad naar de doelmap voor Hallo gebeurtenissen vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="35443-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="35443-166">Toodeploy resources voor Azure Storage als bestemming toocaptured gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="35443-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="35443-167">Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en schakelt vastleggen tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="35443-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="35443-168">Toodeploy resources voor Azure Data Lake Store als bestemming</span><span class="sxs-lookup"><span data-stu-id="35443-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="35443-169">Hiermee maakt u een naamruimte van het type **EventHubs**, met een event hub en schakelt vastleggen tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35443-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="35443-170">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="35443-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="35443-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35443-171">PowerShell</span></span>

<span data-ttu-id="35443-172">Uw sjabloon tooenable Event Hubs vastleggen implementeren in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="35443-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="35443-173">Uw sjabloon tooenable Event Hubs vastleggen implementeren in Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="35443-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="35443-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35443-174">Azure CLI</span></span>

<span data-ttu-id="35443-175">Azure Blob Storage kiezen als doel:</span><span class="sxs-lookup"><span data-stu-id="35443-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="35443-176">Azure Data Lake Store kiezen als doel:</span><span class="sxs-lookup"><span data-stu-id="35443-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="35443-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35443-177">Next steps</span></span>

<span data-ttu-id="35443-178">U kunt ook configureren Event Hubs vastleggen via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35443-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="35443-179">Zie voor meer informatie [Azure-portal met behulp van inschakelen van Event Hubs vastleggen Hallo](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35443-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="35443-180">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35443-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="35443-181">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="35443-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="35443-182">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="35443-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="35443-183">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="35443-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
