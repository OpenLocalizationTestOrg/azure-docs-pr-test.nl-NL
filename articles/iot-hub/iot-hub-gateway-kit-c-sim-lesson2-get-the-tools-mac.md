---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Hulpprogramma's installeren op uw Mac-computer, een iothub maken en uw apparaat registreren in de IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, install python mac, installeer git op mac gulp uitvoert, installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a>Download de hulpprogramma's (Mac OS)
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

- Het installeren van [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).
  - GIT is een open-source gedistribueerd versiebeheersysteem. De voorbeeldtoepassing voor deze les wordt opgeslagen op Git.
  - Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.
- Het gebruik van [NPM](https://www.npmjs.com/) Node.js ontwikkelingsprogramma's te installeren.
  - De minimaal vereiste versie van Node.js is 4.5 TNS.
  - NPM is een van de pakket-managers voor Node.js.
- Klik hier voor meer informatie over het installeren van Visual Studio Code.
  - Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS. Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.
- Klik hier voor meer informatie over het installeren van Python.
  - Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.
- Klik hier voor meer informatie over het installeren van de Azure CLI.
  - De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanaf een opdrachtregel inrichten en beheren van resources.
- Het gebruik van de Azure CLI voor het maken van een IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een internetverbinding beschikken om het downloaden van de hulpprogramma's en software.
- Een Mac-computer met OS X Yosemite (10.10) of hoger.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Wilt installeren Git en Node.js, gebruikt u het hulpprogramma voor het Homebrew pakket met de volgende stappen:

1. [Download](http://brew.sh/) en Homebrew installeren. Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.
   1. Druk op `Cmd + Space` en voer `Terminal` een terminal openen.
   2. Voer de volgende opdracht uit:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Git en Node.js installeren met de volgende opdracht:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.

Als u wilt installeren gulp, voer de volgende opdracht in de terminal:

```bash
npm install -g gulp
```

Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-python"></a>Installeren van Python

Hoewel Mac OS X wordt geleverd met Python 2.7, raden we u Python via Homebrew te installeren. Zie [Python installeren op Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python en pip installeren met de volgende opdracht:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Azure-CLI installeren

Volg deze stappen voor het installeren van de Azure CLI:

1. Voer de volgende opdrachten in de terminal:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   De installatie kan 5 minuten duren.

2. De installatie controleren door de volgende opdracht uit te voeren:
   ```bash
   az iot -h
   ```
   U ziet de volgende uitvoer als de installatie geslaagd is.

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.

[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U hebt de vereiste hulpprogramma's en software op uw Mac-computer geïnstalleerd. Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een iothub maken en registreren van apparaat](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
