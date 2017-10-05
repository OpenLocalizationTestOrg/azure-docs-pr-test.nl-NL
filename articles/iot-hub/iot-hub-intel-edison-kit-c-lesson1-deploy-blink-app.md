---
title: 'Connect Intel Edison (C) naar Azure IoT - les 1: toepassing implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing C vanuit GitHub, en voor het implementeren van deze toepassing op het mededelingenbord Intel Edison gulp uitgevoerd. Deze voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino geleid projecten, arduino geleid knipperen, arduino geleid knipperen code, arduino knipperen programma, arduino knipperen voorbeeld
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>De Blink-toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Klonen van de voorbeeldtoepassing C vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing op Intel Edison. De voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
* Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op Edison.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid de volgende bewerkingen:

* [Uw apparaat configureren][configure-your-device]
* [Download de hulpprogramma 's][get-the-tools]

## <a name="open-the-sample-application"></a>Open de voorbeeldtoepassing
U opent de voorbeeldtoepassing door de volgende stappen uit:

1. Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

Het bestand in de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.

### <a name="install-application-dependencies"></a>Afhankelijkheden voor toepassingen installeren
Installeer de bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing met de volgende opdracht uit te voeren:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>De apparaatverbinding configureren
Volg deze stappen voor het configureren van de apparaatverbinding:

1. Het configuratiebestand van het apparaat genereren met de volgende opdracht:

   ```bash
   gulp init
   ```

   Het configuratiebestand `config-edison.json` bevat de referenties van de gebruiker die u gebruikt voor aanmelding bij Edison. Om te voorkomen dat het lek van gebruikersreferenties, het configuratiebestand wordt gegenereerd in de submap `.iot-hub-getting-started` van de basismap op uw computer.

2. Open het configuratiebestand van het apparaat in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Vervang de tijdelijke aanduiding `[device hostname or IP address]` en `[device password]` met de IP-adres en het wachtwoord die u hebt gemarkeerd omlaag in de vorige les.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Gefeliciteerd. U hebt de eerste voorbeeldtoepassing voor Edison gemaakt.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a>De Azure IoT-Hub SDK installeren op Edison
Azure IoT Hub SDK installeren op Edison met de volgende opdracht:

```bash
gulp install-tools
```

Deze taak kan lang duren om uit te voeren, afhankelijk van uw netwerkverbinding. Het moet slechts één keer worden uitgevoerd voor één Edison.

### <a name="deploy-and-run-the-sample-app"></a>Implementeren en uitvoeren van de voorbeeld-app
Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Controleer of de app werkt
De voorbeeldtoepassing wordt automatisch beëindigd nadat de LED voor 20 keer knippert. Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.

![LED knippert][led-blinking]

## <a name="summary"></a>Samenvatting
U hebt geïnstalleerd, de vereiste hulpmiddelen voor het werken met Edison en een voorbeeld van toepassing op Edison de LED knipperen geïmplementeerd. U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die Edison verbindt met Azure IoT Hub berichten te verzenden en ontvangen.

## <a name="next-steps"></a>Volgende stappen
[Download de Azure-hulpprogramma 's][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
