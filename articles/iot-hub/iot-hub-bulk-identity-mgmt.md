---
title: exporteren van Azure IoT Hub apparaat-id's aaaImport | Microsoft Docs
description: Hoe toouse hello Azure IoT service SDK tooperform bewerkingen op Hallo identiteit register tooimport bulksgewijs en exporteren van apparaat-id's. Importbewerkingen kunnen u toocreate, update en delete apparaat-id's in bulk.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="25ff9-104">Beheren van uw IoT Hub apparaat-id's in bulk</span><span class="sxs-lookup"><span data-stu-id="25ff9-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="25ff9-105">Elke IoT-hub heeft een id-register kunt u toocreate per apparaat resources in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="25ff9-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="25ff9-106">Hallo-id-register kunt u ook toocontrol toegang toohello apparaat gerichte eindpunten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="25ff9-107">Dit artikel wordt beschreven hoe tooimport en exporteren van apparaat-id's in bulk-tooand van een id-register.</span><span class="sxs-lookup"><span data-stu-id="25ff9-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="25ff9-108">Importeren en exporteren bewerkingen plaatsvinden in de context van Hallo *taken* waarmee u tooexecute bulksgewijs servicebewerkingen op basis van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="25ff9-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="25ff9-109">Hallo **RegistryManager** klasse bevat Hallo **ExportDevicesAsync** en **ImportDevicesAsync** methoden die gebruikmaken van Hallo **taak** Framework.</span><span class="sxs-lookup"><span data-stu-id="25ff9-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="25ff9-110">Deze methoden kunnen u tooexport, importeren en synchroniseren Hallo geheel van een id-register van IoT hub.</span><span class="sxs-lookup"><span data-stu-id="25ff9-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="25ff9-111">Wat zijn taken?</span><span class="sxs-lookup"><span data-stu-id="25ff9-111">What are jobs?</span></span>

<span data-ttu-id="25ff9-112">Bewerkingen in het systeemregister identiteit gebruiken Hallo **taak** systeem wanneer Hallo bewerking:</span><span class="sxs-lookup"><span data-stu-id="25ff9-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="25ff9-113">Mogelijk veel tijd in uitvoering heeft vergeleken toostandard runtime-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="25ff9-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="25ff9-114">Retourneert een grote hoeveelheid gegevens toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="25ff9-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="25ff9-115">In plaats van één API-aanroep nog of blokkeert op Hallo resultaat van Hallo bewerking, Hallo bewerking maakt u asynchroon een **taak** voor deze iothub.</span><span class="sxs-lookup"><span data-stu-id="25ff9-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="25ff9-116">Hallo-bewerking en vervolgens onmiddellijk retourneert een **JobProperties** object.</span><span class="sxs-lookup"><span data-stu-id="25ff9-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="25ff9-117">Hallo volgende C# code fragment toont hoe toocreate een taak voor het exporteren:</span><span class="sxs-lookup"><span data-stu-id="25ff9-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="25ff9-118">Hallo toouse **RegistryManager** klasse in uw C#-code, het toevoegen van Hallo **Microsoft.Azure.Devices** NuGet-pakket tooyour project.</span><span class="sxs-lookup"><span data-stu-id="25ff9-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="25ff9-119">Hallo **RegistryManager** klasse bevindt zich in Hallo **Microsoft.Azure.Devices** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="25ff9-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="25ff9-120">Kunt u Hallo **RegistryManager** tooquery Hallo status Hallo klasse **taak** Hallo geretourneerd met **JobProperties** metagegevens.</span><span class="sxs-lookup"><span data-stu-id="25ff9-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="25ff9-121">Hallo ziet volgende C#-codefragment u hoe toopoll elke vijf seconden toosee als hello taak is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="25ff9-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="25ff9-122">Exporteren van apparaten</span><span class="sxs-lookup"><span data-stu-id="25ff9-122">Export devices</span></span>

<span data-ttu-id="25ff9-123">Gebruik Hallo **ExportDevicesAsync** methode tooexport Hallo geheel van een IoT hub identiteit register tooan [Azure Storage](../storage/index.md) blob-container gebruiken een [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="25ff9-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="25ff9-124">Deze methode kunt u toocreate betrouwbare back-ups van uw apparaatgegevens in een blob-container die u beheert.</span><span class="sxs-lookup"><span data-stu-id="25ff9-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="25ff9-125">Hallo **ExportDevicesAsync** methode vereist twee parameters:</span><span class="sxs-lookup"><span data-stu-id="25ff9-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="25ff9-126">Een *tekenreeks* die een URI van een blob-container bevat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="25ff9-127">Deze URI moet een SAS-token die schrijftoegang toohello container verleent bevatten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="25ff9-128">Hallo taak maakt een blok-blob in deze container toostore Hallo geserialiseerd export-apparaatgegevens.</span><span class="sxs-lookup"><span data-stu-id="25ff9-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="25ff9-129">Hallo SAS-token moet deze machtigingen zijn:</span><span class="sxs-lookup"><span data-stu-id="25ff9-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="25ff9-130">Een *Booleaanse* die aangeeft dat als u wilt dat tooexclude verificatiesleutels uit uw gegevens exporteren.</span><span class="sxs-lookup"><span data-stu-id="25ff9-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="25ff9-131">Als **false**, verificatiesleutels zijn opgenomen in de uitvoer van de export.</span><span class="sxs-lookup"><span data-stu-id="25ff9-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="25ff9-132">Anders sleutels worden geëxporteerd als **null**.</span><span class="sxs-lookup"><span data-stu-id="25ff9-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="25ff9-133">Hallo ziet volgende C#-codefragment u hoe een exporttaak met apparaat verificatiesleutels in Hallo tooinitiate gegevens exporteren en vervolgens wordt gecontroleerd op voltooiing:</span><span class="sxs-lookup"><span data-stu-id="25ff9-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="25ff9-134">Hallo taak slaat de uitvoer in Hallo opgegeven blob-container als een blok-blob met de naam van de Hallo **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="25ff9-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="25ff9-135">Hallo uitvoergegevens bestaat uit JSON-geserialiseerd apparaatgegevens, met één apparaat per regel.</span><span class="sxs-lookup"><span data-stu-id="25ff9-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="25ff9-136">Hallo toont volgende voorbeeld de uitvoergegevens Hallo:</span><span class="sxs-lookup"><span data-stu-id="25ff9-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Als een apparaat dubbele gegevens heeft, klikt u vervolgens Hallo twin gegevens ook samen met apparaatgegevens Hallo geëxporteerd. Hallo volgende voorbeeld ziet u deze indeling. <span data-ttu-id="25ff9-139">Alle gegevens van Hallo 'twinETag' regel tot einde Hallo zijn twin gegevens.</span><span class="sxs-lookup"><span data-stu-id="25ff9-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="25ff9-140">Als u toegang krijgen gegevens in de code toothis tot moet, kunt u eenvoudig deze gegevens met behulp van Hallo deserialiseren **ExportImportDevice** klasse.</span><span class="sxs-lookup"><span data-stu-id="25ff9-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="25ff9-141">Hallo ziet volgende C#-codefragment u hoe tooread apparaatgegevens die was eerder hebt geëxporteerd tooa blok-blob:</span><span class="sxs-lookup"><span data-stu-id="25ff9-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="25ff9-142">U kunt ook Hallo **GetDevicesAsync** methode Hallo **RegistryManager** klasse toofetch een lijst van uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="25ff9-143">Deze methode heeft echter een vaste limiet van 1000 op Hallo aantal apparaatobjecten die worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="25ff9-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="25ff9-144">Hallo verwacht gebruiksvoorbeeld voor Hallo **GetDevicesAsync** methode voor het opsporen van ontwikkeling scenario's tooaid is en wordt niet aanbevolen voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="25ff9-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="25ff9-145">Apparaten importeren</span><span class="sxs-lookup"><span data-stu-id="25ff9-145">Import devices</span></span>

<span data-ttu-id="25ff9-146">Hallo **ImportDevicesAsync** methode in Hallo **RegistryManager** klasse kunt u tooperform bulksgewijs importeren en synchroniseren van bewerkingen in een id-register van IoT hub.</span><span class="sxs-lookup"><span data-stu-id="25ff9-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="25ff9-147">Zoals Hallo **ExportDevicesAsync** methode, Hallo **ImportDevicesAsync** methode maakt gebruik van Hallo **taak** framework.</span><span class="sxs-lookup"><span data-stu-id="25ff9-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="25ff9-148">Wees voorzichtig met behulp van Hallo **ImportDevicesAsync** methode omdat in toevoeging tooprovisioning nieuwe apparaten in uw id-register, kan het ook bijwerken en verwijderen van bestaande apparaten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="25ff9-149">Een importbewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25ff9-149">An import operation cannot be undone.</span></span> <span data-ttu-id="25ff9-150">Altijd back-up van uw bestaande gegevens met behulp van Hallo **ExportDevicesAsync** methode tooanother blob-container voordat u bulksgewijs tooyour id-register wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="25ff9-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="25ff9-151">Hallo **ImportDevicesAsync** methode heeft twee parameters:</span><span class="sxs-lookup"><span data-stu-id="25ff9-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="25ff9-152">Een *tekenreeks* die een URI van bevat een [Azure Storage](../storage/index.md) blob-container toouse als *invoer* toohello taak.</span><span class="sxs-lookup"><span data-stu-id="25ff9-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="25ff9-153">Deze URI moet een SAS-token die leestoegang toohello container verleent bevatten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="25ff9-154">Deze container moet een blob met de naam van de Hallo bevatten **devices.txt** die Hallo geserialiseerd apparaat gegevens tooimport in de register-id's bevat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="25ff9-155">Hallo importgegevens moet bevatten apparaatgegevens in Hallo dezelfde JSON die Hallo opmaken **ExportImportDevice** taak wordt gebruikt bij het maken van een **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="25ff9-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="25ff9-156">Hallo SAS-token moet deze machtigingen zijn:</span><span class="sxs-lookup"><span data-stu-id="25ff9-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="25ff9-157">Een *tekenreeks* die een URI van bevat een [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob-container toouse als *uitvoer* uit Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="25ff9-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="25ff9-158">Hallo taak maakt een blok-blob in deze container toostore informatie over de fout van Hallo voltooid importeren **taak**.</span><span class="sxs-lookup"><span data-stu-id="25ff9-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="25ff9-159">Hallo SAS-token moet deze machtigingen zijn:</span><span class="sxs-lookup"><span data-stu-id="25ff9-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="25ff9-160">Hallo twee parameters kunnen verwijzen toohello dezelfde blob-container.</span><span class="sxs-lookup"><span data-stu-id="25ff9-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="25ff9-161">de afzonderlijke parameters Hallo inschakelen gewoon meer controle over uw gegevens als Hallo uitvoer container aanvullende machtigingen vereist.</span><span class="sxs-lookup"><span data-stu-id="25ff9-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="25ff9-162">Hallo volgende C# code fragment toont hoe tooinitiate een import-taak:</span><span class="sxs-lookup"><span data-stu-id="25ff9-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="25ff9-163">Deze methode kan ook worden gebruikt tooimport Hallo gegevens voor Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="25ff9-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="25ff9-164">Hallo-indeling voor gegevensinvoer Hallo Hallo is dezelfde als Hallo-indeling wordt weergegeven in Hallo **ExportDevicesAsync** sectie.</span><span class="sxs-lookup"><span data-stu-id="25ff9-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="25ff9-165">Op deze manier kunt u Hallo geëxporteerd gegevens opnieuw importeren.</span><span class="sxs-lookup"><span data-stu-id="25ff9-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="25ff9-166">Hallo **$metadata** is optioneel.</span><span class="sxs-lookup"><span data-stu-id="25ff9-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="25ff9-167">Gedrag importeren</span><span class="sxs-lookup"><span data-stu-id="25ff9-167">Import behavior</span></span>

<span data-ttu-id="25ff9-168">U kunt Hallo **ImportDevicesAsync** methode tooperform Hallo volgende bulksgewijs bewerkingen in de register-id's:</span><span class="sxs-lookup"><span data-stu-id="25ff9-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="25ff9-169">Registratie van nieuwe apparaten bulksgewijs</span><span class="sxs-lookup"><span data-stu-id="25ff9-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="25ff9-170">Bulksgewijs verwijderingen van bestaande apparaten</span><span class="sxs-lookup"><span data-stu-id="25ff9-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="25ff9-171">Bulksgewijs statuswijzigingen (in- of uitschakelen van apparaten)</span><span class="sxs-lookup"><span data-stu-id="25ff9-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="25ff9-172">Toewijzing van nieuwe apparaten verificatiesleutels bulksgewijs</span><span class="sxs-lookup"><span data-stu-id="25ff9-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="25ff9-173">Bulksgewijs automatisch opnieuw genereren van sleutels voor apparaat-verificatie</span><span class="sxs-lookup"><span data-stu-id="25ff9-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="25ff9-174">Bulk-update van dubbele gegevens</span><span class="sxs-lookup"><span data-stu-id="25ff9-174">Bulk update of twin data</span></span>

<span data-ttu-id="25ff9-175">U kunt een combinatie van Hallo voorafgaand aan activiteiten binnen één uitvoeren **ImportDevicesAsync** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="25ff9-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="25ff9-176">Bijvoorbeeld, kunt u nieuwe apparaten registreren en verwijderen of bijwerken van bestaande apparaten op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="25ff9-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="25ff9-177">Wanneer gebruikt samen met de Hallo **ExportDevicesAsync** methode, kunt u al uw apparaten volledig migreren vanaf een IoT hub tooanother.</span><span class="sxs-lookup"><span data-stu-id="25ff9-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="25ff9-178">Als het importbestand Hallo twin metagegevens bevat, overschrijft deze metagegevens Hallo bestaande twin metagegevens.</span><span class="sxs-lookup"><span data-stu-id="25ff9-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="25ff9-179">Als het Hallo-importbestand bevat geen twin metagegevens, klikt u vervolgens alleen Hallo `lastUpdateTime` metagegevens worden bijgewerkt met Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="25ff9-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="25ff9-180">Gebruik Hallo optionele **ImportMode %** eigenschap uit de serialisatiegegevens van Hallo importeren voor elk apparaat toocontrol Hallo importeren proces per apparaat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="25ff9-181">Hallo **ImportMode %** eigenschap heeft Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="25ff9-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="25ff9-182">ImportMode %</span><span class="sxs-lookup"><span data-stu-id="25ff9-182">importMode</span></span> | <span data-ttu-id="25ff9-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="25ff9-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25ff9-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="25ff9-184">**createOrUpdate**</span></span> |<span data-ttu-id="25ff9-185">Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="25ff9-186">Als Hallo apparaat al bestaat, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens zonder inachtneming van toohello **ETag** waarde.</span><span class="sxs-lookup"><span data-stu-id="25ff9-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="25ff9-187">Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="25ff9-188">Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="25ff9-189">Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-190">**maken**</span><span class="sxs-lookup"><span data-stu-id="25ff9-190">**create**</span></span> |<span data-ttu-id="25ff9-191">Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="25ff9-192">Als Hallo apparaat al bestaat, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="25ff9-193">Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="25ff9-194">Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="25ff9-195">Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-196">**bijwerken**</span><span class="sxs-lookup"><span data-stu-id="25ff9-196">**update**</span></span> |<span data-ttu-id="25ff9-197">Als er al een apparaat met Hallo opgegeven bestaat **id**, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens zonder inachtneming van toohello **ETag** waarde.</span><span class="sxs-lookup"><span data-stu-id="25ff9-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="25ff9-198">Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="25ff9-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="25ff9-200">Als er al een apparaat met Hallo opgegeven bestaat **id**, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens alleen als er een **ETag** overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="25ff9-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="25ff9-201">Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="25ff9-202">Als er een **ETag** niet-overeenkomende, een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="25ff9-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="25ff9-204">Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="25ff9-205">Als Hallo apparaat al bestaat, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens alleen als er een **ETag** overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="25ff9-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="25ff9-206">Als er een **ETag** niet-overeenkomende, een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="25ff9-207">Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="25ff9-208">Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="25ff9-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="25ff9-209">Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-210">**verwijderen**</span><span class="sxs-lookup"><span data-stu-id="25ff9-210">**delete**</span></span> |<span data-ttu-id="25ff9-211">Als er al een apparaat met Hallo opgegeven bestaat **id**, wordt deze verwijderd zonder inachtneming van toohello **ETag** waarde.</span><span class="sxs-lookup"><span data-stu-id="25ff9-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="25ff9-212">Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="25ff9-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="25ff9-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="25ff9-214">Als er al een apparaat met Hallo opgegeven bestaat **id**, wordt verwijderd alleen als er een **ETag** overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="25ff9-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="25ff9-215">Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="25ff9-216">Als er een ETag komt niet overeen, is een fout toohello logboekbestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="25ff9-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="25ff9-217">Als de serialisatiegegevens Hallo geen expliciet definieert een **ImportMode %** vlag voor een apparaat, wordt standaard te**createOrUpdate** tijdens Hallo importbewerking.</span><span class="sxs-lookup"><span data-stu-id="25ff9-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="25ff9-218">Voorbeeld van de apparaten te importeren: bulksgewijs apparaten inrichten</span><span class="sxs-lookup"><span data-stu-id="25ff9-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="25ff9-219">Hallo volgende C# codevoorbeeld ziet u hoe toogenerate meerdere apparaat-id's die:</span><span class="sxs-lookup"><span data-stu-id="25ff9-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="25ff9-220">Verificatiesleutels bevatten.</span><span class="sxs-lookup"><span data-stu-id="25ff9-220">Include authentication keys.</span></span>
* <span data-ttu-id="25ff9-221">Schrijf dit apparaat informatie tooa blok-blob.</span><span class="sxs-lookup"><span data-stu-id="25ff9-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="25ff9-222">Hallo apparaten in register Hallo-id's worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="25ff9-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="25ff9-223">Importeren van apparaten voorbeeld – bulksgewijs verwijderen</span><span class="sxs-lookup"><span data-stu-id="25ff9-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="25ff9-224">Hallo volgende codevoorbeeld ziet u hoe toodelete Hallo apparaten die u hebt toegevoegd met behulp van de vorige codevoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="25ff9-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="25ff9-225">Hallo-container SAS URI ophalen</span><span class="sxs-lookup"><span data-stu-id="25ff9-225">Get hello container SAS URI</span></span>

<span data-ttu-id="25ff9-226">Hallo volgende codevoorbeeld ziet u hoe toogenerate een [SAS-URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) met lezen, schrijven en verwijderen van machtigingen voor een blob-container:</span><span class="sxs-lookup"><span data-stu-id="25ff9-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="25ff9-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25ff9-227">Next steps</span></span>

<span data-ttu-id="25ff9-228">In dit artikel hebt u geleerd hoe tooperform bulksgewijs bewerkingen op Hallo identiteitenregister van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="25ff9-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="25ff9-229">Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="25ff9-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="25ff9-230">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="25ff9-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="25ff9-231">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="25ff9-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="25ff9-232">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="25ff9-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="25ff9-233">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="25ff9-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="25ff9-234">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="25ff9-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
