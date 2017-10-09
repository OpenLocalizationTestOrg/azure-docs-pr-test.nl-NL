---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een gesimuleerd apparaat voorbeeld-app toosend temperatuur tooyour iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="2ac97-104">Configureren en uitvoeren van een gesimuleerd apparaat voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="2ac97-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2ac97-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2ac97-105">What you will do</span></span>

- <span data-ttu-id="2ac97-106">Kloon Hallo voorbeeld opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="2ac97-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="2ac97-107">Gebruik uw IoT-hub en logische apparaatgegevens hello Azure CLI tooget voor de voorbeeldtoepassing gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ac97-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="2ac97-108">Configureren en uitvoeren van de voorbeeldtoepassing voor Hallo gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ac97-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="2ac97-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2ac97-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2ac97-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2ac97-110">What you will learn</span></span>

<span data-ttu-id="2ac97-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="2ac97-111">In this article, you will learn:</span></span>

- <span data-ttu-id="2ac97-112">Hoe tooconfigure en Voer Hallo gesimuleerd apparaat voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2ac97-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2ac97-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2ac97-113">What you need</span></span>

<span data-ttu-id="2ac97-114">U moet hebt voltooid</span><span class="sxs-lookup"><span data-stu-id="2ac97-114">You must have successfully completed</span></span>

- [<span data-ttu-id="2ac97-115">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="2ac97-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="2ac97-116">Kloon Hallo voorbeeld opslagplaats toohello hostcomputer</span><span class="sxs-lookup"><span data-stu-id="2ac97-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="2ac97-117">tooclone hello voorbeeld opslagplaats als volgt te werk op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ac97-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2ac97-118">Open een opdrachtprompt in Windows of een terminal in Mac OS of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2ac97-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="2ac97-119">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2ac97-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="2ac97-120">Hallo gesimuleerde apparaat en uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="2ac97-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="2ac97-121">Open Hallo-configuratiebestand `config.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2ac97-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="2ac97-122">Vervang `"has_sensortag": true` met`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="2ac97-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configuratie hebt u niet een TI SensorTag-apparaat](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="2ac97-124">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="2ac97-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="2ac97-125">Open `config-gateway.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2ac97-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="2ac97-126">Hallo volgende coderegel zoeken en vervangen `[device hostname or IP address]` met IP-adres of de hostnaam naam Hallo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2ac97-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="2ac97-127">![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2ac97-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="2ac97-128">De verbindingsreeks Hallo van uw IoT hub logisch apparaat ophalen</span><span class="sxs-lookup"><span data-stu-id="2ac97-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="2ac97-129">tooget hello Azure IoT hub-verbindingsreeks van het logische apparaat, uitvoeren van de volgende opdracht op de hostcomputer Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ac97-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="2ac97-130">`{IoT hub name}`is Hallo naam IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ac97-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="2ac97-131">Iot-gateway gebruiken als de waarde van Hallo `{resource group name}` en mydevice gebruiken als Hallo-waarde van `{device id}` als u Hallo-waarde in les 2 niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2ac97-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="2ac97-132">Hallo gesimuleerd apparaat cloud uploaden-voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="2ac97-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="2ac97-133">tooconfigure en Voer Hallo gesimuleerd apparaat cloud voorbeeldtoepassing uploaden, als volgt te werk op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ac97-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2ac97-134">Open `config-sensortag.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2ac97-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="2ac97-136">Controleer Hallo vervangingen in Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ac97-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="2ac97-137">Vervang `[IoT hub name]` met naam Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac97-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="2ac97-138">Vervang `[IoT device connection string]` met de verbindingsreeks Hallo van uw IoT hub logisch apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ac97-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="2ac97-139">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2ac97-139">Run hello application.</span></span>

   <span data-ttu-id="2ac97-140">Implementeren en uitvoeren van de toepassing hello door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ac97-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="2ac97-141">Controleren Hallo voorbeeld toepassing werkt</span><span class="sxs-lookup"><span data-stu-id="2ac97-141">Verify hello sample application works</span></span>

<span data-ttu-id="2ac97-142">U ziet nu Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2ac97-142">You should now see output like hello following:</span></span>

![de toepassing voorbeelduitvoer gesimuleerd apparaat](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="2ac97-144">Hallo toepassing verzendt temperatuur gegevens tooyour IoT-hub 40 seconden duurt.</span><span class="sxs-lookup"><span data-stu-id="2ac97-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="2ac97-145">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2ac97-145">Summary</span></span>

<span data-ttu-id="2ac97-146">U hebt geconfigureerd en Voer Hallo gesimuleerd apparaat cloud uploaden voorbeeldtoepassing die gegevens tooyour iothub met gesimuleerde apparaat verzendt.</span><span class="sxs-lookup"><span data-stu-id="2ac97-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ac97-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ac97-147">Next steps</span></span>
[<span data-ttu-id="2ac97-148">Berichten van de IoT-hub lezen</span><span class="sxs-lookup"><span data-stu-id="2ac97-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)