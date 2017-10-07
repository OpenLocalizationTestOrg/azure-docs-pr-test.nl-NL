---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 2: Azure-hulpprogramma''s (Windows) | Microsoft Docs'
description: Python en hello Azure-opdrachtregelinterface (Azure CLI) installeren op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT cloud-service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Ophalen van de Azure-hulpprogramma's (Windows 7 en hoger)
> [!div class="op_single_selector"]
> * [Windows 7 en hoger](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet
Installeer Python en hello Azure-opdrachtregelinterface (Azure CLI). Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe tooinstall Python.
* Hoe tooinstall hello Azure CLI.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Windows-computer met een internetverbinding.
* Een actief Azure-abonnement. Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.

## <a name="install-python"></a>Installeren van Python
[Installeren van Python](https://www.python.org/downloads/) op uw Windows-computer. U kunt Python 2.7 3.4 of 3.5 installeren. Deze zelfstudie is gebaseerd op Python 2.7. Als u Python al hebt geïnstalleerd, gaat u de volgende sectie toohello en hello Azure CLI installeren.

U moet ook tooadd Hallo pad Hallo mappen waar systeem geïnstalleerde toohello python.exe en pip.exe zijn `PATH` omgevingsvariabele. Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren
Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.

tooinstall hello Azure CLI, als volgt te werk:

1. Open een opdrachtpromptvenster als administrator.
2. Voer Hallo volgende opdrachten:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot -h
   ```

Ziet u de volgende Hallo uitvoer als Hallo-installatie geslaagd is.

![Uitvoer die slagen aangeeft](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Samenvatting
U kunt hello Azure CLI hebt geïnstalleerd. Uw volgende taak toocreate uw Azure IoT hub- en apparaatidentiteiten met behulp van hello Azure CLI.

## <a name="next-steps"></a>Volgende stappen
[Het maken van uw IoT-hub en frambozen Pi 3 registreren](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

