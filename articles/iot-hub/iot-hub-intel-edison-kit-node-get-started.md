---
title: aaaIntel Edison toocloud (Node.js) - verbinding maken met Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met Intel Edison tooAzure IoT Hub voor Intel Edison toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel edison iothub, intel edison verzenden gegevens toocloud, intel edison toocloud
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a>Verbinding maken met Intel Edison tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met Intel Edison leren. U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

Heb je nog een kit? Start [hier](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Wat u doet

* Intel Edison instellen en en Groove modules.
* Een iothub maken.
* Een apparaat registreren voor Edison in uw IoT-hub.
* Een voorbeeld van een toepassing uitvoeren op Edison toosend sensor gegevens tooyour iothub.

Verbinding maken met een Intel Edison tooan IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op Edison toocollect temperatuur en vochtigheid gegevens uit een temperatuursensor Groove. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.

## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.
* Hoe tooconnect Edison met een temperatuursensor Groove.
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Edison.
* Hoe toosend sensor gegevens tooyour IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

![Wat u nodig hebt](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* Hallo Intel Edison mededelingenbord
* Arduino uitbreiding mededelingenbord
* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Een Mac of een PC die Windows of Linux wordt uitgevoerd.
* Een internetverbinding.
* Een tooType Micro B een USB-kabel
* Een voeding direct huidige (DC). Het prioriteitsniveau van uw voeding moet als volgt:
  - 7 15V DC
  - Ten minste 1500mA
  - Hallo center/interne pincode moet Hallo positieve pool van Hallo-voeding

Hallo volgende items zijn optioneel:

* Groove Base schild V2
* Groove - temperatuursensor
* Groove-kabel
* Een tussenruimte balken of schroeven in Hallo verpakking, met inbegrip van twee schroeven toofasten Hallo module toohello uitbreiding mededelingenbord en vier sets schroeven en plastic spacers meegeleverd.

> [!NOTE] 
Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Intel Edison instellen

### <a name="assemble-your-board"></a>Het mededelingenbord samenstellen

Deze sectie bevat stappen tooattach het mededelingenbord Intel® Edison module tooyour uitbreiding.

1. Hallo Intel® Edison module binnen Hallo wit overzicht op het mededelingenbord uitbreiding, Hallo gaten op Hallo-module met Hallo schroeven op Hallo uitbreiding mededelingenbord uitgelijnd plaatsen.

2. Druk op Hallo module onder Hallo woorden `What will you make?` totdat u denkt een module dat.

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. Hallo twee hexadecimale nuts (opgenomen in het Hallo-pakket) toosecure Hallo module toohello uitbreiding mededelingenbord gebruiken.

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. Een installatie in een van de vier hoek gaten op Hallo uitbreiding mededelingenbord Hallo invoegen. Draai en dat een witte Hallo plastic spacers op Hallo-installatie wordt versterkt.

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. Herhaal dit voor Hallo andere spacers drie hoek.

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

Nu is het mededelingenbord samengesteld.

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Verbinding maken met de Hallo Groove Base schild en Hallo-temperatuursensor

1. Hallo Groove Base schild op het mededelingenbord tooyour plaatsen. Zorg ervoor dat alle pincodes goed zijn aangesloten op het mededelingenbord.
   
   ![Groove Base schild](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. Gebruik Groove kabel tooconnect Groove-temperatuursensor op Hallo Groove Base schild **A0** poort.

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison en sensor verbinding](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

Nu is uw sensor gereed.

### <a name="power-up-edison"></a>Geef Edison

1. Hallo-voeding sluit.

   ![Plug-in-voeding](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. Een groene LED (met de naam DS1 op Hallo Arduino * uitbreiding mededelingenbord) moet branden en blijf branden.

3. Wacht een minuut voor Hallo mededelingenbord toofinish-up wordt opgestart.

   > [!NOTE]
   > Als u een DC-voeding niet hebt, kunt u nog steeds power Hallo mededelingenbord via een USB-poort. Zie `Connect Edison tooyour computer` sectie voor meer informatie. Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.

### <a name="connect-edison-tooyour-computer"></a>Verbind Edison tooyour computer

1. Schakelen naar beneden Hallo microswitch naar Hallo twee micro USB-poorten, zodat Edison in de apparaatmodus. Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Omlaag Hallo microswitch in-of uitschakelen](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. Plug Hallo andere einde van USB-kabel op uw computer.

   ![Computer USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

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

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

Gefeliciteerd. U hebt Edison geconfigureerd.

## <a name="run-a-sample-application-on-intel-edison"></a>Een voorbeeld van een toepassing uitvoeren op Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Hallo-SDK van Azure IoT-apparaat voorbereiden

1. Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour Intel Edison Hallo. Hallo IP-adres is van het hulpprogramma voor serverconfiguratie Hallo en Hallo wachtwoord Hallo een die u hebt ingesteld in dat hulpprogramma.
    - [PuTTY](http://www.putty.org/) voor Windows.
    - Hallo ingebouwde SSH-client op Ubuntu- of Mac OS.

2. Kloon Hallo voorbeeld-app tooyour clientapparaat. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. Navigeer toohello opslagplaats map toorun Hallo opdracht tooinstall na alle pakketten, toocomplete van serval minuten kan duren.
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a>Configureren en uitvoeren van de voorbeeldtoepassing Hallo

1. Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   Er zijn twee macro's in dit bestand kunt u configurate. Hallo eerst een is `INTERVAL`, definieert een Hallo tijdsinterval tussen twee berichten die toocloud verzenden. tweede Hallo `simulatedData`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.

   Als u **geen Hallo sensor**stelt hello `simulatedData` waarde te`true` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.

1. Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.


1. Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.

U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.

![Output - sensorgegevens uit Intel Edison tooyour iothub worden verzonden](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a>Volgende stappen

U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
