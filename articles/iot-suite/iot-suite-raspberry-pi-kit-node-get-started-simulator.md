---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met gesimuleerde telemetrie met behulp van Node.js | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik van Node.js tooconnect uw oplossing voor externe controle frambozen Pi toohello, gesimuleerde telemetrie toohello cloud verzenden en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="a0beb-104">Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en verzenden van gesimuleerde telemetrie met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="a0beb-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="a0beb-105">Deze zelfstudie leert u hoe toouse Hallo frambozen Pi 3 toosimulate temperatuur en vochtigheid gegevens toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="a0beb-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="a0beb-106">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a0beb-106">hello tutorial uses:</span></span>

- <span data-ttu-id="a0beb-107">Raspbian OS Node.js programmeertaal Hallo en hello van Microsoft Azure IoT SDK voor Node.js tooimplement een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a0beb-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="a0beb-108">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="a0beb-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a0beb-109">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0beb-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a0beb-110">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="a0beb-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a0beb-111">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="a0beb-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a0beb-112">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="a0beb-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a0beb-113">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="a0beb-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="a0beb-114">Downloaden en configureren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a0beb-114">Download and configure hello sample</span></span>

<span data-ttu-id="a0beb-115">U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="a0beb-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="a0beb-116">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="a0beb-116">Install Node.js</span></span>

<span data-ttu-id="a0beb-117">Als u dit nog niet hebt gedaan, installeert u Node.js op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="a0beb-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="a0beb-118">Hallo IoT SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger.</span><span class="sxs-lookup"><span data-stu-id="a0beb-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="a0beb-119">Hallo volgende stappen ziet u hoe tooinstall Node.js v6.10.2 op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="a0beb-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="a0beb-120">Hallo opdracht tooupdate na uw frambozen-Pi gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0beb-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="a0beb-121">Hallo opdracht toodownload hello Node.js binaire bestanden tooyour frambozen Pi volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0beb-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a0beb-122">Gebruik Hallo opdracht tooinstall Hallo binaire bestanden te volgen:</span><span class="sxs-lookup"><span data-stu-id="a0beb-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a0beb-123">Gebruik Hallo volgende opdracht tooverify die u hebt de Node.js-v6.10.2 is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="a0beb-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="a0beb-124">Hallo-opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="a0beb-124">Clone hello repositories</span></span>

<span data-ttu-id="a0beb-125">Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten in een terminal op uw Pi volgen:</span><span class="sxs-lookup"><span data-stu-id="a0beb-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="a0beb-126">Verbindingsreeks Hallo-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="a0beb-126">Update hello device connection string</span></span>

<span data-ttu-id="a0beb-127">Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a0beb-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="a0beb-128">Hallo regel zoeken:</span><span class="sxs-lookup"><span data-stu-id="a0beb-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="a0beb-129">Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-apparaat en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a0beb-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="a0beb-130">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="a0beb-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="a0beb-131">Hallo-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a0beb-131">Run hello sample</span></span>

<span data-ttu-id="a0beb-132">Voer Hallo deze opdrachten tooinstall Hallo vereiste pakketten voor Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0beb-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="a0beb-133">U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="a0beb-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="a0beb-134">Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="a0beb-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="a0beb-135">Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:</span><span class="sxs-lookup"><span data-stu-id="a0beb-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="a0beb-137">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="a0beb-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="a0beb-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0beb-138">Next steps</span></span>

<span data-ttu-id="a0beb-139">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="a0beb-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
