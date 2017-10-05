---
featureFlags: usabilla
title: 'Raspberry Pi (knooppunt) verbinden met Azure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: De voorbeeldtoepassing wordt uitgevoerd op Pi en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten naar Pi uit uw iothub de LED knipperen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud naar apparaat, het bericht uit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a>Uitvoeren van de voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen
In dit artikel hebt implementeren u een voorbeeld van toepassing op frambozen Pi 3. De voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub. U kunt ook een taak gulp uitvoeren op uw computer om berichten te verzenden naar Pi uit uw IoT-hub. Wanneer de voorbeeldtoepassing de berichten ontvangt, wordt de LED knippert. Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Wat u doet
* Verbinding maken met de voorbeeldtoepassing met uw iothub.
* Implementeren en uitvoeren van de voorbeeldtoepassing.
* Berichten verzenden van uw IoT-hub tot Pi de LED knipperen.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Het bewaken van inkomende berichten van uw IoT-hub
* Het cloud-naar-apparaat-berichten verzenden vanuit uw IoT-hub tot Pi.

## <a name="what-you-need"></a>Wat u nodig hebt
* Raspberry Pi 3, die zijn ingesteld voor gebruik. Zie voor meer informatie over het instellen van Pi, [configureren van uw apparaat](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Een IoT-hub die wordt gemaakt in uw Azure-abonnement. Zie voor meer informatie over het maken van uw IoT-hub, [uw IoT-hub maken en registreren van frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Verbinding maken met de voorbeeldtoepassing met uw iothub
1. Zorg ervoor dat u in de map opslagplaats `iot-hub-node-raspberrypi-getting-started`. De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   U ziet de `app.js` bestand de `app` submap. De `app.js` bestand is het belangrijkste bronbestand met de code voor het bewaken van binnenkomende berichten uit iothub. De `blinkLED` functie de LED knippert.
   
   ![Structuur van de opslagplaats in de voorbeeldtoepassing](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Het configuratiebestand initialiseren met de volgende opdrachten:
   
   ```bash
   npm install
   gulp init
   ```
   
   Als u de stappen in voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op deze computer, alle configuraties worden overgenomen, zodat u kunt doorgaan met de taak van het implementeren en uitvoeren van de voorbeeldtoepassing. Als u de stappen in voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op een andere computer, moet u Vervang de tijdelijke aanduidingen in de `config-raspberrypi.json` bestand. De `config-raspberrypi.json` bestand bevindt zich in de submap van de basismap.
   
   ![Inhoud van het bestand config raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Vervang **[apparaat-hostnaam of IP-adres]** met het IP-adres van Pi of de hostnaam die u door het uitvoeren van de `devdisco list --eth` opdracht.
* Vervang **[apparaat-verbindingsreeks IoT]** met de verbindingsreeks voor apparaten die u door het uitvoeren van de `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` opdracht.
* Vervang **[IoT hub verbindingsreeks]** met de verbindingsreeks voor IoT-hub die u door het uitvoeren van de `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` opdracht.

> [!NOTE]
> Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op Pi met de volgende opdracht:

```bash
gulp deploy && gulp run
```

De opdracht implementeert de voorbeeldtoepassing tot Pi. Vervolgens wordt de toepassing uitgevoerd op Pi en een afzonderlijke taak op de hostcomputer Pi 20 knipperen berichten verzenden van uw IoT-hub.

Na de voorbeeldtoepassing wordt uitgevoerd, start het luisteren naar berichten van uw IoT-hub. De taak gulp verzendt ondertussen diverse 'knipperen'-berichten van uw IoT-hub tot Pi. Voor elk bericht knipperen die Pi ontvangt, de voorbeeldtoepassing roept de `blinkLED` functie de LED knipperen.

U ziet de LED knipperen elke twee seconden als de taak gulp 20 berichten uit uw iothub tot Pi verzendt. Het laatste bestand is een 'stop' weergegeven waarin wordt gemeld de toepassing dat meer uitgevoerd.

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Samenvatting
U hebt verzonden berichten uit uw IoT-hub tot Pi de LED knipperen. De volgende taak is optioneel: de aan- en uitgeschakeld gedrag van de LED wijzigen.

## <a name="next-steps"></a>Volgende stappen
[De on- en uitgeschakeld gedrag van de LED wijzigen](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

