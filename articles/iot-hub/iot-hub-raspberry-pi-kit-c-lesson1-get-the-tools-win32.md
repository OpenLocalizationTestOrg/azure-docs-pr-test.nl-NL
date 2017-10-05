---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, knooppunt js windows installeren, npm installeren op windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0e58975f4411f97223b2c4374bdd746fe6628c42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a>Download de hulpprogramma's (Windows 7 of hoger)

> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet
Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor frambozen Pi 3. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Hoewel de programmeertaal van de belangrijkste logica C, worden in welke opgedane Node.js-hulpprogramma's gebruikt voor apparaten detecteren en te bouwen en voorbeeldtoepassingen implementeren.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Klik hier voor meer informatie over het installeren van Git en Node.js.
  * [GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem. De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.
  * [Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
* Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.
  * De minimum versievereisten voor Node.js is 4.5 TNS.
  * [NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.

## <a name="what-you-need"></a>Wat u nodig hebt

Om deze bewerking niet voltooien, moet u het:

* Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.
* Een computer waarop Windows wordt uitgevoerd.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Klik op de onderstaande koppelingen wilt downloaden en installeren van Git en Node.js LTS voor Windows.

* [Ophalen van Git voor Windows](https://git-scm.com/download/win/)
* [Node.js TNS ophalen voor Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Extra hulpprogramma's voor Node.js-ontwikkeling

Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi. Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.

Start een opdrachtprompt als beheerder. Installeer `gulp` en `device-discovery-cli` met de volgende opdracht:

```bash
npm install -g device-discovery-cli gulp
```

Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor oplossingen voor bekende problemen.

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren. Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.

## <a name="summary"></a>Samenvatting

U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd. De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.

## <a name="next-steps"></a>Volgende stappen

[De Blink-toepassing maken en implementeren](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
