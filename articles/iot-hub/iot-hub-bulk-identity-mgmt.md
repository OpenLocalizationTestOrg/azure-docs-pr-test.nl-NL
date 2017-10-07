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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Beheren van uw IoT Hub apparaat-id's in bulk

Elke IoT-hub heeft een id-register kunt u toocreate per apparaat resources in Hallo-service. Hallo-id-register kunt u ook toocontrol toegang toohello apparaat gerichte eindpunten. Dit artikel wordt beschreven hoe tooimport en exporteren van apparaat-id's in bulk-tooand van een id-register.

Importeren en exporteren bewerkingen plaatsvinden in de context van Hallo *taken* waarmee u tooexecute bulksgewijs servicebewerkingen op basis van een IoT-hub.

Hallo **RegistryManager** klasse bevat Hallo **ExportDevicesAsync** en **ImportDevicesAsync** methoden die gebruikmaken van Hallo **taak** Framework. Deze methoden kunnen u tooexport, importeren en synchroniseren Hallo geheel van een id-register van IoT hub.

## <a name="what-are-jobs"></a>Wat zijn taken?

Bewerkingen in het systeemregister identiteit gebruiken Hallo **taak** systeem wanneer Hallo bewerking:

* Mogelijk veel tijd in uitvoering heeft vergeleken toostandard runtime-bewerkingen.
* Retourneert een grote hoeveelheid gegevens toohello gebruiker.

In plaats van één API-aanroep nog of blokkeert op Hallo resultaat van Hallo bewerking, Hallo bewerking maakt u asynchroon een **taak** voor deze iothub. Hallo-bewerking en vervolgens onmiddellijk retourneert een **JobProperties** object.

Hallo volgende C# code fragment toont hoe toocreate een taak voor het exporteren:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> Hallo toouse **RegistryManager** klasse in uw C#-code, het toevoegen van Hallo **Microsoft.Azure.Devices** NuGet-pakket tooyour project. Hallo **RegistryManager** klasse bevindt zich in Hallo **Microsoft.Azure.Devices** naamruimte.

Kunt u Hallo **RegistryManager** tooquery Hallo status Hallo klasse **taak** Hallo geretourneerd met **JobProperties** metagegevens.

Hallo ziet volgende C#-codefragment u hoe toopoll elke vijf seconden toosee als hello taak is uitgevoerd:

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

## <a name="export-devices"></a>Exporteren van apparaten

Gebruik Hallo **ExportDevicesAsync** methode tooexport Hallo geheel van een IoT hub identiteit register tooan [Azure Storage](../storage/index.md) blob-container gebruiken een [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).

Deze methode kunt u toocreate betrouwbare back-ups van uw apparaatgegevens in een blob-container die u beheert.

Hallo **ExportDevicesAsync** methode vereist twee parameters:

* Een *tekenreeks* die een URI van een blob-container bevat. Deze URI moet een SAS-token die schrijftoegang toohello container verleent bevatten. Hallo taak maakt een blok-blob in deze container toostore Hallo geserialiseerd export-apparaatgegevens. Hallo SAS-token moet deze machtigingen zijn:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* Een *Booleaanse* die aangeeft dat als u wilt dat tooexclude verificatiesleutels uit uw gegevens exporteren. Als **false**, verificatiesleutels zijn opgenomen in de uitvoer van de export. Anders sleutels worden geëxporteerd als **null**.

Hallo ziet volgende C#-codefragment u hoe een exporttaak met apparaat verificatiesleutels in Hallo tooinitiate gegevens exporteren en vervolgens wordt gecontroleerd op voltooiing:

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

Hallo taak slaat de uitvoer in Hallo opgegeven blob-container als een blok-blob met de naam van de Hallo **devices.txt**. Hallo uitvoergegevens bestaat uit JSON-geserialiseerd apparaatgegevens, met één apparaat per regel.

Hallo toont volgende voorbeeld de uitvoergegevens Hallo:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Als een apparaat dubbele gegevens heeft, klikt u vervolgens Hallo twin gegevens ook samen met apparaatgegevens Hallo geëxporteerd. Hallo volgende voorbeeld ziet u deze indeling. Alle gegevens van Hallo 'twinETag' regel tot einde Hallo zijn twin gegevens.

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

Als u toegang krijgen gegevens in de code toothis tot moet, kunt u eenvoudig deze gegevens met behulp van Hallo deserialiseren **ExportImportDevice** klasse. Hallo ziet volgende C#-codefragment u hoe tooread apparaatgegevens die was eerder hebt geëxporteerd tooa blok-blob:

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
> U kunt ook Hallo **GetDevicesAsync** methode Hallo **RegistryManager** klasse toofetch een lijst van uw apparaten. Deze methode heeft echter een vaste limiet van 1000 op Hallo aantal apparaatobjecten die worden geretourneerd. Hallo verwacht gebruiksvoorbeeld voor Hallo **GetDevicesAsync** methode voor het opsporen van ontwikkeling scenario's tooaid is en wordt niet aanbevolen voor productieworkloads.

## <a name="import-devices"></a>Apparaten importeren

Hallo **ImportDevicesAsync** methode in Hallo **RegistryManager** klasse kunt u tooperform bulksgewijs importeren en synchroniseren van bewerkingen in een id-register van IoT hub. Zoals Hallo **ExportDevicesAsync** methode, Hallo **ImportDevicesAsync** methode maakt gebruik van Hallo **taak** framework.

Wees voorzichtig met behulp van Hallo **ImportDevicesAsync** methode omdat in toevoeging tooprovisioning nieuwe apparaten in uw id-register, kan het ook bijwerken en verwijderen van bestaande apparaten.

> [!WARNING]
> Een importbewerking kan niet ongedaan worden gemaakt. Altijd back-up van uw bestaande gegevens met behulp van Hallo **ExportDevicesAsync** methode tooanother blob-container voordat u bulksgewijs tooyour id-register wordt gewijzigd.

Hallo **ImportDevicesAsync** methode heeft twee parameters:

* Een *tekenreeks* die een URI van bevat een [Azure Storage](../storage/index.md) blob-container toouse als *invoer* toohello taak. Deze URI moet een SAS-token die leestoegang toohello container verleent bevatten. Deze container moet een blob met de naam van de Hallo bevatten **devices.txt** die Hallo geserialiseerd apparaat gegevens tooimport in de register-id's bevat. Hallo importgegevens moet bevatten apparaatgegevens in Hallo dezelfde JSON die Hallo opmaken **ExportImportDevice** taak wordt gebruikt bij het maken van een **devices.txt** blob. Hallo SAS-token moet deze machtigingen zijn:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* Een *tekenreeks* die een URI van bevat een [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob-container toouse als *uitvoer* uit Hallo-taak. Hallo taak maakt een blok-blob in deze container toostore informatie over de fout van Hallo voltooid importeren **taak**. Hallo SAS-token moet deze machtigingen zijn:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> Hallo twee parameters kunnen verwijzen toohello dezelfde blob-container. de afzonderlijke parameters Hallo inschakelen gewoon meer controle over uw gegevens als Hallo uitvoer container aanvullende machtigingen vereist.

Hallo volgende C# code fragment toont hoe tooinitiate een import-taak:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Deze methode kan ook worden gebruikt tooimport Hallo gegevens voor Hallo apparaat twin. Hallo-indeling voor gegevensinvoer Hallo Hallo is dezelfde als Hallo-indeling wordt weergegeven in Hallo **ExportDevicesAsync** sectie. Op deze manier kunt u Hallo geëxporteerd gegevens opnieuw importeren. Hallo **$metadata** is optioneel.

## <a name="import-behavior"></a>Gedrag importeren

U kunt Hallo **ImportDevicesAsync** methode tooperform Hallo volgende bulksgewijs bewerkingen in de register-id's:

* Registratie van nieuwe apparaten bulksgewijs
* Bulksgewijs verwijderingen van bestaande apparaten
* Bulksgewijs statuswijzigingen (in- of uitschakelen van apparaten)
* Toewijzing van nieuwe apparaten verificatiesleutels bulksgewijs
* Bulksgewijs automatisch opnieuw genereren van sleutels voor apparaat-verificatie
* Bulk-update van dubbele gegevens

U kunt een combinatie van Hallo voorafgaand aan activiteiten binnen één uitvoeren **ImportDevicesAsync** aanroepen. Bijvoorbeeld, kunt u nieuwe apparaten registreren en verwijderen of bijwerken van bestaande apparaten op Hallo hetzelfde moment. Wanneer gebruikt samen met de Hallo **ExportDevicesAsync** methode, kunt u al uw apparaten volledig migreren vanaf een IoT hub tooanother.

Als het importbestand Hallo twin metagegevens bevat, overschrijft deze metagegevens Hallo bestaande twin metagegevens. Als het Hallo-importbestand bevat geen twin metagegevens, klikt u vervolgens alleen Hallo `lastUpdateTime` metagegevens worden bijgewerkt met Hallo huidige tijd.

Gebruik Hallo optionele **ImportMode %** eigenschap uit de serialisatiegegevens van Hallo importeren voor elk apparaat toocontrol Hallo importeren proces per apparaat. Hallo **ImportMode %** eigenschap heeft Hallo volgende opties:

| ImportMode % | Beschrijving |
| --- | --- |
| **createOrUpdate** |Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven. <br/>Als Hallo apparaat al bestaat, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens zonder inachtneming van toohello **ETag** waarde. <br> Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven. Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat. Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven. |
| **maken** |Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven. <br/>Als Hallo apparaat al bestaat, is een fout toohello logboekbestand geschreven. <br> Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven. Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat. Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven. |
| **bijwerken** |Als er al een apparaat met Hallo opgegeven bestaat **id**, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens zonder inachtneming van toohello **ETag** waarde. <br/>Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven. |
| **updateIfMatchETag** |Als er al een apparaat met Hallo opgegeven bestaat **id**, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens alleen als er een **ETag** overeenkomen. <br/>Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven. <br/>Als er een **ETag** niet-overeenkomende, een fout toohello logboekbestand geschreven. |
| **createOrUpdateIfMatchETag** |Als een apparaat niet Hello opgegeven bestaat **id**, het zojuist is ingeschreven. <br/>Als Hallo apparaat al bestaat, bestaande gegevens wordt overschreven met Hallo opgegeven invoergegevens alleen als er een **ETag** overeenkomen. <br/>Als er een **ETag** niet-overeenkomende, een fout toohello logboekbestand geschreven. <br> Hallo-gebruiker kan eventueel twin gegevens samen met de Hallo apparaatgegevens opgeven. Hallo twin van etag, wordt indien opgegeven, verwerkt onafhankelijk van etag Hallo-apparaat. Als er niet overeen met de Hallo bestaande twin etag komt, is een fout toohello logboekbestand geschreven. |
| **verwijderen** |Als er al een apparaat met Hallo opgegeven bestaat **id**, wordt deze verwijderd zonder inachtneming van toohello **ETag** waarde. <br/>Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven. |
| **deleteIfMatchETag** |Als er al een apparaat met Hallo opgegeven bestaat **id**, wordt verwijderd alleen als er een **ETag** overeenkomen. Als het Hallo-apparaat bestaat niet, is een fout toohello logboekbestand geschreven. <br/>Als er een ETag komt niet overeen, is een fout toohello logboekbestand geschreven. |

> [!NOTE]
> Als de serialisatiegegevens Hallo geen expliciet definieert een **ImportMode %** vlag voor een apparaat, wordt standaard te**createOrUpdate** tijdens Hallo importbewerking.

## <a name="import-devices-example--bulk-device-provisioning"></a>Voorbeeld van de apparaten te importeren: bulksgewijs apparaten inrichten

Hallo volgende C# codevoorbeeld ziet u hoe toogenerate meerdere apparaat-id's die:

* Verificatiesleutels bevatten.
* Schrijf dit apparaat informatie tooa blok-blob.
* Hallo apparaten in register Hallo-id's worden geïmporteerd.

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

## <a name="import-devices-example--bulk-deletion"></a>Importeren van apparaten voorbeeld – bulksgewijs verwijderen

Hallo volgende codevoorbeeld ziet u hoe toodelete Hallo apparaten die u hebt toegevoegd met behulp van de vorige codevoorbeeld Hallo:

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

## <a name="get-hello-container-sas-uri"></a>Hallo-container SAS URI ophalen

Hallo volgende codevoorbeeld ziet u hoe toogenerate een [SAS-URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) met lezen, schrijven en verwijderen van machtigingen voor een blob-container:

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

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u geleerd hoe tooperform bulksgewijs bewerkingen op Hallo identiteitenregister van een IoT-hub. Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:

* [IoT Hub metrische gegevens][lnk-metrics]
* [Bewerkingen controleren][lnk-monitor]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met IoT rand][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
