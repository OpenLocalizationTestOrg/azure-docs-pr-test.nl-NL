---
title: 'Connect Intel Edison (C) naar Azure IoT - les 4: berichten ontvangen | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Edison en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten naar Edison uit uw iothub de LED knipperen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b7de7a8b53cdb1d7c2560225fce9166e555e5123
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Voer een voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen
In dit artikel hebt implementeren u een voorbeeld van toepassing op Intel Edison. De voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub. U kunt ook een taak gulp uitvoeren op uw computer om berichten te verzenden naar Edison uit uw IoT-hub. Wanneer de voorbeeldtoepassing de berichten ontvangt, wordt de LED knippert. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-do"></a>Wat u doet
* Verbinding maken met de voorbeeldtoepassing met uw iothub.
* Implementeren en uitvoeren van de voorbeeldtoepassing.
* Berichten verzenden van uw IoT-hub naar Edison de LED knipperen.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Het bewaken van inkomende berichten van uw IoT-hub.
* Het verzenden van cloud naar apparaat-berichten uit uw IoT-hub aan Edison.

## <a name="what-you-need"></a>Wat u nodig hebt
* Intel Edison ingesteld voor gebruik. Zie voor meer informatie over het instellen van Edison, [configureren van uw apparaat][configure-your-device].
* Een IoT-hub die wordt gemaakt in uw Azure-abonnement. Zie voor meer informatie over het maken van uw IoT-hub, [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Verbinding maken met de voorbeeldtoepassing met uw iothub
1. Zorg ervoor dat u in de map opslagplaats `iot-hub-c-edison-getting-started`. De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:

   ```bash
   cd Lesson4
   code .
   ```

   Het bestand in de `app` submap is het belangrijkste bronbestand met de code voor het bewaken van binnenkomende berichten uit iothub. De `blinkLED` functie de LED knippert.

   ![Structuur van de opslagplaats in de voorbeeldtoepassing][repo-structure]
2. Het configuratiebestand initialiseren met de volgende opdrachten:

   ```bash
   npm install
   gulp init
   ```

   Als u de stappen in voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle configuraties worden overgenomen, zodat u kunt de stap overslaan voor de taak van het implementeren en uitvoeren van de voorbeeldtoepassing. Als u de stappen in voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u Vervang de tijdelijke aanduidingen in de `config-edison.json` bestand. De `config-edison.json` bestand bevindt zich in de submap van de basismap.

   ![Inhoud van het bestand config edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Vervang **[apparaat-hostnaam of IP-adres]** met het apparaat IP-adres dat u naar beneden gemarkeerd wanneer u uw apparaat geconfigureerd.
   * Vervang **[apparaat-verbindingsreeks IoT]** met de verbindingsreeks voor apparaten die u door het uitvoeren van de `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.
   * Vervang **[IoT hub verbindingsreeks]** met de verbindingsreeks voor IoT-hub die u door het uitvoeren van de `az iot hub show-connection-string --name {my hub name}` opdracht.

   > [!NOTE]
   > Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdrachten:

```bash
gulp deploy && gulp run
```

De opdracht gulp implementeert de voorbeeldtoepassing voor Edison. Vervolgens wordt de toepassing uitgevoerd op Edison en een afzonderlijke taak op de hostcomputer Edison 20 knipperen berichten verzenden van uw IoT-hub.

Na de voorbeeldtoepassing wordt uitgevoerd, start het luisteren naar berichten van uw IoT-hub. Ondertussen verzendt de taak gulp aantal 'knipperen' e-mailberichten van uw IoT-hub naar Edison. Voor elk bericht knipperen die Edison ontvangt, de voorbeeldtoepassing roept de `blinkLED` functie de LED knipperen.

U ziet de LED knipperen elke twee seconden als de taak gulp 20 berichten uit uw IoT-hub naar Edison verzendt. Het laatste bestand is een 'stop'-bericht dat Hiermee stopt u de toepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][gulp-command-and-blink-messages]

## <a name="summary"></a>Samenvatting
U hebt berichten verzonden van uw IoT-hub naar Edison de LED knipperen. De volgende taak is optioneel: de aan- en uitgeschakeld gedrag van de LED wijzigen.

## <a name="next-steps"></a>Volgende stappen
[De on- en uitgeschakeld gedrag van de LED wijzigen][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md