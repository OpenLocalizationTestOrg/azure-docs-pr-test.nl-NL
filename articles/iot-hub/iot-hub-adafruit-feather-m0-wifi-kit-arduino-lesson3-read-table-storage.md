---
title: 'Connect Arduino (C) tooAzure IoT - les 3: Table storage | Microsoft Docs'
description: Hallo apparaat-naar-cloud-berichten bewaken tijdens deze tooyour Azure Table storage worden geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Alleen berichten permanent in Azure Storage
## <a name="what-you-will-do"></a>Wat u doet
Monitor hello apparaat-naar-cloud-berichten die worden verzonden vanuit uw Adafruit Doezelaar M0 Wi-Fi Arduino mededelingenbord tooyour IoT-hub als Hallo-berichten worden geschreven tooyour Azure Table storage.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u hoe toouse hello gulp bericht lezen taak tooread-berichten permanent in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt
Voordat u deze procedure begint, moet is voltooid [hello Azure knipperen voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Nieuwe berichten in uw storage-account lezen
In het vorige artikel hello, kunt u een voorbeeld van toepassing op het mededelingenbord Arduino uitgevoerd. Hallo-voorbeeldtoepassing verzonden berichten tooyour Azure IoT hub. IoT-hub tooyour verzonden Hello-berichten worden opgeslagen in uw Azure-tabelopslag via hello Azure functie-app. U moet Hallo Azure storage connection string tooread berichten uit uw Azure-tabelopslag.

tooread berichten die zijn opgeslagen in uw Azure Table storage, als volgt te werk:

1. Hallo-verbindingsreeks ophalen door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   de eerste opdracht Hallo haalt Hallo `storage name` die wordt gebruikt in Hallo tweede opdracht tooget Hallo verbindingsreeks. Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.
2. Open Hallo-configuratiebestand `config-arduino.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Vervang `[Azure storage connection string]` met Hallo-verbindingsreeks die u in stap 1 hebt verkregen.
4. Hallo opslaan `config-arduino.json` bestand.
5. Berichten opnieuw verzenden en ze door het uitvoeren van de volgende opdracht Hallo uit uw Azure-tabelopslag lezen:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Hallo logica voor het lezen van Azure Table storage is in Hallo `azure-table.js` bestand.

   ![gulp uitgevoerd--lezen-opslag][gulp-run]

## <a name="summary"></a>Samenvatting
U hebt is uw Arduino mededelingenbord tooyour IoT-hub in de cloud Hallo verbonden en hello knipperen voorbeeld toepassing toosend apparaat-naar-cloud-berichten gebruikt. U hebt ook hello Azure functie app toostore binnenkomende IoT hub berichten tooyour Azure Table-opslag gebruikt. Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT hub tooyour Arduino het mededelingenbord.

## <a name="next-steps"></a>Volgende stappen
[Cloud-naar-apparaat-berichten verzenden][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md