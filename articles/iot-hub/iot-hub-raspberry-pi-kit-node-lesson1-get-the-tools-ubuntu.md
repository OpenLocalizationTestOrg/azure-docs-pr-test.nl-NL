---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi Hallo op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Hallo hulpprogramma's (Ubuntu 16.04) ophalen

> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Wat u doet
Hallo-software voor Hallo eerste voorbeeldtoepassing voor frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooinstall Git en Node.js.
  * [GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem. Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.
  * [Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
* Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.
  * Hallo minimaal vereiste versie van Node.js is 4.5 TNS.
  * [NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.

## <a name="what-do-you-need"></a>Wat moet u
toocomplete deze bewerking moet u:

* Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.
* Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.

## <a name="install-git-nodejs-and-npm"></a>Installeer Git, Node.js en NPM
Gebruik Hallo sneltoets `Ctrl + Alt + T` tooopen een terminal en Voer Hallo volgende opdrachten:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Extra hulpprogramma's voor Node.js-ontwikkeling
U gebruikt [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooPi. U ook hello gebruiken [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.

Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:

```bash
sudo npm install -g device-discovery-cli gulp
```

Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor toocommon oplossingen voor problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren
[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.

## <a name="summary"></a>Samenvatting
U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd. de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.

## <a name="next-steps"></a>Volgende stappen
[Hallo knipperen voorbeeldtoepassing maken en implementeren](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

