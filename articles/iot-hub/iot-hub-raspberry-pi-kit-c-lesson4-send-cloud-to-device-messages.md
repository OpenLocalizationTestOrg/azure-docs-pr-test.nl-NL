---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Pi en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooPi van uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: cloud toodevice, het bericht uit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="2baf8-105">Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="2baf8-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="2baf8-106">In dit artikel hebt implementeren u een voorbeeld van toepassing op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2baf8-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="2baf8-107">Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="2baf8-108">U ook uitvoeren een gulp taak op uw computer toosend berichten tooPi uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="2baf8-109">Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="2baf8-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="2baf8-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2baf8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2baf8-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2baf8-111">What you will do</span></span>
* <span data-ttu-id="2baf8-112">Sluit Hallo voorbeeld toepassing tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="2baf8-113">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="2baf8-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="2baf8-114">Berichten verzenden van uw IoT hub tooPi tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="2baf8-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2baf8-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2baf8-115">What you will learn</span></span>
<span data-ttu-id="2baf8-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="2baf8-116">In this article, you will learn:</span></span>
* <span data-ttu-id="2baf8-117">Hoe toomonitor binnenkomende berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="2baf8-118">Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooPi.</span><span class="sxs-lookup"><span data-stu-id="2baf8-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2baf8-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2baf8-119">What you need</span></span>
* <span data-ttu-id="2baf8-120">Raspberry Pi 3, die zijn ingesteld voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="2baf8-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="2baf8-121">hoe tooset van Pi, Zie toolearn [configureren van uw apparaat](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="2baf8-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="2baf8-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2baf8-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="2baf8-123">toolearn hoe toocreate uw IoT-hub Zie [uw IoT-hub maken en registreren van frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2baf8-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="2baf8-124">Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="2baf8-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="2baf8-125">Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="2baf8-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="2baf8-126">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="2baf8-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="2baf8-127">Kennisgeving Hallo `app.c` bestand in Hallo `app` submap.</span><span class="sxs-lookup"><span data-stu-id="2baf8-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="2baf8-128">Hallo `app.c` bestand is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="2baf8-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="2baf8-129">Hallo `blinkLED` functie Hallo LED knippert.</span><span class="sxs-lookup"><span data-stu-id="2baf8-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="2baf8-131">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="2baf8-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="2baf8-132">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt toostep toohello taak implementeren en uitvoeren van de voorbeeldtoepassing Hallo overslaan.</span><span class="sxs-lookup"><span data-stu-id="2baf8-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="2baf8-133">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-raspberrypi.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="2baf8-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="2baf8-134">Hallo `config-raspberrypi.json` bestand bevindt zich in de submap Hallo van de basismap.</span><span class="sxs-lookup"><span data-stu-id="2baf8-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Inhoud van Hallo config raspberrypi.json bestand](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="2baf8-136">Vervang **[apparaat-hostnaam of IP-adres]** met Pi van IP-adres of de hostnaam naam die u door het uitvoeren van Hallo `devdisco list --eth` opdracht.</span><span class="sxs-lookup"><span data-stu-id="2baf8-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="2baf8-137">Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="2baf8-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="2baf8-138">Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="2baf8-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="2baf8-139">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="2baf8-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2baf8-140">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="2baf8-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="2baf8-141">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="2baf8-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="2baf8-142">Hallo gulp opdracht is uitgevoerd Hallo eerst taak install-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2baf8-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="2baf8-143">Vervolgens implementeert het Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="2baf8-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="2baf8-144">Ten slotte op wordt uitgevoerd toepassing hello Pi en een afzonderlijke taak op uw host computer toosend 20 knipperen berichten tooPi uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="2baf8-145">Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2baf8-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="2baf8-146">Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooPi.</span><span class="sxs-lookup"><span data-stu-id="2baf8-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="2baf8-147">Voor elk bericht knipperen die Pi ontvangt, roept de voorbeeldtoepassing Hallo Hallo `blinkLED` functie tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="2baf8-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="2baf8-148">U ziet Hallo LED knipperen elke twee seconden als Hallo taak verzendt 20 berichten van uw IoT hub tooPi gulp.</span><span class="sxs-lookup"><span data-stu-id="2baf8-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="2baf8-149">Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2baf8-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="2baf8-151">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2baf8-151">Summary</span></span>
<span data-ttu-id="2baf8-152">U hebt berichten uit uw IoT hub tooPi tooblink Hallo LED verzonden.</span><span class="sxs-lookup"><span data-stu-id="2baf8-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="2baf8-153">de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2baf8-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2baf8-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2baf8-154">Next steps</span></span>
[<span data-ttu-id="2baf8-155">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="2baf8-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
