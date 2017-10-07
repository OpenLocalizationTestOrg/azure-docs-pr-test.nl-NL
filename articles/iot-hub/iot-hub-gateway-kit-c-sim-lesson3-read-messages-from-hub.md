---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

## <a name="what-you-will-do"></a>Wat u doet

- Voorbeeldcode uitvoeren op uw host computer tooread berichten uit uw IoT-hub.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

Hoe gulp toouse Hallo hulpprogramma tooread berichten van uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Hallo gesimuleerd apparaat voorbeeld in [configureren en voer een gesimuleerd apparaat cloud uploaden voorbeeldtoepassing](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen

Hallo apparaat verbindingsreeks wordt gebruikt door uw gesimuleerde apparaat tooconnect tooyour IoT-hub. Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub.

- Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u deze niet wijzigen.
- Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`Hallo-naam die u hebt opgegeven in les 2 is.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Hallo-apparaatverbinding Hallo voorbeeld van code configureren

Bijwerken van IoT hub en het apparaat verbinding configuraties in `config-azure.json` door Hallo volgende stappen uit te voeren:

1. Open `config-azure.json` in Visual Studio Code door het uitvoeren van de volgende opdracht in een consolevenster Hallo:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Zorg Hallo vervangingen in Hallo na `config-azure.json` bestand:

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Vervang `[IoT hub connection string]` Hello IoT hub-verbindingsreeks.

## <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

Hallo gesimuleerd apparaat voorbeeldtoepassing uitvoeren en het lezen van de IoT Hub berichten door de volgende opdracht Hallo:

```bash
gulp run --iot-hub
```

Hallo-opdracht wordt uitgevoerd Hallo-toepassing die berichten tooyour iothub elke 2 seconden verzendt. Deze ook een onderliggend proces tooreceive Hallo-bericht gestart.

Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine. Hallo-toepassing wordt afgesloten in 40 seconden.

![Gesimuleerde voorbeeldtoepassing met verzonden en ontvangen berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Samenvatting

U hebt Hallo voorbeeld toepassing toosend gegevens tooyour iothub met succes uitvoeren met het gesimuleerde apparaat. U hebt ook lezen Hallo-berichten die tooyour IoT-hub zijn verzonden.

## <a name="next-steps"></a>Volgende stappen
[Een Azure Functions-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


