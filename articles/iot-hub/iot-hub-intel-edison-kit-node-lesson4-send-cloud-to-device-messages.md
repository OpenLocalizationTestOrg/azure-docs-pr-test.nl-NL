---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 4: berichten ontvangen | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Edison en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooEdison van uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten
In dit artikel hebt implementeren u een voorbeeld van toepassing op Intel Edison. Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub. U ook uitvoeren een gulp taak op uw computer toosend berichten tooEdison uit uw IoT-hub. Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-do"></a>Wat u doet
* Sluit Hallo voorbeeld toepassing tooyour iothub.
* Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.
* Berichten verzenden van uw IoT hub tooEdison tooblink Hallo LED.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe toomonitor binnenkomende berichten uit uw IoT-hub.
* Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooEdison.

## <a name="what-you-need"></a>Wat u nodig hebt
* Intel Edison ingesteld voor gebruik. hoe tooset up Edison, Zie toolearn [configureren van uw apparaat][configure-your-device].
* Een IoT-hub die wordt gemaakt in uw Azure-abonnement. toolearn hoe toocreate uw IoT-hub Zie [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub
1. Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-node-edison-getting-started`. Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd Lesson4
   code .
   ```

   Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat. Hallo `blinkLED` functie Hallo LED knippert.

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing][repo-structure]
2. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   npm install
   gulp init
   ```

   Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt Hallo stap toohello taak voor het implementeren van overslaan en Hallo-voorbeeldtoepassing wordt uitgevoerd. Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-edison.json` bestand. Hallo `config-edison.json` bestand bevindt zich in de submap Hallo van de basismap.

   ![Inhoud van Hallo config edison.json bestand](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Vervang **[apparaat-hostnaam of IP-adres]** met Hallo apparaat IP-adres u omlaag gemarkeerd wanneer u uw apparaat geconfigureerd.
   * Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.
   * Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name}` opdracht.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdrachten Hallo:

```bash
gulp deploy && gulp run
```

Hallo gulp opdracht implementeert Hallo voorbeeld toepassing tooEdison. Vervolgens waarop de toepassing hello Edison en een afzonderlijke taak op de host computer toosend 20 knipperen berichten tooEdison uit uw IoT-hub.

Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub. Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooEdison. Voor elk bericht knipperen die Edison ontvangt, roept de voorbeeldtoepassing Hallo Hallo `blinkLED` functie tooblink Hallo LED.

U ziet Hallo LED knipperen elke twee seconden als Hallo taak verzendt 20 berichten van uw IoT hub tooEdison gulp. Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][gulp-command-and-blink-messages]

## <a name="summary"></a>Samenvatting
U hebt berichten uit uw IoT hub tooEdison tooblink Hallo LED verzonden. de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.

## <a name="next-steps"></a>Volgende stappen
[Hallo in- en uitschakelen gedrag van Hallo LED wijzigen][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md