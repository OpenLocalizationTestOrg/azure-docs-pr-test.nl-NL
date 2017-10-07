---
title: 'SensorTag apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Hulpprogramma's installeren op uw Mac-computer, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, install python mac, installeer git op mac gulp uitvoert, installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Hallo hulpprogramma's (Mac OS) ophalen
> [!div class="op_single_selector"]
> * [Windows 7 of hoger](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet

- Installeer Git, Node.js, Gulp, Python.
- Hello Azure-opdrachtregelinterface (Azure CLI) installeren. 

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe tooinstall [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).
  - GIT is een open-source gedistribueerd versiebeheersysteem. Hallo-voorbeeldtoepassing voor deze les wordt opgeslagen op Git.
  - Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
- Hoe toouse [NPM](https://www.npmjs.com/) tooinstall Node.js ontwikkelingsprogramma's.
  - Hallo minimaal vereiste versie van Node.js is 4.5 TNS.
  - NPM is een van de Hallo pakket managers voor Node.js.
- Hoe tooinstall Visual Studio Code.
  - Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.
- Hoe tooinstall Python.
  - Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.
- Hoe tooinstall hello Azure CLI.
  - Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanaf een opdrachtregel tooprovision en beheren van resources.
- Hoe toouse hello Azure CLI toocreate een IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een Internet verbinding toodownload Hallo hulpprogramma's en software.
- Een Mac-computer met OS X Yosemite (10.10) of hoger.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

tooinstall Git en Node.js, gebruikt hulpprogramma voor Hallo Homebrew pakket met de volgende stappen:

1. [Download](http://brew.sh/) en Homebrew installeren. Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.
   1. Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.
   2. Hallo volgende opdracht uitvoeren:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Installeer Git en Node.js Hallo na de opdracht uitgevoerd:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.

tooinstall gulp uitvoeren van de volgende opdracht in de terminal Hallo Hallo:

```bash
npm install -g gulp
```

Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-python"></a>Installeren van Python

Hoewel Mac OS X wordt geleverd met Python 2.7, raden we u Python via Homebrew te installeren. Zie [Python installeren op Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python en pip door het uitvoeren van de volgende opdracht Hallo installeren:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren

tooinstall hello Azure CLI, als volgt te werk:

1. Voer Hallo opdrachten in de terminal hello te volgen:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Hallo-installatie kan 5 minuten duren.

2. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:
   ```bash
   az iot -h
   ```
   U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.

[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op uw Mac-computer. Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een iothub maken en registreren van apparaat](iot-hub-gateway-kit-c-lesson2-register-device.md)
