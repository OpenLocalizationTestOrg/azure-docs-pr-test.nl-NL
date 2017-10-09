---
title: aaaManage Azure IoT Hub cloud apparaat met iothub explorer messaging | Microsoft Docs
description: Ontdek hoe toouse Hallo iothub explorer CLI-hulpprogramma toomonitor apparaat toocloud (D2C)-berichten en berichten cloud toodevice (C2D) in Azure IoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iothub explorer cloud apparaat messaging, iot hub cloud toodevice cloud toodevice messaging
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Gebruik iothub explorer toosend en ontvangen van berichten tussen het apparaat en IoT-Hub

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub explorer](https://github.com/azure/iothub-explorer) heeft een aantal opdrachten die IoT Hub beheer vergemakkelijkt. Deze zelfstudie is gericht op het toouse iothub explorer toosend en ontvangen van berichten tussen het apparaat en uw IoT-hub.

## <a name="what-you-will-learn"></a>Wat u leert

U leert hoe toouse iothub explorer toomonitor apparaat-naar-cloud-berichten en berichten die toosend cloud-naar-apparaat. Apparaat-naar-cloud-berichten kunnen worden sensorgegevens dat uw apparaat verzamelt en vervolgens tooyour IoT-hub verzendt. Cloud-naar-apparaat-berichten kunnen worden opdrachten uw IoT-hub verzendt tooyour apparaat tooblink een LED die is verbonden tooyour apparaat.

## <a name="what-you-will-do"></a>Wat u doet

- Gebruik iothub explorer toomonitor apparaat-naar-cloud-berichten.
- Gebruik iothub explorer toosend cloud-naar-apparaat-berichten.

## <a name="what-you-need"></a>Wat u nodig hebt

- Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:
  - Een actief Azure-abonnement.
  - Een Azure-IoT-hub in uw abonnement.
  - Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.
- iothub-explorer. ([Iothub explorer installeren](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten worden gecontroleerd

toomonitor berichten die vanaf uw apparaat tooyour IoT-hub worden verzonden als volgt te werk:

1. Open een consolevenster.
1. Hallo volgende opdracht uitvoeren:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Ophalen van `<device-id>` en `<IoTHubConnectionString>` uit uw IoT-hub. Zorg ervoor dat u klaar bent met eerdere Hallo-zelfstudie. Of u kunt proberen toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` hebt u `HostName`, `SharedAccessKeyName` en `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Cloud-naar-apparaat-berichten verzenden

toosend een bericht van uw IoT hub tooyour-apparaat als volgt te werk:

1. Open een consolevenster.
1. Start een sessie op uw IoT-hub door het Hallo volgende opdracht uitvoeren:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Een bericht tooyour apparaat verzenden door te voeren Hallo volgende opdracht:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

Hallo opdracht knippert Hallo LED die is verbonden tooyour apparaat en Hallo-bericht tooyour apparaat verzendt.

> [!Note]
> Er is een afzonderlijke ack opdracht back tooyour IoT-hub bij ontvangst van het Hallo-bericht niet nodig voor Hallo apparaat toosend.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toomonitor apparaat-naar-cloud-berichten en berichten tussen uw IoT-apparaat en de Azure IoT Hub cloud naar apparaat verzenden.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
