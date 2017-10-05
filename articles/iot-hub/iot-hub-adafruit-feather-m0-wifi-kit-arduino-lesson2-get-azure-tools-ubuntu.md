---
title: 'Arduino verbinden met Azure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) op Ubuntu installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)

> [!div class="op_single_selector"]
> * [Windows 7 of hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet

Installeer de Azure-opdrachtregelinterface (Azure CLI). Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Klik hier voor meer informatie over het installeren van de Azure CLI.
* Het toevoegen van een IoT-subgroep van de Azure CLI.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een virtuele Ubuntu-computer met een internetverbinding.
* Een actief Azure-abonnement. Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.

## <a name="install-the-azure-cli"></a>Azure-CLI installeren
De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure, zodat u kunt werken rechtstreeks vanaf de opdrachtregel voor het inrichten en beheren van resources.

Volg deze stappen voor het installeren van de nieuwste Azure CLI:

1. Voer de volgende opdrachten in een terminalvenster. Het duurt vijf minuten voor het installeren van de Azure CLI.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. De installatie controleren door de volgende opdracht uit te voeren:

   ```bash
   az iot -h
   ```

U ziet de volgende uitvoer als de installatie geslaagd is.

![Uitvoer die slagen aangeeft][output]

## <a name="summary"></a>Samenvatting
U kunt de Azure CLI hebt geïnstalleerd. Uw volgende taak is het maken van uw Azure IoT hub- en apparaatidentiteiten met de Azure CLI.

## <a name="next-steps"></a>Volgende stappen
[Het maken van uw IoT-hub en het mededelingenbord Arduino registreren][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md