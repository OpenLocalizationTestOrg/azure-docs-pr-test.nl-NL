---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met C met gesimuleerde telemetrie | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik C tooconnect uw oplossing voor externe controle frambozen Pi toohello, gesimuleerde telemetrie toohello cloud verzenden en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="9ed19-104">Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en gesimuleerde telemetrie met C verzenden</span><span class="sxs-lookup"><span data-stu-id="9ed19-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="9ed19-105">Deze zelfstudie leert u hoe toouse Hallo frambozen Pi 3 toosimulate temperatuur en vochtigheid gegevens toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="9ed19-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="9ed19-106">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9ed19-106">hello tutorial uses:</span></span>

- <span data-ttu-id="9ed19-107">Raspbian OS Hallo C programmeertaal en Hallo Microsoft Azure IoT SDK voor C tooimplement een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9ed19-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="9ed19-108">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="9ed19-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="9ed19-109">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9ed19-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="9ed19-110">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="9ed19-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="9ed19-111">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="9ed19-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="9ed19-112">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="9ed19-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="9ed19-113">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9ed19-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="9ed19-114">Downloaden en configureren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9ed19-114">Download and configure hello sample</span></span>

<span data-ttu-id="9ed19-115">U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="9ed19-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="9ed19-116">Hallo-opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="9ed19-116">Clone hello repositories</span></span>

<span data-ttu-id="9ed19-117">Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten in een terminal op uw Pi volgen:</span><span class="sxs-lookup"><span data-stu-id="9ed19-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="9ed19-118">Verbindingsreeks Hallo-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="9ed19-118">Update hello device connection string</span></span>

<span data-ttu-id="9ed19-119">Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9ed19-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="9ed19-120">Zoek Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="9ed19-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="9ed19-121">Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-apparaat en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="9ed19-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="9ed19-122">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="9ed19-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="9ed19-123">Hallo voorbeeld bouwen</span><span class="sxs-lookup"><span data-stu-id="9ed19-123">Build hello sample</span></span>

<span data-ttu-id="9ed19-124">Vereiste hello-pakketten voor Hallo Microsoft Azure IoT-apparaat-SDK voor C door het uitvoeren van de volgende opdrachten in een terminal op Hallo frambozen Pi Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="9ed19-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="9ed19-125">U kunt nu Voorbeeldoplossing Hallo bijgewerkt op Hallo frambozen Pi bouwen:</span><span class="sxs-lookup"><span data-stu-id="9ed19-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="9ed19-126">U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="9ed19-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="9ed19-127">Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="9ed19-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="9ed19-128">Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:</span><span class="sxs-lookup"><span data-stu-id="9ed19-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="9ed19-130">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="9ed19-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="9ed19-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ed19-131">Next steps</span></span>

<span data-ttu-id="9ed19-132">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9ed19-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
