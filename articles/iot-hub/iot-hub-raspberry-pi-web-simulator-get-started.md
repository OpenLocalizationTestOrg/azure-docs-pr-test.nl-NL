---
title: aaaSimulated frambozen Pi toocloud (Node.js) - verbinding frambozen Pi web simulator tooAzure IoT Hub | Microsoft Docs
description: Verbinding maken met tooAzure simulator web Pi frambozen IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Raspberry pi simulator azure iot raspberry pi raspberry pi iothub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Verbinding maken met frambozen Pi online simulator tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In deze zelfstudie maakt eerst u learning Hallo basisbeginselen van het werken met frambozen Pi online simulator. U leert vervolgens hoe tooseamlessly Hallo Pi simulator toohello cloud verbinding via [Azure IoT Hub](iot-hub-what-is-iot-hub.md). 

Als u fysieke apparaten hebt, gaat u naar [verbinding frambozen Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget gestart. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Wat u doet

* Hallo basisbegrippen van frambozen Pi online simulator.
* Een iothub maken.
* Een apparaat registreren voor Pi in uw IoT-hub.
* Een voorbeeld van een toepassing uitvoeren op Pi toosend gesimuleerde sensor gegevens tooyour iothub.

Verbinding maken met gesimuleerde frambozen Pi tooan IoT-hub die u maakt. Voer vervolgens een voorbeeldtoepassing met Hallo simulator toogenerate sensorgegevens. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.

## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Hoe toowork met frambozen Pi online simulator.
* Hoe toosend sensor gegevens tooyour IoT-hub.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Overzicht van frambozen Pi web simulator

Klik op Hallo knop toolaunch frambozen Pi online simulator.

> [!div class="button"]
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Starten van de Simulator Raspberry Pi</a>

Er zijn drie gebieden in Hallo web simulator.
1. Assemblagegebied - Hallo standaard circuit is dat een Pi verbinding met een sensor BME280 en een LED maakt. Hallo-gebied is vergrendeld in de preview-versie dus momenteel niet aanpassen.
2. Het coderen van gebied - een online code-editor voor toocode met frambozen Pi. Standaard-voorbeeldtoepassing Hallo toocollect sensorgegevens helpt van BME280 sensor en tooyour Azure IoT Hub verzendt. Hallo-toepassing is volledig compatibel is met echte Pi-apparaten. 
3. Geïntegreerde consolevenster - het Hallo-uitvoer van uw code bevat. Er zijn drie knoppen Hallo bovenaan dit venster in.
   * **Voer** -Hallo toepassing uitvoert in Hallo gebied coderen.
   * **Opnieuw instellen** -Reset Hallo gebied toohello standaard voorbeeldtoepassing coderen.
   * **Vouw/uitvouwen** - op Hallo rechts naast er zich een knop voor u toofold/uitbreiden Hallo consolevenster.

> [!NOTE] 
Hallo frambozen Pi web simulator is nu beschikbaar in de preview-versie. Willen we graag toohear uw stem in Hallo [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). Hallo broncode is openbare op [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Overzicht van online simulator Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Een voorbeeld van een toepassing uitvoeren op Pi web simulator

1. Controleer of u bezig bent met Hallo standaard voorbeeldtoepassing in het gebied coderen. Hallo-tijdelijke aanduiding in regel 15 vervangen door hello Azure IoT hub apparaat-verbindingsreeks.
   ![Hallo apparaat verbindingsreeks vervangen](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Klik op **uitvoeren** of type `npm start` toorun Hallo-toepassing.


U ziet Hallo na de uitvoer die toont Hallo sensorgegevens en Hallo-berichten die worden verzonden tooyour IoT-hub ![uitvoer - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Volgende stappen

U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
