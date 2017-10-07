---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 4: berichten ontvangen | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Edison en bewaakt binnenkomende berichten van uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooEdison van uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="62954-105">Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="62954-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="62954-106">In dit artikel hebt implementeren u een voorbeeld van toepassing op Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="62954-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="62954-107">Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="62954-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="62954-108">U ook uitvoeren een gulp taak op uw computer toosend berichten tooEdison uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="62954-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="62954-109">Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="62954-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="62954-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="62954-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="62954-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="62954-111">What you will do</span></span>
* <span data-ttu-id="62954-112">Sluit Hallo voorbeeld toepassing tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="62954-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="62954-113">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="62954-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="62954-114">Berichten verzenden van uw IoT hub tooEdison tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="62954-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="62954-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="62954-115">What you will learn</span></span>
<span data-ttu-id="62954-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="62954-116">In this article, you will learn:</span></span>
* <span data-ttu-id="62954-117">Hoe toomonitor binnenkomende berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="62954-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="62954-118">Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooEdison.</span><span class="sxs-lookup"><span data-stu-id="62954-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="62954-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="62954-119">What you need</span></span>
* <span data-ttu-id="62954-120">Intel Edison ingesteld voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="62954-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="62954-121">hoe tooset up Edison, Zie toolearn [configureren van uw apparaat][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="62954-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="62954-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="62954-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="62954-123">toolearn hoe toocreate uw IoT-hub Zie [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="62954-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="62954-124">Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="62954-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="62954-125">Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="62954-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="62954-126">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="62954-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="62954-127">Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="62954-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="62954-128">Hallo `blinkLED` functie Hallo LED knippert.</span><span class="sxs-lookup"><span data-stu-id="62954-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing][repo-structure]
2. <span data-ttu-id="62954-130">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="62954-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="62954-131">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt Hallo stap toohello taak voor het implementeren van overslaan en Hallo-voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="62954-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="62954-132">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-edison.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="62954-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="62954-133">Hallo `config-edison.json` bestand bevindt zich in de submap Hallo van de basismap.</span><span class="sxs-lookup"><span data-stu-id="62954-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Inhoud van Hallo config edison.json bestand](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="62954-135">Vervang **[apparaat-hostnaam of IP-adres]** met Hallo apparaat IP-adres u omlaag gemarkeerd wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="62954-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="62954-136">Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="62954-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="62954-137">Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="62954-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="62954-138">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="62954-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="62954-139">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="62954-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="62954-140">Hallo gulp opdracht implementeert Hallo voorbeeld toepassing tooEdison.</span><span class="sxs-lookup"><span data-stu-id="62954-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="62954-141">Vervolgens waarop de toepassing hello Edison en een afzonderlijke taak op de host computer toosend 20 knipperen berichten tooEdison uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="62954-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="62954-142">Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="62954-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="62954-143">Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooEdison.</span><span class="sxs-lookup"><span data-stu-id="62954-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="62954-144">Voor elk bericht knipperen die Edison ontvangt, roept de voorbeeldtoepassing Hallo Hallo `blinkLED` functie tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="62954-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="62954-145">U ziet Hallo LED knipperen elke twee seconden als Hallo taak verzendt 20 berichten van uw IoT hub tooEdison gulp.</span><span class="sxs-lookup"><span data-stu-id="62954-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="62954-146">Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="62954-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="62954-148">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="62954-148">Summary</span></span>
<span data-ttu-id="62954-149">U hebt berichten uit uw IoT hub tooEdison tooblink Hallo LED verzonden.</span><span class="sxs-lookup"><span data-stu-id="62954-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="62954-150">de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="62954-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62954-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62954-151">Next steps</span></span>
<span data-ttu-id="62954-152">[Hallo in- en uitschakelen gedrag van Hallo LED wijzigen][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="62954-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md