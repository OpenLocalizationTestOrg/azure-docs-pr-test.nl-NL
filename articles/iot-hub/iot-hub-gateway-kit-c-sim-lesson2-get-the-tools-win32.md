---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Windows) | Microsoft Docs'
description: De hulpprogramma's en de software installeren op de hostcomputer waarop Windows wordt uitgevoerd, een iothub maken en Registreer uw apparaat in de IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git voor windows, gulp uitvoeren, knooppunt js windows installeren, npm in windows te installeren, python op windows installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a>Download de hulpprogramma's (Windows 7 en hoger)
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
- Een Windows-computer.

## <a name="install-git-and-nodejs"></a>Installeer Git en Node.js

Klik op de volgende koppelingen wilt downloaden en installeren van Git en Node.js LTS voor Windows.

- [Ophalen van Git voor Windows](https://git-scm.com/download/win/)
- [Node.js TNS ophalen voor Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Node.js ontwikkelingsprogramma's installeren

U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.

Druk op `Windows + R`, type `cmd` en druk op `Enter` open een opdrachtpromptvenster en voer de volgende opdracht:

```cmd
npm install -g gulp
```

Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.

> [!Note]
> Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.

## <a name="install-python"></a>Installeren van Python

U kunt kiezen uit Python 2.7 3.4 of 3.5. In deze zelfstudie gebruiken we Python 2.7. Als u python al hebt geïnstalleerd, gaat u naar de volgende sectie.

[Python ophalen voor Windows](https://www.python.org/downloads/)

Ook moet u het pad van de mappen waar Python.exe en pip.exe zijn geïnstalleerd op het systeem toevoegen `PATH` omgevingsvariabele. Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Azure-CLI installeren

Volg deze stappen voor het installeren van de Azure CLI:

1. Open een opdrachtpromptvenster als administrator.

2. Azure CLI installeren met de volgende opdrachten:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   De installatie kan 5 minuten duren.

3. De installatie controleren door de volgende opdracht uit te voeren:

   ```cmd
   az iot -h
   ```

   U ziet de volgende uitvoer als de installatie geslaagd is.

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Visual Studio Code installeren

U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.

[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.

## <a name="summary"></a>Samenvatting

U hebt de vereiste hulpprogramma's en software op uw computer geïnstalleerd. Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
