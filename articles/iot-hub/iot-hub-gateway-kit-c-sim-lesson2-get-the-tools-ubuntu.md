---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: De hulpprogramma's en de software installeren op de hostcomputer Ubuntu uitgevoerd, een iothub maken en Registreer uw apparaat in de IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>De hulpprogramma's downloaden (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet

- Installeer Git, Node.js, Gulp, Python.
- Installeer de Azure-opdrachtregelinterface (Azure CLI). 

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).
## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Klik hier voor meer informatie over het installeren van Git en Node.js.
  - GIT is een open-source gedistribueerd versiebeheersysteem. De voorbeeldtoepassing voor deze les wordt opgeslagen op Git.
  - Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
- Hoe Node.js ontwikkelingsprogramma's installeren met NPM.
  - De minimaal vereiste versie van Node.js is 4.5 TNS.
  - NPM is een van de pakket-managers voor Node.js.
- Klik hier voor meer informatie over het installeren van Visual Studio Code.
  - Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.
- Het installeren van de Azure CLI
  - De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanaf een opdrachtregel inrichten en beheren van resources.
- Het gebruik van de Azure CLI voor het maken van een IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een internetverbinding beschikken om het downloaden van de hulpprogramma's en software.
- Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Volg deze stappen voor het installeren van de Git- en Node.js:

1. Druk op `Ctrl + Alt + T` een terminal openen.
2. Voer de volgende opdrachten uit:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.

Als u wilt installeren gulp, voer de volgende opdracht in de terminal:

```bash
sudo npm install -g gulp
```

Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-the-azure-cli"></a>Azure-CLI installeren

Volg deze stappen voor het installeren van de Azure CLI:

1. Voer de volgende opdrachten in de terminal:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   De installatie kan 5 minuten duren.

2. De installatie controleren door de volgende opdracht uit te voeren:

   ```bash
   az iot -h
   ```
U ziet de volgende uitvoer als de installatie geslaagd is.
![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Visual Studio Code installeren

U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.

[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U hebt de vereiste hulpprogramma's en software op uw computer geïnstalleerd. Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
