---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Pi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, git installeren op mac gulp uitvoert, installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Hallo hulpprogramma's (Mac OS 10.10) ophalen
> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet
Hallo-software voor Hallo eerste voorbeeldtoepassing voor uw frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Hoewel Hallo programmeertaal van logische Hallo C, Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toodiscover apparaten en voorbeeldtoepassingen maken en distribueren.

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
Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Pi. Gebruik Hallo [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.

Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:

```bash
sudo npm install -g device-discovery-cli gulp
```

Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren
[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.

## <a name="summary"></a>Samenvatting
U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd. de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.

## <a name="next-steps"></a>Volgende stappen
[Hallo knipperen toepassing maken en implementeren](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

