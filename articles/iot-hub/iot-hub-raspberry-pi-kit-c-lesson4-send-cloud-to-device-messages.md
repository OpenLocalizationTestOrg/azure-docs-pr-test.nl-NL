---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Pi en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooPi van uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: cloud toodevice, het bericht uit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten
In dit artikel hebt implementeren u een voorbeeld van toepassing op frambozen Pi 3. Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub. U ook uitvoeren een gulp taak op uw computer toosend berichten tooPi uit uw IoT-hub. Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-do"></a>Wat u doet
* Sluit Hallo voorbeeld toepassing tooyour iothub.
* Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.
* Berichten verzenden van uw IoT hub tooPi tooblink Hallo LED.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe toomonitor binnenkomende berichten uit uw IoT-hub.
* Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooPi.

## <a name="what-you-need"></a>Wat u nodig hebt
* Raspberry Pi 3, die zijn ingesteld voor gebruik. hoe tooset van Pi, Zie toolearn [configureren van uw apparaat](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).
* Een IoT-hub die wordt gemaakt in uw Azure-abonnement. toolearn hoe toocreate uw IoT-hub Zie [uw IoT-hub maken en registreren van frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub
1. Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-c-raspberrypi-getting-started`. Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd Lesson4
   code .
   ```

   Kennisgeving Hallo `app.c` bestand in Hallo `app` submap. Hallo `app.c` bestand is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat. Hallo `blinkLED` functie Hallo LED knippert.

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   npm install
   gulp init
   ```

   Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt toostep toohello taak implementeren en uitvoeren van de voorbeeldtoepassing Hallo overslaan. Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-raspberrypi.json` bestand. Hallo `config-raspberrypi.json` bestand bevindt zich in de submap Hallo van de basismap.

   ![Inhoud van Hallo config raspberrypi.json bestand](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Vervang **[apparaat-hostnaam of IP-adres]** met Pi van IP-adres of de hostnaam naam die u door het uitvoeren van Hallo `devdisco list --eth` opdracht.
* Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` opdracht.
* Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` opdracht.

> [!NOTE]
> Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdrachten Hallo:

```
gulp deploy && gulp run
```

Hallo gulp opdracht is uitgevoerd Hallo eerst taak install-hulpprogramma's. Vervolgens implementeert het Hallo voorbeeld toepassing tooPi. Ten slotte op wordt uitgevoerd toepassing hello Pi en een afzonderlijke taak op uw host computer toosend 20 knipperen berichten tooPi uit uw IoT-hub.

Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub. Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooPi. Voor elk bericht knipperen die Pi ontvangt, roept de voorbeeldtoepassing Hallo Hallo `blinkLED` functie tooblink Hallo LED.

U ziet Hallo LED knipperen elke twee seconden als Hallo taak verzendt 20 berichten van uw IoT hub tooPi gulp. Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a>Samenvatting
U hebt berichten uit uw IoT hub tooPi tooblink Hallo LED verzonden. de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.

## <a name="next-steps"></a>Volgende stappen
[Hallo in- en uitschakelen gedrag van Hallo LED wijzigen](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
