---
featureFlags: usabilla
title: 'Raspberry Pi (knooppunt) verbinden met Azure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: De voorbeeldtoepassing wordt uitgevoerd op Pi en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten naar Pi uit uw iothub de LED knipperen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud naar apparaat, het bericht uit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="f5922-105">Uitvoeren van de voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="f5922-105">Run the sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="f5922-106">In dit artikel hebt implementeren u een voorbeeld van toepassing op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f5922-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="f5922-107">De voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f5922-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="f5922-108">U kunt ook een taak gulp uitvoeren op uw computer om berichten te verzenden naar Pi uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f5922-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="f5922-109">Wanneer de voorbeeldtoepassing de berichten ontvangt, wordt de LED knippert.</span><span class="sxs-lookup"><span data-stu-id="f5922-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="f5922-110">Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f5922-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f5922-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f5922-111">What you will do</span></span>
* <span data-ttu-id="f5922-112">Verbinding maken met de voorbeeldtoepassing met uw iothub.</span><span class="sxs-lookup"><span data-stu-id="f5922-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="f5922-113">Implementeren en uitvoeren van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f5922-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="f5922-114">Berichten verzenden van uw IoT-hub tot Pi de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="f5922-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f5922-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f5922-115">What you will learn</span></span>
<span data-ttu-id="f5922-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="f5922-116">In this article, you will learn:</span></span>
* <span data-ttu-id="f5922-117">Het bewaken van inkomende berichten van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="f5922-117">How to monitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="f5922-118">Het cloud-naar-apparaat-berichten verzenden vanuit uw IoT-hub tot Pi.</span><span class="sxs-lookup"><span data-stu-id="f5922-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5922-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="f5922-119">What you need</span></span>
* <span data-ttu-id="f5922-120">Raspberry Pi 3, die zijn ingesteld voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="f5922-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="f5922-121">Zie voor meer informatie over het instellen van Pi, [configureren van uw apparaat](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="f5922-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="f5922-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f5922-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="f5922-123">Zie voor meer informatie over het maken van uw IoT-hub, [uw IoT-hub maken en registreren van frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f5922-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="f5922-124">Verbinding maken met de voorbeeldtoepassing met uw iothub</span><span class="sxs-lookup"><span data-stu-id="f5922-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="f5922-125">Zorg ervoor dat u in de map opslagplaats `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="f5922-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="f5922-126">De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f5922-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="f5922-127">U ziet de `app.js` bestand de `app` submap.</span><span class="sxs-lookup"><span data-stu-id="f5922-127">Notice the `app.js` file in the `app` subfolder.</span></span> <span data-ttu-id="f5922-128">De `app.js` bestand is het belangrijkste bronbestand met de code voor het bewaken van binnenkomende berichten uit iothub.</span><span class="sxs-lookup"><span data-stu-id="f5922-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="f5922-129">De `blinkLED` functie de LED knippert.</span><span class="sxs-lookup"><span data-stu-id="f5922-129">The `blinkLED` function blinks the LED.</span></span>
   
   ![Structuur van de opslagplaats in de voorbeeldtoepassing](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="f5922-131">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f5922-131">Initialize the configuration file by using the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="f5922-132">Als u de stappen in voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op deze computer, alle configuraties worden overgenomen, zodat u kunt doorgaan met de taak van het implementeren en uitvoeren van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f5922-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span></span> <span data-ttu-id="f5922-133">Als u de stappen in voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op een andere computer, moet u Vervang de tijdelijke aanduidingen in de `config-raspberrypi.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="f5922-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="f5922-134">De `config-raspberrypi.json` bestand bevindt zich in de submap van de basismap.</span><span class="sxs-lookup"><span data-stu-id="f5922-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>
   
   ![Inhoud van het bestand config raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="f5922-136">Vervang **[apparaat-hostnaam of IP-adres]** met het IP-adres van Pi of de hostnaam die u door het uitvoeren van de `devdisco list --eth` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f5922-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="f5922-137">Vervang **[apparaat-verbindingsreeks IoT]** met de verbindingsreeks voor apparaten die u door het uitvoeren van de `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f5922-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="f5922-138">Vervang **[IoT hub verbindingsreeks]** met de verbindingsreeks voor IoT-hub die u door het uitvoeren van de `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f5922-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="f5922-139">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="f5922-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f5922-140">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="f5922-140">Deploy and run the sample application</span></span>
<span data-ttu-id="f5922-141">Implementeren en uitvoeren van de voorbeeldtoepassing op Pi met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f5922-141">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="f5922-142">De opdracht implementeert de voorbeeldtoepassing tot Pi.</span><span class="sxs-lookup"><span data-stu-id="f5922-142">The command deploys the sample application to Pi.</span></span> <span data-ttu-id="f5922-143">Vervolgens wordt de toepassing uitgevoerd op Pi en een afzonderlijke taak op de hostcomputer Pi 20 knipperen berichten verzenden van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f5922-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="f5922-144">Na de voorbeeldtoepassing wordt uitgevoerd, start het luisteren naar berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f5922-144">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="f5922-145">De taak gulp verzendt ondertussen diverse 'knipperen'-berichten van uw IoT-hub tot Pi.</span><span class="sxs-lookup"><span data-stu-id="f5922-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="f5922-146">Voor elk bericht knipperen die Pi ontvangt, de voorbeeldtoepassing roept de `blinkLED` functie de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="f5922-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="f5922-147">U ziet de LED knipperen elke twee seconden als de taak gulp 20 berichten uit uw iothub tot Pi verzendt.</span><span class="sxs-lookup"><span data-stu-id="f5922-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="f5922-148">Het laatste bestand is een 'stop' weergegeven waarin wordt gemeld de toepassing dat meer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f5922-148">The last one is a "stop" message that tells the application to stop running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="f5922-150">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f5922-150">Summary</span></span>
<span data-ttu-id="f5922-151">U hebt verzonden berichten uit uw IoT-hub tot Pi de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="f5922-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="f5922-152">De volgende taak is optioneel: de aan- en uitgeschakeld gedrag van de LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f5922-152">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5922-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5922-153">Next steps</span></span>
[<span data-ttu-id="f5922-154">De on- en uitgeschakeld gedrag van de LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="f5922-154">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

