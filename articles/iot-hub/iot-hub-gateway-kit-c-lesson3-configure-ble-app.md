---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een voorbeeldtoepassing uitschakelen gegevens ontvangt uit SensorTag uitschakelen en uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: uitschakelen app, de app controleren sensor, gegevensverzameling sensor, gegevens van sensoren sensorgegevens in de cloud
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="9a168-104">Configureren en uitvoeren van een voorbeeldtoepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="9a168-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9a168-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="9a168-105">What you will do</span></span>

- <span data-ttu-id="9a168-106">Kloon de opslagplaats voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9a168-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="9a168-107">De verbinding tussen de SensorTag en Intel NUC instellen.</span><span class="sxs-lookup"><span data-stu-id="9a168-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="9a168-108">De Azure CLI gebruiken om uw IoT-hub en SensorTag-informatie voor een voorbeeldtoepassing uitschakelen (Bluetooth lage energie).</span><span class="sxs-lookup"><span data-stu-id="9a168-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="9a168-109">Configureren en uitvoeren van de voorbeeldtoepassing uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a168-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="9a168-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9a168-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9a168-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="9a168-111">What you will learn</span></span>

<span data-ttu-id="9a168-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="9a168-112">In this article, you will learn:</span></span>

- <span data-ttu-id="9a168-113">Informatie over het configureren en uitvoeren van de voorbeeldtoepassing uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a168-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9a168-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="9a168-114">What you need</span></span>

<span data-ttu-id="9a168-115">U moet hebt voltooid</span><span class="sxs-lookup"><span data-stu-id="9a168-115">You must have successfully completed</span></span>

- [<span data-ttu-id="9a168-116">Het maken van een IoT-hub en SensorTag registreren</span><span class="sxs-lookup"><span data-stu-id="9a168-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="9a168-117">Kloon de opslagplaats voorbeeld met de hostcomputer</span><span class="sxs-lookup"><span data-stu-id="9a168-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="9a168-118">De voorbeeld-opslagplaats klonen, moet u deze stappen volgen op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="9a168-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="9a168-119">Open een opdrachtpromptvenster in Windows of een terminal in Mac OS of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9a168-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="9a168-120">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="9a168-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="9a168-121">De verbinding tussen de SensorTag en Intel NUC instellen</span><span class="sxs-lookup"><span data-stu-id="9a168-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="9a168-122">Volg deze stappen op de host voordat u de connectiviteit kunt instellen:</span><span class="sxs-lookup"><span data-stu-id="9a168-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="9a168-123">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9a168-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="9a168-124">Open `config-gateway.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9a168-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="9a168-125">Zoek de volgende regel code en vervang `[device hostname or IP address]` met de naam voor IP-adres of de hostnaam van Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="9a168-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="9a168-126">![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="9a168-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="9a168-127">Help-hulpprogramma's installeren op Intel NUC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9a168-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="9a168-128">Schakel SensorTag door op de knop power als in de volgende afbeelding en de groene LED moet knipperen.</span><span class="sxs-lookup"><span data-stu-id="9a168-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![Sensor Tag inschakelen](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="9a168-130">Scannen SensorTag-apparaten met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9a168-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="9a168-131">Test de connectiviteit tussen de SensorTag en Intel NUC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9a168-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="9a168-132">Vervang `{mac address}` met de MAC-adres dat u hebt verkregen in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="9a168-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="9a168-133">De verbindingsreeks van SensorTag ophalen</span><span class="sxs-lookup"><span data-stu-id="9a168-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="9a168-134">Als u de verbindingsreeks voor Azure IoT hub van SensorTag, voer de volgende opdracht op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="9a168-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="9a168-135">`{IoT hub name}`is de naam van de IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a168-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="9a168-136">Iot-gateway gebruiken als de waarde van `{resource group name}` en mydevice gebruiken als de waarde van `{device id}` als u de waarde in les 2 is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9a168-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="9a168-137">Configureren van de voorbeeldtoepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="9a168-137">Configure the BLE sample application</span></span>

<span data-ttu-id="9a168-138">Als u wilt configureren en uitvoeren van de voorbeeldtoepassing uitschakelen, moet u deze stappen volgen op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="9a168-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="9a168-139">Open `config-sensortag.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9a168-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="9a168-141">Controleer de volgende vervangingen in de code:</span><span class="sxs-lookup"><span data-stu-id="9a168-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="9a168-142">Vervang `[IoT hub name]` met de naam van de IoT-hub die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a168-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="9a168-143">Vervang `[IoT device connection string]` met de verbindingsreeks van SensorTag die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="9a168-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="9a168-144">Vervang `[device_mac_address]` met het MAC-adres van de SensorTag die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="9a168-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="9a168-145">Voer de voorbeeldtoepassing uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a168-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="9a168-146">Voor het uitvoeren van de voorbeeldtoepassing uitschakelen, moet u deze stappen volgen op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="9a168-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="9a168-147">SensorTag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a168-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="9a168-148">Implementeren en uitvoeren van de voorbeeldtoepassing uitschakelen op Intel NUC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9a168-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="9a168-149">Controleer of de voorbeeldtoepassing uitschakelen werkt</span><span class="sxs-lookup"><span data-stu-id="9a168-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="9a168-150">U ziet nu de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9a168-150">You should now see an output like the following:</span></span>

![De toepassing voorbeelduitvoer uitschakelen](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="9a168-152">De voorbeeldtoepassing houdt temperatuur gegevens worden verzameld en verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="9a168-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="9a168-153">De voorbeeldtoepassing wordt automatisch beëindigd na het verzenden van 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="9a168-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="9a168-154">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9a168-154">Summary</span></span>

<span data-ttu-id="9a168-155">U hebt is de verbinding tussen de SensorTag en Intel NUC instellen en uitvoeren van een voorbeeldtoepassing uitschakelen die worden verzameld en gegevens van SensorTag naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="9a168-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="9a168-156">U kunt meer informatie over het controleren of uw IoT-hub heeft de gegevens worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="9a168-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a168-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a168-157">Next steps</span></span>
[<span data-ttu-id="9a168-158">Berichten van de IoT-hub lezen</span><span class="sxs-lookup"><span data-stu-id="9a168-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)