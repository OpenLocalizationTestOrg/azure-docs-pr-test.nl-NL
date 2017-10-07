---
title: 'SensorTag apparaat & Azure IoT Gateway - les 1: Intel NUC instellen | Microsoft Docs'
description: Intel NUC toowork instellen als een IoT-gateway tussen een sensor en Azure IoT Hub toocollect sensor, gegevens en deze tooIoT Hub te verzenden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-gateway, intel-nuc nuc computer, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC instellen als een IoT-gateway
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Wat u doet

- Intel NUC instellen als een IoT-gateway.
- Hello Azure IoT rand pakket installeren op Hallo Intel NUC.
- Een voorbeeldtoepassing 'hello_world' uitgevoerd op Hallo Intel NUC tooverify Hallo gatewayfunctionaliteit.

  > Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe tooconnect Intel NUC met de randapparaten.
- Hoe Hallo tooinstall en update vereist hello-pakketten over het gebruik van Intel NUC Smart Package Manager.
- Hoe steekproef toorun Hallo 'hello_world' toepassingsfunctionaliteit tooverify Hallo gateway.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een Intel NUC Kit DE3815TYKE Hello softwarepakket voor Intel IoT Gateway (o de Linux * 7.0.0.13) vooraf is geïnstalleerd. [Klik hier toopurchase Groove IoT commerciële Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Een Ethernet-kabel.
- Een toetsenbord.
- Een HDMI of VGA-kabel.
- Een monitor met een HDMI of VGA-poort.
- Optioneel: [Texas instrumenten Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC verbinding met de randapparaten Hallo

Hallo in onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:

1. Verbonden tooa toetsenbord.
2. Monitor tooa verbonden met een VGA-kabel of HDMI-kabel.
3. Verbonden tooa bekabelde netwerk met een Ethernet-kabel.
4. Voeding tooa verbonden met een power-kabel.

![Intel NUC tooperipherals verbonden](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Verbinding maken met toohello Intel NUC systeem van de hostcomputer via Secure Shell (SSH)

U moet een toetsenbord en een monitor tooget Hallo IP-adres van uw apparaat Intel NUC. Als u Hallo IP weet-adres, kunt u vooruit toostep 3 in deze sectie overslaan.

1. Hallo Intel NUC inschakelen door te drukken Hallo / uit-knop en meld u vervolgens aan.

   Hallo standaard-gebruikersnaam en wachtwoord zijn beide `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Hallo IP-adres van Hallo Intel NUC ophalen door het uitvoeren van Hallo `ifconfig` opdracht op Hallo Intel NUC apparaat.

   Hier volgt een voorbeeld van uitvoer van de opdracht Hallo.

   ![ifconfig-uitvoer met Intel NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   In dit voorbeeld Hallo waarde die volgt `inet addr:` Hallo IP-adres is die u nodig hebt wanneer een verbinding tussen toohello Intel NUC van een hostcomputer.

3. Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooIntel NUC Hallo.

    - [PuTTY](http://www.putty.org/) voor Windows.
    - Hallo ingebouwde SSH-client op Ubuntu- of Mac OS.

   Het is efficiënter en productiever toooperate een Intel NUC van een hostcomputer. U zult nodig Hallo Intel NUC van IP-adres, gebruiker en het wachtwoord tooconnect tooit via een SSH-client. Hier volgt een voorbeeld dat gebruikmaakt van een SSH-client op Mac OS.
   ![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Hello Azure IoT rand pakket installeren

Hello Azure IoT rand pakket bevat de binaire bestanden voor Hallo vooraf gecompileerde van IoT-rand en de bijbehorende afhankelijkheden. Deze binaire bestanden zijn Azure IoT Edge, hello Azure IoT SDK en Hallo bijbehorende hulpprogramma's. Hallo pakket bevat ook een 'hello_world' is gebruikte toovalidate Hallo gatewayfunctionaliteit voorbeeldtoepassing. IoT-rand Hallo core deel uitmaakt van Hallo-gateway. 

Volg deze stappen tooinstall Hallo-pakket.

1. Hallo IoT Cloud-opslagplaats toevoegen door het uitvoeren van de volgende opdrachten in een terminalvenster Hallo:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Voer 'y' als too'Include vraagt dit kanaal?'
   
   Als u krijgt een `import read failed(-1)` gebruik Hallo opdrachten tooresolve Hallo probleem volgende fout is opgetreden:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Hallo `rpm` opdracht invoer Hallo rpm-sleutel. Hallo `smart channel` opdracht voegt Hallo rpm channel toohello Smart Package Manager. Voordat u Hallo uitvoert `smart update` uitvoert, ziet u uitvoer zoals hieronder.

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Hallo smart update-opdracht uitvoeren:

   ```bash
   smart update
   ```

3. Hello Azure IoT Gateway-pakket installeren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`Hallo-naam van het Hallo-pakket is. Hallo `smart install` opdracht gebruikte tooinstall Hallo pakket is.

    > Voer Hallo volgende opdracht uit als u deze fout te zien: 'openbare sleutel niet beschikbaar'

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Hallo Intel NUC opnieuw opstarten als u deze fout ziet: 'Er is geen pakket biedt util-linux-dev'

   Nadat het Hallo-pakket is geïnstalleerd, is Intel NUC gereed toofunction als een gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Hello Azure IoT Edge 'hello_world' voorbeeld van een toepassing uitvoeren

Hallo volgende voorbeeld van een toepassing maakt een gateway vanuit een `hello_world.json` bestands- en Hallo fundamentele onderdelen van Azure IoT rand architectuur toolog een hello world tooa berichtbestand (log.txt) gebruikt om de vijf seconden.

U kunt Hallo Hallo wereld-voorbeeld uitvoeren door het uitvoeren van de volgende opdrachten Hallo:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Hallo wereld Hallo-toepassing uitvoeren voor een paar minuten en klik vervolgens op Hallo Enter key toostop, kunnen deze.
![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> U kunt negeren 'ongeldig argument handle(NULL)' fouten die worden weergegeven nadat u druk op Enter.

U kunt controleren dat Hallo-gateway is uitgevoerd door het openen van Hallo log.txt-bestand dat is nu in de map hello_world ![log.txt directory weergeven](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Open log.txt Hallo volgende opdracht gebruiken:

```bash
vim log.txt
```

Vervolgens ziet u Hallo inhoud van log.txt die als een JSON-indeling uitvoer van Hallo berichtregistratie die elke vijf seconden module voor gateway Hallo wereld Hallo zijn geschreven.
![log.txt directory weergeven](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Samenvatting

Gefeliciteerd. U klaar bent met het instellen van Intel NUC als een gateway. Nu u klaar toomove op de volgende les tooset toohello uw hostcomputer van de bent, een Azure-IoT-Hub maken en registreren van uw logische Azure IoT Hub-apparaat.

## <a name="next-steps"></a>Volgende stappen
[Een IoT gateway tooconnect een apparaat tooAzure IoT Hub gebruiken](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

