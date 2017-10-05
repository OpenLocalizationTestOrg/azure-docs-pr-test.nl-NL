---
title: Een Pi frambozen verbinden met behulp van Node.js met gesimuleerde telemetrie van Azure IoT Suite | Microsoft Docs
description: Gebruik de Microsoft Azure IoT Starter Kit voor de Raspberry Pi 3 en Azure IoT Suite. Gebruik Node.js verbinding maken met uw frambozen-Pi de oplossing voor externe controle gesimuleerde telemetrie verzenden naar de cloud, en reageren op de methoden die worden aangeroepen vanuit het dashboard van oplossing.
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
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="7dda7-104">Uw frambozen Pi 3 verbinding met de oplossing voor externe controle en verzenden van gesimuleerde telemetrie met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="7dda7-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="7dda7-105">Deze zelfstudie laat zien hoe u met de frambozen Pi 3 simuleren temperatuur en vochtigheid gegevens worden verzonden naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="7dda7-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="7dda7-106">De zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="7dda7-106">The tutorial uses:</span></span>

- <span data-ttu-id="7dda7-107">Raspbian OS, de programmeertaal Node.js en Microsoft Azure IoT SDK voor Node.js voor het implementeren van een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7dda7-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="7dda7-108">IoT Suite remote monitoring vooraf geconfigureerde oplossing als de cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="7dda7-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="7dda7-109">De oplossing voor externe controle levert een set van Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7dda7-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="7dda7-110">De implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="7dda7-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="7dda7-111">Om te voorkomen dat een Azure-verbruik onnodige kosten, verwijdert u uw exemplaar van de vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="7dda7-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="7dda7-112">Als u de vooraf geconfigureerde oplossing meer nodig hebt, kunt u het eenvoudig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7dda7-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="7dda7-113">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="7dda7-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="7dda7-114">Downloaden en configureren van de steekproef</span><span class="sxs-lookup"><span data-stu-id="7dda7-114">Download and configure the sample</span></span>

<span data-ttu-id="7dda7-115">U kunt nu downloaden en configureren van de externe clienttoepassing bewaking op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="7dda7-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="7dda7-116">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="7dda7-116">Install Node.js</span></span>

<span data-ttu-id="7dda7-117">Als u dit nog niet hebt gedaan, installeert u Node.js op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="7dda7-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="7dda7-118">De IoT-SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger.</span><span class="sxs-lookup"><span data-stu-id="7dda7-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="7dda7-119">De volgende stappen ziet u hoe Node.js v6.10.2 installeren op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="7dda7-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="7dda7-120">Gebruik de volgende opdracht om bij te werken uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="7dda7-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="7dda7-121">Gebruik de volgende opdracht voor het downloaden van de Node.js-binaire bestanden naar uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="7dda7-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7dda7-122">Gebruik de volgende opdracht voor het installeren van de binaire bestanden:</span><span class="sxs-lookup"><span data-stu-id="7dda7-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7dda7-123">Gebruik de volgende opdracht om te controleren of dat u hebt de Node.js-v6.10.2 is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="7dda7-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="7dda7-124">De opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="7dda7-124">Clone the repositories</span></span>

<span data-ttu-id="7dda7-125">Als u dit nog niet hebt gedaan, moet u de vereiste opslagplaatsen klonen met de volgende opdrachten in een terminal op uw Pi:</span><span class="sxs-lookup"><span data-stu-id="7dda7-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="7dda7-126">De verbindingsreeks apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="7dda7-126">Update the device connection string</span></span>

<span data-ttu-id="7dda7-127">Open het voorbeeld-bronbestand in de **nano** editor met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7dda7-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="7dda7-128">Zoek de regel:</span><span class="sxs-lookup"><span data-stu-id="7dda7-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="7dda7-129">Vervang de tijdelijke aanduiding voor waarden met het apparaat en IoT Hub informatie u gemaakt en opgeslagen aan het begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7dda7-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="7dda7-130">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="7dda7-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="7dda7-131">Het voorbeeld uitvoert</span><span class="sxs-lookup"><span data-stu-id="7dda7-131">Run the sample</span></span>

<span data-ttu-id="7dda7-132">Voer de volgende opdrachten voor het installeren van de vereiste pakketten voor de steekproef:</span><span class="sxs-lookup"><span data-stu-id="7dda7-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="7dda7-133">U kunt nu het voorbeeldprogramma uitvoeren op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="7dda7-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="7dda7-134">Voer de opdracht:</span><span class="sxs-lookup"><span data-stu-id="7dda7-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="7dda7-135">De volgende voorbeelduitvoer volgt een voorbeeld van de uitvoer die u bij de opdrachtprompt op de Pi frambozen zien:</span><span class="sxs-lookup"><span data-stu-id="7dda7-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="7dda7-137">Druk op **Ctrl-C** om af te sluiten van het programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="7dda7-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="7dda7-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7dda7-138">Next steps</span></span>

<span data-ttu-id="7dda7-139">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="7dda7-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
