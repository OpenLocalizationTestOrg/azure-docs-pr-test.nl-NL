---
title: 'Arduino verbinden met Azure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Adafruit Doezelaar M0 Wi-Fi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git installeren op mac installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a6dc2555367e5fe530b3acde1f1f04ac442fb638
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>De hulpprogramma's downloaden (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 of hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet

Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino. 

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

> [!NOTE]
> Hoewel de programmeertaal van de belangrijkste logica Arduino, worden in de uitkomsten Node.js-hulpprogramma's om te bouwen en implementeren van de voorbeeldtoepassingen gebruikt.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Klik hier voor meer informatie over het installeren van Git en Node.js.
  * [GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem. De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.
  * [Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
* Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.
  * De minimaal vereiste versie van Node.js is 4.5 TNS.
  * [NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.

## <a name="what-you-need"></a>Wat u nodig hebt
Om deze bewerking niet voltooien, moet u het:
* Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.
* Een Mac met Mac OS Yosemite (10.10) of hoger.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js
U installeert Git en Node.js via de [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:

1. Homebrew installeren. Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.

   1. Druk op `Cmd + Space` en voer `Terminal` een terminal openen.
   2. Voer de volgende opdracht uit:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Git en Node.js installeren met de volgende opdracht:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Extra hulpprogramma's voor Node.js-ontwikkeling
Gebruik [gulp.js](http://gulpjs.com) voor de implementatie van de voorbeeldtoepassing op het mededelingenbord Arduino automatiseren.

Installeer `gulp`, `device-discovery-cli` met de volgende opdracht in de terminal:

```bash
sudo npm install -g gulp device-discovery-cli
```

Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren
[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.

## <a name="summary"></a>Samenvatting
U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd. De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino.

## <a name="next-steps"></a>Volgende stappen
[De toepassing knipperen maken en implementeren][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md