---
title: 'Connect Arduino (C) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Configureer Adafruit Doezelaar M0 Wi-Fi voor eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding arduino toopc, setup arduino, arduino mededelingenbord
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Uw apparaat configureren
## <a name="what-you-will-do"></a>Wat u doet
Configureren het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino voor eerste gebruik Hallo mededelingenbord, het opstarten van en samen te stellen. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Wat u nodig hebt
toocomplete deze bewerking moet u volgende onderdelen voor uw Adafruit Doezelaar M0 Wi-Fi Starter Kit Hallo:

* Hallo Adafruit Doezelaar M0 Wi-Fi mededelingenbord
* Een tooType Micro B een USB-kabel

![Kit][kit]

U hebt ook het volgende nodig:

* Een computer met Windows, Mac of Linux.
* Een draadloze verbinding voor uw Arduino mededelingenbord tooconnect aan.
* Een Internet verbinding toodownload configuratiehulpprogramma.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooassemble Arduino mededelingenbord- en stroomkabels lessen deze voor hello te volgen.
* Hoe tooadd seriële poort machtigingen op Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Verbinding maken met uw computer Arduino mededelingenbord tooyour

1. Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.

   ![Bovenste micro USB-poort][top-micro-usb-port]

2. Plug Hallo andere einde van USB-kabel op uw computer.

   ![Computer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Machtigingen van de seriële poort toevoegen aan Ubuntu

Als u Windows of Mac OS gebruikt, kunt u deze sectie overslaan. Ubuntu moet u Hallo stappen toomake ervoor Hallo normale linux gebruiker heeft Hallo machtigingen toooperate op Hallo USB-poort van het mededelingenbord Arduino te volgen.

1. Nu als normale gebruiker in de terminal:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   U ontvangt ongeveer als volgt:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Hallo '0' mogelijk een ander nummer of meerdere items kunnen worden geretourneerd. Hallo eerste case Hallo gegevens die we nodig is `uucp`, in Hallo is het tweede `dialout`, dit is de Groepseigenaar Hallo van Hallo-bestand.

2. Gebruikersgroep toohello toohello toevoegen:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Waar `group-name` Hallo-gegevens gevonden in de eerste stap Hallo en `username` uw linux-gebruikersnaam.

3. U moet toolog out en in opnieuw voor deze wijziging tootake effect en volledige Hallo setup.

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd hoe tooconfigure het mededelingenbord Arduino. de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op het mededelingenbord Arduino.

![Hardware is gereed][hardware-is-ready]

## <a name="next-steps"></a>Volgende stappen
[Hallo-hulpprogramma's ophalen][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md