---
title: 'Connect Intel Edison (C) tooAzure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) op Ubuntu installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a7691c13d43aa6dfff24adf2b470728d5266713e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)
> [!div class="op_single_selector"]
> * [Windows 7 en hoger][windows]
> * [Ubuntu 16.04][ubuntu]
> * [Mac OS 10.10][macos]

## <a name="what-you-will-do"></a>Wat u doet
Hello Azure-opdrachtregelinterface (Azure CLI) installeren. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe tooinstall hello Azure CLI.
* Hoe tooadd een subgroep IoT Hallo Azure CLI.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een virtuele Ubuntu-computer met een internetverbinding.
* Een actief Azure-abonnement. Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI installeren
Hello Azure CLI biedt meerdere platforms opdrachtregelprogramma voor Azure, zodat u toowork rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.

tooinstall Hallo nieuwste Azure CLI, als volgt te werk:

1. Hallo volgende opdrachten in een terminalvenster worden uitgevoerd. Vijf minuten tooinstall hello Azure CLI kan duren.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot -h
   ```

U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Samenvatting
U kunt hello Azure CLI hebt geïnstalleerd. Het is uw volgende taak toocreate uw Azure-IoT-hub en apparaten identiteit met hello Azure CLI.

## <a name="next-steps"></a>Volgende stappen
[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
