---
title: uploaden van het bestand aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - Hallo-bestand uploaden-functie van IoT Hub toomanage uploaden van bestanden van een apparaat tooan Azure storage blob-container gebruiken.
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="9b91a-103">Uploaden van bestanden met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9b91a-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="9b91a-104">Gedetailleerde in Hallo [IoT-hubeindpunten] [ lnk-endpoints] artikel, een apparaat kunt starten uploaden van een bestand met het verzenden van een melding via een apparaat gerichte-eindpunt (**/devices/ {deviceId} /bestanden**).</span><span class="sxs-lookup"><span data-stu-id="9b91a-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="9b91a-105">Wanneer een apparaat een melding van IoT Hub een upload is voltooid, IoT Hub verzendt een bericht op bestand uploaden via Hallo **/messages/servicebound/filenotifications** gerichte service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9b91a-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="9b91a-106">In plaats van het uitgeven van de berichten via IoT Hub zelf fungeert IoT-Hub in plaats daarvan als een dispatcher tooan Azure Storage-account gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="9b91a-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="9b91a-107">Een apparaat vraagt een token van de opslag van IoT-Hub die specifieke toohello bestand Hallo apparaat tooupload wenst.</span><span class="sxs-lookup"><span data-stu-id="9b91a-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="9b91a-108">Hallo-apparaat gebruikt Hallo SAS-URI tooupload Hallo bestand toostorage en wanneer Hallo uploaden voltooid is Hallo-apparaat een melding van voltooiing tooIoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="9b91a-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="9b91a-109">IoT Hub controleert Hallo-bestand uploaden is voltooid en een bestand uploaden notification message toohello service gerichte bestand meldingseindpunt worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9b91a-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="9b91a-110">Voordat u een bestand tooIoT Hub vanaf een apparaat uploadt, moet u uw hub door configureren [koppelen van een Azure Storage] [ lnk-associate-storage] tooit-account.</span><span class="sxs-lookup"><span data-stu-id="9b91a-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="9b91a-111">Uw apparaat kunt vervolgens [initialiseren van een upload] [ lnk-initialize] en vervolgens [IoT-hub in kennis] [ lnk-notify] wanneer Hallo uploaden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b91a-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="9b91a-112">Eventueel, wanneer een apparaat een melding van IoT-Hub die Hallo uploaden is voltooid, Hallo-service kan genereren een [Meldingsbericht][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="9b91a-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="9b91a-113">Wanneer toouse</span><span class="sxs-lookup"><span data-stu-id="9b91a-113">When toouse</span></span>

<span data-ttu-id="9b91a-114">Bestand uploaden toosend mediabestanden en grote telemetrie batches geüpload door afwisselend verbonden apparaten of gecomprimeerde toosave bandbreedte gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b91a-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="9b91a-115">Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="9b91a-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="9b91a-116">Een Azure Storage-account koppelen met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9b91a-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="9b91a-117">functionaliteit voor toouse Hallo-bestand uploaden, moet u eerst een Azure Storage-account toohello IoT Hub koppelen.</span><span class="sxs-lookup"><span data-stu-id="9b91a-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="9b91a-118">U kunt deze taak uitvoeren via Hallo [Azure-portal][lnk-management-portal], of via een programma via Hallo [resourceprovider IoT Hub REST-API's] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="9b91a-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="9b91a-119">Zodra u hebt een Azure Storage-account gekoppeld aan uw IoT-Hub, retourneert Hallo-service een SAS-URI tooa apparaat wanneer Hallo apparaat een aanvraag voor het uploaden van bestand initieert.</span><span class="sxs-lookup"><span data-stu-id="9b91a-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="9b91a-120">Hallo [Azure IoT SDK's] [ lnk-sdks] automatisch bij het ophalen van ingangen Hallo SAS URI, Hallo-bestand uploadt en meldingen van IoT Hub een voltooide geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="9b91a-121">Initialiseren van een bestand is geüpload</span><span class="sxs-lookup"><span data-stu-id="9b91a-121">Initialize a file upload</span></span>
<span data-ttu-id="9b91a-122">IoT Hub heeft een eindpunt specifiek voor apparaten toorequest een SAS-URI voor opslag tooupload een bestand.</span><span class="sxs-lookup"><span data-stu-id="9b91a-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="9b91a-123">tooinitiate hello bestand uploadproces Hallo apparaat verzendt een POST-aanvraag te`{iot hub}.azure-devices.net/devices/{deviceId}/files` Hello JSON-hoofdtekst te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b91a-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="9b91a-124">IoT Hub retourneert Hallo volgt gegevens, welk apparaat Hallo tooupload Hallo-bestand wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9b91a-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="9b91a-125">Afgeschafte: het uploaden van een bestand met een GET initialiseren</span><span class="sxs-lookup"><span data-stu-id="9b91a-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="9b91a-126">Deze sectie beschrijft afgeschafte functionaliteit voor het tooreceive een SAS-URI van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9b91a-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="9b91a-127">Gebruik Hallo POST-methode die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="9b91a-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="9b91a-128">IoT Hub heeft twee REST-eindpunten toosupport bestand uploadt, één tooget Hallo SAS-URI voor opslag en andere toonotify Hallo IoT-hub van het uploaden van een voltooide Hallo wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b91a-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="9b91a-129">Hallo apparaat initieert uploadproces Hallo-bestand door te verzenden naar een GET toohello iothub op `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="9b91a-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="9b91a-130">Hallo IoT-hub als resultaat:</span><span class="sxs-lookup"><span data-stu-id="9b91a-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="9b91a-131">Een SAS-URI van specifieke toohello bestand toobe geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="9b91a-132">Een correlatie-ID toobe gebruikt nadat Hallo uploaden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b91a-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="9b91a-133">Melding van IoT Hub een voltooide bestand is geüpload</span><span class="sxs-lookup"><span data-stu-id="9b91a-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="9b91a-134">Hallo-apparaat is verantwoordelijk voor het uploaden van Hallo bestand toostorage hello Azure-opslag-SDK's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b91a-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="9b91a-135">Wanneer Hallo uploaden voltooid is, Hallo-apparaat een POST-aanvraag te verzendt`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` Hello JSON-hoofdtekst te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b91a-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="9b91a-136">waarde van Hallo `isSuccess` wordt een Boolean die aangeeft of Hallo-bestand is geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="9b91a-137">Hallo statuscode voor `statusCode` status voor het uploaden van Hallo bestand toostorage Hallo Hallo en Hallo `statusDescription` overeenkomt met toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="9b91a-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="9b91a-138">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="9b91a-138">Reference topics:</span></span>

<span data-ttu-id="9b91a-139">Hallo bieden volgende naslagonderwerpen u meer informatie over het uploaden van bestanden van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="9b91a-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="9b91a-140">Bestand uploaden meldingen</span><span class="sxs-lookup"><span data-stu-id="9b91a-140">File upload notifications</span></span>

<span data-ttu-id="9b91a-141">Wanneer een apparaat een melding van IoT Hub een upload is voltooid, kunt IoT Hub eventueel een bericht op dat Hallo naam- en storage-locatie van Hallo-bestand bevat genereren.</span><span class="sxs-lookup"><span data-stu-id="9b91a-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="9b91a-142">Zoals uitgelegd in [eindpunten][lnk-endpoints], IoT Hub biedt bestand uploaden meldingen via een gerichte service-eindpunt (**/messages/servicebound/fileuploadnotifications**) Als berichten.</span><span class="sxs-lookup"><span data-stu-id="9b91a-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="9b91a-143">Hallo ontvangen semantiek voor bestand uploaden meldingen zijn dezelfde als voor cloud-naar-apparaatberichten Hallo en hebben dezelfde Hallo [bericht lifecycle][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="9b91a-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="9b91a-144">Elk bericht opgehaald uit het Hallo-bestand uploaden meldingseindpunt is een JSON-record met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="9b91a-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="9b91a-145">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9b91a-145">Property</span></span> | <span data-ttu-id="9b91a-146">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9b91a-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b91a-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="9b91a-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="9b91a-148">De tijdstempel die aangeeft wanneer Hallo melding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b91a-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="9b91a-149">Apparaat-id</span><span class="sxs-lookup"><span data-stu-id="9b91a-149">DeviceId</span></span> |<span data-ttu-id="9b91a-150">**DeviceId** van Hallo-apparaat dat Hallo bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="9b91a-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="9b91a-151">BlobUri</span></span> |<span data-ttu-id="9b91a-152">URI van Hallo bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="9b91a-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="9b91a-153">BlobName</span></span> |<span data-ttu-id="9b91a-154">Naam van Hallo bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="9b91a-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="9b91a-155">LastUpdatedTime</span></span> |<span data-ttu-id="9b91a-156">De tijdstempel die aangeeft wanneer Hallo-bestand het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9b91a-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="9b91a-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="9b91a-157">BlobSizeInBytes</span></span> |<span data-ttu-id="9b91a-158">Grootte van Hallo bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="9b91a-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="9b91a-159">**Voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="9b91a-159">**Example**.</span></span> <span data-ttu-id="9b91a-160">Dit voorbeeld toont het Hallo-hoofdtekst van een bestand uploaden Meldingsbericht.</span><span class="sxs-lookup"><span data-stu-id="9b91a-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="9b91a-161">Bestand uploaden meldingsopties configuratie</span><span class="sxs-lookup"><span data-stu-id="9b91a-161">File upload notification configuration options</span></span>

<span data-ttu-id="9b91a-162">Elke IoT-hub toont Hallo configuratieopties voor het bestand uploaden meldingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b91a-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="9b91a-163">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9b91a-163">Property</span></span> | <span data-ttu-id="9b91a-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9b91a-164">Description</span></span> | <span data-ttu-id="9b91a-165">Bereik en standaard</span><span class="sxs-lookup"><span data-stu-id="9b91a-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b91a-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="9b91a-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="9b91a-167">Hiermee bepaalt u of bestand uploaden meldingen toohello bestand meldingen eindpunt worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="9b91a-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="9b91a-168">BOOL.</span><span class="sxs-lookup"><span data-stu-id="9b91a-168">Bool.</span></span> <span data-ttu-id="9b91a-169">Standaard: True.</span><span class="sxs-lookup"><span data-stu-id="9b91a-169">Default: True.</span></span> |
| <span data-ttu-id="9b91a-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="9b91a-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="9b91a-171">Standaard-TTL voor meldingen van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="9b91a-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="9b91a-172">Interval ISO_8601 up too48H (minimaal 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="9b91a-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="9b91a-173">Standaardwaarde: 1 uur.</span><span class="sxs-lookup"><span data-stu-id="9b91a-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="9b91a-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="9b91a-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="9b91a-175">De duur van de vergrendeling voor Hallo-bestand uploaden meldingen wachtrij.</span><span class="sxs-lookup"><span data-stu-id="9b91a-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="9b91a-176">5 too300 seconden (minimaal 5 seconden).</span><span class="sxs-lookup"><span data-stu-id="9b91a-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="9b91a-177">Standaard: 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="9b91a-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="9b91a-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="9b91a-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="9b91a-179">Levering van het maximum aantal voor Hallo-bestand uploaden meldingswachtrij.</span><span class="sxs-lookup"><span data-stu-id="9b91a-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="9b91a-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="9b91a-180">1 too100.</span></span> <span data-ttu-id="9b91a-181">Standaard: 100.</span><span class="sxs-lookup"><span data-stu-id="9b91a-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="9b91a-182">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="9b91a-182">Additional reference material</span></span>

<span data-ttu-id="9b91a-183">Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9b91a-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="9b91a-184">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="9b91a-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="9b91a-185">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's en beperking gedrag die van toepassing zijn toohello service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9b91a-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="9b91a-186">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.</span><span class="sxs-lookup"><span data-stu-id="9b91a-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="9b91a-187">[IoT Hub-querytaal] [ lnk-query] Hallo querytaal tooretrieve informatie uit IoT Hub over uw apparaat horende taken kunt u hierin wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="9b91a-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="9b91a-188">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="9b91a-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b91a-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b91a-189">Next steps</span></span>

<span data-ttu-id="9b91a-190">Nu u hebt geleerd hoe tooupload bestanden van apparaten met behulp van IoT Hub, kunt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:</span><span class="sxs-lookup"><span data-stu-id="9b91a-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="9b91a-191">[Apparaat-id's van IoT-Hub beheren][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="9b91a-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="9b91a-192">[Beheer toegang tooIoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="9b91a-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="9b91a-193">[Gebruik Apparaatstatus horende toosynchronize en configuraties][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="9b91a-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="9b91a-194">[Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="9b91a-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="9b91a-195">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="9b91a-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="9b91a-196">Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="9b91a-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="9b91a-197">[Hoe tooupload bestanden van apparaten toohello cloud met IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="9b91a-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
