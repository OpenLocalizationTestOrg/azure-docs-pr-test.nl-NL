---
title: Azure IoT Hub - aan de slag IoT-apparaten toohello cloud verbinden | Microsoft Docs
description: Meer informatie over hoe tooconnect uw IoT-boards en starter Kit tooAzure IoT Hub. Uw apparaten kunnen verzenden telemetrie tooIoT Hub en IoT-Hub kunt controleren en beheren van uw apparaten.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Azure iot hub-zelfstudie
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a>Azure IoT Hub get zelfstudies gestart

U kunt Azure IoT Hub en hello Azure IoT SDK's toobuild Internet der dingen (IoT)-oplossingen voor apparaten:

* Azure IoT Hub is een volledig beheerde service in Hallo cloud die veilig verbindt, bewaakt en beheert uw IoT-apparaten. Gebruik hello Azure IoT-apparaat-SDK's tooimplement uw IoT-apparaten.
* Gebruik een IoT-gateway in complexere IoT-scenario's. Waar moet u wel tooconsider factoren zoals de oudere apparaten, kosten van bandbreedte, beveiliging en privacy-beleid of gegevensverwerking rand weergeven. In deze scenario's gebruikt u Azure IoT rand tooimplement een gateway die is verbonden apparaten tooyour IoT-hub.

## <a name="what-hello-tutorials-cover"></a>Wat Hallo zelfstudies hebben betrekking op

Deze zelfstudies introduceren tooAzure IoT Hub en Hallo apparaat-SDK's. Hallo zelfstudies omvatten algemene IoT scenario's toodemonstrate Hallo mogelijkheden van IoT-Hub. Hallo zelfstudies ook laten zien hoe toocombine IoT Hub met andere Azure-services en hulpprogramma's voor toobuild meer krachtige IoT-oplossingen. In de zelfstudies hello, kunt u toouse gesimuleerde of echte IoT-apparaten. Bovendien leert u hoe toouse een gateway tooenable apparaten tooconnect tooyour iothub.

## <a name="set-up-your-device"></a>Uw apparaat instellen

Verbinding maken met een IoT-apparaat of de gateway tooAzure IoT Hub. U kunt een fysieke of gesimuleerde apparaat tooget gestart:

| IoT-apparaat                       | Programmeertaal |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IoT DevKit                       | [Arduino in VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Doezelaar HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 ding Dev       | [Arduino][Th_Ard]              |
| Adafruit Doezelaar M0              | [Arduino][M0_Ard]              |
| Gesimuleerde apparaat op PC           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Online apparaatsimulator         | [Raspberry Pi (Node.js)][Ol_Sim] |

Bovendien kunt u een IoT-Edge gateway tooenable apparaten tooconnect tooyour IoT-hub:

| Gateway-apparaat               | Programmeertaal | Platform         |
|------------------------------|----------------------|------------------|
| Intel NUC (model DE3815TYKE) | C                    | [De o Linux][NUC_Lnx] |
| Gesimuleerde gateway            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
