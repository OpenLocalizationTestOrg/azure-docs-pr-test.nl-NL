---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison Hallo op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, windows voor knooppunt js installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Ophalen van Hallo hulpprogramma's (Windows 7 of hoger)
> [!div class="op_single_selector"]
> * [Windows 7 of hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet
Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor Intel Edison Hallo Hallo downloaden. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooinstall Git en Node.js.
  * [GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem. Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.
  * [Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
* Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.
  * Hallo minimum versievereisten voor Node.js is 4.5 TNS.
  * [NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.

## <a name="what-you-need"></a>Wat u nodig hebt

toocomplete deze bewerking moet u:

* Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.
* Een computer waarop Windows wordt uitgevoerd.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Klik op onderstaande toodownload Hallo koppelingen en installeer Git en Node.js LTS voor Windows.

* [Ophalen van Git voor Windows](https://git-scm.com/download/win/)
* [Node.js TNS ophalen voor Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Extra hulpprogramma's voor Node.js-ontwikkeling

Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooEdison.

Start een opdrachtprompt als beheerder. Installeer `gulp` door het uitvoeren van de volgende opdracht Hallo:

```cmd
npm install -g gulp
```

Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.

## <a name="summary"></a>Samenvatting

U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd. de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison.

## <a name="next-steps"></a>Volgende stappen

[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
