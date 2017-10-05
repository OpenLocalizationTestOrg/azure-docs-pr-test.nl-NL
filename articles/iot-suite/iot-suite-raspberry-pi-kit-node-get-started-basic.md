---
title: Verbinding maken met een Pi frambozen Azure IoT Suite met echte sensoren met behulp van Node.js | Microsoft Docs
description: Gebruik de Microsoft Azure IoT Starter Kit voor de Raspberry Pi 3 en Azure IoT Suite. Gebruik Node.js verbinding maken met uw frambozen-Pi de oplossing voor externe controle verzenden van telemetrie van sensoren naar de cloud, en reageren op de methoden die worden aangeroepen vanuit het dashboard van oplossing.
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
ms.openlocfilehash: 91546157cc8eabf68706391ce706038d8dc5f82d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="b00d8-104">Uw frambozen Pi 3 verbinding met de oplossing voor externe controle en verzend telemetrie vanuit een echte sensor met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="b00d8-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="b00d8-105">Deze zelfstudie laat zien hoe de Microsoft Azure IoT Starter Kit voor frambozen Pi 3 gebruiken voor het ontwikkelen van een temperatuur en vochtigheid lezer die met de cloud communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="b00d8-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="b00d8-106">De zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b00d8-106">The tutorial uses:</span></span>

- <span data-ttu-id="b00d8-107">Raspbian OS, de programmeertaal Node.js en Microsoft Azure IoT SDK voor Node.js voor het implementeren van een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b00d8-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="b00d8-108">IoT Suite remote monitoring vooraf geconfigureerde oplossing als de cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="b00d8-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="b00d8-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b00d8-109">Overview</span></span>

<span data-ttu-id="b00d8-110">In deze zelfstudie maakt uitvoeren u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b00d8-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="b00d8-111">Implementeer een exemplaar van de vooraf geconfigureerde oplossing voor externe controle op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b00d8-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="b00d8-112">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="b00d8-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="b00d8-113">Instellen van het apparaat en de sensoren om te communiceren met uw computer en de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="b00d8-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="b00d8-114">Werk de voorbeeldcode van de apparaten verbinding maken met de oplossing voor externe controle en verzenden van telemetrie die u op het dashboard van de oplossing weergeven kunt.</span><span class="sxs-lookup"><span data-stu-id="b00d8-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="b00d8-115">De oplossing voor externe controle levert een set van Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b00d8-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="b00d8-116">De implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="b00d8-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="b00d8-117">Om te voorkomen dat een Azure-verbruik onnodige kosten, verwijdert u uw exemplaar van de vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="b00d8-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="b00d8-118">Als u de vooraf geconfigureerde oplossing meer nodig hebt, kunt u het eenvoudig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b00d8-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="b00d8-119">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="b00d8-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="b00d8-120">Downloaden en configureren van de steekproef</span><span class="sxs-lookup"><span data-stu-id="b00d8-120">Download and configure the sample</span></span>

<span data-ttu-id="b00d8-121">U kunt nu downloaden en configureren van de externe clienttoepassing bewaking op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="b00d8-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="b00d8-122">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="b00d8-122">Install Node.js</span></span>

<span data-ttu-id="b00d8-123">Installeer Node.js op uw Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b00d8-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="b00d8-124">De IoT-SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger.</span><span class="sxs-lookup"><span data-stu-id="b00d8-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="b00d8-125">De volgende stappen ziet u hoe Node.js v6.10.2 installeren op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="b00d8-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="b00d8-126">Gebruik de volgende opdracht om bij te werken uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="b00d8-126">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="b00d8-127">Gebruik de volgende opdracht voor het downloaden van de Node.js-binaire bestanden naar uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="b00d8-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="b00d8-128">Gebruik de volgende opdracht voor het installeren van de binaire bestanden:</span><span class="sxs-lookup"><span data-stu-id="b00d8-128">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="b00d8-129">Gebruik de volgende opdracht om te controleren of dat u hebt de Node.js-v6.10.2 is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="b00d8-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="b00d8-130">De opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="b00d8-130">Clone the repositories</span></span>

<span data-ttu-id="b00d8-131">Als u dit nog niet hebt gedaan, moet u de vereiste opslagplaatsen klonen door de volgende opdrachten uitvoeren op uw Pi:</span><span class="sxs-lookup"><span data-stu-id="b00d8-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="b00d8-132">De verbindingsreeks apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="b00d8-132">Update the device connection string</span></span>

<span data-ttu-id="b00d8-133">Open het voorbeeld-bronbestand in de **nano** editor met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b00d8-133">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="b00d8-134">Zoek de regel:</span><span class="sxs-lookup"><span data-stu-id="b00d8-134">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="b00d8-135">Vervang de tijdelijke aanduiding voor waarden met het apparaat en IoT Hub informatie u gemaakt en opgeslagen aan het begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b00d8-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="b00d8-136">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="b00d8-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="b00d8-137">Het voorbeeld uitvoert</span><span class="sxs-lookup"><span data-stu-id="b00d8-137">Run the sample</span></span>

<span data-ttu-id="b00d8-138">Voer de volgende opdrachten voor het installeren van de vereiste pakketten voor de steekproef:</span><span class="sxs-lookup"><span data-stu-id="b00d8-138">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="b00d8-139">U kunt nu het voorbeeldprogramma uitvoeren op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="b00d8-139">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="b00d8-140">Voer de opdracht:</span><span class="sxs-lookup"><span data-stu-id="b00d8-140">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="b00d8-141">De volgende voorbeelduitvoer volgt een voorbeeld van de uitvoer die u bij de opdrachtprompt op de Pi frambozen zien:</span><span class="sxs-lookup"><span data-stu-id="b00d8-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="b00d8-143">Druk op **Ctrl-C** om af te sluiten van het programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="b00d8-143">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="b00d8-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b00d8-144">Next steps</span></span>

<span data-ttu-id="b00d8-145">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b00d8-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
