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
# <a name="upload-files-with-iot-hub"></a>Uploaden van bestanden met IoT Hub

Gedetailleerde in Hallo [IoT-hubeindpunten] [ lnk-endpoints] artikel, een apparaat kunt starten uploaden van een bestand met het verzenden van een melding via een apparaat gerichte-eindpunt (**/devices/ {deviceId} /bestanden**). Wanneer een apparaat een melding van IoT Hub een upload is voltooid, IoT Hub verzendt een bericht op bestand uploaden via Hallo **/messages/servicebound/filenotifications** gerichte service-eindpunt.

In plaats van het uitgeven van de berichten via IoT Hub zelf fungeert IoT-Hub in plaats daarvan als een dispatcher tooan Azure Storage-account gekoppeld. Een apparaat vraagt een token van de opslag van IoT-Hub die specifieke toohello bestand Hallo apparaat tooupload wenst. Hallo-apparaat gebruikt Hallo SAS-URI tooupload Hallo bestand toostorage en wanneer Hallo uploaden voltooid is Hallo-apparaat een melding van voltooiing tooIoT Hub verzendt. IoT Hub controleert Hallo-bestand uploaden is voltooid en een bestand uploaden notification message toohello service gerichte bestand meldingseindpunt worden toegevoegd.

Voordat u een bestand tooIoT Hub vanaf een apparaat uploadt, moet u uw hub door configureren [koppelen van een Azure Storage] [ lnk-associate-storage] tooit-account.

Uw apparaat kunt vervolgens [initialiseren van een upload] [ lnk-initialize] en vervolgens [IoT-hub in kennis] [ lnk-notify] wanneer Hallo uploaden is voltooid. Eventueel, wanneer een apparaat een melding van IoT-Hub die Hallo uploaden is voltooid, Hallo-service kan genereren een [Meldingsbericht][lnk-service-notification].

### <a name="when-toouse"></a>Wanneer toouse

Bestand uploaden toosend mediabestanden en grote telemetrie batches geüpload door afwisselend verbonden apparaten of gecomprimeerde toosave bandbreedte gebruiken.

Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Een Azure Storage-account koppelen met IoT Hub

functionaliteit voor toouse Hallo-bestand uploaden, moet u eerst een Azure Storage-account toohello IoT Hub koppelen. U kunt deze taak uitvoeren via Hallo [Azure-portal][lnk-management-portal], of via een programma via Hallo [resourceprovider IoT Hub REST-API's] [ lnk-resource-provider-apis]. Zodra u hebt een Azure Storage-account gekoppeld aan uw IoT-Hub, retourneert Hallo-service een SAS-URI tooa apparaat wanneer Hallo apparaat een aanvraag voor het uploaden van bestand initieert.

> [!NOTE]
> Hallo [Azure IoT SDK's] [ lnk-sdks] automatisch bij het ophalen van ingangen Hallo SAS URI, Hallo-bestand uploadt en meldingen van IoT Hub een voltooide geüpload.


## <a name="initialize-a-file-upload"></a>Initialiseren van een bestand is geüpload
IoT Hub heeft een eindpunt specifiek voor apparaten toorequest een SAS-URI voor opslag tooupload een bestand. tooinitiate hello bestand uploadproces Hallo apparaat verzendt een POST-aanvraag te`{iot hub}.azure-devices.net/devices/{deviceId}/files` Hello JSON-hoofdtekst te volgen:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT Hub retourneert Hallo volgt gegevens, welk apparaat Hallo tooupload Hallo-bestand wordt gebruikt:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Afgeschafte: het uploaden van een bestand met een GET initialiseren

> [!NOTE]
> Deze sectie beschrijft afgeschafte functionaliteit voor het tooreceive een SAS-URI van IoT Hub. Gebruik Hallo POST-methode die eerder zijn beschreven.

IoT Hub heeft twee REST-eindpunten toosupport bestand uploadt, één tooget Hallo SAS-URI voor opslag en andere toonotify Hallo IoT-hub van het uploaden van een voltooide Hallo wordt uitgevoerd. Hallo apparaat initieert uploadproces Hallo-bestand door te verzenden naar een GET toohello iothub op `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. Hallo IoT-hub als resultaat:

* Een SAS-URI van specifieke toohello bestand toobe geüpload.
* Een correlatie-ID toobe gebruikt nadat Hallo uploaden is voltooid.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Melding van IoT Hub een voltooide bestand is geüpload

Hallo-apparaat is verantwoordelijk voor het uploaden van Hallo bestand toostorage hello Azure-opslag-SDK's gebruiken. Wanneer Hallo uploaden voltooid is, Hallo-apparaat een POST-aanvraag te verzendt`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` Hello JSON-hoofdtekst te volgen:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

waarde van Hallo `isSuccess` wordt een Boolean die aangeeft of Hallo-bestand is geüpload. Hallo statuscode voor `statusCode` status voor het uploaden van Hallo bestand toostorage Hallo Hallo en Hallo `statusDescription` overeenkomt met toohello `statusCode`.

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:

Hallo bieden volgende naslagonderwerpen u meer informatie over het uploaden van bestanden van een apparaat.

## <a name="file-upload-notifications"></a>Bestand uploaden meldingen

Wanneer een apparaat een melding van IoT Hub een upload is voltooid, kunt IoT Hub eventueel een bericht op dat Hallo naam- en storage-locatie van Hallo-bestand bevat genereren.

Zoals uitgelegd in [eindpunten][lnk-endpoints], IoT Hub biedt bestand uploaden meldingen via een gerichte service-eindpunt (**/messages/servicebound/fileuploadnotifications**) Als berichten. Hallo ontvangen semantiek voor bestand uploaden meldingen zijn dezelfde als voor cloud-naar-apparaatberichten Hallo en hebben dezelfde Hallo [bericht lifecycle][lnk-lifecycle]. Elk bericht opgehaald uit het Hallo-bestand uploaden meldingseindpunt is een JSON-record met Hallo volgende eigenschappen:

| Eigenschap | Beschrijving |
| --- | --- |
| EnqueuedTimeUtc |De tijdstempel die aangeeft wanneer Hallo melding is gemaakt. |
| Apparaat-id |**DeviceId** van Hallo-apparaat dat Hallo bestand geüpload. |
| BlobUri |URI van Hallo bestand geüpload. |
| BlobName |Naam van Hallo bestand geüpload. |
| LastUpdatedTime |De tijdstempel die aangeeft wanneer Hallo-bestand het laatst is bijgewerkt. |
| BlobSizeInBytes |Grootte van Hallo bestand geüpload. |

**Voorbeeld**. Dit voorbeeld toont het Hallo-hoofdtekst van een bestand uploaden Meldingsbericht.

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

## <a name="file-upload-notification-configuration-options"></a>Bestand uploaden meldingsopties configuratie

Elke IoT-hub toont Hallo configuratieopties voor het bestand uploaden meldingen te volgen:

| Eigenschap | Beschrijving | Bereik en standaard |
| --- | --- | --- |
| **enableFileUploadNotifications** |Hiermee bepaalt u of bestand uploaden meldingen toohello bestand meldingen eindpunt worden geschreven. |BOOL. Standaard: True. |
| **fileNotifications.ttlAsIso8601** |Standaard-TTL voor meldingen van bestand uploaden. |Interval ISO_8601 up too48H (minimaal 1 minuut). Standaardwaarde: 1 uur. |
| **fileNotifications.lockDuration** |De duur van de vergrendeling voor Hallo-bestand uploaden meldingen wachtrij. |5 too300 seconden (minimaal 5 seconden). Standaard: 60 seconden. |
| **fileNotifications.maxDeliveryCount** |Levering van het maximum aantal voor Hallo-bestand uploaden meldingswachtrij. |1 too100. Standaard: 100. |

## <a name="additional-reference-material"></a>Aanvullende referentiemateriaal

Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's en beperking gedrag die van toepassing zijn toohello service IoT Hub.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.
* [IoT Hub-querytaal] [ lnk-query] Hallo querytaal tooretrieve informatie uit IoT Hub over uw apparaat horende taken kunt u hierin wordt beschreven.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe tooupload bestanden van apparaten met behulp van IoT Hub, kunt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:

* [Apparaat-id's van IoT-Hub beheren][lnk-devguide-identities]
* [Beheer toegang tooIoT Hub][lnk-devguide-security]
* [Gebruik Apparaatstatus horende toosynchronize en configuraties][lnk-devguide-device-twins]
* [Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:

* [Hoe tooupload bestanden van apparaten toohello cloud met IoT Hub][lnk-fileupload-tutorial]

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
