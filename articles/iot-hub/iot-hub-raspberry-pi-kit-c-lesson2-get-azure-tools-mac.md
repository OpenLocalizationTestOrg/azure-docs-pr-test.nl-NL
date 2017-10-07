---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 2: Azure-hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) installeren op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT cloud-service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Azure-hulpprogramma's (Mac OS 10.10) ophalen
> [!div class="op_single_selector"]
> * [Windows 7 en hoger](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [Mac OS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Wat u doet
Hello Azure-opdrachtregelinterface (Azure CLI) installeren. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe tooinstall Azure CLI.
* Hoe tooadd een subgroep IoT Hallo Azure CLI.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Mac met een internetverbinding.
* Een actief Azure-abonnement. Als u geen Azure-account hebt, kunt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.

## <a name="install-python"></a>Installeren van Python
Hoewel Mac OS wordt geleverd met Python 2.7 out of box hello, raden wij aan dat u Python via Homebrew installeert. Zie [Python installeren op Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python en pip door het uitvoeren van de volgende opdracht Hallo installeren:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren
Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure. U werkt rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources. 

tooinstall Hallo nieuwste Azure CLI, als volgt te werk:

1. Hallo volgende opdrachten in een terminalvenster worden uitgevoerd. Vijf minuten tooinstall hello Azure CLI kan duren.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot -h
   ```

U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.

![Uitvoer die slagen aangeeft](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Samenvatting
U kunt hello Azure CLI hebt geïnstalleerd. Het is uw volgende taak toocreate uw Azure IoT hub- en apparaatidentiteiten met behulp van hello Azure CLI.

## <a name="next-steps"></a>Volgende stappen
[Het maken van uw IoT-hub en frambozen Pi 3 registreren](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

