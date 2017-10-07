---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: app implementeren | Microsoft Docs'
description: Hallo C voorbeeldtoepassing vanuit GitHub klonen en voer gulp toodeploy deze toepassing tooyour Intel Edison mededelingenbord. Deze voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino geleid projecten, arduino geleid knipperen, arduino geleid knipperen code, arduino knipperen programma, arduino knipperen voorbeeld
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Hallo knipperen toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Hallo C voorbeeldtoepassing vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooIntel Edison gebruiken. Hallo-voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
* Hoe toodeploy en Voer Hallo voorbeeldtoepassing op Edison.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebben voltooid Hallo volgende bewerkingen:

* [Uw apparaat configureren][configure-your-device]
* [Hallo-hulpprogramma's ophalen][get-the-tools]

## <a name="open-hello-sample-application"></a>Open Hallo-voorbeeldtoepassing
tooopen hello voorbeeldtoepassing, als volgt te werk:

1. Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.

### <a name="install-application-dependencies"></a>Afhankelijkheden voor toepassingen installeren
Hallo-bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo installeren:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren
tooconfigure Hallo apparaatverbinding, als volgt te werk:

1. Hallo apparaat configuratiebestand gegenereerd door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp init
   ```

   Hallo-configuratiebestand `config-edison.json` Hallo gebruikersreferenties u toolog in tooEdison bevat. Hallo-geheugenlek tooavoid van gebruikersreferenties, Hallo-configuratiebestand wordt gegenereerd in de submap Hallo `.iot-hub-getting-started` van Hallo basismap op uw computer.

2. Hallo apparaat configuratiebestand openen in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Vervang Hallo tijdelijke aanduiding voor `[device hostname or IP address]` en `[device password]` met Hallo IP-adres en het wachtwoord die u hebt gemarkeerd omlaag in de vorige les.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Gefeliciteerd. Hallo eerste voorbeeldtoepassing voor Edison hebt gemaakt.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo

### <a name="deploy-and-run-hello-sample-app"></a>Implementeren en Hallo voorbeeld-app uitvoeren
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Controleer of de app werkt het Hallo
Hallo-voorbeeldtoepassing wordt automatisch beëindigd nadat Hallo LED voor 20 keer knippert. Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.

![LED knippert][led-blinking]

## <a name="summary"></a>Samenvatting
U hebt geïnstalleerd Hallo vereist extra toowork met Edison en een voorbeeld toepassing tooEdison tooblink Hallo LED geïmplementeerd. U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die verbinding Edison tooAzure toosend IoT Hub maakt en ontvangen van berichten.

## <a name="next-steps"></a>Volgende stappen
[Hello Azure-hulpprogramma's ophalen][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
