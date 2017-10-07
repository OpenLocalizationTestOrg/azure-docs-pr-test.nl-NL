---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met echte sensoren met behulp van Node.js | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Node.js tooconnect uw oplossing voor externe controle frambozen Pi toohello gebruiken, verzenden van telemetrie van sensoren toohello cloud en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="9bef7-104">Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en verzend telemetrie vanuit een echte sensor met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="9bef7-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="9bef7-105">Deze zelfstudie leert u hoe toouse hello Microsoft Azure IoT Starter Kit voor frambozen Pi 3 toodevelop temperatuur en vochtigheid lezer die kan communiceren met de Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="9bef7-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="9bef7-106">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9bef7-106">hello tutorial uses:</span></span>

- <span data-ttu-id="9bef7-107">Raspbian OS Node.js programmeertaal Hallo en hello van Microsoft Azure IoT SDK voor Node.js tooimplement een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9bef7-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="9bef7-108">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="9bef7-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="9bef7-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9bef7-109">Overview</span></span>

<span data-ttu-id="9bef7-110">In deze zelfstudie maakt uitvoeren u Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="9bef7-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="9bef7-111">Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9bef7-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="9bef7-112">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="9bef7-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="9bef7-113">Stel uw apparaat en sensoren toocommunicate met uw computer en het Hallo oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="9bef7-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="9bef7-114">Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle bijwerken en verzenden van telemetrie die u op Hallo oplossing dashboard weergeven kunt.</span><span class="sxs-lookup"><span data-stu-id="9bef7-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="9bef7-115">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9bef7-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="9bef7-116">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="9bef7-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="9bef7-117">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="9bef7-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="9bef7-118">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="9bef7-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="9bef7-119">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9bef7-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="9bef7-120">Downloaden en configureren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9bef7-120">Download and configure hello sample</span></span>

<span data-ttu-id="9bef7-121">U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="9bef7-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="9bef7-122">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="9bef7-122">Install Node.js</span></span>

<span data-ttu-id="9bef7-123">Installeer Node.js op uw Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9bef7-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="9bef7-124">Hallo IoT SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger.</span><span class="sxs-lookup"><span data-stu-id="9bef7-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="9bef7-125">Hallo volgende stappen ziet u hoe tooinstall Node.js v6.10.2 op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="9bef7-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="9bef7-126">Hallo opdracht tooupdate na uw frambozen-Pi gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9bef7-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="9bef7-127">Hallo opdracht toodownload hello Node.js binaire bestanden tooyour frambozen Pi volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9bef7-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="9bef7-128">Gebruik Hallo opdracht tooinstall Hallo binaire bestanden te volgen:</span><span class="sxs-lookup"><span data-stu-id="9bef7-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="9bef7-129">Gebruik Hallo volgende opdracht tooverify die u hebt de Node.js-v6.10.2 is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="9bef7-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="9bef7-130">Hallo-opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="9bef7-130">Clone hello repositories</span></span>

<span data-ttu-id="9bef7-131">Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten op uw Pi volgen:</span><span class="sxs-lookup"><span data-stu-id="9bef7-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="9bef7-132">Verbindingsreeks Hallo-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="9bef7-132">Update hello device connection string</span></span>

<span data-ttu-id="9bef7-133">Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bef7-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="9bef7-134">Hallo regel zoeken:</span><span class="sxs-lookup"><span data-stu-id="9bef7-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="9bef7-135">Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-apparaat en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="9bef7-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="9bef7-136">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="9bef7-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="9bef7-137">Hallo-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9bef7-137">Run hello sample</span></span>

<span data-ttu-id="9bef7-138">Voer Hallo deze opdrachten tooinstall Hallo vereiste pakketten voor Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9bef7-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="9bef7-139">U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="9bef7-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="9bef7-140">Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="9bef7-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="9bef7-141">Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:</span><span class="sxs-lookup"><span data-stu-id="9bef7-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="9bef7-143">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="9bef7-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="9bef7-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bef7-144">Next steps</span></span>

<span data-ttu-id="9bef7-145">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9bef7-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
