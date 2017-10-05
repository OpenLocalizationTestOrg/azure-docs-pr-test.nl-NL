---
title: 'Connect Intel Edison (C) naar Azure IoT - les 4: berichten ontvangen | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Edison en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten naar Edison uit uw iothub de LED knipperen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b7de7a8b53cdb1d7c2560225fce9166e555e5123
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="bfffe-105">Voer een voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="bfffe-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="bfffe-106">In dit artikel hebt implementeren u een voorbeeld van toepassing op Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="bfffe-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="bfffe-107">De voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="bfffe-108">U kunt ook een taak gulp uitvoeren op uw computer om berichten te verzenden naar Edison uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="bfffe-109">Wanneer de voorbeeldtoepassing de berichten ontvangt, wordt de LED knippert.</span><span class="sxs-lookup"><span data-stu-id="bfffe-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="bfffe-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bfffe-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bfffe-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bfffe-111">What you will do</span></span>
* <span data-ttu-id="bfffe-112">Verbinding maken met de voorbeeldtoepassing met uw iothub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="bfffe-113">Implementeren en uitvoeren van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="bfffe-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="bfffe-114">Berichten verzenden van uw IoT-hub naar Edison de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="bfffe-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bfffe-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bfffe-115">What you will learn</span></span>
<span data-ttu-id="bfffe-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="bfffe-116">In this article, you will learn:</span></span>
* <span data-ttu-id="bfffe-117">Het bewaken van inkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="bfffe-118">Het verzenden van cloud naar apparaat-berichten uit uw IoT-hub aan Edison.</span><span class="sxs-lookup"><span data-stu-id="bfffe-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bfffe-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bfffe-119">What you need</span></span>
* <span data-ttu-id="bfffe-120">Intel Edison ingesteld voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="bfffe-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="bfffe-121">Zie voor meer informatie over het instellen van Edison, [configureren van uw apparaat][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="bfffe-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="bfffe-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bfffe-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="bfffe-123">Zie voor meer informatie over het maken van uw IoT-hub, [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="bfffe-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="bfffe-124">Verbinding maken met de voorbeeldtoepassing met uw iothub</span><span class="sxs-lookup"><span data-stu-id="bfffe-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="bfffe-125">Zorg ervoor dat u in de map opslagplaats `iot-hub-c-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="bfffe-125">Make sure that you're in the repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="bfffe-126">De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bfffe-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="bfffe-127">Het bestand in de `app` submap is het belangrijkste bronbestand met de code voor het bewaken van binnenkomende berichten uit iothub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="bfffe-128">De `blinkLED` functie de LED knippert.</span><span class="sxs-lookup"><span data-stu-id="bfffe-128">The `blinkLED` function blinks the LED.</span></span>

   ![Structuur van de opslagplaats in de voorbeeldtoepassing][repo-structure]
2. <span data-ttu-id="bfffe-130">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bfffe-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="bfffe-131">Als u de stappen in voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle configuraties worden overgenomen, zodat u kunt de stap overslaan voor de taak van het implementeren en uitvoeren van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="bfffe-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="bfffe-132">Als u de stappen in voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u Vervang de tijdelijke aanduidingen in de `config-edison.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="bfffe-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="bfffe-133">De `config-edison.json` bestand bevindt zich in de submap van de basismap.</span><span class="sxs-lookup"><span data-stu-id="bfffe-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Inhoud van het bestand config edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="bfffe-135">Vervang **[apparaat-hostnaam of IP-adres]** met het apparaat IP-adres dat u naar beneden gemarkeerd wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bfffe-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="bfffe-136">Vervang **[apparaat-verbindingsreeks IoT]** met de verbindingsreeks voor apparaten die u door het uitvoeren van de `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="bfffe-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="bfffe-137">Vervang **[IoT hub verbindingsreeks]** met de verbindingsreeks voor IoT-hub die u door het uitvoeren van de `az iot hub show-connection-string --name {my hub name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="bfffe-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bfffe-138">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="bfffe-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="bfffe-139">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="bfffe-139">Deploy and run the sample application</span></span>
<span data-ttu-id="bfffe-140">Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bfffe-140">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="bfffe-141">De opdracht gulp implementeert de voorbeeldtoepassing voor Edison.</span><span class="sxs-lookup"><span data-stu-id="bfffe-141">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="bfffe-142">Vervolgens wordt de toepassing uitgevoerd op Edison en een afzonderlijke taak op de hostcomputer Edison 20 knipperen berichten verzenden van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-142">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="bfffe-143">Na de voorbeeldtoepassing wordt uitgevoerd, start het luisteren naar berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfffe-143">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="bfffe-144">Ondertussen verzendt de taak gulp aantal 'knipperen' e-mailberichten van uw IoT-hub naar Edison.</span><span class="sxs-lookup"><span data-stu-id="bfffe-144">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="bfffe-145">Voor elk bericht knipperen die Edison ontvangt, de voorbeeldtoepassing roept de `blinkLED` functie de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="bfffe-145">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="bfffe-146">U ziet de LED knipperen elke twee seconden als de taak gulp 20 berichten uit uw IoT-hub naar Edison verzendt.</span><span class="sxs-lookup"><span data-stu-id="bfffe-146">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="bfffe-147">Het laatste bestand is een 'stop'-bericht dat Hiermee stopt u de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bfffe-147">The last one is a "stop" message that stops the application from running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="bfffe-149">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bfffe-149">Summary</span></span>
<span data-ttu-id="bfffe-150">U hebt berichten verzonden van uw IoT-hub naar Edison de LED knipperen.</span><span class="sxs-lookup"><span data-stu-id="bfffe-150">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="bfffe-151">De volgende taak is optioneel: de aan- en uitgeschakeld gedrag van de LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bfffe-151">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfffe-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfffe-152">Next steps</span></span>
<span data-ttu-id="bfffe-153">[De on- en uitgeschakeld gedrag van de LED wijzigen][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="bfffe-153">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md