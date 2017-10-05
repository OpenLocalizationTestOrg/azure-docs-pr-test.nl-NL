---
title: Azure IoT Hub-bestand uploaden begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - gebruik de functie voor het laden van bestand van IoT Hub voor het beheren van uploaden van van een apparaat aan een Azure-opslag-blob-container bestanden.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="940de-103">Uploaden van bestanden met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="940de-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="940de-104">Zoals beschreven in de [IoT-hubeindpunten] [ lnk-endpoints] artikel, een apparaat kunt starten uploaden van een bestand met het verzenden van een melding via een apparaat gerichte-eindpunt (**/devices/ {deviceId} /bestanden**).</span><span class="sxs-lookup"><span data-stu-id="940de-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="940de-105">Wanneer een apparaat een melding van IoT Hub een upload is voltooid, IoT Hub verzendt een bericht op bestand uploaden via de **/messages/servicebound/filenotifications** gerichte service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="940de-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="940de-106">In plaats van het uitgeven van de berichten via IoT Hub zelf fungeert IoT-Hub in plaats daarvan als een dispatcher op een gekoppelde Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="940de-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="940de-107">Een apparaat vraagt een token voor de opslag van IoT-Hub die specifiek is voor het bestand dat het apparaat wenst te uploaden.</span><span class="sxs-lookup"><span data-stu-id="940de-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="940de-108">Het apparaat gebruikmaakt van de SAS-URI van het bestand te uploaden naar de opslag en wanneer het uploaden voltooid is het apparaat een melding van voltooiing naar IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="940de-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="940de-109">IoT Hub controleert het bestand te uploaden is voltooid en vervolgens een melding van bestand uploaden toegevoegd aan het meldingseindpunt service gerichte-bestand.</span><span class="sxs-lookup"><span data-stu-id="940de-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="940de-110">Voordat u een bestand naar IoT Hub vanaf een apparaat uploadt, moet u uw hub door configureren [koppelen van een Azure Storage] [ lnk-associate-storage] account toe aan het.</span><span class="sxs-lookup"><span data-stu-id="940de-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="940de-111">Uw apparaat kunt vervolgens [initialiseren van een upload] [ lnk-initialize] en vervolgens [IoT-hub in kennis] [ lnk-notify] wanneer het uploaden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="940de-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="940de-112">Eventueel, wanneer een apparaat een melding van IoT Hub het uploaden is voltooid, de service kan genereren een [Meldingsbericht][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="940de-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="940de-113">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="940de-113">When to use</span></span>

<span data-ttu-id="940de-114">Uploaden bestand gebruiken voor het verzenden van media-bestanden en grote telemetrie batches geüpload door afwisselend verbonden apparaten of gecomprimeerd om bandbreedte besparen.</span><span class="sxs-lookup"><span data-stu-id="940de-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="940de-115">Raadpleeg [apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="940de-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="940de-116">Een Azure Storage-account koppelen met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="940de-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="940de-117">Voor het gebruik van de functionaliteit voor het uploaden van bestanden, moet u eerst een Azure Storage-account koppelen aan de IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="940de-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="940de-118">U kunt deze taak uitvoeren via de [Azure-portal][lnk-management-portal], of via een programma via de [resourceprovider IoT Hub REST-API's] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="940de-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="940de-119">Zodra u hebt een Azure Storage-account gekoppeld aan uw IoT-Hub, stuurt de service een SAS-URI op een apparaat wanneer het apparaat een aanvraag voor het uploaden van bestand initieert.</span><span class="sxs-lookup"><span data-stu-id="940de-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="940de-120">De [Azure IoT SDK's] [ lnk-sdks] automatisch bij het ophalen van de SAS-URI, het bestand uploadt en IoT-Hub van het uploaden van een voltooide verwittigen verwerken.</span><span class="sxs-lookup"><span data-stu-id="940de-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="940de-121">Initialiseren van een bestand is geüpload</span><span class="sxs-lookup"><span data-stu-id="940de-121">Initialize a file upload</span></span>
<span data-ttu-id="940de-122">IoT Hub heeft een eindpunt specifiek voor apparaten om aan te vragen van een SAS-URI voor de opslag van een bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="940de-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="940de-123">Voor het initiëren van het uploadproces bestand, het apparaat verzendt een POST-aanvraag voor `{iot hub}.azure-devices.net/devices/{deviceId}/files` met de volgende JSON-hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="940de-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="940de-124">IoT Hub retourneert de volgende gegevens, het apparaat gebruikmaakt van het bestand te uploaden:</span><span class="sxs-lookup"><span data-stu-id="940de-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="940de-125">Afgeschafte: het uploaden van een bestand met een GET initialiseren</span><span class="sxs-lookup"><span data-stu-id="940de-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="940de-126">Deze sectie beschrijft afgeschafte functionaliteit voor het ontvangen van een SAS-URI van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="940de-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="940de-127">Gebruik de POST-methode die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="940de-127">Use the POST method described previously.</span></span>

<span data-ttu-id="940de-128">IoT Hub heeft twee REST-eindpunten voor de ondersteuning van bestand is geüpload, een voor de SAS-URI voor opslag en de andere op de hoogte van de IoT-hub van het uploaden van een voltooide wilt ophalen.</span><span class="sxs-lookup"><span data-stu-id="940de-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="940de-129">Het apparaat het uploadproces bestand door een GET te sturen naar de IoT-hub aan initieert `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="940de-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="940de-130">De IoT-hub als resultaat:</span><span class="sxs-lookup"><span data-stu-id="940de-130">The IoT hub returns:</span></span>

* <span data-ttu-id="940de-131">Een SAS-URI specifiek zijn voor het bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="940de-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="940de-132">Een correlatie-ID moet worden gebruikt wanneer het uploaden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="940de-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="940de-133">Melding van IoT Hub een voltooide bestand is geüpload</span><span class="sxs-lookup"><span data-stu-id="940de-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="940de-134">Het apparaat is verantwoordelijk voor het uploaden van het bestand naar de opslag met behulp van de Azure-opslag-SDK's.</span><span class="sxs-lookup"><span data-stu-id="940de-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="940de-135">Wanneer het uploaden voltooid is, het apparaat verzendt een POST-aanvraag voor `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` met de volgende JSON-hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="940de-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="940de-136">De waarde van `isSuccess` wordt een Boolean die aangeeft of het bestand is geüpload.</span><span class="sxs-lookup"><span data-stu-id="940de-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="940de-137">De statuscode voor `statusCode` is de status voor het uploaden van het bestand naar de opslag, en de `statusDescription` komt overeen met de `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="940de-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="940de-138">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="940de-138">Reference topics:</span></span>

<span data-ttu-id="940de-139">De volgende onderwerpen met naslaginformatie bieden u meer informatie over het uploaden van bestanden van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="940de-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="940de-140">Bestand uploaden meldingen</span><span class="sxs-lookup"><span data-stu-id="940de-140">File upload notifications</span></span>

<span data-ttu-id="940de-141">Wanneer een apparaat een melding van IoT Hub een upload is voltooid, kunt IoT Hub eventueel genereren in een bericht op dat de locatie van de naam en de opslag van het bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="940de-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="940de-142">Zoals uitgelegd in [eindpunten][lnk-endpoints], IoT Hub biedt bestand uploaden meldingen via een gerichte service-eindpunt (**/messages/servicebound/fileuploadnotifications**) Als berichten.</span><span class="sxs-lookup"><span data-stu-id="940de-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="940de-143">De receive-semantiek voor het bestand uploaden meldingen zijn hetzelfde als voor cloud-naar-apparaat-berichten en hebben dezelfde [bericht lifecycle][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="940de-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="940de-144">Elk bericht opgehaald uit het bestand uploaden-meldingseindpunt is een JSON-record met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="940de-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="940de-145">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="940de-145">Property</span></span> | <span data-ttu-id="940de-146">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="940de-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="940de-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="940de-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="940de-148">De tijdstempel die aangeeft wanneer de melding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="940de-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="940de-149">Apparaat-id</span><span class="sxs-lookup"><span data-stu-id="940de-149">DeviceId</span></span> |<span data-ttu-id="940de-150">**DeviceId** van het apparaat waarop het bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="940de-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="940de-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="940de-151">BlobUri</span></span> |<span data-ttu-id="940de-152">De URI van het geüploade bestand.</span><span class="sxs-lookup"><span data-stu-id="940de-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="940de-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="940de-153">BlobName</span></span> |<span data-ttu-id="940de-154">Naam van het geüploade bestand.</span><span class="sxs-lookup"><span data-stu-id="940de-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="940de-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="940de-155">LastUpdatedTime</span></span> |<span data-ttu-id="940de-156">De tijdstempel die aangeeft wanneer het bestand het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="940de-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="940de-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="940de-157">BlobSizeInBytes</span></span> |<span data-ttu-id="940de-158">Grootte van het geüploade bestand.</span><span class="sxs-lookup"><span data-stu-id="940de-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="940de-159">**Voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="940de-159">**Example**.</span></span> <span data-ttu-id="940de-160">Dit voorbeeld toont de hoofdtekst van een bestand uploaden een melding.</span><span class="sxs-lookup"><span data-stu-id="940de-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="940de-161">Bestand uploaden meldingsopties configuratie</span><span class="sxs-lookup"><span data-stu-id="940de-161">File upload notification configuration options</span></span>

<span data-ttu-id="940de-162">Elke IoT-hub toont de volgende configuratieopties voor bestand uploaden meldingen:</span><span class="sxs-lookup"><span data-stu-id="940de-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="940de-163">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="940de-163">Property</span></span> | <span data-ttu-id="940de-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="940de-164">Description</span></span> | <span data-ttu-id="940de-165">Bereik en standaard</span><span class="sxs-lookup"><span data-stu-id="940de-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="940de-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="940de-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="940de-167">Bepaalt of meldingen van bestand uploaden naar het eindpunt van de meldingen bestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="940de-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="940de-168">BOOL.</span><span class="sxs-lookup"><span data-stu-id="940de-168">Bool.</span></span> <span data-ttu-id="940de-169">Standaard: True.</span><span class="sxs-lookup"><span data-stu-id="940de-169">Default: True.</span></span> |
| <span data-ttu-id="940de-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="940de-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="940de-171">Standaard-TTL voor meldingen van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="940de-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="940de-172">ISO_8601 interval maximaal 48 uur (minimaal 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="940de-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="940de-173">Standaardwaarde: 1 uur.</span><span class="sxs-lookup"><span data-stu-id="940de-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="940de-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="940de-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="940de-175">De duur van de vergrendeling voor de wachtrij bestand uploaden meldingen.</span><span class="sxs-lookup"><span data-stu-id="940de-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="940de-176">5-300 seconden (minimaal 5 seconden).</span><span class="sxs-lookup"><span data-stu-id="940de-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="940de-177">Standaard: 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="940de-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="940de-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="940de-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="940de-179">Levering van het maximum aantal voor het bestand uploaden meldingswachtrij.</span><span class="sxs-lookup"><span data-stu-id="940de-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="940de-180">1 tot 100.</span><span class="sxs-lookup"><span data-stu-id="940de-180">1 to 100.</span></span> <span data-ttu-id="940de-181">Standaard: 100.</span><span class="sxs-lookup"><span data-stu-id="940de-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="940de-182">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="940de-182">Additional reference material</span></span>

<span data-ttu-id="940de-183">Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="940de-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="940de-184">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="940de-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="940de-185">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijving van de quota en beperking gedrag die betrekking hebben op de service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="940de-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="940de-186">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] geeft een lijst van de verschillende SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub-taal.</span><span class="sxs-lookup"><span data-stu-id="940de-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="940de-187">[IoT Hub-querytaal] [ lnk-query] beschrijft de querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.</span><span class="sxs-lookup"><span data-stu-id="940de-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="940de-188">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="940de-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="940de-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="940de-189">Next steps</span></span>

<span data-ttu-id="940de-190">Nu u het uploaden van bestanden van apparaten met behulp van IoT Hub hebt geleerd, kunt u mogelijk geïnteresseerd in de volgende onderwerpen van IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="940de-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="940de-191">[Apparaat-id's van IoT-Hub beheren][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="940de-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="940de-192">[Toegang beheren met IoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="940de-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="940de-193">[Horende apparaten gebruiken om de status en configuraties te synchroniseren][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="940de-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="940de-194">[Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="940de-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="940de-195">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="940de-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="940de-196">Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="940de-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="940de-197">[Het uploaden van bestanden van apparaten naar de cloud met IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="940de-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
