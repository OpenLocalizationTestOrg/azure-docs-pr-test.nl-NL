---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een Aanmeldingsprompt toepassing tooreceive voorbeeldgegevens uit SensorTag uitschakelen en uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: uitschakelen app, de app controleren sensor, gegevensverzameling sensor, gegevens van sensoren, sensor gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="d0875-104">Configureren en uitvoeren van een voorbeeldtoepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d0875-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d0875-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d0875-105">What you will do</span></span>

- <span data-ttu-id="d0875-106">Kloon Hallo voorbeeld opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d0875-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="d0875-107">Hallo-connectiviteit tussen SensorTag en Intel NUC instellen.</span><span class="sxs-lookup"><span data-stu-id="d0875-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="d0875-108">Gebruik hello Azure CLI tooget uw iothub en SensorTag-informatie voor een voorbeeldtoepassing uitschakelen (Bluetooth lage energie).</span><span class="sxs-lookup"><span data-stu-id="d0875-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="d0875-109">Configureren en Hallo uitschakelen voorbeeldtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0875-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="d0875-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d0875-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d0875-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d0875-111">What you will learn</span></span>

<span data-ttu-id="d0875-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="d0875-112">In this article, you will learn:</span></span>

- <span data-ttu-id="d0875-113">Hoe tooconfigure en Voer Hallo uitschakelen voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d0875-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d0875-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d0875-114">What you need</span></span>

<span data-ttu-id="d0875-115">U moet hebt voltooid</span><span class="sxs-lookup"><span data-stu-id="d0875-115">You must have successfully completed</span></span>

- [<span data-ttu-id="d0875-116">Het maken van een IoT-hub en SensorTag registreren</span><span class="sxs-lookup"><span data-stu-id="d0875-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="d0875-117">Kloon Hallo voorbeeld opslagplaats toohello hostcomputer</span><span class="sxs-lookup"><span data-stu-id="d0875-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="d0875-118">tooclone hello voorbeeld opslagplaats als volgt te werk op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="d0875-119">Open een opdrachtpromptvenster in Windows of een terminal in Mac OS of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d0875-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="d0875-120">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d0875-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="d0875-121">Hallo-connectiviteit tussen SensorTag en Intel NUC instellen</span><span class="sxs-lookup"><span data-stu-id="d0875-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="d0875-122">tooset hello connectiviteit, als volgt te werk op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="d0875-123">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="d0875-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="d0875-124">Open `config-gateway.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d0875-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="d0875-125">Hallo volgende coderegel zoeken en vervangen `[device hostname or IP address]` met Hallo IP-adres of de hostnaam naam van Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d0875-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="d0875-126">![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="d0875-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="d0875-127">Help-hulpprogramma's installeren op Intel NUC door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="d0875-128">Schakel SensorTag door te drukken Hallo / uit-knop als Hallo volgende afbeelding en Hallo die groene LED moet knipperen.</span><span class="sxs-lookup"><span data-stu-id="d0875-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![Sensor Tag inschakelen](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="d0875-130">SensorTag-apparaten door het uitvoeren van de volgende opdrachten Hallo scannen:</span><span class="sxs-lookup"><span data-stu-id="d0875-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="d0875-131">Hallo-connectiviteit tussen Hallo SensorTag en Intel NUC testen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="d0875-132">Vervang `{mac address}` Hello MAC-adres dat u hebt verkregen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0875-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="d0875-133">De verbindingsreeks Hallo van SensorTag ophalen</span><span class="sxs-lookup"><span data-stu-id="d0875-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="d0875-134">tooget hello Azure IoT hub-verbindingsreeks van SensorTag, uitvoeren van de volgende opdracht op de hostcomputer Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="d0875-135">`{IoT hub name}`is Hallo naam IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0875-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="d0875-136">Iot-gateway gebruiken als de waarde van Hallo `{resource group name}` en mydevice gebruiken als Hallo-waarde van `{device id}` als u Hallo-waarde in les 2 niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d0875-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="d0875-137">Hallo uitschakelen voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="d0875-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="d0875-138">tooconfigure en Voer Hallo uitschakelen voorbeeldtoepassing, volg deze stappen op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="d0875-139">Open `config-sensortag.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d0875-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="d0875-141">Controleer Hallo vervangingen in Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0875-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="d0875-142">Vervang `[IoT hub name]` met Hallo naam IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0875-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="d0875-143">Vervang `[IoT device connection string]` met de verbindingsreeks Hallo van SensorTag die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="d0875-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="d0875-144">Vervang `[device_mac_address]` Hello MAC-adres van Hallo SensorTag die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="d0875-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="d0875-145">Hallo uitschakelen voorbeeldtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0875-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="d0875-146">toorun hello voorbeeldtoepassing uitschakelen als volgt te werk op de hostcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="d0875-147">SensorTag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0875-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="d0875-148">Implementeren en uitvoeren van de voorbeeldtoepassing voor Hallo uitschakelen op Intel NUC door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0875-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="d0875-149">Controleer of Hallo uitschakelen voorbeeldtoepassing werkt</span><span class="sxs-lookup"><span data-stu-id="d0875-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="d0875-150">U ziet nu Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d0875-150">You should now see an output like hello following:</span></span>

![De toepassing voorbeelduitvoer uitschakelen](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="d0875-152">Hallo-voorbeeldtoepassing blijft temperatuur gegevens verzamelen en deze tooyour iothub heeft verzonden.</span><span class="sxs-lookup"><span data-stu-id="d0875-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="d0875-153">Hallo-voorbeeldtoepassing wordt automatisch beëindigd na het verzenden van 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="d0875-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="d0875-154">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d0875-154">Summary</span></span>

<span data-ttu-id="d0875-155">U hebt met succes Hallo connectiviteit tussen SensorTag en Intel NUC instellen en uitvoeren van een voorbeeldtoepassing uitschakelen die worden verzameld en verzonden gegevens uit SensorTag tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="d0875-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="d0875-156">U bent klaar toolearn hoe tooverify die uw IoT-hub heeft ontvangen gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0875-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0875-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0875-157">Next steps</span></span>
[<span data-ttu-id="d0875-158">Berichten van de IoT-hub lezen</span><span class="sxs-lookup"><span data-stu-id="d0875-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)