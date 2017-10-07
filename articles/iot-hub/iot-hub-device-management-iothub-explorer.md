---
title: aaaAzure IoT device management met iothub explorer | Microsoft Docs
description: Hallo iothub explorer CLI-hulpprogramma gebruiken voor Azure IoT Hub Apparaatbeheer, met directe Hallo-methoden en Hallo Twin van de eigenschappen van de gewenste opties.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot-Apparaatbeheer, Apparaatbeheer via azure iot hub, apparaat management iot, Apparaatbeheer via iot hub
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Iothub-explorer gebruiken voor het beheer van Azure IoT Hub-apparaten

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub explorer](https://github.com/azure/iothub-explorer) is een CLI-hulpprogramma dat u op een host computer toomanage apparaat-id's in het register van IoT hub uitvoert. Wordt geleverd met opties waarmee u tooperform kunt diverse taken.

| Beheeroptie          | Taak                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Directe methoden             | Een apparaat fungeren zoals starten of stoppen van verzenden van berichten of Hallo-apparaat opnieuw maken.                                        |
| Eigenschappen van de gewenste Twin    | Een apparaat in een bepaalde status, zoals het instellen van een toogreen LED plaatsen of interval too30 minuten instellen Hallo telemetrie verzenden.         |
| Dubbele eigenschappen gerapporteerd   | Ophalen van Hallo gerapporteerde status van een apparaat. Hallo apparaat rapporteert bijvoorbeeld Hallo die LED nu knippert.                                    |
| Labels Twin                  | Apparaatspecifieke metagegevens opslaan in de cloud Hallo. Bijvoorbeeld, de implementatielocatie van de van een machine snoep Hallo.                         |
| Cloud-naar-apparaat-berichten   | Meldingen tooa apparaat verzenden. Bijvoorbeeld 'het is zeer waarschijnlijk toorain vandaag. Vergeet niet een overkoepelende toobring."              |
| Apparaat twin query 's        | Query uitvoeren op alle apparaten horende tooretrieve die met een willekeurige voorwaarden, zoals het Hallo-apparaten die gebruikt worden om te identificeren. |

Zie voor meer gedetailleerde uitleg over Hallo verschillen en richtlijnen over het gebruik van deze opties, [apparaat-naar-cloud communicatie richtlijnen](iot-hub-devguide-d2c-guidance.md) en [Cloud-naar-apparaat communicatie richtlijnen](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen. IoT Hub persistente een apparaat twin voor elk apparaat dat tooit verbindt. Zie voor meer informatie over apparaat horende [aan de slag met apparaat horende](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Wat u leert

U leert met iothub-explorer met de verschillende beheeropties op uw ontwikkelcomputer.

## <a name="what-you-do"></a>Wat u doet

Voer iothub explorer met verschillende opties.

## <a name="what-you-need"></a>Wat u nodig hebt

- Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:
  - Een actief Azure-abonnement.
  - Een Azure-IoT-hub in uw abonnement.
  - Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.
- Zorg ervoor dat uw apparaat wordt uitgevoerd met de clienttoepassing Hallo tijdens deze zelfstudie.
- iothub-explorer [iothub explorer installeren](https://github.com/azure/iothub-explorer) op uw ontwikkelcomputer.

## <a name="connect-tooyour-iot-hub"></a>Verbinding maken met tooyour IoT-hub

Sluit tooyour iothub door het uitvoeren van de volgende opdracht Hallo:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Iothub explorer gebruiken met directe methoden

Hallo aanroepen `start` methode in Hallo apparaat app toosend berichten tooyour IoT-hub door het uitvoeren van de volgende opdracht Hallo:

```bash
iothub-explorer device-method <your device Id> start
```

Hallo aanroepen `stop` methode bij het verzenden van Hallo apparaat app toostop tooyour IoT-hub door het uitvoeren van de volgende opdracht Hallo-berichten:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Gebruik iothub-explorer met de gewenste eigenschappen van twin

Instellen van een interval van de gewenste eigenschap 3000 = door het uitvoeren van de volgende opdracht Hallo:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Deze eigenschap kan worden gelezen door uw apparaat.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Gebruik iothub-explorer met de dubbele eigenschappen gerapporteerd

Ophalen van hello gemelde eigenschappen van Hallo apparaat door te voeren Hallo de volgende opdracht:

```bash
iothub-explorer get-twin <your device id>
```

Een van de eigenschappen Hallo is $metadata. $lastUpdated waaruit blijkt Hallo laatste keer dat dit apparaat worden verzonden of ontvangen van een bericht.

## <a name="use-iothub-explorer-with-twins-tags"></a>Gebruik iothub-explorer met de labels van twin

Hallo-labels en eigenschappen van Hallo apparaat weergegeven door het uitvoeren van de volgende opdracht Hallo:

```bash
iothub-explorer get-twin <your device id>
```

Voeg een veld rol = temperatuur en vochtigheid toohello apparaat door te voeren Hallo volgende opdracht:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Gebruik iothub-explorer met de Cloud-naar-apparaat-berichten

Een apparaat met 'Hallo wereld' bericht toohello door het uitvoeren van de volgende opdracht Hallo verzenden:

```bash
iothub-explorer send <device-id> "Hello World"
```

Zie [iothub explorer toosend gebruiken en te ontvangen van berichten tussen het apparaat en IoT Hub](iot-hub-explorer-cloud-device-messaging.md) voor een echte scenario van het gebruik van deze opdracht.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Met iothub-Verkenner terwijl het apparaat horende query 's

Query uitvoeren op apparaten met een label van de rol 'temperatuur en vochtigheid' door het uitvoeren van de volgende opdracht Hallo =:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Query uitvoeren op alle apparaten, behalve die met een label van de rol 'temperatuur en vochtigheid' door het uitvoeren van de volgende opdracht Hallo =:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse iothub-explorer met de verschillende opties.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
