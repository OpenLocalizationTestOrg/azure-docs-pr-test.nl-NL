---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op de hostcomputer de berichten lezen uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

## <a name="what-you-will-do"></a>Wat u doet

- Voorbeeldcode uitvoeren op de hostcomputer om berichten te lezen uit uw IoT-hub.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

Het gebruik van het hulpprogramma gulp om berichten te lezen uit uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Het gesimuleerde apparaat voorbeeld in [configureren en voer een gesimuleerd apparaat cloud uploaden voorbeeldtoepassing](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen

De verbindingsreeks van het apparaat wordt gebruikt door uw gesimuleerde apparaat verbinding maken met uw IoT-hub. De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinding maken met het identiteitenregister van uw IoT-hub voor het beheren van de apparaten die verbinding maken met uw IoT-hub zijn toegestaan.

- Een overzicht van uw IoT-hubs in de resourcegroep met de volgende opdracht:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Gebruik `iot-gateway` als de waarde van `{resource group name}` als u deze niet wijzigen.
- De IoT hub-verbindingsreeks ophalen met de volgende opdracht:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`is de naam die u hebt opgegeven in les 2.

## <a name="configure-the-device-connection-for-the-sample-code"></a>Het apparaatverbinding configureren voor de voorbeeldcode

Bijwerken van IoT hub en het apparaat verbinding configuraties in `config-azure.json` door de volgende stappen uit te voeren:

1. Open `config-azure.json` in Visual Studio Code met de volgende opdracht in een consolevenster:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Controleer de volgende vervangingen in de `config-azure.json` bestand:

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Vervang `[IoT hub connection string]` met de verbindingsreeks van de IoT-hub.

## <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub

Voer de voorbeeldtoepassing gesimuleerde apparaat en IoT Hub berichten lezen door de volgende opdracht:

```bash
gulp run --iot-hub
```

De opdracht wordt de toepassing die berichten naar uw IoT-hub elke 2 seconden verzendt uitgevoerd. Deze ook een onderliggend proces voor het ontvangen van het bericht gestart.

De berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op de dezelfde consolevenster in de hostmachine. De toepassing wordt afgesloten in 40 seconden.

![Gesimuleerde voorbeeldtoepassing met verzonden en ontvangen berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Samenvatting

U hebt de voorbeeldtoepassing gegevens verzenden naar uw IoT-hub met gesimuleerde apparaat uitgevoerd. U hebt ook de berichten die zijn verzonden naar uw IoT-hub lezen.

## <a name="next-steps"></a>Volgende stappen
[Een Azure Functions-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


