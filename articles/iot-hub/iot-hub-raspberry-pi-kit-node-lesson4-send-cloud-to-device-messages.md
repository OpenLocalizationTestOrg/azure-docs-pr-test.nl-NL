---
featureFlags: usabilla
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: Hallo-voorbeeldtoepassing wordt uitgevoerd op Pi en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooPi van uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud toodevice, het bericht uit de cloud
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
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="6d52a-105">Hallo voorbeeld tooreceive cloud-naar-apparaat toepassingsberichten uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6d52a-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="6d52a-106">In dit artikel hebt implementeren u een voorbeeld van toepassing op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="6d52a-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="6d52a-107">Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d52a-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="6d52a-108">U ook uitvoeren een gulp taak op uw computer toosend berichten tooPi uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d52a-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="6d52a-109">Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="6d52a-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="6d52a-110">Als u problemen hebt, zoeken naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6d52a-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6d52a-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="6d52a-111">What you will do</span></span>
* <span data-ttu-id="6d52a-112">Sluit Hallo voorbeeld toepassing tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="6d52a-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="6d52a-113">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d52a-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="6d52a-114">Berichten verzenden van uw IoT hub tooPi tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="6d52a-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6d52a-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="6d52a-115">What you will learn</span></span>
<span data-ttu-id="6d52a-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="6d52a-116">In this article, you will learn:</span></span>
* <span data-ttu-id="6d52a-117">Hoe toomonitor inkomende berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6d52a-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="6d52a-118">Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooPi.</span><span class="sxs-lookup"><span data-stu-id="6d52a-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6d52a-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="6d52a-119">What you need</span></span>
* <span data-ttu-id="6d52a-120">Raspberry Pi 3, die zijn ingesteld voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="6d52a-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="6d52a-121">hoe tooset van Pi, Zie toolearn [configureren van uw apparaat](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="6d52a-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="6d52a-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d52a-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="6d52a-123">toolearn hoe toocreate uw IoT-hub Zie [uw IoT-hub maken en registreren van frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6d52a-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="6d52a-124">Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6d52a-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="6d52a-125">Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="6d52a-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="6d52a-126">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="6d52a-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="6d52a-127">Kennisgeving Hallo `app.js` bestand in Hallo `app` submap.</span><span class="sxs-lookup"><span data-stu-id="6d52a-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="6d52a-128">Hallo `app.js` bestand is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="6d52a-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="6d52a-129">Hallo `blinkLED` functie Hallo LED knippert.</span><span class="sxs-lookup"><span data-stu-id="6d52a-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="6d52a-131">Hallo-configuratiebestand met behulp van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="6d52a-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="6d52a-132">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt toohello taak implementeren en uitvoeren van de voorbeeldtoepassing Hallo overslaan.</span><span class="sxs-lookup"><span data-stu-id="6d52a-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="6d52a-133">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-raspberrypi.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="6d52a-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="6d52a-134">Hallo `config-raspberrypi.json` bestand bevindt zich in de submap Hallo van de basismap.</span><span class="sxs-lookup"><span data-stu-id="6d52a-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Inhoud van Hallo config raspberrypi.json bestand](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="6d52a-136">Vervang **[apparaat-hostnaam of IP-adres]** met Hallo IP-adres van Pi of Hallo hostnaam die u door het uitvoeren van Hallo `devdisco list --eth` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6d52a-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="6d52a-137">Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6d52a-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="6d52a-138">Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6d52a-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="6d52a-139">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="6d52a-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="6d52a-140">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="6d52a-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="6d52a-141">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6d52a-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="6d52a-142">Hallo opdracht implementeert Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="6d52a-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="6d52a-143">Vervolgens het Hallo toepassing uitvoert op een afzonderlijke taak op de host en Pi computer toosend 20 knipperen berichten tooPi uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d52a-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="6d52a-144">Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d52a-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="6d52a-145">Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooPi.</span><span class="sxs-lookup"><span data-stu-id="6d52a-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="6d52a-146">Voor elk bericht knipperen die Pi ontvangt, roept de voorbeeldtoepassing Hallo Hallo `blinkLED` functie tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="6d52a-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="6d52a-147">U ziet Hallo LED knipperen elke twee seconden als Hallo taak verzendt 20 berichten van uw IoT hub tooPi gulp.</span><span class="sxs-lookup"><span data-stu-id="6d52a-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="6d52a-148">Hallo laatste is een een 'stop' weergegeven waarin wordt uitgelegd Hallo toepassing toostop uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d52a-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="6d52a-150">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6d52a-150">Summary</span></span>
<span data-ttu-id="6d52a-151">U hebt berichten uit uw IoT hub tooPi tooblink Hallo LED verzonden.</span><span class="sxs-lookup"><span data-stu-id="6d52a-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="6d52a-152">de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d52a-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d52a-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d52a-153">Next steps</span></span>
[<span data-ttu-id="6d52a-154">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="6d52a-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

