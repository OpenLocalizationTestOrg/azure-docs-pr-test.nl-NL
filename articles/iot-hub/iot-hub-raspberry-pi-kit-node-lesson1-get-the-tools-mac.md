---
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, python mac installeren, installeer git op mac, gulp uitvoeren, knooppunt js mac installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>De hulpprogramma's downloaden (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet
Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw frambozen Pi 3. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi. Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.

Installeer `gulp` en `device-discovery-cli` met de volgende opdracht in de terminal:

```bash
npm install -g device-discovery-cli gulp
```

Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor oplossingen voor bekende problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren
[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.

## <a name="summary"></a>Samenvatting
U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd. De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.

## <a name="next-steps"></a>Volgende stappen
[Maken en implementeren van de voorbeeldtoepassing knipperen](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

