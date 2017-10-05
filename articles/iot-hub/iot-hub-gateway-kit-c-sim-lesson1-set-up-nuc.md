---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 1: NUC instellen | Microsoft Docs'
description: Intel NUC instellen om te werken als een IoT-gateway tussen een sensor en Azure IoT Hub sensor gegevens kunt verzamelen en verzenden naar IoT Hub.
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC instellen als een IoT-gateway

## <a name="what-you-will-do"></a>Wat u doet

- Intel NUC instellen als een IoT-gateway.
- Installeer het pakket Azure IoT Edge op Intel NUC.
- Voer een voorbeeldtoepassing 'hello_world' op Intel NUC om te controleren of de functionaliteit van de gateway.
Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Klik hier voor meer informatie over het Intel NUC verbinding met de randapparaten.
- Informatie over het installeren en bijwerken van de vereiste pakketten op Intel NUC met behulp van de smartcard Package Manager.
- Het uitvoeren van de voorbeeldtoepassing 'hello_world' om te controleren of de functionaliteit van de gateway.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een Intel NUC Kit DE3815TYKE met Intel IoT Gateway Software Suite (o de Linux * 7.0.0.13) vooraf is geïnstalleerd.
- Een Ethernet-kabel.
- Een toetsenbord.
- Een HDMI of VGA-kabel.
- Een monitor met een HDMI of VGA-poort.

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a>Intel NUC verbinden met de randapparaten

De onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:

1. Verbonden met een toetsenbord.
2. Verbonden met de monitor door een VGA-kabel of HDMI-kabel.
3. Verbonden met een bekabeld netwerk door een Ethernet-kabel.
4. Verbonden met de voeding met een power-kabel.

![Intel NUC verbonden met de randapparaten](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Verbinding maken met de Intel NUC-systeem van de hostcomputer via Secure Shell (SSH)

U moet hier toetsenbord en de monitor voor het IP-adres van uw apparaat NUC ophalen. Als u het IP-adres al weet, kunt u naar stap 3 in deze sectie overslaan.

1. Intel NUC inschakelen door op de knop Power en meld u bij het systeem.

   De standaard-gebruikersnaam en wachtwoord zijn beide `root`.

2. Het IP-adres van NUC ophalen door het uitvoeren van de `ifconfig` opdracht. Deze stap wordt uitgevoerd op het apparaat NUC.

   Hier volgt een voorbeeld van uitvoer van de opdracht.

   ![ifconfig-uitvoer met NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   In dit voorbeeld wordt de waarde die volgt `inet addr:` is het IP-adres dat u nodig hebt wanneer u van plan bent extern verbinding kunnen maken van een hostcomputer te Intel NUC.

3. Gebruik een van de volgende SSH-clients van uw hostmachine verbinding maken met de Intel NUC.

   - [PuTTY](http://www.putty.org/) voor Windows.
   - De build in SSH-client op Ubuntu- of Mac OS.

   Het is efficiënter en productiever bewerkingen uitvoeren op Intel NUC van een hostcomputer. U moet het de IP-adres, gebruikersnaam en wachtwoord voor het verbinding maken met de NUC via SSH-client. Hier volgt de voorbeeld gebruik SSH-client op Mac OS.
   ![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-the-azure-iot-edge-package"></a>Installeer het Azure IoT Edge-pakket

Het Azure-IoT-Edge-pakket bevat de vooraf gecompileerde binaire bestanden van de SDK en de bijbehorende afhankelijkheden. Deze binaire bestanden zijn Azure IoT Edge, de Azure IoT SDK en de bijbehorende hulpprogramma's. Het pakket bevat ook een 'hello_world'-voorbeeldtoepassing die wordt gebruikt voor het valideren van de functionaliteit van de gateway. IoT-rand is het belangrijkste deel van de gateway. Volg deze stappen voor het installeren van het pakket:

1. De IoT-cloud-opslagplaats met de volgende opdrachten in een terminalvenster toevoegen:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   De `rpm` opdracht wordt de sleutel rpm geïmporteerd. De `smart channel` opdracht voegt het rpm-kanaal naar de smartcard Package Manager. Voordat u de `smart update` opdracht, ziet u uitvoer zoals hieronder.

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Installeer het pakket met de volgende opdracht:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`is de naam van het pakket. De `smart install` opdracht wordt gebruikt om het pakket te installeren.

   Nadat het pakket is geïnstalleerd, Intel NUC naar verwachting werken als een gateway.

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a>De voorbeeldtoepassing voor Azure IoT Edge 'hello_world' uitvoeren

Ga naar `azureiotgatewaysdk/samples` en de voorbeeldtoepassing 'hello_world' in het voorbeeld uitvoert. Deze voorbeeldtoepassing maakt u een gateway vanuit de `hello_world.json` bestand en de fundamentele onderdelen van de rand van Azure IoT-architectuur gebruikt voor het vastleggen van een Hallo wereld-bericht in een bestand om de vijf seconden.

U kunt de voorbeeldtoepassing 'hello_world'-voorbeeld uitvoeren door met de volgende opdracht:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Als de functionaliteit van de gateway correct werkt, wordt de voorbeeldtoepassing in de volgende uitvoer gegenereerd:

![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Samenvatting

Gefeliciteerd. U klaar bent met het instellen van Intel NUC als een gateway. U kunt nu klaar om door te gaan met de volgende les instellen van de hostcomputer, een Azure IoT hub maken en registreren van uw logische Azure IoT hub-apparaat.

## <a name="next-steps"></a>Volgende stappen
[Bereid u voor uw hostcomputer en Azure IoT hub](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
