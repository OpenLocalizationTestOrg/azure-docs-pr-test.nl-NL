---
title: 'SensorTag apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Windows) | Microsoft Docs'
description: Hallo-hulpprogramma's en Hallo software installeren op de hostcomputer waarop Windows wordt uitgevoerd, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git voor windows, gulp uitvoeren, knooppunt js windows installeren, npm in windows te installeren, python op windows installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Ophalen van Hallo hulpprogramma's (Windows 7 en hoger)
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
- Een Windows-computer.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Klik op Hallo toodownload koppelingen volgen en Git en Node.js LTS voor Windows installeren.

- [Ophalen van Git voor Windows](https://git-scm.com/download/win/)
- [Node.js TNS ophalen voor Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.

Druk op `Windows + R`, type `cmd` en druk op `Enter` tooopen een opdrachtpromptvenster, en vervolgens uitvoeren Hallo opdracht:

```cmd
npm install -g gulp
```

Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-python"></a>Installeren van Python

U kunt kiezen uit Python 2.7 3.4 of 3.5. In deze zelfstudie gebruiken we Python 2.7. Als u python al hebt geïnstalleerd, gaat u de volgende sectie toohello.

[Python ophalen voor Windows](https://www.python.org/downloads/)

U moet ook tooadd Hallo pad Hallo mappen waar systeem geïnstalleerde toohello Python.exe en pip.exe zijn `PATH` omgevingsvariabele. Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren

tooinstall hello Azure CLI, als volgt te werk:

1. Open een opdrachtpromptvenster als administrator.

2. Hello Azure CLI installeren door het uitvoeren van de volgende opdrachten Hallo:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Hallo-installatie kan 5 minuten duren.

3. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:

   ```cmd
   az iot -h
   ```

   U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.

[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op de hostcomputer. Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-lesson2-register-device.md)
