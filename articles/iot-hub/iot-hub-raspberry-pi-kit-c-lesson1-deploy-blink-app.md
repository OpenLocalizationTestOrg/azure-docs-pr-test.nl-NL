---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 1: app implementeren | Microsoft Docs'
description: Kloon Hallo C voorbeeldtoepassing vanuit GitHub en gulp toodeploy het mededelingenbord tooyour frambozen Pi 3 van deze toepassing. Deze voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Raspberry pi geleid knipperen, knipperen geleid met raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Hallo knipperen toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Hallo voorbeeldtoepassing C vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooRaspberry Pi 3 gebruiken. Hallo-voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe toouse hello `device-discover-cli` hulpprogramma tooretrieve informatie over Pi over het netwerk.
* Hoe toodeploy en Voer Hallo voorbeeldtoepassing met Pi.
* Hoe toodeploy en foutopsporing toepassingen die worden uitgevoerd op afstand met Pi.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebben voltooid Hallo volgende bewerkingen:

* [Uw apparaat configureren](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Hallo-hulpprogramma's ophalen](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Hallo IP-adres en hostnaam naam verkregen van Pi
Open een opdrachtprompt in Windows of in een terminal in Mac OS of Ubuntu en voer vervolgens Hallo volgende opdracht:

```bash
devdisco list --eth
```

Hier ziet u uitvoer die vergelijkbaar toohello volgende:

![Detectie van netwerkapparaten](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Let op Hallo `IP address` en `hostname` van Pi. U moet deze informatie later in dit artikel.

> [!NOTE]
> Zorg ervoor dat Pi verbonden toohello netwerk als de computer is. Bijvoorbeeld, als uw computer verbonden tooa draadloze netwerk is wanneer Pi verbonden tooa standaardnetwerk is, ziet u mogelijk niet Hallo IP-adres in Hallo devdisco uitvoer.

## <a name="open-hello-sample-application"></a>Open Hallo-voorbeeldtoepassing
tooopen hello voorbeeldtoepassing, als volgt te werk:

1. Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Hallo `main.c` bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.

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
   
   Hallo-configuratiebestand `config-raspberrypi.json` Hallo gebruikersreferenties u toolog in tooPi bevat. Hallo-geheugenlek tooavoid van gebruikersreferenties, Hallo-configuratiebestand wordt gegenereerd in de submap Hallo `.iot-hub-getting-started` van Hallo basismap op uw computer.

2. Hallo apparaat configuratiebestand openen in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Vervang Hallo tijdelijke aanduiding voor `[device hostname or IP address]` met Hallo IP-adres of hostnaam Hallo die u eerder hebt verkregen in "Verkrijgen Hallo IP-adres en hostnaam naam van Pi."
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> U kunt SSH-sleutel in plaats van de gebruikersnaam en wachtwoord gebruiken wanneer u verbinding maakt tooRaspberry Pi. In volgorde toodo dit hebt u toogenerate Hallo sleutel met behulp van **ssh-keygen** en **ssh-exemplaar-id pi @\<adres van apparaat\>**.
>
> In Windows deze opdrachten zijn beschikbaar in **Git Bash**.
>
> Op Mac OS moet u toorun **brew installeren ssh-exemplaar-id**.
>
> Na het uploaden is Hallo sleutel toohello frambozen Pi, Vervang **device_password** met **device_key_path** eigenschap in **config raspberrypi.json**.
>
> Bijgewerkte regels ziet er als hieronder:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Gefeliciteerd. U hebt gemaakt Hallo eerste voorbeeldtoepassing voor Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Hello Azure IoT Hub SDK op Pi installeren
Hello Azure IoT Hub SDK installeren op Pi door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp install-tools
```

Deze taak duurt een paar minuten toocomplete Hallo eerste keer dat u deze uitvoeren.

### <a name="deploy-and-run-hello-sample-app"></a>Implementeren en Hallo voorbeeld-app uitvoeren
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Controleer of de app werkt het Hallo
Hallo-voorbeeldtoepassing wordt automatisch beëindigd nadat Hallo LED voor 20 keer knippert. Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.
![LED knippert](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Samenvatting
U hebt geïnstalleerd Hallo vereist extra toowork met Pi en een voorbeeld toepassing tooPi tooblink Hallo LED geïmplementeerd. U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die verbinding Pi tooAzure toosend IoT Hub maakt en ontvangen van berichten.

## <a name="next-steps"></a>Volgende stappen
[Azure-hulpprogramma's ophalen](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

