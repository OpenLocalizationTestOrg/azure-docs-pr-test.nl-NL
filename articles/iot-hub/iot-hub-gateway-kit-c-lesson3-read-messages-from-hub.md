---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

## <a name="what-you-will-do"></a>Wat u doet

- Voorbeeldcode uitvoeren op uw host computer tooread berichten uit uw IoT-hub.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

Hoe gulp toouse Hallo hulpprogramma tooread berichten van uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Hallo uitschakelen-voorbeeldtoepassing die u in les 3 uitgevoerd.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen

Hallo apparaat verbindingsreeks wordt gebruikt door uw apparaat (TI SensorTag of gesimuleerd apparaat) tooconnect tooyour IoT-hub. Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub.

- Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.
- Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`Hallo-naam die u hebt opgegeven in les 2 is.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Hallo-apparaatverbinding Hallo voorbeeld van code configureren

Update Hallo apparaat configuratiebestand `config-azure.json` zodat u berichten uit uw IoT-hub op de hostcomputer lezen kan. toodo dit als volgt te werk:

1. Open `config-azure.json` in Visual Studio Code door het uitvoeren van de volgende opdracht in een consolevenster Hallo:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Zorg Hallo vervangingen in Hallo na `config-azure.json` bestand:

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Vervang `[IoT hub connection string]` Hello verbindingsreeks van het IoT-hub die u hebt verkregen.

## <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

Als u een SensorTag TI hebt, zorg er dan voor dat uw SensorTag is al ingeschakeld. Hallo gateway voorbeeldtoepassing uitvoeren en het lezen van de IoT Hub berichten door de volgende opdracht Hallo:

```bash
gulp run --iot-hub
```

Hallo-opdracht wordt uitgevoerd Hallo uitschakelen-voorbeeldtoepassing die leest en pakketten temperatuur gegevens van uw SensorTag of het gesimuleerde apparaat en elke 2 seconden voor Hallo-bericht tooyour iothub verzendt. Deze ook een onderliggend proces tooreceive Hallo-bericht gestart.

Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine. Hallo voorbeeld toepassingsexemplaar wordt in 40 seconden automatisch beëindigd.

![Voorbeeldtoepassing uitschakelen met verzonden en ontvangen van berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Samenvatting

U hebt een code voorbeeld tooread berichten uitvoeren van uw IoT-hub. U bent klaar tooread Hallo-berichten die zijn opgeslagen in uw Azure-tabelopslag.

## <a name="next-steps"></a>Volgende stappen
[Een Azure Functions-app en Azure Storage-account maken](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


