---
featureFlags: usabilla
title: 'Raspberry Pi (knooppunt) verbinden met Azure IoT - les 1: app implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing Node.js vanuit GitHub en gulp voor het implementeren van deze toepassing op het mededelingenbord frambozen Pi 3. Deze voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Raspberry pi geleid knipperen, knipperen geleid met raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>De Blink-toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Klonen van de voorbeeldtoepassing Node.js vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing op uw frambozen Pi 3. De voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Het gebruik van de `device-discover-cli` hulpprogramma netwerken informatie ophalen over Pi.
* Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op Pi.
* Het implementeren en foutopsporing op afstand worden uitgevoerd op Pi-toepassingen.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid de volgende bewerkingen:

* [Uw apparaat configureren](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [Download de hulpprogramma 's](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a>Het IP-adres en hostnaam de naam van Pi verkrijgen
Open een opdrachtprompt in Windows of in een terminal in Mac OS of Ubuntu en voer vervolgens de volgende opdracht:

```bash
devdisco list --eth
```

Hier ziet u uitvoer die vergelijkbaar is met het volgende:

![Detectie van netwerkapparaten](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Noteer de `IP address` en `hostname` van Pi. U moet deze informatie later in dit artikel.

> [!NOTE]
> Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer. Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.

## <a name="clone-the-sample-application"></a>De voorbeeldtoepassing klonen
U opent de voorbeeldcode door de volgende stappen uit:

1. Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

De `app.js` bestand de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.

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
   
   Het configuratiebestand `config-raspberrypi.json` bevat de referenties van de gebruiker die u gebruikt voor aanmelding bij Pi. Om te voorkomen dat het lek van gebruikersreferenties, het configuratiebestand wordt gegenereerd in de submap `.iot-hub-getting-started` van de basismap op uw computer.

2. Open het configuratiebestand van het apparaat in Visual Studio Code met de volgende opdracht:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. Vervang de tijdelijke aanduiding `[device hostname or IP address]` met het IP-adres of de hostnaam die u eerder hebt verkregen in ' de IP-adres en hostnaam naam achterhalen van Pi."
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> U kunt SSH-sleutel in plaats van de gebruikersnaam en wachtwoord gebruiken bij het verbinden met frambozen Pi. Hiervoor hebt, moet u de sleutel genereren met **ssh-keygen** en **ssh-exemplaar-id pi @\<adres van apparaat\>**.
>
> In Windows deze opdrachten zijn beschikbaar in **Git Bash**.
>
> Op Mac OS die u wilt uitvoeren **brew installeren ssh-exemplaar-id**.
>
> Na het uploaden is de sleutel tot het Pi frambozen, Vervang **device_password** met **device_key_path** eigenschap in **config raspberrypi.json**.
>
> Bijgewerkte regels ziet er als hieronder:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Gefeliciteerd. U hebt de eerste voorbeeldtoepassing voor Pi gemaakt.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
### <a name="install-nodejs-and-npm-on-pi"></a>Node.js en NPM op Pi installeren
Node.js en NPM met Pi installeren met de volgende opdracht:

```bash
gulp install-tools
```

Deze taak duurt 10 minuten de eerste keer dat u deze uitvoeren.

### <a name="deploy-and-run-the-sample-app"></a>Implementeren en uitvoeren van de voorbeeld-app
Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Controleer of de app werkt
U ziet nu de LED op Pi knippert elke twee seconden.  Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor oplossingen voor bekende problemen.
![LED knippert](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Samenvatting
U hebt de vereiste hulpmiddelen voor het werken met Pi geïnstalleerd en een voorbeeldtoepassing tot Pi de LED knipperen geïmplementeerd. U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die Pi verbindt met Azure IoT Hub berichten te verzenden en ontvangen.

## <a name="next-steps"></a>Volgende stappen
[Download de Azure-hulpprogramma 's](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

