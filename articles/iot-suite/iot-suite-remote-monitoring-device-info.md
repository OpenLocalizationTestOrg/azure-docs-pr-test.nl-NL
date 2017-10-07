---
title: aaaDevice informatie metagegevens in Hallo oplossing voor externe controle | Microsoft Docs
description: Een beschrijving van hello Azure IoT vooraf geconfigureerde oplossing voor externe controle en de bijbehorende architectuur.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle

Hello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle demonstreert een benadering voor het beheren van metagegevens van apparaten. In dit artikel bevat een overzicht van Hallo benadering deze oplossing wordt tooenable u toounderstand:

* Welke oplossing Hallo metagegevens worden opgeslagen.
* Hoe beheert Hallo oplossing Hallo Apparaatmetagegevens.

## <a name="context"></a>Context

Hallo externe controle vooraf geconfigureerde oplossing maakt gebruik van [Azure IoT Hub] [ lnk-iot-hub] tooenable uw apparaten toosend gegevens toohello cloud. Hallo oplossing bevat informatie over apparaten op drie verschillende locaties:

| Locatie | Gegevens die zijn opgeslagen | Implementatie |
| -------- | ------------------ | -------------- |
| ID-register | Apparaat-id, verificatiesleutels, de status ingeschakeld | Ingebouwde tooIoT Hub |
| Apparaat horende | Metagegevens: gemelde eigenschappen, gewenste eigenschappen, tags | Ingebouwde tooIoT Hub |
| Cosmos DB | Geschiedenis van de opdracht en methode | Aangepaste voor oplossing |

IoT-Hub bevat een [register voor apparaat-id's] [ lnk-identity-registry] toomanage toegang tot tooan iothub en maakt gebruik van [apparaat horende] [ lnk-device-twin] toomanage Apparaatmetagegevens . Er is ook een externe controle oplossings-specifieke *apparaatregister* die worden opgeslagen geschiedenis van de opdracht en de methode. Hallo voor externe controle oplossing gebruikt een [Cosmos DB] [ lnk-docdb] database tooimplement een aangepast archief voor de opdracht en methode geschiedenis.

> [!NOTE]
> Hallo vooraf geconfigureerde oplossing voor externe controle houdt register Hallo apparaat-id's gesynchroniseerd met de Hallo informatie in Hallo Cosmos-DB-database. Beide gebruik van dezelfde apparaat-id toouniquely identificeren Hallo elk apparaat verbonden tooyour IoT-hub.

## <a name="device-metadata"></a>Metagegevens van apparaten

IoT Hub onderhoudt een [apparaat twin] [ lnk-device-twin] voor elk apparaat gesimuleerde en fysieke verbonden tooa oplossing voor externe controle. Hallo-oplossing gebruikt horende toomanage Hallo metagegevens van apparaten die zijn gekoppeld aan apparaten. Een apparaat-twin is een JSON-document bijgehouden door de IoT Hub en Hallo oplossing maakt gebruik van Hallo IoT Hub API toointeract met horende apparaten.

Een apparaat-twin drie soorten metagegevens worden opgeslagen:

- *Eigenschappen gerapporteerd* tooan iothub worden verzonden door een apparaat. In de oplossing voor externe controle hello, gesimuleerde apparaten verzenden gemelde eigenschappen bij het opstarten en in reactie te**Changedevicestate** opdrachten en -methoden. U kunt gemelde eigenschappen weergeven in Hallo **lijst met apparaten** en **details apparaat** in de oplossingsportal Hallo. Gerapporteerde eigenschappen zijn alleen-lezen.
- *Eigenschappen gewenst* worden opgehaald uit de IoT-hub Hallo door apparaten. Het is de verantwoordelijkheid Hallo van Hallo apparaat toomake alle benodigde configuratie wijzigen op Hallo-apparaat. Het is ook Hallo verantwoordelijkheid van Hallo apparaat tooreport Hallo wijziging back toohello hub als een eigenschap gemeld. U kunt een waarde van de gewenste eigenschap via de portal van de oplossing Hallo instellen.
- *Labels* alleen bestaan in Hallo apparaat twin en nooit worden gesynchroniseerd met een apparaat. U kunt in de oplossingsportal Hallo labelwaarden en ze gebruiken bij het filteren van Hallo lijst met apparaten. een label tooidentify Hallo pictogram toodisplay Hallo oplossing ook gebruikt voor een apparaat in de oplossingsportal Hallo.

Voorbeeld gerapporteerd eigenschappen van Hallo gesimuleerde apparaten zijn onder meer de fabrikant, modelnummer breedtegraad en lengtegraad. Hallo-lijst van ondersteunde methoden gesimuleerde apparaten ook geretourneerd als een gerapporteerde eigenschap.

> [!NOTE]
> Hallo gesimuleerd apparaatcode gebruikt alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenste eigenschappen tooupdate Hallo eigenschappen teruggestuurd gerapporteerd tooIoT Hub. Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.

Een apparaat informatie metagegevens JSON-document opgeslagen in Hallo apparaat register Cosmos-DB-database heeft Hallo structuur te volgen:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Gegevens van een apparaat kan ook metagegevens toodescribe Hallo telemetrie Hallo apparaat verzendt tooIoT Hub bevatten. Hallo-oplossing voor externe controle maakt gebruik van deze telemetrie metagegevens toocustomize hoe Hallo dashboard toont de [dynamische telemetrie][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Levenscyclus

Wanneer u eerst een apparaat in de oplossingsportal Hallo maakt, maakt Hallo oplossing een vermelding in Hallo Cosmos DB database toostore opdracht en de geschiedenis van de methode. Hallo-oplossing maakt een vermelding voor Hallo apparaat op dit moment ook in Hallo apparaat identiteitenregister, waardoor Hallo sleutels Hallo apparaat maakt gebruik van tooauthenticate met IoT Hub worden gegenereerd. Dit leidt ook tot een apparaat-twin.

Wanneer een apparaat toohello oplossing de eerst verbinding maakt, wordt gemeld eigenschappen en een informatiebericht van het apparaat verzonden. Hallo gerapporteerd eigenschapswaarden worden automatisch opgeslagen in Hallo apparaat twin. Hallo gerapporteerd eigenschappen zijn onder meer apparaatfabrikant hello, modelnummer, serienummer en een lijst van ondersteunde methoden. Hallo-bericht van apparaat informatie bevat de lijst Hallo Hallo opdrachten Hallo apparaat inclusief informatie over eventuele opdrachtparameters ondersteunt. Wanneer Hallo oplossing dit bericht ontvangt, werkt het Hallo-apparaatgegevens in Hallo Cosmos-DB-database.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Apparaat-informatie in de oplossingsportal Hallo weergeven en bewerken

Hallo lijst met apparaten in de oplossingsportal Hallo geeft Hallo apparaateigenschappen volgen als kolommen in een standaard: **Status**, **DeviceId**, **fabrikant**, **Modelnummer**, **serienummer**, **Firmware**, **Platform**, **Processor**, en  **Geïnstalleerd RAM-geheugen**. U kunt Hallo kolommen aanpassen door te klikken op **kolom editor**. Apparaateigenschappen Hallo **breedtegraad** en **lengtegraad** station Hallo locatie in Hallo Bing-kaart op Hallo-dashboard.

![Editor voor kolom in de lijst met apparaten][img-device-list]

In Hallo **Apparaatdetails** deelvenster in de oplossingsportal hello, kunt u gewenste eigenschappen en labels bewerken (gerapporteerd eigenschappen zijn alleen-lezen).

![Deelvenster Apparaatdetails][img-device-edit]

U kunt Hallo oplossing portal tooremove een apparaat gebruiken van uw oplossing. Wanneer u een apparaat verwijdert, wordt Hallo oplossing vermelding Hallo-apparaat verwijdert uit het identiteitenregister en verwijdert vervolgens Hallo apparaat twin. Hallo oplossing verwijdert informatie gerelateerde toohello apparaat ook uit Hallo Cosmos DB database. Voordat u een apparaat verwijdert kunt, moet u deze uitschakelen.

![Apparaat verwijderen][img-device-remove]

## <a name="device-information-message-processing"></a>Apparaat informatie berichtverwerking

Berichten met apparaatgegevens verzonden door een apparaat zijn telemetrieberichten. Berichten met apparaatgegevens omvatten een apparaat kan reageren op Hallo-opdrachten en eventuele opdrachtgeschiedenis. IoT-Hub zelf heeft geen informatie over Hallo metagegevens in het informatiebericht van een apparaat en processen Hallo-bericht in Hallo dezelfde manier als alle apparaat-naar-cloud-berichten worden verwerkt. In het Hallo-oplossing, voor externe controle een [Azure Stream Analytics] [ lnk-stream-analytics] (ASA) taak Hallo-berichten uit IoT Hub kan lezen. Hallo **DeviceInfo** stream analytics-taak filters voor berichten met **'ObjectType': 'DeviceInfo'** en stuurt ze toohello **EventProcessorHost** host exemplaar dat wordt uitgevoerd in een web-taak. Logica in Hallo **EventProcessorHost** instantie Hallo apparaat-id toofind hello Cosmos DB record voor Hallo specifieke apparaat- en update Hallo record gebruikt.

> [!NOTE]
> Een informatiebericht van het apparaat is een standaard apparaat-naar-cloud-bericht. Hallo-oplossing wordt onderscheid gemaakt tussen berichten met apparaatgegevens en telemetrieberichten met behulp van de ASA-query's.

## <a name="next-steps"></a>Volgende stappen

Nu u klaar bent met het leren hoe u Hallo vooraf geconfigureerde oplossingen kunt aanpassen, vindt u enkele Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]
* [Veelgestelde vragen over IoT Suite][lnk-faq]
* [Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
