---
title: 'Arduino verbinden met Azure IoT - les 2: Azure-hulpprogramma''s (Windows) | Microsoft Docs'
description: Python en de Azure-opdrachtregelinterface (Azure CLI) installeren op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1f121d9f22f8a7c8582df4d2e62191cec364da46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Ophalen van de Azure-hulpprogramma's (Windows 7 en hoger)

> [!div class="op_single_selector"]
> * [Windows 7 of hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet

Python en de Azure-opdrachtregelinterface (Azure CLI) installeren. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Klik hier voor meer informatie over het installeren van Python.
* Klik hier voor meer informatie over het installeren van de Azure CLI.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Windows-computer met een internetverbinding.
* Een actief Azure-abonnement. Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.

## <a name="install-python"></a>Installeren van Python
[Installeren van Python](https://www.python.org/downloads/) op uw Windows-computer. U kunt Python 2.7 3.4 of 3.5 installeren. Deze zelfstudie is gebaseerd op Python 2.7. Als u Python al hebt geïnstalleerd, gaat u naar de volgende sectie en Azure CLI installeren.

Ook moet u het pad van de mappen waar python.exe en pip.exe zijn geïnstalleerd op het systeem toevoegen `PATH` omgevingsvariabele. Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Azure-CLI installeren
De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanaf de opdrachtregel inrichten en beheren van resources.

Volg deze stappen voor het installeren van de Azure CLI:

1. Open een opdrachtpromptvenster als administrator.
2. Voer de volgende opdrachten uit:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. De installatie controleren door de volgende opdracht uit te voeren:

   ```bash
   az iot -h
   ```

U ziet de volgende uitvoer als de installatie geslaagd is.

![Uitvoer die slagen aangeeft][output]

## <a name="summary"></a>Samenvatting
U kunt de Azure CLI hebt geïnstalleerd. Uw volgende taak voor het maken van uw Azure IoT hub- en apparaatidentiteiten met behulp van de Azure CLI.

## <a name="next-steps"></a>Volgende stappen
[Het maken van uw IoT-hub en het mededelingenbord Arduino registreren][create-your-iot-hub-and-register-your-arduino-board]


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md