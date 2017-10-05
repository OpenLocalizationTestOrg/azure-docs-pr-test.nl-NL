---
title: Gesimuleerde frambozen Pi naar cloud (Node.js) - web-simulator frambozen Pi verbinding maken met Azure IoT Hub | Microsoft Docs
description: Frambozen Pi web simulator verbinding met Azure IoT Hub voor frambozen Pi gegevens verzenden naar de Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Raspberry pi simulator, azure iot raspberry pi, raspberry pi iothub, raspberry pi verzenden gegevens naar de cloud, raspberry pi naar cloud
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 3b80bf35d6af91d5bdb196d97668dc0f837b92cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="cdf51-104">Online simulator frambozen Pi verbinden met Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="cdf51-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="cdf51-105">In deze zelfstudie maakt beginnen u door te leren over het werken met frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="cdf51-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="cdf51-106">Vervolgens leert u hoe de simulator Pi naadloos verbinding naar de cloud via [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="cdf51-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="cdf51-107">Als u fysieke apparaten hebt, gaat u naar [frambozen Pi verbinding maken met Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) aan de slag.</span><span class="sxs-lookup"><span data-stu-id="cdf51-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="cdf51-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="cdf51-108">What you do</span></span>

* <span data-ttu-id="cdf51-109">Leer de basisbeginselen van frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="cdf51-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="cdf51-110">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="cdf51-110">Create an IoT hub.</span></span>
* <span data-ttu-id="cdf51-111">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cdf51-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="cdf51-112">Een voorbeeld van een toepassing uitvoeren op Pi gesimuleerde sensorgegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cdf51-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="cdf51-113">Verbinding maken met gesimuleerde frambozen Pi naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="cdf51-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="cdf51-114">Voer vervolgens een voorbeeldtoepassing met de simulator sensorgegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="cdf51-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="cdf51-115">U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cdf51-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cdf51-116">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="cdf51-116">What you learn</span></span>

* <span data-ttu-id="cdf51-117">Het maken van een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="cdf51-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="cdf51-118">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="cdf51-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="cdf51-119">Klik hier voor meer informatie over het werken met frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="cdf51-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="cdf51-120">Hoe sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cdf51-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="cdf51-121">Overzicht van frambozen Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="cdf51-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="cdf51-122">Klik op de knop Start frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="cdf51-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="cdf51-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Starten van de Simulator Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="cdf51-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="cdf51-124">Er zijn drie gebieden in de web-simulator.</span><span class="sxs-lookup"><span data-stu-id="cdf51-124">There are three areas in the web simulator.</span></span>
1. <span data-ttu-id="cdf51-125">Assemblagegebied - het circuit standaard is dat een Pi verbinding met een sensor BME280 en een LED maakt.</span><span class="sxs-lookup"><span data-stu-id="cdf51-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="cdf51-126">Het gebied is vergrendeld in de preview-versie dus momenteel niet aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cdf51-126">The area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="cdf51-127">Het coderen van gebied - een online code-editor voor u code met frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="cdf51-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="cdf51-128">De voorbeeldtoepassing standaard helpt om sensorgegevens te verzamelen van BME280 sensor en verzendt naar uw Azure-IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="cdf51-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="cdf51-129">De toepassing is volledig compatibel is met echte Pi-apparaten.</span><span class="sxs-lookup"><span data-stu-id="cdf51-129">The application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="cdf51-130">Geïntegreerde consolevenster - wordt de uitvoer van uw code.</span><span class="sxs-lookup"><span data-stu-id="cdf51-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="cdf51-131">Er zijn drie knoppen aan de bovenkant van dit venster.</span><span class="sxs-lookup"><span data-stu-id="cdf51-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="cdf51-132">**Voer** -de toepassing uitvoeren in het gebied van programmeren nodig.</span><span class="sxs-lookup"><span data-stu-id="cdf51-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="cdf51-133">**Opnieuw instellen** -opnieuw instellen van het gebied van programmeren nodig tot de voorbeeldtoepassing standaard.</span><span class="sxs-lookup"><span data-stu-id="cdf51-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="cdf51-134">**Vouw/uitvouwen** -aan de rechterkant bevindt zich een knop voor u het consolevenster vouwen/uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="cdf51-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="cdf51-135">De web Pi frambozen simulator is nu beschikbaar in de preview-versie.</span><span class="sxs-lookup"><span data-stu-id="cdf51-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="cdf51-136">Wij willen graag uw horen in de [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="cdf51-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="cdf51-137">De broncode is openbare op [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="cdf51-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Overzicht van online simulator Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="cdf51-139">Een voorbeeld van een toepassing uitvoeren op Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="cdf51-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="cdf51-140">Controleer of u bezig bent met de voorbeeldtoepassing standaard in het coderen van gebied.</span><span class="sxs-lookup"><span data-stu-id="cdf51-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="cdf51-141">Vervang de tijdelijke aanduiding in regel 15 met de verbindingsreeks voor Azure IoT hub-apparaat.</span><span class="sxs-lookup"><span data-stu-id="cdf51-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="cdf51-142">![Vervang de apparaat-verbindingsreeks](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="cdf51-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="cdf51-143">Klik op **uitvoeren** of type `npm start` de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cdf51-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="cdf51-144">U ziet de volgende uitvoer waarin de sensorgegevens en de berichten die worden verzonden naar uw IoT-hub ![uitvoer - sensorgegevens verzonden van frambozen Pi naar uw IoT-hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="cdf51-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="cdf51-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdf51-145">Next steps</span></span>

<span data-ttu-id="cdf51-146">U kunt een voorbeeldtoepassing sensorgegevens verzamelen en verzenden naar uw IoT-hub hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdf51-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
