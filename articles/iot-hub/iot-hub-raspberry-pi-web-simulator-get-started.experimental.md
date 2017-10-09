---
title: aaaSimulated frambozen Pi toocloud (Node.js) - verbinding frambozen Pi web simulator tooAzure IoT Hub | Microsoft Docs
description: Verbinding maken met tooAzure simulator web Pi frambozen IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Raspberry pi simulator azure iot raspberry pi raspberry pi iothub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="b43f1-104">Verbinding maken met frambozen Pi online simulator tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="b43f1-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="b43f1-105">In deze zelfstudie maakt eerst u learning Hallo basisbeginselen van het werken met frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="b43f1-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="b43f1-106">U leert vervolgens hoe tooseamlessly Hallo Pi simulator toohello cloud verbinding via [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="b43f1-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="b43f1-107">Als u fysieke apparaten hebt, gaat u naar [verbinding frambozen Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="b43f1-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="b43f1-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="b43f1-108">What you do</span></span>

* <span data-ttu-id="b43f1-109">Hallo basisbegrippen van frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="b43f1-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="b43f1-110">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="b43f1-110">Create an IoT hub.</span></span>
* <span data-ttu-id="b43f1-111">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b43f1-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="b43f1-112">Een voorbeeld van een toepassing uitvoeren op Pi toosend gesimuleerde sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="b43f1-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="b43f1-113">Verbinding maken met gesimuleerde frambozen Pi tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="b43f1-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="b43f1-114">Voer vervolgens een voorbeeldtoepassing met Hallo simulator toogenerate sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="b43f1-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="b43f1-115">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="b43f1-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b43f1-116">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="b43f1-116">What you learn</span></span>

* <span data-ttu-id="b43f1-117">Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="b43f1-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="b43f1-118">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="b43f1-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b43f1-119">Hoe toowork met frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="b43f1-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="b43f1-120">Hoe toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b43f1-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="b43f1-121">Overzicht van frambozen Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="b43f1-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="b43f1-122">Klik op Hallo knop toolaunch frambozen Pi online simulator.</span><span class="sxs-lookup"><span data-stu-id="b43f1-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="b43f1-123">Starten van de simulator frambozen Pi</span><span class="sxs-lookup"><span data-stu-id="b43f1-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="b43f1-124">Er zijn drie gebieden in Hallo web simulator.</span><span class="sxs-lookup"><span data-stu-id="b43f1-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="b43f1-125">Assemblagegebied - Hallo standaard circuit is dat een Pi verbinding met een sensor BME280 en een LED maakt.</span><span class="sxs-lookup"><span data-stu-id="b43f1-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="b43f1-126">Hallo-gebied is vergrendeld in de preview-versie dus momenteel niet aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b43f1-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="b43f1-127">Het coderen van gebied - een online code-editor voor toocode met frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="b43f1-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="b43f1-128">Standaard-voorbeeldtoepassing Hallo toocollect sensorgegevens helpt van BME280 sensor en tooyour Azure IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="b43f1-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="b43f1-129">Hallo-toepassing is volledig compatibel is met echte Pi-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b43f1-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="b43f1-130">Geïntegreerde consolevenster - het Hallo-uitvoer van uw code bevat.</span><span class="sxs-lookup"><span data-stu-id="b43f1-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="b43f1-131">Er zijn drie knoppen Hallo bovenaan dit venster in.</span><span class="sxs-lookup"><span data-stu-id="b43f1-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="b43f1-132">**Voer** -Hallo toepassing uitvoert in Hallo gebied coderen.</span><span class="sxs-lookup"><span data-stu-id="b43f1-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="b43f1-133">**Opnieuw instellen** -Reset Hallo gebied toohello standaard voorbeeldtoepassing coderen.</span><span class="sxs-lookup"><span data-stu-id="b43f1-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="b43f1-134">**Vouw/uitvouwen** - op Hallo rechts naast er zich een knop voor u toofold/uitbreiden Hallo consolevenster.</span><span class="sxs-lookup"><span data-stu-id="b43f1-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="b43f1-135">Hallo frambozen Pi web simulator is nu beschikbaar in de preview-versie.</span><span class="sxs-lookup"><span data-stu-id="b43f1-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="b43f1-136">Willen we graag toohear uw stem in Hallo [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="b43f1-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="b43f1-137">Hallo broncode is openbare op [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="b43f1-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Overzicht van online simulator Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="b43f1-139">Een voorbeeld van een toepassing uitvoeren op Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="b43f1-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="b43f1-140">Controleer of u bezig bent met Hallo standaard voorbeeldtoepassing in het gebied coderen.</span><span class="sxs-lookup"><span data-stu-id="b43f1-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="b43f1-141">Hallo-tijdelijke aanduiding in regel 15 vervangen door hello Azure IoT hub apparaat-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="b43f1-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="b43f1-142">![Hallo apparaat verbindingsreeks vervangen](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="b43f1-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="b43f1-143">Klik op **uitvoeren** of type `npm start` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b43f1-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="b43f1-144">U ziet Hallo na de uitvoer die toont Hallo sensorgegevens en Hallo-berichten die worden verzonden tooyour IoT-hub ![uitvoer - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="b43f1-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="b43f1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b43f1-145">Next steps</span></span>

<span data-ttu-id="b43f1-146">U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b43f1-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
