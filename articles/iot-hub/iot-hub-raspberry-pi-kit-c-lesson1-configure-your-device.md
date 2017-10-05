---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Frambozen Pi 3 configureren voor gebruik van de eerste en het besturingssysteem Raspbian, een gratis besturingssysteem dat is geoptimaliseerd voor de hardware frambozen Pi installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: installatie raspbian, raspbian downloaden waarop voor het installeren van raspbian, raspbian setup, raspberry pi installeren raspbian, raspberry pi installeren os, raspberry pi sd-kaart installeren, frambozen pi verbinding maken, verbinding maken met raspberry pi raspberry pi connectiviteit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Uw apparaat configureren
## <a name="what-you-will-do"></a>Wat u doet
Pi configureren voor het eerste gebruik en het besturingssysteem Raspbian installeren. Raspbian is een gratis besturingssysteem die is geoptimaliseerd voor de hardware frambozen Pi. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Het installeren van Raspbian op Pi.
* Klik hier voor meer informatie over het opstarten van Pi via een USB-kabel.
* Klik hier voor meer informatie over het Pi verbinding met het netwerk met behulp van een Ethernet-kabel of draadloze netwerk.
* Hoe een LED toevoegen aan de breadboard en te verbinden met Pi.

## <a name="what-you-need"></a>Wat u nodig hebt
Om deze bewerking niet voltooien, moet u de volgende onderdelen van uw frambozen Pi 3 Starter Kit:

* De kaart frambozen Pi 3
* De 16 GB microSD-kaart
* De 5-v 2 amp power supply met 6 mond micro USB-kabel
* De breadboard
* Connector-kabels
* Een weerstand 560 ohm
* Een gedempt 10 mm LED
* De Ethernet-kabel

![Dingen in uw starterskit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

U hebt ook het volgende nodig:

* Een bekabelde of draadloze verbinding voor Pi verbinding maken met.
* Een USB-SD adapter of mini-SD-kaart zet de OS-installatiekopie op de microSD-kaart.
* Een computer met Windows, Mac of Linux. De computer wordt gebruikt voor het installeren van Raspbian op de microSD-kaart.
* Een internetverbinding beschikken om het downloaden van de benodigde hulpprogramma's en software.

## <a name="install-raspbian-on-the-microsd-card"></a>Raspbian installeren op de MicroSD-kaart
Bereid de microSD-kaart voor de installatie van de installatiekopie van het Raspbian.

1. Raspbian downloaden.
   1. [Download](https://www.raspberrypi.org/downloads/raspbian/) het ZIP-bestand voor Raspbian Jessie met Pixel.
   2. Pak de installatiekopie van het Raspbian naar een map op uw computer.
2. Installeer Raspbian naar de microSD-kaart.
   1. [Download](https://www.etcher.io) en installeer het hulpprogramma Etcher SD-kaart brander.
   2. Voer Etcher en selecteer de installatiekopie van het Raspbian die u hebt opgehaald in stap 1.
   3. Selecteer het station microSD-kaart.
      Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd de juiste station.
   4. Klik op **Flash** Raspbian installeren op de microSD-kaart.
   5. Verwijder de microSD-kaart van uw computer wanneer de installatie voltooid is.
      Het is veilig worden verwijderd, de microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of ontkoppelt de microSD-kaart is voltooid.
   6. De microSD-kaart invoegen in uw Pi.

![Invoegen van de SD-kaart](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Pi inschakelen
Pi inschakelen met behulp van het micro USB-kabel en de voeding.

![Inschakelen](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Het is belangrijk dat u de voeding in de kit ten minste 2A om ervoor te zorgen dat uw frambozen heeft onvoldoende stroom correct te laten werken.

## <a name="enable-ssh"></a>SSH inschakelen
Vanaf de release van November 2016 heeft Raspbian de SSH-server standaard uitgeschakeld. U moet handmatig inschakelen. U kunt verwijzen naar de [officiële instructies](https://www.raspberrypi.org/documentation/remote-access/ssh/) of verbinding maken met een monitor en Ga naar **Voorkeuren -> frambozen Pi configuratie** SSH inschakelen.

## <a name="connect-raspberry-pi-3-to-the-network"></a>Frambozen Pi 3 verbinding met het netwerk
U kunt Pi verbinding maken met een bekabeld netwerk of een draadloos netwerk. Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer. U kunt bijvoorbeeld Pi verbinden met dezelfde switch waarmee uw computer is verbonden.

### <a name="connect-to-a-wired-network"></a>Verbinding maken met een bekabeld netwerk
Via het Ethernet-kabel Pi verbinden met het bekabelde netwerk. De twee LED's met Pi inschakelen als de verbinding tot stand is gebracht.

![Verbinding maken met behulp van een Ethernet-kabel](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a>Verbinding maken met een draadloos netwerk
Ga als volgt de [instructies](https://www.raspberrypi.org/learning/software-guide/wifi/) van de Stichting frambozen Pi Pi verbinding met uw draadloze netwerk. Deze instructies, moet u eerst een verbinding tussen een monitor en een toetsenbord tot Pi.

## <a name="connect-the-led-to-pi"></a>Verbinding maken met de LED Pi
Gebruik voor het voltooien van deze taak de [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), de kabels connector, de LED en de weerstand. Verbind ze naar de [voor algemene doeleinden input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO)-poorten van Pi.

![Breadboard LED en weerstand](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Verbinding maken met de kortere zijde van de LED naar **GPIO GND (pincode 6)**.
2. Verbinding maken met de langer zijde van de LED één arm van de weerstand.
3. Verbinding maken met de andere zijde van de weerstand naar **GPIO 4 (7 pincode)**.

Houd er rekening mee dat de polariteit LED belangrijk is. Deze instelling polariteit staat bekend als actief laag.

![Pin-out](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Gefeliciteerd. U hebt geconfigureerd Pi.

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd hoe Pi configureren met Raspbian installeren en verbinding maken met een LED Pi Pi verbinden met een netwerk. Houd er rekening mee dat de LED nog niet branden. De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeldtoepassing met Pi.

![Hardware is gereed](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Volgende stappen
[Download de hulpprogramma 's](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

