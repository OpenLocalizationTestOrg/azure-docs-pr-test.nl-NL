---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Intel Edison configureren voor het eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding maken met arduino pc, setup arduino, arduino mededelingenbord
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a>Uw Edison Intel configureren
## <a name="what-you-will-do"></a>Wat u doet
Intel Edison configureren voor het eerste gebruik door de bestuur, het opstarten van montage en configuration tool installeren op uw bureaublad besturingssysteem naar flash Edison van firmware, stel het wachtwoord en verbinding met Wi-Fi. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Informatie over het samenstellen van Edison mededelingenbord en inschakelen van.
* Het flash Edison van firmware, wachtwoord instellen en Wi-Fi-verbinding.

## <a name="what-you-need"></a>Wat u nodig hebt
Om deze bewerking niet voltooien, moet u de volgende onderdelen met de Intel Edison Starter Kit:

* Intel® Edison-module
* Arduino uitbreiding mededelingenbord
* Een tussenruimte balken of schroeven opgenomen in de verpakking, met inbegrip van twee schroeven om de module aan de bestuur uitbreiding en vier sets schroeven en plastic spacers bevestigen.
* Een B Micro van Type A USB-kabel
* Een voeding direct huidige (DC). Het prioriteitsniveau van uw voeding moet als volgt:
  - 7 15V DC
  - Ten minste 1500mA
  - De pincode center/interne moet de positieve pool van de voeding

  ![Dingen in uw starterskit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

U hebt ook het volgende nodig:

* Een computer met Windows, Mac of Linux.
* Een draadloze verbinding voor Edison verbinding maken met.
* Een internetverbinding beschikken om het downloaden van hulpprogramma voor serverconfiguratie.

## <a name="assemble-your-board"></a>Het mededelingenbord samenstellen

Deze sectie bevat stappen om uw module Intel® Edison koppelen aan het mededelingenbord uitbreiding.

1. Plaats de Intel® Edison module binnen het wit overzicht op het mededelingenbord uitbreiding uitgelijnd in de gaten in de module met de schroeven op het mededelingenbord van de uitbreiding.

2. Druk op de module onder de woorden `What will you make?` totdat u denkt een module dat.

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. De twee hexadecimale nuts (opgenomen in het pakket) gebruiken voor het beveiligen van de module in op het mededelingenbord van de uitbreiding.

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Voeg een installatie in een van de vier hoek gaten op het mededelingenbord van de uitbreiding. Draai en dat een van de witte plastic spacers op de installatie wordt versterkt.

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Herhaal voor de andere drie hoek spacers.

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Nu is het mededelingenbord samengesteld.

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Geef Edison

1. Sluit de voeding.

   ![Plug-in-voeding](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Een groene LED (met de naam DS1 op het mededelingenbord Arduino * uitbreiding) moet branden en blijf branden.

3. Wacht een minuut voor de kaart te voltooien wordt opgestart.

   > [!NOTE]
   > Als u een DC-voeding niet hebt, kunt u nog steeds het mededelingenbord via een USB-poort voor energiebeheer. Zie `Connect Edison to your computer` sectie voor meer informatie. Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.

## <a name="connect-edison-to-your-computer"></a>Edison aansluiten op uw computer

1. Schakelen naar beneden de microswitch naar de twee micro USB-poorten, zodat Edison in de apparaatmodus. Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Uitschakelen van de microswitch](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. De micro USB-kabel aansluiten op de bovenste micro USB-poort.

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Het andere einde van USB-kabel aansluiten op uw computer.

   ![Computer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).

## <a name="download-and-run-the-configuration-tool"></a>Downloaden en uitvoeren van het configuratiehulpprogramma
Ophalen van de nieuwste hulpprogramma voor serverconfiguratie van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld in de `Installers` kop. Het hulpprogramma uitvoeren en volg de aanwijzingen op het scherm instructies en klik vervolgens op waar nodig

### <a name="flash-firmware"></a>Flash-firmware
1. Op de `Set up options` pagina, klikt u op `Flash Firmware`.
2. Selecteer de installatiekopie moet op het mededelingenbord flash op een van de volgende manieren:
   - Als u wilt downloaden en het mededelingenbord met de meest recente firmware-installatiekopie beschikbaar van Intel flash, selecteer `Download the latest image version xxxx`.
   - Selecteer Flash het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, `Select the local image`. Blader naar en selecteer de installatiekopie die u wilt flash op het mededelingenbord.
3. Het hulpprogramma setup probeert te flash het mededelingenbord. Het hele knipperende proces kan maximaal 10 minuten duren.

### <a name="set-password"></a>Wachtwoord instellen
1. Op de `Set up options` pagina, klikt u op `Enable Security`.
2. U kunt een aangepaste naam voor uw kaart Intel® Edison instellen. Dit is optioneel.
3. Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.
4. Markeert u het wachtwoord dat later wordt gebruikt.

### <a name="connect-wi-fi"></a>Wi-Fi-verbinding
1. Op de `Set up options` pagina, klikt u op `Connect Wi-Fi`. Wacht maximaal één minuut als uw computer wordt gescand naar beschikbare Wi-Fi-netwerken.
2. Van de `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.
3. Van de `Security` vervolgkeuzelijst Selecteer beveiligingstype van het netwerk.
4. Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.
5. Markeer de IP-adres, die later wordt gebruikt.

> [!NOTE]
> Zorg ervoor dat Edison is verbonden met hetzelfde netwerk bevindt als uw computer. Uw computer verbinding maakt met uw Edison met behulp van het IP-adres.

Gefeliciteerd. U hebt Edison geconfigureerd.

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd hoe het mededelingenbord Edison samenstellen, flash de firmware, setup wachtwoord en verbinding met Wi-Fi met behulp van hulpprogramma voor serverconfiguratie. Houd er rekening mee dat de LED nog niet branden. De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op Edison.

## <a name="next-steps"></a>Volgende stappen
[Download de hulpprogramma 's][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md