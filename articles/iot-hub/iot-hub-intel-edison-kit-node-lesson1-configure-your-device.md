---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Intel Edison configureren voor het eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding arduino toopc, setup arduino, arduino mededelingenbord
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
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Uw Edison Intel configureren
## <a name="what-you-will-do"></a>Wat u doet
Intel Edison configureren voor gebruik van de eerste keer door montage Hallo mededelingenbord, het opstarten van en configuratie hulpprogramma tooyour bureaublad OS tooflash installeren van Edison firmware, instellen van het wachtwoord in en sluit het tooWi-Fi. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe tooassemble Edison board en inschakelen van.
* Hoe tooflash Edison van firmware, wachtwoord instellen en Wi-Fi-verbinding.

## <a name="what-you-need"></a>Wat u nodig hebt
toocomplete deze bewerking moet u volgende onderdelen met de Intel Edison Starter Kit Hallo:

* Intel® Edison-module
* Arduino uitbreiding mededelingenbord
* Een tussenruimte balken of schroeven in Hallo verpakking, met inbegrip van twee schroeven toofasten Hallo module toohello uitbreiding mededelingenbord en vier sets schroeven en plastic spacers meegeleverd.
* Een tooType Micro B een USB-kabel
* Een voeding direct huidige (DC). Het prioriteitsniveau van uw voeding moet als volgt:
  - 7 15V DC
  - Ten minste 1500mA
  - Hallo center/interne pincode moet Hallo positieve pool van Hallo-voeding

  ![Dingen in uw starterskit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

U hebt ook het volgende nodig:

* Een computer met Windows, Mac of Linux.
* Een draadloze verbinding voor Edison tooconnect aan.
* Een Internet verbinding toodownload configuratiehulpprogramma.

## <a name="assemble-your-board"></a>Het mededelingenbord samenstellen

Deze sectie bevat stappen tooattach het mededelingenbord Intel® Edison module tooyour uitbreiding.

1. Hallo Intel® Edison module binnen Hallo wit overzicht op het mededelingenbord uitbreiding, Hallo gaten op Hallo-module met Hallo schroeven op Hallo uitbreiding mededelingenbord uitgelijnd plaatsen.

2. Druk op Hallo module onder Hallo woorden `What will you make?` totdat u denkt een module dat.

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Hallo twee hexadecimale nuts (opgenomen in het Hallo-pakket) toosecure Hallo module toohello uitbreiding mededelingenbord gebruiken.

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Een installatie in een van de vier hoek gaten op Hallo uitbreiding mededelingenbord Hallo invoegen. Draai en dat een witte Hallo plastic spacers op Hallo-installatie wordt versterkt.

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Herhaal dit voor Hallo andere spacers drie hoek.

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Nu is het mededelingenbord samengesteld.

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Geef Edison

1. Hallo-voeding sluit.

   ![Plug-in-voeding](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Een groene LED (met de naam DS1 op Hallo Arduino * uitbreiding mededelingenbord) moet branden en blijf branden.

3. Wacht een minuut voor Hallo mededelingenbord toofinish-up wordt opgestart.

   > [!NOTE]
   > Als u een DC-voeding niet hebt, kunt u nog steeds power Hallo mededelingenbord via een USB-poort. Zie `Connect Edison tooyour computer` sectie voor meer informatie. Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.

## <a name="connect-edison-tooyour-computer"></a>Verbind Edison tooyour computer

1. Schakelen naar beneden Hallo microswitch naar Hallo twee micro USB-poorten, zodat Edison in de apparaatmodus. Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Omlaag Hallo microswitch in-of uitschakelen](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug Hallo andere einde van USB-kabel op uw computer.

   ![Computer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).

## <a name="download-and-run-hello-configuration-tool"></a>Downloaden en uitvoeren van hulpprogramma voor serverconfiguratie Hallo
Ophalen van de nieuwste configuratiehulpprogramma Hallo van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld onder Hallo `Installers` kop. Hallo-hulpprogramma uitvoeren en volg de op het scherm te klikken naast waar nodig-instructies

### <a name="flash-firmware"></a>Flash-firmware
1. Op Hallo `Set up options` pagina, klikt u op `Flash Firmware`.
2. Selecteer Hallo installatiekopie tooflash op het mededelingenbord op een van de volgende Hallo manieren:
   - toodownload en flash het mededelingenbord met Hallo meest recente firmware installatiekopie beschikbaar van Intel, selecteer `Download hello latest image version xxxx`.
   - het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, selecteert u tooflash `Select hello local image`. Tooand Selecteer Hallo afbeelding u tooflash tooyour mededelingenbord wilt doorzoeken.
3. hulpprogramma voor Hallo setup probeert tooflash het mededelingenbord. Hallo hele knipperende proces kan too10 minuten duren.

### <a name="set-password"></a>Wachtwoord instellen
1. Op Hallo `Set up options` pagina, klikt u op `Enable Security`.
2. U kunt een aangepaste naam voor uw kaart Intel® Edison instellen. Dit is optioneel.
3. Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.
4. Markeer omlaag Hallo-wachtwoord wordt later gebruikt.

### <a name="connect-wi-fi"></a>Wi-Fi-verbinding
1. Op Hallo `Set up options` pagina, klikt u op `Connect Wi-Fi`. Wacht up tooone minuut als uw computer scans voor Wi-Fi-netwerken beschikbaar.
2. Van Hallo `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.
3. Van Hallo `Security` vervolgkeuzelijst, selecteer Hallo-netwerk beveiligingstype.
4. Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.
5. Markeer omlaag Hallo IP-adres, wordt later gebruikt.

> [!NOTE]
> Zorg ervoor dat Edison verbonden toohello netwerk als de computer is. Uw computer verbinding maakt tooyour Edison met Hallo IP-adres.

Gefeliciteerd. U hebt Edison geconfigureerd.

## <a name="summary"></a>Samenvatting
In dit artikel hebt geleerd hoe tooassemble Edison mededelingenbord Hallo, flash de firmware, setup wachtwoord en verbindt u deze tooWi-Fi met behulp van hulpprogramma voor serverconfiguratie. Houd er rekening mee dat Hallo die LED nog niet branden. de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op Edison.

## <a name="next-steps"></a>Volgende stappen
[Hallo-hulpprogramma's ophalen][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md