---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een gesimuleerd apparaat voorbeeld-app temperatuur om gegevens te verzenden naar uw IoT-hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="3b531-104">Configureren en uitvoeren van een gesimuleerd apparaat voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="3b531-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3b531-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3b531-105">What you will do</span></span>

- <span data-ttu-id="3b531-106">Kloon de opslagplaats voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3b531-106">Clone the sample repository.</span></span>
- <span data-ttu-id="3b531-107">De Azure CLI gebruiken om uw IoT-hub en logische apparaatgegevens voor de voorbeeldtoepassing gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b531-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="3b531-108">Configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b531-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="3b531-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3b531-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3b531-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3b531-110">What you will learn</span></span>

<span data-ttu-id="3b531-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="3b531-111">In this article, you will learn:</span></span>

- <span data-ttu-id="3b531-112">Informatie over het configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b531-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3b531-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3b531-113">What you need</span></span>

<span data-ttu-id="3b531-114">U moet hebt voltooid</span><span class="sxs-lookup"><span data-stu-id="3b531-114">You must have successfully completed</span></span>

- [<span data-ttu-id="3b531-115">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="3b531-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="3b531-116">Kloon de opslagplaats voorbeeld met de hostcomputer</span><span class="sxs-lookup"><span data-stu-id="3b531-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="3b531-117">De voorbeeld-opslagplaats klonen, moet u deze stappen volgen op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="3b531-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3b531-118">Open een opdrachtprompt in Windows of een terminal in Mac OS of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3b531-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="3b531-119">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="3b531-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="3b531-120">Het gesimuleerde apparaat en uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="3b531-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="3b531-121">Open het configuratiebestand `config.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b531-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="3b531-122">Vervang `"has_sensortag": true` met`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="3b531-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configuratie hebt u niet een TI SensorTag-apparaat](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="3b531-124">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3b531-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="3b531-125">Open `config-gateway.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b531-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="3b531-126">Zoek de volgende regel code en vervang `[device hostname or IP address]` met IP-adres of de host-naam van de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="3b531-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="3b531-127">![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="3b531-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="3b531-128">De verbindingsreeks van uw IoT hub logisch apparaat ophalen</span><span class="sxs-lookup"><span data-stu-id="3b531-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="3b531-129">Als u de verbindingsreeks voor Azure IoT hub van het logische apparaat, voer de volgende opdracht op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="3b531-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="3b531-130">`{IoT hub name}`is de naam van de IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3b531-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="3b531-131">Iot-gateway gebruiken als de waarde van `{resource group name}` en mydevice gebruiken als de waarde van `{device id}` als u de waarde in les 2 is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3b531-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="3b531-132">Configureren van de voorbeeldtoepassing gesimuleerd apparaat cloud uploaden</span><span class="sxs-lookup"><span data-stu-id="3b531-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="3b531-133">Configureren en uitvoeren van de voorbeeldtoepassing gesimuleerd apparaat cloud uploaden, als volgt te werk op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="3b531-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3b531-134">Open `config-sensortag.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b531-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="3b531-136">Controleer de volgende vervangingen in de code:</span><span class="sxs-lookup"><span data-stu-id="3b531-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="3b531-137">Vervang `[IoT hub name]` met de naam van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3b531-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="3b531-138">Vervang `[IoT device connection string]` met de verbindingsreeks van uw IoT hub logisch apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b531-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="3b531-139">Voer de toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="3b531-139">Run the application.</span></span>

   <span data-ttu-id="3b531-140">Implementeren en uitvoeren van de toepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b531-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="3b531-141">Controleer of de toepassing voorbeeld werkt</span><span class="sxs-lookup"><span data-stu-id="3b531-141">Verify the sample application works</span></span>

<span data-ttu-id="3b531-142">U ziet nu de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3b531-142">You should now see output like the following:</span></span>

![de toepassing voorbeelduitvoer gesimuleerd apparaat](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="3b531-144">De toepassing verzendt temperatuur gegevens naar uw IoT-hub 40 seconden duurt.</span><span class="sxs-lookup"><span data-stu-id="3b531-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="3b531-145">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="3b531-145">Summary</span></span>

<span data-ttu-id="3b531-146">U hebt is geconfigureerd en uitvoeren van de voorbeeldtoepassing van gesimuleerd apparaat cloud uploaden die gegevens naar uw IoT-hub met gesimuleerde apparaat verzendt.</span><span class="sxs-lookup"><span data-stu-id="3b531-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b531-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b531-147">Next steps</span></span>
[<span data-ttu-id="3b531-148">Berichten van de IoT-hub lezen</span><span class="sxs-lookup"><span data-stu-id="3b531-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)