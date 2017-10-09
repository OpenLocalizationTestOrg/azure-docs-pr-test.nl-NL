---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Frambozen Pi 3 configureren voor gebruik van de eerste keer en Hallo Raspbian OS een gratis besturingssysteem dat is geoptimaliseerd voor Hallo frambozen Pi hardware installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: installatie raspbian, raspbian downloaden waarop tooinstall raspbian, raspbian setup raspberry pi installeren raspbian raspberry pi installeren os raspberry pi sd-kaart installeren, raspberry pi verbinding maken, verbinding tooraspberry pi raspberry pi connectiviteit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Uw apparaat configureren
## <a name="what-you-will-do"></a>Wat u doet
Pi configureren voor gebruik van de eerste keer en Hallo Raspbian besturingssysteem installeren. Raspbian is een gratis besturingssysteem die is geoptimaliseerd voor Hallo frambozen Pi hardware. Als u problemen hebt, kunt u proberen oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooinstall Raspbian met Pi.
* Hoe toopower up Pi via een USB-kabel.
* Hoe tooconnect Pi toohello netwerk met behulp van een Ethernet-kabel of draadloze netwerk.
* Hoe een LED toohello tooadd breadboard en verbind deze tooPi.

## <a name="what-you-will-need"></a>Wat u nodig hebt
toocomplete deze bewerking moet u volgende onderdelen van uw frambozen Pi 3 Starter Kit Hallo:

* Hallo frambozen Pi 3 mededelingenbord
* Hallo 16 GB microSD-kaart
* Hallo 5 v 2 amp voeding met Hallo 6 mond micro USB-kabel
* Hallo breadboard
* Connector-kabels
* Een weerstand 560 ohm
* Een gedempt 10 mm LED
* Hallo Ethernet-kabel

![Dingen in uw starterskit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

U hebt ook het volgende nodig:

* Een bekabelde of draadloze verbinding voor Pi tooconnect aan.
* Een USB-SD adapter of miniSD kaart tooburn Hallo besturingssysteeminstallatiekopie op Hallo microSD-kaart.
* Een computer met Windows, Mac of Linux. Hallo-computer is gebruikte tooinstall Raspbian op Hallo microSD-kaart.
* Een Internet verbinding toodownload Hallo benodigde hulpprogramma's en software.

## <a name="install-raspbian-on-hello-microsd-card"></a>Raspbian installeren op Hallo microSD-kaart
Hallo microSD-kaart voor de installatie van Hallo Raspbian afbeelding voorbereiden.

1. Raspbian downloaden.
   1. [Download](https://www.raspberrypi.org/downloads/raspbian/) Hallo ZIP-bestand voor Raspbian Jessie met Pixel.
   2. Pak Hallo Raspbian installatiekopie tooa map op uw computer.
2. Installeer Raspbian toohello microSD-kaart.
   1. [Download](https://www.etcher.io) en Hallo Etcher SD-kaart brander hulpprogramma installeren.
   2. Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.
   3. Selecteer Hallo microSD-kaart station.
      Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.
   4. Klik op **Flash** tooinstall Raspbian toohello microSD-kaart.
   5. Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is.
      Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.
   6. Hallo microSD-kaart invoegen in Pi.

![Plaats Hallo SD-kaart](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Pi inschakelen
Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding.

![Inschakelen](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Het is belangrijk toouse Hallo voeding in Hallo kit ten minste 2A toomake ervoor dat uw frambozen voldoende toowork power correct heeft.

## <a name="enable-ssh"></a>SSH inschakelen
Vanaf de release van November 2016 Hallo heeft Raspbian Hallo SSH-server is standaard uitgeschakeld. U moet tooenable deze handmatig. U kunt verwijzen toohello [officiële instructies](https://www.raspberrypi.org/documentation/remote-access/ssh/) of verbinding maken met een monitor en gaat u te**voorkeuren-frambozen Pi Configuration >** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Frambozen Pi 3 toohello netwerk verbinden
U kunt Pi tooa bekabeld netwerk of tooa draadloze netwerk verbinding maken. Zorg ervoor dat Pi verbonden toohello netwerk als de computer is. U kunt bijvoorbeeld Pi toohello die dezelfde switch dat uw computer is verbonden met verbinden.

### <a name="connect-tooa-wired-network"></a>Verbinding maken met tooa bekabelde netwerk
Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk. Hallo inschakelen twee LED's op Pi als Hallo-verbinding tot stand is gebracht.

![Verbinding maken met behulp van een Ethernet-kabel](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Verbinding maken met het draadloze netwerk tooa
Ga als volgt Hallo [instructies](https://www.raspberrypi.org/learning/software-guide/wifi/) van Hallo frambozen Pi Foundation tooconnect Pi tooyour draadloos netwerk. Deze instructies, moet u toofirst verbinding maken met een monitor en een toetsenbord tooPi.

## <a name="connect-hello-led-toopi"></a>Hallo LED tooPi verbinding
toocomplete deze taak, gebruik Hallo [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), connector kabels Hallo Hallo LED en Hallo weerstand. Verbind ze toohello [voor algemene doeleinden input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO)-poorten van Pi.

![Breadboard LED en weerstand](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Hallo korter arm van Hallo LED te verbinden**GPIO GND (pincode 6)**.
2. Verbinding maken met Hallo langer arm van Hallo LED tooone arm van Hallo weerstand.
3. Verbinding maken met andere arm van Hallo weerstand te Hallo**GPIO 4 (7 pincode)**.

Houd er rekening mee dat Hallo LED polariteit belangrijk is. Deze instelling polariteit staat bekend als actief laag.

![Pin-out](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Gefeliciteerd. U hebt geconfigureerd Pi.

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd hoe tooconfigure door Raspbian, verbindende Pi tooa netwerk, installeren en verbinding maken met een tooPi LED Pi. Houd er rekening mee dat Hallo die LED nog niet branden. de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeldtoepassing met Pi.

![Hardware is gereed](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Volgende stappen
[Hallo-hulpprogramma's ophalen](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

