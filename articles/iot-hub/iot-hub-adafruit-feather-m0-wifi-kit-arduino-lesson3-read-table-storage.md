---
title: 'Connect Arduino (C) naar Azure IoT - les 3: Table storage | Microsoft Docs'
description: De apparaat-naar-cloud-berichten bewaken omdat ze naar uw Azure Table-opslag zijn geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
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
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Alleen berichten permanent in Azure Storage
## <a name="what-you-will-do"></a>Wat u doet
Controleer de apparaat-naar-cloud-berichten die vanaf het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino naar uw IoT-hub worden verzonden omdat de berichten naar uw Azure Table-opslag zijn geschreven.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u hoe u met de taak bericht lezen gulp lezen berichten permanent in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt
Voordat u deze procedure begint, moet is voltooid [de voorbeeldtoepassing Azure knipperen uitvoeren op het mededelingenbord Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Nieuwe berichten in uw storage-account lezen
In het vorige artikel kunt u een voorbeeld van toepassing op het mededelingenbord Arduino uitgevoerd. De voorbeeld-toepassing verzonden berichten naar uw Azure-IoT-hub. De verzonden naar uw IoT-hub berichten worden opgeslagen in uw Azure Table storage via de Azure-functie-app. U moet de verbindingsreeks voor Azure-opslag om berichten te lezen uit uw Azure-tabelopslag.

Als u wilt lezen van berichten die zijn opgeslagen in uw Azure Table storage, de volgende stappen uit:

1. De verbindingsreeks ophalen met de volgende opdrachten:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   De eerste opdracht haalt de `storage name` die wordt gebruikt in de tweede opdracht om de verbindingsreeks ophalen. Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.
2. Open het configuratiebestand `config-arduino.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Vervang `[Azure storage connection string]` met de verbindingsreeks die u in stap 1 hebt verkregen.
4. Sla de `config-arduino.json` bestand.
5. Berichten opnieuw verzenden en ze uit uw Azure-tabelopslag lezen door de volgende opdracht uit te voeren:

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   De logica voor het lezen van Azure Table storage is in de `azure-table.js` bestand.

   ![gulp uitgevoerd--lezen-opslag][gulp-run]

## <a name="summary"></a>Samenvatting
U hebt is het mededelingenbord Arduino verbonden met uw IoT-hub in de cloud en de voorbeeldtoepassing knipperen gebruikt om apparaat-naar-cloud-berichten te verzenden. U hebt ook de functie Azure-app gebruikt voor het opslaan van IoT hub berichten naar uw Azure Table-opslag. Nu kunt u op het mededelingenbord Arduino cloud-naar-apparaat-berichten uit uw IoT-hub verzenden.

## <a name="next-steps"></a>Volgende stappen
[Cloud-naar-apparaat-berichten verzenden][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md