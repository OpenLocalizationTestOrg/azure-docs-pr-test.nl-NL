---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 1: NUC instellen | Microsoft Docs'
description: Intel NUC toowork instellen als een IoT-gateway tussen een sensor en Azure IoT Hub toocollect sensor, gegevens en deze tooIoT Hub te verzenden.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: IOT-gateway, intel-nuc nuc computer, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC instellen als een IoT-gateway

## <a name="what-you-will-do"></a>Wat u doet

- Intel NUC instellen als een IoT-gateway.
- Hello Azure IoT rand pakket installeren op Intel NUC.
- Een voorbeeldtoepassing 'hello_world' uitgevoerd op Intel NUC tooverify Hallo gatewayfunctionaliteit.
Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe tooconnect Intel NUC met de randapparaten.
- Hoe Hallo tooinstall en update vereist hello-pakketten over het gebruik van Intel NUC Smart Package Manager.
- Hoe steekproef toorun Hallo 'hello_world' toepassingsfunctionaliteit tooverify Hallo gateway.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een Intel NUC Kit DE3815TYKE Hello softwarepakket voor Intel IoT Gateway (o de Linux * 7.0.0.13) vooraf is geïnstalleerd.
- Een Ethernet-kabel.
- Een toetsenbord.
- Een HDMI of VGA-kabel.
- Een monitor met een HDMI of VGA-poort.

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC verbinding met de randapparaten Hallo

Hallo in onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:

1. Verbonden tooa toetsenbord.
2. Verbonden toohello monitor door een VGA-kabel of HDMI-kabel.
3. Verbonden tooa bekabelde netwerk door een Ethernet-kabel.
4. Voeding toohello verbonden met een power-kabel.

![Intel NUC tooperipherals verbonden](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Verbinding maken met toohello Intel NUC systeem van de hostcomputer via Secure Shell (SSH)

Hier moet u een toetsenbord en monitor tooget Hallo IP-adres van uw apparaat NUC. Als u Hallo IP weet-adres, kunt u toostep 3 in deze sectie overslaan.

1. Intel NUC inschakelen door op Hallo / uit-knop en logboekbestanden op Hallo-systeem.

   Hallo standaard-gebruikersnaam en wachtwoord zijn beide `root`.

2. Hallo IP-adres van NUC ophalen door het uitvoeren van Hallo `ifconfig` opdracht. Deze stap wordt uitgevoerd op Hallo NUC apparaat.

   Hier volgt een voorbeeld van uitvoer van de opdracht Hallo.

   ![ifconfig-uitvoer met NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   In dit voorbeeld Hallo waarde die volgt `inet addr:` Hallo IP-adres dat u nodig hebt wanneer u van plan tooconnect extern vanaf een host computer tooIntel NUC bent.

3. Gebruik een van de volgende clients SSH uit uw host machine tooconnect tooIntel NUC Hallo.

   - [PuTTY](http://www.putty.org/) voor Windows.
   - Hallo build in SSH-client op Ubuntu- of Mac OS.

   Het is efficiënter en productiever toooperate op Intel NUC van een hostcomputer. U moet Hallo Hallo IP-adres, gebruikersnaam en wachtwoord tooconnect hello NUC via SSH-client. Hier volgt Hallo voorbeeld gebruik SSH-client op Mac OS.
   ![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Hello Azure IoT rand pakket installeren

Hello Azure IoT rand pakket bevat de binaire bestanden voor Hallo vooraf gecompileerde Hallo SDK en de bijbehorende afhankelijkheden. Deze binaire bestanden zijn Azure IoT Edge, hello Azure IoT SDK en Hallo bijbehorende hulpprogramma's. Hallo-pakket bevat ook een 'hello_world'-voorbeeldtoepassing die is gebruikt toovalidate Hallo gatewayfunctionaliteit. IoT-rand Hallo core deel uitmaakt van Hallo-gateway. tooinstall Hallo van het pakket, als volgt te werk:

1. Hallo IoT cloud opslagplaats toevoegen door het uitvoeren van de volgende opdrachten in een terminalvenster Hallo:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Hallo `rpm` opdracht invoer Hallo rpm-sleutel. Hallo `smart channel` opdracht voegt Hallo rpm channel toohello Smart Package Manager. Voordat u Hallo uitvoert `smart update` opdracht, ziet u uitvoer zoals hieronder.

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Hallo-pakket installeren door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`Hallo-naam van het Hallo-pakket is. Hallo `smart install` opdracht gebruikte tooinstall Hallo pakket is.

   Nadat het Hallo-pakket is geïnstalleerd, is Intel NUC verwachte toowork als een gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Hello Azure IoT Edge 'hello_world' voorbeeld van een toepassing uitvoeren

Ga te`azureiotgatewaysdk/samples` en voer 'hello_world' Hallo-voorbeeld voorbeeldtoepassing. Deze voorbeeldtoepassing een gateway maakt van Hallo `hello_world.json` bestands- en Hallo fundamentele onderdelen van hello Azure IoT rand architectuur toolog een Hallo wereld berichtbestand tooa gebruikt om de vijf seconden.

U kunt 'hello_world' Hallo-voorbeeld voorbeeldtoepassing uitvoeren door het uitvoeren van de volgende opdracht Hallo:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Hallo-voorbeeldtoepassing produceert Hallo volgende uitvoer als Hallo gatewayfunctionaliteit correct werkt:

![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Samenvatting

Gefeliciteerd. U klaar bent met het instellen van Intel NUC als een gateway. Nu kunt u nu wordt toomove op het volgende les tooset toohello van uw hostcomputer maken van een Azure-IoT-hub en Registreer uw logische Azure IoT hub-apparaat.

## <a name="next-steps"></a>Volgende stappen
[Bereid u voor uw hostcomputer en Azure IoT hub](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
