---
title: 'Verbinding maken met Arduino tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Adafruit Doezelaar M0 Wi-Fi op Mac OS.
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
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Hallo hulpprogramma's (Mac OS 10.10) ophalen
> [!div class="op_single_selector"]
> * [Windows 7 of hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet

Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino Hallo Hallo downloaden. 

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

> [!NOTE]
> Hoewel Hallo programmeertaal van logische Hallo Arduino is, wordt Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toobuild en voorbeeldtoepassingen implementeren.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooinstall Git en Node.js.
  * [GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem. Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.
  * [Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
* Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.
  * Hallo minimaal vereiste versie van Node.js is 4.5 TNS.
  * [NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.

## <a name="what-you-need"></a>Wat u nodig hebt
toocomplete deze bewerking moet u:
* Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.
* Een Mac met Mac OS Yosemite (10.10) of hoger.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js
tooinstall Git en Node.js, gebruikt u Hallo [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:

1. Homebrew installeren. Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.

   1. Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.
   2. Hallo volgende opdracht uitvoeren:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Installeer Git en Node.js Hallo na de opdracht uitgevoerd:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Extra hulpprogramma's voor Node.js-ontwikkeling
Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Arduino het mededelingenbord.

Installeer `gulp`, `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:

```bash
sudo npm install -g gulp device-discovery-cli
```

Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren
[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.

## <a name="summary"></a>Samenvatting
U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd. de volgende taak Hallo is toocreate, implementeren en Hallo voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino.

## <a name="next-steps"></a>Volgende stappen
[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md