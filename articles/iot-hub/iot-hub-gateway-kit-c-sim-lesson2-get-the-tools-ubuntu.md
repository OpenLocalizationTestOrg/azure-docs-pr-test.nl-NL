---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Hallo-hulpprogramma's en Hallo software installeren op de hostcomputer Ubuntu uitgevoerd, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
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
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Hallo hulpprogramma's (Ubuntu 16.04) ophalen
> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet

- Installeer Git, Node.js, Gulp, Python.
- Hello Azure-opdrachtregelinterface (Azure CLI) installeren. 

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).
## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe tooinstall Git en Node.js.
  - GIT is een open-source gedistribueerd versiebeheersysteem. Hallo-voorbeeldtoepassing voor deze les wordt opgeslagen op Git.
  - Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
- Hoe toouse NPM tooinstall Node.js ontwikkelingsprogramma's.
  - Hallo minimaal vereiste versie van Node.js is 4.5 TNS.
  - NPM is een van de Hallo pakket managers voor Node.js.
- Hoe tooinstall Visual Studio Code.
  - Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.
- Hoe tooinstall hello Azure CLI
  - Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanaf een opdrachtregel tooprovision en beheren van resources.
- Hoe toouse hello Azure CLI toocreate een IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een Internet verbinding toodownload Hallo hulpprogramma's en software.
- Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

tooinstall Git- en Node.js, volg deze stappen:

1. Druk op `Ctrl + Alt + T` tooopen een terminal.
2. Voer Hallo volgende opdrachten:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.

tooinstall gulp uitvoeren van de volgende opdracht in de terminal Hallo Hallo:

```bash
sudo npm install -g gulp
```

Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor toocommon oplossingen voor problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren

tooinstall hello Azure CLI, als volgt te werk:

1. Voer Hallo opdrachten in de terminal hello te volgen:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   Hallo-installatie kan 5 minuten duren.

2. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot -h
   ```
U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.
![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Visual Studio Code installeren

Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.

[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op de hostcomputer. Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
