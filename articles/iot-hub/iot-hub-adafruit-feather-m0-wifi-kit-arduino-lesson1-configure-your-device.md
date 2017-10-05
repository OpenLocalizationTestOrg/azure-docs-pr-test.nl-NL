---
title: 'Connect Arduino (C) naar Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Configureer Adafruit Doezelaar M0 Wi-Fi voor eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding maken met arduino pc, setup arduino, arduino mededelingenbord
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Uw apparaat configureren
## <a name="what-you-will-do"></a>Wat u doet
Het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino voor eerste gebruik door de bestuur, het opstarten van samen te configureren. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Wat u nodig hebt
Om deze bewerking niet voltooien, moet u de volgende onderdelen voor uw Adafruit Doezelaar M0 Wi-Fi Starter Kit:

* De Adafruit Doezelaar M0 Wi-Fi-kaart
* Een B Micro van Type A USB-kabel

![Kit][kit]

U hebt ook het volgende nodig:

* Een computer met Windows, Mac of Linux.
* Een draadloze verbinding voor uw kaart Arduino verbinding maken met.
* Een internetverbinding beschikken om het downloaden van hulpprogramma voor serverconfiguratie.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Informatie over het samenstellen van het mededelingenbord Arduino en inschakelen voor de volgende uitkomsten.
* Het toevoegen van de seriële poort machtigingen op Ubuntu.

## <a name="connect-your-arduino-board-to-your-computer"></a>Het mededelingenbord Arduino aansluiten op uw computer

1. De micro USB-kabel aansluiten op de bovenste micro USB-poort.

   ![Bovenste micro USB-poort][top-micro-usb-port]

2. Het andere einde van USB-kabel aansluiten op uw computer.

   ![Computer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Machtigingen van de seriële poort toevoegen aan Ubuntu

Als u Windows of Mac OS gebruikt, kunt u deze sectie overslaan. Ubuntu moet u de volgende stappen uit om ervoor te zorgen dat de gebruiker normaal linux de machtigingen heeft voor de USB-poort van het mededelingenbord Arduino niet bewerken.

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

   De '0' mogelijk een ander nummer of meerdere items kunnen worden geretourneerd. In het eerste geval de gegevens die we nodig is `uucp`, wordt in de tweede `dialout`, dit is de eigenaar van de groep van het bestand.

2. Gebruiker toevoegen aan de aan de groep:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Waar `group-name` zijn de gegevens gevonden in de eerste stap en `username` uw linux-gebruikersnaam.

3. U moet zich aanmelden en opnieuw om deze wijziging van kracht en voltooit de installatie.

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd hoe het mededelingenbord Arduino configureren. De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op het mededelingenbord Arduino.

![Hardware is gereed][hardware-is-ready]

## <a name="next-steps"></a>Volgende stappen
[Download de hulpprogramma 's][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md